---
title: Visão geral da API do Servidor de rede de borda
description: Saiba o que é a API do servidor de rede de borda e como usá-la.
seo-description: Learn what the Edge Network Server API is and how you can use it.
keywords: coleta de dados, coleta, Adobe Experience Platform Edge Network, api do servidor;
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 5%

---

# Visão geral da API do Servidor de rede de borda {#overview}

A rede de borda Adobe Experience Platform oferece uma maneira otimizada para os clientes interagirem com qualquer serviço Adobe Experience Cloud ou Adobe Experience Platform Edge.

O [!DNL Edge Network Server API] O pode ser usado para uma variedade de casos de uso de coleta de dados, personalização, publicidade e marketing. O [!DNL Server API] podem ser usados em servidores, [!DNL IoT] dispositivos, decodificadores e uma variedade de outros dispositivos.

Como a variável [!DNL Server API] não depende de nenhuma biblioteca para carregar, ela fornece uma maneira extremamente rápida de interagir com a rede de borda da Adobe Experience Platform e com as soluções compatíveis.

Os benefícios do [!DNL Server API] a arquitetura inclui:

* Redução do tempo de carregamento da página
* Latência aprimorada
* Coleta de dados primários
* Comunicação simplificada do lado do servidor entre serviços

O [!DNL Server API] O suporta coleta de dados interativa e em lote, por meio de dois endpoints dedicados:

1. O endpoint interativo oferece suporte à comunicação com os serviços da Adobe Experience Platform e da Adobe Experience Cloud que oferecem suporte à segmentação avançada, personalização e outros casos de uso de marketing.
2. O endpoint de lote permitirá o envio de solicitações em lote quando os dados precisarem ser integrados sem receber uma resposta dos aplicativos que estão sendo chamados.

O [!DNL Server API] O suporta o seguinte tipo de solicitações:

* Solicitações autenticadas via [Adobe I/O](https://developer.adobe.com/), usando o novo `server.adobedc.net` endpoint .
* Solicitações não autenticadas por meio do `edge.adobedc.net` endpoint .

Isso permite casos de uso que permitem a coleta segura e autenticada de dados confidenciais, de acordo com as políticas de privacidade da sua organização. Além da autenticação, a API do servidor suporta a marcação de conjuntos de dados para aceitar apenas a comunicação autenticada por meio da API.

Assista ao vídeo abaixo para obter uma visão geral simplificada da API do servidor.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
