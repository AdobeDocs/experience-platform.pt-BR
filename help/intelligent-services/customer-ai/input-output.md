---
keywords: Experience Platform;introdução;ia do cliente;tópicos populares;entrada de ia do cliente;saída de ia do cliente
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Entrada e saída na IA do cliente
description: Saiba mais sobre os eventos, entradas e saídas necessários utilizados pela IA do cliente.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '3195'
ht-degree: 2%

---

# Entrada e saída na IA do cliente

O documento a seguir descreve os diferentes eventos, entradas e saídas necessários utilizados na IA do cliente.

## Introdução

A IA do cliente funciona analisando um dos seguintes conjuntos de dados para prever pontuações de churn ou propensão de conversão:

- Dados do Adobe Analytics usando o [Conector de origem do Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Dados do Adobe Audience Manager usando o [conector de origem do Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- Conjunto de dados Evento de experiência (EE)
- Conjunto de dados do Evento de experiência do consumidor (CEE)

Você pode adicionar vários conjuntos de dados de diferentes fontes se cada um dos conjuntos de dados compartilhar o mesmo tipo de identidade (namespace), como uma ECID. Para obter mais informações sobre como adicionar vários conjuntos de dados, visite a [Guia do usuário da IA do cliente](./user-guide/configure.md#select-data)

>[!IMPORTANT]
>
>Os conectores de origem levam até quatro semanas para preencher os dados retroativamente. Se você configurou um conector recentemente, deve verificar se o conjunto de dados tem o comprimento mínimo de dados necessário para a IA do cliente. Revise o [dados históricos](#data-requirements) seção para verificar se você tem dados suficientes para sua meta de previsão.

Este documento requer uma compreensão básica do schema CEE. Revise o [Preparação de dados dos Serviços inteligentes](../data-preparation.md) antes de continuar.

A tabela a seguir descreve algumas terminologias comuns usadas neste documento:

| Termo | Definição |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | O XDM é a estrutura fundamental que permite ao Adobe Experience Cloud, viabilizado pelo Adobe Experience Platform, enviar a mensagem certa à pessoa certa, no canal certo, no momento exato. A metodologia na qual o Experience Platform é criado, o Sistema XDM, operacionaliza esquemas do Modelo de dados de experiência para uso pelos serviços da plataforma. |
| Esquema do XDM | A Experience Platform utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados. Antes que os dados possam ser assimilados na Platform, um esquema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que podem estar contidos em cada campo. Os esquemas consistem em uma classe base XDM e zero ou mais grupos de campos de esquema. |
| Classe XDM | Todos os esquemas XDM descrevem dados que podem ser categorizados como registro ou série de tempo. O comportamento dos dados de um schema é definido pela classe do schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM descrevem o menor número de propriedades que um esquema deve conter para representar um comportamento de dados específico. |
| [Grupos de campos](../../xdm/schema/composition.md) | Um componente que define um ou mais campos em um esquema. Os grupos de campos impõem como os campos aparecem na hierarquia do esquema e, portanto, exibem a mesma estrutura em cada esquema em que estão incluídos. Os grupos de campos são compatíveis apenas com classes específicas, conforme identificado por seus `meta:intendedToExtend` atributo. |
| [Tipo de dados](../../xdm/schema/composition.md) | Um componente que também pode fornecer um ou mais campos para um esquema. No entanto, diferentemente dos grupos de campos, os tipos de dados não estão restritos a uma classe específica. Isso torna os tipos de dados uma opção mais flexível para descrever estruturas de dados comuns que são reutilizáveis em vários esquemas com classes potencialmente diferentes. Os tipos de dados descritos neste documento são compatíveis com os esquemas CEE e Adobe Analytics. |
| Churn | Uma medida da porcentagem de contas que cancelam ou optam por não renovar suas assinaturas. Uma alta taxa de churn pode afetar negativamente a Receita recorrente mensal (MRR) e também pode indicar insatisfação com um produto ou serviço. |
| [Perfil do cliente em tempo real](../../profile/home.md) | O Perfil do cliente em tempo real fornece um perfil do cliente centralizado para gerenciamento de experiência direcionado e personalizado. Cada perfil contém dados agregados em todos os sistemas, bem como contas acionáveis com carimbo de data e hora de eventos envolvendo o indivíduo que ocorreram em qualquer um dos sistemas usados com o Experience Platform. |

## Dados de entrada da IA do cliente

>[!TIP]
>
> A IA do cliente determina automaticamente quais eventos são úteis para previsões e emite um aviso se os dados disponíveis não forem suficientes para gerar previsões de qualidade.

A IA do cliente é compatível com conjuntos de dados do Adobe Analytics, Adobe Audience Manager, Evento de experiência (EE) e Evento de experiência do consumidor (CEE). O esquema CEE exige a adição de grupos de campos durante o processo de criação do esquema. Se você estiver usando conjuntos de dados do Adobe Analytics ou do Adobe Audience Manager, o conector de origem mapeará diretamente os eventos padrão (Comércio, detalhes da página da Web, Aplicativo e Pesquisa) listados abaixo durante o processo de conexão. Você pode adicionar vários conjuntos de dados de diferentes fontes se cada um dos conjuntos de dados compartilhar o mesmo tipo de identidade (namespace), como uma ECID.

Para obter mais informações sobre o mapeamento de dados Adobe Analytics ou dados Audience Manager, visite o [Mapeamentos de campo do Analytics](../../sources/connectors/adobe-applications/analytics.md) ou [mapeamentos de campo Audience Manager](../../sources/connectors/adobe-applications/mapping/audience-manager.md) guia.

### Eventos padrão usados pela IA do cliente {#standard-events}

Eventos de experiência XDM são usados para determinar vários comportamentos do cliente. Dependendo de como seus dados são estruturados, os tipos de evento listados abaixo podem não abranger todos os comportamentos do cliente. Cabe a você determinar quais campos têm os dados necessários para identificar de forma clara e inequívoca a atividade do usuário da Web. Dependendo da meta de previsão, os campos obrigatórios que são necessários podem mudar.

A IA do cliente depende de diferentes tipos de evento para criar recursos de modelo. Esses tipos de evento são adicionados automaticamente ao esquema usando vários grupos de campos XDM.

>[!NOTE]
>
>Se estiver usando dados do Adobe Analytics ou Adobe Audience Manager, o esquema será criado automaticamente com os eventos padrão necessários para capturar seus dados. Se você estiver criando seu próprio esquema CEE personalizado para capturar dados, será necessário considerar quais grupos de campos são necessários para capturar seus dados.

Não é necessário ter dados para cada um dos eventos padrão listados abaixo, mas determinados eventos são necessários para determinados cenários. Se você tiver algum dos dados de eventos padrão disponíveis, é recomendável incluí-lo no esquema. Por exemplo, se você deseja criar um aplicativo da IA do cliente para prever eventos de compra, seria útil ter dados do `Commerce` e `Web page details` tipos de dados.

Para exibir um grupo de campos na interface do Platform, selecione a variável **[!UICONTROL Esquemas]** no painel esquerdo, seguido pela seleção da guia **[!UICONTROL Grupos de campos]** guia.

| Grupo de campos | Tipo de evento | Caminho do campo XDM |
| --- | --- | --- |
| [!UICONTROL Detalhes do comércio] | pedido | <li> commerce.order.purchaseID </li> <li> productListItems.SKU </li> |
|  | productListViews | <li> commerce.productListViews.value </li> <li> productListItems.SKU </li> |
|  | check-outs | <li> commerce.checkouts.value </li> <li> productListItems.SKU </li> |
|  | compras | <li> commerce.purchases.value </li> <li> productListItems.SKU </li> |
|  | productListRemovals | <li> commerce.productListRemovals.value </li> <li> productListItems.SKU </li> |
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

Além disso, a IA do cliente pode usar dados de assinatura para criar modelos de churn melhores. Os dados de subscrição são necessários para cada perfil que usa o [[!UICONTROL Inscrição]](../../xdm/data-types/subscription.md) formato do tipo de dados. A maioria dos campos é opcional. No entanto, para um modelo de churn ideal, é altamente recomendável fornecer dados para o maior número de campos possível, como `startDate`, `endDate`e quaisquer outros detalhes relevantes.

### Adicionar eventos personalizados e atributos de perfil

Se você tiver informações que deseja incluir além da variável [campos de evento padrão](#standard-events) usada pela IA do cliente, um evento personalizado e uma opção de atributo de perfil personalizado são fornecidos durante o [configuração da instância](./user-guide/configure.md#custom-events).

Se o conjunto de dados selecionado incluir eventos personalizados ou atributos de perfil, como &quot;reserva de hotel&quot; ou &quot;funcionário da empresa X&quot; definidos no esquema, você poderá adicioná-los à instância. Esses eventos personalizados adicionais e atributos de perfil são usados pela IA do cliente para melhorar a qualidade do seu modelo e fornecer resultados mais precisos.

### Dados históricos {#data-requirements}

A IA do cliente exige dados históricos para o treinamento de modelos, mas a quantidade de dados necessária se baseia em dois elementos principais: janela de resultado e população qualificada.

Por padrão, a IA do cliente procura um usuário que tenha tido atividade nos últimos 120 dias se nenhuma definição de população qualificada for fornecida durante a configuração do aplicativo. Além disso, a IA do cliente exige um mínimo de 500 eventos qualificados e 500 eventos não qualificados (total de 1000) de dados históricos com base em uma definição de meta prevista.

Os exemplos a seguir fornecidos usam uma fórmula simples para ajudar a determinar a quantidade mínima de dados necessária. Se você tiver mais do que o requisito mínimo, seu modelo provavelmente fornecerá resultados mais precisos. Se você tiver menos do que a quantidade mínima necessária, o modelo falhará, pois não há uma quantidade suficiente de dados para o treinamento do modelo.

**Fórmula**:

Comprimento mínimo dos dados necessários = população elegível + janela de resultado

>[!NOTE]
>
> 30 é o número mínimo de dias necessário para a população elegível. Se isso não for fornecido, o padrão será 120 dias.

Exemplos:

- Você deseja prever se é provável que um cliente compre um relógio nos próximos 30 dias. Você também deseja pontuar os usuários que tiveram alguma atividade da Web nos últimos 60 dias. Nesse caso, a duração mínima dos dados exigidos é de 60 dias + 30 dias. A população elegível é de 60 dias e a janela de resultado é de 30 dias, totalizando 90 dias.

- Você deseja prever se o usuário provavelmente comprará um relógio nos próximos 7 dias. Nesse caso, o período mínimo de dados necessário é = 120 dias + 7 dias. O padrão da população elegível é 120 dias e a janela de resultado é 7 dias, totalizando 127 dias.

- Você deseja prever se é provável que o cliente compre um relógio nos próximos 7 dias. Você também deseja pontuar os usuários que tiveram alguma atividade da Web nos últimos sete dias. Nesse caso, a duração mínima dos dados exigidos é de 30 dias + 7 dias. A população elegível requer um mínimo de 30 dias e a janela de resultado é de 7 dias, totalizando 37 dias.

Além dos dados mínimos necessários, a IA do cliente também funciona melhor com os dados recentes. Nesse caso de uso, a IA do cliente está fazendo uma previsão para o futuro com base nos dados comportamentais recentes de um usuário. Em outras palavras, dados mais recentes provavelmente produzirão uma previsão mais precisa.

### Exemplos de cenários

Nesta seção, diferentes cenários para instâncias da IA do cliente são descritos, bem como os tipos de evento necessários e recomendados. Consulte a [tabela de eventos padrão](#standard-events) acima para obter mais informações sobre o grupo de campos e seu caminho.

>[!NOTE]
>
> Os tipos de evento necessários são usados para identificar de forma clara e inequívoca a atividade do usuário da Web. O número de tipos de evento necessários será alterado com base na meta de previsão e na estrutura do esquema. Se não tiver certeza de que um tipo de evento específico é necessário, é recomendável incluir esse tipo de evento ao criar seu esquema CEE. Se estiver usando dados do Adobe Analytics ou Adobe Audience Manager, os eventos padrão necessários deverão estar disponíveis, dependendo dos dados que você estiver transmitindo.

### Cenário 1: conversão de compra em um site de varejo de comércio eletrônico

**Meta de previsão:** Preveja a propensão de conversão para que os perfis qualificados comprem determinado artigo de roupas em um site.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída ideal da IA do cliente com essa meta de previsão específica. É possível excluir um evento obrigatório dependendo da sua meta de previsão. No entanto, a exclusão de vários eventos pode levar a resultados ruins.

- pedido
- check-outs
- compras
- webVisit
- pesquisa

**Outros tipos de evento padrão recomendados:**

Qualquer um dos [tipos de evento](#standard-events) pode ser necessário com base na complexidade da meta e do público qualificado ao configurar a instância da IA do cliente. Recomenda-se que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 2: conversão de assinatura em um site de serviço de streaming de mídia

**Meta de previsão:** Preveja a propensão de conversão da assinatura para que os perfis qualificados se comprometam com um determinado nível de assinatura, como um plano padrão ou premium.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída ideal da IA do cliente com essa meta de previsão específica. É possível excluir um evento obrigatório dependendo da sua meta de previsão. No entanto, a exclusão de vários eventos pode levar a resultados ruins.

- pedido
- check-outs
- compras
- webVisit
- pesquisa

Neste exemplo, `order`, `checkouts`, e `purchases` são usados para indicar que uma assinatura foi adquirida e seu tipo.

Além disso, para um modelo preciso, sugere-se usar algumas das propriedades disponíveis no [tipo de dados de assinatura](../../xdm/data-types/subscription.md).

**Outros tipos de evento padrão recomendados:**

Qualquer um dos [tipos de evento](#standard-events) pode ser necessário com base na complexidade da meta e do público qualificado ao configurar a instância da IA do cliente. Recomenda-se que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 3: churn em um site de varejo de comércio eletrônico

**Meta de previsão:** Preveja a probabilidade de um evento de compra não ocorrer.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída ideal da IA do cliente com essa meta de previsão específica. É possível excluir um evento obrigatório dependendo da sua meta de previsão. No entanto, a exclusão de vários eventos pode levar a resultados ruins.

- pedido
- check-outs
- compras
- webVisit
- pesquisa

**Outros tipos de evento padrão recomendados:**

Qualquer um dos [tipos de evento](#standard-events) pode ser necessário com base na complexidade da meta e do público qualificado ao configurar a instância da IA do cliente. Recomenda-se que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 4: conversão de venda adicional em um site de varejo de comércio eletrônico

**Meta de previsão:** Preveja a propensão de compra da população que comprou um produto específico para comprar um novo produto relacionado.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída ideal da IA do cliente com essa meta de previsão específica. É possível excluir um evento obrigatório dependendo da sua meta de previsão. No entanto, a exclusão de vários eventos pode levar a resultados ruins.

- pedido
- check-outs
- compras
- webVisit
- pesquisa

**Outros tipos de evento padrão recomendados:**

Qualquer um dos [tipos de evento](#standard-events) pode ser necessário com base na complexidade da meta e do público qualificado ao configurar a instância da IA do cliente. Recomenda-se que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 5: cancelar a assinatura (churn) em uma agência de notícias online

**Meta de previsão:** Preveja a propensão da população qualificada para cancelar a assinatura de um serviço no próximo mês.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída ideal da IA do cliente com essa meta de previsão específica. É possível excluir um evento obrigatório dependendo da sua meta de previsão. No entanto, a exclusão de vários eventos pode levar a resultados ruins.

- webVisit
- pesquisa

Além disso, para um modelo preciso, sugere-se usar algumas das propriedades disponíveis no [tipo de dados de assinatura](../../xdm/data-types/subscription.md).

**Outros tipos de evento padrão recomendados:**

Qualquer um dos [tipos de evento](#standard-events) pode ser necessário com base na complexidade da meta e do público qualificado ao configurar a instância da IA do cliente. Recomenda-se que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 6: iniciar aplicativo móvel

**Meta de previsão:** Preveja a propensão dos perfis qualificados para iniciar um aplicativo para dispositivos móveis pago nos próximos X dias. É semelhante à previsão do KPI (Indicador Chave de Desempenho) de &quot;Usuários Ativos Mensais&quot;.

**Tipos de evento padrão obrigatórios:**

Os tipos de evento listados abaixo são necessários para uma saída ideal da IA do cliente com essa meta de previsão específica. É possível excluir um evento obrigatório dependendo da sua meta de previsão. No entanto, a exclusão de vários eventos pode levar a resultados ruins.

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

Neste exemplo, `order`, `checkouts`, e `purchases` são usados quando um aplicativo móvel precisa ser comprado.

**Outros tipos de evento padrão recomendados:**

Qualquer um dos [tipos de evento](#standard-events) pode ser necessário com base na complexidade da meta e do público qualificado ao configurar a instância da IA do cliente. Recomenda-se que, se os dados estiverem disponíveis para um tipo de dados específico, esses dados sejam incluídos no esquema.

### Cenário 7: características realizadas (Adobe Audience Manager)

**Meta de previsão:** Preveja a propensão para algumas características a serem realizadas.

**Tipos de evento padrão obrigatórios:**

Para usar características do Adobe Audience Manager, é necessário criar uma conexão de origem usando o [conector de origem do Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md). O conector de origem cria automaticamente o esquema com os grupos de campos adequados. Não é necessário adicionar manualmente outros tipos de evento para que o esquema funcione com a IA do cliente.

Ao configurar uma nova instância da IA do cliente, `audienceName` e `audienceID` pode ser usado para selecionar uma característica específica para pontuação ao definir sua meta.

## Dados de saída da IA do cliente

A IA do cliente gera vários atributos para perfis individuais que são considerados qualificados. Há duas maneiras de consumir a pontuação (saída) com base no que você provisionou. Se você tiver um conjunto de dados habilitado para o Perfil do cliente em tempo real, poderá consumir insights do Perfil do cliente em tempo real na [Construtor de segmentos](../../segmentation/ui/segment-builder.md). Se você não tiver um conjunto de dados habilitado para perfis, poderá [baixar a saída do Customer AI](./user-guide/download-scores.md) conjunto de dados disponível no data lake.

Você pode encontrar o conjunto de dados de saída em **Conjuntos de dados** na Platform. Todos os conjuntos de dados de saída da IA do cliente começam com o nome **Pontuações da IA do cliente - Nome_do_aplicativo**. Da mesma forma, todos os esquemas de saída da IA do cliente começam com o nome **Esquema da IA do cliente - Nome_do_aplicativo**.

![cai-schema-name-of-app](./images/user-guide/cai-schema-name-of-app.png)

>[!NOTE]
>
> Os valores de saída são consumidos pelo Perfil do cliente em tempo real, que pode ser usado para criar e definir segmentos.

A tabela abaixo descreve os vários atributos encontrados na saída da IA do cliente:

| Atributo | Descrição |
| ----- | ----------- |
| Pontuação | A probabilidade relativa de um cliente atingir a meta prevista dentro do período definido. Este valor não deve ser tratado como uma percentagem de probabilidade, mas sim como a probabilidade de um indivíduo em comparação com a população global. Essa pontuação varia de 0 a 100. |
| Probabilidade | Esse atributo é a verdadeira probabilidade de um perfil alcançar a meta prevista dentro do período definido. Ao comparar saídas entre metas diferentes, recomenda-se considerar a probabilidade sobre o percentil ou a pontuação. A probabilidade deve ser sempre usada ao determinar a probabilidade média em toda a população elegível, já que a probabilidade tende a ser menor para eventos que não ocorrem com frequência. Valores para o intervalo de probabilidade entre 0 e 1. |
| Percentil | Esse valor fornece informações sobre o desempenho de um perfil em relação a outros perfis com pontuação semelhante. Por exemplo, um perfil com classificação de percentil de 99 para churn indica que ele tem um risco maior de churn em comparação a 99% de todos os outros perfis que foram pontuados. Os percentuais variam de 1 a 100. |
| Tipo de propensão | O tipo de propensão selecionado. |
| Data da pontuação | A data em que a pontuação ocorreu. |
| Fatores influentes | Motivos previstos sobre por que um perfil tem probabilidade de conversão ou churn. Os fatores são compostos pelos seguintes atributos:<ul><li>Código: o atributo de perfil ou comportamental que influencia positivamente a pontuação prevista de um perfil. </li><li>Valor: o valor do perfil ou atributo comportamental.</li><li>Importância: indica o peso do perfil ou do atributo comportamental na pontuação prevista (baixa, média, alta)</li></ul> |

>[!NOTE]
>
> - A IA do cliente usa apenas dados atualizados para treinamento adicional e pontuação. Da mesma forma, quando você solicita a exclusão de dados, a IA do cliente evita usar os dados excluídos.
> - A IA do cliente aproveita os conjuntos de dados da plataforma. Para dar suporte às solicitações de direitos do consumidor que uma marca pode receber, as marcas devem usar o Platform Privacy Service para enviar solicitações do consumidor de acesso e exclusão para remover seus dados no data lake, no Serviço de identidade e no Perfil do cliente em tempo real.
> - Todos os conjuntos de dados que usamos para entrada/saída de modelos seguirão as diretrizes da plataforma. A Criptografia de dados da plataforma se aplica a dados inativos e em trânsito. Consulte a documentação para saber mais sobre [criptografia de dados](../../../help/landing/governance-privacy-security/encryption.md)


## Próximas etapas {#next-steps}

Depois de preparar seus dados e ter todas as credenciais e esquemas em vigor, comece seguindo a [Configurar uma instância da IA do cliente](./user-guide/configure.md) guia. Este guia aborda a criação de uma instância da IA do cliente.




