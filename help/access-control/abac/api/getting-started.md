---
keywords: Experience Platform, home, tópicos populares, Controle de acesso com base em atributos, controle de acesso com base em atributos
title: Introdução ao controle de acesso baseado em atributos
description: O Controle de acesso baseado em atributos permite gerenciar programaticamente as funções e as políticas no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 9e44e647e4647a323fa9d1af55266d6f32b5ccb9
workflow-type: tm+mt
source-wordcount: '325'
ht-degree: 4%

---

# Introdução ao controle de acesso baseado em atributos

Este guia do desenvolvedor fornece etapas para ajudá-lo a usar o controle de acesso baseado em atributos para gerenciar funções, produtos, categorias de permissão e conjuntos de permissões no Adobe Experience Platform, e inclui chamadas de API de exemplo para executar várias operações.

## Lendo exemplos de chamadas de API

Este guia fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler exemplos de chamadas de API](../../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

## Coletar valores para cabeçalhos necessários

Este guia requer que você tenha completado o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para APIs da plataforma. A conclusão do tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API do Experience Platform, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Além dos cabeçalhos de autenticação, todas as solicitações exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga útil (POST, PUT e PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Próximas etapas

Agora que você coletou as credenciais necessárias, pode continuar a ler o resto do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus endpoints e demonstra chamadas de API de exemplo para executar operações CRUD. Cada chamada inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e as cargas corretamente formatadas e uma resposta de amostra para uma chamada bem-sucedida.

Consulte os seguintes tutoriais de API para começar a fazer chamadas para a API de controle de acesso baseada em atributos:

* [Ponto de extremidade de funções](./roles.md)
* [Ponto de extremidade de produtos](./products.md)
