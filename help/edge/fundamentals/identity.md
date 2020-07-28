---
title: Recuperando ID de Experience Cloud
seo-title: Adobe Experience Platform Web SDK Recuperando Experience Cloud ID
description: Saiba como obter a Adobe Experience Cloud Id.
seo-description: Saiba como obter a Adobe Experience Cloud Id.
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 10%

---


# Identidade - Recuperando a ID do Experience Cloud

O Adobe Experience Platform [!DNL Web SDK] aproveita o serviço [de identidade do](../../identity-service/ecid.md)Adobe. Isso garante que cada dispositivo tenha um identificador exclusivo que seja persistente no dispositivo para que a atividade entre as páginas possa ser vinculada.

## Identidade da primeira parte

O [!DNL Identity Service] armazena a identidade em um cookie em um domínio próprio. As [!DNL Identity Service] tentativas de definir o cookie usando um cabeçalho HTTP no domínio. Se isso falhar, a configuração dos cookies [!DNL Identity Service] voltará para o Javascript. O Adobe recomenda que você configure um CNAME para garantir que seus cookies não sejam limitados pelas restrições ITP do lado do cliente.

## Identidade de terceiros

O [!DNL Identity Service] tem a capacidade de sincronizar uma ID com um domínio de terceiros (demdex.net) para habilitar o rastreamento entre sites. Quando esta opção estiver ativada, a primeira solicitação de um visitante (por exemplo, alguém sem uma ECID) será feita para demdex.net. Isso só será feito em navegadores que o permitem (por exemplo, o Chrome) e é controlado pelo `thirdPartyCookiesEnabled` parâmetro na configuração. Se você quiser desativar esse recurso todos juntos, defina `thirdPartyCookiesEnabled` como falso.

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

Além disso, o [!DNL Identity Service] permite sincronizar seus próprios identificadores com a ECID usando o `syncIdentity` comando.

```javascript
alloy("syncIdentity",{
    identity:{
      "AppNexus":{
        "id":"123456,
        "authenticationState":"ambiguous",
        "primary":false,
        "hashEnabled": true,
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
