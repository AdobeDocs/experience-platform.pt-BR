---
keywords: Experience Platform;página inicial;tópicos populares;solução de problemas;controle de acesso
solution: Experience Platform
title: Guia de solução de problemas de controle de acesso
description: Este documento fornece respostas a perguntas frequentes sobre o controle de acesso no Adobe Experience Platform.
exl-id: c299c0c4-dbee-4e6d-8af4-2446444bed69
source-git-commit: 7b197f253aa5ce04a682040814cf749407154ebc
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Guia de solução de problemas de controle de acesso

Este documento fornece respostas a perguntas frequentes sobre o controle de acesso no Adobe Experience Platform. Para perguntas e solução de problemas relacionados a outros [!DNL Platform] serviços, consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

[!DNL Experience Platform] utiliza perfis de produto no [Adobe Admin Console](https://adminconsole.adobe.com) para fornecer controle de acesso com base em funções, vinculando usuários com permissões e sandboxes.  Consulte a [visão geral do controle de acesso](home.md) para obter mais informações.

## Onde posso encontrar minhas permissões de acesso atuais?

Se você for um administrador de sistema, administrador de produto ou administrador de perfil de produto para sua Organização IMS, poderá exibir o perfil de produto atribuído e as permissões fornecidas na Adobe Admin Console. Consulte a [guia do usuário de controle de acesso](./ui/overview.md) para obter instruções sobre como navegar no [!DNL Admin Console] para exibir as permissões de um perfil de produto.

Se você não for um administrador, ainda poderá visualizar suas permissões de acesso atuais enviando uma solicitação para o `/acl/effective-policies` ponto de extremidade na API de controle de acesso. Consulte a seção &quot;Exibir políticas efetivas&quot; em [guia do desenvolvedor de controle de acesso](./api/effective-policies.md) para obter mais informações.

## Alguns recursos na [!DNL Platform] A interface do usuário não está disponível. Como o acesso a esses recursos é controlado por permissões?

Se você não tiver permissões de acesso para um [!DNL Platform] recurso, esse recurso ficará oculto ou esmaecido na [!DNL Experience Platform] IU. Por exemplo, para visualizar o &quot;[!UICONTROL Perfis]&quot;, você deve ter a tag &quot;[!UICONTROL Exibir perfis]&quot; ou &quot;[!UICONTROL Gerenciar perfis]&quot;. Entre em contato com o administrador se precisar de permissões adicionais para [!DNL Experience Platform] recursos.

## Como as permissões são agrupadas e qual grupo contém a permissão que desejo usar?

As permissões são agrupadas e categorizadas pelo [!DNL Platform] recursos aos quais se aplicam (como [!DNL Data Management] e [!DNL Profile Management]). Para obter uma lista completa das permissões disponíveis e os grupos aos quais elas pertencem, consulte a [seção de permissões](home.md#permissions) na visão geral do controle de acesso.

Consulte a [visão geral do controle de acesso](home.md) para obter mais informações sobre como fornecer controle de acesso baseado em função.

## O que acontece com as permissões após a migração do Adobe IO para a Business ID?

O controle de acesso usa a ID do usuário (uma ID exclusiva interna atribuída a um usuário) para conceder permissões. Quando uma organização for migrada do Adobe ID para a Business ID, todas as permissões definidas para os usuários serão perdidas, pois as alterações na ID do usuário e o controle de acesso usarão a ID do usuário recém-gerada. Se sua organização migrou para a Business ID, entre em contato com o representante da Adobe para migrar sua ID de usuário da Adobe ID para a Business ID.
