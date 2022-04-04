---
title: Autenticação
description: Saiba como configurar a autenticação para a API do servidor de rede de borda do Adobe Experience Platform
seo-description: Learn how to configure authentication for the Adobe Experience Platform Edge Network Server API
keywords: recolha de dados; autenticação; api da rede de borda Adobe Experience Platform; autorização
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: 422f859bef8faf292fd7e5fd8b6a8d31967421c1
workflow-type: tm+mt
source-wordcount: '628'
ht-degree: 2%

---

# Autenticação {#authentication}

## Visão geral

O [!DNL Adobe Experience Platform Edge Network Server API] O lida com a coleta de dados autenticada e não autenticada, dependendo da fonte dos eventos e do domínio de coleta da API.

Para cada solicitação, a variável [!DNL Server API] verifica o armazenamento de dados `access_type` configuração.

Usando essa configuração, os clientes podem configurar um armazenamento de dados para aceitar dados autenticados ou dados autenticados e não autenticados. Por padrão, ambos os tipos de dados são aceitos.

Abaixo está um resumo do comportamento, com base no `access_type` e o terminal no qual a solicitação é recebida.

| `access_type` | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| mista (padrão) | Não autentica solicitação | Autentica solicitação |
| autenticado | Autentica solicitação | Autentica solicitação |

Chamadas de API provenientes de um servidor privado em `server.adobedc.net` deve ser sempre autenticado.

## Pré-requisitos {#prerequisites}

Antes de poder fazer chamadas para a [!DNL Server API], certifique-se de atender aos seguintes pré-requisitos:

* Você tem uma conta da Organização IMS com acesso à Adobe Experience Platform.
* Sua conta do Experience Platform tem a variável `developer` e `user` funções ativadas para o perfil de produto da API do Adobe Experience Platform. Entre em contato com seu [Admin Console](../access-control/home.md) para ativar essas funções em sua conta.
* Você tem uma Adobe ID. Caso não tenha uma Adobe ID, acesse [Console do desenvolvedor do Adobe](https://developer.adobe.com/console) e criar uma nova conta.

## Obter credenciais {#credentials}

Para fazer chamadas para APIs da plataforma, primeiro conclua o [tutorial de autenticação](../landing/api-authentication.md). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Os recursos no Experience Platform podem ser isolados para sandboxes virtuais específicas. Em solicitações para APIs da plataforma, é possível especificar o nome e a ID da sandbox em que a operação ocorrerá. Esses são parâmetros opcionais.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no Experience Platform, consulte o [documentação de visão geral da sandbox](../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Configurar permissões de gravação do conjunto de dados {#dataset-write-permissions}

Para configurar permissões de gravação do conjunto de dados, acesse [Admin Console](https://adminconsole.adobe.com), localize o perfil de produto anexado à sua chave de API e defina as seguintes permissões:

* No [!UICONTROL Sandboxes] selecione a sandbox do datastream.
* No [!UICONTROL Gerenciamento de dados] selecione a **[!UICONTROL Gerenciar conjuntos de dados]** permissão.

## Solução de problemas de erros de autorização {#troubleshooting-authorization}

| Código de erro | Mensagem de erro | Descrição |
| --- | --- | --- |
| `EXEG-0500-401` | Token de autorização inválido | Essa mensagem de erro é exibida em qualquer uma das seguintes situações:  <ul><li>O `authorization` o valor do cabeçalho está ausente.</li><li>O `authorization` o valor do cabeçalho não inclui o `Bearer` token.</li><li>O token de autorização fornecido tem um formato inválido.</li><li>O armazenamento de dados requer autenticação, mas a solicitação está sem os cabeçalhos obrigatórios.</li></ul> |
| `EXEG-0501-401` | Token de autorização de usuário inválido | Essa mensagem de erro é exibida em qualquer uma das seguintes situações: <ul><li>A chamada da API está sem o `x-user-token` cabeçalho.</li><li>O token de usuário fornecido tem um formato inválido.</li></ul> |
| `EXEG-0502-401` | Token de autorização inválido | Esta mensagem de erro é exibida quando o token de autorização fornecido tem um formato válido (JWT), mas sua assinatura é inválida. Verifique a [tutorial de autenticação](../landing/api-authentication.md) para saber como obter um token JWT válido. |
| `EXEG-0503-401` | Token de autorização inválido | Esta mensagem de erro é exibida quando o token de autorização fornecido expira. Percorra o [tutorial de autenticação](../landing/api-authentication.md) para gerar um novo token. |
| `EXEG-0504-401` | O contexto de produto necessário está ausente | Essa mensagem de erro é exibida em qualquer uma das seguintes situações:  <ul><li>A conta do desenvolvedor não tem acesso ao contexto de produto do Adobe Experience Platform.</li><li>A conta da empresa ainda não tem direito à Adobe Experience Platform.</li></ul> |
| `EXEG-0505-401` | O escopo do token de autorização necessário está ausente | Esse erro se aplica somente à autenticação da conta de serviço. A mensagem de erro é exibida quando o token de autorização de serviço incluído na chamada pertence a uma conta de serviço que não tem acesso ao `acp.foundation` Escopo IMS. |
| `EXEG-0506-401` | Sandbox não acessível para gravação | Essa mensagem de erro é exibida quando a conta do desenvolvedor não tem `WRITE` acesso à sandbox do Experience Platform em que o datastream é definido. |
