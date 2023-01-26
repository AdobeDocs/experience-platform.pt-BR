---
title: Conector de origem do Adobe Analytics para dados do conjunto de relatórios
description: Este documento fornece uma visão geral do Analytics e descreve os casos de uso para dados do Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 486f5bdd834808c6262f41c0b0187721fc9b0799
workflow-type: tm+mt
source-wordcount: '1040'
ht-degree: 6%

---

# Conector de origem do Adobe Analytics para dados do conjunto de relatórios

O Adobe Experience Platform permite assimilar dados do Adobe Analytics por meio do conector de origem do Analytics. O [!DNL Analytics] dados de fluxos do conector de origem coletados por [!DNL Analytics] para Plataforma em tempo real, convertendo formato SCDS [!DNL Analytics] dados em [!DNL Experience Data Model] (XDM) para consumo por plataforma.

Este documento fornece uma visão geral de [!DNL Analytics] e descreve os casos de uso para [!DNL Analytics] dados.

## Dados do Adobe Analytics e do Analytics

[!DNL Analytics] O é um mecanismo poderoso que ajuda você a saber mais sobre seus clientes, como eles interagem com suas propriedades da Web, a ver onde seu investimento em marketing digital é eficaz e a identificar áreas de aprimoramento. [!DNL Analytics] O lida com trilhões de transações da Web por ano e a variável [!DNL Analytics] o conector de origem permite que você toque facilmente em esses dados comportamentais avançados e enriqueça o [!DNL Real-Time Customer Profile] em questão de minutos.

![Um gráfico que ilustra a jornada de dados de diferentes aplicativos do Adobe, incluindo o Adobe Analytics.](./images/analytics-data-experience-platform.png)

Em um alto nível, [!DNL Analytics] O coleta dados de vários canais digitais e vários data centers em todo o mundo. Depois que os dados são coletados, as regras VISTA (Visitor Identification, Segmentation and Transformation Architecture) e as regras de processamento são aplicadas para moldar os dados recebidos. Depois que os dados brutos passarem por esse processamento leve, serão considerados prontos para consumo por [!DNL Real-Time Customer Profile]. Em um processo paralelo ao acima, os mesmos dados processados são microlotes e assimilados em conjuntos de dados da plataforma para consumo por [!DNL Data Science Workspace], [!DNL Query Service]e outros aplicativos de detecção de dados.

Consulte a [visão geral das regras de processamento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html) para obter mais informações sobre regras de processamento.

## Experience Data Model (XDM)

O XDM é uma especificação documentada publicamente que fornece estruturas e definições comuns para um aplicativo usar para se comunicar com serviços no Experience Platform.

O cumprimento dos padrões XDM permite que os dados sejam incorporados uniformemente, facilitando a entrega de dados e a coleta de informações.

Para saber mais sobre o XDM, consulte o [Visão geral do sistema XDM](../../../xdm/home.md).

## Como os campos são mapeados do Adobe Analytics para o XDM?

>[!IMPORTANT]
>
>As transformações da Preparação de dados podem adicionar latência ao fluxo de dados geral. A latência adicional adicionada varia com base na complexidade da lógica de transformação.

