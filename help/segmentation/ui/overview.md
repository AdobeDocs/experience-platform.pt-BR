---
keywords: Experience Platform;home;popular topics;Segmentation Service;segmentation;segmentation service;user guide;ui guide;segmentation ui guide;segment builder;Segment builder;
solution: Experience Platform
title: Guia do usuário do Serviço de segmentação
topic: ui guide
translation-type: tm+mt
source-git-commit: 0f3a4ba6ad96d2226ae5094fa8b5073152df90f7
workflow-type: tm+mt
source-wordcount: '1359'
ht-degree: 0%

---


# [!UICONTROL Guia do usuário do Serviço] de segmentação

[!DNL Adobe Experience Platform Segmentation Service] fornece uma interface de usuário para criar e gerenciar definições de segmentos.

## Introdução

Trabalhar com definições de segmento requer uma compreensão dos vários [!DNL Experience Platform] serviços envolvidos com a segmentação. Antes de ler este guia do usuário, consulte a documentação dos seguintes serviços:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] permite dividir os dados armazenados em [!DNL Experience Platform] que se relacionam a indivíduos (como clientes, prospectos, usuários ou organizações) em grupos menores.
- [[!DNL Perfil do cliente em tempo real]](../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): Permite a criação de perfis do cliente, fazendo a ponte entre identidades de diferentes fontes de dados que estão sendo assimiladas [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Platform] organiza os dados de experiência do cliente.

Também é importante saber dois termos chave que são usados por meio desse documento e entender a diferença entre eles:
- **Definição** do segmento: O conjunto de regras usado para descrever as principais características ou comportamentos de uma audiência de público alvo.
- **Audiência**: O conjunto resultante de perfis que atendem aos critérios de uma definição de segmento.

## Visão geral

