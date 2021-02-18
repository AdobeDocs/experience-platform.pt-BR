---
title: Pré-requisitos para usar o Adobe Experience Platform Web SDK
description: Saiba mais sobre os pré-requisitos para usar o Adobe Experience Platform Web SDK.
keywords: domínio próprio;CNAME;schema;criar schema;iniciar;extensão sdk da Web;extensão;extensão;id de configuração;ferramenta de configuração;elemento de dados;criar elemento de dados;Objeto XDM;sendEvent;send Evento;
translation-type: tm+mt
source-git-commit: 69f2e6069546cd8b913db453dd9e4bc3f99dd3d9
workflow-type: tm+mt
source-wordcount: '270'
ht-degree: 0%

---


# Pré-requisitos para usar o Adobe Experience Platform Web SDK

Para usar o SDK da Web da plataforma, é necessário primeiro:

- Tenha sua organização provisionada para este recurso. (O acesso ao SDK da Web da plataforma é gratuito, caso você queira obter acesso, entre em contato com o Gerente de sucesso do cliente (CSM).
- Ter um domínio próprio (CNAME) ativado. Se você já tiver um CNAME para Adobe Analytics, use esse. Testar no desenvolvimento funciona sem um CNAME, mas é necessário um antes de ir para a produção.

>[!IMPORTANT]
>
>**Observe que a partir de 10/11/20, as implementações CNAME originais têm uma expiração de 7 dias em todos os navegadores Safari e dispositivos iOS móveis.**

- Esteja qualificado para a Adobe Experience Platform. Se você não tiver comprado a Adobe Experience Platform, o Adobe fornecerá o acesso necessário para uso de forma limitada com o SDK, sem custos adicionais.
- Se seu site já estiver usando o [serviço de ID do Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) em seu site, por meio da API do Visitante ou da extensão do serviço de ID do Experience Cloud dentro da Adobe Experience Platform Launch, e você quiser continuar usando-o durante a migração para o Adobe Experience Platform Web SDK, deverá usar a versão mais recente da API do Visitante ou a extensão do serviço de ID do Experience Cloud. Consulte [Migração de ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) para obter mais informações.
