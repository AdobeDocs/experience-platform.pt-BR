---
title: Dados de identidade no SDK da Web
description: Saiba como recuperar e gerenciar Adobe Experience Cloud IDs (ECIDs) usando o SDK da Web da Adobe Experience Platform.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: b8c38108e7481a5c4e94e4122e0093fa6f00b96c
workflow-type: tm+mt
source-wordcount: '1481'
ht-degree: 0%

---

# Dados de identidade no SDK da Web

O Adobe Experience Platform Web SDK usa [Adobe Experience Cloud IDs (ECIDs)](../../identity-service/features/ecid.md) para rastrear o comportamento do visitante. Usando ECIDs, você pode garantir que cada dispositivo tenha um identificador exclusivo que possa persistir em várias sessões, vinculando todas as ocorrências que ocorrem durante e entre sessões da Web a um dispositivo específico.

Este documento fornece uma visão geral de como gerenciar ECIDs usando o SDK da Web da plataforma.

## Rastreamento de ECIDs usando o SDK

O SDK da Web da Platform atribui e rastreia ECIDs usando cookies, com vários métodos disponíveis para configurar como esses cookies são gerados.

Quando um novo usuário chega ao seu site, o Serviço de identidade da Adobe Experience Cloud tenta definir um cookie de identificação de dispositivo para esse usuário. Para visitantes novos, uma ECID é gerada e retornada na primeira resposta do Edge Network Adobe Experience Platform. Para visitantes repetidos, a ECID é recuperada do `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` e adicionado à carga pelo Edge Network.

Depois que o cookie que contém a ECID for definido, cada solicitação subsequente gerada pelo SDK da Web incluirá uma ECID codificada na `kndctr_{YOUR-ORG-ID}_AdobeOrg_identity` cookie.

Ao usar cookies para identificação de dispositivo, você tem duas opções para interagir com o Edge Network:

