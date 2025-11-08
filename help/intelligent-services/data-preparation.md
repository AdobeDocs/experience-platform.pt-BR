---
keywords: Experience Platform;home;Serviços inteligentes;tópicos populares;serviço inteligente;serviço inteligente
solution: Experience Platform
title: Preparar dados para uso em serviços inteligentes
description: Para que os Serviços inteligentes descubram insights dos dados de eventos de marketing, os dados devem ser semanticamente enriquecidos e mantidos em uma estrutura padrão. Para isso, os Serviços inteligentes usam os esquemas do Experience Data Model (XDM).
exl-id: 17bd7cc0-da86-4600-8290-cd07bdd5d262
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '2951'
ht-degree: 0%

---

# Preparar dados para uso em [!DNL Intelligent Services]

Para que [!DNL Intelligent Services] descubra insights dos dados de eventos de marketing, os dados devem ser semanticamente enriquecidos e mantidos em uma estrutura padrão. [!DNL Intelligent Services] use [!DNL Experience Data Model] esquemas (XDM) para fazer isso. Especificamente, todos os conjuntos de dados usados em [!DNL Intelligent Services] devem estar em conformidade com o esquema XDM do Consumer ExperienceEvent (CEE) ou usar o conector do Adobe Analytics. Além disso, a IA do cliente é compatível com o conector do Adobe Audience Manager.

