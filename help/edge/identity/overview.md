---
title: Recuperando ID de Experience Cloud
seo-title: ID de Experience Cloud de recuperação do SDK da Web do Adobe Experience Platform
description: Saiba como obter a Adobe Experience Cloud Id.
seo-description: Saiba como obter a Adobe Experience Cloud Id.
keywords: Identidade;Identidade da Primeira Parte;Serviço de Identidade;Identidade de Terceiros;Migração de ID;ID de Visitante;identidade de terceiros;identidade de terceirosCookiesEnabled;idMigrationEnabled;getIdentity;Syncing Identidades;syncIdentity;sendEvent;identityMap;Primary;ecid;Identity Namespace;authenticationState;hashEnabled;
translation-type: tm+mt
source-git-commit: 3ac00fda2c0a43437fb212dcba7e98c63503b9c4
workflow-type: tm+mt
source-wordcount: '919'
ht-degree: 3%

---


# Identidade - Recuperando a ID do Experience Cloud

O Adobe Experience Platform Web SDK aproveita o [Adobe Identity Service](../../identity-service/ecid.md). Isso garante que cada dispositivo tenha um identificador exclusivo que seja persistente no dispositivo para que a atividade entre as páginas possa ser vinculada.

## Identidade primária

O [!DNL Identity Service] armazena a identidade em um cookie em um domínio próprio. O [!DNL Identity Service] tenta definir o cookie usando um cabeçalho HTTP no domínio. Se isso falhar, o [!DNL Identity Service] voltará para a configuração de cookies via Javascript. O Adobe recomenda que você configure um CNAME para garantir que seus cookies não sejam limitados pelas restrições ITP do lado do cliente.

## Identidade de terceiros

O [!DNL Identity Service] tem a capacidade de sincronizar uma ID com um domínio de terceiros (demdex.net) para ativar o rastreamento entre sites. Quando esta opção estiver ativada, a primeira solicitação de um visitante (por exemplo, alguém sem uma ECID) será feita para demdex.net. Isso só será feito em navegadores que permitem isso (como o Chrome) e é controlado pelo parâmetro `thirdPartyCookiesEnabled` na configuração. Se você quiser desativar esse recurso todos juntos, defina `thirdPartyCookiesEnabled` como falso.

## Migração de ID

Ao migrar da API do Visitante, você também pode migrar os cookies AMCV existentes. Para ativar a migração ECID, defina o parâmetro `idMigrationEnabled` na configuração. A migração de ID permite os seguintes casos de uso:

* Quando algumas páginas de um domínio estiverem usando a API de Visitante e outras páginas estiverem usando esse SDK. Para suportar esse caso, o SDK lê os cookies AMCV existentes e grava um novo cookie com o ECID existente. Além disso, o SDK grava cookies AMCV para que, se o ECID for obtido primeiro em uma página instrumentada com o SDK, as páginas subsequentes instrumentadas com a API do Visitante tenham o mesmo ECID.
* Quando o Adobe Experience Platform Web SDK é configurado em uma página que também tem a API do Visitante. Para suportar esse caso, se o cookie AMCV não estiver definido, o SDK procura a API do Visitante na página e a chama para obter a ECID.
* Quando todo o site estiver usando o Adobe Experience Platform Web SDK e não tiver a API do Visitante, é útil migrar as ECIDs para que as informações do visitante de retorno sejam retidas. Depois que o SDK é implantado com `idMigrationEnabled` por um período de tempo para que a maioria dos cookies do visitante seja migrada, a configuração pode ser desativada.

## Atualização de características para migração

Quando os dados formatados XDM são enviados para o Audience Manager, esses dados precisam ser convertidos em sinais ao migrar. Suas características precisarão ser atualizadas para refletir as novas teclas fornecidas pelo XDM. Esse processo é facilitado usando a [ferramenta BAAAM](https://docs.adobe.com/content/help/en/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) que o Audience Manager criou.

## Encaminhamento pelo lado do servidor

Se o encaminhamento pelo lado do servidor estiver ativado e estiver usando `appmeasurement.js`. e `visitor.js` você pode manter o recurso de encaminhamento pelo lado do servidor ativado e isso não causará problemas. No back-end, o Adobe busca todos os segmentos AAM e os adiciona à chamada para o Analytics. Se a chamada para o Analytics contiver esses segmentos, o Analytics não chamará o Audience Manager para encaminhar quaisquer dados, portanto, não há nenhuma coleta de dados do duplo. Também não há necessidade de Dica de localização ao usar o SDK da Web, pois os mesmos pontos finais de segmentação são chamados no backend.

## Recuperando a ID do Visitante

Se desejar usar essa ID exclusiva, use o comando `getIdentity`. `getIdentity` retorna o ECID existente para o visitante atual. Para visitantes que ainda não têm um ECID, este comando gera um novo ECID.

>[!NOTE]
>
>Normalmente, esse método é usado com soluções personalizadas que exigem a leitura da ID [!DNL Experience Cloud]. Ela não é usada em uma implementação padrão.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log(result.identity.ECID);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## Sincronizando identidades

>[!NOTE]
>
>O método `syncIdentity` foi removido na versão 2.1.0, além do recurso de hash. Se estiver usando a versão 2.1.0+ e quiser sincronizar identidades, você pode enviá-las diretamente na opção `xdm` do comando `sendEvent`, no campo `identityMap`.

Além disso, o [!DNL Identity Service] permite sincronizar seus próprios identificadores com o ECID usando o comando `syncIdentity`.

>[!NOTE]
>
>É altamente recomendável passar todas as identidades disponíveis em cada comando `sendEvent`. Isso desbloqueia diversos casos de uso, incluindo personalização. Agora que você pode passar essas identidades no comando `sendEvent`, elas podem ser colocadas diretamente em sua DataLayer.

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

Cada propriedade dentro de `identityMap` representa identidades pertencentes a uma determinada [namespace de identidade](../../identity-service/namespaces.md). O nome da propriedade deve ser o símbolo de namespace de identidade, que você pode encontrar listado na interface do usuário do Adobe Experience Platform em &quot;[!UICONTROL Identidades]&quot;. O valor da propriedade deve ser uma matriz de identidades pertencentes a essa namespace de identidade.

Cada objeto de identidade na matriz identidades é estruturado da seguinte maneira:

### `id`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Sim | nenhuma |

Essa é a ID que você deseja sincronizar para a namespace em questão.

### `authenticationState`

| **Tipo** | **Obrigatório** | **Valor padrão** | **Valores possíveis** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| String | Sim | ambíguo | ambíguo, autenticado e loggedOut |

O estado de autenticação da ID.

### `primary`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | opcional | false |

Determina se essa identidade deve ser usada como um fragmento principal no perfil unificado. Por padrão, o ECID é definido como o identificador principal do usuário.
