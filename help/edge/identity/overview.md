---
title: Dados de identidade no SDK da Web da plataforma
description: Saiba como recuperar e gerenciar Adobe Experience Cloud IDs (ECIDs) usando o Adobe Experience Platform Web SDK.
keywords: Identidade, Identidade Primária, Serviço de Identidade, Identidade de Terceiros, Migração de ID, ID de Visitante, identidade de terceiros, thirdPartyCookiesEnabled, idMigrationEnabled, getIdentity, Identidades de Sincronização, syncIdentity, sendEvent, identityMap, primário, ecid, Namespace de Identidade, id de namespace, authenticationState, hashEnabled;
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 85ff35e0e7f7e892de5252e8f3ad069eff83aa15
workflow-type: tm+mt
source-wordcount: '1334'
ht-degree: 1%

---

# Dados de identidade no SDK da Web da plataforma

O Adobe Experience Platform Web SDK aproveita [Adobe Experience Cloud IDs (ECIDs)](../../identity-service/ecid.md) para rastrear o comportamento do visitante. Com as ECIDs, você pode garantir que cada dispositivo tenha um identificador exclusivo que possa persistir em várias sessões, vinculando todas as ocorrências que ocorrerem durante e em várias sessões da Web a um dispositivo específico.

Este documento fornece uma visão geral de como gerenciar ECIDs usando o SDK da Web da plataforma.

## Rastreamento de ECIDs usando o SDK

O SDK da Web da plataforma atribui e rastreia ECIDs por meio do uso de cookies, com vários métodos disponíveis para configurar como esses cookies são gerados.

Quando um novo usuário chega ao seu site, o Adobe Experience Cloud Identity Service tenta definir um cookie de identificação do dispositivo para esse usuário. Para visitantes pela primeira vez, uma ECID é gerada e retornada na primeira resposta da rede de borda da Adobe Experience Platform. Para visitantes repetidos, a ECID é recuperada do `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` e adicionado ao payload pela Edge Network.

Depois que o cookie contendo a ECID for definido, cada solicitação subsequente gerada pelo SDK da Web incluirá uma ECID codificada no `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie.

Ao usar cookies para identificação do dispositivo, você tem duas opções para interagir com a Edge Network:

1. Enviar dados diretamente para o domínio Rede de borda `adobedc.net`. Este método é conhecido como [coleta de dados de terceiros](#third-party).
1. Crie um CNAME em seu próprio domínio que aponte para `adobedc.net`. Este método é conhecido como [coleta de dados primários](#first-party).

Conforme explicado nas seções abaixo, o método de coleta de dados escolhido para usar tem um impacto direto na vida útil do cookie nos navegadores.

### Coleta de dados de terceiros {#third-party}

A coleta de dados de terceiros envolve o envio de dados diretamente para o domínio da rede de borda `adobedc.net`.

Nos últimos anos, os navegadores da Web têm se tornado cada vez mais restritos em sua manipulação de cookies definidos por terceiros. Alguns navegadores bloqueiam cookies de terceiros por padrão. Se você usa cookies de terceiros para identificar visitantes do site, a duração desses cookies é quase sempre menor do que a disponível caso contrário, usando cookies primários. Em alguns casos, um cookie de terceiros expirará em apenas sete dias.

Além disso, quando a coleta de dados de terceiros é usada, alguns bloqueadores de anúncios restringem o tráfego aos endpoints de coleta de dados do Adobe.

### Coleta de dados primários {#first-party}

A coleta de dados primários envolve definir cookies por meio de um CNAME em seu próprio domínio que aponta para `adobedc.net`.

Embora os navegadores tenham cookies longos tratados definidos por pontos de extremidade CNAME de maneira semelhante àqueles definidos por pontos de extremidade próprios do site, as alterações recentes implementadas pelos navegadores criaram uma distinção em como os cookies CNAME são tratados. Embora não haja navegadores que atualmente bloqueiam cookies CNAME primários por padrão, alguns navegadores restringem a vida dos cookies definidos usando um CNAME a apenas sete dias.

### Efeitos do tempo de vida do cookie em aplicativos Adobe Experience Cloud {#lifespans}

Independentemente de você escolher a coleta de dados primária ou de terceiros, o tempo em que um cookie pode persistir tem um impacto direto na contagem de visitantes no Adobe Analytics e no Customer Journey Analytics. Além disso, os usuários finais podem experimentar experiências de personalização inconsistentes quando o Adobe Target ou Offer Decisioning é usado no site.

Por exemplo, considere uma situação em que você criou uma experiência de personalização que promoverá qualquer item para a página inicial se um usuário a tiver visualizado três vezes nos últimos sete dias.

Se um usuário final visitar três vezes em uma semana e não retornar ao site por sete dias, esse uso pode ser considerado um novo usuário quando ele retornar ao site, pois seus cookies podem ter sido excluídos por uma política de navegador (dependendo do navegador usado quando visitaram o site). Se isso ocorrer, a ferramenta Analytics tratará o visitante como um novo usuário, mesmo que ele tenha visitado o site há pouco mais de sete dias. Além disso, qualquer esforço para personalizar a experiência para o usuário começará novamente.

### IDs de dispositivo próprio

Para levar em conta os efeitos do tempo de vida do cookie, conforme descrito acima, você pode optar por definir e gerenciar seus próprios identificadores de dispositivos. Consulte o guia sobre [IDs de dispositivo primário](./first-party-device-ids.md) para obter mais informações.

## Recuperar a ECID e a região do usuário atual

Para recuperar a ECID exclusiva do visitante atual, use o `getIdentity` comando. Para visitantes pela primeira vez que ainda não têm uma ECID, esse comando gera uma nova ECID. `getIdentity` também retorna a ID da região do visitante.

>[!NOTE]
>
>Normalmente, esse método é usado com soluções personalizadas que exigem a leitura da variável [!DNL Experience Cloud] ID ou precisa de uma dica de localização para o Adobe Audience Manager. Ela não é usada em uma implementação padrão.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## Usar `identityMap`

Uso de um XDM [`identityMap` campo](../../xdm/schema/composition.md#identityMap), você pode identificar um dispositivo/usuário usando várias identidades, definir seu estado de autenticação e decidir qual identificador é considerado o principal. Se nenhum identificador foi definido como `primary`, o padrão principal é `ECID`.

`identityMap` são atualizados usando a variável `sentEvent` comando.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "ambiguous",
          "primary": true
        }
      ]
    }
  }
});
```

