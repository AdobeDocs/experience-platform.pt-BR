---
title: Visão geral da API do servidor de rede de borda
description: Saiba o que é a API do servidor de rede de borda e como usá-la.
seo-description: Learn what the Edge Network Server API is and how you can use it.
keywords: coleção de dados;coleção;Rede de borda da Adobe Experience Platform;api do servidor;
exl-id: 46bd8798-d7f9-405b-9ca8-856ad4aa688c
source-git-commit: f52603f7e65ac553e00a2b632857561cd07ae441
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 5%

---

# Visão geral da API do servidor de rede de borda {#overview}

A rede de borda da Adobe Experience Platform oferece uma maneira otimizada para os clientes interagirem com qualquer serviço de borda da Adobe Experience Cloud ou da Adobe Experience Platform.

A variável [!DNL Edge Network Server API] O pode ser usado para uma variedade de casos de uso de coleta de dados, personalização, publicidade e marketing. A variável [!DNL Server API] pode ser usado em servidores, [!DNL IoT] dispositivos, decodificadores de sinais e diversos outros dispositivos.

Uma vez que a [!DNL Server API] O não depende de bibliotecas para carregar, ele oferece uma maneira ultrarrápida de interagir com a Rede de borda da Adobe Experience Platform e as soluções compatíveis.

Os benefícios da [!DNL Server API] incluem:

* Tempo de carregamento de página reduzido
* Latência aprimorada
* Coleta de dados primários
* Comunicação simplificada do lado do servidor entre serviços

A variável [!DNL Server API] O é compatível com a coleta de dados interativa e em lote, por meio de dois endpoints dedicados:

1. O endpoint interativo oferece suporte à comunicação com os serviços do Adobe Experience Platform e da Adobe Experience Cloud que oferecem suporte à segmentação avançada, personalização e outros casos de uso de marketing.
2. O endpoint do lote permitirá que as solicitações sejam enviadas em lote quando os dados precisarem ser integrados sem receber uma resposta dos aplicativos que estão sendo chamados.

A variável [!DNL Server API] O é compatível com os seguintes tipos de solicitações:

* Solicitações autenticadas via [Adobe I/O](https://developer.adobe.com/), utilizando o novo `server.adobedc.net` terminal.
* Solicitações não autenticadas por meio do `edge.adobedc.net` terminal.

Isso permite casos de uso que permitem a coleta segura e autenticada de dados confidenciais, de acordo com as políticas de privacidade da sua organização. Além da autenticação, a API do servidor é compatível com a marcação de sequências de dados para aceitar apenas a comunicação autenticada por meio da API.

Assista ao vídeo abaixo para obter uma visão geral simplificada da API do servidor.

>[!VIDEO](https://video.tv.adobe.com/v/341448/)
