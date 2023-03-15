---
title: Segredos na API do Reator
description: Saiba mais sobre os fundamentos de como configurar segredos na API do Reator para uso no encaminhamento de eventos.
exl-id: 0298c0cd-9fba-4b54-86db-5d2d8f9ade54
source-git-commit: 88939d674c0002590939004e0235d3da8b072118
workflow-type: tm+mt
source-wordcount: '1232'
ht-degree: 1%

---

# Segredos na API do Reator

Na API do Reator, um segredo é um recurso que representa uma credencial de autenticação. Segredos são usados no encaminhamento de eventos para autenticar em outro sistema para troca segura de dados. Portanto, os segredos só podem ser criados nas propriedades de encaminhamento de eventos (propriedades cujas `platform` atributo está definido como `edge`).

Atualmente, há três tipos secretos compatíveis indicados no `type_of` atributo:

| Tipo secreto | Descrição |
| --- | --- |
| `token` | Uma única cadeia de caracteres que representa um valor de token de autenticação conhecido e compreendido por ambos os sistemas. |
| `simple-http` | Contém dois atributos de string para um nome de usuário e senha, respectivamente. |
| `oauth2-client_credentials` | Contém vários atributos para suportar [OAuth](https://datatracker.ietf.org/doc/html/rfc6749) especificação de autenticação. O encaminhamento de eventos solicita as informações necessárias e, em seguida, lida com a renovação desses tokens em um intervalo especificado. |

{style="table-layout:auto"}

Este guia fornece uma visão geral de alto nível sobre como configurar segredos para usar no encaminhamento de eventos. Para obter orientação detalhada sobre como gerenciar segredos na API do Reator, incluindo o exemplo JSON da estrutura de um segredo, consulte o [manual de endpoint de segredos](../endpoints/secrets.md).

## Credenciais

Cada segredo contém um `credentials` que mantém seus respectivos valores de credencial. Quando [criação de um segredo na API](../endpoints/secrets.md#create), cada tipo de segredo tem atributos obrigatórios diferentes, conforme mostrado nas seções abaixo:

* [`token`](#token)
* [&quot;simple-http&quot;](#simple-http)
* [`oauth2-client_credentials`](#oauth2-client_credentials)
* [&quot;oauth2-google&quot;](#oauth2-google)

### `token` {#token}

Segredos com um `type_of` valor de `token` exigir apenas um único atributo em `credentials`:

| Atributo de credencial | Tipo de dados | Descrição |
| --- | --- | --- |
| `token` | String | Um token secreto compreendido pelo sistema de destino. |

{style="table-layout:auto"}

O token é armazenado como um valor estático e, portanto, o valor do segredo `expires_at` e `refresh_at` As propriedades do estão definidas como `null` quando o segredo é criado.

### `simple-http` {#simple-http}

Segredos com um `type_of` valor de `simple-http` exigir os seguintes atributos em `credentials`:

| Atributo de credencial | Tipo de dados | Descrição |
| --- | --- | --- |
| `username` | String | Um nome de usuário. |
| `password` | String | Uma senha. Esse valor não está incluído na resposta da API. |

{style="table-layout:auto"}

Quando o segredo é criado, os dois atributos são trocados com uma codificação BASE64 de `username:password`. Após a troca, o segredo é `expires_at` e `refresh_at` As propriedades do estão definidas como `null`.

### `oauth2-client_credentials` {#oauth2-client_credentials}

Segredos com um `type_of` valor de `oauth2-client_credentials` exigir os seguintes atributos em `credentials`:

| Atributo de credencial | Tipo de dados | Descrição |
| --- | --- | --- |
| `client_id` | String | A ID do cliente para a integração OAuth. |
| `client_secret` | String | O segredo do cliente para a integração OAuth. Esse valor não está incluído na resposta da API. |
| `token_url` | String | O URL de autorização para a integração OAuth. |
| `refresh_offset` | Número inteiro | *(Opcional)* O valor, em segundos, para compensar a operação de atualização. Se esse atributo for omitido ao criar o segredo, o valor será definido como `14400` (quatro horas) por padrão. |
| `options` | Objeto | *(Opcional)* Especifica opções adicionais para a integração OAuth:<ul><li>`scope`: uma string que representa a variável [Escopo do OAuth 2.0](https://oauth.net/2/scope/) para as credenciais.</li><li>`audience`: uma string que representa um [Token de acesso Auth0](https://auth0.com/docs/protocols/protocol-oauth2).</li></ul> |

Quando um `oauth2-client_credentials` for criado ou atualizado, a variável `client_id` e `client_secret` (e possivelmente `options`) são trocadas em uma solicitação POST para o `token_url`, de acordo com o fluxo Credenciais de cliente do protocolo OAuth.

>[!NOTE]
>
>Espera-se que o corpo da resposta do serviço de autorização seja compatível com o protocolo OAuth.

Se o serviço de autorização responder com `200 OK` e um corpo de resposta JSON, o corpo é analisado e a variável `access_token` é enviado para o ambiente de borda e `expires_in` é usado para calcular o `expires_at` e `refresh_at` atributos para o segredo. Se não houver associação de ambiente no segredo, `access_token` é descartado.

Uma troca de credenciais é considerada bem-sucedida sob as seguintes condições:

* `expires_in` é maior que `28800` (oito horas).
* `refresh_offset` é menor que o valor de `expires_in` menos `14400` (quatro horas). Por exemplo, se `expires_in` é `36000` (dez horas), e a variável `refresh_offset` é `28800` (oito horas), considera-se que a troca falhou porque `28800` é maior que `36000` - `14400` (`21600`).

Se a troca for bem-sucedida, o atributo de status do segredo será definido como `succeeded` e valores para `expires_at` e `refresh_at` são definidos:

* `expires_at` é a hora UTC atual mais o valor de `expires_in`.
* `refresh_at` é a hora UTC atual mais o valor de `expires_in`, menos o valor de `refresh_offset`. Por exemplo, se `expires_in` é `43200` (doze horas) e a `refresh_offset` é `14400` (quatro horas), a `refresh_at` a propriedade seria definida como `28800` (oito horas) após a hora UTC atual.

Se a troca falhar por qualquer motivo, a variável `status_details` atributo no `meta` atualizações de objetos com informações relevantes.

#### Atualizando um `oauth2-client_credentials` segredo

Se um `oauth2-client_credentials` o segredo foi atribuído a um ambiente e o status é `succeeded` (as credenciais foram trocadas com êxito), uma nova troca será executada automaticamente em `refresh_at`.

Se a troca for bem-sucedida, a variável `refresh_status` atributo no `meta` objeto está definido como `succeeded` enquanto `expires_at`, `refresh_at`, e `activated_at` são atualizados de acordo.

Se houver falha na troca, haverá mais três tentativas com a última tentativa até não mais do que duas horas antes de o token de acesso expirar. Se todas as tentativas falharem, a variável `refresh_status_details` atributo do `meta` atualizações de objetos com detalhes relevantes.

### `oauth2-google` {#oauth2-google}

Segredos com um `type_of` valor de `oauth2-google` exige o seguinte atributo em `credentials`:

| Atributo de credencial | Tipo de dados | Descrição |
| --- | --- | --- |
| `scopes` | Matriz | Lista os escopos de produto do Google para autenticação. Os seguintes escopos são compatíveis:<ul><li>[Anúncios do Google](https://developers.google.com/google-ads/api/docs/oauth/overview): `https://www.googleapis.com/auth/adwords`</li><li>[Google Pub/Sub](https://cloud.google.com/pubsub/docs/reference/service_apis_overview): `https://www.googleapis.com/auth/pubsub`</li></ul> |

Depois de criar o `oauth2-google` secreta, a resposta inclui uma `meta.authorization_url` propriedade. Você deve copiar e colar esse URL em um navegador para concluir o fluxo de autenticação do Google.

#### Reautorizar um `oauth2-google` segredo

O URL de autorização de um `oauth2-google` o segredo expira uma hora após sua criação (conforme indicado pelo `meta.authorization_url_expires_at`). Após esse período, o segredo deverá ser reautorizado para renovar o processo de autenticação.

Consulte a [manual de endpoint de segredos](../endpoints/secrets.md#reauthorize) para obter detalhes sobre como reautorizar uma `oauth2-google` secreta fazendo uma solicitação PATCH para a API do Reator.

## Relacionamento de ambiente

Ao criar um segredo, você deve especificar o [ambiente](../endpoints/environments.md) em que existirá. Segredos são imediatamente implantados no ambiente em que são criados.

Um segredo só pode ser associado a um ambiente. Uma vez estabelecida a relação entre um segredo e um ambiente, o segredo não pode ser apagado do ambiente e o segredo não pode ser associado a um ambiente diferente.

>[!NOTE]
>
>A única exceção a essa regra é se o ambiente em questão for excluído. Nesse caso, a relação é limpa e o segredo pode ser atribuído a um ambiente diferente.

Depois que as credenciais de um segredo forem trocadas com êxito, para que um segredo seja associado a um ambiente, o artefato de troca (a sequência de token para `token`, a sequência de caracteres codificada em Base64 para `simple-http`ou o token de acesso para `oauth2-client_credentials`) é salvo com segurança no ambiente.

Depois que o artefato do Exchange for salvo com êxito no ambiente, as `activated_at` O atributo é definido com a hora UTC atual e agora pode ser referenciado usando um elemento de dados. Consulte a [próxima seção](#referencing-secrets) para obter mais informações sobre como fazer referência a segredos.

## Referência de segredos {#referencing-secrets}

Para fazer referência a um segredo, você deve criar um elemento de dados do tipo &quot;[!UICONTROL Segredo]&quot; (fornecido pela [[!UICONTROL Núcleo] extensão](../../extensions/client/core/overview.md)) em uma propriedade de encaminhamento de eventos. Ao configurar esse elemento de dados, você será solicitado a indicar qual segredo usar para cada ambiente. Em seguida, você pode criar regras que fazem referência a um elemento de dados secreto, como no cabeçalho de uma chamada HTTP.

![Elemento de dados secreto](../../images/api/guides/secrets/data-element.png)

>[!NOTE]
>
>Para adicionar um elemento de dados secreto a uma biblioteca, você deve ter pelo menos um `succeeded` segredo associado ao ambiente no qual a biblioteca está sendo criada. Por exemplo, se uma biblioteca tiver um elemento de dados secreto que não tenha um `succeeded` segredo configurado para o [!UICONTROL Segredo de armazenamento temporário] seção, tentar criar essa biblioteca no ambiente de preparo resultará em um erro.

No tempo de execução, o elemento de dados secreto é substituído pelo artefato de troca secreta correspondente salvo no ambiente.

## Próximas etapas

Este guia abordou os fundamentos do trabalho com segredos na API do Reator. Para obter detalhes sobre como gerenciar segredos usando chamadas de API, consulte a [manual de endpoint de segredos](../endpoints/secrets.md).
