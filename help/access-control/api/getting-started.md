---
keywords: Experience Platform;início;tópicos populares;controle de acesso;api;introdução;;home;popular topics;access control;api;getting started
solution: Experience Platform
title: Guia da API de controle de acesso
description: O controle de acesso no Adobe Experience Platform permite gerenciar funções e permissões para vários recursos da plataforma usando o Adobe Admin Console. As seções a seguir fornecem informações adicionais que os desenvolvedores precisarão saber para fazer chamadas com êxito para a API do Registro de esquema.
role: Developer
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 21%

---

# [!DNL Access Control] Manual da API

[!DNL Access control] para [!DNL Experience Platform] é administrado através do [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade aproveita perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes. Consulte a [visão geral do controle de acesso](../home.md) para obter mais informações.

Este guia do desenvolvedor fornece informações sobre como formatar suas solicitações para o [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)e abrange as seguintes operações:

- [Listar nomes de permissões e tipos de recursos](./permissions-and-resource-types.md)
- [Exibir políticas de acesso efetivo para o usuário atual](./effective-policies.md)

## Introdução

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para o [!DNL Access Control] API.

### Leitura de chamadas de API de amostra

Este manual fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] APIs, primeiro conclua o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API da [!DNL Experience Platform], conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{ORG_ID}`

Todos os recursos em [!DNL Experience Platform] são isolados em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes no [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm um conteúdo (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Próximas etapas

Agora que você reuniu as credenciais necessárias, pode continuar lendo o restante do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus endpoints e demonstra exemplos de chamadas de API para executar operações CRUD. Cada chamada inclui o formato da API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e cargas úteis formatadas corretamente e uma resposta de amostra para uma chamada bem-sucedida.