Quando uma conexão de origem é estabelecida para trazer [!DNL Analytics] dados no Experience Platform usando a interface do usuário do Platform, os campos de dados são mapeados e assimilados automaticamente no [!DNL Real-Time Customer Profile] em minutos. Para obter instruções sobre como criar uma conexão de origem com [!DNL Analytics] usando a interface do usuário da plataforma, consulte o [Tutorial do conector de origem do Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Para obter informações detalhadas sobre o mapeamento de campos que ocorre entre [!DNL Analytics] e Experience Platform, consulte a [Mapeamento de campo do Adobe Analytics](./mapping/analytics.md) guia.

## Qual é a latência esperada para os dados do Analytics na plataforma?

A latência esperada de dados do Analytics na plataforma é descrita na tabela abaixo. A latência varia de acordo com a configuração do cliente, os volumes de dados e os aplicativos do consumidor. Por exemplo, se a implementação do Analytics estiver configurada com `A4T` a latência para pipeline aumentará para 5-10 minutos.

| Dados do Analytics | Latência esperada |
| -------------- | ---------------- |
| Novos dados para [!DNL Real-Time Customer Profile] (A4T **not** ativado) | &lt; 2 minutos |
| Novos dados para [!DNL Real-Time Customer Profile] (A4T **é** ativado) | &lt; 15 minutos |
| Novos dados para o Data Lake | &lt; 90 minutos |
| Preenchimento retroativo de menos de 10 bilhões de eventos | &lt; 4 semanas |

Por padrão, os preenchimentos retroativos do Analytics são de 13 meses. O limite de 10 mil milhões de eventos mencionado no quadro acima é estritamente relativo à latência esperada.

>[!NOTE]
>
>Os dados de preenchimento retroativo do Analytics não são assimilados em [!DNL Profile] e, portanto, não é contabilizado em perfis de licença.

## Identificadores primários em [!DNL Analytics] dados

Cada ocorrência do [!DNL Analytics] O conector de origem contém um identificador principal que depende da existência de uma ECID ou de um AAID. Se houver uma ECID, a ECID será designada como o identificador principal. Se houver um AAID, o AAID será designado como o principal.

A tabela a seguir fornece mais informações sobre campos de identidade em seu [!DNL Analytics] dados.

| Campo de identidade | Descrição |
| --- | --- |
| AAID | O AAID é o principal identificador de dispositivo no Adobe Analytics e tem garantia de que existe em todos os eventos passados pelo [!DNL Analytics] fonte. O AAID é, por vezes, chamado de *ID herdada do Analytics* ou como `s_vi` ID do cookie. Apesar disso, um AAID é criado mesmo se a variável `s_vi` cookie não está presente. O AAID é representado pelo `post_visid_high` e `post_visid_low` colunas em [[!DNL Analytics] feeds de dados](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=pt-BR). Em qualquer evento, o campo AAID contém uma única identidade que pode ser um dos vários tipos diferentes descritos no [ordem das operações [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Observação**: Em um conjunto de relatórios inteiro, um AAID pode conter uma combinação de tipos entre eventos. |
| ECID | A ECID (Experience Cloud ID) é um campo identificador de dispositivo separado, que é preenchido no Adobe Analytics quando [!DNL Analytics] é implementada usando o Serviço de identidade do Experience Cloud. A ECID às vezes também é chamada de MCID (ID do Marketing Cloud). Se uma ECID existir em um evento, a AAID poderá se basear na ECID, dependendo se o Analytics [período de carência](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) está configurado. A ECID é representada pela variável `mcvisid` nos feeds de dados do Analytics. Para obter mais informações sobre a ECID, consulte o [Visão geral da ECID](../../../identity-service/ecid.md). Para obter informações sobre como a ECID funciona com o [!DNL Analytics], consulte o documento em [Solicitações do Analytics e do Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html?lang=pt-BR). |
| AACUSTOMID | A AACUSTOMID é um campo de identificador separado, preenchido no Adobe Analytics com base no uso da variável `s.VisitorID` na variável [!DNL Analytics] implementação. O AACUSTOMID é representado pela variável `cust_visid` coluna em [[!DNL Analytics] feeds de dados](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=pt-BR). Se a AACUSTOMID estiver presente, a AAID será baseada na AACUSTOMID porque a AACUSTOMID agrupa todos os outros identificadores, conforme definido pela variável [ordem das operações [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Como a função [!DNL Analytics] identidades de tratamento de origem

O [!DNL Analytics] A fonte transmite essas identidades para o Experience Platform no formulário XDM como:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Esses campos não são marcados como identidades. Em vez disso, as mesmas identidades são copiadas para o `identityMap` como pares de valores chave:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

No mapa de identidade, se ECID estiver presente, ele será marcado como a identidade primária do evento. Nesse caso, o AAID pode se basear na ECID devido ao [Período de carência do Serviço de identidade](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). Caso contrário, a AAID é marcada como a identidade principal do evento. AACUSTOMID nunca é marcada como a ID principal do evento. No entanto, se AACUSTOMID estiver presente, o AAID será baseado no AACUSTOMID devido à ordem Experience Cloud das operações.