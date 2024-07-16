---
keywords: Experience Platform;serviço de consulta;serviço de consulta;consulta;;query service;Query service;query
title: Exemplo de caso de uso para o serviço de consulta do Adobe Experience Platform
description: Um exemplo completo para demonstrar a versatilidade e os benefícios do Adobe Experience Platform Query Service.
exl-id: 00bdae47-71b7-44ea-9365-a1d64c88d2bf
source-git-commit: 38689125a43ad0b1a12a00efe6800bb310d7557c
workflow-type: tm+mt
source-wordcount: '695'
ht-degree: 0%

---

# Exemplo de caso de uso para o Adobe Experience Platform [!DNL Query Service]

Este documento e a apresentação em vídeo que o acompanha fornecem um fluxo de trabalho completo de alto nível demonstrando como o Adobe Experience Platform [!DNL Query Service] beneficia os insights comerciais estratégicos da sua organização. Usando um caso de uso de abandono de navegação como exemplo, este guia ilustra os seguintes conceitos principais:

* A principal importância do processamento de dados para maximizar o potencial do Adobe Experience Platform.
* Maneiras de criar a consulta com base na arquitetura de dados existente.
* Garanta a qualidade dos dados que atenda às suas necessidades e métodos para atenuar qualquer falha.
* O processo para agendar uma consulta para execução em uma frequência definida para uso downstream na segmentação e destinos para personalização.
* A facilidade para os profissionais de marketing incluírem conjuntos de dados derivados em seus públicos-alvo através do [!DNL Query Service].

## Objetivos {#objectives}

Essa demonstração do fluxo de trabalho depende de vários serviços da Adobe Experience Platform. Se você quiser acompanhar, é recomendável ter uma boa compreensão dos seguintes recursos e serviços:

* As [noções básicas da composição do esquema do Experience Data Model (XDM)](../../xdm/schema/composition.md)
* Como [criar conjuntos de dados e assimilar dados](https://experienceleague.adobe.com/docs/platform-learn/tutorials/data-ingestion/create-datasets-and-ingest-data.html)
* Como [assimilar dados usando o conector de origem do Adobe Analytics](https://experienceleague.adobe.com/docs/platform-learn/tutorials/sources/ingest-data-from-adobe-analytics.html?lang=pt-BR)
* [Segmentação](../../segmentation/home.md)
* [Destinos](../../destinations/home.md)

O exemplo de abandono de navegação se concentra no uso dos dados do Adobe [!DNL Analytics] para criar um público acionável específico. O público-alvo é refinado para incluir todos os clientes que navegaram no site nos últimos quatro dias, mas não fizeram uma compra. Cada perfil no público-alvo é então direcionado com o SKU de preço mais alto que resultou do padrão de comportamento do cliente.

A consulta em si é muito prescritiva e inclui apenas dados que atendem aos critérios de caso de uso para a definição do segmento. Isso melhora o desempenho minimizando a quantidade de [!DNL Analytics] dados sendo processados. Ele também solicita os dados por preço do mais alto para o mais baixo e escolhe o SKU de maior preço que o usuário estava navegando.

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

## Exemplo de abandono de navegação [!DNL Query Service] usando o adobe analytics {#video-example}

A apresentação em vídeo vista abaixo fornece um caso de uso holístico, real, para seus dados de Experience Platform com foco nas integrações do [!DNL Query Service] e da análise de Adobe.

>[!VIDEO](https://video.tv.adobe.com/v/342533?quality=12&learn=on)

## Benefícios do [!DNL Query Service] {#benefits}

Os recursos fornecidos pelo [!DNL Query Service] servem a várias finalidades. Você pode usá-lo para acomodar uma lógica complexa para segmentação, para calcular vários atributos personalizados para uso downstream ou para simplificar bastante a criação de seus públicos-alvo.

O [!DNL Query Service] permite que você inclua restrições em suas consultas para simplificar seu processo de criação de público-alvo. Isso melhora a qualidade dos dados, garantindo que os dados certos se qualifiquem para seus públicos-alvo. Manter a qualidade da sua consulta resulta em um público-alvo preciso e ajuda na confiabilidade dos dados. Você também pode salvar seu público-alvo criando esquemas e tabelas personalizadas com base em atributos derivados de sua consulta. Uma tabela personalizada pode ser ativada para o Perfil e você pode usar esses pontos de dados para segmentação e personalização. Esse recurso auxilia profissionais de marketing que desejam criar um público-alvo claro de pessoas.

Além disso, ao incluir na consulta uma lógica que satisfaça quaisquer condições recorrentes ou estáticas, o [!DNL Query Service] extrai a carga de uma segmentação elaborada.

O Adobe Experience Platform fornece um repositório de dados e as ferramentas necessárias para ativar seus dados de forma eficiente e confiável. Ao manter os dados dentro da Platform, você pode derivar atributos enquanto executa outros processos e elimina a necessidade de exportar dados para ferramentas de terceiros para manipulação e processamento. Essas despesas gerais de processamento podem afetar bastante a linha do tempo de um projeto ao lidar com centenas de atributos ou campanhas. Isso fornece aos profissionais de marketing um único local para acessar seus dados e criar campanhas, bem como um meio muito dinâmico de segmentar e personalizar suas mensagens.

## Próximas etapas

Após a leitura desse documento, você deve entender como o [!DNL Query Service] afeta não apenas a qualidade dos seus dados e a facilidade de segmentação, mas também sua importância na arquitetura de dados para todo o fluxo de trabalho completo. Para obter mais exemplos de SQL aplicáveis que usam o Adobe Analytics com [!DNL Query Service], consulte o [caso de uso de variáveis de merchandising do Adobe Analytics](./merchandising-variables.md).

Outros documentos que demonstram os benefícios do [!DNL Query Service] para os insights estratégicos de negócios da sua organização são o exemplo de [caso de uso de filtragem de bot](./bot-filtering.md).

Como alternativa, esses documentos podem beneficiar sua compreensão dos recursos do [!DNL Query Service]:

* [Orientação para execução de consulta](../best-practices/writing-queries.md)
* [Orientação para a organização do ativo de dados](../best-practices/organize-data-assets.md).


