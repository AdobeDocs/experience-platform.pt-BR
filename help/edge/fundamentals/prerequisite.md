---
title: Pré-requisitos para usar o SDK da Web da Adobe Experience Platform
description: Saiba mais sobre os pré-requisitos para usar o Adobe Experience Platform Web SDK.
keywords: Domínio próprio; CNAME; esquema; criar esquema; iniciar; extensão do sdk da aep web; extensão; id de configuração; ferramenta de configuração; elemento de dados; criar elemento de dados; objeto XDM; enviar evento; enviar evento;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 9d3965be1956de754f0d2a82178bf5dcd871e239
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# Pré-requisitos para usar o SDK da Web da Adobe Experience Platform

Para usar o SDK da Web da plataforma, primeiro você deve:

- Tenha sua organização provisionada para esse recurso. (O acesso ao SDK da Web da plataforma é gratuito, caso você queira obter acesso, entre em contato com o Gerente de sucesso do cliente (CSM).
- Recomenda-se ter o domínio próprio (CNAME) ativado. Se você já tiver um CNAME para Adobe Analytics, use-o. O teste em desenvolvimento funciona sem um CNAME, mas o Adobe recomenda ter um antes de ir para a produção. Embora uma implementação CNAME não forneça benefícios em termos de duração do cookie, ela pode impedir que determinados bloqueadores de anúncios e navegadores menos comuns bloqueiem solicitações de SDK. Nesses casos, o uso de um CNAME pode impedir que sua coleta de dados seja interrompida para usuários que utilizam essas ferramentas.

>[!IMPORTANT]
>
>**Observe que, a partir de 10/11/20, as implementações CNAME primárias têm um prazo de 7 dias em todos os navegadores Safari e dispositivos iOS móveis.**

- Tenha direito ao Adobe Experience Platform. Se você não tiver comprado o Adobe Experience Platform, o Adobe fornecerá o acesso necessário para uso de forma limitada com o SDK, sem custos adicionais.
- Se o seu site já estiver usando o [Experience Cloud ID Service](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) em seu site, por meio da API de visitante ou da extensão do Serviço de Experience Cloud ID no Adobe Experience Platform Launch, e você quiser continuar usando o serviço durante a migração para o Adobe Experience Platform Web SDK, será necessário usar a versão mais recente da API de visitante ou a extensão do Serviço de Experience Cloud ID. Consulte [Migração de ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) para obter mais informações.

## Gerenciamento de permissões para o Adobe Experience Platform Web SDK

O uso do Adobe Experience Platform não requer permissões especiais, mas você precisa ter as [permissões](https://experienceleague.adobe.com/docs/experience-platform/access-control/home.html?lang=br) certas para criar seus esquemas no Adobe Experience Platform. As permissões mínimas necessárias podem ser encontradas na categoria Modelagem de dados e identidades .

![](../images/AEP-permission-categories.png)

Na categoria Modelagem de dados, conceda aos usuários as permissões Gerenciar esquemas e Visualizar esquemas .

![](../images/data-modeling-permissions.png)

Na categoria Identity Management , conceda aos usuários as permissões Gerenciar namespaces de identidade e Exibir namespaces de identidade .

![](../images/identity-management-permissions.png)
