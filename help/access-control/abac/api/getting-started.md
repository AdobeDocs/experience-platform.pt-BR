---
keywords: Experience Platform;página inicial;tópicos populares;Controle de acesso baseado em atributos;controle de acesso baseado em atributos
title: Introdução à API de controle de acesso baseado em atributos
description: A API de controle de acesso baseado em atributos permite gerenciar programaticamente funções e políticas de acesso no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
role: Developer
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: c16ce1020670065ecc5415bc3e9ca428adbbd50c
workflow-type: tm+mt
source-wordcount: '327'
ht-degree: 17%

---

# Introdução à API de controle de acesso baseada em atributos

Este guia do desenvolvedor fornece etapas para ajudar você a usar a API de controle de acesso baseada em atributos para gerenciar funções, produtos, categorias de permissão e conjuntos de permissões no Adobe Experience Platform, e inclui chamadas de API de exemplo para executar várias operações.

## Leitura de chamadas de API de amostra

Este manual fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

## Coletar valores para cabeçalhos necessários

Este guia requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para APIs da Platform. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Além dos cabeçalhos de autenticação, todas as solicitações exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT e PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Próximas etapas

Agora que você reuniu as credenciais necessárias, pode continuar lendo o restante do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus endpoints e demonstra exemplos de chamadas de API para executar operações CRUD. Cada chamada inclui o formato da API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e cargas úteis formatadas corretamente e uma resposta de amostra para uma chamada bem-sucedida.

Consulte os seguintes tutoriais de API para começar a fazer chamadas para a API de controle de acesso baseada em atributos:

* [Endpoint de funções](./roles.md)
* [Endpoint de produtos](./products.md)
