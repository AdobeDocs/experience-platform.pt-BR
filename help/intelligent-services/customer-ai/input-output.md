---
keywords: Experience Platform, introdução, atendimento ao cliente, tópicos populares, entrada de atendimento ao cliente, saída de atendimento ao cliente
solution: Experience Platform, Intelligent Services, Real-time Customer Data Platform
title: Entrada e saída no Customer AI
topic-legacy: Getting started
description: Saiba mais sobre os eventos, entradas e saídas necessários utilizados pela API do cliente.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: c534b66d7617023df8dbac57115036146c2cab01
workflow-type: tm+mt
source-wordcount: '2971'
ht-degree: 1%

---

# Entrada e saída no Customer AI

O documento a seguir descreve os diferentes eventos, entradas e saídas necessários utilizados na API do cliente.

## Introdução

O Customer AI funciona analisando um dos seguintes conjuntos de dados para prever pontuações de abandono ou propensão de conversão:

- Conjunto de dados CEE (Evento de experiência do consumidor)
- Dados do Adobe Analytics usando o [conector de origem do Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Dados do Adobe Audience Manager usando o [conector de fonte Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)

>[!IMPORTANT]
>
>Os conectores de origem levam até quatro semanas para preencher dados. Se você tiver configurado um conector recentemente, verifique se o conjunto de dados tem o comprimento mínimo de dados necessário para a API do cliente. Revise a seção [histórico de dados](#data-requirements) para verificar se você tem dados suficientes para sua meta de previsão.

Este documento requer uma compreensão básica do esquema CEE. Consulte a documentação de [Preparação de dados dos Serviços inteligentes](../data-preparation.md) antes de continuar.

A tabela a seguir descreve algumas terminologias comuns usadas neste documento:

| Termo | Definição |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | O XDM é a estrutura fundamental que permite ao Adobe Experience Cloud, desenvolvido pela Adobe Experience Platform, enviar a mensagem certa para a pessoa certa, no canal certo, no momento certo. A metodologia na qual o Experience Platform é criado, o Sistema XDM, opera esquemas do Experience Data Model para uso pelos serviços da plataforma. |
| Esquema do XDM | A Experience Platform utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados. Para que os dados possam ser assimilados na Platform, um schema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que pode ser contido em cada campo. Os esquemas consistem em uma classe base XDM e zero ou mais grupos de campos de esquema. |
| Classe XDM | Todos os esquemas XDM descrevem dados que podem ser categorizados como registro ou série de tempo. O comportamento de dados de um schema é definido pela classe do schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM descrevem o menor número de propriedades que um schema deve conter para representar um comportamento de dados específico. |
| [Grupos de campos](../../xdm/schema/composition.md) | Um componente que define um ou mais campos em um schema. Os grupos de campos impõem como seus campos aparecem na hierarquia do esquema e, portanto, exibem a mesma estrutura em cada esquema em que estão incluídos. Os grupos de campos são compatíveis apenas com classes específicas, conforme identificado pelo atributo `meta:intendedToExtend`. |
| [Tipo de dados](../../xdm/schema/composition.md) | Um componente que também pode fornecer um ou mais campos para um schema. No entanto, ao contrário de grupos de campos, os tipos de dados não estão restritos a uma classe específica. Isso torna os tipos de dados uma opção mais flexível para descrever estruturas de dados comuns que são reutilizáveis em vários esquemas com classes potencialmente diferentes. Os tipos de dados descritos neste documento são compatíveis com os esquemas CEE e Adobe Analytics. |
| Churn | Uma medida da porcentagem de contas que cancelam ou optam por não renovar suas assinaturas. Uma alta taxa de churn pode afetar negativamente a Receita recorrente mensal (MRR) e também pode indicar insatisfação com um produto ou serviço. |
| [Perfil do cliente em tempo real](../../profile/home.md) | O Perfil do cliente em tempo real oferece um perfil de consumidor centralizado para gerenciamento de experiência direcionado e personalizado. Cada perfil contém dados agregados em todos os sistemas, bem como contas acionáveis com carimbos de data e hora de eventos que envolvem o indivíduo e que ocorreram em qualquer um dos sistemas usados com o Experience Platform. |

## Dados de entrada do Customer AI

>[!TIP]
>
> O Customer AI determina automaticamente quais eventos são úteis para previsões e emite um aviso se os dados disponíveis não forem suficientes para gerar previsões de qualidade.

O Customer AI é compatível com conjuntos de dados CEE, Adobe Analytics e Adobe Audience Manager. O esquema CEE requer que você adicione grupos de campos durante o processo de criação do schema. Se você estiver usando conjuntos de dados do Adobe Analytics ou Adobe Audience Manager, o conector de origem mapeia diretamente os eventos padrão (Comércio, detalhes da página da Web, Aplicativo e Pesquisa) listados abaixo durante o processo de conexão.

Para obter mais informações sobre o mapeamento de dados do Adobe Analytics ou de Audience Manager, visite o guia [Mapeamentos de campo do Analytics](../../sources/connectors/adobe-applications/analytics.md) ou [Mapeamentos de campo Audience Manager](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

### Eventos padrão usados pelo Customer AI {#standard-events}

Os Eventos de experiência XDM são usados para determinar vários comportamentos do cliente. Dependendo de como seus dados são estruturados, os tipos de evento listados abaixo podem não abranger todos os comportamentos do cliente. Cabe a você determinar quais campos têm os dados necessários para identificar clara e inequivocamente a atividade do usuário da Web. Dependendo da meta de previsão, os campos necessários podem ser alterados.

O Customer AI depende de tipos de evento diferentes para criar recursos do modelo. Esses tipos de eventos são adicionados automaticamente ao esquema usando vários grupos de campos XDM.

>[!NOTE]
>
>Se você estiver usando dados do Adobe Analytics ou Adobe Audience Manager, o esquema será criado automaticamente com os eventos padrão necessários para capturar seus dados. Se você estiver criando seu próprio esquema CEE personalizado para capturar dados, precisará considerar quais grupos de campos são necessários para capturar seus dados.

Não é necessário ter dados para cada um dos eventos padrão listados abaixo, mas determinados eventos são necessários para determinados cenários. Se você tiver algum dos dados de eventos padrão disponíveis, é recomendável incluí-lo no esquema . Por exemplo, se você quisesse criar um aplicativo do Customer AI para prever eventos de compra, seria útil ter dados dos tipos de dados `Commerce` e `Web page details` .

Para exibir um grupo de campos na interface do usuário da plataforma, selecione a guia **[!UICONTROL Schemas]** no painel à esquerda, em seguida, selecione a guia **[!UICONTROL Field groups]**.

| Grupo de campos | Tipo de evento | Caminho do campo XDM |
| --- | --- | --- |
| [!UICONTROL Detalhes de comércio] | pedido | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | check-outs | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | compras | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemoments | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
|  | productListOpens | <li> commerce.productListOpens.value </li> <li> productListItems.SKU </li> |
|  | productViews | <li> commerce.productViews.value </li> <li> productListItems.SKU </li> |
| [!UICONTROL Detalhes da Web] | webVisit | web.webPageDetails.name |
|  | webInteraction | web.webInteraction.linkClicks.value |
| [!UICONTROL Detalhes do aplicativo] | applicationCloses | <li> application.applicationCloses.value </li> <li> application.name </li> |
|  | applicationCrashes | <li> application.crashes.value </li> <li> application.name </li> |
|  | applicationFeatureUsages | <li> application.featureUsages.value </li> <li> application.name </li> |
|  | applicationFirstLaunches | <li> application.firstLaunches.value </li> <li> application.name </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> application.name </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> application.name </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> application.name </li> |
| [!UICONTROL Detalhes da pesquisa] | pesquisa | search.keywords |

Além disso, o Customer AI pode usar os dados de assinatura para criar melhores modelos de rotatividade. Os dados de assinatura são necessários para cada perfil usando o formato de tipo de dados [[!UICONTROL Subscription]](../../xdm/data-types/subscription.md) . A maioria dos campos é opcional, no entanto, para um modelo de rotatividade ideal, é altamente recomendável fornecer dados para o maior número possível de campos, como `startDate`, `endDate` e quaisquer outros detalhes relevantes.

### Adicionar grupos de campos personalizados

Se você tiver informações adicionais que deseja incluir além dos [campos de evento padrão](#standard-events) usados pelo Customer AI. Uma opção de eventos personalizados é fornecida durante a [configuração de instância](./user-guide/configure.md#custom-events).

Se o conjunto de dados selecionado incluir eventos personalizados, como uma reserva de hotel ou restaurante definida em seu esquema, você poderá adicioná-los à sua instância. Esses eventos personalizados adicionais são usados pela API do cliente para melhorar a qualidade do modelo e fornecer resultados mais precisos.

### Dados históricos {#data-requirements}

O Customer AI exige dados históricos para o treinamento do modelo, mas a quantidade de dados necessária é baseada em dois elementos principais: janela de resultados e população elegível.

Por padrão, o Customer AI procura que um usuário tenha tido atividade nos últimos 120 dias se nenhuma definição de população qualificada for fornecida durante a configuração do aplicativo. Além disso, a API do cliente requer um mínimo de 500 eventos qualificados e 500 eventos não qualificados (total de 1000) de dados históricos com base em uma definição de meta prevista.

Os exemplos a seguir fornecidos usam uma fórmula simples para ajudar você a determinar a quantidade mínima de dados necessária. Se você tiver mais do que o requisito mínimo, seu modelo provavelmente fornecerá resultados mais precisos. Se você tiver menos do que o mínimo necessário, o modelo falhará, pois não há quantidade suficiente de dados para o treinamento do modelo.

**Fórmula**:

Comprimento mínimo dos dados necessários = população elegível + janela de resultados

>[!NOTE]
>
> 30 é o número mínimo de dias necessário para a população elegível. Se isso não for fornecido, o padrão será 120 dias.

Exemplos :

- Você deseja prever se um cliente provavelmente comprará um relógio nos próximos 30 dias. Você também deseja pontuar os usuários que têm alguma atividade da Web nos últimos 60 dias. Nesse caso, o comprimento mínimo de dados exigido é de 60 dias + 30 dias. A população elegível é de 60 dias e a janela de resultado é de 30 dias, totalizando 90 dias.

- Você deseja prever se o usuário provavelmente comprará um relógio nos próximos 7 dias. Nesse caso, o comprimento mínimo de dados exigido é de 120 dias + 7 dias. O padrão da população elegível é 120 dias e a janela de resultado é 7 dias, totalizando 127 dias.

- Você deseja prever se o cliente provavelmente comprará um relógio nos próximos 7 dias. Você também deseja pontuar os usuários que têm alguma atividade da Web nos últimos 7 dias. Nesse caso, o comprimento mínimo de dados exigido é de 30 dias + 7 dias. A população elegível requer um mínimo de 30 dias e a janela de resultados é de 7 dias, totalizando 37 dias.

Além dos dados mínimos necessários, o Customer AI também funciona melhor com dados recentes. Nesse caso de uso, a API do cliente faz uma previsão para o futuro com base nos dados comportamentais recentes de um usuário. Em outras palavras, dados mais recentes provavelmente produzirão uma previsão mais precisa.

### Cenários de exemplo

Nesta seção, cenários diferentes para instâncias do Customer AI são descritos, bem como os tipos de evento necessários e recomendados. Consulte a [tabela de eventos padrão](#standard-events) acima para obter mais informações sobre o grupo de campos e seu caminho de campo.

>[!NOTE]
>
> Os tipos de evento obrigatórios são usados para identificar clara e inequivocamente a atividade do usuário da Web. O número de tipos de evento necessários será alterado com base na meta de previsão e na estrutura do esquema. Se você não tiver certeza de que um determinado tipo de evento é necessário, é recomendável incluir esse tipo de evento ao criar seu esquema CEE. Se você estiver usando dados do Adobe Analytics ou Adobe Audience Manager, os eventos padrão necessários devem estar disponíveis, dependendo dos dados que você está fazendo streaming.

### Cenário 1: Conversão de compra em um site de varejo de comércio eletrônico

**Objetivo de previsão:** prevê a tendência de conversão para que os perfis elegíveis comprem um determinado artigo de roupas em um site.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída de IA do cliente ideal com esse objetivo de previsão específico. É possível excluir um evento necessário dependendo do objetivo da sua previsão, no entanto, excluir vários eventos pode levar a resultados ruins.

- pedido
- check-outs
- compras
- webVisit
- pesquisa

**Tipos de evento padrão recomendados adicionais:**

Qualquer um dos [tipos de evento restantes](#standard-events) pode ser necessário com base na complexidade de sua meta e população qualificada ao configurar a instância do Customer AI. É recomendável que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 2: Conversão de assinatura em um site de serviço de transmissão de mídia

**Objetivo de previsão:** prevê a propensão de conversão de assinatura para que os perfis qualificados se comprometam a um determinado nível de assinatura, como um plano padrão ou premium.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída de IA do cliente ideal com esse objetivo de previsão específico. É possível excluir um evento necessário dependendo do objetivo da sua previsão, no entanto, excluir vários eventos pode levar a resultados ruins.

- pedido
- check-outs
- compras
- webVisit
- pesquisa

Neste exemplo, `order`, `checkouts` e `purchases` são usados para indicar que uma assinatura foi comprada e seu tipo.

Além disso, para um modelo preciso, sugerimos que você use algumas das propriedades disponíveis no [subscription data type](../../xdm/data-types/subscription.md).

**Tipos de evento padrão recomendados adicionais:**

Qualquer um dos [tipos de evento restantes](#standard-events) pode ser necessário com base na complexidade de sua meta e população qualificada ao configurar a instância do Customer AI. É recomendável que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 3: Churn em um site de varejo de comércio eletrônico

**Objetivo de previsão:** prevê a probabilidade de um evento de compra não ocorrer.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída de IA do cliente ideal com esse objetivo de previsão específico. É possível excluir um evento necessário dependendo do objetivo da sua previsão, no entanto, excluir vários eventos pode levar a resultados ruins.

- pedido
- check-outs
- compras
- webVisit
- pesquisa

**Tipos de evento padrão recomendados adicionais:**

Qualquer um dos [tipos de evento restantes](#standard-events) pode ser necessário com base na complexidade de sua meta e população qualificada ao configurar a instância do Customer AI. É recomendável que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 4: Conversão de venda adicional em um site de varejo de comércio eletrônico

**Objetivo de previsão:** prevê a propensão de compra da população que comprou um produto específico para comprar um novo produto relacionado.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída de IA do cliente ideal com esse objetivo de previsão específico. É possível excluir um evento necessário dependendo do objetivo da sua previsão, no entanto, excluir vários eventos pode levar a resultados ruins.

- pedido
- check-outs
- compras
- webVisit
- pesquisa

**Tipos de evento padrão recomendados adicionais:**

Qualquer um dos [tipos de evento restantes](#standard-events) pode ser necessário com base na complexidade de sua meta e população qualificada ao configurar a instância do Customer AI. É recomendável que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 5: Cancelar a assinatura (churn) em um canal de notícias online

**Objetivo de previsão:** prevê a propensão da população qualificada para cancelar a assinatura de um serviço no próximo mês.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída de IA do cliente ideal com esse objetivo de previsão específico. É possível excluir um evento necessário dependendo do objetivo da sua previsão, no entanto, excluir vários eventos pode levar a resultados ruins.

- webVisit
- pesquisa

Além disso, para um modelo preciso, sugerimos que você use algumas das propriedades disponíveis no [subscription data type](../../xdm/data-types/subscription.md).

**Tipos de evento padrão recomendados adicionais:**

Qualquer um dos [tipos de evento restantes](#standard-events) pode ser necessário com base na complexidade de sua meta e população qualificada ao configurar a instância do Customer AI. É recomendável que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 6: Iniciar aplicativo móvel

**Objetivo de previsão:** prevê a propensão de perfis qualificados para iniciar um aplicativo móvel pago nos próximos X dias. É semelhante a prever o KPI (Indicador-chave de desempenho) dos &quot;Usuários ativos mensais&quot;.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída de IA do cliente ideal com esse objetivo de previsão específico. É possível excluir um evento necessário dependendo do objetivo da sua previsão, no entanto, excluir vários eventos pode levar a resultados ruins.

- pedido
- check-outs
- compras
- webVisit
- applicationCloses
- applicationCrashes
- applicationFeatureUsages
- applicationFirstLaunches
- applicationInstalls
- applicationLaunches
- applicationUpgrades

Neste exemplo, `order`, `checkouts` e `purchases` são usados quando um aplicativo móvel precisa ser comprado.

**Tipos de evento padrão recomendados adicionais:**

Qualquer um dos [tipos de evento restantes](#standard-events) pode ser necessário com base na complexidade de sua meta e população qualificada ao configurar a instância do Customer AI. É recomendável que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 7: Características realizadas (Adobe Audience Manager)

**Objetivo de previsão:** prevê a propensão para que algumas características sejam realizadas.

**Tipos de evento padrão obrigatórios:**

Para usar características do Adobe Audience Manager, é necessário criar uma conexão de origem usando o [Audience Manager source connector](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). O conector de origem cria automaticamente o schema com os grupos de campos adequados. Não é necessário adicionar manualmente outros tipos de evento para que o esquema funcione com o Customer AI.

Ao configurar uma nova instância do AI do cliente, `audienceName` e `audienceID` podem ser usadas para selecionar uma característica específica para pontuação ao definir sua meta.

## Dados de saída do Customer AI

O Customer AI gera vários atributos para perfis individuais considerados elegíveis. Há duas maneiras de consumir a pontuação (saída) com base no que você provisionou. Se você tiver um conjunto de dados ativado para o Perfil do cliente em tempo real, poderá consumir insights do Perfil do cliente em tempo real no [Construtor de segmentos](../../segmentation/ui/segment-builder.md). Se você não tiver um conjunto de dados habilitado para perfil, poderá [baixar o conjunto de dados do Customer AI output](./user-guide/download-scores.md) disponível no lago de dados.

>[!NOTE]
>
> Os valores de saída são consumidos pelo Perfil do cliente em tempo real, que pode ser usado para criar e definir segmentos.

A tabela abaixo descreve os vários atributos encontrados na saída do Customer AI:

| Atributo | Descrição |
| ----- | ----------- |
| Pontuação | A probabilidade relativa de um cliente atingir a meta prevista dentro do período definido. Este valor não deve ser tratado como uma percentagem de probabilidade, mas sim como a probabilidade de um indivíduo em comparação com a população global. Essa pontuação varia de 0 a 100. |
| Probabilidade | Esse atributo é a probabilidade real de um perfil para atingir a meta prevista dentro do intervalo de tempo definido. Ao comparar resultados em diferentes metas, é recomendável considerar a probabilidade sobre o percentil ou a pontuação. A probabilidade deve ser sempre usada ao determinar a probabilidade média entre a população elegível, pois a probabilidade tende a estar do lado inferior para eventos que não ocorrem com frequência. Os valores para o intervalo de probabilidade entre 0 e 1. |
| Percentil | Esse valor fornece informações sobre o desempenho de um perfil em relação a outros perfis com pontuação semelhante. Por exemplo, um perfil com uma classificação de percentil de 99 para churn indica que ele está com um risco maior de churning em comparação a 99% de todos os outros perfis que foram classificados. Os percentis variam de 1 a 100. |
| Tipo de propensão | O tipo de propensão selecionado. |
| Data da pontuação | A data em que a pontuação ocorreu. |
| Fatores influentes | Motivos previstos para a probabilidade de um perfil converter ou churn. Os fatores são compostos pelos seguintes atributos:<ul><li>Código: O perfil ou atributo comportamental que influencia positivamente a pontuação prevista de um perfil. </li><li>Valor: O valor do perfil ou do atributo comportamental.</li><li>Importância: Indica o peso do perfil ou do atributo comportamental na pontuação prevista (baixo, médio, alto)</li></ul> |

## Próximas etapas {#next-steps}

Depois de preparar seus dados e ter todas as credenciais e esquemas em vigor, comece seguindo o guia [Configurar uma instância do Customer AI](./user-guide/configure.md) . Este guia aborda a criação de uma instância para o Customer AI.
