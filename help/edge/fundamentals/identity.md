---
title: Recuperando a Experience Cloud ID
seo-title: Adobe Experience Platform Web SDK para recuperação da Experience Cloud ID
description: Saiba como obter a Adobe Experience Cloud Id.
seo-description: Saiba como obter a Adobe Experience Cloud Id.
translation-type: tm+mt
source-git-commit: e9fb726ddb84d7a08afb8c0f083a643025b0f903
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 8%

---


# Recuperando a Experience Cloud ID

O Adobe Experience Platform Web SDK aproveita o serviço [de identidade da](../../identity-service/ecid.md)Adobe. Isso garante que cada dispositivo tenha um identificador exclusivo que seja persistente no dispositivo para que a atividade entre as páginas possa ser vinculada.

## Identidade da primeira parte

O serviço de ID armazena a identidade em um cookie em um domínio próprio. Os serviços de ID tentam definir o cookie usando um cabeçalho HTTP no domínio se isso falhar, o serviço de ID voltará à configuração de cookies via Javascript. A Adobe recomenda que você configure um CNAME para garantir que seus cookies não sejam limitados pelas restrições ITP do lado do cliente.

## Identidade de terceiros

Os serviços de ID têm a capacidade de sincronizar uma ID com um domínio de terceiros (demdex.net) para ativar o rastreamento no site. Quando esta opção estiver ativada, a primeira solicitação de um visitante (por exemplo, alguém sem uma ECID) será feita para demdex.net. Isso só será feito em navegadores que o permitem (por exemplo, o Chrome) e é controlado pelo `thirdPartyCookiesEnabled` parâmetro na configuração. Se você quiser desativar esse recurso, todos juntos definidos `thirdPartyCookiesEnabled` como falso.

## Recuperando a ID do Visitante

Se você quiser usar essa ID exclusiva, use o `getIdentity` comando. `getIdentity` retorna o ECID existente para o visitante atual. Para visitantes que ainda não têm um ECID, este comando gera um novo ECID.

>[!NOTE]
>
>Normalmente, esse método é usado com soluções personalizadas que exigem a leitura da Experience Cloud ID. Ela não é usada em uma implementação padrão.

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

Além disso, o Serviço de identidade permite sincronizar seus próprios identificadores com a ECID usando o `syncIdentity` comando.

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

A chave do objeto é o Símbolo de Namespace [de](../../identity-service/namespaces.md) identidade. Isso pode ser encontrado na interface do usuário da Adobe Experience Platform em Identidades.

#### `id`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| String | Sim | none |

Essa é a ID que você deseja sincronizar para a namespace em questão.

#### `primary`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | opcional | false |

Essa identidade deve ser usada como um fragmento primário no perfil unificado. Por padrão, o ECID é definido como o identificador principal do usuário.

#### `hashEnabled`

| **Tipo** | **Obrigatório** | **Valor padrão** |
| -------- | ------------ | ----------------- |
| Booleano | opcional | false |

Se ativada, hash a identidade usando hash SHA256.