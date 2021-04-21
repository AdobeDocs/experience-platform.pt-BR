---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, guia de solução de problemas, perguntas frequentes, solução de problemas;
solution: Experience Platform
title: Guia de solução de problemas do serviço de query
topic-legacy: troubleshooting
description: Este documento contém informações sobre códigos de erro comuns encontrados e as possíveis causas.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '177'
ht-degree: 3%

---

# [!DNL Query Service] Guia de solução de problemas

## Erros da API REST

| Código de status HTTP | Descrição | Causas possíveis |
| ---------------- | ----------- | --------------- |
| 400 | Solicitação inválida | Consulta malformada ou ilegal |
| 401° | Falha na autenticação | Token de autenticação inválido |
| 500 | Erro interno do servidor | Falha do sistema interno |

## Erros da API PostgreSQL

| Código de erro e estado de conexão | Descrição | Causa Possível |
| ------------------------------- | ----------- | -------------- |
| **28P01** Inicialização - autenticação | Senha inválida | Token de autenticação inválido |
| **28000** Inicialização - autenticação | Tipo de autorização inválido | Tipo de autorização inválido. Deve ser `AuthenticationCleartextPassword`. |
| **42P12** Inicialização - autenticação | Nenhuma tabela encontrada | Nenhuma tabela encontrada para uso |
| **42601** Consulta | Erro de sintaxe | Comando ou erro de sintaxe inválido |
| **58000** Consulta | Erro do sistema | Falha do sistema interno |
| **42P01** Consulta | Tabela não encontrada | A tabela especificada na consulta não foi encontrada |
| **42P07** Consulta | Tabela existe | A tabela já existe com o mesmo nome (CRIAR TABELA) |
| **53400** Consulta | LIMITE excede o valor máximo | O usuário especificou uma cláusula LIMIT superior a 100.000 |
| **53400** Consulta | Tempo limite do demonstrativo | A declaração ao vivo enviada demorou mais de 10 minutos |
| **08P01** N/D | Tipo de mensagem não suportado | Tipo de mensagem não suportado |
