---
solution: Experience Platform
title: Guia da interface do usuário do Serviço de segmentação
description: Saiba como criar e gerenciar públicos e definições de segmento na interface do usuário do Adobe Experience Platform.
exl-id: 0a2e8d82-281a-4c67-b25b-08b7a1466300
source-git-commit: acfe91144175e136955ffd9f0cdae2c351217c16
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---

# Guia da interface do usuário do serviço de segmentação

[!DNL Adobe Experience Platform Segmentation Service] O fornece uma interface para criar e gerenciar públicos-alvo e definições de segmento.

## Introdução

Trabalhar com públicos-alvo e definições de segmento requer uma compreensão dos vários [!DNL Experience Platform] serviços envolvidos com a segmentação. Antes de ler este guia do usuário, consulte a documentação dos seguintes serviços:

- [[!DNL Segmentation Service]](../home.md): [!DNL Segmentation Service] permite segmentar dados armazenados no [!DNL Experience Platform] que se relaciona a indivíduos (como clientes, clientes potenciais, usuários ou organizações) em grupos menores.
- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Identity Service]](../../identity-service/home.md): permite a criação de perfis de clientes, unindo identidades de diferentes fontes de dados que estão sendo assimiladas na [!DNL Platform].
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente. Para melhor usar a segmentação, verifique se seus dados são assimilados como perfis e eventos de acordo com a [práticas recomendadas para modelagem de dados](../../xdm/schema/best-practices.md).

Você também deve compreender os termos principais a seguir que são usados neste documento e compreender a diferença entre eles:

- **Público**: uma coleção de pessoas que compartilham comportamentos e/ou características semelhantes. Essa coleção de pessoas pode ser gerada pelo Adobe Experience Platform usando definições de segmento (público-alvo gerado pela Platform), composição de público-alvo ou de fontes externas, como uploads personalizados (público-alvo gerado externamente).
- **Definição de segmento**: as regras que o Adobe Experience Platform usa para descrever as principais características ou comportamento de um público-alvo.
- **Segmento**: o ato de separar perfis em públicos.

## Visão geral

Na interface do Experience Platform, selecione **[!UICONTROL Públicos-alvo]** na navegação à esquerda, para abrir a **[!UICONTROL Visão geral]** guia exibindo o [!UICONTROL Públicos-alvo] painel.

>[!NOTE]
>
>Se sua organização for nova na Plataforma e ainda não tiver conjuntos de dados de Perfil ativos ou políticas de mesclagem criadas, a variável [!UICONTROL Públicos-alvo] o painel não está visível. Em vez disso, a variável [!UICONTROL Visão geral] A guia exibe links e a documentação para ajudar você a começar a usar os públicos-alvo.

### [!UICONTROL Públicos-alvo] painel {#segments-dashboard}

A variável **[!UICONTROL Públicos-alvo]** O painel descreve as principais métricas relacionadas aos dados de público-alvo de sua organização.

Para saber mais, visite o [guia do painel de públicos-alvo](../../dashboards/guides/audiences.md).

![O painel do público-alvo é exibido. Ele mostra vários widgets, incluindo o tamanho do público, perfis por identidade, sobreposição de identidade e a tendência de alteração do tamanho do público.](../../dashboards/images/segments/dashboard-overview.png)

## Navegar {#browse}

Selecione o **[!UICONTROL Procurar]** para ver o Portal de público-alvo. O Portal de público-alvo fornece uma lista de todos os públicos-alvo que pertencem à sua organização e sandbox, e inclui detalhes como contagem de perfis, origem, data de criação, data da última modificação, tags e detalhamento.

Além disso, o Audience Portal permite criar novos públicos-alvo usando o Construtor de segmentos ou a Composição de público-alvo, bem como importar públicos gerados externamente para a Platform.

Para obter mais informações sobre o Audience Portal, leia o [Visão geral do portal de público](./audience-portal.md).

## Composições {#compositions}

Selecione o **[!UICONTROL Composições]** para ver uma lista de todos os públicos-alvo gerados pela Composição de público-alvo para sua organização.

![Uma lista de públicos-alvo criada na Composição de público-alvo para sua organização.](../images/ui/overview/compositions.png)

Por padrão, essa exibição lista informações sobre os públicos-alvo, incluindo nome, status, data de criação, criado por, data da última atualização e atualizado pela última vez por.

