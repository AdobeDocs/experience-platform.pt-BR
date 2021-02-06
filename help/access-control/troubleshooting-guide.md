---
keywords: Experience Platform;home;popular topics;solução de problemas;controle de acesso;home;popular topics;troubleshooting;
solution: Experience Platform
title: Guia de solução de problemas do controle de acesso
topic: troubleshooting guide
description: Este documento fornece respostas para perguntas frequentes sobre o controle de acesso no Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---


# Guia de solução de problemas do controle de acesso

Este documento fornece respostas para perguntas frequentes sobre o controle de acesso no Adobe Experience Platform. Para questões e solução de problemas relacionados a outros serviços [!DNL Platform], consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] aproveita perfis de produtos no  [Adobe Admin ](http://adminconsole.adobe.com) Consolide para fornecer controles de acesso baseados em funções, vinculando usuários com permissões e caixas de proteção.  Consulte a [visão geral do controle de acesso](home.md) para obter mais informações.

## Onde posso encontrar minhas permissões de acesso atuais?

Se você for um administrador do sistema, administrador do produto ou administrador do perfil do produto para a organização IMS, poderá visualização o perfil do produto atribuído e as permissões que ele fornece no Adobe Admin Console. Consulte o [Guia do usuário do controle de acesso](./ui/overview.md) para obter instruções sobre como navegar [!DNL Admin Console] para visualização de permissões de perfil do produto.

Se você não for um administrador, ainda poderá visualização suas permissões de acesso atuais enviando uma solicitação para o terminal `/acl/effective-policies` na API do Controle de acesso. Consulte a seção &quot;Políticas eficazes de Visualização&quot; em [Guia do desenvolvedor do controle de acesso](./api/effective-policies.md) para obter mais informações.

## Alguns recursos na interface do usuário [!DNL Platform] não estão disponíveis. Como o acesso a esses recursos é controlado por permissões?

Se você não tiver permissões de acesso para um recurso específico [!DNL Platform], esse recurso ficará oculto ou esmaecido na interface do usuário [!DNL Experience Platform]. Por exemplo, para visualização da guia &quot;[!UICONTROL Perfis]&quot;, você deve ter as permissões &quot;[!UICONTROL Perfis de Visualização]&quot; ou &quot;[!UICONTROL Gerenciar Perfis]&quot;. Entre em contato com o administrador se precisar de permissões adicionais para os recursos [!DNL Experience Platform].

## Como as permissões são agrupadas e qual grupo contém a permissão que eu quero usar?

As permissões são agrupadas e categorizadas pelos recursos [!DNL Platform] aos quais se aplicam (como [!DNL Data Management] e [!DNL Profile Management]). Para obter uma lista completa das permissões disponíveis e dos grupos aos quais pertencem, consulte a seção [permissões](home.md#permissions) na visão geral do controle de acesso.

Consulte a [visão geral do controle de acesso](home.md) para obter mais informações sobre como fornecer controles de acesso baseados em funções.