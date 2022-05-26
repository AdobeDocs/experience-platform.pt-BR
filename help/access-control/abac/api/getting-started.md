---
keywords: Experience Platform, home, tópicos populares, Controle de acesso com base em atributos, controle de acesso com base em atributos
title: Introdução ao controle de acesso baseado em atributos
description: O Controle de acesso baseado em atributos permite gerenciar programaticamente as funções e as políticas no Adobe Experience Platform. Siga este manual para saber como executar operações importantes usando a API.
hide: true
hidefromtoc: true
exl-id: d1a66afa-dff4-49d7-b57c-527f05977155
source-git-commit: 19f1e8df8cd8b55ed6b03f80e42810aefd211474
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 4%

---

# Introdução ao controle de acesso baseado em atributos

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível em uma versão limitada para clientes de assistência médica com base nos EUA. Esse recurso estará disponível para todos os clientes da Real-time Customer Data Platform assim que for totalmente lançado.

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