Ao lado de cada público há um ícone de reticências. Selecionar essa opção exibe uma lista de ações rápidas disponíveis para o público-alvo.

| Ação | Descrição |
| ------ | ----------- |
| Duplicar | Copia o público selecionado. |
| Gerenciar acesso | Gerencia os rótulos de acesso que pertencem ao público. Para obter mais informações sobre rótulos de acesso, leia a documentação em [gerenciamento de rótulos](../../access-control/abac/ui/labels.md). |
| Excluir | Exclui o público selecionado. Públicos-alvo usados em destinos downstream ou que são dependentes de outros públicos-alvo **não é possível** ser excluídos. Para obter mais informações sobre exclusão de público-alvo, leia a [perguntas frequentes sobre segmentação](../faq.md#lifecycle-states). |

É possível selecionar a variável ![Personalizar tabela](../images/ui/overview/customize-table.png) ícone para alterar os campos exibidos.

![O botão personalizar tabela é realçado. Selecionar esse botão permite personalizar os campos exibidos na página Composições de públicos-alvo.](../images/ui/overview/compositions-select-customize-table.png)

Um popover é exibido, listando todos os campos que podem ser exibidos dentro da tabela.

![Os atributos que podem ser exibidos para a seção Composição.](../images/ui/overview/compositions-customize-table.png)

| Campo | Descrição |
| ----- | ----------- | 
| [!UICONTROL Nome] | O nome do público. |
| [!UICONTROL Status] | O status do público. Os valores possíveis para esse campo incluem `Draft`, `Inactive`, e `Published`. |
| [!UICONTROL Criado] | A hora e a data em que o público-alvo foi criado. |
| [!UICONTROL Criado por] | O nome da pessoa que criou o público-alvo. |
| [!UICONTROL Atualizado] | A hora e a data em que o público-alvo foi atualizado pela última vez. |
| [!UICONTROL Atualizado por] | O nome da última pessoa que atualizou o público. |

Para ver como o público é composto, selecione o nome de um público na [!UICONTROL Públicos-alvo] guia.

A página Composição de público-alvo é exibida com os blocos fundamentais que compõem seu público-alvo. Para obter mais detalhes sobre como usar a Composição de público-alvo, leia a [Guia da interface do usuário da Composição de público-alvo](./audience-composition.md).

## Segmentação de transmissão {#streaming-segmentation}

A segmentação de transmissão é a capacidade de fazer a segmentação em [!DNL Platform] em tempo quase real, concentrando-se na riqueza de dados. Com a segmentação por transmissão, a qualificação para segmentação agora acontece à medida que os dados chegam ao [!DNL Platform], reduzindo a necessidade de agendar e executar trabalhos de segmentação.

Mais informações sobre a segmentação por transmissão podem ser encontradas na [guia do usuário de segmentação por transmissão](./streaming-segmentation.md).

>[!NOTE]
>
>Para que a segmentação por transmissão funcione, é necessário habilitar a segmentação agendada para a organização. Para obter detalhes sobre como ativar a segmentação programada, consulte [a seção segmentação por transmissão neste guia do usuário](#scheduled-segmentation).

## Segmentação de borda {#edge-segmentation}

A segmentação do Edge é a capacidade de avaliar públicos-alvo na Platform instantaneamente na borda, permitindo casos de uso de personalização da mesma página e da próxima página.

Mais informações sobre segmentação de borda podem ser encontradas no [guia da interface de segmentação de borda](./edge-segmentation.md)

## Violações de política

>[!NOTE]
>
>As violações de política só se aplicam se você estiver criando um público atribuído a um destino.

Quando terminar de criar o público-alvo, ele será analisado pela Governança de dados da Adobe Experience Platform para garantir que não haja violações de política no público-alvo. Consulte a [Visão geral da governança de dados](../../data-governance/home.md) para obter mais informações.

![As violações de política para o público-alvo são exibidas.](../images/ui/overview/audience-dule-policy-violations.png)

## Próximas etapas e recursos adicionais {#next-steps}

A variável [!DNL Segmentation Service] A interface do usuário fornece um fluxo de trabalho avançado que permite criar públicos comercializáveis a partir do [!DNL Real-Time Customer Profile] dados.

Para saber mais sobre [!DNL Segmentation Service], continue lendo a documentação. Para saber como usar o [!DNL Segmentation Service] API, leia as [[!DNL Segmentation Service] guia do desenvolvedor](../api/overview.md).
