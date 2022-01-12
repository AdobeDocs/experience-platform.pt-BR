---
keywords: Experience Platform, home, tópicos populares, solução de problemas, controle de acesso
solution: Experience Platform
title: Guia de solução de problemas de controle de acesso
topic-legacy: troubleshooting guide
description: Este documento fornece respostas a perguntas frequentes sobre o controle de acesso no Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: dc81da58594fac4ce304f9d030f2106f0c3de271
workflow-type: tm+mt
source-wordcount: '321'
ht-degree: 0%

---

# Guia de solução de problemas de controle de acesso

Este documento fornece respostas a perguntas frequentes sobre o controle de acesso no Adobe Experience Platform. Para perguntas e solução de problemas relacionados a outros [!DNL Platform] consulte os [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] utiliza perfis de produto no [Adobe Admin Console](https://adminconsole.adobe.com) para fornecer controle de acesso baseado em funções, vinculando usuários com permissões e sandboxes.  Consulte a [visão geral do controle de acesso](home.md) para obter mais informações.

## Onde posso encontrar minhas permissões de acesso atuais?

Se você for um administrador de sistema, administrador de produto ou administrador de perfil de produto da Organização IMS, poderá visualizar o perfil de produto atribuído e as permissões fornecidas na Adobe Admin Console. Consulte a [guia do usuário de controle de acesso](./ui/overview.md) para obter instruções sobre como navegar no [!DNL Admin Console] para exibir as permissões de um perfil de produto.

Se você não for um administrador, ainda poderá visualizar suas permissões de acesso atuais enviando uma solicitação para a `/acl/effective-policies` endpoint na API de controle de acesso. Consulte a seção &quot;Exibir políticas eficazes&quot; em [guia do desenvolvedor do controle de acesso](./api/effective-policies.md) para obter mais informações.

## Alguns recursos na [!DNL Platform] A interface do usuário não está disponível. Como o acesso a esses recursos é controlado por permissões?

Se você não tiver permissões de acesso para um [!DNL Platform] , esse recurso será oculto ou esmaecido na variável [!DNL Experience Platform] IU. Por exemplo, para visualizar o &quot;[!UICONTROL Perfis]&quot;, você deve ter o &quot;[!UICONTROL Exibir perfis]&quot; ou &quot;[!UICONTROL Gerenciar perfis]&quot; permissões. Entre em contato com o administrador se precisar de permissões adicionais para [!DNL Experience Platform] recursos.

## Como as permissões são agrupadas e qual grupo contém a permissão que deseja usar?

As permissões são agrupadas e categorizadas pela variável [!DNL Platform] recursos aos quais elas se aplicam (como [!DNL Data Management] e [!DNL Profile Management]). Para obter uma lista completa das permissões disponíveis e os grupos aos quais pertencem, consulte o [seção de permissões](home.md#permissions) na visão geral do controle de acesso.

Consulte a [visão geral do controle de acesso](home.md) para obter mais informações sobre como fornecer controle de acesso com base em funções.
