---
title: Autenticação
description: Saiba como configurar a autenticação para a API do servidor de rede de borda do Adobe Experience Platform.
exl-id: 73c7a186-9b85-43fe-a586-4c6260b6fa8c
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 2%

---

# Autenticação {#authentication}

## Visão geral

A variável [!DNL Edge Network Server API] O lida com a coleta de dados autenticada e não autenticada, dependendo da origem dos eventos e do domínio de coleta da API.

Para cada solicitação, o [!DNL Server API] verifica o fluxo de dados [!DNL access type] configuração. Usando essa configuração, os clientes podem configurar um fluxo de dados para aceitar dados autenticados ou dados autenticados e não autenticados. Por padrão, ambos os tipos de dados são aceitos.

Para obter detalhes sobre como configurar o tipo de acesso do fluxo de dados, consulte a documentação sobre como [criar e configurar um fluxo de dados](../edge/datastreams/overview.md#create).

Abaixo está um resumo do comportamento, com base na sequência de dados [!DNL Access Type] e o endpoint no qual a solicitação é recebida.

| [!DNL Access Type] | edge.adobedc.net | server.adobedc.net |
|-----------------|-------------------------------|-----------------------|
| misto (padrão) | Não autentica a solicitação | Autentica a solicitação |
| autenticado | Autentica a solicitação | Autentica a solicitação |

Chamadas de API provenientes de um servidor privado em `server.adobedc.net` O deve ser sempre autenticado.

## Pré-requisitos {#prerequisites}

Antes de fazer chamadas para a variável [!DNL Server API], verifique se você atende aos seguintes pré-requisitos:

* Você tem uma conta da Organização IMS com acesso ao Adobe Experience Platform.
* Sua conta Experience Platform tem o `developer` e `user` funções habilitadas para o perfil de produto API do Adobe Experience Platform. Entre em contato com [Admin Console](../access-control/home.md) administrador para habilitar essas funções para sua conta.
* Você tem uma Adobe ID. Se você não tiver uma Adobe ID, acesse o [Console do Adobe Developer](https://developer.adobe.com/console) e criar uma nova conta.

## Coletar credenciais {#credentials}

Para fazer chamadas para APIs da Platform, primeiro conclua o [tutorial de autenticação](../landing/api-authentication.md). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{ORG_ID}`

Os recursos no Experience Platform podem ser isolados em sandboxes virtuais específicas. Em solicitações para APIs da Platform, é possível especificar o nome e a ID da sandbox em que a operação ocorrerá. Esses parâmetros são opcionais.

* x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no Experience Platform, consulte a [documentação de visão geral da sandbox](../sandboxes/home.md).

Todas as solicitações que contêm uma carga (POST, PUT, PATCH) exigem um cabeçalho de tipo de mídia adicional:

* Tipo de conteúdo: `application/json`

## Configurar permissões de gravação do conjunto de dados {#dataset-write-permissions}

Para configurar permissões de gravação do conjunto de dados, vá para a [Admin Console](https://adminconsole.adobe.com), localize o perfil de produto anexado à sua chave de API e defina as seguintes permissões:

* No [!UICONTROL Sandboxes] selecione a sandbox do fluxo de dados.
* No [!UICONTROL Gerenciamento de dados] , selecione a **[!UICONTROL Gerenciar conjuntos de dados]** permissão.

## Solução de problemas de erros de autorização {#troubleshooting-authorization}

| Código de erro | Mensagem de erro | Descrição |
| --- | --- | --- |
| `EXEG-0500-401` | Token de autorização inválido | Essa mensagem de erro é exibida em qualquer uma das seguintes situações:  <ul><li>A variável `authorization` valor de cabeçalho ausente.</li><li>A variável `authorization` o valor do cabeçalho não inclui o `Bearer` token.</li><li>O token de autorização fornecido tem um formato inválido.</li><li>A sequência de dados requer autenticação, mas a solicitação não tem cabeçalhos obrigatórios.</li></ul> |
| `EXEG-0501-401` | Token de autorização de usuário inválido | Essa mensagem de erro é exibida em qualquer uma das seguintes situações: <ul><li>A chamada da API não tem o necessário `x-user-token` cabeçalho.</li><li>O token de usuário fornecido tem um formato inválido.</li></ul> |
| `EXEG-0502-401` | Token de autorização inválido | Esta mensagem de erro é exibida quando o token de autorização fornecido tem um formato válido (JWT), mas sua assinatura é inválida. Verifique a [tutorial de autenticação](../landing/api-authentication.md) para saber como obter um token JWT válido. |
| `EXEG-0503-401` | Token de autorização inválido | Esta mensagem de erro é exibida quando o token de autorização fornecido expira. Passe pelo [tutorial de autenticação](../landing/api-authentication.md) para gerar um novo token. |
| `EXEG-0504-401` | O contexto do produto obrigatório está ausente | Essa mensagem de erro é exibida em qualquer uma das seguintes situações:  <ul><li>A conta de desenvolvedor não tem acesso ao contexto de produto do Adobe Experience Platform.</li><li>A conta da empresa ainda não está qualificada para a Adobe Experience Platform.</li></ul> |
| `EXEG-0505-401` | O escopo do token de autorização necessário está ausente | Este erro se aplica somente à autenticação da conta de serviço. A mensagem de erro é exibida quando o token de autorização de serviço incluído na chamada pertence a uma conta de serviço que não tem acesso à `acp.foundation` Escopo IMS. |
| `EXEG-0506-401` | Sandbox não acessível para gravação | Esta mensagem de erro é exibida quando a conta do desenvolvedor não tem `WRITE` acesso à sandbox Experience Platform em que o fluxo de dados é definido. |
