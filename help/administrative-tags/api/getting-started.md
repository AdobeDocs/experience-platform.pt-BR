---
solution: Experience Platform
title: Introdução à API de tags unificadas
description: A documentação a seguir fornece informações adicionais que você precisa saber para trabalhar com êxito com a API de tags unificadas.
role: Developer
exl-id: 8f33707f-b46d-4054-802c-9e42ecabd9ba
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '262'
ht-degree: 9%

---

# Introdução à API de tags unificadas {#getting-started}

A API de tags unificadas permite categorizar e gerenciar os objetos comerciais na Adobe Experience Platform.

As seções a seguir fornecem as informações adicionais que você precisará saber para trabalhar com êxito com a API de tags unificadas.

## Leitura de chamadas de API de amostra

A documentação da API de tags unificadas fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para pontos de extremidade do Experience Platform. Concluir o tutorial de autenticação fornece os valores de cada um dos cabeçalhos necessários nas chamadas de API do Experience Platform, conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] estão isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Experience Platform] APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com sandboxes em [!DNL Experience Platform], consulte a [documentação de visão geral das sandboxes](../../sandboxes/home.md).

## Próximas etapas

Para fazer chamadas usando a API de Marcas Unificadas, selecione um dos manuais de endpoint disponíveis usando a navegação à esquerda ou na [visão geral do guia do desenvolvedor](./overview.md)
