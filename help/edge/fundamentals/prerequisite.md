---
title: Pré-requisitos para usar o SDK da Web da Adobe Experience Platform
description: Saiba mais sobre os pré-requisitos para usar o Adobe Experience Platform Web SDK.
keywords: Domínio próprio; CNAME; esquema; criar esquema; iniciar; extensão do sdk da aep web; extensão; id de configuração; ferramenta de configuração; elemento de dados; criar elemento de dados; objeto XDM; enviar evento; enviar evento;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 5f3b82edbc52d96cad13932be1d201e275780f3c
workflow-type: tm+mt
source-wordcount: '318'
ht-degree: 0%

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
