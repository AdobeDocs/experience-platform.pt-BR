---
keywords: ativar destinos de solicitação de perfil; ativar dados; destinos de solicitação de perfil
title: Ativar dados do público-alvo para destinos de solicitação de perfil
type: Tutorial
description: Saiba como ativar os dados de público-alvo que você tem no Adobe Experience Platform, mapeando segmentos para destinos de solicitação de perfil.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: f771cf0c9ea692ad02cf987608b3710772712d54
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# Ativar dados do público-alvo para destinos de solicitação de perfil

>[!IMPORTANT]
> 
> * Para ativar os dados e ativar o [etapa de mapeamento](#mapping) do fluxo de trabalho, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
> * Para ativar dados sem passar pela variável [etapa de mapeamento](#mapping) do fluxo de trabalho, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar segmento sem mapeamento]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
> 
> Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

## Visão geral {#overview}

Este artigo explica o fluxo de trabalho necessário para ativar dados de público-alvo em destinos de solicitação de perfil do Adobe Experience Platform. Quando usado em conjunto com [segmentação de borda](../../segmentation/ui/edge-segmentation.md), esses destinos permitem casos de uso de personalização da mesma página e da próxima página nas propriedades da Web e dispositivos móveis. Leia mais sobre [ativação de casos de uso de personalização de mesma página e próxima página](/help/destinations/ui/configure-personalization-destinations.md).

Exemplos de destinos de solicitação de perfil são [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [Personalização personalizada](../../destinations/catalog/personalization/custom-personalization.md) conexões.

## Pré-requisitos {#prerequisites}

Para ativar dados em destinos, você deve ter [conectado a um destino](./connect-destination.md). Se ainda não o fez, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos de personalização compatíveis e configure o destino que deseja usar.

### Política de mesclagem de segmentos {#merge-policy}

Atualmente, os destinos de solicitação de perfil suportam apenas a ativação de segmentos que usam o [Política de Mesclagem Ativa na Borda](../../segmentation/ui/segment-builder.md#merge-policies) definido como padrão.

## Selecione o destino {#select-destination}

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione o **[!UICONTROL Catálogo]** guia .

   ![Guia Catálogo de destino](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecionar **[!UICONTROL Ativar segmentos]** no cartão correspondente ao destino de personalização, onde você deseja ativar seus segmentos, conforme mostrado na imagem abaixo.

   ![Botões Ativar](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Selecione a conexão de destino que deseja usar para ativar seus segmentos e selecione **[!UICONTROL Próximo]**.

   ![Selecionar destino](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Mova para a próxima seção para [selecione seus segmentos](#select-segments).

## Selecione seus segmentos {#select-segments}

Use as caixas de seleção à esquerda dos nomes de segmentos para selecionar os segmentos que deseja ativar para o destino e, em seguida, selecione **[!UICONTROL Próximo]**.

![Selecionar segmentos](../assets/ui/activate-profile-request-destinations/select-segments.png)

## (Beta) Mapear atributos {#map-attributes}

>[!IMPORTANT]
>
>A etapa de mapeamento, que permite a personalização baseada em atributo para [Adobe Target](/help/destinations/catalog/personalization/adobe-target-connection.md) e [destinos de personalização genérica](/help/destinations/catalog/personalization/custom-personalization.md)O está atualmente na versão beta e sua organização pode ainda não ter acesso a ele. Esta documentação está sujeita a alterações.

Selecione os atributos com base nos quais você deseja ativar os casos de uso de personalização para seus usuários. Isso significa que, se o valor de um atributo for alterado ou se um atributo for adicionado a um perfil, esse perfil se tornará um membro do segmento e será ativado para o destino de personalização.

A adição de atributos é opcional e você ainda pode prosseguir para a próxima etapa e ativar a personalização da mesma página e da próxima página sem selecionar atributos. Se você não adicionar atributos nesta etapa, a personalização ainda ocorrerá com base na associação de segmentos e nas qualificações do mapa de identidade para perfis.

![Imagem mostrando a etapa de mapeamento com um atributo selecionado](../assets/ui/activate-profile-request-destinations/mapping-step.png)

### Selecionar atributos de origem {#select-source-attributes}

Para adicionar atributos de origem, selecione o **[!UICONTROL Adicionar novo campo]** controlo da **[!UICONTROL Campo de origem]** e pesquise ou navegue até o campo de atributo XDM desejado, conforme mostrado abaixo.

![Gravação de tela mostrando como selecionar um atributo de destino na etapa de mapeamento](../assets/ui/activate-profile-request-destinations/mapping-step-select-attribute.gif)

### Selecionar atributos de destino {#select-target-attributes}

>[!NOTE]
>
>Alguns destinos exigem que você selecione apenas os atributos de origem, enquanto outros exigem tanto os atributos de origem quanto os de destino.
>
>Atualmente, o [Adobe Target V2](../catalog/personalization/adobe-target-connection.md) o destino requer apenas atributos de origem, enquanto [Personalização personalizada com atributos](../catalog/personalization/custom-personalization.md) O requer atributos de origem e de destino.

Para adicionar atributos de destino, selecione o **[!UICONTROL Adicionar novo campo]** controlo da **[!UICONTROL Campo de destino]** e digite o nome do atributo personalizado para o qual deseja mapear o atributo de origem.

![Gravação de tela mostrando como selecionar um atributo XDM na etapa de mapeamento](../assets/ui/activate-profile-request-destinations/mapping-step-select-target-attribute.gif)

## Agendar exportação de segmentos {#scheduling}

Por padrão, a variável [!UICONTROL Agendamento do segmento] mostra somente os segmentos recém-selecionados que você escolheu no fluxo de ativação atual.

![Novos segmentos](../assets/ui/activate-profile-request-destinations/new-segments.png)

Para ver todos os segmentos ativados para o seu destino, use a opção de filtragem e desative o **[!UICONTROL Mostrar somente novos segmentos]** filtro.

![Todos os segmentos](../assets/ui/activate-profile-request-destinations/all-segments.png)

No **[!UICONTROL Agendamento do segmento]** selecione cada segmento e use a **[!UICONTROL Data de início]** e **[!UICONTROL Data final]** seletores para configurar o intervalo de tempo para enviar dados ao seu destino.

![Agendamento do segmento](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Selecionar **[!UICONTROL Próximo]** para acessar o [!UICONTROL Revisão] página.

## Consulte a seção {#review}

No **[!UICONTROL Revisão]** você pode ver um resumo da sua seleção. Selecionar **[!UICONTROL Cancelar]** para quebrar o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações, ou **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

![Resumo da seleção na etapa de revisão.](../assets/ui/activate-profile-request-destinations/review.png)

### Avaliação da política de consentimento {#consent-policy-evaluation}

Se sua organização comprou **Blindagem do Adobe Healthcare** ou **Privacidade e proteção de segurança do Adobe**, selecione **[!UICONTROL Exibir políticas de consentimento aplicáveis]** para ver quais políticas de consentimento são aplicadas e quantos perfis são incluídos na ativação como resultado delas. Leia sobre [avaliação da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obter mais informações.

### Verificações da política de uso de dados {#data-usage-policy-checks}

No **[!UICONTROL Revisão]** , o Experience Platform também verifica se há violações da política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de segmento até que você tenha resolvido a violação. Para obter informações sobre como resolver violações de política, leia sobre [violações da política de uso de dados](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) na seção de documentação de governança de dados .

![violação da política de dados](../assets/common/data-policy-violation.png)

### Filtrar segmentos {#filter-segments}

Além disso, nesta etapa, você pode usar os filtros disponíveis na página para exibir apenas os segmentos cujo agendamento ou mapeamento foi atualizado como parte desse fluxo de trabalho. Também é possível alternar quais colunas de tabela você deseja visualizar.

![Gravação de tela mostrando os filtros de segmento disponíveis na etapa de revisão.](/help/destinations/assets/ui/activate-profile-request-destinations/filter-segments-review-step.gif)

Se estiver satisfeito com sua seleção e nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->