---
title: Conector de origem do Adobe Analytics para dados do conjunto de relatórios
description: Este documento fornece uma visão geral do Analytics e descreve os casos de uso para dados do Analytics.
exl-id: c4887784-be12-40d4-83bf-94b31eccdc2e
source-git-commit: 251b00e0f0e063859f8d0a0e188fa805c7bf3f87
workflow-type: tm+mt
source-wordcount: '1110'
ht-degree: 2%

---

# Conector de origem do Adobe Analytics para dados do conjunto de relatórios

O Adobe Experience Platform permite assimilar dados do Adobe Analytics por meio do conector de origem do Analytics. A variável [!DNL Analytics] o conector de origem transmite dados coletados pelo [!DNL Analytics] para a Platform em tempo real, convertendo arquivos formatados em SCDS [!DNL Analytics] entrada de dados [!DNL Experience Data Model] Campos do (XDM) para consumo pela Platform.

Este documento fornece uma visão geral de [!DNL Analytics] e descreve os casos de uso para [!DNL Analytics] dados.

## Dados do Adobe Analytics e do Analytics

[!DNL Analytics] O é um mecanismo poderoso que ajuda você a saber mais sobre os clientes, como eles interagem com as propriedades da Web, ver onde o investimento em marketing digital é eficaz e identificar áreas de melhoria. [!DNL Analytics] processa trilhões de transações via web por ano e o [!DNL Analytics] conector de origem permite que você acesse facilmente esses dados comportamentais avançados e enriqueça a [!DNL Real-Time Customer Profile] em questão de minutos.

![Um gráfico que ilustra a jornada de dados de diferentes aplicativos Adobe, incluindo o Adobe Analytics.](./images/analytics-data-experience-platform.png)

Em um alto nível, [!DNL Analytics] O coleta dados de vários canais digitais e vários data centers em todo o mundo. Depois que os dados são coletados, as regras de identificação do visitante, arquitetura de segmentação e transformação (VISTA) e as regras de processamento são aplicadas para moldar os dados recebidos. Depois que os dados brutos passam por esse processamento leve, eles são considerados prontos para consumo pela [!DNL Real-Time Customer Profile]. Em um processo paralelo ao mencionado acima, os mesmos dados processados são microarmazenados em lote e assimilados em conjuntos de dados da plataforma para consumo pelo [!DNL Query Service]e outros aplicativos de detecção de dados.

