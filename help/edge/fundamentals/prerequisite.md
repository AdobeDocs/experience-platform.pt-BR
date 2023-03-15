---
title: Pré-requisitos para usar o SDK da Web da Adobe Experience Platform
description: Saiba mais sobre os pré-requisitos para usar o Adobe Experience Platform Web SDK.
keywords: domínio próprio;CNAME;esquema;criar esquema;iniciar;extensão sdk da web da aep;extensão;id de configuração;ferramenta de configuração;elemento de dados;criar elemento de dados;Objeto XDM;sendEvent;enviar Evento;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 6a9882224cba08718c81a3aead237107b3e47726
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Pré-requisitos para usar o SDK da Web da Adobe Experience Platform

Para usar o SDK da Web da Adobe Experience Platform, primeiro é necessário:

- Ter as permissões certas configuradas para usuários em sua organização. Todos os clientes do Experience Cloud têm acesso às ferramentas de Coleta de dados. Cada usuário na organização só precisará de permissões para Esquemas, Identidades e Fluxos de dados. Para saber mais sobre como configurar essas permissões, consulte nossa documentação em [gerenciamento de permissões de coleta de dados](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).
- É recomendável ter o CNAME (domínio próprio) ativado. Se você já tiver um CNAME do Adobe Analytics, deverá usá-lo. Os testes no desenvolvimento funcionam sem um CNAME, mas o Adobe recomenda ter um antes de você ir para a produção. Embora uma implementação CNAME não forneça benefícios em termos de tempo de vida do cookie, ela pode impedir que determinados bloqueadores de anúncios e navegadores menos comuns bloqueiem solicitações do SDK. Nesses casos, o uso de um CNAME pode impedir que a coleção de dados seja interrompida para usuários que utilizam essas ferramentas.

>[!IMPORTANT]
>
>**Observe que a partir de 10/11/20, implementações CNAME primárias têm uma expiração de 7 dias em todos os navegadores Safari e dispositivos móveis iOS.**

- Se o site já estiver usando o [Serviço de ID Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) no seu site, por meio da API de visitante ou da extensão do Serviço de ID de Experience Cloud no Adobe Experience Platform Launch, e você deseja continuar usando-o ao migrar para o SDK da Web da Adobe Experience Platform, é necessário usar a versão mais recente da API de visitante ou a extensão do Serviço de ID de Experience Cloud. Consulte [Migração de ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) para obter mais informações.
