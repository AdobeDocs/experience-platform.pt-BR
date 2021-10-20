---
keywords: Experience Platform, home, tópicos populares, Serviço de segmentação, segmentação, serviço de segmentação, guia do usuário, guia da interface do usuário, guia da interface de segmentação, construtor de segmentos, construtor de segmentos, realizado, existente, existente, sair;
solution: Experience Platform
title: Guia da interface do usuário do serviço de segmentação
topic-legacy: ui guide
description: O Serviço de segmentação do Adobe Experience Platform fornece uma interface de usuário para criar e gerenciar definições de segmento.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: d65bcf62f0de29dc293a1a1313178a408613a024
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 0%

---

# Guia da interface do usuário do serviço de segmentação

[!DNL Adobe Experience Platform Segmentation Service] O fornece uma interface de usuário para criar e gerenciar definições de segmento.

## Introdução

Trabalhar com definições de segmento requer uma compreensão das várias [!DNL Experience Platform] serviços envolvidos com a segmentação. Antes de ler este guia do usuário, reveja a documentação dos seguintes serviços:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] permite dividir os dados armazenados em [!DNL Experience Platform] que se relaciona a indivíduos (como clientes, clientes potenciais, usuários ou organizações) em grupos menores.
- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Permite a criação de perfis de clientes ao unir identidades de fontes de dados diferentes que estão sendo assimiladas em [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

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

## Procurar

Selecione o **[!UICONTROL Procurar]** para ver uma lista de todas as definições de segmento para sua Organização IMS.

![](../images/ui/overview/segment-browse-all.png)

This view lists information about the segment definition including the breakdown, churn, profile count, evaluation method, created date, and last modified date.

O detalhamento mostra um gráfico de barras que descreve a porcentagem de perfis que pertencem a cada um dos seguintes status: [!UICONTROL Realizado], [!UICONTROL Existente]e [!UICONTROL Saindo]. Além disso, o detalhamento mostrado na variável [!UICONTROL Procurar] é o detalhamento mais preciso do status do segmento. Se este número diferir do que está indicado na variável [!UICONTROL Visão geral] use os números na guia [!UICONTROL Procurar] como a fonte correta de informações, já que [!UICONTROL Visão geral] os números de guia só são atualizados uma vez por dia.

![](../images/ui/overview/segment-browse-breakdown.png)

| Status | Descrição |
| ------ | ----------- |
| Realizado | Um novo perfil no segmento. |
| Existing | Um perfil existente que permaneceu no segmento. |
| Exiting | Um perfil existente que está deixando o segmento. |

O churn representa a porcentagem de perfis que estão mudando em uma definição de segmento em comparação à última vez que o trabalho do segmento foi executado, enquanto a contagem de perfis representa o número total de perfis qualificados para o segmento.

The evaluation method can either be streaming or batch. Segmentos de fluxo são constantemente avaliados à medida que os dados entram no sistema. Segmentos em lote são avaliados de acordo com uma programação definida.

![](../images/ui/overview/segment-browse-segments.png)

Na parte superior da página, há opções para adicionar todos os segmentos a uma programação e para criar um novo segmento.

Toggling **[!UICONTROL Add all segments to schedule]** will enable scheduled segmentation. Mais informações sobre a segmentação agendada podem ser encontradas na seção [seção de segmentação agendada deste guia do usuário](#scheduled-segmentation).

Selecting **[!UICONTROL Create segment]** will take you to the Segment Builder. Para saber mais sobre como criar segmentos, leia a seção sobre [criar um segmento no guia do usuário](#create-segment).

![](../images/ui/overview/segment-browse-top.png)

The right sidebar contains information about all the segments within the IMS organization, listing the total number of segments, the last evaluation date, the next evaluation date, as well as a breakdown of the segments by evaluation method.

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

Além disso, você tem a opção de ativar o segmento para um destino ou editar o segmento. Selecionar **[!UICONTROL Ativar para destino]** permitirá ativar o segmento para um destino. For more detailed information on activating a segment to a destination, please read the [activation overview](../../destinations/ui/activation-overview.md).

![](../images/ui/overview/segment-details-activate.png)

Selecionar **[!UICONTROL Editar segmento]** trará você ao [!DNL Segment Builder]. Para obter informações mais detalhadas sobre o uso da variável [!DNL Segment Builder] espaço de trabalho, leia o [[!DNL Segment Builder] guia do usuário](./segment-builder.md).

![](../images/ui/overview/segment-details-edit-segment.png)

### Público-alvo total no segmento

O **[!UICONTROL Público-alvo total no segmento]** mostra o número total de perfis qualificados para o segmento.

As estimativas são geradas usando um tamanho de amostra dos dados de amostra desse dia. Se houver menos de 1 milhão de entidades em seu armazenamento de perfil, o conjunto de dados completo será usado; para entre 1 e 20 milhões de entidades, são utilizadas 1 milhão de entidades; e para mais de 20 milhões de entidades, são utilizados 5% do total de entidades. More information about generating segment estimates can be found in the [estimate generation section](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) of the segment creation tutorial.

### Destinos ativados

O **[!UICONTROL Destinos ativados]** mostra os destinos para os quais este segmento está ativado.

>[!NOTE]
>
> Destinations are a feature available with [!DNL Real-time Customer Data Platform], and allow you to export data to external platforms. Para obter mais informações sobre destinos, leia o [visão geral dos destinos](../../destinations/home.md). Para saber como ativar um segmento para um destino, consulte [visão geral da ativação](../../destinations/ui/activation-overview.md).

### Amostras de perfil

Abaixo está uma amostra dos perfis qualificados para o segmento, detalhando as informações, incluindo o [!DNL Profile] ID, nome, sobrenome e email pessoal.

A forma como a amostragem de dados é acionada depende do método de ingestão.

Para a assimilação em lote, o armazenamento de perfil é verificado automaticamente a cada quinze minutos para ver se um novo lote foi assimilado com êxito desde a execução do último trabalho de amostragem. Se esse for o caso, a loja de perfis é digitalizada subsequentemente para ver se houve pelo menos uma mudança de 5% no número de registros. If these conditions are met, a new sampling job is triggered.

For streaming ingestion, the profile store is automatically scanned every hour to see if there&#39;s been at least a 5% change in the number of records. Se essa condição for atendida, um novo trabalho de amostragem será acionado.

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

Once segment definitions have been created, you can then evaluate them through on-demand or scheduled (continuous) evaluation. Avaliação significa mudança [!DNL Real-time Customer Profile] por meio de definições de segmento, para produzir públicos-alvo correspondentes. Once created, the audiences are saved and stored so that they can be exported using [!DNL Experience Platform] APIs.

On-demand evaluation involves using the API to perform evaluation and build audiences as needed, whereas scheduled evaluation (also known as &#39;scheduled segmentation&#39;) allows you to create a recurring schedule to evaluate segment definitions at a specific time (at a maximum, once daily).

### Enable scheduled segmentation {#enable-scheduled-segmentation}

Habilitar suas definições de segmento para avaliação agendada pode ser feito usando a interface do usuário ou a API. In the UI, return to the **[!UICONTROL Browse]** tab within **[!UICONTROL Segments]** and toggle on **[!UICONTROL Add all segments to schedule]**. Isso fará com que todos os segmentos sejam avaliados com base no agendamento definido pela organização.

>[!NOTE]
>
>A avaliação programada pode ser ativada para sandboxes com no máximo cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. If your organization has more than five merge policies for [!DNL XDM Individual Profile] within a single sandbox environment, you will not be able to use scheduled evaluation.

No momento, os agendamentos só podem ser criados usando a API. For detailed steps on creating, editing, and working with schedules using the API, please follow the tutorial for evaluating and accessing segment results, specifically the section on [scheduled evaluation using the API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Segmentação de streaming {#streaming-segmentation}

Streaming segmentation is the ability to do segmentation on [!DNL Platform] in near real-time, while focusing on data richness. With streaming segmentation, segment qualification now happens as data lands into [!DNL Platform], alleviating the need to schedule and run segmentation jobs.

Mais informações sobre a segmentação de streaming podem ser encontradas na seção [guia do usuário de segmentação de fluxo](./streaming-segmentation.md).

>[!NOTE]
>
>Para que a segmentação de transmissão funcione, é necessário ativar a segmentação agendada para a organização. Para obter detalhes sobre como ativar a segmentação agendada, consulte [a seção de segmentação de fluxo neste guia do usuário](#scheduled-segmentation).

## Edge segmentation {#edge-segmentation}

A segmentação de borda é a capacidade de avaliar segmentos na Platform instantaneamente na borda, permitindo casos de uso de personalização de página da mesma página e da próxima página.

Mais informações sobre a segmentação de borda podem ser encontradas na seção [guia da interface do usuário de segmentação de borda](./edge-segmentation.md)

## Violações políticas

>[!NOTE]
>
>As violações de política se aplicam somente se você estiver criando um segmento que foi atribuído a um destino.

Quando terminar de criar seu segmento, o segmento será analisado pela Governança de dados do Adobe Experience Platform para garantir que não haja violações de política no segmento. Consulte a [[!DNL Data Governance] visão geral](../../data-governance/home.md) para obter mais informações.

![](../images/ui/overview/segment-dule-policy-violations.png)

## Próximas etapas e recursos adicionais {#next-steps}

The [!DNL Segmentation Service] UI provides a rich workflow allowing you to isolate marketable audiences from [!DNL Real-time Customer Profile] data.

To learn more about [!DNL Segmentation Service], please continue reading the documentation. To learn how to use the [!DNL Segmentation Service] API, please read the [[!DNL Segmentation Service] developer guide](../api/overview.md).
