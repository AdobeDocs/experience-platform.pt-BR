---
keywords: Experience Platform;home;popular topics;sandbox developer guide
solution: Experience Platform
title: Guia do desenvolvedor da API Sandbox
topic: developer guide
description: Este guia do desenvolvedor fornece etapas para ajudá-lo a usar a API do Sandbox para gerenciar caixas de proteção no Experience Platform e inclui chamadas de API de amostra para executar várias operações.
translation-type: tm+mt
source-git-commit: 0af537e965605e6c3e02963889acd85b9d780654
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 0%

---


# Guia do desenvolvedor da API Sandbox

As caixas de proteção da Adobe Experience Platform fornecem ambientes de desenvolvimento isolados que permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar seu ambiente de produção.

Este guia do desenvolvedor fornece etapas para ajudá-lo a usar a API do Sandbox para gerenciar caixas de proteção no Experience Platform e inclui chamadas de API de amostra para executar várias operações.

## Introdução à API do Sandbox

Para gerenciar caixas de proteção para a organização IMS, é necessário ter permissões de administração de caixa de proteção. Os usuários sem permissões de acesso podem usar somente o ponto de extremidade para [listar as caixas de proteção ativas do usuário](./list-active-sandboxes.md)atual. Consulte a visão geral [do](../../access-control/home.md) controle de acesso para obter mais informações sobre como atribuir permissões de caixa de proteção para o Experience Platform.

### Lendo chamadas de exemplo da API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md#how-do-i-format-an-api-request) de API de exemplo no guia de solução de problemas do Experience Platform.

### Reunir valores para cabeçalhos necessários

Este guia requer que você tenha concluído o tutorial [de](../../tutorials/authentication.md) autenticação para fazer chamadas com êxito para as APIs da plataforma. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, como mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Além dos cabeçalhos de autenticação, todas as solicitações exigem um cabeçalho que especifique o nome da caixa de proteção em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT e PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Próximas etapas

Agora que você reuniu as credenciais necessárias, pode continuar a ler o restante do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus pontos de extremidade e demonstra exemplos de chamadas de API para executar operações CRUD. Cada chamada inclui o formato **geral da** API, uma **solicitação** de amostra mostrando os cabeçalhos necessários e cargas formatadas corretamente e uma **resposta** de amostra para uma chamada bem-sucedida.