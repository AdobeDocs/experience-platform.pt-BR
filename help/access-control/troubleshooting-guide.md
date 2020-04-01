---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia de solução de problemas do Controle de acesso
topic: troubleshooting guide
translation-type: tm+mt
source-git-commit: c4da32630d3a6476956347b76d611553ef1853fa

---


# Guia de solução de problemas do Controle de acesso

Este documento fornece respostas para perguntas frequentes sobre o controle de acesso na Adobe Experience Platform. Para questões e solução de problemas relacionados a outros serviços da plataforma, consulte o guia [de solução de problemas da plataforma](../landing/troubleshooting.md)Experience.

A Experience Platform aproveita perfis de produtos no [Adobe Admin Console](http://adminconsole.adobe.com) para fornecer **controles de acesso** baseados em funções, vinculando usuários com permissões e caixas de proteção.  Consulte a visão geral [do](home.md) controle de acesso para obter mais informações.

## Onde posso encontrar minhas permissões de acesso atuais?

Se você for administrador do sistema, administrador do produto ou administrador do perfil do produto para a organização IMS, poderá visualização o perfil do produto atribuído e as permissões que ele fornece no Adobe Admin Console. Consulte o guia [do usuário do](./ui/overview.md) controle de acesso para obter instruções sobre como navegar pelo Admin Console para visualização de permissões de perfis de produtos.

Se você não for um administrador, ainda será possível visualização das permissões de acesso atuais enviando uma solicitação para o ponto de extremidade `/acl/effective-policies` na API do Controle de acesso. Consulte a seção &quot;Políticas eficazes para a Visualização&quot; no guia [do desenvolvedor do](./api/effective-policies.md) controle de acesso para obter mais informações.

## Alguns recursos na interface do usuário da plataforma não estão disponíveis. Como o acesso a esses recursos é controlado por permissões?

Se você não tiver permissões de acesso para um recurso específico da Plataforma, esse recurso ficará oculto ou esmaecido na interface do usuário da plataforma de experiência. Por exemplo, para visualização na guia &quot;Perfis&quot;, é necessário ter as permissões &quot;Perfis de Visualização&quot; ou &quot;Gerenciar Perfis&quot;. Entre em contato com o administrador se precisar de permissões adicionais para os recursos da plataforma de experiência.

## Como as permissões são agrupadas e qual grupo contém a permissão que eu quero usar?

As permissões são agrupadas e categorizadas pelos recursos da Plataforma aos quais se aplicam (como Gerenciamento de Gestões de dados e Perfis). Para obter uma lista completa das permissões disponíveis e dos grupos aos quais pertencem, consulte a seção [](home.md#permissions) Permissões na visão geral do controle de acesso.

Consulte a visão geral [do](home.md) controle de acesso para obter mais informações sobre como fornecer controles de acesso baseados em funções.