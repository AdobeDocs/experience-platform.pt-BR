---
keywords: Experience Platform, introdução, atendimento ao cliente, tópicos populares, entrada de atendimento ao cliente, saída de atendimento ao cliente; requisitos em matéria de dados
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Requisitos de dados no Customer AI
topic-legacy: Getting started
description: Saiba mais sobre os eventos, entradas e saídas necessários utilizados pela API do cliente.
exl-id: 9b21a89c-bf48-4c45-9eb3-ace38368481d
source-git-commit: 5f7b602b68f5cbf4b1f4b08603757b0956e36408
workflow-type: tm+mt
source-wordcount: '2484'
ht-degree: 2%

---


# Entrada e saída no Customer AI

O documento a seguir descreve os diferentes eventos, entradas e saídas necessários utilizados na API do cliente.

## Introdução {#getting-started}

Estas são as etapas para criar modelos de propensão e identificar públicos-alvo para marketing personalizado no Customer AI:

1. Casos de uso da estrutura de tópicos: Como os modelos de propensão ajudariam a identificar públicos-alvo para marketing personalizado? Quais são meus objetivos de negócios e as táticas correspondentes para atingir o objetivo? Onde a modelagem de propensão pode se encaixar nesse processo?

2. Priorizar casos de uso: Quais são as prioridades mais altas para o negócio?

