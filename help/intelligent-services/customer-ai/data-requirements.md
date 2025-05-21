---
keywords: Experience Platform;introdução;ia do cliente;tópicos populares;entrada de ia do cliente;saída de ia do cliente; requisitos de dados
solution: Experience Platform, Real-Time Customer Data Platform
feature: Customer AI
title: Requisitos de dados na IA do cliente
topic-legacy: Getting started
description: Saiba mais sobre os eventos, entradas e saídas necessários utilizados pela IA do cliente.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 73dea391f8fcb1d2d491c814b453afb4e538459d
workflow-type: tm+mt
source-wordcount: '2552'
ht-degree: 1%

---


# Entrada e saída na IA do cliente

O documento a seguir descreve os diferentes eventos, entradas e saídas necessários utilizados na IA do cliente.

## Introdução {#getting-started}

Estas são as etapas para criar modelos de propensão e identificar públicos-alvo para marketing personalizado na IA do cliente:

1. Descrever casos de uso: como os modelos de propensão ajudariam a identificar públicos-alvo para marketing personalizado? Quais são minhas metas comerciais e as táticas correspondentes para atingir a meta? Onde a modelagem de propensão pode se encaixar nesse processo?

2. Priorizar casos de uso: quais são as maiores prioridades para a empresa?

3. Criar modelos na IA do cliente: assista a este [tutorial rápido](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=pt-BR) e consulte nosso [guia da interface do usuário](../customer-ai/user-guide/configure.md) para obter um processo passo a passo para criar um modelo.

4. [Criar segmentos](../customer-ai/user-guide/create-segment.md) usando resultados de modelo.

5. Realizar ações comerciais direcionadas com base nesses segmentos. Monitore os resultados e repita as ações para melhorar.

Estes são exemplos de configurações para seu primeiro modelo.  O modelo de exemplo, criado neste documento, usa um modelo de IA do cliente para prever quem provavelmente fará a conversão para um negócio de varejo nos próximos 30 dias. O conjunto de dados de entrada é um conjunto de dados do Adobe Analytics.

| Etapa | Definição | Exemplo |
| ---- | ------ | ------- |
| Configurar | Especifique informações básicas sobre o modelo. | **Nome**: modelo de propensão de compra de lápis <br> **Tipo de Modelo**: Conversão |
| Selecionar dados | Especifique os conjuntos de dados usados para criar o modelo. | **Conjunto de dados**: conjunto de dados Adobe Analytics <br> **Identidade**: verifique se a coluna de identidade de cada conjunto de dados está definida como uma identidade comum. |
| Definir objetivo | Defina a meta, o público elegível, os eventos personalizados e os atributos do perfil. | **Meta de Previsão**: Selecionar `commerce.purchases.value` igual ao lápis <br> **Janela de resultado**: 30 dias. |
| Definir opções | Configurar a programação para atualização do modelo e ativar pontuações para o Perfil | **Agenda**: Semanalmente <br> **Habilitar para o perfil**: isso deve ser habilitado para que a saída do modelo seja usada na segmentação. |

## Visão geral dos dados {#data-overview}

As seções a seguir descrevem os diferentes eventos, entradas e saídas necessários utilizados na IA do cliente.

A IA do cliente funciona analisando os seguintes conjuntos de dados para prever as pontuações de propensão de churn (quando é provável que um cliente pare de usar o produto) ou conversão (quando é provável que um cliente faça uma compra):

