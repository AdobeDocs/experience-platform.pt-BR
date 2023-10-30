---
title: Introdução à API de ferramentas de sandbox
description: Use a API de ferramentas de sandbox para examinar artefatos, exportar e importar um instantâneo das configurações de sandbox entre as sandboxes. Siga este manual para saber como executar operações importantes usando a API.
exl-id: 0b34d153-a603-4397-a375-9cc846efe23a
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '314'
ht-degree: 14%

---

# Introdução à API de ferramentas de sandbox {#getting-started}

Este guia do desenvolvedor fornece etapas para ajudar você a usar a API de ferramentas da sandbox para gerenciar pacotes e ferramentas no Adobe Experience Platform, e inclui chamadas de API de exemplo para executar várias operações.

## Leitura de chamadas de API de amostra {#api-calls}

Este manual fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e conteúdos de solicitação formatados corretamente. Também são fornecidos exemplos de dados JSON retornados à resposta da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](/help/landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

## Coletar valores para cabeçalhos necessários {#headers}

Este guia requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para APIs da Platform. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários em todas as chamadas de API de Experience Platform, conforme mostrado abaixo:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {ORG_ID}`

Além dos cabeçalhos de autenticação, todas as solicitações exigem um cabeçalho que especifique o nome da sandbox em que a operação ocorrerá:

* `x-sandbox-name: {SANDBOX_NAME}`

Todas as solicitações que contêm uma carga (POST, PUT e PATCH) exigem um cabeçalho adicional:

* `Content-Type: application/json`

## Próximas etapas {#next-steps}

Agora que você reuniu as credenciais necessárias, pode continuar lendo o restante do guia do desenvolvedor. Cada seção fornece informações importantes sobre seus endpoints e demonstra exemplos de chamadas de API para executar operações CRUD. Cada chamada inclui o formato da API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e cargas úteis formatadas corretamente e uma resposta de amostra para uma chamada bem-sucedida.

Consulte os seguintes tutoriais de API para começar a fazer chamadas para a API de ferramentas da sandbox:

* [Endpoint de pacotes](./packages.md)
* [Endpoint de ferramentas](./tools.md)