Na [[!DNL Experience Platform] interface do usuário](http://platform.adobe.com/), selecione **[!UICONTROL Segmentos]** na navegação à esquerda para abrir a guia **[!UICONTROL Visão geral]** . Esta guia fornece links para a documentação e vídeos para ajudá-lo a entender e começar a trabalhar com segmentos.

![](../images/ui/overview/segment-overview.png)

## Procurar

Selecione a guia **[!UICONTROL Procurar]** para ver uma lista de todas as definições de segmento para sua Organização IMS.

![](../images/ui/overview/segment-browse-all.png)

Essa visualização lista informações sobre a definição do segmento, incluindo o método de avaliação, a data de criação e a data da última modificação.

O método de avaliação pode ser streaming ou lote. Segmentos de transmissão são constantemente avaliados à medida que os dados entram no sistema. Os segmentos de lote são avaliados de acordo com uma programação definida.

![](../images/ui/overview/segment-browse-segments.png)

Na parte superior da página estão as opções para adicionar todos os segmentos a uma programação e para criar um novo segmento.

Alternar **[!UICONTROL Adicionar todos os segmentos para agendar]** permitirá a segmentação programada. Mais informações sobre a segmentação programada podem ser encontradas na seção de segmentação [programada deste guia](#scheduled-segmentation)do usuário.

Selecionar **[!UICONTROL Criar segmento]** levará você ao Construtor de segmentos. Para saber mais sobre como criar segmentos, leia a seção sobre como [criar um segmento no guia](#create-segment)do usuário.

![](../images/ui/overview/segment-browse-top.png)

A barra lateral direita contém informações sobre todos os segmentos dentro da organização IMS, listando o número total de segmentos, a última data de avaliação, a próxima data de avaliação, bem como um detalhamento dos segmentos por método de avaliação.

![](../images/ui/overview/segment-browse-segment-info.png)

A seleção da linha de definição do segmento fornece um resumo da definição do segmento, incluindo opções para editar ou excluir o segmento, a audiência qualificada para o segmento, o tamanho total da audiência, além do nome, descrição, método de avaliação, data de criação e data da última modificação do segmento.

![](../images/ui/overview/segment-browse-details.png)

## Detalhes da definição do segmento {#segment-details}

Para ver mais detalhes sobre uma definição de segmento específica, selecione o nome de um segmento na guia **[!UICONTROL Procurar]** .

A página de detalhes do segmento é exibida. Na parte superior, há um resumo da definição do segmento, informações sobre o tamanho da audiência qualificada, bem como os destinos para os quais o segmento é ativado.

![](../images/ui/overview/segment-details-summary.png)

### Resumo do segmento

A seção de resumo **[!UICONTROL do]** segmento fornece informações como ID, nome, descrição e detalhes dos atributos.

Além disso, você tem a opção de editar o segmento. Selecionar **[!UICONTROL Editar segmento]** o levará ao [!DNL Segment Builder]. Para obter informações mais detalhadas sobre como usar a [!DNL Segment Builder] área de trabalho, leia o guia [[!DNL Segment Builder] do](./segment-builder.md)usuário.

### Audiência total no segmento

A audiência **[!UICONTROL total na seção do segmento]** mostra o número total de perfis que se qualificam para o segmento.

As estimativas são geradas usando um tamanho de amostra dos dados de amostra desse dia. Se houver menos de 1 milhão de entidades em sua loja de perfis, o conjunto de dados completo será usado; para entre 1 e 20 milhões de entidades, são utilizadas 1 milhão de entidades; e para mais de 20 milhões de entidades, são utilizados 5% do total de entidades. Mais informações sobre a geração de estimativas de segmentos podem ser encontradas na seção [de geração de](../tutorials/create-a-segment.md#estimate-and-preview-an-audience) estimativas do tutorial de criação de segmentos.

### Destinos ativados

A seção Destinos **** ativados mostra os destinos para os quais esse segmento está ativado.

>[!NOTE]
>
> Os destinos são um recurso disponível com [!DNL Real-time Customer Data Platform]e permitem exportar dados para plataformas externas. Para obter mais informações sobre os destinos, leia a visão geral [dos](../../rtcdp/destinations/destinations-overview.md)destinos. Para saber como ativar um segmento em um destino, leia o [guia sobre como ativar segmentos em um destino](../../rtcdp/destinations/activate-destinations.md).

### Amostras de perfil

Abaixo está uma amostra de perfis que se qualificam para o segmento, detalhando as informações, incluindo a [!DNL Profile] ID, o nome, o sobrenome e o email pessoal.

A forma como a amostragem de dados é acionada depende do método de ingestão.

Para a ingestão em lote, o armazenamento de perfis é verificado automaticamente a cada quinze minutos para ver se um novo lote foi ingerido com êxito desde a execução do último trabalho de amostragem. Se for esse o caso, a loja de perfis é analisada posteriormente para verificar se houve pelo menos uma mudança de 5% no número de registros. Se essas condições forem atendidas, um novo trabalho de amostragem será acionado.

Para a ingestão em streaming, a loja de perfis é automaticamente verificada a cada hora para ver se houve pelo menos uma mudança de 5% no número de registros. Se essa condição for cumprida, um novo trabalho de amostragem será acionado.

O tamanho da amostra da verificação depende do número geral de entidades na loja de perfis. Esses tamanhos de amostra são representados na tabela a seguir:

| Entidades na loja de perfis | Tamanho da amostra |
| ------------------------- | ----------- |
| Menos de 1 milhão | Conjunto completo de dados |
| 1 a 20 milhões | 1 milhão |
| Mais de 20 milhões | 5% do total |

Para obter informações mais detalhadas sobre cada um, [!DNL Profile] selecione a [!DNL Profile] ID. Para saber mais sobre os detalhes de um perfil, leia o guia [[!DNL Real-time Customer Profile] do](../../profile/ui/user-guide.md#profile-detail)usuário.

![](../images/ui/overview/segment-details-profiles.png)

## Criação de um segmento {#create-segment}

Selecionar **[!UICONTROL Criar segmento]** no canto superior direito abre a área de [!DNL Segment Builder] trabalho, onde você pode começar a criar uma definição de segmento.

![](../images/ui/overview/segment-browse-create.png)

### [!DNL Segment Builder] espaço de trabalho

[!DNL Segment Builder] fornece uma área de trabalho avançada que permite interagir com elementos [!DNL Profile] de dados. A área de trabalho fornece controles intuitivos para criar e editar regras, como os blocos de arrastar e soltar usados para representar propriedades de dados.

Para obter informações mais detalhadas sobre como usar a [!DNL Segment Builder] área de trabalho, leia o guia [[!DNL Segment Builder] do](./segment-builder.md)usuário.

![](../images/ui/overview/segment-builder.png)

## Segmentação programada {#scheduled-segmentation}

Depois que as definições de segmento forem criadas, você poderá avaliá-las por meio de uma avaliação sob demanda ou programada (contínua). Avaliação significa mover [!DNL Real-time Customer Profile] dados através de definições de segmento para produzir audiências correspondentes. Depois de criadas, as audiências são salvas e armazenadas para que possam ser exportadas usando [!DNL Experience Platform] APIs.

A avaliação sob demanda envolve o uso da API para realizar a avaliação e criar audiências conforme necessário, enquanto a avaliação programada (também conhecida como &quot;segmentação programada&quot;) permite criar um agendamento recorrente para avaliar definições de segmentos em um horário específico (no máximo, uma vez por dia).

### Ativar a segmentação programada {#enable-scheduled-segmentation}

A ativação das definições de segmento para avaliação programada pode ser feita usando a interface do usuário ou a API. Na interface do usuário, volte para a guia **[!UICONTROL Procurar]** em **[!UICONTROL Segmentos]** e alterne para **[!UICONTROL Adicionar todos os segmentos para agendar]**. Isso fará com que todos os segmentos sejam avaliados com base na programação definida pela sua organização.

>[!NOTE]
>
>A avaliação agendada pode ser ativada para caixas de proteção com um máximo de cinco (5) políticas de mesclagem para [!DNL XDM Individual Profile]. Se sua organização tiver mais de cinco políticas de mesclagem para [!DNL XDM Individual Profile] dentro de um único ambiente de sandbox, você não poderá usar a avaliação agendada.

No momento, os agendamentos só podem ser criados usando a API. Para obter etapas detalhadas sobre como criar, editar e trabalhar com programações usando a API, siga o tutorial para avaliar e acessar os resultados do segmento, especificamente a seção sobre avaliação [programada usando a API](../tutorials/evaluate-a-segment.md#scheduled-evaluation).

![](../images/ui/overview/segment-browse-scheduled.png)

## Segmentação em streaming {#streaming-segmentation}

A segmentação contínua é a capacidade de segmentação [!DNL Platform] em tempo quase real, enquanto se concentra na riqueza de dados. Com a segmentação de fluxo contínuo, a qualificação de segmentos acontece à medida que os dados chegam, o que diminui a necessidade de programar e executar tarefas de segmentação. [!DNL Platform]

Mais informações sobre a segmentação de streaming podem ser encontradas no guia [do usuário da segmentação de](./streaming-segmentation.md)streaming.

>[!NOTE]
>
>Para que a segmentação de fluxo funcione, será necessário ativar a segmentação programada para a organização. Para obter detalhes sobre como ativar a segmentação programada, consulte [a seção de segmentação de streaming neste guia](#scheduled-segmentation)do usuário.

## Violações políticas

>[!NOTE]
>
>As violações de política se aplicam somente se você estiver criando um segmento que foi atribuído a um destino.

Quando terminar de criar seu segmento, ele será analisado pelo Adobe Experience Platform Data Governance para garantir que não haja violações de política no segmento. Consulte a [[!DNL Data Governance] visão geral](../../data-governance/home.md) para obter mais informações.

![](../images/ui/overview/segment-dule-policy-violations.png)

## Próximos passos e recursos adicionais {#next-steps}

A [!DNL Segmentation Service] interface do usuário fornece um fluxo de trabalho avançado que permite isolar audiências comercializáveis dos [!DNL Real-time Customer Profile] dados.

Para saber mais sobre [!DNL Segmentation Service], continue lendo a documentação. Para saber como usar a [!DNL Segmentation Service] API, leia o guia [[!DNL Segmentation Service] do](../api/overview.md)desenvolvedor.