Este documento fornece orientação geral sobre como mapear os dados de eventos de marketing de vários canais para o esquema CEE, descrevendo informações sobre campos importantes no esquema para ajudar a determinar como mapear com eficiência os dados de acordo com sua estrutura. Se você planeja usar os dados do Adobe Analytics, exiba a seção para [preparação de dados do Adobe Analytics](#analytics-data). Se você planeja usar os dados do Adobe Audience Manager (somente IA do cliente), consulte a seção para [Preparação de dados do Adobe Audience Manager](#AAM-data).

## Requisitos de dados

[!DNL Intelligent Services] exigem quantidades diferentes de dados históricos, dependendo da meta que você criar. Independentemente disso, os dados que você preparar para **todos** [!DNL Intelligent Services] devem incluir jornadas/eventos positivos e negativos do cliente. Ter eventos negativos e positivos melhora a precisão e a precisão do modelo.

Por exemplo, se você estiver usando a IA do cliente para prever a propensão para comprar um produto, o modelo da IA do cliente precisará de exemplos de caminhos de compra bem-sucedidos e exemplos de caminhos malsucedidos. Isso ocorre porque, durante o treinamento do modelo, a IA do cliente procura entender quais eventos e jornadas levam a uma compra. Isso também inclui as ações tomadas pelos clientes que não compraram, como uma pessoa que interrompeu a jornada de adicionar um item ao carrinho. Esses clientes podem apresentar comportamentos semelhantes. No entanto, a IA do cliente pode fornecer insights e detalhar as principais diferenças e fatores que levam a uma pontuação de propensão mais alta. Da mesma forma, a IA de atribuição exige ambos os tipos de eventos e jornadas para exibir métricas como eficácia do ponto de contato, os principais caminhos de conversão e detalhamentos por posição de ponto de contato.

Para obter mais exemplos e informações sobre requisitos de dados históricos, visite a seção requisitos de dados históricos da [IA de cliente](./customer-ai/data-requirements.md#data-requirements) ou da [IA de atribuição](./attribution-ai/input-output.md#data-requirements) na documentação de entrada/saída.

### Diretrizes para compilação de dados

É recomendável compilar os eventos de um usuário em uma ID comum, quando possível. Por exemplo, você pode ter dados de usuário com &quot;id1&quot; em 10 eventos. Posteriormente, o mesmo usuário excluiu a ID do cookie e foi registrado como &quot;id2&quot; nos próximos 20 eventos. Se você souber que id1 e id2 correspondem ao mesmo usuário, a prática recomendada é compilar todos os 30 eventos com uma id comum.

Se isso não for possível, você deverá tratar cada conjunto de eventos como um usuário diferente ao criar os dados de entrada do modelo. Isso garante os melhores resultados durante o treinamento e a pontuação do modelo.

## Resumo do fluxo de trabalho

O processo de preparação varia dependendo se os dados estão armazenados no Adobe Experience Platform ou externamente. Esta seção resume as etapas necessárias que você precisa executar em ambos os cenários.

### Preparação de dados externos

Se os dados forem armazenados fora do Experience Platform, será necessário mapear os dados para os campos necessários e relevantes em um [esquema do ExperienceEvent do consumidor](#cee-schema). Esse esquema pode ser aumentado com grupos de campos personalizados para capturar melhor os dados do cliente. Depois de mapeado, você pode criar um conjunto de dados usando seu esquema Consumer ExperienceEvent e [assimilar seus dados na Experience Platform](../ingestion/home.md). O conjunto de dados CEE pode ser selecionado ao configurar um [!DNL Intelligent Service].

Dependendo do [!DNL Intelligent Service] que você deseja usar, campos diferentes podem ser obrigatórios. Observe que é uma prática recomendada adicionar dados a um campo se você tiver os dados disponíveis. Para saber mais sobre os campos obrigatórios, visite o [guia de requisitos de dados da IA de atribuição](./attribution-ai/input-output.md) ou da [IA do cliente](./customer-ai/data-requirements.md).

### Preparação de dados do Adobe Analytics {#analytics-data}

A IA do cliente e a IA de atribuição oferecem suporte nativo aos dados do Adobe Analytics. Para usar os dados do Adobe Analytics, siga as etapas descritas na documentação para configurar um [conector de origem do Analytics](../sources/tutorials/ui/create/adobe-applications/analytics.md).

Depois que o conector de origem estiver transmitindo seus dados para a Experience Platform, você poderá selecionar o Adobe Analytics como uma fonte de dados seguida por um conjunto de dados durante a configuração da instância. Todos os grupos de campos de esquema obrigatórios e campos individuais são criados automaticamente durante a configuração da conexão. Não é necessário extrair, transformar, carregar (ETL) os conjuntos de dados no formato CEE.

Se você comparar os dados transportados pelo conector de origem do Adobe Analytics para o Adobe Experience Platform com os dados do Adobe Analytics, poderá notar algumas discrepâncias. O conector Source do Analytics pode descartar linhas durante a transformação para um esquema do Experience Data Model (XDM). Pode haver vários motivos para a linha inteira ser imprópria para transformação, que incluem carimbos de data e hora ausentes, personIDs ausentes, IDs de pessoa inválidas ou grandes, valores analíticos inválidos e muito mais.

Para obter mais informações e exemplos, visite a documentação de [comparação dos dados do Adobe Analytics e do Customer Journey Analytics](https://www.adobe.com/go/compare-aa-data-to-cja-data). Este artigo foi projetado para ajudá-lo a diagnosticar e resolver essas diferenças, de modo que você e sua equipe possam usar os dados da Adobe Experience Platform para Serviços inteligentes sem obstáculos devido a preocupações com a integridade dos dados.

Nos Serviços de consulta da Adobe Experience Platform, execute o seguinte Total de registros entre o carimbo de data e hora inicial e final por channel.typeAtSource query para encontrar a contagem por canais de marketing.

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
>O conector do Adobe Analytics leva até quatro semanas para preencher os dados. Se você configurou uma conexão recentemente, deve verificar se o conjunto de dados tem o comprimento mínimo de dados necessário para o Cliente ou a IA de atribuição. Revise as seções de dados históricos na [IA do cliente](./customer-ai/data-requirements.md#data-requirements) ou na [IA de atribuição](./attribution-ai/input-output.md#data-requirements) e verifique se você tem dados suficientes para a sua meta de previsão.

### Preparação de dados do Adobe Audience Manager (somente IA do cliente) {#AAM-data}

A IA do cliente oferece suporte nativo aos dados do Adobe Audience Manager. Para usar os dados do Audience Manager, siga as etapas descritas na documentação para configurar um [conector de origem do Audience Manager](../sources/tutorials/ui/create/adobe-applications/audience-manager.md).

Quando o conector de origem estiver transmitindo seus dados para a Experience Platform, você poderá selecionar o Adobe Audience Manager como uma fonte de dados seguida de um conjunto de dados durante a configuração da IA do cliente. Todos os grupos de campos de esquema e campos individuais são criados automaticamente durante a configuração da conexão. Não é necessário extrair, transformar, carregar (ETL) os conjuntos de dados no formato CEE.

>[!IMPORTANT]
>
>Se você configurou um conector recentemente, deve verificar se o conjunto de dados tem o comprimento mínimo de dados necessário. Revise a seção de dados históricos na [documentação de entrada/saída](./customer-ai/data-requirements.md) da IA do cliente e verifique se você tem dados suficientes para a meta de previsão.

### Preparação de dados de [!DNL Experience Platform]

Se os dados já estiverem armazenados no [!DNL Experience Platform] e não estiverem sendo transmitidos pelos conectores de origem da Adobe Analytics ou da Adobe Audience Manager (somente IA do cliente), siga as etapas abaixo. Ainda é recomendável que você entenda o esquema CEE.

1. Revise a estrutura do [esquema ExperienceEvent do Consumidor](#cee-schema) e determine se os dados podem ser mapeados para seus campos.
2. Contate os Serviços Adobe Consulting para ajudar a mapear seus dados para o esquema e assimilá-los no [!DNL Intelligent Services], ou [siga as etapas deste guia](#mapping) se desejar mapear os dados você mesmo.

## Noções básicas sobre o esquema CEE {#cee-schema}

O esquema ExperienceEvent do consumidor descreve o comportamento de um indivíduo, pois está relacionado a eventos de marketing digital (Web ou móvel), bem como a atividades de comércio online ou offline. O uso deste esquema é necessário para [!DNL Intelligent Services] devido a seus campos (colunas) semanticamente bem definidos, evitando nomes desconhecidos que de outra forma tornariam os dados menos claros.

O esquema CEE, como todos os esquemas XDM ExperienceEvent, captura o estado do sistema com base em séries de tempo quando um evento (ou conjunto de eventos) ocorreu, incluindo o momento e a identidade do assunto envolvido. Eventos de experiência são registros fatuais do que ocorreu e, portanto, são imutáveis e representam o que aconteceu sem agregação ou interpretação.

[!DNL Intelligent Services] utilize vários campos principais deste esquema para gerar insights dos dados dos eventos de marketing, todos podem ser encontrados no nível raiz e expandidos para mostrar os subcampos obrigatórios.

![Demonstração da expansão de esquema na interface do usuário do Adobe Experience Platform, mostrando detalhes de navegação e subcampos.](./images/data-preparation/schema-expansion.gif)

Como todos os esquemas XDM, o grupo de campos do esquema CEE é extensível. Em outras palavras, campos adicionais podem ser adicionados ao grupo de campos CEE e variações diferentes podem ser incluídas em vários esquemas, se necessário.

Um exemplo completo do grupo de campos pode ser encontrado no [repositório XDM público](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-consumer.schema.md). Além disso, você pode visualizar e copiar o seguinte [arquivo JSON](https://github.com/AdobeDocs/experience-platform.pt-BR/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) para obter um exemplo de como os dados podem ser estruturados para estar em conformidade com o esquema CEE. Consulte ambos os exemplos ao saber mais sobre os campos principais descritos na seção abaixo, para determinar como mapear seus próprios dados para o esquema.

## Campos-chave

Há vários campos principais no grupo de campos CEE que devem ser utilizados para que [!DNL Intelligent Services] gere insights úteis. Esta seção descreve o caso de uso e os dados esperados para esses campos, e fornece links para a documentação de referência para obter mais exemplos.

### Campos obrigatórios

Embora o uso de todos os campos principais seja altamente recomendado, há dois campos **obrigatórios** para que [!DNL Intelligent Services] funcione:

* [Um campo de identidade principal](#identity)
* [xdm:timestamp](#timestamp)
* [xdm:channel](#channel) (obrigatório somente para IA de atribuição)

#### Identidade principal {#identity}

Um dos campos no esquema deve ser definido como um campo de identidade principal, o que permite a [!DNL Intelligent Services] vincular cada instância de dados de série temporal a uma pessoa individual.

Você deve determinar o melhor campo para usar como identidade primária com base na fonte e na natureza dos seus dados. Um campo de identidade deve incluir um **namespace de identidade** que indica o tipo de dados de identidade que o campo espera como um valor. Alguns valores de namespace válidos incluem:

>[!NOTE]
>
>A Experience Cloud ID (ECID) também é conhecida como MCID e continua a ser usada em namespaces.

* &quot;email&quot;
* &quot;phone&quot;
* &quot;mcid&quot; (para Adobe Audience Manager IDs)
* &quot;aaid&quot; (para Adobe Analytics IDs)

Se não tiver certeza de qual campo você deve usar como identidade principal, entre em contato com os Serviços da Adobe Consulting para determinar a melhor solução. Se uma identidade primária não for definida, o aplicativo de Serviço Inteligente usará o seguinte comportamento padrão:

| Padrão | IA de atribuição | IA do cliente |
| --- | --- | --- |
| Coluna de identidade | `endUserIDs._experience.aaid.id` | `endUserIDs._experience.mcid.id` |
| Namespace | AAID | ECID |

Para definir uma identidade primária, navegue até o esquema na guia **[!UICONTROL Esquemas]** e selecione o hiperlink do nome do esquema para abrir o **[!DNL Schema Editor]**.

![Navegação até o esquema na interface do usuário do Adobe Experience Platform.](./images/data-preparation/navigate_schema.png)

Em seguida, navegue até o campo desejado como uma identidade principal e selecione-o. O menu **[!UICONTROL Propriedades do campo]** é aberto para esse campo.

![O processo de seleção do campo desejado na interface do usuário do Adobe Experience Platform.](./images/data-preparation/find_field.png)

No menu **[!UICONTROL Propriedades do campo]**, role para baixo até localizar a caixa de seleção **[!UICONTROL Identidade]**. Após marcar a caixa de seleção, é exibida a opção para definir a identidade selecionada como a **[!UICONTROL Identidade principal]**. Selecione esta caixa também.

![Caixa de seleção para definir a identidade principal na interface do usuário do Adobe Experience Platform.](./images/data-preparation/set_primary_identity.png)

Em seguida, você deve fornecer um **[!UICONTROL Namespace de identidade]** da lista de namespaces predefinidos na lista suspensa. Neste exemplo, o namespace da ECID está selecionado, pois uma Adobe Audience Manager ID `mcid.id` está sendo usada. Selecione **[!UICONTROL Aplicar]** para confirmar as atualizações e selecione **[!UICONTROL Salvar]** no canto superior direito para salvar as alterações no esquema.

![Menu suspenso que mostra a seleção do namespace ECID na interface do usuário do Adobe Experience Platform.](./images/data-preparation/select_namespace.png)

#### xdm:timestamp {#timestamp}

Este campo representa a data e hora em que o evento ocorreu. Esse valor deve ser fornecido como uma string, de acordo com o padrão ISO 8601.

#### xdm:channel {#channel}

>[!NOTE]
>
>Este campo é obrigatório somente ao usar a IA de atribuição.

Este campo representa o canal de marketing relacionado ao ExperienceEvent. O campo inclui informações sobre o tipo de canal, tipo de mídia e tipo de local.

![Diagrama mostrando a estrutura do campo xdm:channel, incluindo subcampos como type, mediaType e mediaAction.](./images/data-preparation/channel.png)

**Exemplo de esquema**

```json
{
  "@id": "https://ns.adobe.com/xdm/channels/facebook-feed",
  "@type": "https://ns.adobe.com/xdm/channel-types/social",
  "xdm:mediaType": "earned",
  "xdm:mediaAction": "clicks"
}
```

Para obter informações completas sobre cada um dos subcampos obrigatórios de `xdm:channel`, consulte as especificações do [esquema do canal de experiência](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/channels/channel.schema.md). Para obter alguns mapeamentos de exemplo, consulte a [tabela abaixo](#example-channels).

#### Exemplo de mapeamentos de canal {#example-channels}

A tabela a seguir fornece alguns exemplos de canais de marketing mapeados para o esquema `xdm:channel`:

| Canal | `@type` | `mediaType` | `mediaAction` |
| --- | --- | --- | --- |
| Pesquisa paga | https:/<span>/ns.adobe.com/xdm/channel-types/search | pago | cliques |
| Social - Marketing | https:/<span>/ns.adobe.com/xdm/channel-types/social | ganho | cliques |
| Exibir | https:/<span>/ns.adobe.com/xdm/channel-types/display | pago | cliques |
| Email | https:/<span>/ns.adobe.com/xdm/channel-types/email | pago | cliques |
| Referenciador interno | https:/<span>/ns.adobe.com/xdm/channel-types/direct | próprio | cliques |
| Exibir ViewThrough | https:/<span>/ns.adobe.com/xdm/channel-types/display | pago | impressões |
| Redirecionamento de código QR | https:/<span>/ns.adobe.com/xdm/channel-types/direct | próprio | cliques |
| Dispositivo móvel | https:/<span>/ns.adobe.com/xdm/channel-types/mobile | próprio | cliques |

### Campos recomendados

O restante dos campos principais é descrito nesta seção. Embora esses campos não sejam necessariamente obrigatórios para o [!DNL Intelligent Services] funcionar, é altamente recomendável que você use o máximo possível deles para obter insights mais avançados.

#### xdm:productListItems

Esse campo é uma matriz de itens que representam produtos selecionados por um cliente, incluindo o SKU, nome, preço e quantidade do produto.

![O campo xdm:productListItems, incluindo subcampos como SKU, nome, currencyCode, quantidade e priceTotal.](./images/data-preparation/productListItems.png)

**Exemplo de esquema**

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

Para obter informações completas sobre cada um dos subcampos obrigatórios de `xdm:productListItems`, consulte a especificação do [esquema de detalhes do comércio](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:commerce

Este campo contém informações específicas de comércio sobre o ExperienceEvent, incluindo o número da ordem de compra e informações de pagamento.

![A estrutura do campo xdm:commerce, incluindo subcampos como pedido, compras e pagamentos.](./images/data-preparation/commerce.png)

**Exemplo de esquema**

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

Para obter informações completas sobre cada um dos subcampos obrigatórios de `xdm:commerce`, consulte a especificação do [esquema de detalhes do comércio](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-commerce.schema.md).

#### xdm:web

Esse campo representa detalhes da Web relacionados ao ExperienceEvent, como interação, detalhes da página e referenciador.

![O campo xdm:web, incluindo subcampos como webPageDetails e webReferrer.](./images/data-preparation/web.png)

**Exemplo de esquema**

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

Para obter informações completas sobre cada um dos subcampos obrigatórios de `xdm:productListItems`, consulte a especificação do [esquema de detalhes da Web do ExperienceEvent](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/experienceevent-web.schema.md).

#### xdm:marketing

Esse campo contém informações relacionadas às atividades de marketing ativas com o ponto de contato.

![A estrutura do campo xdm:marketing, incluindo subcampos como trackingCode, campaignGroup e campaignName.](./images/data-preparation/marketing.png)

**Exemplo de esquema**

```json
{
  "xdm:trackingCode": "marketingcampaign111",
  "xdm:campaignGroup": "50%_DISCOUNT",
  "xdm:campaignName": "50%_DISCOUNT_USA"
}
```

Para obter informações completas sobre cada um dos subcampos obrigatórios de `xdm:productListItems`, consulte a especificação do [esquema de marketing](https://github.com/adobe/xdm/blob/797cf4930d5a80799a095256302675b1362c9a15/docs/reference/context/marketing.schema.md).

## Mapeamento e assimilação de dados {#mapping}

Depois de determinar se os dados dos eventos de marketing podem ser mapeados para o esquema CEE, a próxima etapa é determinar quais dados você deve trazer para o [!DNL Intelligent Services]. Todos os dados históricos usados em [!DNL Intelligent Services] devem estar dentro da janela de tempo mínimo de quatro meses de dados, mais o número de dias planejados como um período de pesquisa.

Depois de decidir o intervalo de dados que deseja enviar, entre em contato com os Serviços da Adobe Consulting para ajudar a mapear seus dados para o esquema e assimilá-los no serviço.

Se você tiver uma assinatura do [!DNL Adobe Experience Platform] e quiser mapear e assimilar os dados sozinho, siga as etapas descritas na seção abaixo.

### Utilização do Adobe Experience Platform

>[!NOTE]
>
>As etapas abaixo exigem uma assinatura do Experience Platform. Se você não tiver acesso ao Experience Platform, vá para a seção [próximas etapas](#next-steps).

Esta seção descreve o fluxo de trabalho para mapeamento e assimilação de dados na Experience Platform para uso no [!DNL Intelligent Services], incluindo links para tutoriais para etapas detalhadas.

#### Criar um esquema e um conjunto de dados CEE

Quando estiver pronto para começar a preparar seus dados para assimilação, a primeira etapa é criar um novo esquema XDM que empregue o grupo de campos CEE. Os seguintes tutoriais caminham pelo processo de criação de um novo esquema na interface ou na API:

* [Criar um esquema na interface](../xdm/tutorials/create-schema-ui.md)
* [Criar um esquema na API](../xdm/tutorials/create-schema-api.md)

>[!IMPORTANT]
>
>Os tutoriais acima seguem um fluxo de trabalho genérico para criar um schema. Ao escolher uma classe para o esquema, você deve usar a **classe XDM ExperienceEvent**. Depois que essa classe for escolhida, você poderá adicionar o grupo de campos CEE ao esquema.

Depois de adicionar o grupo de campos CEE ao esquema, é possível adicionar outros grupos de campos, conforme necessário, para campos adicionais nos dados.

Depois de criar e salvar o esquema, você pode criar um novo conjunto de dados com base nesse esquema. Os seguintes tutoriais orientam o processo de criação de um novo conjunto de dados na interface ou na API:

* [Criar um conjunto de dados na interface](../catalog/datasets/user-guide.md#create) (Siga o fluxo de trabalho para usar um esquema existente)
* [Criar um conjunto de dados na API](../catalog/datasets/create.md)

Depois que o conjunto de dados for criado, você poderá encontrá-lo na interface do usuário do Experience Platform dentro do espaço de trabalho **[!UICONTROL Conjuntos de dados]**.

![](images/data-preparation/dataset-location.png)

#### Adicionar campos de identidade ao conjunto de dados

Se você estiver trazendo dados de [!DNL Adobe Audience Manager], [!DNL Adobe Analytics] ou outra fonte externa, você terá a opção de definir um campo de esquema como um campo de identidade. Para definir um campo de esquema como um campo de identidade, exiba a seção sobre como definir campos de identidade no [tutorial de interface do usuário](../xdm/tutorials/create-schema-ui.md#identity-field) ou no [tutorial de API](../xdm/tutorials/create-schema-api.md#define-an-identity-descriptor) para a criação de um esquema.

Se estiver assimilando dados de um arquivo CSV local, você pode pular para a próxima seção em [mapeando e assimilando dados](#ingest).

#### Mapear e assimilar dados {#ingest}

Depois de criar um esquema e um conjunto de dados CEE, você pode começar a mapear suas tabelas de dados para o esquema e assimilar esses dados na Experience Platform. Consulte o tutorial sobre [mapeamento de um arquivo CSV para um esquema XDM](../ingestion/tutorials/map-csv/overview.md) para obter etapas sobre como fazer isso na interface do usuário. Você pode usar o seguinte [arquivo JSON de amostra](https://github.com/AdobeDocs/experience-platform.pt-BR/blob/master/help/intelligent-services/assets/CEE_XDM_sample_rows.json) para testar o processo de assimilação antes de usar seus próprios dados.

Depois que um conjunto de dados é preenchido, o mesmo conjunto de dados pode ser usado para assimilar arquivos de dados adicionais.

Se seus dados estiverem armazenados em um aplicativo de terceiros com suporte, você também poderá optar por criar um [conector de origem](../sources/home.md) para assimilar seus dados de eventos de marketing no [!DNL Experience Platform] em tempo real.

## Próximas etapas {#next-steps}

Este documento forneceu orientação geral sobre como preparar seus dados para uso no [!DNL Intelligent Services]. Se você precisar de consultoria adicional com base em seu caso de uso, entre em contato com o Suporte da Adobe Consulting.

Depois de preencher com êxito um conjunto de dados com os dados de experiência do cliente, você pode usar o [!DNL Intelligent Services] para gerar insights. Consulte os seguintes documentos para começar:

* [Visão geral do Attribution AI](./attribution-ai/overview.md)
* [Visão geral do Customer AI](./customer-ai/overview.md)
