---
keywords: Experience Platform;home;popular topics;sandbox developer guide
solution: Experience Platform
title: Guia da API do Sandbox
topic: developer guide
description: A API Sandbox permite que desenvolvedores gerenciem programaticamente as caixas de proteção no Adobe Experience Platform. Siga este guia para saber como executar operações principais usando a API.
translation-type: tm+mt
source-git-commit: e649ab3da077cdd8e98562199b8bdece6108a572
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 0%

---


# Guia da API do Sandbox

As caixas de proteção da Adobe Experience Platform fornecem ambientes de desenvolvimento isolados que permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar seu ambiente de produção.

Este guia do desenvolvedor fornece etapas para ajudá-lo a usar a API do Sandbox para gerenciar caixas de proteção no Experience Platform e inclui chamadas de API de amostra para executar várias operações.

## Introdução à API do Sandbox

Para gerenciar caixas de proteção para a organização IMS, é necessário ter permissões de administração de caixa de proteção. Os usuários sem permissões de acesso podem usar somente o ponto de extremidade para [listar caixas de proteção ativas para o usuário atual](./list-active-sandboxes.md). Consulte a [visão geral do controle de acesso](../../access-control/home.md) para obter mais informações sobre como atribuir permissões de caixa de proteção para Experience Platform.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Reunir valores para cabeçalhos necessários

Este guia requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para APIs de plataforma. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Além dos cabeçalhos de autenticação, todas as solicitações exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT e PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Próximas etapas

Agora que você reuniu as credenciais necessárias, pode continuar a ler o restante do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus pontos de extremidade e demonstra exemplos de chamadas de API para executar operações CRUD. Cada chamada inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e as cargas formatadas corretamente e uma resposta de amostra para uma chamada bem-sucedida.