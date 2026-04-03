---
title: Uso do identityMap na coleção de dados
description: Saiba como criar e enviar cargas do identityMap para identificar visitantes conhecidos em namespaces na implementação do Web SDK.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 0%

---

# Uso do identityMap na coleção de dados

O objeto de carga `identityMap` é como você informa à Edge Network quem um visitante está além da [ECID](./overview.md) de nível de dispositivo. Quando um visitante faz logon, conclui uma compra ou se torna conhecido de alguma outra forma, você pode enviar identificadores de nível de pessoa (ID de CRM, email com hash, ID de fidelidade etc.) juntamente com a ECID. Esses identificadores de nível de pessoa fornecem informações valiosas para serviços downstream para que possam:

* **Associe a atividade a uma pessoa em dispositivos e canais.O** [Serviço de Identidade](/help/identity-service/home.md) vincula as identidades enviadas para um [gráfico de identidade](/help/identity-service/features/identity-graph-viewer.md), conectando o comportamento anônimo no nível do dispositivo a uma pessoa conhecida.
* **Crie perfis unificados de clientes.** O [Perfil de cliente em tempo real](/help/profile/home.md) usa a identidade principal definida para ancorar eventos e atributos em um único perfil, permitindo a segmentação em nível de pessoa e a criação de público-alvo.
* **Ativar públicos-alvo em destinos downstream.** Muitos [Destinos](/help/destinations/home.md) exigem identidades de nível de pessoa resolvidas (emails com hash, números de telefone etc.) para corresponder seus públicos-alvo às suas bases de usuários.
* **Orquestrar jornadas entre canais.O** [Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/ajo-home.html?lang=pt-BR) usa identidades resolvidas para acionar e personalizar jornadas em canais de email, push e no aplicativo com base no comportamento autenticado de um visitante.

Esta página aborda como construir cargas do `identityMap`, escolher as configurações corretas para cada identidade e lidar com cenários comuns de implementação.

## Estrutura de carga útil {#structure}

O `identityMap` é um objeto JSON em que cada chave de nível superior é um namespace e o valor é uma matriz de descritores de identidade. Você pode incluir um ou mais namespaces em uma única carga, e cada descritor contém três campos: `id`, `authenticatedState` e `primary`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

| Campo | Tipo | Obrigatório | Descrição |
| --- | --- | --- | --- |
| `id` | String | Sim | O valor do identificador (por exemplo, `user@example.com` ou `ABC123`). |
| `authenticatedState` | String | Sim | Com que confiança você sabe que essa identidade pertence ao visitante. Os valores válidos incluem `ambiguous`, `authenticated` e `loggedOut`. |
| `primary` | Booleano | Sim | Se essa identidade deve ser o identificador principal do evento. Exatamente uma identidade em todos os namespaces deve ser marcada `primary: true`. |

As seções abaixo abordam cada parte do conteúdo em detalhes.

### Chaves de namespace {#namespace-keys}

Cada chave de nível superior em `identityMap` é um [namespace de identidade](/help/identity-service/features/namespaces.md) — uma cadeia que classifica o tipo de identificador (por exemplo, `CRMID`, `Email`, `Phone` ou `LoyaltyId`). Os namespaces devem existir no Serviço de identidade antes de você referenciá-los em uma carga. Você pode incluir várias chaves de namespace no mesmo evento quando tiver mais de um identificador para o visitante.

Não é necessário incluir a ECID como uma chave de namespace. O Edge Network adiciona automaticamente a ECID à carga da identidade. Se você incluir a ECID explicitamente, não marque-a como `primary` quando uma identidade de nível de pessoa também estiver presente.

### `id` {#id}

O campo `id` é a própria cadeia de caracteres do identificador — o valor que informa ao Experience Platform qual pessoa ou dispositivo específico essa identidade representa. Cada [namespace de identidade](/help/identity-service/features/namespaces.md) espera um formato de valor específico, e o envio de um valor no formato errado cria uma identidade distinta que não pode ser mesclada com a versão formatada corretamente, resultando em perfis fragmentados.

Antes de incluir um valor em `identityMap`, prepare-o de acordo com o formato que o namespace de destino espera:

