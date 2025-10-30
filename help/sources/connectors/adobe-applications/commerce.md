---
title: Adobe Commerce Source Connector
description: Saiba como usar a fonte do Adobe Commerce para trazer seus dados comerciais para a Experience Platform.
last-substantial-update: 2023-12-13T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Adobe Commerce

O Adobe Commerce é uma plataforma de comércio B2B e B2C ágil que permite que comerciantes e marcas acelerem a receita por meio de experiências de comércio digital centradas no cliente em espaços online e físicos.

As Fontes do Adobe Experience Platform oferecem suporte à integração do Adobe Commerce para permitir que os comerciantes enviem dados de vitrine e back-office para a Experience Platform Edge Network, para que outros produtos da Adobe Experience Cloud, como a Adobe Analytics e a Adobe Target, possam usar os dados do [!DNL Commerce].

* **Eventos de vitrine**: Capture interações do comprador como `View Page`, `View Product` e `Add to Cart`. Para comerciantes B2B, os eventos de vitrine também capturam [listas de requisições](https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html).
* **Eventos do back office**: captura informações sobre o status de um pedido, como se um pedido foi feito, cancelado, reembolsado, remetido ou concluído.

>[!NOTE]
>
>Os dados capturados no Adobe Commerce não incluem informações de identificação pessoal (PII). Todos os identificadores de usuário, como IDs de cookies e endereços IP, são estritamente anônimos.

## Pré-requisitos

Para conectar o Adobe Commerce ao Experience Platform, você deve ter o seguinte:

* Adobe Commerce 2.4.3 ou mais recente.
* Uma Adobe ID e ID de organização válidas.
* Acesso à [extensão da Camada de Dados do Cliente Adobe](../../../tags/extensions/client/client-data-layer/overview.md). Essa extensão é necessária para coletar dados de evento da loja.
* Qualificações para outros produtos Adobe DX.

## Etapas de integração

Para integrar completamente sua conta de origem do Adobe Commerce, siga as etapas descritas abaixo, juntamente com a documentação correspondente.

* [Instale a [!DNL Data Connection] extensão](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/install.html) para o Adobe Commerce. Você pode baixar a extensão do conector do [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* Depois de instalar com êxito a extensão do conector, entre na sua conta da Adobe no Experience Cloud e [confirme a ID da organização](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Essa ID está associada à empresa provisionada pela Experience Cloud. Ela é formatada como uma sequência de 24 caracteres alfanuméricos e inclui um `@AdobeOrg` obrigatório.
* Em seguida, crie ou atualize seu esquema do Experience Data Model (XDM) com seus grupos de campos específicos do Commerce. Para obter etapas detalhadas sobre como adicionar grupos de campos específicos do Commerce ao esquema XDM, leia o guia em [adicionar grupos de campos a um esquema XDM](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/update-xdm.html).
* Depois que o esquema for configurado, você deverá criar um conjunto de dados com base no novo esquema. Esse conjunto de dados conterá os dados [!DNL Commerce] que você enviar. Para obter etapas detalhadas sobre como criar um conjunto de dados para dados do [!DNL Commerce], leia o manual sobre [envio de dados para o Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* Em seguida, crie um fluxo de dados e selecione o esquema XDM que contém seus grupos de campos específicos do Commerce. Para obter mais informações sobre sequências de dados, leia a [visão geral sobre sequências de dados](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html).
* Em seguida, conecte sua instância do Adobe Commerce ao [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). Isso permite que sua instância do Commerce seja implantada como SaaS (Software as a Service).
* Com todas as configurações acima concluídas, agora é possível conectar-se ao Experience Platform configurando o Commerce Services Connector e a extensão [!DNL Data Connection] usando o [!DNL Commerce Admin]. Para obter mais informações sobre esta etapa final, leia o guia em [conectando dados do Commerce ao Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/data-connection/fundamentals/connect-data.html).
