---
solution: Experience Platform
title: Visão geral da coleção de dados
description: Saiba como enviar dados para o Adobe Experience Platform.
exl-id: 03ce5339-e68d-4adf-8c3c-82846a626dad
source-git-commit: 3d51f01d314587510d900d335dc92fedb8ac31e8
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 2%

---

# Visão geral da coleção de dados

O Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados de experiência do cliente de várias fontes e enviá-los para o Adobe Experience Platform Edge Network. Esses dados podem então ser enriquecidos, transformados e distribuídos para destinos Adobe ou que não sejam da Adobe.

A Adobe oferece suporte às seguintes linguagens de código com bibliotecas dedicadas para coleta de dados:

* **JavaScript**: para sites e aplicativos baseados na Web
* **Kotlin**: para dispositivos Android
* **Swift**: para dispositivos iOS
* **Brightscript**: Para dispositivos Roku
* **Flutter**: Para aplicativos Android + iOS usando Flutter
* **React Native**: para aplicativos Android + iOS usando o React Native

A interface das tags na Coleção de dados da Adobe Experience Platform inclui uma extensão para SDK da Web e SDK móvel.

Se nenhum dos SDKs acima atender às necessidades do seu projeto, você poderá usar a [API do Adobe Experience Platform Edge Network](https://developer.adobe.com/data-collection-apis/docs/) para enviar dados diretamente para a Adobe.

## Processo de coleta de dados

Em vez de instalar e implementar bibliotecas individuais separadas para cada produto da Adobe, você pode implementar um dos SDKs ou extensões de tag acima para agregar todos os dados desejados em uma única carga. Essa carga é enviada para uma [sequência de dados](/help/datastreams/overview.md) na Edge Network do Adobe Experience Platform.

![Diagrama da coleção de dados](assets/tags-sdks.png)

O Adobe Experience Platform Edge Network é uma rede de servidores distribuídos globalmente, rápida e confiável, capaz de receber e processar dados em uma enorme escala. Quando um fluxo de dados recebe dados, ele distribui esses dados para cada solução respectiva que você configurou. Os dados são transmitidos em um formato que cada produto entende.

![Diagrama de soluções da Adobe](assets/adobe-solutions.png)

Você também pode usar o [encaminhamento de eventos](/help/tags/ui/event-forwarding/overview.md) para transformar, enriquecer e enviar dados para qualquer destino que não seja da Adobe com baixa latência e sem nenhum código de implementação do lado do cliente.

![Diagrama de encaminhamento de eventos](assets/event-forwarding.png)
