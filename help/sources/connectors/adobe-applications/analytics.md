---
title: Conector de origem do Adobe Analytics para dados do conjunto de relatórios
description: Este documento fornece uma visão geral do Analytics e descreve os casos de uso para dados do Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 60447ef6f881bf2a34f5502f2259328bf73d08c0
workflow-type: tm+mt
source-wordcount: '1345'
ht-degree: 0%

---

# Conector de origem do Adobe Analytics para dados do conjunto de relatórios

O Adobe Experience Platform permite assimilar dados do Adobe Analytics por meio do conector de origem do Analytics. O conector de origem [!DNL Analytics] transmite dados coletados por [!DNL Analytics] para o Experience Platform em tempo real, convertendo dados [!DNL Analytics] formatados em SCDS em campos [!DNL Experience Data Model] (XDM) para consumo do Experience Platform.

Este documento fornece uma visão geral do [!DNL Analytics] e descreve os casos de uso para dados do [!DNL Analytics].

## Dados do Adobe Analytics e do Analytics

O [!DNL Analytics] é um mecanismo eficiente que ajuda você a saber mais sobre os clientes, como eles interagem com as propriedades da Web, ver onde o marketing digital é eficaz e identificar áreas de aprimoramento. O [!DNL Analytics] lida com trilhões de transações da web por ano e o conector de origem do [!DNL Analytics] permite que você acesse facilmente esses dados comportamentais avançados e enriqueça o [!DNL Real-Time Customer Profile] em questão de minutos.

![Um gráfico que ilustra a jornada de dados de diferentes aplicativos da Adobe, incluindo o Adobe Analytics.](./images/analytics-data-experience-platform.png)

Em um nível superior, o [!DNL Analytics] coleta dados de vários canais digitais e vários data centers no mundo inteiro. Depois que os dados são coletados, as regras de identificação do visitante, arquitetura de segmentação e transformação (VISTA) e as regras de processamento são aplicadas para moldar os dados recebidos. Após dados brutos terem passado por esse processamento leve, ele é considerado pronto para consumo por [!DNL Real-Time Customer Profile]. Em um processo paralelo ao mencionado acima, os mesmos dados processados são em microlote e assimilados em conjuntos de dados do Experience Platform para consumo pelo [!DNL Query Service] e outros aplicativos de descoberta de dados.

Consulte a [visão geral das regras de processamento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=pt-BR) para obter mais informações sobre regras de processamento.

## Experience Data Model (XDM)

O XDM é uma especificação documentada publicamente que fornece estruturas e definições comuns para um aplicativo usar para se comunicar com os serviços na Experience Platform.

Seguir os padrões XDM permite que os dados sejam incorporados uniformemente, facilitando a entrega de dados e a coleta de informações.

Para saber mais sobre o XDM, consulte a [Visão geral do sistema XDM](../../../xdm/home.md).

## Como os campos são mapeados do Adobe Analytics para o XDM?

>[!IMPORTANT]
>
>As transformações de Preparo de dados podem adicionar latência ao fluxo de dados geral. A latência adicional adicionada varia de acordo com a complexidade da lógica de transformação.

