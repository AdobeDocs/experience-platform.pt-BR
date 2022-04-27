---
keywords: Experience Platform, home, tópicos populares, guia do desenvolvedor do sandbox
solution: Experience Platform
title: Introdução à API do Sandbox
topic-legacy: developer guide
description: A API de sandbox permite que os desenvolvedores gerenciem programaticamente as sandboxes no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: d38df5ede84c1306a76fd1ec83d9d0a540b0d01c
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 5%

---

# Introdução à API do Sandbox

As sandboxes no Adobe Experience Platform fornecem ambientes de desenvolvimento isolados que permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar seu ambiente de produção.

Este guia do desenvolvedor fornece etapas para ajudá-lo a usar a API de sandbox para gerenciar sandboxes no Experience Platform e inclui exemplos de chamadas de API para executar várias operações.

## Pré-requisitos

Para gerenciar sandboxes para a organização de IMS, é necessário ter permissões de administração de sandbox. Os usuários sem permissões de acesso só podem usar o [ponto de extremidade de sandboxes disponível](./available.md) para listar sandboxes ativas para o usuário atual. Consulte a [visão geral do controle de acesso](../../access-control/home.md) para obter mais informações sobre como atribuir permissões de sandbox para o Experience Platform.

### Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Coletar valores para cabeçalhos necessários

Este guia requer que você tenha completado o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para APIs da plataforma. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Além dos cabeçalhos de autenticação, todas as solicitações exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT e PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Próximas etapas

Agora que você coletou as credenciais necessárias, pode continuar a ler o resto do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus endpoints e demonstra chamadas de API de exemplo para executar operações CRUD. Cada chamada inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e as cargas corretamente formatadas e uma resposta de amostra para uma chamada bem-sucedida.
