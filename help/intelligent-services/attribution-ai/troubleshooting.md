---
keywords: Experience Platform;introdução;ia de atribuição;tópicos populares;entrada de ia de atribuição;saída de ia de atribuição;solução de problemas de ia de atribuição;erros de ia de atribuição
solution: Experience Platform, Real-time Customer Data Platform
feature: Attribution AI
title: solução de problemas de erros do Attribution AI
description: Encontre respostas para erros comuns no Attribution AI.
type: Documentation
exl-id: c2ff700a-1e36-4ba2-876c-9f8b56344241
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# solução de problemas de erros do Attribution AI

Este documento fornece respostas a perguntas frequentes sobre o Attribution AI.

## Não é possível acessar o Attribution AI no Chrome incógnito

Erros de carregamento no modo incógnito do Google Chrome estão presentes devido a atualizações nas configurações de segurança do modo incógnito do Google Chrome. O problema está sendo ativamente trabalhada com o Chrome para tornar o experience.adobe.com um domínio confiável.

<img src="./images/faq/error.PNG" width="500" /><br />

### Correção recomendada

Para contornar esse problema, é necessário adicionar experience.adobe.com como um site que sempre pode usar cookies. Comece navegando até **chrome://settings/cookies**. Em seguida, role para baixo até o **Comportamentos personalizados** seção seguida pela seleção do **Adicionar** botão ao lado de &quot;sites que sempre podem usar cookies&quot;. No popover exibido, copie e cole `[*.]experience.adobe.com` em seguida, selecione o **Inclusão de cookies de terceiros** nesta caixa de seleção do site. Após a conclusão, selecione **Adicionar** e recarregar o Attribution AI incógnito.

![correção recomendada](./images/faq/cookies2.gif)
