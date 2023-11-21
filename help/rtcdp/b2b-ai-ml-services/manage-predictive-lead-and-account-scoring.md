---
title: Gerenciar lead preditivo e pontuação da conta no Real-Time CDP B2B
type: Documentation
description: Este documento fornece informações sobre como gerenciar o lead preditivo e o recurso de pontuação da conta no Experience Platform CDP B2B.
feature: Profiles, B2B
badgeB2B: label="Edição B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: db57fa753a3980dca671d476521f9849147880f1
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 3%

---

# Gerenciar pontuação preditiva de leads e contas no Adobe Real-time Customer Data Platform, B2B Edition

>[!NOTE]
>
>Somente usuários com a permissão Gerenciar IA B2B podem criar, alterar e excluir metas de pontuação.

Este tutorial percorre as etapas para gerenciar metas de pontuação do lead preditivo e do serviço de pontuação da conta. As metas de pontuação podem ser para perfil de pessoa ou perfil de conta

## Criar uma nova pontuação

Para criar uma nova pontuação, selecione o **[!UICONTROL Serviços]** na barra lateral e selecione **[!UICONTROL Criar pontuação]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

A variável **[!UICONTROL Informações básicas]** é exibida, solicitando que você selecione um tipo de perfil, insira um nome e uma descrição opcional. Quando terminar, selecione **[!UICONTROL Próxima]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

A variável **[!UICONTROL Definir sua meta]** é exibida. Selecione a seta suspensa e, em seguida, selecione um tipo de meta na janela suspensa exibida.