Quando uma conexão de origem é estabelecida para trazer dados do [!DNL Analytics] para o Experience Platform usando a interface do usuário do Experience Platform, os campos de dados são mapeados e assimilados automaticamente no [!DNL Real-Time Customer Profile] em minutos. Para obter instruções sobre como criar uma conexão de origem com [!DNL Analytics] usando a interface do usuário do Experience Platform, consulte o [Tutorial do conector de origem do Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Para obter informações detalhadas sobre o mapeamento de campos que ocorre entre o [!DNL Analytics] e o Experience Platform, consulte o guia de [mapeamento de campos do Adobe Analytics](./mapping/analytics.md).

>[!TIP]
>
>Siga estas práticas recomendadas para não exceder seus direitos de licença e sobrecarregar suas métricas de armazenamento total e riqueza de dados:
>
>* Configure o TTL (Time-To-Live, tempo de vida útil) de retenção do conjunto de dados do evento de experiência no início para otimizar o gerenciamento do ciclo de vida dos dados e a eficiência do armazenamento. Para obter mais detalhes, consulte o manual sobre [gerenciamento da Retenção do Conjunto de Dados do Evento de Experiência no data lake usando TTL](../../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md).
>
>* Ao criar um fluxo de dados de origem do Analytics, comece configurando o conector para assimilar dados somente no data lake. Depois de confirmar que o fluxo de dados está funcionando, você pode ativar a assimilação de perfis para o conjunto de dados. Essa abordagem funciona melhor quando os filtros de linha e coluna reduzem efetivamente o volume de dados. Saiba mais na documentação [conectando o Adobe Analytics ao Experience Platform](../../tutorials/ui/create/adobe-applications/analytics.md).

## Qual é a latência esperada para dados do Analytics no Experience Platform?

A latência esperada para dados do Analytics no Experience Platform é descrita na tabela abaixo. A latência varia dependendo da configuração do cliente, dos volumes de dados e dos aplicativos do consumidor. Por exemplo, se a implementação do Analytics estiver configurada com `A4T`, a latência para o Pipeline aumentará de 5 a 10 minutos.

| Dados do Analytics | Latência esperada |
| -------------- | ---------------- |
| Novos dados para [!DNL Real-Time Customer Profile] (A4T **não** habilitado) | &lt; 2 minutos |
| Novos dados para [!DNL Real-Time Customer Profile] (A4T **está** habilitado) | até 30 minutos |
| Novos dados para o Data Lake | &lt; 2,25 horas |
| Novos dados para o Customer Journey Analytics sem [compilação](https://experienceleague.adobe.com/docs/analytics-platform/using/stitching/overview.html?lang=pt-BR) | &lt; 3,75 horas |
| Novos dados para o Customer Journey Analytics com compilação | &lt; 7 horas |
| Preenchimento retroativo de menos de 10 bilhões de eventos | &lt; 4 semanas |

Para obter mais informações sobre latências de Customer Journey Analytics, consulte: [Medidas de Proteção do Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-admin/guardrails.html?lang=pt-BR).

O preenchimento retroativo do Analytics para sandboxes de produção assume o padrão de 13 meses. Para dados do Analytics em sandboxes de não produção, o preenchimento retroativo é definido como três meses. O limite de 10 bilhões de eventos mencionados na tabela acima diz respeito estritamente à latência esperada.

Para sandboxes de produção, se você tiver licenciado o SKU adicional que o autoriza a importar mais de 13 meses de dados históricos de preenchimento retroativo, entre em contato com a Adobe para solicitar o preenchimento retroativo estendido.

Ao criar um fluxo de dados de origem do Analytics em uma sandbox de produção, dois fluxos de dados são criados:

* Um fluxo de dados que faz um preenchimento retroativo de 13 meses de dados históricos do conjunto de relatórios no data lake. Esse fluxo de dados termina quando o preenchimento retroativo é concluído.
* Um fluxo de dados que envia dados em tempo real para o data lake e para [!DNL Real-Time Customer Profile]. Esse fluxo de dados é executado continuamente.

>[!NOTE]
>
>Os dados de preenchimento retroativo do Analytics não são assimilados em [!DNL Profile] e, portanto, não são contabilizados em perfis de licença.

## Identificadores primários em dados [!DNL Analytics]

Cada ocorrência do conector de origem [!DNL Analytics] contém um identificador principal dependente da existência de uma ECID ou AAID. Se houver uma ECID, a ECID será designada como o identificador principal. Se houver uma AAID, ela será designada como a principal.

A tabela a seguir fornece mais informações sobre campos de identidade nos dados do [!DNL Analytics].

| Campo de identidade | Descrição |
| --- | --- |
| AAID | A AAID é o principal identificador de dispositivo no Adobe Analytics e sua presença está garantida em todos os eventos transmitidos pela origem [!DNL Analytics]. Às vezes, a AAID é chamada de *ID herdada do Analytics* ou de `s_vi` ID do cookie. Apesar disso, uma AAID é criada mesmo se o cookie `s_vi` não estiver presente. A AAID é representada pelas colunas `post_visid_high` e `post_visid_low` em [[!DNL Analytics] feeds de dados](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=pt-BR). Em qualquer evento, o campo AAID contém uma única identidade que pode ser um dos vários tipos diferentes descritos na [ordem das operações para [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html?lang=pt-BR). **Observação**: em um conjunto de relatórios inteiro, uma AAID pode conter uma combinação de tipos entre eventos. |
| ECID | A ECID (Experience Cloud ID) é um campo de identificador de dispositivo separado, que é preenchido no Adobe Analytics quando [!DNL Analytics] é implementado usando o Experience Cloud Identity Service. Às vezes, a ECID também é chamada de MCID (Marketing Cloud ID). Se uma ECID existir em um evento, a AAID poderá se basear na ECID, dependendo se o [período de carência](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html?lang=pt-BR) do Analytics está configurado. A ECID é representada pelo `mcvisid` nos feeds de dados do Analytics. Para obter mais informações sobre a ECID, consulte a [visão geral da ECID](../../../identity-service/features/ecid.md). Para obter informações sobre como a ECID funciona com [!DNL Analytics], consulte o documento sobre [Solicitações do Analytics e da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=pt-BR). |
| AACUSTOMID | A AACUSTOMID é um campo de identificador separado, preenchido no Adobe Analytics com base no uso da variável `s.VisitorID` na implementação [!DNL Analytics]. A AACUSTOMID é representada pela coluna `cust_visid` em [[!DNL Analytics] feeds de dados](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=pt-BR). Se a AACUSTOMID estiver presente, a AAID será baseada na AACUSTOMID, pois a AACUSTOMID supera todos os outros identificadores, conforme definido pela [ordem de operações para [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html?lang=pt-BR). |

### Como a origem [!DNL Analytics] trata identidades

A origem [!DNL Analytics] passa essas identidades para o Experience Platform no formato XDM como:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Esses campos não são marcados como identidades. Em vez disso, as mesmas identidades (se presentes no evento) são copiadas para o `identityMap` do XDM como pares de valores chave:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

Quando a identidade ou identidades são copiadas para `identityMap`, `endUserIDs._experience.mcid.namespace.code` também é definido no mesmo evento:

* Se a AAID estiver presente, `endUserIDs._experience.aaid.namespace.code` será definido como &quot;AAID&quot;.
* Se a ECID estiver presente, `endUserIDs._experience.mcid.namespace.code` será definido como &quot;ECID&quot;.
* Se AACUSTOMID estiver presente, `endUserIDs._experience.aacustomid.namespace.code` será definido como &quot;AACUSTOMID&quot;.

No mapa de identidade, se a ECID estiver presente, ela será marcada como a identidade principal do evento. Nesse caso, a AAID pode se basear na ECID devido ao [período de carência do Serviço de identidade](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html?lang=pt-BR). Caso contrário, a AAID será marcada como a identidade principal do evento. AACUSTOMID nunca é marcada como a ID primária do evento. No entanto, se a AACUSTOMID estiver presente, a AAID será baseada na AACUSTOMID devido à ordem de operações da Experience Cloud.

>[!NOTE]
>
>Você pode usar o Preparo de dados para filtrar identidades secundárias provenientes do Analytics, como AAID e AACUSTOMID. Se filtradas, essas identidades não serão assimiladas no Perfil se estiverem disponíveis nos dados de entrada do Analytics. Os dados não filtrados continuarão a ser carregados no data lake.
