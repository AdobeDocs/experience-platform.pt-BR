---
title: Introdução à API do Serviço MTLS
description: Este documento fornece informações adicionais que você precisa saber para trabalhar com êxito com a API MTLS.
role: Developer
exl-id: db5978cf-fe47-4b76-86ba-c8ea1ee6b12f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 6%

---

# Introdução à API do Serviço MTLS {#getting-started}

A API de Serviço MTLS permite recuperar e verificar com segurança os certificados públicos emitidos pela Adobe.

As seções a seguir fornecem informações adicionais que você precisará saber para trabalhar com êxito com a API de Serviço MTLS.

## Leitura de chamadas de API de amostra

A documentação da API de serviço do MTLS fornece um exemplo de chamada de API para demonstrar como formatar suas solicitações. Isso inclui o caminho, os cabeçalhos necessários e a carga útil da solicitação formatada corretamente. Também fornece exemplos de JSON retornado nas respostas da API. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md#how-do-i-format-an-api-request) no guia de solução de problemas do Experience Platform.

## Cabeçalhos obrigatórios

A documentação da API também requer que você tenha concluído o [tutorial de autenticação](https://www.adobe.com/go/platform-api-authentication-en) para fazer chamadas com êxito para pontos de extremidade do Experience Platform. Concluir o tutorial de autenticação fornece os valores de cada um dos cabeçalhos necessários nas chamadas de API do Experience Platform, conforme mostrado abaixo:

- Autorização: `Bearer {ACCESS_TOKEN}`
- x-api-key: `{API_KEY}`
- x-gw-ims-org-id `{ORG_ID}`

## Próximas etapas

Para fazer chamadas usando a API de Serviço MTLS, selecione os manuais de ponto de extremidade usando a navegação à esquerda ou na [visão geral do guia do desenvolvedor](./overview.md)
