---
title: Pré-requisitos para usar o SDK da Web da Adobe Experience Platform
description: Saiba mais sobre os pré-requisitos para usar o Adobe Experience Platform Web SDK.
keywords: Domínio próprio; CNAME; esquema; criar esquema; iniciar; extensão do sdk da aep web; extensão; id de configuração; ferramenta de configuração; elemento de dados; criar elemento de dados; objeto XDM; enviar evento; enviar evento;
exl-id: 98ae69db-bc87-4ea3-b101-664ac53e7ae0
source-git-commit: 6a9882224cba08718c81a3aead237107b3e47726
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 0%

---

# Pré-requisitos para usar o SDK da Web da Adobe Experience Platform

Para usar o SDK da Web da Adobe Experience Platform, primeiro você deve:

- Tenha as permissões certas configuradas para usuários em sua organização. Todos os clientes do Experience Cloud têm acesso às ferramentas de Coleta de dados, cada usuário na organização precisará apenas de permissões para esquemas, identidades e conjuntos de dados. Para ler mais sobre como configurar essas permissões, consulte nossa documentação em [gerenciamento de permissões de coleta de dados](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=en).
- Recomenda-se ter o domínio próprio (CNAME) ativado. Se já tiver um CNAME para Adobe Analytics, use-o. O teste em desenvolvimento funciona sem um CNAME, mas o Adobe recomenda ter um antes de ir para a produção. Embora uma implementação CNAME não forneça benefícios em termos de duração do cookie, ela pode impedir que determinados bloqueadores de anúncios e navegadores menos comuns bloqueiem solicitações de SDK. Nesses casos, o uso de um CNAME pode impedir que sua coleta de dados seja interrompida para usuários que utilizam essas ferramentas.

>[!IMPORTANT]
>
>**Observe que, a partir de 10/11/20, as implementações CNAME primárias têm um prazo de 7 dias em todos os navegadores Safari e dispositivos iOS móveis.**

- Se seu site já estiver usando a variável [Serviço de ID de Experience Cloud](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html) no seu site, por meio da API de visitante ou da extensão do Serviço de ID de Experience Cloud no Adobe Experience Platform Launch, e você gostaria de continuar usando a extensão durante a migração para o SDK da Web da Adobe Experience Platform, é necessário usar a versão mais recente da API de visitante ou a extensão do Serviço de ID de Experience Cloud. Consulte [Migração de ID](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#identity) para obter mais informações.
