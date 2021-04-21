---
keywords: Experience Platform, home, tópicos populares, solução de problemas, controle de acesso
solution: Experience Platform
title: Guia de solução de problemas de controle de acesso
topic-legacy: troubleshooting guide
description: Este documento fornece respostas a perguntas frequentes sobre o controle de acesso no Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 0%

---

# Guia de solução de problemas de controle de acesso

Este documento fornece respostas a perguntas frequentes sobre o controle de acesso no Adobe Experience Platform. Para dúvidas e solução de problemas relacionados a outros serviços [!DNL Platform], consulte o [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] Usa perfis de produto no  [Adobe Admin ](http://adminconsole.adobe.com) Consoles para fornecer controle de acesso baseado em funções, vinculando usuários com permissões e sandboxes.  Consulte a [visão geral do controle de acesso](home.md) para obter mais informações.

## Onde posso encontrar minhas permissões de acesso atuais?

Se você for um administrador de sistema, administrador de produto ou administrador de perfil de produto da Organização IMS, poderá visualizar o perfil de produto atribuído e as permissões fornecidas na Adobe Admin Console. Consulte o [guia do usuário de controle de acesso](./ui/overview.md) para obter instruções sobre como navegar pelo [!DNL Admin Console] para visualizar as permissões de um perfil de produto.

Se você não for um administrador, ainda poderá visualizar suas permissões de acesso atuais enviando uma solicitação para o terminal `/acl/effective-policies` na API de Controle de Acesso. Consulte a seção &quot;Exibir políticas eficazes&quot; em [guia do desenvolvedor de controle de acesso](./api/effective-policies.md) para obter mais informações.

## Alguns recursos na interface do usuário [!DNL Platform] não estão disponíveis. Como o acesso a esses recursos é controlado por permissões?

Se você não tiver permissões de acesso para um recurso [!DNL Platform] específico, esse recurso ficará oculto ou esmaecido na interface do usuário [!DNL Experience Platform]. Por exemplo, para visualizar a guia &quot;[!UICONTROL Profiles]&quot;, você deve ter as permissões &quot;[!UICONTROL View Profiles]&quot; ou &quot;[!UICONTROL Manage Profiles]&quot;. Entre em contato com o administrador se precisar de permissões adicionais para os recursos [!DNL Experience Platform].

## Como as permissões são agrupadas e qual grupo contém a permissão que deseja usar?

As permissões são agrupadas e categorizadas pelos recursos [!DNL Platform] aos quais se aplicam (como [!DNL Data Management] e [!DNL Profile Management]). Para obter uma lista completa das permissões disponíveis e dos grupos aos quais pertencem, consulte a [seção de permissões](home.md#permissions) na visão geral do controle de acesso.

Consulte a [visão geral do controle de acesso](home.md) para obter mais informações sobre como fornecer controle de acesso baseado em funções.