1. Enviar dados diretamente para o domínio Edge Network `adobedc.net`. Esse método é conhecido como [coleta de dados de terceiros](#third-party).
1. Crie um CNAME em seu próprio domínio que aponte para `adobedc.net`. Esse método é conhecido como [coleta de dados primários](#first-party).

Conforme explicado nas seções abaixo, o método de coleta de dados que você escolhe usar tem um impacto direto na vida útil do cookie nos navegadores.

### Coleta de dados de terceiros {#third-party}

A coleta de dados de terceiros envolve o envio de dados diretamente para o domínio Edge Network `adobedc.net`.

Nos últimos anos, os navegadores da Web têm se tornado cada vez mais restritivos no manuseio de cookies definidos por terceiros. Alguns navegadores bloqueiam cookies de terceiros por padrão. Se você usar cookies de terceiros para identificar visitantes do site, a vida útil desses cookies é quase sempre mais curta do que o que estaria disponível usando cookies primários. Às vezes, um cookie de terceiros expira em apenas sete dias.

Além disso, quando a coleta de dados de terceiros é usada, alguns bloqueadores de anúncios restringem o tráfego aos endpoints de coleta de dados do Adobe.

### Coleta de dados primários {#first-party}

A coleta de dados primários envolve a configuração de cookies por meio de um CNAME em seu próprio domínio que aponta para `adobedc.net`.

Embora os navegadores tenham durante muito tempo tratado os cookies definidos por endpoints CNAME de maneira semelhante aos definidos por endpoints pertencentes ao site, as alterações recentes implementadas pelos navegadores criaram uma distinção em como os cookies CNAME são tratados. Embora não haja navegadores que atualmente bloqueiam cookies próprios CNAME por padrão, alguns navegadores restringem a duração dos cookies definidos usando um CNAME para apenas sete dias.

### Efeitos da duração do cookie em aplicativos Adobe Experience Cloud {#lifespans}

Independentemente de você escolher a coleta de dados própria ou de terceiros, o tempo em que um cookie pode persistir tem um impacto direto na contagem de visitantes no Adobe Analytics e no Customer Journey Analytics. Além disso, os usuários finais podem experimentar experiências de personalização inconsistentes quando o Adobe Target ou o Offer Decisioning são usados no site.

Por exemplo, considere uma situação em que você criou uma experiência de personalização que promove qualquer item para a página inicial se um usuário o visualizou três vezes nos últimos sete dias.

Se um usuário final visitar três vezes por semana e não retornar ao site por sete dias, ele poderá ser considerado um novo usuário quando retornar ao site, pois seus cookies podem ter sido excluídos por uma política do navegador (dependendo do navegador usado quando visitou o site). Se isso ocorrer, a ferramenta do Analytics tratará o visitante como um novo usuário, embora ele tenha visitado o site há pouco mais de sete dias. Além disso, qualquer esforço para personalizar a experiência do usuário começa novamente.

### IDs de dispositivo próprio

Para levar em conta os efeitos da duração do cookie conforme descrito acima, você pode optar por definir e gerenciar seus próprios identificadores de dispositivo. Consulte o guia sobre [IDs de dispositivo primário](./first-party-device-ids.md) para obter mais informações.

## Recuperar a ECID e a região do usuário atual {#retrieve-ecid}

Dependendo do caso de uso, há duas maneiras de acessar a variável [!DNL ECID]:

* [Recuperar o [!DNL ECID] por meio do Preparo de dados para a coleção de dados](#retrieve-ecid-data-prep): este é o método recomendado que você deve usar.
* [Recuperar o [!DNL ECID] por meio da `getIdentity()` comando](#retrieve-ecid-getidentity): use esse método somente quando precisar da variável [!DNL ECID] informações no lado do cliente.

### Recuperar o [!DNL ECID] por meio do Preparo de dados para a coleção de dados {#retrieve-ecid-data-prep}

Uso [Preparação de dados para coleção de dados](../../datastreams/data-prep.md) para mapear o [!DNL ECID] para um [!DNL XDM] campo. Essa é a maneira recomendada de acessar o [!DNL ECID].

Para fazer isso, defina o campo de origem para o seguinte caminho:

```js
xdm.identityMap.ECID[0].id
```

Em seguida, defina o campo de destino como um caminho XDM, onde o campo é do tipo `string`.

![](../../tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### Recuperar o [!DNL ECID] por meio da `getIdentity()` comando {#retrieve-ecid-getidentity}


>[!IMPORTANT]
>
>Você só deve recuperar a ECID por meio da `getIdentity()` se você precisar de uma [!DNL ECID] no lado do cliente. Se desejar mapear apenas a ECID para um campo XDM, use [Preparação de dados para coleção de dados](#retrieve-ecid-data-prep) em vez disso.

Para recuperar o ECID exclusivo para o visitante atual, use o `getIdentity` comando. Para visitantes novos que não têm uma [!DNL ECID] ainda assim, esse comando gera um novo [!DNL ECID]. `getIdentity` também retorna a ID da região do visitante.

>[!NOTE]
>
>Normalmente, esse método é usado com soluções personalizadas que exigem a leitura da [!DNL Experience Cloud] ID ou é necessária uma dica de localização do Adobe Audience Manager. Ela não é usada em uma implementação padrão.

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

## Usar `identityMap` {#using-identitymap}

Uso de um XDM [`identityMap` campo](../../xdm/schema/composition.md#identityMap), você pode identificar um dispositivo/usuário usando várias identidades, definir seu estado de autenticação e decidir qual identificador é considerado o principal. Se nenhum identificador foi definido como `primary`, o padrão principal será `ECID`.

`identityMap` Os campos são atualizados usando o `sentEvent` comando.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>A Adobe recomenda enviar namespaces que representam uma pessoa, como `CRMID`, como a identidade principal.


Cada propriedade dentro de `identityMap` representa identidades pertencentes a um determinado [namespace de identidade](../../identity-service/features/namespaces.md). O nome da propriedade deve ser o símbolo de namespace de identidade, que pode ser encontrado listado na interface do usuário do Adobe Experience Platform em &quot;[!UICONTROL Identidades]&quot;. O valor da propriedade deve ser uma matriz de identidades pertencentes a esse namespace de identidade.

>[!IMPORTANT]
>
>A ID do namespace transmitida na variável `identityMap` O diferencia maiúsculas e minúsculas. Use a ID de namespace correta para evitar uma coleta de dados incompleta.

Cada objeto de identidade na matriz de identidades contém as seguintes propriedades:

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `id` | String | **(Obrigatório)** A ID que você deseja definir para o namespace fornecido. |
| `authenticationState` | String | **(Obrigatório)** O estado de autenticação da ID. Os valores possíveis são `ambiguous`, `authenticated`, e `loggedOut`. |
| `primary` | Booleano | Determina se essa identidade deve ser usada como um fragmento primário no perfil. Por padrão, a ECID é definida como o identificador principal do usuário. Se omitido, esse valor assumirá como padrão `false`. |

Usar o `identityMap` para identificar dispositivos ou usuários leva ao mesmo resultado que o uso de [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) método do [!DNL ID Service API]. Consulte a [Documentação da API do serviço de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html) para obter mais detalhes.

## Migração da API do visitante para ECID

Ao migrar do usando a API do visitante, também é possível migrar os cookies AMCV existentes. Para habilitar a migração ECID, defina o `idMigrationEnabled` parâmetro na configuração. A migração de ID habilita os seguintes casos de uso:

* Quando algumas páginas de um domínio estão usando a API de visitante e outras páginas estão usando esse SDK. Para dar suporte a esse caso, o SDK lê os cookies AMCV existentes e grava um novo cookie com a ECID existente. Além disso, o SDK grava cookies AMCV para que, se a ECID for obtida primeiro em uma página instrumentada com o SDK, as páginas subsequentes instrumentadas com a API do visitante terão a mesma ECID.
* Quando o Adobe Experience Platform Web SDK é configurado em uma página que também tem a API do visitante. Para dar suporte a esse caso, se o cookie AMCV não estiver definido, o SDK procurará a API do visitante na página e a chamará para obter a ECID.
* Quando o site inteiro estiver usando o SDK da Web da Adobe Experience Platform e não tiver uma API de visitante, é útil migrar as ECIDs para que as informações do visitante retornadas sejam mantidas. Depois que o SDK for implantado com `idMigrationEnabled` por um momento para que a maioria dos cookies do visitante seja migrada, a configuração pode ser desativada.

### Atualização de características para migração

Quando dados formatados em XDM são enviados para o Audience Manager, esses dados devem ser convertidos em sinais ao migrar. Suas características devem ser atualizadas para refletir as novas chaves que o XDM fornece. Esse processo é facilitado com o uso do [Ferramenta BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) que o Audience Manager criou.

## Usar no encaminhamento de eventos

Se você tiver [encaminhamento de eventos](../../tags/ui/event-forwarding/overview.md) ativado e está usando `appmeasurement.js` e `visitor.js`, você pode manter o recurso de encaminhamento de eventos ativado e isso não causará problemas. No back-end, o Adobe busca segmentos AAM e os adiciona à chamada para o Analytics. Se a chamada para o Analytics contiver esses segmentos, o Analytics não chamará o Audience Manager para encaminhar dados, portanto, não há nenhuma coleta de dados dupla. Também não há necessidade de Dica de localização ao usar o SDK da Web, pois os mesmos pontos de extremidade de segmentação são chamados no back-end.
