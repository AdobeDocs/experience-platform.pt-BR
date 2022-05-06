---
keywords: Experience Platform, serviço de consulta, serviço de consulta, query
title: Exemplo de caso de uso para o serviço de consulta Adobe Experience Platform
topic-legacy: tutorial
description: Um exemplo completo para demonstrar a versatilidade e os benefícios do Adobe Experience Platform Query Service.
source-git-commit: 00039961bcda8e77bcff3cee36da422b3e466f52
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 2%

---

# Exemplo de caso de uso para Adobe Experience Platform [!DNL Query Service]

Este documento e a apresentação de vídeo complementar fornecem um fluxo de trabalho completo de alto nível demonstrando como o Adobe Experience Platform [!DNL Query Service] beneficia os insights estratégicos de negócios de sua organização. Usando um caso de uso de abandono de navegação como exemplo, este guia ilustra os seguintes conceitos principais:

* A principal importância do processamento de dados para maximizar o potencial do Adobe Experience Platform
* Maneiras de criar a query com base na arquitetura de dados existente.
* Garanta a qualidade dos dados que atenda às suas necessidades e aos métodos para atenuar as falhas.
* O processo para agendar uma consulta para ser executada em uma frequência definida para uso downstream na segmentação e destinos para personalização.
* A facilidade de os profissionais de marketing incluírem atributos derivados em seus segmentos por meio do poder da [!DNL Query Service].

## Objetivos {#objectives}

Essa demonstração do workflow depende de vários serviços da Adobe Experience Platform. Caso queira seguir em frente, é recomendável ter uma boa compreensão dos seguintes recursos e serviços:

* O [noções básicas da composição do esquema do Experience Data Model (XDM)](../../xdm/schema/composition.md)
* Como [criar conjuntos de dados e assimilar dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html?lang=pt-BR)
* Como [assimilar dados usando o conector de origem do Adobe Analytics](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=pt-BR)
* [Segmentação](../../segmentation/home.md)
* [Destinos](../../destinations/home.md)

O exemplo de abandono de navegação se concentra no uso do Adobe [!DNL Analytics] dados para criar um público-alvo acionável específico. O público-alvo é refinado para incluir todos os clientes que navegaram pelo site nos últimos quatro dias, mas não fizeram uma compra. Cada perfil no público-alvo é então direcionado com o SKU de preço mais alto que resultou do padrão de comportamento do cliente.

A query em si é muito prescritiva e inclui apenas dados que atendem aos critérios do caso de uso para a definição do segmento. Isso melhora o desempenho ao minimizar a quantidade de [!DNL Analytics] dados que estão sendo processados. Ele também solicita os dados por preço do mais alto para o mais baixo e escolhe o SKU de preço mais alto que o usuário estava navegando.

A query usada na apresentação pode ser vista abaixo:

```sql
INSERT INTO summit_adv_data_prep_dataset
SELECT STRUCT(
    customerId AS crmCustomerId, struct(sku AS sku, price AS sku_price, abandonTS AS abandonTS) AS abandonBrowse) AS _pfreportingonprod
FROM
(SELECT
B.personKey.sourceId,
A.productListItems[0].SKU AS sku,
max(A.timestamp) AS abandonTS,
max(c._pfreportingonprod.price) AS price
FROM summit_adobe_analytics_dataset A,profile_attribute_14adf268_2a20_4dee_bee6_a6b0e34616a9 B,summit_product_dataset c
WHERE A._experience.analytics.customDimension.evars.evar1 = B.personKey.sourceID
AND productListItems[0].SKU = C._pfreportingonprod.sku
AND A.web.webpagedetails.URL NOT LIKE '%orderconfirmation%'
AND timestamp > current_date - interval '4 day'
GROUP BY customerId,sku
order by price desc)D;
```

## [!DNL Query Service] exemplo de abandono de navegação usando o adobe analytics {#video-example}

A apresentação de vídeo vista abaixo fornece um caso de uso holístico e real para seus dados de Experience Platform, focado em [!DNL Query Service] Integrações do e do Adobe Analytics.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Benefícios do [!DNL Query Service] {#benefits}

Os recursos fornecidos pelo [!DNL Query Service] serve muitos propósitos. Você pode usá-lo para acomodar a lógica complexa de segmentação, para calcular vários atributos personalizados para uso em downstream ou para simplificar bastante a criação de seus segmentos.

[!DNL Query Service] permite incluir restrições em suas consultas para simplificar o processo de criação de segmentos. Isso melhora a qualidade dos dados, garantindo que os dados certos se qualificem para seus segmentos e cria públicos-alvo mais precisos. Manter a qualidade do seu query resulta em um público-alvo preciso e ajuda na confiabilidade dos dados. Você também pode salvar seu público-alvo criando esquemas e tabelas personalizadas com base em atributos derivados de seu query. Uma tabela personalizada pode ser ativada para o Perfil e você pode usar esses pontos de dados para segmentação e personalização. Esse recurso auxilia os profissionais de marketing que desejam criar um público-alvo claro.

Além disso, ao incluir a lógica em seu query que satisfaça quaisquer condições recorrentes ou estáticas, [!DNL Query Service] extrai a carga da segmentação elaborada.

A Adobe Experience Platform fornece um repositório de dados e as ferramentas necessárias para ativar seus dados de maneira eficiente e confiável. Ao manter os dados dentro do Platform, ele permite derivar atributos ao executar outros processos e remove a necessidade de exportar dados para ferramentas de terceiros para manipulação e processamento. Esses custos indiretos de processamento podem afetar muito a linha do tempo de um projeto ao lidar com centenas de atributos ou campanhas. Isso fornece aos profissionais de marketing um único local para acessar seus dados e criar campanhas, bem como um meio muito dinâmico de segmentar e personalizar suas mensagens.

## Próximas etapas

Ao ler este documento, você deve entender como [!DNL Query Service] afeta não apenas a qualidade de seus dados e a facilidade de segmentação, mas também sua importância na arquitetura de dados para todo o fluxo de trabalho completo.

Outros documentos que beneficiarão a compreensão de [!DNL Query Service] incluem recursos e usos [orientação para a execução da consulta](../best-practices/writing-queries.md) e [orientação para a organização de ativos de dados](../best-practices/organize-data-assets.md).

Para exemplos de SQL mais aplicáveis que usam o Adobe Analytics com [!DNL Query Service], consulte o [Documentação de consultas de amostra do Adobe Analytics](../sample-queries/adobe-analytics.md).
