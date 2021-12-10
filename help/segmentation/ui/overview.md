---
keywords: Experience Platform, home, tópicos populares, Serviço de segmentação, segmentação, serviço de segmentação, guia do usuário, guia da interface do usuário, guia da interface de segmentação, construtor de segmentos, construtor de segmentos, realizado, existente, existente, sair;
solution: Experience Platform
title: Guia da interface do usuário do serviço de segmentação
topic-legacy: ui guide
description: O Serviço de segmentação do Adobe Experience Platform fornece uma interface de usuário para criar e gerenciar definições de segmento.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: ce3d5e3db28d39b8d7d5a984700dd681c650ac94
workflow-type: tm+mt
source-wordcount: '1693'
ht-degree: 0%

---

# Guia da interface do usuário do serviço de segmentação

[!DNL Adobe Experience Platform Segmentation Service] O fornece uma interface de usuário para criar e gerenciar definições de segmento.

## Introdução

Trabalhar com definições de segmento requer uma compreensão das várias [!DNL Experience Platform] serviços envolvidos com a segmentação. Antes de ler este guia do usuário, reveja a documentação dos seguintes serviços:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] permite dividir os dados armazenados em [!DNL Experience Platform] que se relaciona a indivíduos (como clientes, clientes potenciais, usuários ou organizações) em grupos menores.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Permite a criação de perfis de clientes ao unir identidades de fontes de dados diferentes que estão sendo assimiladas em [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente. Para utilizar melhor a Segmentação, verifique se os dados são assimilados como perfis e eventos de acordo com a variável [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).

Também é importante saber dois termos principais que são usados por meio deste documento e entender a diferença entre eles:
- **Definição de segmento**: O conjunto de regras usado para descrever as principais características ou comportamentos de um público-alvo.
- **Público**: O conjunto resultante de perfis que atendem aos critérios de uma definição de segmento.

## Visão geral

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Segmentos]** na navegação à esquerda para abrir o **[!UICONTROL Visão geral]** exibição da guia [!UICONTROL Segmentos] painel.

>[!NOTE]
>
>Se sua organização for nova na Plataforma e ainda não tiver conjuntos de dados ativos do Perfil ou políticas de mesclagem criadas, a variável [!UICONTROL Segmentos] o painel não está visível. Em vez disso, a variável [!UICONTROL Visão geral] A guia exibe links e documentação para ajudar você a começar a usar segmentos.

### [!UICONTROL Segmentos] painel {#segments-dashboard}

O **[!UICONTROL Segmentos]** o painel descreve as métricas principais relacionadas aos dados de segmento de sua organização.

Para saber mais, visite o [guia do painel de segmentos](../../dashboards/guides/segments.md).

![](../../dashboards/images/segments/dashboard-overview.png)

## Procurar {#browse}

Selecione o **[!UICONTROL Procurar]** para ver uma lista de todas as definições de segmento para sua Organização IMS.

![](../images/ui/overview/segment-browse-all.png)

Essa exibição lista informações sobre a definição do segmento, incluindo detalhamento, churn, contagem de perfis, método de avaliação, data criada e data da última modificação.

O detalhamento mostra um gráfico de barras que descreve a porcentagem de perfis que pertencem a cada um dos seguintes status: [!UICONTROL Realizado], [!UICONTROL Existente]e [!UICONTROL Saindo]. Além disso, o detalhamento mostrado na variável [!UICONTROL Procurar] é o detalhamento mais preciso do status do segmento. Se este número diferir do que está indicado na variável [!UICONTROL Visão geral] use os números na guia [!UICONTROL Procurar] como a fonte correta de informações, já que [!UICONTROL Visão geral] os números de guia só são atualizados uma vez por dia.

![](../images/ui/overview/segment-browse-breakdown.png)

| Status | Descrição |
| ------ | ----------- |
| Realizado | Um novo perfil no segmento. |
| Existente | Um perfil existente que permaneceu no segmento. |
| Saindo | Um perfil existente que está deixando o segmento. |

O churn representa a porcentagem de perfis que estão mudando em uma definição de segmento em comparação à última vez que o trabalho do segmento foi executado, enquanto a contagem de perfis representa o número total de perfis qualificados para o segmento.

O método de avaliação pode ser streaming ou batch. Segmentos de fluxo são constantemente avaliados à medida que os dados entram no sistema. Segmentos em lote são avaliados de acordo com uma programação definida.

![](../images/ui/overview/segment-browse-segments.png)

Na parte superior da página, há opções para adicionar todos os segmentos a uma programação e para criar um novo segmento.

