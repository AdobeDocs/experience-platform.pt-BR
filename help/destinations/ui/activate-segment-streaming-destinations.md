---
keywords: ativar destinos de transmissão de segmento, ativar destinos de transmissão de segmento, ativar dados
title: Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo
type: Tutorial
description: Saiba como ativar os dados do público-alvo no Adobe Experience Platform, mapeando segmentos para destinos de transmissão de segmentos.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: a6fe0f5a0c4f87ac265bf13cb8bba98252f147e0
workflow-type: tm+mt
source-wordcount: '832'
ht-degree: 0%

---

# Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]** e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

## Visão geral {#overview}

Este artigo explica o fluxo de trabalho necessário para ativar os dados do público-alvo nos destinos de transmissão do segmento do Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Para ativar dados em destinos, você deve ter [conectado a um destino](./connect-destination.md). Se ainda não o fez, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

## Selecione o destino {#select-destination}

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione o **[!UICONTROL Catálogo]** guia .

   ![Guia Catálogo de destino](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecionar **[!UICONTROL Ativar segmentos]** no cartão correspondente ao destino onde você deseja ativar seus segmentos, conforme mostrado na imagem abaixo.

   ![Botões Ativar](../assets/ui/activate-segment-streaming-destinations/activate-segments-button.png)

1. Selecione a conexão de destino que deseja usar para ativar seus segmentos e selecione **[!UICONTROL Próximo]**.

   ![Selecionar destino](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Mova para a próxima seção para [selecione seus segmentos](#select-segments).

## Selecione seus segmentos {#select-segments}

Use as caixas de seleção à esquerda dos nomes de segmentos para selecionar os segmentos que deseja ativar para o destino e, em seguida, selecione **[!UICONTROL Próximo]**.

![Selecionar segmentos](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Mapear atributos e identidades {#mapping}

>[!IMPORTANT]
>
>Essa etapa se aplica somente a alguns destinos de transmissão de segmento. Se o destino não tiver uma **[!UICONTROL Mapeamento]** etapa, pule para [Agendar exportação de segmentos](#scheduling).

Alguns destinos de transmissão de segmento exigem que você selecione atributos de origem ou namespaces de identidade para mapear como identidades de destino no destino.

1. No **[!UICONTROL Mapeamento]** página, selecione **[!UICONTROL Adicionar novo mapeamento]**.

   ![Adicionar novo mapeamento](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Selecione a seta à direita da **[!UICONTROL Campo de origem]** entrada.

   ![Selecionar campo de origem](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. No **[!UICONTROL Selecionar campo de origem]** use a **[!UICONTROL Selecionar atributos]** ou **[!UICONTROL Selecionar namespace de identidade]** opções para alternar entre as duas categorias de campos de origem disponíveis. Em [!DNL XDM] atributos do perfil e namespaces de identidade, selecione aqueles que deseja mapear para o destino e escolha **[!UICONTROL Selecionar]**.

   ![Página Selecionar campo de origem](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Selecione o botão à direita do **[!UICONTROL Campo de destino]** entrada.

   ![Selecionar campo de destino](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. No **[!UICONTROL Selecionar campo de destino]** selecione o namespace de identidade de destino para o qual deseja mapear o campo de origem e escolha **[!UICONTROL Selecionar]**.

   ![Página Selecionar campo de destino](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Para adicionar mais mapeamentos, repita as etapas de 1 a 5.

### Aplicar transformação {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Aplicar transformação"
>abstract="Marque essa opção ao usar campos de origem sem hash para que o Adobe Experience Platform os faça automaticamente com hash na ativação."
>additional-url="https://experienceleague.adobe.com/docs/experience-platform/destinations/ui/activate/activate-segment-streaming-destinations.html#apply-transformation" text="Saiba mais na documentação"

Quando você está mapeando atributos de origem sem hash para atributos de destino que o destino espera ter hash (por exemplo: `email_lc_sha256` ou `phone_sha256`), marque a opção **Aplicar transformação** para que o Adobe Experience Platform faça o hash automático dos atributos de origem na ativação.

![Mapeamento de identidade](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Agendar exportação de segmentos {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Data de término"
>abstract="A adição de uma data de término para a programação de segmentos não está disponível."
>additional-url="https://www.adobe.com/go/destinations-activate-segment-scheduling-en" text="Saiba mais na documentação"

Por padrão, a variável [!UICONTROL Agendamento do segmento] mostra somente os segmentos recém-selecionados que você escolheu no fluxo de ativação atual.

![Novos segmentos](../assets/ui/activate-segment-streaming-destinations/new-segments.png)

Para ver todos os segmentos ativados para o seu destino, use a opção de filtragem e desative o **[!UICONTROL Mostrar somente novos segmentos]** filtro.

![Todos os segmentos](../assets/ui/activate-segment-streaming-destinations/all-segments.png)

1. No **[!UICONTROL Agendamento do segmento]** selecione cada segmento e use a **[!UICONTROL Data de início]** e **[!UICONTROL Data final]** seletores para configurar o intervalo de tempo para enviar dados ao seu destino.

   ![Agendamento do segmento](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * Alguns destinos exigem que você selecione a variável **[!UICONTROL Origem do público]** para cada segmento, usando o menu suspenso abaixo dos seletores de calendário. Se o destino não incluir esse seletor, pule esta etapa.

      ![ID de mapeamento](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Alguns destinos exigem o mapeamento manual [!DNL Platform] segmentos para sua contrapartida no destino do target. Para fazer isso, selecione cada segmento e insira a ID de segmento correspondente na plataforma de destino na **[!UICONTROL ID de mapeamento]** campo. Se o destino não incluir este campo, pule esta etapa.

      ![ID de mapeamento](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Alguns destinos exigem que você insira um **[!UICONTROL ID do aplicativo]** ao ativar [!DNL IDFA] ou [!DNL GAID] segmentos. Se o destino não incluir este campo, pule esta etapa.

      ![ID do aplicativo](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Selecionar **[!UICONTROL Próximo]** para acessar o [!UICONTROL Revisão] página.

## Revisão {#review}

No **[!UICONTROL Revisão]** você pode ver um resumo da sua seleção. Selecionar **[!UICONTROL Cancelar]** para quebrar o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações, ou **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

>[!IMPORTANT]
>
>Nesta etapa, o Adobe Experience Platform verifica violações da política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de segmento até que você tenha resolvido a violação. Para obter informações sobre como resolver violações de política, consulte [Aplicação da política](../../rtcdp/privacy/data-governance-overview.md#enforcement) na seção de documentação de governança de dados .

![violação da política de dados](../assets/common/data-policy-violation.png)

Se nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

![Revisão](../assets/ui/activate-segment-streaming-destinations/review.png)

## Verificar ativação de segmento {#verify}

Verifique a [documentação de monitoramento de destino](../../dataflows/ui/monitor-destinations.md) para obter informações detalhadas sobre como monitorar o fluxo de dados para seus destinos.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
