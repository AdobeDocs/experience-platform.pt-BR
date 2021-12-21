---
keywords: Experience Platform, home, tópicos populares, controle de acesso, api, introdução
solution: Experience Platform
title: Guia da API de controle de acesso
topic-legacy: developer guide
description: O controle de acesso no Adobe Experience Platform permite gerenciar funções e permissões para vários recursos da plataforma usando a Adobe Admin Console. As seções a seguir fornecem informações adicionais que os desenvolvedores precisarão saber para fazer chamadas com êxito para a API do Registro de Schema.
exl-id: 6fd956fb-ade4-48d3-843f-4c9a605945c9
source-git-commit: b1edea734f58762cfa895f768ea8e2969fdd5c02
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 2%

---

# [!DNL Access Control] Manual da API

[!DNL Access control] para [!DNL Experience Platform] é administrada através do [Adobe Admin Console](https://adminconsole.adobe.com). Essa funcionalidade utiliza perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes. Consulte a [visão geral do controle de acesso](../home.md) para obter mais informações.

Este guia do desenvolvedor fornece informações sobre como formatar suas solicitações para a [[!DNL Access Control API]](https://www.adobe.io/experience-platform-apis/references/access-control/)e abrange as seguintes operações:

- [Listar nomes de permissões e tipos de recursos](./permissions-and-resource-types.md)
- [Exibir políticas eficazes para o usuário atual](./effective-policies.md)

## Introdução

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas para o [!DNL Access Control] API.

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no [!DNL Experience Platform] guia de solução de problemas.

### Coletar valores para cabeçalhos necessários

Para fazer chamadas para [!DNL Platform] As APIs devem ser concluídas primeiro [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en). A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todos [!DNL Experience Platform] Chamadas de API, conforme mostrado abaixo:

- Autorização: Portador `{ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id: `{IMS_ORG}`

Todos os recursos em [!DNL Experience Platform] são isoladas em sandboxes virtuais específicas. Todas as solicitações para [!DNL Platform] As APIs exigem um cabeçalho que especifica o nome da sandbox em que a operação ocorrerá:

- x-sandbox-name: `{SANDBOX_NAME}`

>[!NOTE]
>
>Para obter mais informações sobre sandboxes em [!DNL Platform], consulte o [documentação de visão geral da sandbox](../../sandboxes/home.md).

Todas as solicitações que contêm uma carga útil (POST, PUT, PATCH) exigem um cabeçalho adicional:

- Tipo de conteúdo: application/json

## Próximas etapas

Agora que você coletou as credenciais necessárias, pode continuar a ler o resto do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus endpoints e demonstra chamadas de API de exemplo para executar operações CRUD. Cada chamada inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e as cargas corretamente formatadas e uma resposta de amostra para uma chamada bem-sucedida.