Alternando **[!UICONTROL Adicionar todos os segmentos para agendar]** habilitará a segmentação agendada. Mais informações sobre a segmentação agendada podem ser encontradas na seção [seção de segmentação agendada deste guia do usuário](#scheduled-segmentation).

Selecionar **[!UICONTROL Criar segmento]** levará você ao Construtor de segmentos. Para saber mais sobre como criar segmentos, leia a seção sobre [criar um segmento no guia do usuário](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

A barra lateral direita contém informações sobre todos os segmentos na organização IMS, listando o número total de segmentos, a última data de avaliação, a próxima data de avaliação, bem como um detalhamento dos segmentos por método de avaliação.

![](../images/ui/overview/segment-browse-segment-info.png)

A seleção da linha de definição de segmento fornece um resumo da definição do segmento, incluindo opções para editar ou excluir o segmento, ativar o segmento para um destino, o público-alvo qualificado para o segmento, o tamanho total do público-alvo, além do nome do segmento, descrição, método de avaliação, data criada e data da última modificação.

>[!NOTE]
>
> Você irá **not** ser capaz de excluir um segmento usado em uma ativação de destino.

![](../images/ui/overview/segment-browse-details.png)

## Detalhes da definição do segmento {#segment-details}

Para ver mais detalhes sobre uma definição de segmento específica, selecione o nome de um segmento na **[!UICONTROL Procurar]** guia .

A página de detalhes do segmento é exibida. Na parte superior, há um resumo da definição do segmento, informações sobre o tamanho do público-alvo qualificado, bem como destinos para os quais o segmento é ativado.

![](../images/ui/overview/segment-details-summary.png)

### Resumo do segmento

O **[!UICONTROL Resumo do segmento]** A seção fornece informações como ID, nome, descrição e detalhes dos atributos.

Além disso, você tem a opção de ativar o segmento para um destino ou editar o segmento. Selecionar **[!UICONTROL Ativar para destino]** permitirá ativar o segmento para um destino. Para obter informações mais detalhadas sobre como ativar um segmento em um destino, leia o [visão geral da ativação](../../destinations/ui/activation-overview.md).

![](../images/ui/overview/segment-details-activate.png)

Selecionar **[!UICONTROL Editar segmento]** trará você ao [!DNL Segment Builder]. Para obter informações mais detalhadas sobre o uso da variável [!DNL Segment Builder] espaço de trabalho, leia o [[!DNL Segment Builder] guia do usuário](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### Público-alvo total no segmento

O **[!UICONTROL Público-alvo total no segmento]** mostra o número total de perfis qualificados para o segmento.

As estimativas são geradas usando um tamanho de amostra dos dados de amostra desse dia. Se houver menos de 1 milhão de entidades em seu armazenamento de perfil, o conjunto de dados completo será usado; para entre 1 e 20 milhões de entidades, são utilizadas 1 milhão de entidades; e para mais de 20 milhões de entidades, são utilizados 5% do total de entidades. Mais informações sobre a geração de estimativas de segmento podem ser encontradas na seção [seção de geração de estimativa](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) do tutorial de criação de segmentos.

### Destinos ativados

O **[!UICONTROL Destinos ativados]** mostra os destinos para os quais este segmento está ativado.

>[!NOTE]
>
> Os destinos são um recurso disponível com [!DNL Real-time Customer Data Platform]e permitem exportar dados para plataformas externas. Para obter mais informações sobre destinos, leia o [visão geral dos destinos](../../destinations/home.md). Para saber como ativar um segmento para um destino, consulte [visão geral da ativação](../../destinations/ui/activation-overview.md).

### Amostras de perfil

Abaixo está uma amostra dos perfis qualificados para o segmento, detalhando as informações, incluindo o [!DNL Profile] ID, nome, sobrenome e email pessoal.

A forma como a amostragem de dados é acionada depende do método de ingestão.

Para a assimilação em lote, o armazenamento de perfil é verificado automaticamente a cada quinze minutos para ver se um novo lote foi assimilado com êxito desde a execução do último trabalho de amostragem. Se esse for o caso, a loja de perfis é digitalizada subsequentemente para ver se houve pelo menos uma mudança de 5% no número de registros. Se essas condições forem atendidas, um novo trabalho de amostragem será acionado.

Para assimilação de streaming, o armazenamento de perfil é verificado automaticamente a cada hora para verificar se houve pelo menos uma mudança de 5% no número de registros. Se essa condição for atendida, um novo trabalho de amostragem será acionado.

O tamanho da amostra da verificação depende do número geral de entidades no armazenamento de perfis. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades no armazenamento de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto de dados completo |
| 1 a 20 milhões | 1 milhão |
| Mais de 20 milhões | 5% do total |

Informações mais detalhadas sobre cada [!DNL Profile] pode ser visualizada selecionando a variável [!DNL Profile] ID. Para saber mais sobre os detalhes de um perfil, leia o [[!DNL Real-time Customer Profile] guia do usuário](../../profile/ui/user-guide.md#profile-detail).

![](../images/ui/overview/segment-details-profiles.png)

## Criação de um segmento {#create-segment}

Selecionar **[!UICONTROL Criar segmento]** no canto superior direito, abre o [!DNL Segment Builder] , onde é possível começar a criar uma definição de segmento.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] espaço de trabalho

[!DNL Segment Builder] O fornece um espaço de trabalho avançado com o qual você pode interagir [!DNL Profile] elementos de dados. O espaço de trabalho oferece controles intuitivos para criar e editar regras, como blocos de arrastar e soltar usados para representar propriedades de dados.

Para obter informações mais detalhadas sobre o uso da variável [!DNL Segment Builder] espaço de trabalho, leia o [[!DNL Segment Builder] guia do usuário](./segment-builder.md).

![](../images/ui/overview/segment-builder.png)

## Segmentação programada {#scheduled-segmentation}

Depois que as definições de segmento forem criadas, você poderá avaliá-las por meio de uma avaliação sob demanda ou programada (contínua). Avaliação significa mudança [!DNL Real-time Customer Profile] por meio de definições de segmento, para produzir públicos-alvo correspondentes. Depois de criados, os públicos-alvo são salvos e armazenados para que possam ser exportados usando [!DNL Experience Platform] APIs.

A avaliação sob demanda envolve o uso da API para executar a avaliação e criar públicos-alvo, conforme necessário, enquanto a avaliação agendada (também conhecida como &quot;segmentação agendada&quot;) permite criar um agendamento recorrente para avaliar as definições de segmento em um horário específico (no máximo, uma vez por dia).

### Ativar a segmentação agendada {#enable-scheduled-segmentation}

Habilitar suas definições de segmento para avaliação agendada pode ser feito usando a interface do usuário ou a API. Na interface do usuário do , retorne ao **[!UICONTROL Procurar]** guia no **[!UICONTROL Segmentos]** e ativar **[!UICONTROL Adicionar todos os segmentos para agendar]**. Isso fará com que todos os segmentos sejam avaliados com base no agendamento definido pela organização.

>[!NOTE]
>
>A avaliação programada pode ser ativada para sandboxes com no máximo cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. Se sua organização tiver mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile] em um único ambiente de sandbox, você não poderá usar a avaliação agendada.

No momento, os agendamentos só podem ser criados usando a API. Para obter etapas detalhadas sobre como criar, editar e trabalhar com agendamentos usando a API, siga o tutorial para avaliar e acessar os resultados do segmento, especificamente a seção sobre [avaliação programada usando a API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Segmentação de streaming {#streaming-segmentation}

A segmentação por streaming é a capacidade de fazer segmentação em [!DNL Platform] em tempo quase real, enquanto se concentra na riqueza de dados. Com a segmentação de fluxo, a qualificação de segmento agora acontece à medida que os dados chegam ao [!DNL Platform], aliviando a necessidade de agendar e executar tarefas de segmentação.

Mais informações sobre a segmentação de streaming podem ser encontradas na seção [guia do usuário de segmentação de fluxo](./streaming-segmentation.md).

>[!NOTE]
>
>Para que a segmentação de transmissão funcione, é necessário ativar a segmentação agendada para a organização. Para obter detalhes sobre como ativar a segmentação agendada, consulte [a seção de segmentação de fluxo neste guia do usuário](#scheduled-segmentation).

## Segmentação de borda {#edge-segmentation}

A segmentação de borda é a capacidade de avaliar segmentos na Platform instantaneamente na borda, permitindo casos de uso de personalização de página da mesma página e da próxima página.

Mais informações sobre a segmentação de borda podem ser encontradas na seção [guia da interface do usuário de segmentação de borda](./edge-segmentation.md)

## Violações políticas

>[!NOTE]
>
>As violações de política se aplicam somente se você estiver criando um segmento que foi atribuído a um destino.

Quando terminar de criar seu segmento, o segmento será analisado pela Governança de dados do Adobe Experience Platform para garantir que não haja violações de política no segmento. Consulte a [Visão geral da governança de dados](../../data-governance/home.md) para obter mais informações.

![](../images/ui/overview/segment-dule-policy-violations.png)

## Próximas etapas e recursos adicionais {#next-steps}

O [!DNL Segmentation Service] A interface do usuário fornece um fluxo de trabalho avançado que permite isolar públicos comercializáveis do [!DNL Real-time Customer Profile] dados.

Para saber mais sobre [!DNL Segmentation Service], continue lendo a documentação. Para saber como usar o [!DNL Segmentation Service] Leia a API [[!DNL Segmentation Service] guia do desenvolvedor](../api/overview.md).
