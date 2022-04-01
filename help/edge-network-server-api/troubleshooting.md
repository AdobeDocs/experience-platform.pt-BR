---
title: Solução de problemas
description: Saiba como solucionar erros ao usar a API do servidor de rede de borda do Adobe Experience Platform
seo-description: Learn how to troubleshoot errors when using the Adobe Experience Platform Edge Network Server API
keywords: rede de borda, gateway, api, solução de problemas, erros, griffon
source-git-commit: 2b501c9384fecb016489a21a308a595186153f03
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 1%

---


# Solução de problemas

A API do Servidor de Rede de Borda da Adobe Experience Platform permite capturar informações de depuração de serviços, pois os eventos são processados por meio do pipeline de coleta de dados da Rede de Borda.

O mesmo mecanismo utilizado pela [Experience Platform Debugger](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) O permite depurar implementações baseadas em API.

Usando [Projeto Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon), é possível criar uma ID de sessão de depuração que possa ser usada nas solicitações da Rede de borda para rastrear os eventos.

