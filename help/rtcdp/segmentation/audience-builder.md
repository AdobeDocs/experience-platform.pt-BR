---
title: Construtor de público-alvo no Real-Time Customer Data Platform
description: Saiba como usar o Construtor de público-alvo no Real-Time Customer Data Platform para criar públicos-alvo.
feature: Get Started, Audiences
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=pt-BR#rtcdp-editions" newtab=true
exl-id: da87baad-b82a-4a45-89c3-cf20d66fe657
source-git-commit: 809f80c721d6eedf5ee88dbb1cf4bf7e5a413614
workflow-type: tm+mt
source-wordcount: '1079'
ht-degree: 7%

---

# Construtor de público-alvo no Real-Time Customer Data Platform

Criado com base no Adobe Experience Platform, o [!DNL Adobe Real-Time Customer Data Platform] pode usar todos os recursos do Audience Builder que fazem parte do [!DNL Experience Platform]. O espaço de trabalho fornece controles intuitivos para criar e editar regras, como arrastar e soltar blocos usados para representar propriedades de dados.

![O Construtor de público-alvo na seção Contas.](../assets/segmentation/audience-builder/audience-builder.png){zoomable="yes"}

## Campos {#fields}

>[!CONTEXTUALHELP]
>id="platform_b2b_audiencebuilder_showfullxdmschema"
>title="Mostrar esquema XDM completo"
>abstract="Por padrão, somente os campos que contêm dados são exibidos. Habilite essa opção para mostrar todos os campos no esquema XDM."

>[!CONTEXTUALHELP]
>id="platform_b2b_audiencebuilder_showrelationselectors"
>title="Mostrar seletores de relação"
>abstract="Por padrão, são usadas as relações padrão de sua organização. Habilite esta opção para mostrar os seletores de relação usados."

>[!CONTEXTUALHELP]
>id="platform_b2b_audiencebuilder_showconstrainedfields"
>title="Mostrar campos restritos"
>abstract="Por padrão, somente os campos que não têm restrições são exibidos. Habilite esta opção para mostrar os campos que possuem restrições."

Ao usar o Construtor de público-alvo para contas, você pode usar atributos de conta ou públicos-alvo existentes como campos do público-alvo.

Você pode selecionar o ![ícone de configurações](../../images/icons/settings.png) para ajustar as configurações dos campos exibidos.

![Os ícones de configurações estão realçados no Audience Builder.](../assets/segmentation/audience-builder/select-settings.png){zoomable="yes"}

A seção [!UICONTROL Settings] é exibida. Nesta seção, você pode atualizar quais campos são exibidos, bem como a relação dos campos.

Para **[!UICONTROL Field options]**, você pode mostrar apenas os campos que contêm dados ou o esquema XDM completo.

Para o **[!UICONTROL Relationship of fields]**, você pode usar as relações padrão para sua organização ou mostrar os seletores de relação.

![O módulo de configurações é exibido.](../assets/segmentation/audience-builder/settings.png){width="300"}

### Atributos {#attributes}

