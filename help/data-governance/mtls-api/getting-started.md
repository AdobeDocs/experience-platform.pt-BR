---
title: Introdução à API do Serviço MTLS
description: Este documento fornece informações adicionais que você precisa saber para trabalhar com êxito com a API MTLS.
role: Developer
source-git-commit: f0b9d414d7b08015478c132de6910629d86c9cf9
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 7%

---

# Introdução à API do Serviço MTLS {#getting-started}

A API do Serviço MTLS permite recuperar e verificar com segurança os certificados públicos emitidos pelo Adobe.

As seções a seguir fornecem informações adicionais que você precisará saber para trabalhar com êxito com a API de Serviço MTLS.

## Leitura de chamadas de API de amostra

A documentação da API de serviço do MTLS fornece um exemplo de chamada de API para demonstrar como formatar suas solicitações. Isso inclui o caminho, os cabeçalhos necessários e a carga útil da solicitação formatada corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas de Experience Platform.

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para pontos de extremidade da Platform. Concluir o tutorial de autenticação fornece os valores para cada um dos cabeçalhos necessários nas chamadas de API de Experience Platform, conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

## Próximas etapas

Para fazer chamadas usando a API de Serviço MTLS, selecione os manuais de ponto de extremidade usando a navegação à esquerda ou na [visão geral do guia do desenvolvedor](./overview.md)
