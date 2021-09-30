---
keywords: ativar destinos de solicitação de perfil; ativar dados; destinos de solicitação de perfil
title: Ativar dados do público-alvo para destinos de solicitação de perfil (Beta)
type: Tutorial
seo-title: Activate audience data to profile request destinations
description: Saiba como ativar os dados de público-alvo que você tem no Adobe Experience Platform, mapeando segmentos para destinos de solicitação de perfil.
seo-description: Learn how to activate the audience data you have in Adobe Experience Platform by mapping segments to profile request destinations.
source-git-commit: 0635828cf3f637e67d2cabda860ca452e61892d4
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 0%

---

# Ativar dados do público-alvo para destinos de solicitação de perfil (Beta)

## Visão geral {#overview}

>[!IMPORTANT]
>
>Os destinos de solicitação de perfil no Adobe Experience Platform estão atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

Este artigo explica o fluxo de trabalho necessário para ativar dados de público-alvo em destinos de solicitação de perfil do Adobe Experience Platform. Exemplos de destinos de solicitação de perfil são as conexões [Adobe Target](../../destinations/catalog/personalization/adobe-target-connection.md) e [Personalização personalizada](../../destinations/catalog/personalization/custom-personalization.md) .

## Pré-requisitos {#prerequisites}

Para ativar dados em destinos, você deve ter [conectado com êxito a um destino](./connect-destination.md). Se ainda não tiver feito isso, vá para o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

### Política de mesclagem de segmentos {#merge-policy}

Atualmente, os destinos de solicitação de perfil oferecem suporte apenas à ativação de segmentos que usam a [política de mesclagem padrão](../../segmentation/ui/segment-builder.md#merge-policies).

## Selecione o destino {#select-destination}

1. Vá para **[!UICONTROL Connections > Destinations]** e selecione a guia **[!UICONTROL Catalog]**.

   ![Guia Catálogo de destino](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecione **[!UICONTROL Ativar segmentos]** no cartão correspondente ao destino onde deseja ativar seus segmentos, conforme mostrado na imagem abaixo.

   ![Botões Ativar](../assets/ui/activate-profile-request-destinations/activate-segments-button.png)

1. Selecione a conexão de destino que deseja usar para ativar seus segmentos e selecione **[!UICONTROL Next]**.

   ![Selecionar destino](../assets/ui/activate-profile-request-destinations/select-destination.png)

1. Mova para a próxima seção para [selecionar seus segmentos](#select-segments).

## Selecione seus segmentos {#select-segments}

Use as caixas de seleção à esquerda dos nomes de segmentos para selecionar os segmentos que deseja ativar para o destino e selecione **[!UICONTROL Next]**.

![Selecionar segmentos](../assets/ui/activate-profile-request-destinations/select-segments.png)

## Agendar exportação de segmentos {#scheduling}

Por padrão, a página [!UICONTROL Segment schedule] mostra apenas os segmentos recém-selecionados que você escolheu no fluxo de ativação atual.

![Novos segmentos](../assets/ui/activate-profile-request-destinations/new-segments.png)

Para visualizar todos os segmentos que estão sendo ativados no seu destino, use a opção de filtragem e desative o filtro **[!UICONTROL Mostrar somente novos segmentos]**.

![Todos os segmentos](../assets/ui/activate-profile-request-destinations/all-segments.png)

Na página **[!UICONTROL Segment schedule]**, selecione cada segmento e use os seletores **[!UICONTROL Start date]** e **[!UICONTROL End date]** para configurar o intervalo de tempo para enviar dados ao seu destino.

![Agendamento do segmento](../assets/ui/activate-profile-request-destinations/segment-schedule.png)

Selecione **[!UICONTROL Next]** para ir para a página [!UICONTROL Review].

## Revisão {#review}

Na página **[!UICONTROL Revisar]**, você pode ver um resumo da sua seleção. Selecione **[!UICONTROL Cancelar]** para quebrar o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar sua seleção e começar a enviar dados para o destino.

>[!IMPORTANT]
>
>Nesta etapa, o Adobe Experience Platform verifica violações da política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de segmento até que você tenha resolvido a violação. Para obter informações sobre como resolver violações de política, consulte [Aplicação de política](../../rtcdp/privacy/data-governance-overview.md#enforcement) na seção Documentação de governança de dados.

![violação da política de dados](../assets/common/data-policy-violation.png)

Se nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Finish]** para confirmar a seleção e iniciar o envio de dados para o destino.

![Revisão](../assets/ui/activate-profile-request-destinations/review.png)

## Verificar ativação de segmento {#verify}

Verifique a [documentação de monitoramento de destino](../../dataflows/ui/monitor-destinations.md) para obter informações detalhadas sobre como monitorar o fluxo de dados para seus destinos.