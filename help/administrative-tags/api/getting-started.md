---
solution: Experience Platform
title: Introdução à API de tags unificadas
description: A documentação a seguir fornece informações adicionais que você precisa saber para trabalhar com êxito com a API de tags unificadas.
role: Developer
source-git-commit: 8280281fa8b676b13c0601e2c9a50515ce8979c3
workflow-type: tm+mt
source-wordcount: '261'
ht-degree: 9%

---

# Introdução à API de tags unificadas {#getting-started}

A API de tags unificadas permite categorizar e gerenciar os objetos comerciais na Adobe Experience Platform.

As seções a seguir fornecem as informações adicionais que você precisará saber para trabalhar com êxito com a API de tags unificadas.

## Leitura de chamadas de API de amostra

A documentação da API de tags unificadas fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

## Cabeçalhos obrigatórios

A documentação da API também exige que você tenha concluído a [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para endpoints da Platform. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários nas chamadas de API de Experience Platform, conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre como trabalhar com sandboxes no [!DNL Experience Platform], consulte o [documentação de visão geral das sandboxes](../../sandboxes/home.md).

## Próximas etapas

Para fazer chamadas usando a API de tags unificadas, selecione um dos manuais de endpoint disponíveis usando a navegação à esquerda ou no [visão geral do guia do desenvolvedor](./overview.md)