![plas-select-a-goal](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

A variável **[!UICONTROL Especificações da meta]** será aberta. Selecione a seta suspensa e selecione o nome do campo de meta na janela suspensa exibida.

![plas-select-a-goal-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

A variável **[!UICONTROL Condições da meta]** é exibida. Selecione a seta suspensa e selecione condição na janela suspensa exibida.

![plas-goal-specis-condition](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

A variável **[!UICONTROL Valor da meta]** é exibido. Em seguida, configure o [!UICONTROL Especificações da meta]. Selecione o [!UICONTROL Inserir valor do campo] e insira o valor da meta.

>[!NOTE]
>
>Vários valores de meta podem ser adicionados.

![valor de campo específico do objetivo do plano](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Para adicionar campos extras, selecione **[!UICONTROL Adicionar campo]**.

![evento de adição de especificações do objetivo do plano](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Para configurar o período de previsão, selecione a seta suspensa e selecione o período desejado.

![plas-prediction-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

A política de mesclagem selecionada determina como os valores de campo de um perfil de pessoa são selecionados. Usando a seta suspensa, selecione a política de mesclagem de escolha e selecione **[!UICONTROL Concluir]**.

A variável **[!UICONTROL A configuração de pontuação foi concluída]** será exibida confirmando que a nova pontuação foi criada. Selecionar **[!UICONTROL OK]**.

![pontuação total](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Pode levar até 24 horas para que cada processo de pontuação seja concluído.

Você retornará à janela **[!UICONTROL Serviços]** guia, onde você pode ver a nova pontuação criada na lista de pontuações.

![pontuação plas-criada](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Selecione a pontuação para exibir detalhes e informações adicionais sobre os detalhes da última execução.

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Para obter informações mais detalhadas sobre os códigos de erro que podem ser vistos nos detalhes da última execução, consulte a seção em [códigos de erro de pipeline de IA para clientes potenciais](#leads-ai-pipeline-error-codes) neste documento.

## Editar uma pontuação

Para editar uma pontuação, selecione uma das **[!UICONTROL Serviços]** e selecione **[!UICONTROL Editar]** no painel de detalhes adicionais no lado direito da tela.

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

A variável **[!UICONTROL Editar instância]** será exibida, onde você poderá editar a descrição da pontuação. Faça as alterações e selecione **[!UICONTROL Salvar]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>A configuração de pontuação não pode ser alterada, pois isso acionará o novo treinamento e a nova pontuação do modelo. É equivalente a excluir a pontuação e criar uma nova. Para editar a configuração da pontuação, você precisará clonar essa pontuação ou criar uma nova.

Você retornará à janela **[!UICONTROL Serviços]** guia. Selecione a pontuação para exibir os detalhes da descrição atualizada no painel de detalhes adicionais no lado direito da tela.

## Clonar uma pontuação

Para clonar uma pontuação, selecione uma pontuação na **[!UICONTROL Serviços]** e selecione **[!UICONTROL Clonar]** no painel de detalhes adicionais no lado direito da tela.

![plas-clone-score](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

A variável **[!UICONTROL Informações básicas]** é exibida. O tipo, o nome e a descrição do perfil são clonados da pontuação original. Corrija esses detalhes e selecione **[!UICONTROL Próxima]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

A variável **[!UICONTROL Definir sua meta]** é exibida. Complete a seção de metas como faria ao criar uma nova pontuação e selecione **[!UICONTROL Concluir]**.

Você retornará à janela **[!UICONTROL Serviços]** guia, onde você pode ver a pontuação recém-clonada na lista.

>[!NOTE]
>
>A variável **[!UICONTROL Definir sua meta]** A seção não é clonada da pontuação original.

## Excluir uma pontuação

Para excluir uma pontuação, selecione uma das **[!UICONTROL Serviços]** e selecione **[!UICONTROL Excluir]** no painel de detalhes adicionais no lado direito da tela.

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

A variável **[!UICONTROL Excluir documentação]** confirmação será exibida. Clique em **[!UICONTROL Excluir]**.

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>A exclusão da definição de pontuação também excluiria todas as pontuações previstas no perfil de pessoa ou no perfil de conta, mas não no grupo de campos criado para a definição de pontuação. O grupo de campos será deixado &quot;órfão&quot; no modelo de dados.

Você retornará à janela **[!UICONTROL Serviços]** onde não é mais possível ver a pontuação na lista.

## Códigos de erro de pipeline de IA de clientes potenciais

| Código de erro | Mensagem de erro |
| --- | --- |
| 401 | ERRO 401. O pipeline de IA de cliente potencial foi interrompido: não há contas válidas suficientes para a pontuação da conta. Contagem de contas: {}. |
| 402 | ERRO 402. O pipeline de IA de cliente potencial foi interrompido: não há contatos válidos suficientes para a pontuação de contatos. Contagem de contatos: {}. |
| 403 | ERRO 403. O pipeline de IA de cliente potencial foi interrompido: volume de atividade insuficiente para treinamento de modelo. Contagem de eventos: {}. |
| 404 | ERRO 404. O pipeline de IA de cliente potencial foi interrompido: não há conversões suficientes para treinamento de modelo. Contagem de conversões: {}. |
| 405 | ERRO 405. O pipeline de IA de cliente potencial foi interrompido: atividade muito esparsa para treinamento de modelo válido. Somente {} porcentagem de contas tem atividade. |
| 406 | ERRO 406. O pipeline de IA de cliente potencial foi interrompido: atividade muito esparsa para treinamento de modelo válido. Somente {} porcentagem de contatos tem atividade. |
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
| 102 | INFORMAÇÃO 102. Conduz à verificação de qualidade da IA: a contagem de oportunidades é: {}. |
| 103 | INFORMAÇÃO 103. Conduz a verificação de qualidade da IA: o teste de auc é baixo. Iniciar ajuste de parâmetro. Testando auc: {}. |
| 200 | AVISO 200. Conduz à verificação de qualidade da IA: a taxa de recursos firmográficos ausentes é: {}. |
| 201 | AVISO 201. Conduz à verificação de qualidade da IA: a taxa de recursos de atividade ausentes é: {}. |

## Próximas etapas

Ao seguir este tutorial, agora é possível criar e gerenciar pontuações com êxito. Consulte os seguintes documentos para obter mais detalhes:

* [Pontuação preditiva de conta e lead](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Monitorar trabalhos de pontuação preditiva de leads e contas](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