3. Criar modelos no Customer AI: Veja isto [tutorial rápido](https://experienceleague.adobe.com/docs/platform-learn/tutorials/intelligent-services/configure-customer-ai.html?lang=pt-BR) e consulte nossa [Guia da interface do usuário](../customer-ai/user-guide/configure.md) para um processo passo a passo para criar um modelo.

4. [Construir segmentos](../customer-ai/user-guide/create-segment.md) usando resultados do modelo.

5. Realize ações comerciais direcionadas com base nesses segmentos. Monitore os resultados e repita as ações para melhorar.

Veja exemplos de configurações para o seu primeiro modelo.  O modelo de exemplo, criado neste documento, usa um modelo de API do cliente para prever quem provavelmente fará a conversão em um negócio de varejo nos próximos 30 dias. O conjunto de dados de entrada é um conjunto de dados Adobe Analytics.

| Etapa | Definição | Exemplo |
| ---- | ------ | ------- |
| Configurar | Especifique informações básicas sobre o modelo. | **Nome**: Modelo de propensão de compra de lápis <br> **Tipo de modelo**: Conversão |
| Selecionar dados | Especifique os conjuntos de dados usados para criar o modelo. | **Conjunto de dados**: Conjunto de dados Adobe Analytics <br> **Identidade**: Verifique se a coluna de identidade de cada conjunto de dados está definida como uma identidade comum. |
| Definir meta | Defina a meta, a população qualificada, os eventos personalizados e os atributos do perfil. | **Objetivo de previsão**: Selecionar `commerce.purchases.value` é igual a lápis <br> **Janela de resultados**: 30 dias. |
| Definir opções | Configurar o agendamento para atualização do modelo e ativar pontuações para o Perfil | **Agendar**: Semanalmente <br> **Ativar para perfil**: Isso deve ser ativado para que a saída do modelo seja usada na segmentação. |

## Visão geral dos dados {#data-overview}

As seções a seguir descrevem os diferentes eventos, entradas e saídas necessários utilizados na API do cliente.

O Customer AI funciona analisando os seguintes conjuntos de dados para prever o abandono (quando um cliente provavelmente deixará de usar o produto) ou a conversão (quando um cliente provavelmente fará uma compra) das pontuações de propensão:

- Dados do Adobe Analytics usando o [Conector de origem do Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md)
- Dados do Adobe Audience Manager usando o [Conector de fonte Audience Manager](../../sources/tutorials/ui/create/adobe-applications/audience-manager.md)
- [Conjunto de dados de eventos de experiência](https://experienceleague.adobe.com/docs/experience-platform/xdm/classes/experienceevent.html)
- [Conjunto de dados Evento de experiência do consumidor](https://experienceleague.adobe.com/docs/experience-platform/intelligent-services/data-preparation.html#cee-schema)

É possível adicionar vários conjuntos de dados de fontes diferentes se cada um dos conjuntos de dados compartilhar o mesmo tipo de identidade (namespace), como uma ECID. Para obter mais informações sobre como adicionar vários conjuntos de dados, visite o [Guia do usuário de IA do cliente](../customer-ai/user-guide/configure.md).

>[!IMPORTANT]
>
>Os conectores de origem levam até quatro semanas para preencher dados. Se você tiver configurado um conector recentemente, verifique se o conjunto de dados tem o comprimento mínimo de dados necessário para a API do cliente. Revise o [dados históricos](#data-requirements) para verificar se você tem dados suficientes para sua meta de previsão.

A tabela a seguir descreve algumas terminologias comuns usadas neste documento:

| Termo | Definição |
| --- | --- |
| [Experience Data Model (XDM)](../../xdm/home.md) | O XDM é a estrutura fundamental que permite ao Adobe Experience Cloud, desenvolvido pela Adobe Experience Platform, enviar a mensagem certa para a pessoa certa, no canal certo, no momento certo. A Platform usa o Sistema XDM para organizar os dados de uma certa maneira que facilita o uso pelos serviços da plataforma. |
| [Esquema do XDM](../../xdm/schema/composition.md) | A Experience Platform utiliza esquemas para descrever a estrutura dos dados de forma consistente e reutilizável. Ao definir os dados de forma consistente em todos os sistemas, fica mais fácil manter o significado e, portanto, obter valor dos dados. Para que os dados possam ser assimilados na Platform, um schema deve ser composto para descrever a estrutura dos dados e fornecer restrições ao tipo de dados que pode ser contido em cada campo. Os esquemas consistem em uma classe base XDM e zero ou mais grupos de campos de esquema. |
| [Classe XDM](../../xdm/schema/field-constraints.md) | Todos os esquemas XDM descrevem dados que podem ser categorizados como `Experience Event`. O comportamento de dados de um schema é definido pela classe do schema, que é atribuída a um schema quando ele é criado pela primeira vez. As classes XDM descrevem o menor número de propriedades que um schema deve conter para representar um comportamento de dados específico. |
| [Grupos de campos](../../xdm/schema/composition.md) | Um componente que define um ou mais campos em um schema. Os grupos de campos impõem como seus campos aparecem na hierarquia do esquema e, portanto, exibem a mesma estrutura em cada esquema em que estão incluídos. Os grupos de campos são compatíveis apenas com classes específicas, conforme identificado por seus `meta:intendedToExtend` atributo. |
| [Tipo de dados](../../xdm/schema/composition.md) | Um componente que também pode fornecer um ou mais campos para um schema. No entanto, ao contrário de grupos de campos, os tipos de dados não estão restritos a uma classe específica. Isso torna os tipos de dados uma opção mais flexível para descrever estruturas de dados comuns que são reutilizáveis em vários esquemas com classes potencialmente diferentes. Os tipos de dados descritos neste documento são compatíveis com os esquemas CEE e Adobe Analytics. |
| [Perfil do cliente em tempo real](../../profile/home.md) | O Perfil do cliente em tempo real oferece um perfil de consumidor centralizado para gerenciamento de experiência direcionado e personalizado. Cada perfil contém dados agregados em todos os sistemas, bem como contas acionáveis com carimbos de data e hora de eventos que envolvem o indivíduo e que ocorreram em qualquer um dos sistemas usados com o Experience Platform. |

## Dados de entrada do Customer AI {#customer-ai-input-data}

Para conjuntos de dados de entrada, como Adobe Analytics e Adobe Audience Manager, os respectivos conectores de origem mapeiam diretamente os eventos nesses grupos de campos padrão (Comércio, Web, Aplicativo e Pesquisa) por padrão durante o processo de conexão. A tabela abaixo mostra os campos de evento nos grupos de campos padrão padrão para o Customer AI.

Para obter mais informações sobre o mapeamento de dados do Adobe Analytics ou do Audience Manager, visite os mapeamentos de campo ou o Audience Manager do Analytics [guia de mapeamentos de campo](../../sources/connectors/adobe-applications/mapping/audience-manager.md).

Você pode usar esquemas XDM de Evento de experiência ou Evento de experiência do consumidor para conjuntos de dados de entrada que não são preenchidos por meio de um dos conectores acima. Grupos de campos XDM adicionais podem ser adicionados durante o processo de criação do schema. Os grupos de campos podem ser fornecidos por Adobe, como os grupos de campos padrão ou um grupo de campos personalizado, que corresponde à representação de dados na Plataforma.

>[!IMPORTANT]
>
>Você deve garantir que os dados estejam sendo preenchidos nesses conjuntos de dados de entrada. Se nenhum evento de grupos de campos padrão for encontrado nos conjuntos de dados de entrada, será necessário adicionar eventos personalizados durante o fluxo de trabalho de configuração. Veja detalhes sobre eventos personalizados.

### Grupos de campos padrão usados pelo Customer AI {#standard-events}

Os Eventos de experiência são usados para determinar vários comportamentos do cliente. Dependendo de como seus dados são estruturados, os tipos de evento listados abaixo podem não abranger todos os comportamentos do cliente. Cabe a você determinar quais campos têm os dados necessários para identificar a atividade da Web ou outra atividade do usuário específica do canal de forma clara e inequívoca. Dependendo da meta de previsão, os campos necessários podem ser alterados.

>[!NOTE]
>
>Se você estiver usando dados do Adobe Analytics ou Adobe Audience Manager, o esquema será criado automaticamente com os eventos padrão necessários para capturar seus dados. Se você estiver criando seu próprio esquema EE personalizado para capturar dados, precisará considerar quais grupos de campos são necessários para capturar seus dados.

O Customer AI usa os eventos nesses quatro grupos de campos padrão por padrão: Comércio, Web, Aplicativo e Pesquisa. Não é necessário ter dados para cada evento nos grupos de campos padrão listados abaixo, mas determinados eventos são necessários para determinados cenários. Se você tiver eventos nos grupos de campos padrão disponíveis, é recomendável incluí-los no esquema . Por exemplo, se você quiser criar um modelo de API do cliente para prever eventos de compra, é útil ter dados dos grupos de campos Detalhes da página da Web e do Comércio .

Para exibir um grupo de campos na interface do usuário da plataforma, selecione o **[!UICONTROL Esquemas]** no painel à esquerda, em seguida, selecione o **[!UICONTROL Grupos de campos]** guia .

| Grupo de campos | Tipo de evento | Caminho do campo XDM |
| --- | --- | --- |
| [!UICONTROL Detalhes de comércio] | pedido | <li> `commerce.order.purchaseID` </li> <li> `productListItems.SKU` </li> |
|  | productListViews | <li> `commerce.productListViews.value` </li> <li> `productListItems.SKU` </li> |
|  | check-outs | <li> `commerce.checkouts.value` </li> <li> `productListItems.SKU` </li> |
|  | compras | <li> `commerce.purchases.value` </li> <li> `productListItems.SKU` </li> |
|  | productListRemoments | <li> `commerce.productListRemovals.value` </li> <li> `productListItems.SKU` </li> |
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
| [!UICONTROL Detalhes da pesquisa] | pesquisa | `search.keywords` |

Além disso, o Customer AI pode usar os dados de assinatura para criar melhores modelos de rotatividade. Os dados de assinatura são necessários para cada perfil usando o [[!UICONTROL Assinatura]](../../xdm/data-types/subscription.md) formato do tipo de dados. A maioria dos campos é opcional, no entanto, para um modelo de rotatividade ideal, é altamente recomendável fornecer dados para o maior número possível de campos, como `startDate`, `endDate`e quaisquer outros elementos pertinentes. Entre em contato com a equipe de conta para obter suporte adicional sobre esse recurso.

### Adicionar eventos personalizados e atributos de perfil {#add-custom-events}

Se você tiver informações que deseja incluir além do padrão [campos de evento padrão](#standard-events) usado pelo Customer AI, você pode usar o [configuração de evento personalizado](./user-guide/configure.md#custom-events) para aumentar os dados usados pelo modelo.

#### Quando usar eventos personalizados

Os eventos personalizados são necessários quando os conjuntos de dados escolhidos na etapa de seleção do conjunto de dados contêm *nenhum* dos campos de evento padrão usados pelo Customer AI. O Customer AI precisa de informações sobre pelo menos um evento de comportamento de usuário diferente do resultado.

Os eventos personalizados são úteis para:

- Incorporação de conhecimento de domínio ou experiência prévia ao modelo.

- Melhorar a qualidade do modelo preditivo.

- Obter insights e interpretações adicionais.

Os melhores candidatos para eventos personalizados são dados que contêm conhecimento de domínio que podem ser preditivos do resultado. Alguns exemplos gerais de eventos personalizados incluem:

- Registrar por conta

- Assinar informativo

- Efetuar uma chamada para o serviço de atendimento ao cliente

Veja a seguir uma seleção de exemplos de eventos personalizados específicos do setor:

| Setor | Eventos personalizados |
| --- | --- |
| Varejo | Transação na loja<br>Inscreva-se no cartão do clube<br>Recorte o cupom móvel. |
| Entretenimento | Associação da temporada de compras <br> Vídeo de fluxo. |
| Hospitalidade | Fazer reserva de restaurante <br> Pontos de fidelidade de compra. |
| Viagens | Adicione informações conhecidas do viajante: milhas de compra. |
| Comunicações | Atualizar/fazer downgrade/cancelar plano. |

Os eventos personalizados devem representar ações iniciadas pelo usuário para serem selecionados. Por exemplo, &quot;Enviar email&quot; é uma ação iniciada por um profissional de marketing e não pelo usuário, portanto, não deve ser usada como um evento personalizado.

### Dados históricos

O Customer AI exige dados históricos para o treinamento do modelo. A duração necessária para que os dados existam no sistema é determinada por dois elementos-chave: a janela de resultados e a população elegível.

Por padrão, o Customer AI procura que um usuário tenha tido atividade nos últimos 45 dias se nenhuma definição de população qualificada for fornecida durante a configuração do aplicativo. Além disso, a API do cliente exige um mínimo de 500 eventos qualificados e 500 eventos não qualificados (total de 1000) dos dados históricos com base em uma definição de meta prevista.

Os exemplos a seguir demonstram o uso de uma fórmula simples que ajuda a determinar a quantidade mínima de dados necessária. Se você tiver mais dados do que o requisito mínimo, seu modelo provavelmente fornecerá resultados mais precisos. Se você tiver menos do que o mínimo necessário, o modelo falhará, pois não há dados suficientes para o treinamento do modelo.

**Fórmula**:

Para decidir a duração mínima exigida dos dados existentes no sistema:

- Os dados mínimos necessários para criar recursos são 30 dias. Compare a janela de retrospectiva de qualificação com 30 dias:

   - Se a janela de lookback de qualificação for superior a 30 dias, o requisito de dados = janela de lookback de qualificação + janela de resultado.

   - Caso contrário, o requisito de dados = 30 dias + janela de resultado.

** Se houver mais de uma condição para definir a população elegível, a janela de retrospectiva de elegibilidade será a mais longa.

>[!NOTE]
>
>30 é o número mínimo de dias necessário para a população elegível. Se isso não for fornecido, o padrão será 45 dias.

**Exemplos**:

- Você deseja prever se um cliente provavelmente comprará um relógio nos próximos 30 dias para aqueles que têm alguma atividade da Web nos últimos 60 dias.

   - Janela de retrospectiva de elegibilidade = 60 dias

   - Janela de saída = 30 dias

   - Dados necessários = 60 dias + 30 dias = 90 dias

- Você deseja prever se o usuário provavelmente comprará um relógio nos próximos 7 dias **without** proporcionar uma população elegível explícita. Nesse caso, o padrão da população elegível é &quot;aqueles que tiveram atividade nos últimos 45 dias&quot; e a janela de resultado é 7 dias.

   - Janela de retrospectiva de elegibilidade = 45 dias

   - Janela de saída = 7 dias

   - Dados necessários = 45 dias + 7 dias = 52 dias

- Você deseja prever se o cliente provavelmente comprará um relógio nos próximos 7 dias para aqueles que têm alguma atividade da Web nos últimos 7 dias.

   - Janela de retrospectiva de elegibilidade = 7 dias

   - Dados mínimos necessários para criar recursos = 30 dias

   - Janela de saída = 7 dias

   - Dados necessários = 30 dias + 7 dias = 37 dias

Embora a API do cliente exija um período mínimo para que os dados existam no sistema, ela também funciona melhor com os dados recentes. Ao usar dados comportamentais mais recentes, a API do cliente provavelmente produzirá uma previsão mais precisa do comportamento futuro de um usuário.

## Dados de saída do Customer AI {#customer-ai-output-data}

O Customer AI gera vários atributos para perfis individuais considerados elegíveis. Há duas maneiras de consumir a pontuação (saída) com base no que você provisionou. Se você tiver um conjunto de dados habilitado para o Perfil do cliente em tempo real, poderá consumir insights do Perfil do cliente em tempo real na [Construtor de segmentos](../../segmentation/ui/segment-builder.md). Se você não tiver um conjunto de dados habilitado para perfil, poderá [faça o download da saída do Customer AI](./user-guide/download-scores.md) conjunto de dados disponível no lago de dados.

Você pode encontrar o conjunto de dados de saída na Plataforma **Conjuntos de dados** espaço de trabalho. Todos os conjuntos de dados de saída do Customer AI começam com o nome **Pontuações do Customer AI - NAME_OF_APP**. Da mesma forma, todos os esquemas de saída do Customer AI começam com o nome **Esquema do Customer AI - Nome_do_aplicativo**.

![Nome dos conjuntos de dados de saída no Customer AI](./images/user-guide/cai-schema-name-of-app.png)

A tabela abaixo descreve os vários atributos encontrados na saída do Customer AI:

| Atributo | Descrição |
| ----- | ----------- |
| [!UICONTROL Pontuação] | A probabilidade relativa de um cliente atingir a meta prevista dentro do período definido. Este valor não deve ser tratado como uma percentagem de probabilidade, mas sim como a probabilidade de um indivíduo em comparação com a população global. Essa pontuação varia de 0 a 100. |
| Probabilidade | Esse atributo é a probabilidade real de um perfil para atingir a meta prevista dentro do intervalo de tempo definido. Ao comparar resultados em diferentes metas, é recomendável considerar a probabilidade sobre o percentil ou a pontuação. A probabilidade deve ser sempre usada ao determinar a probabilidade média entre a população elegível, pois a probabilidade tende a estar do lado inferior para eventos que não ocorrem com frequência. Valores para o intervalo de probabilidade entre 0 e 1. |
| Percentil | Esse valor fornece informações sobre o desempenho de um perfil em relação a outros perfis com pontuação semelhante. Por exemplo, um perfil com uma classificação de percentil de 99 para churn indica que ele está com um risco maior de churning em comparação a 99% de todos os outros perfis que foram classificados. Os percentis variam de 1 a 100. |
| Tipo de propensão | O tipo de propensão selecionado. |
| Data da pontuação | A data em que a pontuação ocorreu. |
| Fatores influentes | Esses são motivos preditivos para a probabilidade de um perfil converter ou churn. Esses fatores são compostos pelos seguintes atributos:<ul><li>Código: O perfil ou atributo comportamental que influencia positivamente a pontuação prevista de um perfil. </li><li>Valor: O valor do perfil ou do atributo comportamental.</li><li>Importância: Indica o peso do perfil ou do atributo comportamental na pontuação prevista (baixo, médio, alto)</li></ul> |

## Próximas etapas {#next-steps}

Depois de preparar os dados e garantir que todas as credenciais e esquemas estejam em vigor, consulte a [Configurar uma instância do Customer AI](./user-guide/configure.md) guia , que aborda um tutorial passo a passo para criar uma instância do Customer AI.