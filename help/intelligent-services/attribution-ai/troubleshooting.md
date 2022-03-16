---
keywords: Experience Platform, introdução, ai de atribuição, tópicos populares, entrada de ai de atribuição, saída de ai de atribuição, solução de problemas de ai de atribuição, erros de ai de atribuição
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
feature: Attribution AI
title: Solução de problemas de erros de Attribution AI
description: Encontre respostas para erros comuns no Attribution AI.
type: Documentation
source-git-commit: 896dda631cd4182f278de0607bea442d8366fe8c
workflow-type: tm+mt
source-wordcount: '167'
ht-degree: 0%

---

# Solução de problemas de erros de Attribution AI

Este documento fornece respostas a perguntas frequentes sobre o Attribution AI.

## Não é possível acessar o Attribution AI no Chrome incógnito

Os erros de carregamento no modo incógnito do Google Chrome estão presentes devido às atualizações nas configurações de segurança do modo incógnito do Google Chrome. O problema está sendo trabalhado ativamente com o Chrome para tornar o experience.adobe.com um domínio confiável.

<img src="./images/faq/error.PNG" width="500" /><br />

### Correção recomendada

Para contornar esse problema, você precisa adicionar experience.adobe.com como um site que sempre pode usar cookies. Comece navegando até **chrome://settings/cookies**. Em seguida, role para baixo até o **Comportamentos personalizados** seção seguida por selecionar a variável **Adicionar** ao lado de &quot;sites que sempre podem usar cookies&quot;. No recipiente que aparece, copie e cole `[*.]experience.adobe.com` em seguida, selecione o **Inclusão de cookies de terceiros** nesta caixa de seleção de site. Depois de concluir, selecione **Adicionar** e recarregar o Attribution AI no incógnito.

![correção recomendada](./images/faq/cookies2.gif)