Cada propriedade no `identityMap` representa identidades pertencentes a um [namespace de identidade](../../identity-service/namespaces.md). O nome da propriedade deve ser o símbolo do namespace de identidade, que você pode encontrar listado na interface do usuário do Adobe Experience Platform em &quot;[!UICONTROL Identidades]&quot;. O valor da propriedade deve ser uma matriz de identidades pertencentes a esse namespace de identidade.

Cada objeto de identidade na matriz de identidades contém as seguintes propriedades:

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `id` | String | **(Obrigatório)** A ID que você deseja definir para o namespace em questão. |
| `authenticationState` | String | **(Obrigatório)** O estado de autenticação da ID. Os valores possíveis são `ambiguous`, `authenticated`e `loggedOut`. |
| `primary` | Booleano | Determina se essa identidade deve ser usada como um fragmento principal no perfil. Por padrão, a ECID é definida como o identificador principal do usuário. Se for omitido, esse valor assumirá como padrão `false`. |

## Migração da API de visitante para a ECID

Ao migrar da API de visitante, você também pode migrar cookies AMCV existentes. Para habilitar a migração da ECID, defina a variável `idMigrationEnabled` na configuração. A migração de ID permite os seguintes casos de uso:

* Quando algumas páginas de um domínio estão usando a API do visitante e outras estão usando esse SDK. Para ser compatível com esse caso, o SDK lê os cookies AMCV existentes e grava um novo cookie com a ECID existente. Além disso, o SDK grava cookies AMCV para que, se a ECID for obtida primeiro em uma página instrumentada com o SDK, as páginas subsequentes instrumentadas com a API do visitante tenham a mesma ECID.
* Quando o SDK da Web da Adobe Experience Platform é configurado em uma página que também tem a API do visitante. Para ser compatível com esse caso, se o cookie AMCV não estiver definido, o SDK procura a API do visitante na página e a chama para obter a ECID.
* Quando o site inteiro estiver usando o SDK da Web da Adobe Experience Platform e não tiver a API de visitante, é útil migrar as ECIDs para que as informações de visitante de retorno sejam retidas. Depois que o SDK é implantado com `idMigrationEnabled` por um período de tempo para que a maioria dos cookies do visitante seja migrada, a configuração pode ser desativada.

### Atualização de características da migração

Quando os dados formatados do XDM são enviados para o Audience Manager, esses dados precisam ser convertidos em sinais ao migrar. Suas características precisarão ser atualizadas para refletir as novas chaves fornecidas pelo XDM. Esse processo é facilitado com o uso da variável [Ferramenta BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) esse Audience Manager criou.

## Usar no encaminhamento de eventos

Se você tiver [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) habilitado e usando `appmeasurement.js` e `visitor.js`, mantenha o recurso de encaminhamento de eventos ativado e isso não causará problemas. No back-end, o Adobe busca qualquer segmento de AAM e os adiciona à chamada para o Analytics. Se a chamada para o Analytics contiver esses segmentos, o Analytics não chamará o Audience Manager para encaminhar dados, de modo que não haja nenhuma coleta de dados dupla. Também não há necessidade de Dica de localização ao usar o SDK da Web, pois os mesmos endpoints de segmentação são chamados no back-end.