| Tipos de namespace comuns | Como preparar o valor | Exemplo |
| --- | --- | --- |
| **ID interno/CRM** | Use o identificador exato atribuído pelo sistema de registro. Mantenha o formato consistente em todos os eventos (letras maiúsculas e minúsculas, zeros à esquerda, prefixos). | `ABC-12345`, `00098765` |
| **Email (bruto)** | Reduza o endereço de email completo e elimine os espaços em branco à esquerda e à direita. | `user@example.com` |
| **Email (com hash)** | Reduza as letras minúsculas e corte o endereço de email primeiro e, em seguida, use o hash com SHA-256. Envie a sequência hexadecimal de 64 caracteres resultante. Não adicione um salt, a menos que a definição do namespace exija um salt. | `a1b2c3d4e5f6a7b8c9...` |
| **Telefone (E.164)** | Formate o número em [E.164](https://en.wikipedia.org/wiki/E.164): um `+` à esquerda, o código do país e o número do assinante sem espaços ou pontuação. | `+15551234567` |
| **FPID** | Gerar uma cadeia de caracteres [UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). Consulte [IDs de dispositivo próprio](./fpid.md) para obter os requisitos de geração. | `123e4567-e89b-42d3-9456-426614174000` |

Para obter a lista completa de namespaces padrão e suas definições, consulte [Visão geral do namespace de identidade](/help/identity-service/features/namespaces.md#standard).

>[!TIP]
>
>O valor `id` diferencia maiúsculas de minúsculas. `User@Example.com` e `user@example.com` são tratados como duas identidades separadas. Normalize a capitalização antes de enviar o valor (geralmente ao reduzir o email e cortar espaços em branco) para evitar a criação de identidades duplicadas no gráfico.

#### Coletando `id` no tempo de execução {#collect-id}

O identificador necessário raramente está disponível diretamente na página. As estratégias comuns de coleta incluem:

* **Camada de dados**: leia o identificador na camada de dados do site depois que o visitante entrar. Esse local é a abordagem mais confiável, pois a camada de dados é preenchida pelo back-end do aplicativo e reflete o estado da sessão autenticada.
* **Token de autenticação ou cookie de sessão**: decodifique ou procure o identificador a partir de um cookie JWT ou de sessão definido pelo seu sistema de autenticação. Valide se o token ainda está ativo antes de usar o valor.
* **Enriquecimento do lado do servidor**: use o [Preparo de Dados para a Coleção de Dados](/help/datastreams/data-prep.md) ou uma [regra de encaminhamento de eventos](/help/tags/ui/event-forwarding/overview.md) para mapear ou transformar o identificador na Edge antes que ele atinja os serviços downstream. Esse local é útil quando o cliente tem apenas um token de sessão opaco que mapeia para uma ID interna no lado do servidor.

>[!TIP]
>
>Se determinado valor `id` for resolvido como uma cadeia de caracteres vazia, `null` ou `undefined`, não inclua o namespace em `identityMap`. Enviar um `id` vazio cria um registro de identidade corrompido. Proteja sua implementação com uma verificação antes de criar a carga.

### `authenticatedState` {#authenticated-state}

O campo `authenticatedState` informa aos serviços downstream quanta confiança colocar em uma determinada identidade. Os seguintes valores são válidos para este campo:

| Valor | Quando usar |
| --- | --- |
| **`authenticated`** | O visitante provou ativamente sua identidade durante a sessão atual (por exemplo, fazendo logon com credenciais, concluindo o MFA ou verificação semelhante). |
| **`loggedOut`** | O visitante foi autenticado anteriormente, mas saiu. A identidade ainda está associada ao dispositivo, mas a sessão não está mais ativa. |
| **`ambiguous`** | A identidade não pode ser confirmada como pertencente ao visitante atual. Use esse valor para identificadores no nível do dispositivo, como FPIDs ou qualquer identificador que ainda não tenha ocorrido. |

>[!TIP]
>
>O valor `authenticatedState` afeta como o Adobe Experience Platform Identity Service compila e mescla gráficos de identidade. Enviar `authenticated` para uma identidade que não foi verificada pode criar links entre dispositivos incorretos que são difíceis de desfazer.

### `primary` {#primary-identity}

Toda carga de `identityMap` deve ter exatamente uma identidade marcada como `primary: true`. A identidade principal determina qual identidade é usada como âncora para o evento no Experience Platform.

Siga estas diretrizes ao definir a identidade principal:

* **Quando uma identidade de nível de pessoa estiver disponível** (o visitante está conectado), marque o namespace de nível de pessoa como principal e a ECID como não principal. Isso instrui o Experience Platform a ancorar o evento na pessoa, em vez do dispositivo.
* **Quando apenas identidades no nível do dispositivo estão disponíveis** (o visitante é anônimo), a ECID é usada automaticamente como a identidade principal. Não é necessário incluir a ECID no `identityMap` — a Edge Network a adiciona automaticamente.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

## Envio do identityMap na implementação {#send-identity}

>[!BEGINTABS]

>[!TAB biblioteca JavaScript]

Passar o `identityMap` no objeto `xdm` de uma chamada [`sendEvent`](/help/collection/js/commands/sendevent/overview.md):

```js
alloy("sendEvent", {
  xdm: {
    identityMap: {
      CRMID: [
        {
          id: "abc-123-xyz",
          authenticatedState: "authenticated",
          primary: true
        }
      ]
    },
    eventType: "web.webpagedetails.pageViews"
  }
});
```

>[!TAB Extensão de tag do Web SDK]

Use o tipo de elemento de dados [Mapa de identidade](/help/tags/extensions/client/web-sdk/data-element-types.md#identity-map) para criar sua carga de identidade na interface de marcas:

1. Crie um elemento de dados com a extensão **[!UICONTROL Adobe Experience Platform Web SDK]** e o tipo de elemento de dados **[!UICONTROL Identity map]**.
2. Adicione identidades especificando o namespace, o elemento de dados ou o valor que é resolvido para o identificador e o estado autenticado.
3. Marcar uma identidade como primária.
4. Referencie este elemento de dados na sua ação **[!UICONTROL Send event]** em **[!UICONTROL Identity map]**.

>[!ENDTABS]

## Cenários comuns {#common-scenarios}

+++**Logon**

Quando um visitante entrar, envie seu identificador de nível de pessoa com `authenticatedState: "authenticated"` e `primary: true`. Inclua essa identidade no primeiro evento após a autenticação e em todos os eventos subsequentes na sessão.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

+++

+++**Logoff**

Quando um visitante sair, atualizar `authenticatedState` para `loggedOut` mantendo o mesmo identificador. Isso preserva a associação entre o dispositivo e a pessoa enquanto sinaliza que a sessão não está mais ativa.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "loggedOut",
        "primary": false
      }
    ]
  }
}
```

Após o logout, a ECID volta a ser a identidade principal efetiva (a Edge Network a aplica automaticamente). Não marque uma identidade diferente no nível da pessoa como primária, a menos que o visitante entre com uma conta diferente.

>[!IMPORTANT]
>
>Não pare de enviar o identificador totalmente após o logout. Alternar de `authenticated` para `loggedOut` informa aos serviços downstream que a sessão foi encerrada. A omissão do identificador deixa uma lacuna no gráfico de identidade que pode causar perfis fragmentados.

+++

+++**Vários namespaces**

Você pode enviar vários namespaces de identidade no mesmo evento. Esse cenário é comum quando um visitante está conectado e você tem vários identificadores disponíveis (por exemplo, uma ID de CRM, um email com hash e uma ID de fidelidade). Inclua todos os identificadores conhecidos, marque apenas um como primário e defina os outros como `primary: false`.

```json
{
  "identityMap": {
    "CRMID": [
      {
        "id": "abc-123-xyz",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ],
    "Email_LC_SHA256": [
      {
        "id": "a1b2c3d4e5f6...",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ],
    "LoyaltyId": [
      {
        "id": "LOY-98765",
        "authenticatedState": "authenticated",
        "primary": false
      }
    ]
  }
}
```

>[!TIP]
>
>O envio de vários namespaces com o mesmo `authenticatedState` no mesmo evento fornece ao Serviço de Identidade o sinal mais forte para vincular essas identidades. Inclua todos os identificadores disponíveis no ponto de autenticação, em vez de espalhá-los em eventos separados.

+++

+++**Visitantes anônimos**

Para visitantes anônimos, normalmente não é necessário enviar nenhum `identityMap`. O Edge Network atribui automaticamente uma ECID e a usa como a identidade principal. Se você usa [IDs de dispositivo próprio](./fpid.md), o FPID é a única identidade que você precisa incluir para visitantes anônimos.

+++

## Como o identityMap afeta o gráfico de identidade {#identity-graph}

Toda carga do `identityMap` que chega à Experience Platform é processada pelo [Serviço de Identidade](/help/identity-service/home.md), que vincula as identidades enviadas a um [gráfico de identidade](/help/identity-service/features/identity-graph-viewer.md). Os namespaces que você inclui, como você define `authenticatedState` e qual identidade você marca como `primary`, moldam diretamente como o Serviço de Identidade cria e mescla esses gráficos.

Comportamentos principais a serem observados:

* **As identidades enviadas no mesmo evento são vinculadas.** Se você incluir um CRMID e um namespace de email na mesma chamada `sendEvent`, o Serviço de Identidade criará um vínculo entre essas duas identidades. A disseminação de identificadores em eventos separados produz links mais fracos e pode resultar em gráficos fragmentados.
* **A identidade `primary` ancora o evento no Perfil de Cliente em Tempo Real.** O perfil usa a identidade principal para determinar a qual perfil o evento pertence. Marcar a identidade errada como primária (por exemplo, definir a ECID como primária quando uma ID de nível de pessoa estiver disponível) pode fazer com que os eventos sejam armazenados em perfis de nível de dispositivo, em vez de perfis de nível de pessoa.
* **O `authenticatedState` influencia a confiança do gráfico.** Enviar `authenticated` para uma identidade que não foi realmente verificada pode criar links incorretos entre dispositivos que são difíceis de desfazer. Use `authenticated` somente quando o visitante tiver provado ativamente sua identidade durante a sessão atual.

Se sua implementação usar [regras de vinculação de gráficos de identidade](/help/identity-service/identity-graph-linking-rules/overview.md) (como a prioridade de namespace ou o algoritmo de otimização de identidade), revise o [guia de implementação](/help/identity-service/identity-graph-linking-rules/implementation-guide.md) para entender como essas regras interagem com as identidades enviadas por meio do `identityMap`.

>[!NOTE]
>
>O `identityMap` só é enviado quando o Web SDK faz uma solicitação à Edge Network, que é fechada pelo estado de consentimento do visitante. Se sua implementação usar `defaultConsent: "pending"`, as identidades não serão enviadas até que o consentimento seja concedido. Consulte [Consentimento e identidade](./consent.md) para obter detalhes.
