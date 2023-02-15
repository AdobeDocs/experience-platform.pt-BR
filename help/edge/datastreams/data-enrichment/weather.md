---
title: Usar dados meteorológicos do DNL The Weather Channel
description: Use dados meteorológicos do DNL O canal meteorológico para aprimorar os dados coletados pelos conjuntos de dados.
source-git-commit: b53be9f2f2d55d5f9e8081fb0ca6732dcc2a8c11
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 3%

---


# Usar dados meteorológicos de [!DNL The Weather Channel]

A Adobe fez parceria com [!DNL [The Weather Company]](https://www.ibm.com/weather) trazer o contexto adicional do clima dos Estados Unidos para os dados coletados por meio de datastreams. Você pode usar esses dados para análise, direcionamento e criação de segmentos no Experience Platform.

Há três tipos de dados disponíveis no [!DNL The Weather Channel]:

* **[!UICONTROL Tempo atual]**: As condições meteorológicas atuais do usuário, com base em sua localização. Isso inclui temperatura atual, percipitação, cobertura de nuvem e muito mais.
* **[!UICONTROL Tempo Previsto]**: A previsão inclui a previsão de 1,2,3,5,7 e 10 dias para a localização do usuário.
* **[!UICONTROL Triggers]**: Os acionadores são combinações específicas que mapeiam para diferentes condições semanticas de tempo. Há três tipos diferentes de disparadores meteorológicos:

   * **[!UICONTROL Acionadores do tempo]**: Condições semisignificativas, como tempo frio ou chuvoso. Estas podem diferir nas suas definições entre vários climas.
   * **[!UICONTROL Acionadores do produto]**: Condições que levariam à compra de diferentes tipos de produtos. Por exemplo: previsões de tempo frio podem significar que as compras de capas de chuva são mais prováveis.
   * **[!UICONTROL Disparadores meteorológicos graves]**: Avisos meteorológicos graves, como tempestade de inverno ou aviso de furacão.

## Pré-requisitos {#prerequisites}

Antes de usar os dados meteorológicos, verifique se você atende aos seguintes pré-requisitos:

* Você deve licenciar os dados meteorológicos que usará, de [!DNL The Weather Channel]. Eles então o ativarão em sua conta.
* Os dados meteorológicos estão disponíveis somente por meio de conjuntos de dados. Para usar os dados meteorológicos, você deve usar [!DNL Web SDK], [!DNL Mobile Edge Extension] ou [API do servidor](../../../server-api/overview.md) para aproveitar esses dados.
* Seu armazenamento de dados deve ter [[!UICONTROL Localização geográfica]](../configure.md#advanced-options) habilitado.
* Adicione o [grupo de campos meteorológicos](#schema-configuration) ao schema que você está usando.

## Provisionamento {#provisioning}

Depois de ter licenciado os dados do [!DNL The Weather Channel], eles permitirão que sua conta acesse os dados do . Em seguida, entre em contato com o Atendimento ao cliente do Adobe para ativar os dados no conjunto de dados. Após ativados, os dados serão anexados automaticamente.

Você pode validar se ele está sendo adicionado executando um rastreamento de borda com o depurador ou usando o Assurance para rastrear uma ocorrência pelo [!DNL Edge Network].

### Configuração do esquema {#schema-configuration}

Você deve adicionar os grupos de campos de tempo ao esquema Experience Platform correspondente ao conjunto de dados de evento que você está usando no conjunto de dados. Há cinco grupos de campos disponíveis:

* [!UICONTROL Tempo Previsto]
* [!UICONTROL Tempo atual]
* [!UICONTROL Acionadores do produto]
* [!UICONTROL Acionadores relativos]
* [!UICONTROL Disparadores meteorológicos graves]

## Acessar os dados meteorológicos {#access-weather-data}

Assim que seus dados forem licenciados e disponibilizados, você poderá acessá-los de várias maneiras pelos serviços da Adobe.

### Adobe Analytics {#analytics}

Em [!DNL Adobe Analytics], os dados meteorológicos estão disponíveis para mapear por meio das regras de processamento, juntamente com o restante de seu [!DNL XDM] esquema.

Você pode encontrar a lista de campos que pode ser mapeada na variável [referência meteorológica](weather-reference.md) página. Como com todos [!DNL XDM] schemas, as chaves recebem o prefixo `a.x`. Por exemplo, um campo chamado `weather.current.temperature.farenheit` apareceria em [!DNL Analytics] as `a.x.weather.current.temperature.farenheit`.

![Interface da regra de processamento](../../assets/datastreams/data-enrichment/weather/processing-rules.png)

### Adobe Customer Journey Analytics {#cja}

Em [!DNL Adobe Customer Journey Analytics], os dados meteorológicos estão disponíveis no conjunto de dados especificado no conjunto de dados. Contanto que os atributos meteorológicos sejam [adicionado ao esquema](#prerequisites-prerequisites), estarão disponíveis para [adicionar a uma exibição de dados](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/create-dataview.html?lang=pt-BR) em [!DNL Customer Journey Analytics].

### Real-Time Customer Data Platform {#rtcdp}

Os dados de tempo estão disponíveis na variável [Real-time Customer Data Platform](../../../rtcdp/overview.md), para uso em segmentos. Os dados meteorológicos são anexados aos eventos.

![Construtor de segmentos exibindo eventos meteorológicos](../../assets/datastreams/data-enrichment/weather/schema-builder.png)

Como as condições climáticas mudam com frequência, o Adobe recomenda que você defina as restrições de tempo nos segmentos, conforme mostrado no exemplo acima. Ter um dia frio no último dia ou dois é muito mais impactante do que ter um dia frio há 6 meses.

Consulte a [referência meteorológica](weather-reference.md) para os campos disponíveis.

### Adobe Target {#target}

Em [!DNL Adobe Target], você pode usar os dados meteorológicos para impulsionar a personalização em tempo real. Os dados meteorológicos são passados para [!DNL Target] as [!UICONTROL mBox] e você pode acessá-lo por meio de [!UICONTROL mBox] parâmetro.

![Construtor de público-alvo do Target](../../assets/datastreams/data-enrichment/weather/target-audience-builder.png)

O parâmetro é o [!DNL XDM] caminho para um campo específico. Consulte a [referência meteorológica](weather-reference.md) para os campos disponíveis e seus caminhos correspondentes.

## Próximas etapas {#next-steps}

Após a leitura deste documento, você tem uma melhor compreensão de como pode usar os dados meteorológicos em várias soluções de Adobe. Para saber mais sobre o mapeamento de campos de dados meteorológicos, consulte o [referência de mapeamento de campo](weather-reference.md).