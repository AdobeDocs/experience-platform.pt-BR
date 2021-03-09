---
title: Recuperar Experience Cloud IDs usando o SDK da Web da Adobe Experience Platform
description: Saiba como recuperar Adobe Experience Cloud IDs (ECIDs) usando o SDK da Web da Adobe Experience Platform.
seo-description: Saiba Como Obter A Adobe Experience Cloud Id.
keywords: Identidade, Identidade Primária, Serviço de Identidade, Identidade de Terceiros, Migração de ID, ID de Visitante, identidade de terceiros, thirdPartyCookiesEnabled, idMigrationEnabled, getIdentity, Identidades de Sincronização, syncIdentity, sendEvent, identityMap, primário, ecid, Namespace de Identidade, id de namespace, authenticationState, hashEnabled;
translation-type: tm+mt
source-git-commit: 882bcd2f9aa7a104270865783eed82089862dea3
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 3%

---


# Recuperar Adobe Experience Cloud IDs

O SDK da Web da Adobe Experience Platform aproveita o [Adobe Identity Service](../../identity-service/ecid.md). Isso garante que cada dispositivo tenha um identificador exclusivo que seja mantido no dispositivo para que a atividade entre páginas possa ser vinculada.

## Identidade própria

O [!DNL Identity Service] armazena a identidade em um cookie em um domínio próprio. O [!DNL Identity Service] tenta definir o cookie usando um cabeçalho HTTP no domínio. Se isso falhar, o [!DNL Identity Service] voltará à configuração de cookies por meio do Javascript. A Adobe recomenda configurar um CNAME para garantir que os cookies não sejam limitados por restrições de ITP do lado do cliente.

## Identidade de terceiros

O [!DNL Identity Service] tem a capacidade de sincronizar uma ID com um domínio de terceiros (demdex.net) para ativar o rastreamento entre sites. Quando isso estiver ativado, a primeira solicitação de um visitante (por exemplo, alguém sem uma ECID) será feita para demdex.net. Isso só será feito em navegadores que permitem (como o Chrome) e é controlado pelo parâmetro `thirdPartyCookiesEnabled` na configuração. Se quiser desativar esse recurso completamente, defina `thirdPartyCookiesEnabled` como falso.

## Migração de ID

Ao migrar da API de visitante, você também pode migrar cookies AMCV existentes. Para habilitar a migração da ECID, defina o parâmetro `idMigrationEnabled` na configuração. A migração de ID permite os seguintes casos de uso:

* Quando algumas páginas de um domínio estão usando a API do visitante e outras estão usando esse SDK. Para ser compatível com esse caso, o SDK lê os cookies AMCV existentes e grava um novo cookie com a ECID existente. Além disso, o SDK grava cookies AMCV para que, se a ECID for obtida primeiro em uma página instrumentada com o SDK, as páginas subsequentes instrumentadas com a API do visitante tenham a mesma ECID.
* Quando o SDK da Web da Adobe Experience Platform é configurado em uma página que também tem a API do visitante. Para ser compatível com esse caso, se o cookie AMCV não estiver definido, o SDK procura a API do visitante na página e a chama para obter a ECID.
* Quando todo o site estiver usando o SDK da Web da Adobe Experience Platform e não tiver a API de visitante, é útil migrar as ECIDs para que as informações de visitante de retorno sejam retidas. Depois que o SDK é implantado com `idMigrationEnabled` por um período de tempo para que a maioria dos cookies do visitante seja migrada, a configuração pode ser desativada.

## Atualização de características da migração

Quando dados formatados em XDM são enviados para o Audience Manager, esses dados precisam ser convertidos em sinais ao migrar. Suas características precisarão ser atualizadas para refletir as novas chaves fornecidas pelo XDM. Esse processo é facilitado usando a [ferramenta BAAAM](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) que o Audience Manager criou.

## Encaminhamento pelo lado do servidor

Se você tiver o encaminhamento pelo lado do servidor habilitado e estiver usando `appmeasurement.js`. e `visitor.js` você pode manter o recurso de encaminhamento pelo lado do servidor habilitado e isso não causará problemas. No back-end, a Adobe busca qualquer segmento do AAM e os adiciona à chamada para o Analytics. Se a chamada para o Analytics contiver esses segmentos, o Analytics não chamará o Audience Manager para encaminhar dados, de modo que não há coleta de dados duplicada. Também não há necessidade de Dica de localização ao usar o SDK da Web, pois os mesmos endpoints de segmentação são chamados no back-end.

## Recuperar a ID de visitante e a ID de região

Se quiser usar a ID de visitante exclusiva, use o comando `getIdentity`. `getIdentity` retorna a ECID existente para o visitante atual. Para visitantes pela primeira vez que ainda não têm uma ECID, esse comando gera uma nova ECID. `getIdentity` também retorna a ID da região do visitante. Consulte o [Guia do usuário do Adobe Audience Manager](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html) para obter mais informações.

>[!NOTE]
>
>Normalmente, esse método é usado com soluções personalizadas que exigem a leitura da ID [!DNL Experience Cloud] ou precisam da dica de localização do Adobe Audience Manager. Ela não é usada em uma implementação padrão.

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

## Sincronização de identidades

>[!NOTE]
>
>O método `syncIdentity` foi removido na versão 2.1.0, além do recurso de hash. Se estiver usando a versão 2.1.0+ e quiser sincronizar identidades, é possível enviá-las diretamente na opção `xdm` do comando `sendEvent`, no campo `identityMap`.

Além disso, o [!DNL Identity Service] permite sincronizar seus próprios identificadores com a ECID usando o comando `syncIdentity`.

>[!NOTE]
>
>É altamente recomendável transmitir todas as identidades disponíveis em cada comando `sendEvent`. Isso desbloqueia uma variedade de casos de uso, incluindo personalização. Agora que você pode passar essas identidades no comando `sendEvent`, elas podem ser colocadas diretamente em seu DataLayer.

A sincronização de identidades permite identificar um dispositivo/usuário usando várias identidades, definir seu estado de autenticação e decidir qual identificador é considerado o principal. Se nenhum identificador tiver sido definido como `primary`, o padrão principal será `ECID`.

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

Cada propriedade dentro de `identityMap` representa identidades pertencentes a um [namespace de identidade](../../identity-service/namespaces.md) específico. O nome da propriedade deve ser o símbolo do namespace de identidade, que pode ser encontrado listado na interface do usuário da Adobe Experience Platform em &quot;[!UICONTROL Identities]&quot;. O valor da propriedade deve ser uma matriz de identidades pertencentes a esse namespace de identidade.

Cada objeto de identidade na matriz de identidades é estruturado da seguinte maneira:

### `id`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Sim | nenhuma |

Essa é a ID que você deseja sincronizar para o namespace em questão.

### `authenticationState`

| **Tipo** | **Obrigatório** | **Valor padrão** | **Valores possíveis** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| String | Sim | ambíguo | ambíguo, autenticado e loggedOut |

O estado de autenticação da ID.

### `primary`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | opcional | false |

Determina se essa identidade deve ser usada como um fragmento principal no perfil unificado. Por padrão, a ECID é definida como o identificador principal do usuário.
