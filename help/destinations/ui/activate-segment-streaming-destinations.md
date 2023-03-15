---
keywords: ativar destinos de transmissão de segmento;ativar destinos de transmissão de segmento;ativar dados
title: Ativar dados do público-alvo para destinos de exportação de segmento de transmissão
type: Tutorial
description: Saiba como ativar os dados de público-alvo no Adobe Experience Platform mapeando segmentos para destinos de transmissão de segmento.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 9bde403338187409892d76de68805535de03d59f
workflow-type: tm+mt
source-wordcount: '935'
ht-degree: 0%

---

# Ativar dados do público-alvo para destinos de exportação de segmento de transmissão

>[!IMPORTANT]
> 
>Para ativar os dados, é necessário **[!UICONTROL Gerenciar destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions). Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

## Visão geral {#overview}

Este artigo explica o fluxo de trabalho necessário para ativar dados de público-alvo em destinos de transmissão de segmento do Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Para ativar dados para destinos, você deve ter o [conectado a um destino](./connect-destination.md). Se ainda não tiver feito isso, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

## Selecione seu destino {#select-destination}

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione a variável **[!UICONTROL Catálogo]** guia.

   ![Guia Catálogo de destino](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecionar **[!UICONTROL Ativar segmentos]** no cartão correspondente ao destino em que deseja ativar os segmentos, conforme mostrado na imagem abaixo.

   ![Ativar botões](../assets/ui/activate-segment-streaming-destinations/activate-segments-button.png)

1. Selecione a conexão de destino que deseja usar para ativar seus segmentos e selecione **[!UICONTROL Próxima]**.

   ![Selecionar destino](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Mover para a próxima seção para [selecionar os segmentos](#select-segments).

## Selecionar seus segmentos {#select-segments}

Use as caixas de seleção à esquerda dos nomes de segmento para selecionar os segmentos que você deseja ativar para o destino e, em seguida, selecione **[!UICONTROL Próxima]**.

![Selecionar segmentos](../assets/ui/activate-segment-streaming-destinations/select-segments.png)

## Mapear atributos e identidades {#mapping}

>[!IMPORTANT]
>
>Essa etapa se aplica somente a alguns destinos de streaming de segmento. Se o seu destino não tiver um **[!UICONTROL Mapeamento]** etapa, saltar para [Agendar exportação de segmento](#scheduling).

Alguns destinos de transmissão de segmento exigem que você selecione atributos de origem ou namespaces de identidade para mapear como identidades de destino no destino.

1. No **[!UICONTROL Mapeamento]** selecione **[!UICONTROL Adicionar novo mapeamento]**.

   ![Adicionar novo mapeamento](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Selecione a seta à direita da **[!UICONTROL Campo de origem]** entrada.

   ![Selecionar campo de origem](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. No **[!UICONTROL Selecionar campo de origem]** , use o **[!UICONTROL Selecionar atributos]** ou o **[!UICONTROL Selecionar namespace de identidade]** opções para alternar entre as duas categorias de campos de origem disponíveis. No disponível [!DNL XDM] atributos de perfil e namespaces de identidade, selecione aqueles que deseja mapear para o destino e escolha **[!UICONTROL Selecionar]**.

   ![Selecionar página de campo de origem](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Selecione o botão à direita da **[!UICONTROL Campo de destino]** entrada.

   ![Selecionar campo de destino](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. No **[!UICONTROL Selecionar campo de destino]** selecione o namespace de identidade de destino para o qual deseja mapear o campo de origem e escolha **[!UICONTROL Selecionar]**.

   ![Selecionar página de campo de destino](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Para adicionar mais mapeamentos, repita as etapas de 1 a 5.

### Aplicar transformação {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Aplicar transformação"
>abstract="Marque essa opção ao usar campos de origem com hash não atribuídos, para que o Adobe Experience Platform os coloque automaticamente com hash na ativação."

Ao mapear atributos de origem com hash não atribuídos para atributos de destino que o destino espera que tenham hash (por exemplo: `email_lc_sha256` ou `phone_sha256`), verifique a **Aplicar transformação** opção para que o Adobe Experience Platform coloque automaticamente os atributos de origem em hash na ativação.

![Mapeamento de identidade](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Agendar exportação de segmento {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Data de término"
>abstract="Não está disponível a adição de uma data final à programação de segmento."

Por padrão, a variável [!UICONTROL Programação de segmento] A página mostra apenas os segmentos recém-selecionados que você escolheu no fluxo de ativação atual.

![Novos segmentos](../assets/ui/activate-segment-streaming-destinations/new-segments.png)

Para ver todos os segmentos que estão sendo ativados para o seu destino, use a opção de filtragem e desative a variável **[!UICONTROL Mostrar somente novos segmentos]** filtro.

![Todos os segmentos](../assets/ui/activate-segment-streaming-destinations/all-segments.png)

1. No **[!UICONTROL Programação de segmento]** selecione cada segmento e use a variável **[!UICONTROL Data inicial]** e **[!UICONTROL Data final]** seletores para configurar o intervalo de tempo para enviar dados ao seu destino.

   ![Programação de segmento](../assets/ui/activate-segment-streaming-destinations/segment-schedule.png)

   * Alguns destinos exigem que você selecione a variável **[!UICONTROL Origem do público]** para cada segmento, usando o menu suspenso abaixo dos seletores de calendário. Se o destino não incluir esse seletor, ignore esta etapa.

      ![ID do mapeamento](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Alguns destinos exigem o mapeamento manual [!DNL Platform] segmentos para sua contraparte no destino final. Para fazer isso, selecione cada segmento e insira a ID de segmento correspondente na plataforma de destino na **[!UICONTROL ID do mapeamento]** campo. Se o destino não incluir esse campo, ignore esta etapa.

      ![ID do mapeamento](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Alguns destinos exigem que você insira um **[!UICONTROL ID do aplicativo]** ao ativar [!DNL IDFA] ou [!DNL GAID] segmentos. Se o destino não incluir esse campo, ignore esta etapa.

      ![ID do aplicativo](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Selecionar **[!UICONTROL Próxima]** para acessar o [!UICONTROL Revisão] página.

## Consulte a seção {#review}

No **[!UICONTROL Revisão]** você poderá ver um resumo da sua seleção. Selecionar **[!UICONTROL Cancelar]** para interromper o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

![Resumo da seleção na etapa de revisão.](/help/destinations/assets/ui/activate-segment-streaming-destinations/review.png)

### Avaliação de política de consentimento {#consent-policy-evaluation}

Se sua organização comprou **Adobe Healthcare Shield** ou **Proteção de segurança e privacidade do Adobe**, selecione **[!UICONTROL Exibir políticas de consentimento aplicáveis]** para ver quais políticas de consentimento são aplicadas e quantos perfis são incluídos na ativação como resultado delas. Ler sobre [avaliação da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obter mais informações.

### Verificações de política de uso de dados {#data-usage-policy-checks}

No **[!UICONTROL Revisão]** etapa, o Experience Platform também verifica se há violações de política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de segmento até que a violação seja resolvida. Para obter informações sobre como resolver violações de política, leia sobre [violações de política de uso de dados](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) na seção documentação de governança de dados.

![violação da política de dados](../assets/common/data-policy-violation.png)

### Filtrar segmentos {#filter-segments}

Também nesta etapa é possível usar os filtros disponíveis na página para exibir apenas os segmentos cujo agendamento ou mapeamento foi atualizado como parte desse fluxo de trabalho. Você também pode alternar quais colunas da tabela deseja visualizar.

![Gravação de tela mostrando os filtros de segmento disponíveis na etapa de revisão.](/help/destinations/assets/ui/activate-segment-streaming-destinations/filter-segments-review-step.gif)

Se estiver satisfeito com a sua seleção e nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

## Verificar ativação de segmento {#verify}

Verifique a [documentação de monitoramento de destino](../../dataflows/ui/monitor-destinations.md) para obter informações detalhadas sobre como monitorar o fluxo de dados para seus destinos.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Segment membership in the audience would be added and removed as users are qualified or disqualified for the activated segments.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical segment qualifications are sent to [!DNL Facebook] when you activate the segments to the destination.
-->
