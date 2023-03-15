---
keywords: Experience Platform;página inicial;tópicos populares;Serviço de segmentação;segmentação;serviço de segmentação;guia do usuário;guia da interface do usuário;guia da interface do usuário de segmentação;construtor de segmentos;construtor de segmentos;realizado;existente;saindo;
solution: Experience Platform
title: Guia da interface do usuário do Serviço de segmentação
description: O Serviço de segmentação da Adobe Experience Platform fornece uma interface para criar e gerenciar definições de segmentos.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '2647'
ht-degree: 1%

---

# Guia da interface do usuário do serviço de segmentação

[!DNL Adobe Experience Platform Segmentation Service] O fornece uma interface para criar e gerenciar definições de segmento.

## Introdução

Trabalhar com definições de segmento requer uma compreensão dos vários [!DNL Experience Platform] serviços envolvidos com a segmentação. Antes de ler este guia do usuário, consulte a documentação dos seguintes serviços:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] permite dividir os dados armazenados no [!DNL Experience Platform] que se relaciona a indivíduos (como clientes, clientes potenciais, usuários ou organizações) em grupos menores.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): permite a criação de perfis de clientes, unindo identidades de diferentes fontes de dados que estão sendo assimiladas na [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente. Para melhor usar a segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com a [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).

Também é importante conhecer dois termos principais usados neste documento e compreender a diferença entre eles:
- **Definição de segmento**: o conjunto de regras usado para descrever as principais características ou comportamentos de um público-alvo.
- **Público**: o conjunto de perfis que atendem aos critérios de uma definição de segmento. Ele pode ser criado por meio do Adobe Experience Platform (público-alvo gerado pela Platform) ou de uma fonte externa (público-alvo gerado externamente).

## Visão geral

Na interface do Experience Platform, selecione **[!UICONTROL Segmentos]** na navegação à esquerda, para abrir a **[!UICONTROL Visão geral]** guia exibindo o [!UICONTROL Segmentos] painel.

>[!NOTE]
>
>Se sua organização for nova na Plataforma e ainda não tiver conjuntos de dados de Perfil ativos ou políticas de mesclagem criadas, a variável [!UICONTROL Segmentos] o painel não está visível. Em vez disso, a variável [!UICONTROL Visão geral] A guia exibe links e a documentação para ajudar você a começar a usar segmentos.

### [!UICONTROL Segmentos] painel {#segments-dashboard}

A variável **[!UICONTROL Segmentos]** O painel descreve as métricas principais relacionadas aos dados de segmento de sua organização.

Para saber mais, visite o [guia do painel de segmentos](../../dashboards/guides/segments.md).

![O painel de segmentos é exibido. Ele mostra vários widgets, incluindo o tamanho do público, perfis por identidade, sobreposição de identidade e a tendência de alteração do tamanho do público.](../../dashboards/images/segments/dashboard-overview.png)

## Navegar {#browse}

>[!CONTEXTUALHELP]
>id="platform_segments_browse_churncolumnname"
>title="Churn"
>abstract="O churn representa a porcentagem de perfis que estão mudando em uma definição de segmento em comparação à última vez que o trabalho de segmento foi executado."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_evaluationmethodcolumnname"
>title="Método de avaliação"
>abstract="Os métodos de avaliação para segmentos incluem lote, fluxo e borda."

>[!CONTEXTUALHELP]
>id="platform_segments_browse_addallsegmentstoschedule"
>title="Adicionar todos os segmentos ao agendamento"
>abstract="Permite incluir todos os segmentos de avaliação em lote na atualização diária programada. Desativar para remover todos os segmentos da atualização programada."

Selecione o **[!UICONTROL Procurar]** para ver uma lista de todas as definições de segmento da organização.

![A tela de navegação de segmentos é exibida. Uma lista de todos os segmentos pertencentes à organização é exibida.](../images/ui/overview/segment-browse-all.png)

Essa exibição lista informações sobre a definição do segmento, incluindo a contagem de perfis, a data de criação e a última data de modificação.

É possível adicionar outros campos a essa exibição selecionando ![o ícone do atributo de filtro](../images/ui/overview/filter-attribute.png). Esses campos adicionais incluem detalhamento, churn, método de avaliação e ID do trabalho.

Se a opção de detalhamento estiver selecionada, a tela mostrará um gráfico de barras descrevendo a porcentagem de perfis que pertencem a cada um dos seguintes status: [!UICONTROL Realizado], [!UICONTROL Existente], e [!UICONTROL Saindo]. Além disso, a discriminação mostrada na [!UICONTROL Procurar] é o detalhamento mais preciso do status do segmento. Se este número for diferente do indicado no [!UICONTROL Visão geral] , você deve usar os números no [!UICONTROL Procurar] guia como a fonte correta de informações, já que a variável [!UICONTROL Visão geral] os números de guia são atualizados apenas uma vez por dia.

| Status | Descrição |
| ------ | ----------- |
| Realizado | Um novo perfil no segmento. |
| Existente | Um perfil existente que permaneceu dentro do segmento. |
| Saindo | Um perfil existente que está deixando o segmento. |

O churn representa a porcentagem de perfis que estão mudando em uma definição de segmento em comparação à última vez que o trabalho de segmento foi executado, enquanto a contagem de perfis representa o número total de perfis qualificados para o segmento.

O método de avaliação pode ser streaming, batch ou borda. Os segmentos de transmissão são constantemente avaliados à medida que os dados entram no sistema. Os segmentos em lote são avaliados de acordo com uma programação definida. Os segmentos de borda são avaliados em tempo real, o que permite casos de uso de personalização da mesma página e da próxima página.

![Os segmentos na página de navegação de segmentos são destacados.](../images/ui/overview/segment-browse-segments.png)

Na parte superior da página há opções para adicionar todos os segmentos a um agendamento e criar um novo segmento.

Alternando **[!UICONTROL Adicionar todos os segmentos ao agendamento]** habilitará a segmentação agendada. Mais informações sobre segmentação agendada podem ser encontradas na [seção segmentação programada deste guia do usuário](#scheduled-segmentation).

Selecionar **[!UICONTROL Criar segmento]** O direcionará para o Construtor de segmentos. Para saber mais sobre como criar segmentos, leia a seção sobre [criação de um segmento no guia do usuário](#create-segment).

![A barra de navegação superior na página de navegação do segmento é realçada. Essa barra contém um botão para adicionar todos os segmentos a um agendamento e outro para criar um segmento.](../images/ui/overview/segment-browse-top.png)

A barra lateral direita contém informações sobre todos os segmentos na organização, listando o número total de segmentos, a última data de avaliação, a próxima data de avaliação, bem como um detalhamento dos segmentos por método de avaliação.

![A barra lateral direita na página de navegação do segmento é realçada. As informações sobre os segmentos na organização são mostradas. Isso inclui informações como o número total de segmentos, o último tempo avaliado, o próximo tempo avaliado, bem como um detalhamento dos diferentes tipos de segmentos.](../images/ui/overview/segment-browse-segment-info.png)

Selecionar a linha da definição de segmento fornece um resumo da definição de segmento, incluindo opções para editar ou excluir o segmento, ativar o segmento para um destino, o público qualificado para o segmento, o tamanho total do público, além do nome do segmento, da descrição, do método de avaliação, da data de criação e da última data modificada.

>[!NOTE]
>
> Você vai **não** poder excluir um segmento usado em uma ativação de destino.

![Detalhes sobre o segmento selecionado são mostrados. Inclui detalhes sobre o número de perfis qualificados, a divisão de porcentagem de perfis qualificados em comparação ao total de perfis, a data da última avaliação.](../images/ui/overview/segment-browse-details.png)

## Detalhes de definição do segmento {#segment-details}

Para ver mais detalhes sobre uma definição de segmento específica, selecione o nome de um segmento na **[!UICONTROL Procurar]** guia.

A página de detalhes do segmento é exibida. Na parte superior, há um resumo da definição de segmento, informações sobre o tamanho do público qualificado, bem como destinos para os quais o segmento é ativado.

![A página de detalhes da definição do segmento é exibida. O resumo do segmento, o público total no segmento e os cartões de destinos ativados são destacados.](../images/ui/overview/segment-details-summary.png)

### Resumo do segmento {#segment-summary}

A variável **[!UICONTROL Resumo do segmento]** fornece informações como ID, nome, descrição e detalhes dos atributos.

Além disso, você tem a opção de ativar o segmento para um destino ou editá-lo. Selecionar **[!UICONTROL Ativar para destino]** permitirá ativar o segmento para um destino. Para obter informações mais detalhadas sobre como ativar um segmento para um destino, leia o [visão geral da ativação](../../destinations/ui/activation-overview.md).

![O botão Ativate to destination (Ativar para destino) é realçado.](../images/ui/overview/segment-details-activate.png)

Selecionar **[!UICONTROL Editar segmento]** O levará você ao [!DNL Segment Builder]. Para obter informações mais detalhadas sobre o uso do [!DNL Segment Builder] espaço de trabalho, leia o [[!DNL Segment Builder] guia do usuário](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### Público total no segmento

A variável **[!UICONTROL Público total no segmento]** mostra o número total de perfis qualificados para o segmento.

As estimativas são geradas usando um tamanho de amostra dos dados de amostra desse dia. Se houver menos de 1 milhão de entidades no armazenamento de perfil, o conjunto de dados completo será usado; para entre 1 e 20 milhões de entidades, será usado 1 milhão de entidades; e para mais de 20 milhões de entidades, será usado 5% do total de entidades. Mais informações sobre a geração de estimativas de segmentos podem ser encontradas no [seção geração de estimativa](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) do tutorial de criação de segmento.

### Destinos ativados

A variável **[!UICONTROL Destinos ativados]** mostra os destinos para os quais esse segmento está ativado.

>[!NOTE]
>
> Os destinos são um recurso disponível com o [!DNL Adobe Real-Time Customer Data Platform]e permitem exportar dados para plataformas externas. Para obter mais informações sobre destinos, leia a [visão geral dos destinos](../../destinations/home.md). Para saber como ativar um segmento para um destino, consulte [visão geral da ativação](../../destinations/ui/activation-overview.md).

### Amostras de perfil

Abaixo está uma amostra de perfis qualificados para o segmento, detalhando informações, incluindo a [!DNL Profile] ID, nome, sobrenome e email pessoal.

A maneira como a amostragem de dados é acionada depende do método de assimilação.

Para assimilação em lote, o armazenamento de perfil é automaticamente verificado a cada quinze minutos para ver se um novo lote foi assimilado com êxito desde que o último trabalho de amostragem foi executado. Se esse for o caso, o armazenamento de perfil será digitalizado posteriormente para ver se houve pelo menos uma alteração de 5% no número de registros. Se essas condições forem atendidas, um novo trabalho de amostragem será acionado.

Para a assimilação por transmissão, o armazenamento de perfil é verificado automaticamente a cada hora para ver se houve pelo menos 5% de alteração no número de registros. Se essa condição for atendida, um novo trabalho de amostragem será acionado.

O tamanho da amostra da verificação depende do número geral de entidades no armazenamento de perfis. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades na loja de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto de dados completo |
| 1 a 20 milhões | 1 milhão |
| Mais de 20 milhões | 5% do total |

Informações mais detalhadas sobre cada [!DNL Profile] pode ser visto selecionando o [!DNL Profile] ID. Para saber mais sobre os detalhes de um perfil, leia o [[!DNL Real-Time Customer Profile] guia do usuário](../../profile/ui/user-guide.md#profile-detail).

![Os perfis de amostra para a definição do segmento são destacados. As informações de perfil de amostra incluem a ID do perfil, o nome, o sobrenome e o email da pessoa.](../images/ui/overview/segment-details-profiles.png)

## Criação de um segmento {#create-segment}

Selecionar **[!UICONTROL Criar segmento]** no canto superior direito abre a janela [!DNL Segment Builder] espaço de trabalho, onde você pode começar a criar uma definição de segmento.

![Na página de navegação do segmento, o botão Criar segmento é realçado.](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] espaço de trabalho

[!DNL Segment Builder] O fornece um espaço de trabalho avançado que permite a você interagir com o [!DNL Profile] elementos de dados. O espaço de trabalho fornece controles intuitivos para criar e editar regras, como arrastar e soltar blocos usados para representar propriedades de dados.

Para obter informações mais detalhadas sobre o uso do [!DNL Segment Builder] espaço de trabalho, leia o [[!DNL Segment Builder] guia do usuário](./segment-builder.md).

![A área de trabalho do Construtor de segmentos é exibida.](../images/ui/overview/segment-builder.png)

## Segmentação programada {#scheduled-segmentation}

Depois que as definições de segmento forem criadas, você poderá avaliá-las por meio de uma avaliação sob demanda ou programada (contínua). Avaliação significa mudança [!DNL Real-Time Customer Profile] por meio de definições de segmento, para produzir públicos-alvo correspondentes. Depois de criados, os públicos-alvo são salvos e armazenados para que possam ser exportados usando [!DNL Experience Platform] APIs.

A avaliação sob demanda envolve o uso da API para executar a avaliação e criar públicos-alvo, conforme necessário, enquanto a avaliação programada (também conhecida como &quot;segmentação programada&quot;) permite criar uma programação recorrente para avaliar as definições de segmento em um horário específico (em um máximo, uma vez por dia).

### Ativar segmentação programada {#enable-scheduled-segmentation}

A ativação das definições de segmento para avaliação agendada pode ser feita usando a interface ou a API. Na interface do usuário, retorne à **[!UICONTROL Procurar]** guia no **[!UICONTROL Segmentos]** e ativar **[!UICONTROL Adicionar todos os segmentos ao agendamento]**. Isso fará com que todos os segmentos sejam avaliados com base no agendamento definido por sua organização.

>[!NOTE]
>
>A avaliação agendada pode ser ativada para sandboxes com um máximo de cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. Se sua organização tiver mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile] em um único ambiente de sandbox, não será possível usar a avaliação programada.

Atualmente, os cronogramas só podem ser criados usando a API. Para obter etapas detalhadas sobre como criar, editar e trabalhar com agendamentos usando a API, siga o tutorial para avaliar e acessar resultados de segmentos, especificamente a seção sobre [avaliação agendada usando a API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![A alternância para Adicionar todos os segmentos a uma programação é realçada na página Procurar segmentos.](../images/ui/overview/segment-browse-scheduled.png)

## Públicos-alvo {#audiences}

>[!IMPORTANT]
>
>A funcionalidade de públicos-alvo está atualmente na versão beta limitada e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Selecione o **[!UICONTROL Públicos-alvo]** para ver uma lista de todos os públicos-alvo da sua organização.

![Uma lista de públicos-alvo para sua organização.](../images/ui/overview/list-audiences.png)

Por padrão, essa exibição lista informações sobre os públicos-alvo, incluindo o nome, a contagem de perfis, a origem, a data de criação e a última data modificada.

É possível selecionar a variável ![Personalizar tabela](../images/ui/overview/customize-table.png) ícone para alterar os campos exibidos.

![O botão personalizar tabela é realçado. Selecionar esse botão permite personalizar os campos exibidos na página de navegação de Públicos-alvo.](../images/ui/overview/select-customize-table.png)

Um popover é exibido, listando todos os campos que podem ser exibidos dentro da tabela.

![Os atributos que podem ser exibidos para a seção Procurar públicos.](../images/ui/overview/customize-table-attributes.png)

| Campo | Descrição |
| ----- | ----------- | 
| [!UICONTROL Nome] | O nome do público-alvo. |
| [!UICONTROL Contagem de perfis] | O número total de perfis qualificados para o público-alvo. |
| [!UICONTROL Origem] | A origem do público. Se esse público-alvo foi gerado pela Platform, ele terá uma origem de Serviço de segmentação. |
| [!UICONTROL Status do ciclo de vida] | O status do público. Os valores possíveis para esse campo incluem `Draft`, `Published`, e `Archived`. |
| [!UICONTROL Frequência das atualizações] | Um valor que indica a frequência com que os dados do público-alvo são atualizados. Os valores possíveis para esse campo incluem `On Demand`, `Scheduled`, e `Continuous`. |
| [!UICONTROL Última atualização realizada por] | O nome da última pessoa que atualizou o público. |
| [!UICONTROL Criado] | A hora e a data em que o público-alvo foi criado. |
| [!UICONTROL Última atualização] | A hora e a data em que o público-alvo foi criado pela última vez. |
| [!UICONTROL Acessar rótulos] | Os rótulos de acesso do público-alvo. Os rótulos de acesso permitem categorizar conjuntos de dados e campos de acordo com as políticas de uso que se aplicam a esses dados. Esses rótulos podem ser aplicados a qualquer momento, fornecendo flexibilidade na maneira como você escolhe controlar os dados. Para obter mais informações sobre rótulos de acesso, leia a documentação em [gerenciamento de rótulos](../../access-control/abac/ui/labels.md). |

É possível selecionar **[!UICONTROL Criar público-alvo]** para criar um público-alvo.

![O botão Criar público-alvo é realçado, mostrando onde selecionar para criar um público-alvo.](../images/ui/overview/create-audience.png)

Um popover é exibido, permitindo que você escolha entre compor um público-alvo ou criar regras.

![Um popover que exibe os dois tipos de públicos-alvo que você pode criar.](../images/ui/overview/create-audience-type.png)

Selecionar **[!UICONTROL Compor públicos]** O direciona para o Construtor de público-alvo. Para saber mais sobre como criar públicos-alvo, leia o [Guia do Audience Builder](./audience-builder.md).

Selecionar **[!UICONTROL Criar regra]** direciona você ao Construtor de segmentos. Para saber mais sobre como criar segmentos, leia a [Guia do Construtor de segmentos](./segment-builder.md)

## Detalhes do público {#audience-details}

Para ver mais detalhes sobre um público específico, selecione o nome de um público na [!UICONTROL Públicos-alvo] guia.

A página de detalhes do público-alvo é exibida. Esta página difere em detalhes, dependendo se o público-alvo foi gerado com o Adobe Experience Platform ou de uma fonte externa, como a Orquestração de público-alvo.

### Público-alvo gerado pela plataforma

Para obter mais informações sobre públicos-alvo gerados pela Platform, leia o [seção de resumo de segmento](#segment-summary).

### Público gerado externamente

Na parte superior da página de detalhes do público-alvo, há um resumo do público-alvo e detalhes sobre o conjunto de dados em que o público-alvo é salvo.

![Os detalhes fornecidos para um público-alvo gerado externamente.](../images/ui/overview/externally-generated-audience.png)

A variável **[!UICONTROL Resumo do público]** fornece informações como ID, nome, descrição e detalhes dos atributos.

A variável **[!UICONTROL Detalhes do conjunto de dados]** fornece informações como nome, descrição, nome da tabela, origem e esquema. É possível selecionar **[!UICONTROL Exibir conjunto de dados]** para ver mais informações sobre o conjunto de dados.

| Campo | Descrição |
| ----- | ----------- |
| [!UICONTROL Nome] | O nome do conjunto de dados. |
| [!UICONTROL Descrição] | A descrição do conjunto de dados. |
| [!UICONTROL Nome da tabela] | O nome da tabela do conjunto de dados. |
| [!UICONTROL Fonte] | A origem do conjunto de dados. Para públicos gerados externamente, esse valor será **Esquema**. |
| [!UICONTROL Esquema] | O tipo de esquema XDM ao qual o conjunto de dados corresponde. |

Para saber mais sobre conjuntos de dados, leia o [visão geral do conjunto de dados](../../catalog/datasets/overview.md).

## Segmentação de transmissão {#streaming-segmentation}

A segmentação de transmissão é a capacidade de fazer a segmentação em [!DNL Platform] em tempo quase real, concentrando-se na riqueza de dados. Com a segmentação por transmissão, a qualificação de segmentos agora acontece à medida que os dados chegam ao [!DNL Platform], reduzindo a necessidade de agendar e executar trabalhos de segmentação.

Mais informações sobre a segmentação por transmissão podem ser encontradas na [guia do usuário de segmentação por transmissão](./streaming-segmentation.md).

>[!NOTE]
>
>Para que a segmentação por transmissão funcione, é necessário habilitar a segmentação agendada para a organização. Para obter detalhes sobre como ativar a segmentação programada, consulte [a seção segmentação por transmissão neste guia do usuário](#scheduled-segmentation).

## Segmentação de borda {#edge-segmentation}

A segmentação de borda é a capacidade de avaliar segmentos na Platform instantaneamente na borda, permitindo casos de uso de personalização da mesma página e da próxima página.

Mais informações sobre segmentação de borda podem ser encontradas no [guia da interface de segmentação de borda](./edge-segmentation.md)

## Violações de política

>[!NOTE]
>
>As violações de política só se aplicam se você estiver criando um segmento que foi atribuído a um destino.

Quando terminar de criar o segmento, ele será analisado pelo Adobe Experience Platform Data Governance para garantir que não haja violações de política no segmento. Consulte a [Visão geral da governança de dados](../../data-governance/home.md) para obter mais informações.

![As violações de política para o segmento são exibidas.](../images/ui/overview/segment-dule-policy-violations.png)

## Próximas etapas e recursos adicionais {#next-steps}

A variável [!DNL Segmentation Service] A interface do usuário fornece um fluxo de trabalho avançado que permite isolar públicos comercializáveis de [!DNL Real-Time Customer Profile] dados.

Para saber mais sobre [!DNL Segmentation Service], continue lendo a documentação. Para saber como usar o [!DNL Segmentation Service] API, leia as [[!DNL Segmentation Service] guia do desenvolvedor](../api/overview.md).
