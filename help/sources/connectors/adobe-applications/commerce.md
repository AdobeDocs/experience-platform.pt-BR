---
title: Conector de origem do Adobe Commerce
description: Saiba como usar a fonte do Adobe Commerce para trazer seus dados comerciais para o Experience Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: 8313e3d5-5c3d-448c-883c-b9386dbbb2f5
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 1%

---

# Adobe Commerce

O Adobe Commerce é uma plataforma de comércio B2B e B2C ágil que permite que comerciantes e marcas acelerem a receita por meio de experiências de comércio digital centradas no cliente em espaços online e físicos.

O Adobe Experience Platform Sources suporta a integração do Adobe Commerce para permitir que os comerciantes enviem dados da loja e do back office para a Rede de borda do Experience Platform, para que outros produtos da Adobe Experience Cloud, como o Adobe Analytics e o Adobe Target, possam usar [!DNL Commerce] dados.

* **Eventos da loja**: capture interações do comprador, como `View Page`, `View Product`, e `Add to Cart`. Para comerciantes B2B, os eventos da loja também capturam [listas de requisição](<https://experienceleague.adobe.com/docs/commerce-admin/b2b/requisition-lists/requisition-lists.html>).
* **Eventos de back office**: captura informações sobre o status de um pedido, como se um pedido foi colocado, cancelado, reembolsado, remetido ou concluído.

>[!NOTE]
>
>Os dados capturados no Adobe Commerce não incluem informações de identificação pessoal (PII). Todos os identificadores de usuário, como IDs de cookies e endereços IP, são estritamente anônimos.

## Pré-requisitos

Para conectar o Adobe Commerce ao Experience Platform, você deve ter o seguinte:

* Adobe Commerce 2.4.3 ou mais recente.
* Uma Adobe ID e ID de organização válidas.
* O acesso à [Extensão de camada de dados do cliente Adobe](../../../tags/extensions/client/client-data-layer/overview.md). Essa extensão é necessária para coletar dados de evento da loja.
* Qualificações para outros produtos Adobe DX.

## Etapas de integração

Para integrar completamente sua conta de origem do Adobe Commerce, siga as etapas descritas abaixo, juntamente com a documentação correspondente.

* [Instale a extensão do conector do Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/install.html) para Adobe Commerce. É possível baixar a extensão do conector em [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html).
* Depois de instalar com êxito a extensão do conector, entre na sua conta do Adobe no Experience Cloud e [confirmar a ID da organização](https://experienceleague.adobe.com/docs/core-services/interface/administration/organizations.html#concept_EA8AEE5B02CF46ACBDAD6A8508646255). Essa ID está associada à empresa de Experience Cloud provisionados. Ele é formatado como uma sequência de 24 caracteres alfanuméricos e inclui um caractere `@AdobeOrg`.
* Em seguida, crie ou atualize seu esquema do Experience Data Model (XDM) com seus grupos de campos específicos do Commerce. Para obter etapas detalhadas sobre como adicionar grupos de campos específicos do Commerce ao esquema XDM, leia o guia em [adicionar grupos de campos a um esquema XDM](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/update-xdm.html).
* Depois que o esquema for configurado, você deverá criar um conjunto de dados com base no novo esquema. Esse conjunto de dados conterá a variável [!DNL Commerce] dados que você envia. Para obter etapas detalhadas sobre como criar um conjunto de dados para [!DNL Commerce] dados, leia o guia em [envio de dados para o Experience Platform](https://experienceleague.adobe.com/docs/platform-learn/implement-mobile-sdk/experience-cloud/platform.html#create-a-dataset).
* Em seguida, crie um fluxo de dados e selecione o esquema XDM que contém seus grupos de campos específicos do Commerce. Para obter mais informações sobre sequências de dados, leia o [visão geral dos fluxos de dados](https://experienceleague.adobe.com/docs/experience-platform/datastreams/overview.html?lang=pt-BR).
* Em seguida, você deve conectar sua instância do Adobe Commerce à [Conector dos Commerce Services](https://experienceleague.adobe.com/docs/commerce-merchant-services/user-guides/integration-services/saas.html). Isso permite que sua instância do Commerce seja implantada como SaaS (Software as a Service).
* Com todas as configurações acima concluídas, agora é possível conectar-se ao Experience Platform configurando o Conector dos Commerce Services e o Conector do Experience Platform usando o [!DNL Commerce Admin]. Para obter mais informações sobre esta etapa final, leia o guia em [conexão de dados do Commerce ao Experience Platform](https://experienceleague.adobe.com/docs/commerce-merchant-services/experience-platform-connector/fundamentals/connect-data.html).
