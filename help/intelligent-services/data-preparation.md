---
keywords: Experience Platform, home, Serviços inteligentes, tópicos populares, serviço inteligente, serviço inteligente
solution: Experience Platform
title: Preparar dados para uso em serviços inteligentes
topic-legacy: Intelligent Services
description: Para que os Serviços inteligentes descubram insights de seus dados de eventos de marketing, os dados devem ser semanticamente enriquecidos e mantidos em uma estrutura padrão. Os Serviços inteligentes usam esquemas do Experience Data Model (XDM) para fazer isso.
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '2919'
ht-degree: 1%

---

# Preparar dados para usar em [!DNL Intelligent Services]

Para [!DNL Intelligent Services] para descobrir insights de seus dados de eventos de marketing, os dados devem ser semanticamente enriquecidos e mantidos em uma estrutura padrão. [!DNL Intelligent Services] aproveitar [!DNL Experience Data Model] Esquemas (XDM) para conseguir isso. Especificamente, todos os conjuntos de dados que são usados em [!DNL Intelligent Services] deve estar em conformidade com o esquema XDM do Consumer ExperienceEvent (CEE) ou usar o conector do Adobe Analytics. Além disso, o Customer AI é compatível com o conector do Adobe Audience Manager.

Este documento fornece orientação geral sobre como mapear os dados de eventos de marketing de vários canais para o esquema CEE, destacando informações sobre campos importantes no esquema para ajudá-lo a determinar como mapear os dados de maneira eficaz para sua estrutura. Se você planeja usar dados do Adobe Analytics, visualize a seção para [Preparação de dados do Adobe Analytics](#analytics-data). Se você planeja usar os dados do Adobe Audience Manager (somente o Customer AI), visualize a seção para [Preparação de dados do Adobe Audience Manager](#AAM-data).

## Requisitos de dados

[!DNL Intelligent Services] exigem quantidades diferentes de dados históricos, dependendo da meta que você criar. Independentemente dos dados para os quais você se prepara **all** [!DNL Intelligent Services] deve incluir jornadas/eventos positivos e negativos do cliente. Ter eventos negativos e positivos melhora a precisão e a precisão do modelo.

Por exemplo, se estiver usando a AI do cliente para prever a propensão a comprar um produto, o modelo para a AI do cliente precisa de exemplos de caminhos de compra bem-sucedidos e exemplos de caminhos mal-sucedidos. Isso ocorre porque, durante o treinamento do modelo, o Customer AI procura entender quais eventos e jornadas levam a uma compra. Isso também inclui as ações executadas por clientes que não compraram, como um indivíduo que parou a jornada ao adicionar um item ao carrinho. No entanto, esses clientes podem exibir comportamentos semelhantes, a API do cliente pode fornecer insights e detalhar as principais diferenças e fatores que levam a uma pontuação de propensão mais alta. Da mesma forma, o Attribution AI requer ambos os tipos de eventos e jornadas para exibir métricas como eficácia do ponto de contato, principais caminhos de conversão e detalhamentos por posição do ponto de contato.

Para obter mais exemplos e informações sobre requisitos de dados históricos, visite a [Customer AI](./customer-ai/input-output.md#data-requirements) ou [Attribution AI](./attribution-ai/input-output.md#data-requirements) seção de requisitos de dados históricos na documentação de entrada/saída.

### Diretrizes para compilar dados

É recomendável costurar os eventos de um usuário em uma id comum, quando possível. Por exemplo, você pode ter dados do usuário com &quot;id1&quot; em 10 eventos. Posteriormente, o mesmo usuário excluiu a id do cookie e é registrado como &quot;id2&quot; nos próximos 20 eventos. Se você sabe que id1 e id2 correspondem ao mesmo usuário, a prática recomendada é unir todos os 30 eventos a uma id comum.

Se isso não for possível, você deve tratar cada conjunto de eventos como um usuário diferente ao criar os dados de entrada do modelo. Isso garante os melhores resultados durante o treinamento e a pontuação do modelo.

## Resumo do workflow

O processo de preparação varia dependendo se os dados são armazenados no Adobe Experience Platform ou externamente. Esta seção resume as etapas necessárias, tendo em conta qualquer um dos cenários.

### Preparação de dados externos

Se os dados forem armazenados fora do Experience Platform, será necessário mapear os dados para os campos obrigatórios e relevantes em uma [Schema ExperienceEvent do consumidor](#cee-schema). Esse esquema pode ser aumentado com grupos de campos personalizados para capturar melhor os dados do cliente. Depois de mapeado, você pode criar um conjunto de dados usando o esquema Consumer ExperienceEvent e [assimilar seus dados na Platform](../ingestion/home.md). O conjunto de dados CEE pode ser selecionado ao configurar um [!DNL Intelligent Service].

Dependendo do [!DNL Intelligent Service] para uso, podem ser necessários campos diferentes. Observe que é uma prática recomendada adicionar dados a um campo se você tiver os dados disponíveis. Para saber mais sobre os campos obrigatórios, visite o [Attribution AI](./attribution-ai/input-output.md) ou [Customer AI](./customer-ai/input-output.md) guia de entrada/saída.

### Preparação de dados do Adobe Analytics {#analytics-data}

O Customer AI e o Attribution AI oferecem suporte nativo aos dados da Adobe Analytics. Para usar os dados do Adobe Analytics, siga as etapas descritas na documentação para configurar um [Conector de origem do Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).

Depois que o conector de origem estiver transmitindo seus dados para o Experience Platform, você poderá selecionar o Adobe Analytics como fonte de dados, seguido por um conjunto de dados durante a configuração da sua instância. Todos os grupos de campos de esquema e campos individuais necessários são criados automaticamente durante a configuração da conexão. Não é necessário extrair, transformar, carregar (ETL) os conjuntos de dados no formato CEE.

Se você comparar os dados fluídos pelo conector de origem do Adobe Analytics com os dados do Adobe Experience Platform, poderá observar algumas discrepâncias. O conector do Analytics Source pode soltar linhas durante a transformação em um esquema do Experience Data Model (XDM). Pode haver vários motivos para que a linha inteira seja imprópria para transformação, incluindo carimbos de data e hora ausentes, IDs de pessoa ausente, IDs de pessoa inválidas ou grandes, valores de análise inválidos e muito mais.

Para obter mais informações e exemplos, visite a documentação para [comparação de dados do Adobe Analytics e do Customer Journey Analytics](https://www.adobe.com/go/compare-aa-data-to-cja-data). Este artigo foi projetado para ajudar você a diagnosticar e resolver essas diferenças para que você e sua equipe possam usar os dados do Adobe Experience Platform para Serviços inteligentes sem restrições devido a preocupações sobre integridade dos dados.

No Adobe Experience Platform Query Services, execute os seguintes Registros totais entre o carimbo de data e hora de início e de término por query channel.typeAtSource para localizar a contagem por canais de marketing.

```SELECT channel.typeAtSource as typeAtSource,
       Count(_id) AS Records 
FROM  df_hotel
WHERE timestamp>=from_utc_timestamp('2021-05-15','UTC')
        AND timestamp<from_utc_timestamp('2022-01-10','UTC')
        AND timestamp IS NOT NULL
        AND enduserids._experience.aaid.id IS NOT NULL
GROUP BY channel.typeAtSource
```

>[!IMPORTANT]
>
>O conector Adobe Analytics leva até quatro semanas para preencher dados. Se você tiver configurado uma conexão recentemente, verifique se o conjunto de dados tem o comprimento mínimo de dados necessário para o Cliente ou o Attribution AI. Revise as seções de dados históricos em [Customer AI](./customer-ai/input-output.md#data-requirements) ou [Attribution AI](./attribution-ai/input-output.md#data-requirements)e verifique se você tem dados suficientes para sua meta de previsão.

### Preparação de dados do Adobe Audience Manager (somente para o Customer AI) {#AAM-data}

O Customer AI oferece suporte nativo aos dados do Adobe Audience Manager. Para usar os dados do Audience Manager, siga as etapas descritas na documentação para configurar um [Conector de fonte Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

Depois que o conector de origem estiver transmitindo seus dados para o Experience Platform, você poderá selecionar o Adobe Audience Manager como fonte de dados, seguido por um conjunto de dados durante a configuração do Customer AI. Todos os grupos de campos de esquema e campos individuais são criados automaticamente durante a configuração da conexão. Não é necessário extrair, transformar, carregar (ETL) os conjuntos de dados no formato CEE.

>[!IMPORTANT]
>
>Se você tiver configurado um conector recentemente, verifique se o conjunto de dados tem o comprimento mínimo de dados necessário. Revise a seção de dados históricos no [documentação de entrada/saída](./customer-ai/input-output.md) para o Customer AI, e verifique se você tem dados suficientes para sua meta de previsão.

### [!DNL Experience Platform] preparação de dados

Se os dados já estiverem armazenados em [!DNL Platform] e não por meio de streaming pelos conectores de origem Adobe Analytics ou Adobe Audience Manager (somente no Customer AI), siga as etapas abaixo. Ainda é recomendável entender o esquema CEE.

1. Revisar a estrutura da [Schema ExperienceEvent do consumidor](#cee-schema) e determinam se os dados podem ser mapeados para seus campos.
2. Entre em contato com os Serviços de consultoria do Adobe para ajudar a mapear seus dados para o esquema e assimilá-los em [!DNL Intelligent Services]ou [siga as etapas neste guia](#mapping) se quiser mapear os dados por conta própria.

## Noções básicas sobre o esquema CEE {#cee-schema}

O schema Consumer ExperienceEvent descreve o comportamento de um indivíduo, pois está relacionado a eventos de marketing digital (Web ou dispositivos móveis), bem como a atividades de comércio online ou offline. O uso desse schema é necessário para [!DNL Intelligent Services] devido aos campos semanticamente bem definidos (colunas), evitando nomes desconhecidos que deixariam os dados menos claros.

O esquema CEE, como todos os esquemas XDM ExperienceEvent, captura o estado baseado em séries de tempo do sistema quando um evento (ou conjunto de eventos) ocorreu, incluindo o ponto no tempo e a identidade do assunto envolvido. Os Eventos de experiência são registros de fatos do que aconteceu e, portanto, são imutáveis e representam o que aconteceu sem agregação ou interpretação.

[!DNL Intelligent Services] utilize vários campos principais dentro desse esquema para gerar insights de seus dados de eventos de marketing, todos eles podem ser encontrados no nível raiz e expandidos para mostrar seus subcampos necessários.

![](./images/data-preparation/schema-expansion.gif)

Como todos os esquemas XDM, o grupo de campos do esquema CEE é extensível. Em outras palavras, campos adicionais podem ser adicionados ao grupo de campos CEE e diferentes variações podem ser incluídas em vários esquemas, se necessário.

Um exemplo completo do grupo de campos pode ser encontrado na função [repositório XDM público](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Além disso, você pode exibir e copiar o seguinte [Arquivo JSON](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) para obter um exemplo de como os dados podem ser estruturados para estar em conformidade com o esquema CEE. Consulte ambos os exemplos enquanto aprende sobre os campos principais descritos na seção abaixo, para determinar como você pode mapear seus próprios dados para o esquema.

## Campos principais

Existem vários campos principais dentro do grupo de campos CEE que devem ser utilizados para [!DNL Intelligent Services] para gerar insights úteis. Esta seção descreve o caso de uso e os dados esperados para esses campos e fornece links para a documentação de referência para mais exemplos.

### Campos obrigatórios

Embora o uso de todos os campos principais seja altamente recomendado, há dois campos que são **obrigatório** para [!DNL Intelligent Services] para trabalhar:

* [Um campo de identidade primário](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel) (obrigatório somente para Attribution AI)

#### Identidade primária {#identity}

Um dos campos no esquema deve ser definido como um campo de identidade primário, que permite [!DNL Intelligent Services] para vincular cada instância dos dados da série de tempo a uma pessoa individual.

Você deve determinar o melhor campo a ser usado como uma identidade primária com base na fonte e na natureza de seus dados. Um campo de identidade deve incluir um **namespace de identidade** que indica o tipo de dados de identidade que o campo espera como um valor. Alguns valores válidos de namespace incluem:

* &quot;email&quot;
* &quot;Telefone&quot;
* &quot;mcid&quot; (para Adobe Audience Manager IDs)
* &quot;aaid&quot; (para Adobe Analytics IDs)

Se não tiver certeza de qual campo você deve usar como identidade primária, entre em contato com os Serviços de consultoria da Adobe para determinar a melhor solução. Se uma identidade primária não estiver definida, o aplicativo Serviço inteligente usará o seguinte comportamento padrão:

| Padrão | Attribution AI | Customer AI |
| --- | --- | --- |
| Coluna de identidade | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| Namespace | AAID | ECID |

Para definir uma identidade primária, navegue até o esquema da **[!UICONTROL Esquemas]** e selecione o hiperlink do nome do esquema para abrir o **[!DNL Schema Editor]**.

![Navegar para o esquema](./images/data-preparation/navigate_schema.png)

Em seguida, navegue até o campo que deseja como uma identidade primária e selecione-o. O **[!UICONTROL Propriedades do campo]** abre para esse campo.

![Selecione o campo](./images/data-preparation/find_field.png)

No **[!UICONTROL Propriedades do campo]** , role para baixo até encontrar a variável **[!UICONTROL Identidade]** caixa de seleção. Depois de marcar a caixa, clique na opção para definir a identidade selecionada como a **[!UICONTROL Identidade primária]** é exibido. Selecione essa caixa também.

![Selecionar caixa de seleção](./images/data-preparation/set_primary_identity.png)

Em seguida, você deve fornecer um **[!UICONTROL Namespace de identidade]** na lista de namespaces predefinidos na lista suspensa. Neste exemplo, o espaço de nome ECID é selecionado desde uma Adobe Audience Manager ID `mcid.id` está sendo usada. Selecionar **[!UICONTROL Aplicar]** para confirmar as atualizações, selecione **[!UICONTROL Salvar]** no canto superior direito para salvar as alterações no esquema.

![Salve as alterações](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

Este campo representa a data e hora em que o evento ocorreu. Esse valor deve ser fornecido como uma string, de acordo com o padrão ISO 8601.

#### xdm:channel {#channel}

>[!NOTE]
>
>Este campo é obrigatório somente ao usar o Attribution AI.

Este campo representa o canal de marketing relacionado ao ExperienceEvent. O campo inclui informações sobre o tipo de canal, o tipo de mídia e o tipo de local.

![](./images/data-preparation/channel.png)

**Exemplo de schema**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Para obter informações completas sobre cada um dos subcampos necessários para `xdm:channel`consulte o [esquema de canal de experiência](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md) especificações. Para obter alguns exemplos de mapeamentos, consulte a [tabela abaixo](#example-channels).

#### Exemplo de mapeamento de canal {#example-channels}

A tabela a seguir fornece alguns exemplos de canais de marketing mapeados para a variável `xdm:channel` schema:

| Canal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Pesquisa paga | https:/<span>/ns.adobe.com/xdm/channel-types/search | pago | clicks |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | ganho | cliques |
| Exibir | https:/<span>/ns.adobe.com/xdm/channel-types/display | pago | cliques |
| Email | https:/<span>/ns.adobe.com/xdm/channel-types/email | pago | cliques |
| Referenciador interno | https:/<span>/ns.adobe.com/xdm/channel-types/direct | possuído | cliques |
| Exibir ViewThrough | https:/<span>/ns.adobe.com/xdm/channel-types/display | pago | impressões |
| Redirecionamento do código QR | https:/<span>/ns.adobe.com/xdm/channel-types/direct | possuído | cliques |
| Dispositivo móvel | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | possuído | cliques |

### Campos recomendados

O restante dos campos principais são descritos nesta seção. Embora esses campos não sejam necessariamente necessários para [!DNL Intelligent Services] para funcionar, é altamente recomendável usar o máximo deles possível para obter insights mais ricos.

#### xdm:productListItems

Este campo é uma matriz de itens que representam produtos selecionados por um cliente, incluindo o SKU do produto, nome, preço e quantidade.

![](./images/data-preparation/productListItems.png)

**Exemplo de schema**

```json
[
  {
    "xdm:SKU": "1002352692",
    "xdm:name": "24-Watt 8-Light Chrome Integrated LED Bath Light",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 159.45
  },
  {
    "xdm:SKU": "3398033623",
    "xdm:name": "16ft RGB LED Strips",
    "xdm:currencyCode": "USD",
    "xdm:quantity": 1,
    "xdm:priceTotal": 79.99
  }
]
```

Para obter informações completas sobre cada um dos subcampos necessários para `xdm:productListItems`consulte o [schema de detalhes do comércio](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) especificações.

#### xdm:commerce

Este campo contém informações específicas de comércio sobre o ExperienceEvent, incluindo o número do pedido de compra e as informações de pagamento.

![](./images/data-preparation/commerce.png)

**Exemplo de schema**

```json
{
    "xdm:order": {
      "xdm:purchaseID": "a8g784hjq1mnp3",
      "xdm:purchaseOrderNumber": "123456",
      "xdm:payments": [
        {
          "xdm:transactionID": "transactid-a111",
          "xdm:paymentAmount": 59,
          "xdm:paymentType": "credit_card",
          "xdm:currencyCode": "USD"
        },
        {
          "xdm:transactionId": "transactid-a222",
          "xdm:paymentAmount": 100,
          "xdm:paymentType": "gift_card",
          "xdm:currencyCode": "USD"
        }
      ],
      "xdm:currencyCode": "USD",
      "xdm:priceTotal": 159
    },
    "xdm:purchases": {
      "xdm:value": 1
    }
  }
```

Para obter informações completas sobre cada um dos subcampos necessários para `xdm:commerce`consulte o [schema de detalhes do comércio](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md) especificações.

#### xdm:web

Este campo representa detalhes da Web relacionados ao ExperienceEvent, como a interação, detalhes da página e referenciador.

![](./images/data-preparation/web.png)

**Exemplo de schema**

```json
{
  "xdm:webPageDetails": {
    "xdm:siteSection": "Shopping Cart",
    "xdm:server": "example.com",
    "xdm:name": "Purchase Confirmation",
    "xdm:URL": "https://www.example.com/orderConf",
    "xdm:errorPage": false,
    "xdm:homePage": false,
    "xdm:pageViews": {
      "xdm:value": 1
    }
  },
  "xdm:webReferrer": {
    "xdm:URL": "https://www.example.com/checkout",
    "xdm:referrerType": "internal"
  }
}
```

Para obter informações completas sobre cada um dos subcampos necessários para `xdm:productListItems`consulte o [Schema de detalhes da Web do ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md) especificações.

#### xdm:marketing

Este campo contém informações relacionadas às atividades de marketing que estão ativas com o ponto de contato.

![](./images/data-preparation/marketing.png)

**Exemplo de schema**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Para obter informações completas sobre cada um dos subcampos necessários para `xdm:productListItems`consulte o [setor de marketing](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md) especificações.

## Mapeamento e assimilação de dados {#mapping}

Depois de determinar se os dados dos eventos de marketing podem ser mapeados para o esquema CEE, a próxima etapa é determinar quais dados você deve trazer para o [!DNL Intelligent Services]. Todos os dados históricos usados em [!DNL Intelligent Services] deve estar dentro da janela de tempo mínimo de quatro meses de dados, além do número de dias planejado como um período de pesquisa.

Depois de decidir o intervalo de dados que deseja enviar, entre em contato com os Serviços de consultoria da Adobe para ajudar a mapear seus dados para o esquema e assimilá-los no serviço.

Se você tiver uma [!DNL Adobe Experience Platform] e desejar mapear e assimilar os dados por conta própria, siga as etapas descritas na seção abaixo.

### Uso do Adobe Experience Platform

>[!NOTE]
>
>As etapas abaixo exigem uma assinatura do Experience Platform. Se você não tiver acesso à Platform, pule para a [próximas etapas](#next-steps) seção.

Esta seção descreve o fluxo de trabalho para mapeamento e assimilação de dados no Experience Platform para uso no [!DNL Intelligent Services], incluindo links para tutoriais para etapas detalhadas.

#### Criar um esquema CEE e um conjunto de dados

Quando estiver pronto para começar a preparar seus dados para assimilação, a primeira etapa é criar um novo esquema XDM que emprega o grupo de campos CEE. Os seguintes tutoriais abordam o processo de criação de um novo schema na interface do usuário ou na API:

* [Criar um esquema na interface do usuário](../xdm/tutorials/create-schema-ui.md)
* [Criar um esquema na API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Os tutoriais acima seguem um workflow genérico para criar um schema. Ao escolher uma classe para o schema, você deve usar o **Classe XDM ExperienceEvent**. Depois que essa classe tiver sido escolhida, você poderá adicionar o grupo de campos CEE ao schema.

Após adicionar o grupo de campos CEE ao schema, é possível adicionar outros grupos de campos, conforme necessário, para campos adicionais em seus dados.

Depois de criar e salvar o esquema, você pode criar um novo conjunto de dados com base nesse esquema. Os seguintes tutoriais abordam o processo de criação de um novo conjunto de dados na interface do usuário ou na API:

* [Criar um conjunto de dados na interface do usuário](../catalog/datasets/user-guide.md#create) (Siga o fluxo de trabalho para usar um esquema existente)
* [Criar um conjunto de dados na API](../catalog/datasets/create.md)

Após a criação do conjunto de dados, você pode encontrá-lo na interface do usuário da plataforma no **[!UICONTROL Conjuntos de dados]** espaço de trabalho.

![](images/data-preparation/dataset-location.png)

#### Adicionar campos de identidade ao conjunto de dados

Caso esteja trazendo dados do [!DNL Adobe Audience Manager], [!DNL Adobe Analytics]ou outra fonte externa, você tem a opção de definir um campo de esquema como um campo de identidade. Para definir um campo de esquema como um campo de identidade, exiba a seção sobre como definir campos de identidade dentro da variável [Tutorial da interface do usuário](../xdm/tutorials/create-schema-ui.md#identity-field) ou [Tutorial de API](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) para criar um schema .

Se você estiver assimilando dados de um arquivo CSV local, ignore a próxima seção em [mapeamento e assimilação de dados](#ingest).

#### Mapear e assimilar dados {#ingest}

Depois de criar um esquema CEE e um conjunto de dados, você pode começar a mapear as tabelas de dados para o esquema e assimilar esses dados na plataforma. Veja o tutorial em [mapeamento de um arquivo CSV para um esquema XDM](../ingestion/tutorials/map-a-csv-file.md) para obter etapas sobre como executar isso na interface do usuário do . Você pode usar o seguinte [exemplo de arquivo JSON](https://github.com/AdobeDocs/experience-platform.en/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) para testar o processo de ingestão antes de usar seus próprios dados.

Depois que um conjunto de dados é preenchido, o mesmo conjunto de dados pode ser usado para assimilar arquivos de dados adicionais.

Se os dados forem armazenados em um aplicativo de terceiros suportado, você também poderá optar por criar um [conector de origem](../sources/home.md) para assimilar seus dados de eventos de marketing no [!DNL Platform] em tempo real.

## Próximas etapas {#next-steps}

Este documento forneceu orientação geral sobre como preparar seus dados para uso no [!DNL Intelligent Services]. Se precisar de consultoria adicional com base no seu caso de uso, entre em contato com o Suporte da Adobe Consulting.

Depois de preencher com êxito um conjunto de dados com os dados de experiência do cliente, você pode usar [!DNL Intelligent Services] para gerar insights. Consulte os seguintes documentos para começar:

* [Visão geral do Attribution AI](./attribution-ai/overview.md)
* [Visão geral do Customer AI](./customer-ai/overview.md)
