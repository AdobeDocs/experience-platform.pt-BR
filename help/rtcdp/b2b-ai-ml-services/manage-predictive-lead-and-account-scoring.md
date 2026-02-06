---
title: Gerenciar lead preditivo e pontuação da conta no Real-Time CDP B2B
type: Documentation
description: Este documento fornece informações sobre como gerenciar o recurso de pontuação preditiva de leads e contas no B2B da Experience Platform CDP.
feature: Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=pt-BR#rtcdp-editions" newtab=true
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: 5998adf98aa7250864983d7e4e629921633e1a1c
workflow-type: tm+mt
source-wordcount: '982'
ht-degree: 3%

---

# Gerenciar pontuação preditiva de leads e contas no Adobe Real-Time Customer Data Platform, B2B edition

>[!NOTE]
>
>Somente usuários com a permissão Gerenciar IA B2B podem criar, alterar e excluir metas de pontuação.

Este tutorial percorre as etapas para gerenciar metas de pontuação do lead preditivo e do serviço de pontuação da conta. As metas de pontuação podem ser para perfil de pessoa ou perfil de conta

## Criar uma nova pontuação

Para criar uma nova pontuação, selecione **[!UICONTROL Services]** na barra lateral e **[!UICONTROL Create score]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

A tela **[!UICONTROL Basic information]** é exibida, solicitando que você selecione um tipo de perfil, insira um nome e uma descrição opcional. Quando terminar, selecione **[!UICONTROL Next]**.

