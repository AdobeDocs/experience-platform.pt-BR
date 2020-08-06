---
title: Recuperando ID de Experience Cloud
seo-title: ID de Experience Cloud de recuperação do SDK da Web do Adobe Experience Platform
description: Saiba como obter a Adobe Experience Cloud Id.
seo-description: Saiba como obter a Adobe Experience Cloud Id.
translation-type: tm+mt
source-git-commit: d2870df230811486c09ae29bf9f600beb24fe4f8
workflow-type: tm+mt
source-wordcount: '730'
ht-degree: 5%

---


# Identidade - Recuperando a ID do Experience Cloud

A Adobe Experience Platform [!DNL Web SDK] aproveita o serviço [de identidade do](../../identity-service/ecid.md)Adobe. Isso garante que cada dispositivo tenha um identificador exclusivo que seja persistente no dispositivo para que a atividade entre as páginas possa ser vinculada.

## Identidade da primeira parte

O [!DNL Identity Service] armazena a identidade em um cookie em um domínio próprio. As [!DNL Identity Service] tentativas de definir o cookie usando um cabeçalho HTTP no domínio. Se isso falhar, a configuração dos cookies [!DNL Identity Service] voltará para o Javascript. O Adobe recomenda que você configure um CNAME para garantir que seus cookies não sejam limitados pelas restrições ITP do lado do cliente.

## Identidade de terceiros

O [!DNL Identity Service] tem a capacidade de sincronizar uma ID com um domínio de terceiros (demdex.net) para habilitar o rastreamento entre sites. Quando esta opção estiver ativada, a primeira solicitação de um visitante (por exemplo, alguém sem uma ECID) será feita para demdex.net. Isso só será feito em navegadores que o permitem (por exemplo, o Chrome) e é controlado pelo `thirdPartyCookiesEnabled` parâmetro na configuração. Se você quiser desativar esse recurso todos juntos, defina `thirdPartyCookiesEnabled` como falso.

## Migração de ID

Ao migrar da API do Visitante, você também pode migrar os cookies AMCV existentes. Para ativar a migração para ECID, defina o `idMigrationEnabled` parâmetro na configuração. A migração de ID está configurada para ativar alguns casos de uso:

* Quando algumas páginas de um domínio estiverem usando a API de Visitante e outras páginas estiverem usando esse SDK. Para suportar esse caso, o SDK lê os cookies AMCV existentes e grava um novo cookie com o ECID existente. Além disso, o SDK grava cookies AMCV para que, se o ECID for obtido primeiro em uma página instrumentada com o SDK da Web do AEP, as páginas subsequentes instrumentadas com a API do Visitante tenham a mesma ECID.
* Quando o AEP Web SDK é configurado em uma página que também tem a API do Visitante. Para suportar esse caso, se o cookie AMCV não estiver definido, o SDK procura a API do Visitante na página e a chama para obter a ECID.
* Quando todo o site estiver usando o SDK da Web AEP e não tiver a API do Visitante, é útil migrar as ECIDs para que as informações do visitante de retorno sejam mantidas. Depois que o SDK é implantado com `idMigrationEnabled` por um período de tempo para que a maioria dos cookies do visitante seja migrada, a configuração pode ser desativada.

## Recuperando a ID do Visitante

Se você quiser usar essa ID exclusiva, use o `getIdentity` comando. `getIdentity` retorna o ECID existente para o visitante atual. Para visitantes que ainda não têm um ECID, este comando gera um novo ECID.

>[!NOTE]
>
>Normalmente, esse método é usado com soluções personalizadas que exigem a leitura da [!DNL Experience Cloud] ID. Ela não é usada em uma implementação padrão.

```javascript
alloy("getIdentity")
  .then(function(result.identity.ECID) {
    // This function will get called with Adobe Experience Cloud Id when the command promise is resolved
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information
  })
```

## Sincronizando identidades

>[!NOTE]
>
>O `syncIdentity` método foi removido na versão 2.1.0, além do recurso de hash. Se você estiver usando a versão 2.1.0+ e quiser sincronizar identidades, é possível enviá-las diretamente na `xdm` opção do `sendEvent` comando, no `identityMap` campo.

Além disso, o [!DNL Identity Service] permite sincronizar seus próprios identificadores com a ECID usando o `syncIdentity` comando.

>[!NOTE]
>
>É altamente recomendável passar todas as identidades disponíveis em cada `sendEvent` comando. Isso desbloqueia diversos casos de uso, incluindo personalização. Agora que você pode passar essas identidades no `sendEvent` comando, elas podem ser colocadas diretamente em sua DataLayer.

A sincronização de identidades permite identificar um dispositivo/usuário usando várias identidades, definir seu estado de autenticação e decidir qual identificador é considerado o principal. Se nenhum identificador tiver sido definido como `primary`, o padrão principal será o `ECID`.

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
})
```


### Opções de sincronização de identidades

#### Símbolo de Namespace de identidade

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Sim | none |

A chave do objeto é o Símbolo de Namespace [de](../../identity-service/namespaces.md) identidade. Você pode encontrar isso listado na interface do usuário do Adobe Experience Platform em [!UICONTROL Identidades].

#### `id`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Sim | none |

Essa é a ID que você deseja sincronizar para a namespace em questão.

#### `authenticationState`

| **Tipo** | **Obrigatório** | **Valor padrão** | **Valores possíveis** |
| -------- | ------------ | ----------------- | ------------------------------------ |
| String | Sim | ambíguo | ambíguo, autenticado e loggedOut |

O estado de autenticação da ID.

#### `primary`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | opcional | false |

Determina se essa identidade deve ser usada como um fragmento principal no perfil unificado. Por padrão, o ECID é definido como o identificador principal do usuário.

#### `hashEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | opcional | false |

Se ativada, hash a identidade usando hash SHA256.