A guia [!UICONTROL Attributes] permite procurar atributos de Conta pertencentes à classe Conta Comercial XDM, bem como atributos baseados em oportunidades e pessoas. Cada pasta pode ser expandida para revelar atributos adicionais, onde cada atributo é um bloco que pode ser arrastado para a [tela do construtor de regras](#rule-builder-canvas) no centro do espaço de trabalho.

![A guia Atributos é exibida no Audience Builder](../assets/segmentation/audience-builder/attributes.png)

Ao selecionar um atributo, você pode ver dados de resumo selecionando o [ícone de informações](../../images/icons/info.png). Os dados de resumo incluem informações como valores principais, uma explicação do que é o campo, a contagem de registro dos valores, bem como a porcentagem de contas que contêm valores para esse atributo.

A seção **[!UICONTROL Populated]** mostra o número de registros em que o atributo é preenchido em comparação ao número total de registros disponíveis, bem como a porcentagem de contas que têm um valor para esse campo.

A seção **[!UICONTROL Top values]** exibe os valores que ocorrem com mais frequência para o atributo e inclui detalhes como o valor, o número de registros que têm o valor, bem como a porcentagem do total de registros que o valor representa.

![Um popover que exibe uma versão totalmente preenchida dos dados de resumo de um atributo.](../assets/segmentation/audience-builder/full-summary-data.png){width="300"}

Como alternativa, você pode ver a distribuição de seus dados com os valores mínimo, médio e máximo exibidos.

![Um popover que exibe as estatísticas de um atributo, incluindo os valores mínimo, médio e máximo.](../assets/segmentation/audience-builder/statistics.png){width="300"}

Se um atributo for preenchido por menos de 25% das contas, o ![ícone de aviso de dados](../../images/icons/data-notice.png) será exibido. Os mesmos dados de resumo serão exibidos para o atributo, independentemente.

![Um popover que exibe uma versão dos dados de resumo de um atributo quando ele é preenchido por menos de 25% das contas.](../assets/segmentation/audience-builder/empty-summary-data.png){width="300"}

>[!NOTE]
>
>Os dados de resumo só estarão disponíveis se o atributo pertencer ao esquema Conta, Pessoa ou Oportunidade. Além disso, os valores principais serão exibidos somente se o campo **não** contiver muitos valores diferentes e se esses valores forem repetidos com frequência.
>
>Estes dados de resumo são atualizados **diariamente**.

Além disso, o atributo tem um **[!UICONTROL Ingestion Type]**. O tipo de assimilação permite saber a origem dos dados e pode ser um dos seguintes valores: **[!UICONTROL Batch]**, **[!UICONTROL Streaming/Edge]** ou **[!UICONTROL No Data Ingested]**.

![O tipo de assimilação do atributo é exibido.](/help/rtcdp/assets/segmentation/audience-builder/ingestion-type.png){width="300"}

Para obter um guia mais detalhado sobre os atributos no Audience Builder, leia o [guia do usuário do Audience Builder](../../segmentation/ui/segment-builder.md){target="_blank"}.

### Públicos-alvo {#audiences}

A guia **[!UICONTROL Audiences]** lista todos os públicos com base em pessoas e em contas disponíveis no Experience Platform.

Você pode passar o mouse sobre o ![ícone de informações](../../images/icons/info.png) ao lado de um público-alvo para ver informações sobre ele, incluindo sua ID, descrição e a hierarquia de pastas para localizá-lo.

![As informações sobre o público são exibidas.](../assets/segmentation/audience-builder/audience-information.png){zoomable="yes"}

## Tela do construtor de regras {#rule-builder-canvas}

Um público-alvo criado no Audience Builder é uma coleção de regras usadas para descrever as principais características ou comportamentos de um público-alvo. Essas regras são criadas usando a tela do construtor de regras, localizada no centro do Audience Builder.

Para adicionar uma nova regra à definição de segmento, arraste um bloco da guia **[!UICONTROL Fields]** e solte-o na tela do construtor de regras.

![A tela do construtor de regras com um campo adicionado.](../assets/segmentation/audience-builder/added-field.png){zoomable="yes"}

Para obter mais informações sobre como usar a tela do construtor de regras, leia a [documentação sobre o Construtor de segmentos](../../segmentation/ui/segment-builder.md#rule-builder-canvas){target="_blank"}.

### Containers {#containers}

As regras de público são avaliadas na ordem em que são listadas. Você pode usar containers para permitir maior controle sobre a ordem de execução por meio do uso de consultas aninhadas.

Para obter mais informações sobre contêineres, leia a [documentação sobre o Construtor de segmentos](../../segmentation/ui/segment-builder.md#containers){target="_blank"}.

## Propriedades de público-alvo {#properties}

A seção **[!UICONTROL Audience properties]** exibe informações sobre o público incluindo o tamanho estimado do público. Você também pode especificar detalhes sobre o público-alvo, incluindo nome, descrição e tags.

![A seção de propriedades do público-alvo é exibida para o público-alvo no Audience Builder.](../assets/segmentation/audience-builder/audience-properties.png){width="300"}

O **[!UICONTROL Qualified accounts]** indica o número real de contas que correspondem às regras do público-alvo. Esse número é atualizado a cada 24 horas, após a execução do trabalho de segmentação.

O **[!UICONTROL Estimated accounts]** indica o número aproximado de contas com base no trabalho de amostra. Você pode atualizar este valor depois de adicionar novas regras ou condições e selecionar **[!UICONTROL Refresh estimate]**.

![A seção de estimativas na seção de propriedades do público-alvo é exibida.](../assets/segmentation/audience-builder/account-estimates.png){width="300"}

Você pode selecionar **[!UICONTROL View accounts]** para ver uma amostra das contas que se qualificariam para o público-alvo com as regras atuais.

![O botão Exibir contas está realçado.](../assets/segmentation/audience-builder/view-accounts.png){width="300"}

O **[!UICONTROL Code view]** fornece uma descrição baseada em texto das regras do público-alvo.

![A versão de exibição de código do público-alvo da conta.](../assets/segmentation/audience-builder/code-view.png)

Você pode selecionar **[!UICONTROL Apply access labels]** para aplicar os rótulos de acesso relevantes ao público. Mais informações sobre rótulos de acesso podem ser encontradas no [guia de gerenciamento de rótulos](../../access-control/abac/ui/labels.md){target="_blank"}.

![O popover Aplicar rótulos de acesso e governança de dados é exibido.](../assets/segmentation/audience-builder/apply-access-labels.png)

O restante da seção de propriedades do público permite editar detalhes relacionados ao público-alvo da conta, incluindo o nome, a descrição e as tags.

![Os detalhes das propriedades do público-alvo são exibidos.](../assets/segmentation/audience-builder/audience-details.png){width="300"}

Você **não pode** alterar o método de avaliação para públicos-alvo da conta, pois todos os públicos-alvo da conta são avaliados usando a segmentação em lotes.

## Próximas etapas {#next-steps}

O Audience Builder fornece um fluxo de trabalho avançado que permite criar públicos a partir dos dados da conta de negócios XDM.

Para saber mais sobre o Serviço de segmentação para dados de perfil do cliente, leia a [Visão geral do serviço de segmentação](../../segmentation/home.md){target="_blank"}.