![informações-básicas-da-inserção-plano](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

A tela **[!UICONTROL Define your goal]** é exibida. Selecione a seta suspensa e, em seguida, selecione um tipo de meta na janela suspensa exibida.

![plas-select-a-goal](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

A caixa de diálogo **[!UICONTROL Goal specifics]** é aberta. Selecione a seta suspensa e selecione o nome do campo de meta na janela suspensa exibida.

![plas-select-a-goal-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

A seleção **[!UICONTROL Goal conditions]** é exibida. Selecione a seta suspensa e selecione condição na janela suspensa exibida.

![condição_específica-meta-plano](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

O campo **[!UICONTROL Goal value]** é exibido. Em seguida, configure o [!UICONTROL Goal specifics]. Selecione o painel [!UICONTROL Enter Field Value] e insira seu valor de meta.

>[!NOTE]
>
>Vários valores de meta podem ser adicionados.

![valor-campo-específico-da-meta-plano](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Para adicionar outros campos, selecione **[!UICONTROL Add field]**.

![plas-goal-specis-add-event](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Para configurar o período de previsão, selecione a seta suspensa e selecione o período desejado.

![período-previsão-plano](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

A política de mesclagem selecionada determina como os valores de campo de um perfil de pessoa são selecionados. Usando a seta suspensa, selecione a política de mesclagem desejada e selecione **[!UICONTROL Finish]**.

A caixa de diálogo **[!UICONTROL Scoring setup is complete]** é exibida confirmando que a nova pontuação foi criada. Selecione **[!UICONTROL OK]**.

![pontuação-completa](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Pode levar até 24 horas para que cada processo de pontuação seja concluído.

Você retornará à guia **[!UICONTROL Services]**, na qual poderá ver a nova pontuação criada na lista de pontuações.

![pontuação planejada-criada](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Selecione a pontuação para exibir detalhes e informações adicionais sobre os detalhes da última execução.

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Para obter informações mais detalhadas sobre os códigos de erro que podem ser vistos nos detalhes da última execução, consulte a seção sobre [códigos de erro do pipeline de IA de clientes potenciais](#leads-ai-pipeline-error-codes) neste documento.

## Editar uma pontuação

Para editar uma pontuação, selecione uma pontuação na guia **[!UICONTROL Services]** e selecione **[!UICONTROL Edit]** no painel de detalhes adicionais no lado direito da tela.

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

A caixa de diálogo **[!UICONTROL Edit instance]** é exibida, onde você pode editar a descrição da pontuação. Faça as alterações e selecione **[!UICONTROL Save]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>A configuração de pontuação não pode ser alterada, pois isso acionará o novo treinamento e a nova pontuação do modelo. É equivalente a excluir a pontuação e criar uma nova. Para editar a configuração da pontuação, você precisará clonar essa pontuação ou criar uma nova.

Você retornará à guia **[!UICONTROL Services]**. Selecione a pontuação para exibir os detalhes da descrição atualizada no painel de detalhes adicionais no lado direito da tela.

## Clonar uma pontuação

Para clonar uma pontuação, selecione uma pontuação na guia **[!UICONTROL Services]** e selecione **[!UICONTROL Clone]** no painel de detalhes adicionais no lado direito da tela.

![pontuação-clone-plas](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

A tela **[!UICONTROL Basic information]** é exibida. O tipo, o nome e a descrição do perfil são clonados da pontuação original. Corrija esses detalhes e selecione **[!UICONTROL Next]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

A tela **[!UICONTROL Define your goal]** é exibida. Complete a seção de metas como faria ao criar uma nova pontuação e selecione **[!UICONTROL Finish]**.

Você retornará à guia **[!UICONTROL Services]**, onde poderá ver a pontuação recém-clonada na lista.

>[!NOTE]
>
>A seção **[!UICONTROL Define your goal]** não é clonada da pontuação original.

## Excluir uma pontuação

Para excluir uma pontuação, selecione-a na guia **[!UICONTROL Services]** e selecione **[!UICONTROL Delete]** no painel de detalhes adicionais no lado direito da tela.

![pontuação de exclusão de planos](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

A caixa de diálogo de confirmação **[!UICONTROL Delete documentation]** é exibida. Selecione **[!UICONTROL Delete]**.

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>A exclusão da definição de pontuação também excluiria todas as pontuações previstas no perfil de pessoa ou no perfil de conta, mas não no grupo de campos criado para a definição de pontuação. O grupo de campos será deixado &quot;órfão&quot; no modelo de dados.

Você retornará à guia **[!UICONTROL Services]**, na qual não poderá mais ver a pontuação na lista.

## Códigos de erro de pipeline de IA de clientes potenciais

| Código de erro | Mensagem de erro |
| --- | --- |
| 401 | ERRO 401. O pipeline de IA de cliente potencial foi interrompido: não há contas válidas suficientes para a pontuação da conta. Contagem de contas: {}. |
| 402 | ERRO 402. O pipeline de IA de cliente potencial foi interrompido: não há contatos válidos suficientes para a pontuação de contatos. Contagem de contatos: {}. |
| 403 | ERRO 403. O pipeline de IA de cliente potencial foi interrompido: volume de atividade insuficiente para treinamento de modelo. Contagem de eventos: {}. |
| 404 | ERRO 404. O pipeline de IA de cliente potencial foi interrompido: não há conversões suficientes para treinamento de modelo. Contagem de conversões: {}. |
| 405 | ERRO 405. O pipeline de IA de cliente potencial foi interrompido: atividade muito esparsa para treinamento de modelo válido. Somente {} por cento das contas tem atividade. |
| 406 | ERRO 406. O pipeline de IA de cliente potencial foi interrompido: atividade muito esparsa para treinamento de modelo válido. Somente {} por cento dos contatos tem atividade. |
| 407 | ERRO 407. O pipeline de IA de cliente potencial foi interrompido: os tipos de atividade de dados de pontuação não correspondem aos dados de treinamento. |
| 408 | ERRO 408. O pipeline de IA de cliente potencial foi interrompido: a taxa de ausências é muito alta para recursos de atividade. Taxa ausente: {}. |
| 409 | ERRO 409. O pipeline de IA de cliente potencial parou: a auc de teste está muito baixa. Auc de teste: {}. |
| 410 | ERRO 410. Pipeline de IA de cliente potencial interrompido: a auc de teste está muito baixa após o ajuste do parâmetro. Auc de teste: {}. |
| 411 | ERRO 411. O pipeline de IA de cliente potencial foi interrompido: os dados de treinamento não têm conversões suficientes para produzir um modelo confiável. Conversões: {}. |
| 412 | ERRO 412. O pipeline de IA de cliente potencial foi interrompido: os dados de teste não têm nenhuma conversão para calcular a AUC-ROC. |

| Código de aviso/informações | Mensagem |
| --- | --- |
| 100 | INFORMAÇÃO 100. Verificação de qualidade de IA de clientes potenciais: a contagem de contas é: {}. |
| 101 | INFORMAÇÃO 101. Verificação de qualidade de IA de clientes potenciais: a contagem de contatos é: {}. |
| 102 | INFORMAÇÃO 102. Conduz verificação de qualidade de IA: a contagem de oportunidades é: {}. |
| 103 | INFORMAÇÃO 103. Conduz a verificação de qualidade da IA: o teste de auc é baixo. Iniciar ajuste de parâmetro. Testando auc: {}. |
| 200 | AVISO 200. Conduz verificação de qualidade de IA: a taxa de recursos firmográficos ausentes é: {}. |
| 201 | AVISO 201. Verificação de qualidade de IA de clientes potenciais: a taxa ausente de recursos de atividade é: {}. |

## Próximas etapas

Ao seguir este tutorial, agora é possível criar e gerenciar pontuações com êxito. Consulte os seguintes documentos para obter mais detalhes:

* [Pontuação preditiva de leads e contas](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Monitorar trabalhos de pontuação preditiva de leads e contas](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
