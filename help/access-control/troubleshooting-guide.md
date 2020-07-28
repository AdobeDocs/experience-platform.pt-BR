---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia de solução de problemas do Controle de acesso
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: 73a492ba887ddfe651e0a29aac376d82a7a1dcc4
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# Guia de solução de problemas do Controle de acesso

Este documento fornece respostas para perguntas frequentes sobre o controle de acesso no Adobe Experience Platform. Para questões e solução de problemas relacionados a outros [!DNL Platform] serviços, consulte o guia [de solução de problemas do](../landing/troubleshooting.md)Experience Platform.

[!DNL Experience Platform] aproveita perfis de produtos no [Adobe Admin Console](http://adminconsole.adobe.com) para fornecer **controles de acesso** baseados em funções, vinculando usuários com permissões e caixas de proteção.  Consulte a visão geral [do](home.md) controle de acesso para obter mais informações.

## Onde posso encontrar minhas permissões de acesso atuais?

Se você for um administrador do sistema, administrador do produto ou administrador do perfil do produto para a organização IMS, poderá visualização o perfil do produto atribuído e as permissões que ele fornece no Adobe Admin Console. Consulte o guia [do usuário do](./ui/overview.md) controle de acesso para obter instruções sobre como navegar até [!DNL Admin Console] a visualização das permissões de um perfil do produto.

Se você não for um administrador, ainda será possível visualização das permissões de acesso atuais enviando uma solicitação para o ponto de extremidade `/acl/effective-policies` na API do Controle de acesso. Consulte a seção &quot;Políticas eficazes para a Visualização&quot; no guia [do desenvolvedor do](./api/effective-policies.md) controle de acesso para obter mais informações.

## Alguns recursos na [!DNL Platform] interface do usuário não estão disponíveis. Como o acesso a esses recursos é controlado por permissões?

Se você não tiver permissões de acesso para um determinado [!DNL Platform] recurso, esse recurso ficará oculto ou esmaecido na [!DNL Experience Platform] interface do usuário. Por exemplo, para visualização na guia &quot;[!UICONTROL Perfis]&quot;, é necessário ter as permissões &quot;Perfis[!UICONTROL de]Visualização&quot; ou &quot;[!UICONTROL Gerenciar Perfis]&quot;. Entre em contato com o administrador se precisar de permissões adicionais para [!DNL Experience Platform] os recursos.

## Como as permissões são agrupadas e qual grupo contém a permissão que eu quero usar?

As permissões são agrupadas e categorizadas pelos [!DNL Platform] recursos aos quais se aplicam (como [!DNL Data Management] e [!DNL Profile Management]). Para obter uma lista completa das permissões disponíveis e dos grupos aos quais pertencem, consulte a seção [](home.md#permissions) Permissões na visão geral do controle de acesso.

Consulte a visão geral [do](home.md) controle de acesso para obter mais informações sobre como fornecer controles de acesso baseados em funções.