---
title: Ativar dados do público-alvo para destinos de transmissão
type: Tutorial
description: Saiba como ativar os públicos-alvo no Adobe Experience Platform mapeando-os para destinos de transmissão.
exl-id: bb61a33e-38fc-4217-8999-9eb9bf899afa
source-git-commit: f741e62b3340b743e465edf3f7a007580b3f61be
workflow-type: tm+mt
source-wordcount: '1164'
ht-degree: 1%

---


# Ativar públicos para destinos de transmissão

>[!IMPORTANT]
> 
> * Para ativar públicos-alvo e ativar a [etapa de mapeamento](#mapping) do fluxo de trabalho, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar destinos]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
> * Para ativar públicos-alvo sem passar pela [etapa de mapeamento](#mapping) do fluxo de trabalho, é necessário **[!UICONTROL Exibir destinos]**, **[!UICONTROL Ativar segmento sem mapeamento]**, **[!UICONTROL Exibir perfis]**, e **[!UICONTROL Exibir segmentos]** [permissões de controle de acesso](/help/access-control/home.md#permissions).
>* Para exportar *identidades*, você precisará do **[!UICONTROL Exibir gráfico de identidade]** [permissão de controle de acesso](/help/access-control/home.md#permissions). <br> ![Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos.](/help/destinations/assets/overview/export-identities-to-destination.png "Selecione o namespace de identidade destacado no fluxo de trabalho para ativar públicos para destinos."){width="100" zoomable="yes"}
> 
> Leia o [visão geral do controle de acesso](/help/access-control/ui/overview.md) ou entre em contato com o administrador do produto para obter as permissões necessárias.

## Visão geral {#overview}

Este artigo explica o fluxo de trabalho necessário para ativar públicos-alvo em destinos de transmissão do Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Para ativar públicos para destinos, você deve ter o [conectado a um destino](./connect-destination.md). Se ainda não tiver feito isso, acesse o [catálogo de destinos](../catalog/overview.md), navegue pelos destinos compatíveis e configure o destino que deseja usar.

## Selecione seu destino {#select-destination}

1. Ir para **[!UICONTROL Conexões > Destinos]** e selecione a variável **[!UICONTROL Catálogo]** guia.

   ![Guia Catálogo de destino mostrando vários destinos de streaming.](../assets/ui/activate-segment-streaming-destinations/catalog-tab.png)

1. Selecionar **[!UICONTROL Ativar públicos]** no cartão correspondente ao destino em que deseja ativar os públicos-alvo, conforme mostrado na imagem abaixo.

   ![Ative o controle destacado no catálogo de destinos.](../assets/ui/activate-segment-streaming-destinations/activate-audiences-button.png)

1. Selecione a conexão de destino que deseja usar para ativar os públicos-alvo e selecione **[!UICONTROL Próxima]**.

   ![Uma conexão de destino destacada na etapa Selecionar destino.](../assets/ui/activate-segment-streaming-destinations/select-destination.png)

1. Mover para a próxima seção para [selecionar seus públicos](#select-audiences).

## Selecione seus públicos-alvo {#select-audiences}

Para selecionar os públicos que deseja ativar para o destino, use as caixas de seleção à esquerda dos nomes dos públicos e selecione **[!UICONTROL Próxima]**.

Você pode selecionar entre vários tipos de públicos-alvo, dependendo de sua origem:

* **[!UICONTROL Serviço de segmentação]**: públicos-alvo gerados no Experience Platform pelo serviço de segmentação. Consulte a [documentação de segmentação](../../segmentation/ui/overview.md) para obter mais detalhes.
* **[!UICONTROL Upload personalizado]**: públicos gerados fora do Experience Platform e carregados na Platform como arquivos CSV. Para saber mais sobre públicos-alvo externos, consulte a documentação em [importação de um público](../../segmentation/ui/overview.md#import-audience).
* Outros tipos de públicos-alvo, provenientes de outras soluções de Adobe, como [!DNL Audience Manager].

![Vários públicos-alvo destacados na etapa Selecionar públicos-alvo.](../assets/ui/activate-segment-streaming-destinations/select-audiences.png)

## Mapear atributos e identidades {#mapping}

>[!IMPORTANT]
>
>Esta etapa se aplica somente a alguns destinos de transmissão de público. Se o seu destino não tiver um **[!UICONTROL Mapeamento]** etapa, saltar para [agendamento de público](#scheduling).
>
>Ao ativar públicos para destinos de transmissão, você também deve mapear *pelo menos um namespace de identidade de destino*, além dos atributos do perfil de público-alvo. Caso contrário, os públicos-alvo não serão ativados para a plataforma de destino.
> ![Imagem da etapa de mapeamento mostrando um mapeamento de namespace de identidade obrigatório.](../assets/ui/activate-segment-streaming-destinations/identity-mapping-mandatory.png) {zoomable="yes"}


Alguns destinos de transmissão de público exigem que você selecione atributos de origem ou namespaces de identidade para mapear como identidades de destino no destino.

1. No **[!UICONTROL Mapeamento]** selecione **[!UICONTROL Adicionar novo mapeamento]**.

   ![Adicionar novo controle de mapeamento realçado.](../assets/ui/activate-segment-streaming-destinations/add-new-mapping.png)

1. Selecione a seta à direita da **[!UICONTROL Campo de origem]** entrada.

   ![Selecione o controle de campo de origem realçado.](../assets/ui/activate-segment-streaming-destinations/select-source-field.png)

1. No **[!UICONTROL Selecionar campo de origem]** , use o **[!UICONTROL Selecionar atributos]** ou o **[!UICONTROL Selecionar namespace de identidade]** opções para alternar entre as duas categorias de campos de origem disponíveis. No disponível [!DNL XDM] atributos de perfil e namespaces de identidade, selecione aqueles que deseja mapear para o destino e escolha **[!UICONTROL Selecionar]**.

   ![Página Selecionar campo de origem mostrando vários campos de origem disponíveis.](../assets/ui/activate-segment-streaming-destinations/source-field-page.png)

1. Selecione o botão à direita da **[!UICONTROL Campo de destino]** entrada.

   ![Selecione o campo de destino em destaque.](../assets/ui/activate-segment-streaming-destinations/select-target-field.png)

1. No **[!UICONTROL Selecionar campo de destino]** selecione o namespace de identidade de destino para o qual deseja mapear o campo de origem e escolha **[!UICONTROL Selecionar]**.

   ![Página Selecionar campo de destino mostrando as opções disponíveis para mapeamentos de campo de destino.](../assets/ui/activate-segment-streaming-destinations/target-field-page.png)

1. Para adicionar mais mapeamentos, repita as etapas de 1 a 5.

### Aplicar transformação {#apply-transformation}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_applytransformation"
>title="Aplicar transformação"
>abstract="Marque essa opção ao usar campos de origem com hash não atribuídos, para que o Adobe Experience Platform os coloque automaticamente com hash na ativação."

Ao mapear atributos de origem com hash não atribuídos para atributos de destino que o destino espera que tenham hash (por exemplo: `email_lc_sha256` ou `phone_sha256`), verifique a **Aplicar transformação** opção para que o Adobe Experience Platform coloque automaticamente os atributos de origem em hash na ativação.

![Aplique o controle de transformação destacado na etapa Mapeamento de identidade.](../assets/ui/activate-segment-streaming-destinations/mapping-summary.png)

## Agendar exportação de público {#scheduling}

>[!CONTEXTUALHELP]
>id="platform_destinations_activate_enddate"
>title="Data de término"
>abstract="A adição de uma data final à programação de público-alvo não está disponível."

Por padrão, a variável **[!UICONTROL Programação de público]** A página mostra apenas os públicos-alvo recém-selecionados que você escolheu no fluxo de ativação atual.

Para ver todos os públicos-alvo sendo ativados para o seu destino, use a opção de filtragem e desative a variável **[!UICONTROL Mostrar somente novos públicos-alvo]** filtro.

![Todos os públicos-alvo](../assets/ui/activate-segment-streaming-destinations/all-audiences.png)

1. No **[!UICONTROL Programação de público]** selecione cada público e use a variável **[!UICONTROL Data inicial]** e **[!UICONTROL Data final]** seletores para configurar o intervalo de tempo para enviar dados ao seu destino.

   ![Filtro de agendamento de público realçado.](../assets/ui/activate-segment-streaming-destinations/audience-schedule.png)

   * Alguns destinos exigem que você selecione a variável **[!UICONTROL Origem do público]** para cada público-alvo, usando o menu suspenso abaixo dos seletores de calendário. Se o destino não incluir esse seletor, ignore esta etapa.

     ![Lista suspensa ID de mapeamento realçada.](../assets/ui/activate-segment-streaming-destinations/origin-of-audience.png)

   * Alguns destinos exigem o mapeamento manual [!DNL Platform] públicos-alvo à contraparte no destino-alvo. Para fazer isso, selecione cada público e insira a ID de público correspondente na plataforma de destino na **[!UICONTROL ID do mapeamento]** campo. Se o destino não incluir esse campo, ignore esta etapa.

     ![Origem da lista suspensa de públicos-alvo destacada.](../assets/ui/activate-segment-streaming-destinations/mapping-id.png)

   * Alguns destinos exigem que você insira um **[!UICONTROL ID do aplicativo]** ao ativar [!DNL IDFA] ou [!DNL GAID] públicos-alvo. Se o destino não incluir esse campo, ignore esta etapa.

     ![Lista suspensa de ID do aplicativo realçada.](../assets/ui/activate-segment-streaming-destinations/destination-appid.png)

1. Selecionar **[!UICONTROL Próxima]** para acessar o [!UICONTROL Revisão] página.

## Revisar {#review}

No **[!UICONTROL Revisão]** você poderá ver um resumo da sua seleção. Selecionar **[!UICONTROL Cancelar]** para interromper o fluxo, **[!UICONTROL Voltar]** para modificar suas configurações ou **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

![Resumo da seleção na etapa de revisão.](../assets/ui/activate-segment-streaming-destinations/review.png)

### Avaliação de política de consentimento {#consent-policy-evaluation}

Se sua organização comprou **Adobe Healthcare Shield** ou **Proteção de segurança e privacidade do Adobe**, selecione **[!UICONTROL Exibir políticas de consentimento aplicáveis]** para ver quais políticas de consentimento são aplicadas e quantos perfis são incluídos na ativação como resultado delas. Ler sobre [avaliação da política de consentimento](/help/data-governance/enforcement/auto-enforcement.md#consent-policy-evaluation) para obter mais informações.

### Verificações de política de uso de dados {#data-usage-policy-checks}

No **[!UICONTROL Revisão]** etapa, o Experience Platform também verifica se há violações de política de uso de dados. Veja abaixo um exemplo de violação de uma política. Não é possível concluir o fluxo de trabalho de ativação de público-alvo até que a violação seja resolvida. Para obter informações sobre como resolver violações de política, leia sobre [violações de política de uso de dados](/help/data-governance/enforcement/auto-enforcement.md#data-usage-violation) na seção documentação de governança de dados.

![Um exemplo de violação da política de dados mostrada no fluxo de trabalho de ativação.](../assets/common/data-policy-violation.png)

### Filtrar públicos {#filter-audiences}

Também nesta etapa é possível usar os filtros disponíveis na página para exibir somente os públicos-alvo cujo agendamento ou mapeamento foi atualizado como parte desse fluxo de trabalho. Você também pode alternar quais colunas da tabela deseja visualizar.

![Gravação de tela mostrando os filtros de público-alvo disponíveis na etapa de revisão.](../assets/ui/activate-segment-streaming-destinations/filter-audiences-review-step.gif)

Se estiver satisfeito com a sua seleção e nenhuma violação de política tiver sido detectada, selecione **[!UICONTROL Concluir]** para confirmar a seleção e começar a enviar dados para o destino.

## Verificar ativação de público {#verify}

Verifique a [documentação de monitoramento de destino](../../dataflows/ui/monitor-destinations.md) para obter informações detalhadas sobre como monitorar o fluxo de dados para seus destinos.

<!-- 
For [!DNL Facebook Custom Audience], a successful activation means that a [!DNL Facebook] custom audience would be created programmatically in [[!UICONTROL Facebook Ads Manager]](https://www.facebook.com/adsmanager/manage/). Audience membership in the audience would be added and removed as users are qualified or disqualified for the activated audiences.

>[!TIP]
>
>The integration between Adobe Experience Platform and [!DNL Facebook] supports historical audience backfills. All historical audience qualifications are sent to [!DNL Facebook] when you activate the audiences to the destination.
-->
