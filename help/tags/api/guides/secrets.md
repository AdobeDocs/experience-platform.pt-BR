---
title: Segredos na API do Reator
description: Saiba mais sobre os fundamentos de como configurar segredos na API do Reator para uso no encaminhamento de eventos.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 2%

---

# Segredos na API do Reator

Na API do Reator, um segredo é um recurso que representa uma credencial de autenticação. Segredos são usados no encaminhamento de eventos para autenticar em outro sistema para troca segura de dados. Portanto, segredos só podem ser criados nas propriedades de encaminhamento de eventos (propriedades cujo atributo `platform` está definido como `edge`).

Atualmente, há três tipos de segredos com suporte indicados no atributo `type_of`:

| Tipo secreto | Descrição |
| --- | --- |
| `token` | Uma única cadeia de caracteres que representa um valor de token de autenticação conhecido e compreendido por ambos os sistemas. |
| `simple-http` | Contém dois atributos de string para um nome de usuário e senha, respectivamente. |
| `oauth2-client_credentials` | Contém vários atributos para oferecer suporte à especificação de autenticação [OAuth](https://datatracker.ietf.org/doc/html/rfc6749). O encaminhamento de eventos solicita as informações necessárias e, em seguida, lida com a renovação desses tokens em um intervalo especificado. |

{style="table-layout:auto"}

Este guia fornece uma visão geral de alto nível sobre como configurar segredos para usar no encaminhamento de eventos. Para obter orientação detalhada sobre como gerenciar segredos na API do Reator, incluindo o exemplo JSON da estrutura de um segredo, consulte o [manual de endpoint de segredos](../endpoints/secrets.md).

## Credenciais

Cada segredo contém um atributo `credentials` que contém seus respectivos valores de credencial. Ao [criar um segredo na API](../endpoints/secrets.md#create), cada tipo de segredo tem atributos obrigatórios diferentes, conforme mostrado nas seções abaixo:

* [&quot;token&quot;](#token)
* [&quot;simple-http&quot;](#simple-http)
* [`oauth2-client_credentials`](#oauth2-client_credentials)
* [&quot;oauth2-google&quot;](#oauth2-google)

### `token` {#token}

Segredos com um valor `type_of` de `token` exigem apenas um único atributo em `credentials`:

| Atributo de credencial | Tipo de dados | Descrição |
| --- | --- | --- |
| `token` | String | Um token secreto compreendido pelo sistema de destino. |

{style="table-layout:auto"}

O token é armazenado como um valor estático e, portanto, as propriedades `expires_at` e `refresh_at` do segredo são definidas como `null` quando o segredo é criado.

### `simple-http` {#simple-http}

Segredos com um valor `type_of` de `simple-http` exigem os seguintes atributos em `credentials`:

| Atributo de credencial | Tipo de dados | Descrição |
| --- | --- | --- |
| `username` | String | Um nome de usuário. |
| `password` | String | Uma senha. Esse valor não está incluído na resposta da API. |

{style="table-layout:auto"}

Quando o segredo é criado, os dois atributos são trocados com uma codificação BASE64 de `username:password`. Após a troca, as propriedades `expires_at` e `refresh_at` do segredo serão definidas como `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

Segredos com um valor `type_of` de `oauth2-client_credentials` exigem os seguintes atributos em `credentials`:

| Atributo de credencial | Tipo de dados | Descrição |
| --- | --- | --- |
| `client_id` | String | A ID do cliente para a integração OAuth. |
| `client_secret` | String | O segredo do cliente para a integração OAuth. Esse valor não está incluído na resposta da API. |
| `token_url` | String | O URL de autorização para a integração OAuth. |
| `refresh_offset` | Número inteiro | *(Opcional)* O valor, em segundos, para compensar a operação de atualização. Se esse atributo for omitido ao criar o segredo, o valor será definido como `14400` (quatro horas) por padrão. |
| `options` | Objeto | *(Opcional)* Especifica opções adicionais para a integração OAuth:<ul><li>`scope`: uma cadeia de caracteres que representa o [escopo do OAuth 2.0](https://oauth.net/2/scope/) para as credenciais.</li><li>`audience`: uma cadeia de caracteres que representa um [token de acesso Auth0](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

Quando um segredo `oauth2-client_credentials` é criado ou atualizado, o `client_id` e o `client_secret` (e possivelmente o `options`) são trocados em uma solicitação POST para o `token_url`, de acordo com o fluxo Credenciais de Cliente do protocolo OAuth.

>[!NOTE]
>
>Espera-se que o corpo da resposta do serviço de autorização seja compatível com o protocolo OAuth.

Se o serviço de autorização responder com `200 OK` e um corpo de resposta JSON, o corpo será analisado e `access_token` será enviado por push para o ambiente de borda e `expires_in` será usado para calcular os atributos `expires_at` e `refresh_at` do segredo. Se não houver associação de ambiente no segredo, `access_token` será descartado.

Uma troca de credenciais é considerada bem-sucedida sob as seguintes condições:

* `expires_in` é maior que `28800` (oito horas).
* `refresh_offset` é menor que o valor de `expires_in` menos `14400` (quatro horas). Por exemplo, se `expires_in` for `36000` (dez horas), e `refresh_offset` for `28800` (oito horas), a troca será considerada com falha porque `28800` é maior que `36000` - `14400` (`21600`).

Se a troca for bem-sucedida, o atributo de status do segredo é definido como `succeeded` e os valores para `expires_at` e `refresh_at` são definidos:

* `expires_at` é a hora UTC atual mais o valor de `expires_in`.
* `refresh_at` é a hora UTC atual mais o valor de `expires_in`, menos o valor de `refresh_offset`. Por exemplo, se `expires_in` for `43200` (doze horas) e `refresh_offset` for `14400` (quatro horas), a propriedade `refresh_at` será definida como `28800` (oito horas) após a hora UTC atual.

Se a troca falhar por algum motivo, o atributo `status_details` no objeto `meta` será atualizado com informações relevantes.

#### Atualizando um segredo `oauth2-client_credentials`

Se um segredo `oauth2-client_credentials` tiver sido atribuído a um ambiente e seu status for `succeeded` (as credenciais foram trocadas com êxito), uma nova troca será executada automaticamente em `refresh_at`.

Se a troca for bem-sucedida, o atributo `refresh_status` no objeto `meta` será definido como `succeeded` enquanto `expires_at`, `refresh_at` e `activated_at` forem devidamente atualizados.

Se houver falha na troca, haverá mais três tentativas com a última tentativa até não mais do que duas horas antes de o token de acesso expirar. Se todas as tentativas falharem, o atributo `refresh_status_details` do objeto `meta` será atualizado com detalhes relevantes.

### `oauth2-google` {#oauth2-google}

Segredos com um valor `type_of` de `oauth2-google` exigem o seguinte atributo em `credentials`:

| Atributo de credencial | Tipo de dados | Descrição |
| --- | --- | --- |
| `scopes` | Matriz | Lista os escopos de produto do Google para autenticação. Os seguintes escopos são compatíveis:<ul><li>[Anúncios do Google](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview) Do Google: `https://www.googleapis.com/auth/pubsub`</li></ul> |

Depois de criar o segredo `oauth2-google`, a resposta inclui uma propriedade `meta.authorization_url`. Você deve copiar e colar esse URL em um navegador para concluir o fluxo de autenticação do Google.

#### Reautorizar um segredo de `oauth2-google`

A URL de autorização para um segredo `oauth2-google` expira uma hora após a criação do segredo (conforme indicado por `meta.authorization_url_expires_at`). Após esse período, o segredo deverá ser reautorizado para renovar o processo de autenticação.

Consulte o [manual de endpoint de segredos](../endpoints/secrets.md#reauthorize) para obter detalhes sobre como reautorizar um segredo `oauth2-google` fazendo uma solicitação PATCH para a API do Reator.

## Relacionamento de ambiente

Ao criar um segredo, você deve especificar o [ambiente](../endpoints/environments.md) no qual ele existirá. Segredos são imediatamente implantados no ambiente em que são criados.

Um segredo só pode ser associado a um ambiente. Uma vez estabelecida a relação entre um segredo e um ambiente, o segredo não pode ser apagado do ambiente e o segredo não pode ser associado a um ambiente diferente.

>[!NOTE]
>
>A única exceção a essa regra é se o ambiente em questão for excluído. Nesse caso, a relação é limpa e o segredo pode ser atribuído a um ambiente diferente.

Depois que as credenciais de um segredo forem trocadas com êxito, para que um segredo seja associado a um ambiente, o artefato de troca (a cadeia de caracteres do token para `token`, a cadeia de caracteres codificada em Base64 para `simple-http` ou o token de acesso para `oauth2-client_credentials`) será salvo com segurança no ambiente.

Depois que o artefato do Exchange é salvo com êxito no ambiente, o atributo `activated_at` do segredo é definido como a hora UTC atual e agora pode ser referenciado usando um elemento de dados. Consulte a [próxima seção](#referencing-secrets) para obter mais informações sobre segredos de referência.

## Referência de segredos {#referencing-secrets}

Para referenciar um segredo, você deve criar um elemento de dados do tipo &quot;[!UICONTROL Segredo]&quot; (fornecido pela [[!UICONTROL Extensão ]](../../extensions/client/core/overview.md)) em uma propriedade de encaminhamento de eventos. Ao configurar esse elemento de dados, você será solicitado a indicar qual segredo usar para cada ambiente. Em seguida, você pode criar regras que fazem referência a um elemento de dados secreto, como no cabeçalho de uma chamada HTTP.

![Elemento de dados secreto](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Para adicionar um elemento de dados secreto a uma biblioteca, você deve ter pelo menos um segredo `succeeded` associado ao ambiente no qual a biblioteca está sendo criada. Por exemplo, se uma biblioteca tiver um elemento de dados secreto que não tenha um segredo `succeeded` configurado para a seção [!UICONTROL Segredo de Preparo], tentar criar essa biblioteca no ambiente de preparo resultará em um erro.

No tempo de execução, o elemento de dados secreto é substituído pelo artefato de troca secreta correspondente salvo no ambiente.

## Próximas etapas

Este guia abordou os fundamentos do trabalho com segredos na API do Reator. Para obter detalhes sobre como gerenciar segredos usando chamadas de API, consulte o [manual de endpoint de segredos](../endpoints/secrets.md).
