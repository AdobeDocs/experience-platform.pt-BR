---
keywords: Experience Platform;página inicial;tópicos populares;guia do desenvolvedor de sandbox
solution: Experience Platform
title: Introdução à API de sandbox
description: A API de sandbox permite que os desenvolvedores gerenciem sandboxes de forma programática no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
role: Developer
exl-id: 1ae27f30-2f89-4bfa-887d-a5def17b5cbc
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '373'
ht-degree: 15%

---

# Introdução à API de sandbox

As sandboxes na Adobe Experience Platform fornecem ambientes de desenvolvimento isolados que permitem testar recursos, executar experimentos e fazer configurações personalizadas sem afetar o ambiente de produção.

Este guia do desenvolvedor fornece etapas para ajudar você a usar a API de sandbox para gerenciar sandboxes no Experience Platform e inclui exemplos de chamadas de API para executar várias operações.

## Pré-requisitos

Para gerenciar sandboxes para sua organização, você deve ter permissões de Administração de sandbox. Os usuários sem permissões de acesso só podem usar o [ponto de extremidade de sandboxes disponível](./available.md) para listar sandboxes ativas para o usuário atual. Consulte a [visão geral do controle de acesso](../../access-control/home.md) para obter mais informações sobre como atribuir permissões de sandbox para o Experience Platform.

### Leitura de chamadas de API de amostra

Este manual fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

### Coletar valores para cabeçalhos necessários

Este guia requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para as APIs do Experience Platform. Concluir o tutorial de autenticação fornece os valores de cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id `{ORG_ID}`

Além dos cabeçalhos de autenticação, todas as solicitações exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* x-sandbox-name: `{SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT e PATCH) exigem um cabeçalho adicional:

* Tipo de conteúdo: application/json

## Próximas etapas

Agora que você reuniu as credenciais necessárias, pode continuar lendo o restante do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus endpoints e demonstra exemplos de chamadas de API para executar operações CRUD. Cada chamada inclui o formato da API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e cargas úteis formatadas corretamente e uma resposta de amostra para uma chamada bem-sucedida.
