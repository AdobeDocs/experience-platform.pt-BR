---
keywords: ativar destinos de solicitação de perfil; ativar dados; destinos de solicitação de perfil
title: Ativar dados do público-alvo para destinos de solicitação de perfil
type: Tutorial
description: Saiba como ativar os dados de público-alvo que você tem no Adobe Experience Platform, mapeando segmentos para destinos de solicitação de perfil.
exl-id: cd7132eb-4047-4faa-a224-47366846cb56
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Ativar dados do público-alvo para destinos de solicitação de perfil

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

## Visão geral {#overview}

Este artigo explica o fluxo de trabalho necessário para ativar dados de público-alvo em destinos de solicitação de perfil do Adobe Experience Platform. Exemplos de destinos de solicitação de perfil são [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [Personalização personalizada](../../destinations/catalog/personalization/custom-personalization.md) conexões.

## Pré-requisitos {#prerequisites}

Para ativar dados em destinos, você deve ter [conectado a um destino](./connect-destination.md). Se ainda não o fez, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

### Política de mesclagem de segmentos {#merge-policy}

Atualmente, os destinos de solicitação de perfil suportam apenas a ativação de segmentos que usam o [Política de Mesclagem Ativa na Borda](../../segmentation/ui/segment-builder.md#merge-policies) definido como padrão.

## Selecione o destino {#select-destination}

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione o **[!UICONTROL Catálogo]** guia .

   ![Guia Catálogo de destino](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecionar **[!UICONTROL Ativar segmentos]** no cartão correspondente ao destino onde você deseja ativar seus segmentos, conforme mostrado na imagem abaixo.

   ![Botões Ativar](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Selecione a conexão de destino que deseja usar para ativar seus segmentos e selecione **[!UICONTROL Próximo]**.

   ![Selecionar destino](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Mova para a próxima seção para [selecione seus segmentos](#select-segments).

## Selecione seus segmentos {#select-segments}

Use as caixas de seleção à esquerda dos nomes de segmentos para selecionar os segmentos que deseja ativar para o destino e, em seguida, selecione **[!UICONTROL Próximo]**.

![Selecionar segmentos](../assets/ui/activate-profile-request-destinations/select-segments.png)

## Agendar exportação de segmentos {#scheduling}

Por padrão, a variável [!UICONTROL Agendamento do segmento] mostra somente os segmentos recém-selecionados que você escolheu no fluxo de ativação atual.

![Novos segmentos](../assets/ui/activate-profile-request-destinations/new-segments.png)

Para ver todos os segmentos ativados para o seu destino, use a opção de filtragem e desative o **[!UICONTROL Mostrar somente novos segmentos]** filtro.

![Todos os segmentos](../assets/ui/activate-profile-request-destinations/all-segments.png)

No **[!UICONTROL Agendamento do segmento]** selecione cada segmento e use a **[!UICONTROL Data de início]** e **[!UICONTROL Data final]** seletores para configurar o intervalo de tempo para enviar dados ao seu destino.

![Agendamento do segmento](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Selecionar **[!UICONTROL Próximo]** para acessar o [!UICONTROL Revisão] página.

## Revisão {#review}

No **[!UICONTROL Revisão]** você pode ver um resumo da sua seleção. Selecionar **[!UICONTROL Cancelar]** para quebrar o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações, ou **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

>[!IMPORTANT]
>
>Nesta etapa, o Adobe Experience Platform verifica violações da política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de segmento até que você tenha resolvido a violação. Para obter informações sobre como resolver violações de política, consulte [Aplicação da política](../../rtcdp/privacy/data-governance-overview.md#enforcement) na seção de documentação de governança de dados .

![violação da política de dados](../assets/common/data-policy-violation.png)

Se nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

![Revisão](../assets/ui/activate-profile-request-destinations/review.png)

<!--

Commenting out this part since destination monitoring is not available currently for the Adobe Target and Custom Personalization destinations.

## Verify segment activation {#verify}

Check the [destination monitoring documentation](../../dataflows/ui/monitor-destinations.md) for detailed information on how to monitor the flow of data to your destinations.

-->