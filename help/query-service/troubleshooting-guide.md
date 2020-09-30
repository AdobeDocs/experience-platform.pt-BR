---
keywords: Experience Platform;home;popular topics;query service;Query service;troubleshooting guide;faq;troubleshooting;
solution: Experience Platform
title: Guia de solução de problemas do Serviço de Query Adobe Experience Platform
topic: troubleshooting
description: Este documento contém informações sobre códigos de erro comuns encontrados e as possíveis causas.
translation-type: tm+mt
source-git-commit: 4b2df39b84b2874cbfda9ef2d68c4b50d00596ac
workflow-type: tm+mt
source-wordcount: '168'
ht-degree: 2%

---


# Erros e solução de problemas

## Erros de API REST

| Código de status HTTP | Descrição | Causas possíveis |
| ---------------- | ----------- | --------------- |
| 400 | Solicitação incorreta | Query malformado ou ilegal |
| 401 | Falha na autenticação | Token de autenticação inválido |
| 500 | Erro interno do servidor | Falha do sistema interno |

## Erros de API do PostgreSQL

| Código de erro e estado da conexão | Descrição | Causa possível |
| ------------------------------- | ----------- | -------------- |
| **start 28P01** - autenticação | Senha inválida | Token de autenticação inválido |
| **start 28000** - autenticação | Tipo de autorização inválido | Tipo de autorização inválido. Deve ser `AuthenticationCleartextPassword`. |
| **start 42P12** - autenticação | Nenhuma tabela encontrada | Nenhuma tabela encontrada para uso |
| **query 42601** | Erro de sintaxe | Erro de comando ou sintaxe inválido |
| **query 58000** | Erro do sistema | Falha do sistema interno |
| **query 42P01** | Tabela não encontrada | A tabela especificada no query não foi encontrada |
| **query 42P07** | A tabela existe | A tabela já existe com o mesmo nome (CREATE TABLE) |
| **query 53400** | LIMITE excede o valor máximo | O usuário especificou uma cláusula LIMIT superior a 100.000 |
| **query 53400** | Tempo limite da declaração | A declaração em tempo real enviada demorou mais de 10 minutos |
| **08P01** N/D | Tipo de mensagem não suportado | Tipo de mensagem não suportado |
