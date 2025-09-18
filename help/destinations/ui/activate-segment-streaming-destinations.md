---
title: Ativar dados do público-alvo para destinos de transmissão
type: Tutorial
description: Saiba como ativar os públicos-alvo no Adobe Experience Platform mapeando-os para destinos de transmissão.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: 595856842a3890426bb196218bd8be4e321ff8aa
workflow-type: tm+mt
source-wordcount: '1189'
ht-degree: 6%

---


# Ativar públicos para destinos de transmissão

>[!IMPORTANT]
> 
> * Para ativar públicos e habilitar a [etapa de mapeamento](#mapping) do fluxo de trabalho, você precisa das **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Destinos]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
> * Para ativar os públicos-alvo sem passar pela [etapa de mapeamento](#mapping) do fluxo de trabalho, você precisa das **[!UICONTROL Exibir Destinos]**, **[!UICONTROL Ativar Segmento sem Mapeamento]**, **[!UICONTROL Exibir Perfis]** e **[!UICONTROL Exibir Segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
> * Para exportar *identidades*, você precisa da **[!UICONTROL permissão Exibir Gráfico de Identidade]** [controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade realçado no fluxo de trabalho para ativar as audiências para os destinos."){width="100" zoomable="yes"}
> 
> Leia a [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou contate o administrador do produto para obter as permissões necessárias.

## Visão geral {#overview}

Este artigo explica o fluxo de trabalho necessário para ativar públicos-alvo em destinos de transmissão do Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Para ativar públicos para destinos, você deve ter [se conectado com êxito a um destino](./connect-destination.md). Se ainda não tiver feito isso, vá para o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

## Selecione seu destino {#select-destination}

1. Vá para **[!UICONTROL Conexões > Destinos]** e selecione a guia **[!UICONTROL Catálogo]**.

   ![Guia Catálogo de Destino mostrando vários destinos de streaming.](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecione **[!UICONTROL Ativar públicos-alvo]** no cartão correspondente ao destino em que você deseja ativar os públicos-alvo, conforme mostrado na imagem abaixo.

   ![Ativar controle realçado no catálogo de destinos.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. Selecione a conexão de destino que você deseja usar para ativar seus públicos e selecione **[!UICONTROL Avançar]**.

   ![Uma conexão de destino foi realçada na etapa Selecionar destino.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Mova para a próxima seção para [selecionar seus públicos-alvo](#select-audiences).

## Selecione seus públicos-alvo {#select-audiences}

Para selecionar os públicos que você deseja ativar para o destino, use as caixas de seleção à esquerda dos nomes de público e selecione **[!UICONTROL Avançar]**.

Você pode selecionar entre vários tipos de públicos-alvo, dependendo de sua origem:

* **[!UICONTROL Serviço de segmentação]**: públicos-alvo gerados no Experience Platform pelo serviço de segmentação. Consulte a [documentação de segmentação](../../segmentation/ui/overview.md) para obter mais detalhes.
* **[!UICONTROL Upload personalizado]**: públicos-alvo gerados fora do Experience Platform e carregados no Experience Platform como arquivos CSV. Para saber mais sobre públicos-alvo externos, consulte a documentação sobre [importação de um público-alvo](../../segmentation/ui/audience-portal.md#import-audience).
* Outros tipos de públicos-alvo, originados de outras soluções da Adobe, como o [!DNL Audience Manager].

![Vários públicos-alvo destacados na etapa Selecionar públicos-alvo.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## Mapear atributos e identidades {#mapping}

>[!IMPORTANT]
>
>Esta etapa se aplica somente a alguns destinos de transmissão de público. Se o destino não tiver uma etapa de **[!UICONTROL Mapeamento]**, pule para [agendamento de público-alvo](#scheduling).
>
>Ao ativar públicos para destinos de streaming, você também deve mapear *pelo menos um namespace de identidade de destino*, além dos atributos de perfil de destino. Caso contrário, os públicos-alvo não serão ativados para a plataforma de destino.
>&#x200B;> ![Imagem da etapa de mapeamento mostrando um mapeamento de namespace de identidade obrigatório.](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


Alguns destinos de transmissão de público exigem que você selecione atributos de origem ou namespaces de identidade para mapear como identidades de destino no destino.

1. Na página **[!UICONTROL Mapeamento]**, selecione **[!UICONTROL Adicionar novo mapeamento]**.

   ![Adicionar novo controle de mapeamento realçado.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Selecione a seta à direita da entrada **[!UICONTROL Source field]**.

   ![Selecionar controle de campo de origem realçado.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. Na página **[!UICONTROL Selecionar campo de origem]**, use as opções **[!UICONTROL Selecionar atributos]** ou **[!UICONTROL Selecionar namespace de identidade]** para alternar entre as duas categorias de campos de origem disponíveis. Nos atributos de perfil e namespaces de identidade [!DNL XDM] disponíveis, selecione aqueles que você deseja mapear para o destino e escolha **[!UICONTROL Selecionar]**.

   Use a opção **[!UICONTROL Mostrar apenas campos com dados]** para exibir apenas campos de esquema preenchidos com valores. Por padrão, somente os campos de esquema preenchidos são exibidos.

   ![Selecionar página de campo de origem mostrando vários campos de origem disponíveis.](../assets/ui/activate-segment-streaming-destinations/select-source-field-modal.png)

1. Selecione o botão à direita da entrada **[!UICONTROL Campo de destino]**.

   ![Selecionar campo de destino realçado.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. Na página **[!UICONTROL Selecionar campo de destino]**, selecione o namespace de identidade de destino para o qual você deseja mapear o campo de origem e escolha **[!UICONTROL Selecionar]**.

   ![Selecionar página de campo de destino mostrando as opções disponíveis para mapeamentos de campo de destino.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Para adicionar mais mapeamentos, repita as etapas de 1 a 5.

### Aplicar transformação {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Aplicar transformação"
>abstract="Marque essa opção ao usar campos de origem sem hash, para que a Adobe Experience Platform faça o hash automaticamente na ativação."

Ao mapear atributos de origem com hash não atribuídos para atributos de destino que o destino espera que tenham hash (por exemplo: `email_lc_sha256` ou `phone_sha256`), marque a opção **Aplicar transformação** para que o Adobe Experience Platform coloque os atributos de origem em hash automaticamente na ativação.

![Aplicar controle de transformação realçado na etapa Mapeamento de identidade.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Programar exportação de público-alvo {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Data final"
>abstract="A adição de uma data final para a programação de público-alvo não está disponível."

Por padrão, a página **[!UICONTROL Agenda de público-alvo]** mostra apenas os públicos-alvo recém-selecionados que você escolheu no fluxo de ativação atual.

Para ver todos os públicos-alvo sendo ativados para o seu destino, use a opção de filtragem e desabilite o filtro **[!UICONTROL Mostrar somente novos públicos-alvo]**.

![Todos os públicos-alvo](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. Na página **[!UICONTROL Agenda de público-alvo]**, selecione cada público-alvo e use os seletores **[!UICONTROL Data de início]** e **[!UICONTROL Data de término]** para configurar o intervalo de tempo para enviar os dados ao seu destino.

   ![Filtro de agendamento de público-alvo realçado.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * Alguns destinos exigem que você selecione a **[!UICONTROL Origem do público-alvo]** para cada público-alvo, usando o menu suspenso abaixo dos seletores de calendário. Se o destino não incluir esse seletor, ignore esta etapa.

     ![Lista suspensa de ID de mapeamento realçada.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Alguns destinos exigem que você mapeie manualmente [!DNL Experience Platform] públicos-alvo para seus homólogos no destino-alvo. Para fazer isso, selecione cada público e insira a ID de público correspondente na plataforma de destino no campo **[!UICONTROL ID de mapeamento]**. Se o destino não incluir esse campo, ignore esta etapa.

     ![Origem da lista suspensa de público-alvo destacada.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Alguns destinos exigem que você insira um **[!UICONTROL ID do aplicativo]** ao ativar públicos-alvo do [!DNL IDFA] ou do [!DNL GAID]. Se o destino não incluir esse campo, ignore esta etapa.

     ![Lista suspensa de ID do aplicativo realçada.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Selecione **[!UICONTROL Avançar]** para ir para a página [!UICONTROL Revisão].

## Revisar {#review}

Na página **[!UICONTROL Revisão]**, você pode ver um resumo da sua seleção. Selecione **[!UICONTROL Cancelar]** para interromper o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar sua seleção e começar a enviar dados ao destino.

![Resumo da seleção na etapa de revisão.](../assets/ui/activate-segment-streaming-destinations/review.png)

### Avaliação da política de consentimento {#consent-policy-evaluation}

Se sua organização adquiriu o **Adobe Healthcare Shield** ou o **Adobe Privacy &amp; Security Shield**, selecione **[!UICONTROL Exibir políticas de consentimento aplicáveis]** para ver quais políticas de consentimento são aplicadas e quantos perfis são incluídos na ativação como resultado delas. Leia sobre [avaliação de política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obter mais informações.

### Verificações de política de uso de dados {#data-usage-policy-checks}

Na etapa **[!UICONTROL Revisão]**, a Experience Platform também verifica se há violações de política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de público-alvo até que a violação seja resolvida. Para obter informações sobre como resolver violações de política, leia sobre [violações de política de uso de dados](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) na seção de documentação sobre governança de dados.

![Um exemplo de violação de política de dados mostrada no fluxo de trabalho de ativação.](../assets/common/data-policy-violation.png)

### Filtrar públicos {#filter-audiences}

Também nesta etapa é possível usar os filtros disponíveis na página para exibir somente os públicos-alvo cujo agendamento ou mapeamento foi atualizado como parte desse fluxo de trabalho. Você também pode alternar quais colunas da tabela deseja visualizar.

![Gravação de tela mostrando os filtros de público-alvo disponíveis na etapa de revisão.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

Se você estiver satisfeito com sua seleção e nenhuma violação de política for detectada, selecione **[!UICONTROL Concluir]** para confirmar sua seleção e começar a enviar dados para o destino.

## Verificar ativação de público {#verify}

Consulte a [documentação de monitoramento de destino](../../dataflows/ui/monitor-destinations.md) para obter informações detalhadas sobre como monitorar o fluxo de dados para seus destinos.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
