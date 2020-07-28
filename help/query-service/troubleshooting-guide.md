---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia de solução de problemas do serviço de Query Adobe Experience Platform
topic: troubleshooting
translation-type: tm+mt
source-git-commit: c5bb112220b40fa6c2adfa89c80ddb87d382fbda
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 3%

---


# Erros e solução de problemas

## Erros de API REST

| Código de status HTTP | Descrição | Causas possíveis |
| ---------------- | ----------- | --------------- |
| 400 | Solicitação incorreta | query malformado ou ilegal |
| 401 | Falha na autenticação | Token de autenticação inválido |
| 500 | Erro interno do servidor | Falha do sistema interno |

## Erros de API do PostgreSQL

| Código de erro e estado da conexão | Descrição | Causa possível |
| ------------------------------- | ----------- | -------------- |
| **Start 28P01** - autenticação | Senha inválida | Token de autenticação inválido |
| **Start 28000** - autenticação | Tipo de autorização inválido | Tipo de autorização inválido. Deve ser `AuthenticationCleartextPassword`. |
| **Start 42P12** - autenticação | Nenhuma tabela encontrada | Nenhuma tabela encontrada para uso |
| **Query 42601** | Erro de sintaxe | Erro de comando ou sintaxe inválido |
| **Query 58000** | Erro do sistema | Falha do sistema interno |
| **Query 42P01** | Tabela não encontrada | A tabela especificada no query não foi encontrada |
| **Query 42P07** | A tabela existe | A tabela já existe com o mesmo nome (CREATE TABLE) |
| **Query 53400** | LIMITE excede o valor máximo | O usuário especificou uma cláusula LIMIT superior a 100.000 |
| **Query 53400** | Tempo limite da declaração | A declaração em tempo real enviada demorou mais de 10 minutos |
| **08P01** N/D | Tipo de mensagem não suportado | Tipo de mensagem não suportado |
