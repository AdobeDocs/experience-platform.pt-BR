---
keywords: Experience Platform;introdução;ia de atribuição;tópicos populares;entrada de ia de atribuição;saída de ia de atribuição;solução de problemas de ia de atribuição;erros de ia de atribuição
solution: Experience Platform, Real-Time Customer Data Platform
feature: Attribution AI
title: solução de problemas de erros do Attribution AI
description: Encontre respostas para erros comuns no Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 07a110f6d293abff38804b939014e28f308e3b30
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# solução de problemas de erros do Attribution AI

Este documento fornece respostas a perguntas frequentes sobre o Attribution AI.

## Não é possível acessar o Attribution AI no Chrome incógnito

Erros de carregamento no modo incógnito do Google Chrome estão presentes devido a atualizações nas configurações de segurança do modo incógnito do Google Chrome. O problema está sendo ativamente trabalhada com a Chrome para tornar experience.adobe.com um domínio confiável.

<img src="./images/faq/error.PNG" width="500" /><br />

### Correção recomendada

Para contornar esse problema, é necessário adicionar experience.adobe.com como um site que sempre pode usar cookies. Comece navegando até **chrome://settings/cookies**. Em seguida, role para baixo até a seção **Comportamentos personalizados**, seguida pelo botão **Adicionar** ao lado de &quot;sites que sempre podem usar cookies&quot;. Na janela pop-up exibida, copie e cole `[*.]experience.adobe.com` e marque a caixa de seleção **Incluir cookies de terceiros** neste site. Depois de concluído, selecione **Adicionar** e recarregar o Attribution AI incógnito.

![correção recomendada](./images/faq/cookies2.gif)