Consulte a [visão geral das regras de processamento](https://experienceleague.adobe.com/docs/analytics/admin/admin-tools/processing-rules/processing-rules.html?lang=pt-BR) para obter mais informações sobre as regras de processamento.

## Experience Data Model (XDM)

O XDM é uma especificação documentada publicamente que fornece estruturas e definições comuns para um aplicativo usar para se comunicar com serviços no Experience Platform.

Seguir os padrões XDM permite que os dados sejam incorporados uniformemente, facilitando a entrega de dados e a coleta de informações.

Para saber mais sobre o XDM, consulte a [Visão geral do sistema XDM](../../../xdm/home.md).

## Como os campos são mapeados do Adobe Analytics para o XDM?

>[!IMPORTANT]
>
>As transformações de Preparo de dados podem adicionar latência ao fluxo de dados geral. A latência adicional adicionada varia de acordo com a complexidade da lógica de transformação.

Quando uma conexão de origem é estabelecida para trazer [!DNL Analytics] dados no Experience Platform usando a interface do usuário da Platform, os campos de dados são mapeados e assimilados automaticamente no [!DNL Real-Time Customer Profile] em minutos. Para obter instruções sobre como criar uma conexão de origem com [!DNL Analytics] usando a interface do Platform, consulte a [Tutorial do conector de origem do Analytics](../../tutorials/ui/create/adobe-applications/analytics.md).

Para obter informações detalhadas sobre o mapeamento de campos que ocorre entre [!DNL Analytics] e Experience Platform, consulte a [Mapeamento de campo do Adobe Analytics](./mapping/analytics.md) guia.

## Qual é a latência esperada para dados do Analytics na plataforma?

A latência esperada para dados do Analytics na plataforma é descrita na tabela abaixo. A latência varia dependendo da configuração do cliente, dos volumes de dados e dos aplicativos do consumidor. Por exemplo, se a implementação do Analytics estiver configurada com `A4T` a latência para o pipeline aumentará de 5 a 10 minutos.

| Dados do Analytics | Latência esperada |
| -------------- | ---------------- |
| Novos dados para o [!DNL Real-Time Customer Profile] (A4T **não** ativado) | &lt; 2 minutos |
| Novos dados para o [!DNL Real-Time Customer Profile] (A4T **é** ativado) | até 30 minutos |
| Novos dados para o Data Lake | &lt; 90 minutos |
| Preenchimento retroativo de menos de 10 bilhões de eventos | &lt; 4 semanas |

O preenchimento retroativo do Analytics para sandboxes de produção assume o padrão de 13 meses. Para dados do Analytics em sandboxes de não produção, o preenchimento retroativo é definido como três meses. O limite de 10 bilhões de eventos mencionados na tabela acima diz respeito estritamente à latência esperada.

Ao criar um fluxo de dados de origem do Analytics em uma sandbox de produção, dois fluxos de dados são criados:

* Um fluxo de dados que faz um preenchimento retroativo de 13 meses de dados históricos do conjunto de relatórios no data lake. Esse fluxo de dados termina quando o preenchimento retroativo é concluído.
* Um fluxo de dados que envia dados em tempo real para o data lake e o [!DNL Real-Time Customer Profile]. Esse fluxo de dados é executado continuamente.

>[!NOTE]
>
>Os dados de preenchimento retroativo do Analytics não são assimilados na [!DNL Profile] e, portanto, não é contabilizado em perfis de licença.

## Identificadores primários em [!DNL Analytics] dados

Cada ocorrência do [!DNL Analytics] O conector de origem contém um identificador principal que depende de uma ECID ou AAID existir. Se houver uma ECID, a ECID será designada como o identificador principal. Se houver uma AAID, ela será designada como a principal.

A tabela a seguir fornece mais informações sobre os campos de identidade na [!DNL Analytics] dados.

| Campo de identidade | Descrição |
| --- | --- |
| AAID | A AAID é o principal identificador de dispositivo no Adobe Analytics e sua presença está garantida em cada evento transmitido pela [!DNL Analytics] origem. Por vezes, a AAID é designada por *ID herdada do Analytics* ou como `s_vi` ID do cookie. Apesar disso, é criada uma AAID, mesmo que a `s_vi` o cookie não está presente. A AAID é representada pela `post_visid_high` e `post_visid_low` colunas em [[!DNL Analytics] feeds de dados](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=pt-BR). Em qualquer evento, o campo AAID contém uma única identidade que pode ser um dos vários tipos diferentes descritos no [ordem de operação para [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). **Nota**: em um conjunto de relatórios inteiro, uma AAID pode conter uma combinação de tipos entre eventos. |
| ECID | A ECID (ID de Experience Cloud) é um campo de identificador de dispositivo separado, que é preenchido no Adobe Analytics quando [!DNL Analytics] é implementado usando o Serviço de identidade Experience Cloud. Às vezes, a ECID também é chamada de MCID (ID do Marketing Cloud). Se uma ECID existir em um evento, a AAID poderá se basear na ECID, dependendo se a variável Analytics [período de carência](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html) está configurado. A ECID é representada pela variável `mcvisid` nos feeds de dados do Analytics. Para obter mais informações sobre a ECID, consulte [Visão geral da ECID](../../../identity-service/ecid.md). Para obter informações sobre como a ECID funciona com a [!DNL Analytics], consulte o documento sobre [Solicitações do Analytics e da Experience Cloud ID](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/legacy-analytics.html). |
| AACUSTOMID | A AACUSTOMID é um campo de identificador separado, preenchido no Adobe Analytics com base no uso da variável `s.VisitorID` na variável [!DNL Analytics] execução. A AACUSTOMID é representada pela variável `cust_visid` coluna em [[!DNL Analytics] feeds de dados](https://experienceleague.adobe.com/docs/analytics/export/analytics-data-feed/data-feed-contents/datafeeds-reference.html?lang=pt-BR). Se a AACUSTOMID estiver presente, a AAID será baseada na AACUSTOMID, pois ela supera todos os outros identificadores, conforme definido pela [ordem de operação para [!DNL Analytics] IDs](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/analytics-order-of-operations.html). |

### Como o [!DNL Analytics] origem trata identidades

A variável [!DNL Analytics] A origem passa essas identidades para o Experience Platform no formato XDM como:

* `endUserIDs._experience.aaid.id`
* `endUserIDs._experience.mcid.id`
* `endUserIDs._experience.aacustomid.id`

Esses campos não são marcados como identidades. Em vez disso, as mesmas identidades são copiadas para o XDM `identityMap` como pares de valor-chave:

* `{ "key": "AAID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "ECID", "value": [ { "id": "<identity>", "primary": <true or false> } ] }`
* `{ "key": "AACUSTOMID", "value": [ { "id": "<identity>", "primary": false } ] }`

No mapa de identidade, se a ECID estiver presente, ela será marcada como a identidade principal do evento. Nesse caso, a AAID pode se basear na ECID devido à [Período de carência do Serviço de identidade](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/grace-period.html). Caso contrário, a AAID será marcada como a identidade principal do evento. AACUSTOMID nunca é marcada como a ID principal do evento. No entanto, se a AACUSTOMID estiver presente, a AAID será baseada na AACUSTOMID devido à ordem Experience Cloud das operações.

>[!NOTE]
>
>Você pode usar o Preparo de dados para filtrar identidades secundárias provenientes do Analytics, como AAID e AACUSTOMID. Se filtradas, essas identidades não serão assimiladas no Perfil se estiverem disponíveis nos dados de entrada do Analytics. Os dados não filtrados continuarão a ser carregados no data lake.