- Dados do Adobe Analytics usando o [conector de origem do Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Dados do Adobe Audience Manager usando o [conector de origem do Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [Conjunto de dados de Evento de Experiência](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html?lang=pt-BR)
- [Conjunto de dados do Evento de experiência do consumidor](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html?lang=pt-BR#cee-schema)

Você pode adicionar vários conjuntos de dados de diferentes fontes se cada um dos conjuntos de dados compartilhar o mesmo tipo de identidade (namespace), como uma ECID. Para obter mais informações sobre como adicionar vários conjuntos de dados, visite o [Guia do usuário da IA do cliente](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>Os conectores do Source levam até quatro semanas para preencher os dados retroativamente. Se você configurou um conector recentemente, deve verificar se o conjunto de dados tem o comprimento mínimo de dados necessário para a IA do cliente. Revise a seção [dados históricos](#data-requirements) para verificar se você tem dados suficientes para a meta de previsão.

A tabela a seguir descreve algumas terminologias comuns usadas neste documento:

| Termo | Definição |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | O XDM é a estrutura fundamental que permite ao Adobe Experience Cloud, viabilizado pelo Adobe Experience Platform, enviar a mensagem certa à pessoa certa, no canal certo, no momento exato. O Experience Platform usa o Sistema XDM para organizar os dados de uma determinada maneira que facilita o uso dos serviços da Experience Platform. |
| [Esquema XDM](../../xdm/schema/composition.md) | A Experience Platform usa esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados. Antes que os dados possam ser assimilados na Experience Platform, um esquema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que podem estar contidos em cada campo. Os esquemas consistem em uma classe base XDM e zero ou mais grupos de campos de esquema. |
| [Classe XDM](../../xdm/schema/field-constraints.md) | Todos os esquemas XDM descrevem dados que podem ser categorizados como `Experience Event`. O comportamento dos dados de um schema é definido pela classe do schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM descrevem o menor número de propriedades que um esquema deve conter para representar um comportamento de dados específico. |
| [Grupos de campos](../../xdm/schema/composition.md) | Um componente que define um ou mais campos em um esquema. Os grupos de campos impõem como os campos aparecem na hierarquia do esquema e, portanto, exibem a mesma estrutura em cada esquema em que estão incluídos. Os grupos de campos são compatíveis apenas com classes específicas, conforme identificado pelo seu atributo `meta:intendedToExtend`. |
| [Tipo de dados](../../xdm/schema/composition.md) | Um componente que também pode fornecer um ou mais campos para um esquema. No entanto, diferentemente dos grupos de campos, os tipos de dados não estão restritos a uma classe específica. Isso torna os tipos de dados uma opção mais flexível para descrever estruturas de dados comuns que são reutilizáveis em vários esquemas com classes potencialmente diferentes. Os tipos de dados descritos neste documento são compatíveis com os esquemas CEE e Adobe Analytics. |
| [Perfil do cliente em tempo real](../../profile/home.md) | O Perfil do cliente em tempo real fornece um perfil do cliente centralizado para gerenciamento de experiência direcionado e personalizado. Cada perfil contém dados agregados em todos os sistemas, bem como contas acionáveis com carimbo de data e hora de eventos que envolvem o indivíduo que ocorreram em qualquer um dos sistemas usados com o Experience Platform. |

## Dados de entrada da IA do cliente {#customer-ai-input-data}

Para conjuntos de dados de entrada, como Adobe Analytics e Adobe Audience Manager, os respectivos conectores de origem mapeiam diretamente os eventos nesses grupos de campos padrão (Commerce, Web, Aplicativo e Pesquisa) por padrão durante o processo de conexão. A tabela abaixo mostra os campos de evento nos grupos de campos padrão para a IA do cliente.

Para obter mais informações sobre como mapear dados do Adobe Analytics ou do Audience Manager, visite o [guia de mapeamentos de campo](../../sources/connectors/adobe-applications/mapping/audience-manager.md) do Analytics ou dos mapeamentos de campo do Audience Manager.

Você pode usar esquemas XDM de Evento de experiência ou Evento de experiência do consumidor para conjuntos de dados de entrada que não são preenchidos por meio de um dos conectores acima. Grupos de campos XDM adicionais podem ser adicionados durante o processo de criação do esquema. Os grupos de campos podem ser fornecidos pela Adobe, como os grupos de campos padrão ou um grupo de campos personalizado, que corresponde à representação de dados na Experience Platform.

>[!IMPORTANT]
>
>Você deve garantir que os dados estejam sendo preenchidos nesses conjuntos de dados de entrada. Se nenhum evento de grupos de campos padrão for encontrado nos conjuntos de dados de entrada, você deverá adicionar eventos personalizados durante o fluxo de trabalho de configuração. Consulte os detalhes sobre eventos personalizados.

### Grupos de campos padrão usados pela IA do cliente {#standard-events}

Eventos de experiência são usados para determinar vários comportamentos do cliente. Dependendo de como seus dados são estruturados, os tipos de evento listados abaixo podem não abranger todos os comportamentos do cliente. Cabe a você determinar quais campos têm os dados necessários para identificar de forma clara e inequívoca a atividade da Web ou de outro usuário específico do canal. Dependendo da meta de previsão, os campos obrigatórios que são necessários podem mudar.

>[!NOTE]
>
>Se estiver usando dados do Adobe Analytics ou Adobe Audience Manager, o esquema será criado automaticamente com os eventos padrão necessários para capturar seus dados. Se você estiver criando seu próprio esquema EE personalizado para capturar dados, será necessário considerar quais grupos de campos são necessários para capturar seus dados.

A IA do cliente usa os eventos nesses quatro grupos de campos padrão por padrão: Commerce, Web, Aplicativo e Pesquisa. Não é necessário ter dados para cada evento nos grupos de campos padrão listados abaixo, mas determinados eventos são necessários para determinados cenários. Se você tiver eventos nos grupos de campos padrão disponíveis, é recomendável incluí-los no esquema. Por exemplo, se você deseja criar um modelo de IA do cliente para prever eventos de compra, é útil ter dados do Commerce e grupos de campos de detalhes da página da Web.

Para exibir um grupo de campos na interface do usuário do Experience Platform, selecione a guia **[!UICONTROL Esquemas]** no painel esquerdo, seguido pela seleção da guia **[!UICONTROL Grupos de campos]**.

| Grupo de campos | Tipo de evento | Caminho do campo XDM |
| --- | --- | --- |
| [!UICONTROL Detalhes do Commerce] | pedido | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | check-outs | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | compras | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemovals | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
|  | productListOpens | <li> `commerce.productListOpens.value` </li> <li> `productListItems.SKU` </li> |
|  | productViews | <li> `commerce.productViews.value` </li> <li> `productListItems.SKU` </li> |
| [!UICONTROL Detalhes da Web] | webVisit | `web.webPageDetails.name` |
|  | webInteraction | `web.webInteraction.linkClicks.value` |
| [!UICONTROL Detalhes do aplicativo] | applicationCloses | <li> `application.applicationCloses.value` </li> <li> `application.name` </li> |
|  | applicationCrashes | <li> `application.crashes.value` </li> <li> `application.name` </li> |
|  | applicationFeatureUsages | <li> `application.featureUsages.value` </li> <li> `application.name` </li> |
|  | applicationFirstLaunches | <li> `application.firstLaunches.value` </li> <li> `application.name` </li> |
|  | applicationInstalls | <li> application.installs.value </li> <li> `application.name` </li> |
|  | applicationLaunches | <li> application.launches.value </li> <li> `application.name` </li> |
|  | applicationUpgrades | <li> application.upgrades.value </li> <li> `application.name` </li> |
| [!UICONTROL Detalhes da Pesquisa] | pesquisar | `search.keywords` |

Além disso, a IA do cliente pode usar dados de assinatura para criar modelos de churn melhores. Os dados de assinatura são necessários para cada perfil que usa o formato de tipo de dados [[!UICONTROL Assinatura]](../../xdm/data-types/subscription.md). A maioria dos campos é opcional. No entanto, para um modelo de churn ideal, é altamente recomendável fornecer dados para o máximo de campos possível, como `startDate`, `endDate` e quaisquer outros detalhes relevantes. Entre em contato com a equipe de conta para obter suporte adicional sobre este recurso.

### Adicionar eventos personalizados e atributos de perfil {#add-custom-events}

Se você tiver informações que deseja incluir, além dos [campos de evento padrão](#standard-events) usados pela IA do cliente, poderá usar a [configuração de evento personalizado](./user-guide/configure.md#custom-events) para aumentar os dados usados pelo modelo.

#### Quando usar eventos personalizados

Os eventos personalizados são necessários quando os conjuntos de dados escolhidos na etapa de seleção do conjunto de dados contêm *nenhum* dos campos de evento padrão usados pela IA do cliente. A IA do cliente precisa de informações sobre pelo menos um evento de comportamento do usuário diferente do resultado.

Eventos personalizados são úteis para:

- Incorporar conhecimento de domínio ou experiência prévia no modelo.

- Melhorando a qualidade do modelo preditivo.

- Obter insights e interpretações adicionais.

Os melhores candidatos para eventos personalizados são dados que contêm conhecimento de domínio que pode ser preditivo do resultado. Alguns exemplos gerais de eventos personalizados incluem:

- Registrar-se na conta

- Assinar informativo

- Faça uma chamada para o atendimento ao cliente

Veja a seguir uma seleção de exemplos de eventos personalizados específicos do setor:

| Setor | Eventos personalizados |
| --- | --- |
| Varejo | Transação na loja<br>Inscreva-se no cartão do clube<br>Cupons de clipe para dispositivos móveis. |
| Entretenimento | Participação na temporada de compras <br>. Faça streaming do vídeo. |
| Hospitalidade | Fazer reserva no restaurante <br> Comprar pontos de fidelidade. |
| Viagem | Adicionar informações conhecidas do viajante Comprar milhas. |
| Comunicações | Atualizar/fazer downgrade/cancelar plano. |

Os eventos personalizados devem representar ações iniciadas pelo usuário para serem selecionados. Por exemplo, &quot;Envio de email&quot; é uma ação iniciada por um profissional de marketing e não pelo usuário, portanto, não deve ser usada como um evento personalizado.

### Dados históricos

A IA do cliente exige dados históricos para o treinamento de modelo. A duração necessária para que os dados existam no sistema é determinada por dois elementos-chave: a janela de resultado e o público elegível.

Por padrão, a IA do cliente procura um usuário que tenha tido atividade nos últimos 45 dias se nenhuma definição de população qualificada for fornecida durante a configuração do aplicativo. Além disso, a IA do cliente exige um mínimo de 500 eventos qualificados e 500 não qualificados (total de 1000) dos dados históricos com base em uma definição de meta prevista.

Os exemplos a seguir demonstram o uso de uma fórmula simples que ajuda a determinar a quantidade mínima de dados necessária. Se você tiver mais dados do que o requisito mínimo, seu modelo provavelmente fornecerá resultados mais precisos. Se você tiver menos do que o valor mínimo necessário, o modelo falhará, pois não há dados suficientes para o treinamento do modelo.

A IA do cliente emprega um modelo de sobrevivência para estimar a probabilidade de um evento ocorrer em um determinado momento e identificar fatores influenciadores, ao lado do aprendizado supervisionado que define populações positivas e negativas, e árvores baseadas em decisão como `lightgbm` para gerar uma pontuação de probabilidade.

**Fórmula**:

Para decidir a duração mínima necessária dos dados existentes no sistema:

- Os dados mínimos necessários para criar recursos são de 30 dias. Comparar a janela de retrospectiva de elegibilidade com 30 dias:

   - Se a janela de retrospectiva de elegibilidade for maior que 30 dias, a exigência de dados = janela de retrospectiva de elegibilidade + janela de resultado.

   - Caso contrário, o requisito de dados = 30 dias + janela de resultado.

** Se houver mais de uma condição para definir a população elegível, a janela de pesquisa de elegibilidade será a mais longa.

>[!NOTE]
>
>30 é o número mínimo de dias necessário para a população elegível. Se isso não for fornecido, o padrão será 45 dias.

**Exemplos**:

- Você deseja prever se um cliente provavelmente comprará um relógio nos próximos 30 dias para aqueles que tiverem alguma atividade na Web nos últimos 60 dias.

   - Janela de pesquisa de elegibilidade = 60 dias

   - Janela de resultados = 30 dias

   - Dados necessários = 60 dias + 30 dias = 90 dias

- Você deseja prever se o usuário provavelmente comprará um relógio nos próximos 7 dias **sem** fornecendo uma população qualificada explícita. Nesse caso, a população elegível assume como padrão &quot;aqueles que tiveram atividade nos últimos 45 dias&quot; e a janela de resultado é de 7 dias.

   - Janela de pesquisa de elegibilidade = 45 dias

   - Janela de resultados = 7 dias

   - Dados necessários = 45 dias + 7 dias = 52 dias

- Você deseja prever se o cliente provavelmente comprará um relógio nos próximos 7 dias para aqueles que tiverem alguma atividade na Web nos últimos 7 dias.

   - Janela de pesquisa de elegibilidade = 7 dias

   - Dados mínimos necessários para criar recursos = 30 dias

   - Janela de resultados = 7 dias

   - Dados necessários = 30 dias + 7 dias = 37 dias

Embora a IA do cliente exija um período mínimo para que os dados existam no sistema, ela também funciona melhor com os dados recentes. Ao usar dados comportamentais mais recentes, a IA do cliente provavelmente produzirá uma previsão mais precisa do comportamento futuro de um usuário.

## Dados de saída da IA do cliente {#customer-ai-output-data}

A IA do cliente gera vários atributos para perfis individuais que são considerados qualificados. Há duas maneiras de consumir a pontuação (saída) com base no que você provisionou. Se você tiver um conjunto de dados habilitado para o Perfil do cliente em tempo real, poderá consumir insights do Perfil do cliente em tempo real no [Construtor de segmentos](../../segmentation/ui/segment-builder.md). Se você não tiver um conjunto de dados habilitado para perfil, poderá [baixar o conjunto de dados de saída da IA do cliente](./user-guide/download-scores.md) disponível no data lake.

Você pode encontrar o conjunto de dados de saída no espaço de trabalho **Conjuntos de dados** do Experience Platform. Todos os conjuntos de dados de saída do Customer AI começam com o nome **Pontuações do Customer AI - NAME_OF_APP**. Da mesma forma, todos os esquemas de saída do Customer AI começam com o nome **Esquema do Customer AI - Nome_do_aplicativo**.

![A convenção de nomenclatura para conjuntos de dados de saída na IA do cliente.](./images/user-guide/cai-schema-name-of-app.png)

A tabela abaixo descreve os vários atributos encontrados na saída da IA do cliente:

| Atributo | Descrição |
| ----- | ----------- |
| [!UICONTROL Pontuação] | A probabilidade relativa de um cliente atingir a meta prevista dentro do período definido. Este valor não deve ser tratado como uma percentagem de probabilidade, mas sim como a probabilidade de um indivíduo em comparação com a população global. Essa pontuação varia de 0 a 100. |
| Probabilidade | Esse atributo é a verdadeira probabilidade de um perfil alcançar a meta prevista dentro do período definido. Ao comparar saídas entre metas diferentes, é recomendável considerar a probabilidade sobre o percentil ou a pontuação. A probabilidade deve ser sempre usada ao determinar a probabilidade média em toda a população elegível, já que a probabilidade tende a ser menor para eventos que não ocorrem com frequência. Valores para o intervalo de probabilidade entre 0 e 1. |
| Percentil | Esse valor fornece informações sobre o desempenho de um perfil em relação a outros perfis com pontuação semelhante. Por exemplo, um perfil com classificação de percentil de 99 para churn indica que ele tem um risco maior de churn em comparação a 99% de todos os outros perfis que foram pontuados. Os percentuais variam de 1 a 100. |
| Tipo de propensão | O tipo de propensão selecionado. |
| Data da pontuação | A data em que a pontuação ocorreu. |
| Fatores influentes | Esses são os motivos previstos para a probabilidade de conversão ou churn de um perfil. Esses fatores são compostos pelos seguintes atributos:<ul><li>Código: o atributo de perfil ou comportamental que influencia positivamente a pontuação prevista de um perfil. </li><li>Valor: o valor do perfil ou atributo comportamental.</li><li>Importância: indica o peso do perfil ou do atributo comportamental na pontuação prevista (baixa, média, alta)</li></ul> |

## Próximas etapas {#next-steps}

Depois de preparar seus dados e garantir que todas as credenciais e esquemas estejam em vigor, consulte o guia [Configurar uma instância da IA do cliente](./user-guide/configure.md), que orienta você por um tutorial passo a passo para criar uma instância da IA do cliente.