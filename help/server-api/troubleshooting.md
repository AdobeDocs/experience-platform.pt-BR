---
title: Solução de problemas
description: Saiba como solucionar erros ao usar a API do Edge Network Server.
exl-id: f0223fca-30ec-4229-93a5-3faa6cef5482
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 2%

---

# Solução de problemas

A API do Servidor de Rede de Borda da Adobe Experience Platform permite capturar informações de depuração de serviços, pois os eventos são processados por meio do pipeline de coleta de dados da Rede de Borda.

O mesmo mecanismo utilizado pela [Experience Platform Debugger](https://experienceleague.adobe.com/docs/debugger-learn/tutorials/experience-platform-debugger/introduction-to-the-experience-platform-debugger.html?lang=en) O permite depurar implementações baseadas em API.

Usando [Projeto Griffon](https://aep-sdks.gitbook.io/docs/beta/project-griffon), é possível criar uma ID de sessão de depuração que possa ser usada nas solicitações da Rede de borda para rastrear os eventos.
