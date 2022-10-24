---
title: Gerenciar lead preditivo e pontuação de conta no Real-Time CDP B2B
type: Documentation
description: Este documento fornece informações sobre o gerenciamento do lead preditivo e do recurso de pontuação de conta no Experience Platform CDP B2B.
exl-id: fe7eb94e-5cf1-46bf-80e5-affe5735c998
source-git-commit: 14e3eff3ea2469023823a35ee1112568f5b5f4f7
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 2%

---

# Gerenciar lead preditivo e pontuação de conta no Adobe Real-time Customer Data Platform, B2B Edition

>[!NOTE]
>
>Somente usuários com permissão de Gerenciar AI B2B podem criar, alterar e excluir metas de pontuação.

Este tutorial o orienta pelas etapas para gerenciar pontuações do lead preditivo e do serviço de pontuação de contas. As metas de pontuação podem ser para perfil de pessoa ou perfil de conta

## Criar uma nova pontuação

Para criar uma nova pontuação, selecione a **[!UICONTROL Serviços]** na barra lateral e selecione **[!UICONTROL Criar pontuação]**.

![plas-new-score](../assets/../b2b-ai-ml-services/assets/plas-create-score.png)

O **[!UICONTROL Informações básicas]** for exibida, solicitando a seleção de um tipo de perfil, insira um nome e uma descrição opcional. Quando terminar, selecione **[!UICONTROL Próximo]**.

![plas-enter-basic-information](../assets/../b2b-ai-ml-services/assets/plas-basic-information.png)

O **[!UICONTROL Definir a meta]** será exibida. Selecione a seta suspensa e selecione um tipo de meta na janela suspensa que é exibida.

![plas-select-a-objetive](../assets/../b2b-ai-ml-services/assets/plas-define-goal.png)

O **[!UICONTROL Especificações da meta]** será aberta. Selecione a seta suspensa e, em seguida, selecione o nome do campo de meta na janela suspensa exibida.

![plas-select-a-objetive-field-name](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-name.png)

O **[!UICONTROL Condições das metas]** será exibida. Selecione a seta suspensa e selecione a condição na janela suspensa que é exibida.

![condição específica do objetivo](../assets/../b2b-ai-ml-services/assets/plas-goal-specidics-condition.png)

O **[!UICONTROL Valor da meta]** é exibido. Em seguida, configure [!UICONTROL Especificações da meta]. Selecione o [!UICONTROL Inserir Valor do Campo] e insira o valor da meta.

>[!NOTE]
>
>Vários valores de meta podem ser adicionados.

![plas-objetivo-específico-valor de campo](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-field-value.png)

Para adicionar mais campos, selecione **[!UICONTROL Adicionar campo]**.

![evento do complemento plas-objetivo-específico](../assets/../b2b-ai-ml-services/assets/plas-goal-specifics-add-event.png)

Para configurar o período de previsão, selecione a seta suspensa e selecione o período de tempo escolhido.

![plas-prediction-timeframe](../assets/../b2b-ai-ml-services/assets/plas-prediction-timeframe.png)

A política de mesclagem selecionada determina como os valores de campo de um perfil de pessoa são selecionados. Usando a seta suspensa, selecione a política de mesclagem escolhida e selecione **[!UICONTROL Concluir]**.

O **[!UICONTROL A configuração de pontuação está concluída]** é exibida confirmando que a nova pontuação foi criada. Selecionar **[!UICONTROL OK]**.

![plas-score-complete](../assets/../b2b-ai-ml-services/assets/plas-score-complete.png)

>[!NOTE]
>
>Pode levar até 24 horas para que cada processo de pontuação seja concluído.

Você volta ao **[!UICONTROL Serviços]** , onde é possível visualizar a nova pontuação criada na lista de pontuações.

![plas-score-created](../assets/../b2b-ai-ml-services/assets/plas-score-created.png)

Selecione a pontuação para exibir detalhes e informações adicionais sobre os detalhes da última execução.

![plas-score-additional-information](../assets/../b2b-ai-ml-services/assets/plas-score-info.png)

Para obter informações mais detalhadas sobre os códigos de erro que podem ser vistos nos detalhes da última execução, consulte a seção em [códigos de erro de pipeline do AI](#leads-ai-pipeline-error-codes) neste documento.

## Editar uma pontuação

Para editar uma pontuação, selecione uma pontuação no **[!UICONTROL Serviços]** e selecione **[!UICONTROL Editar]** no painel de detalhes adicionais, no lado direito da tela.

![plas-edit-score](../assets/../b2b-ai-ml-services/assets/plas-edit-score.png)

O **[!UICONTROL Editar instância]** é exibida, onde é possível editar a descrição da pontuação. Faça as alterações e selecione **[!UICONTROL Salvar]**.

![plas-edit-save](../assets/../b2b-ai-ml-services/assets/plas-edit-save.png)

>[!NOTE]
>
>A configuração de pontuação não pode ser alterada, pois isso acionará o retreinamento e a nova pontuação do modelo. É equivalente a excluir a pontuação e criar uma nova pontuação. Para editar a configuração da pontuação, será necessário clonar essa pontuação ou criar uma nova pontuação.

Você volta ao **[!UICONTROL Serviços]** guia . Selecione a pontuação para exibir os detalhes de descrição atualizados no painel de detalhes adicionais no lado direito da tela.

## Clonar uma pontuação

Para clonar uma pontuação, selecione uma pontuação no **[!UICONTROL Serviços]** e selecione **[!UICONTROL Clonar]** no painel de detalhes adicionais, no lado direito da tela.

![pontuação plas-clone](../assets/../b2b-ai-ml-services/assets/plas-clone-score.png)

O **[!UICONTROL Informações básicas]** será exibida. O tipo de perfil, o nome e a descrição são clonados a partir da pontuação original. Altere esses detalhes e selecione **[!UICONTROL Próximo]**.

![plas-clone-basic-info](../assets/../b2b-ai-ml-services/assets/plas-clone-basic-info.png)

O **[!UICONTROL Definir a meta]** será exibida. Conclua a seção de metas da mesma maneira que faria ao criar uma nova pontuação e selecione **[!UICONTROL Concluir]**.

Você volta ao **[!UICONTROL Serviços]** , onde é possível ver a pontuação recém-clonada na lista.

>[!NOTE]
>
>O **[!UICONTROL Definir a meta]** não é clonada a partir da pontuação original.

## Excluir uma pontuação

Para excluir uma pontuação, selecione uma pontuação no **[!UICONTROL Serviços]** e selecione **[!UICONTROL Excluir]** no painel de detalhes adicionais, no lado direito da tela.

![plas-delete-score](../assets/../b2b-ai-ml-services/assets/plas-delete-score.png)

O **[!UICONTROL Excluir documentação]** a caixa de diálogo de confirmação é exibida. Selecione **[!UICONTROL Delete]**.

![plas-delete-score-confirmation](../assets/../b2b-ai-ml-services/assets/plas-delete-score-confirmation.png)

>[!NOTE]
>
>A exclusão da definição de pontuação também excluiria todas as pontuações previstas no perfil de pessoa ou no perfil de conta, mas não o grupo de campos criado para a definição de pontuação. O grupo de campos será deixado &quot;órfão&quot; no modelo de dados.

Você volta ao **[!UICONTROL Serviços]** , onde não é mais possível visualizar a pontuação na lista.

## Códigos de erro de pipeline AI de clientes potenciais

| Código de erro | Mensagem de erro |
| --- | --- |
| 401° | ERRO 401. O pipeline de AI de clientes potenciais parou: não existem contas válidas suficientes para a classificação de contas. Contagem de contas: {}. |
| 402 | ERRO 402. O pipeline de AI de clientes potenciais parou: não há contatos válidos suficientes para pontuação de contatos. Contagem de contatos: {}. |
| 403 | ERRO 403. O pipeline de AI de clientes potenciais parou: volume de atividade insuficiente para o treinamento do modelo. Contagem de eventos: {}. |
| 404 | ERRO 404. O pipeline de AI de clientes potenciais parou: conversões insuficientes para o treinamento do modelo. Contagem de conversões: {}. |
| 405 | ERRO 405. O pipeline de AI de clientes potenciais parou: atividade muito escassa para treinamento de modelo válido. Apenas {} por cento das contas tem atividade. |
| 406 | ERRO 406. O pipeline de AI de clientes potenciais parou: atividade muito escassa para treinamento de modelo válido. Somente {} por cento dos contatos tem atividade. |
| 407 | ERRO 407. O pipeline de AI de clientes potenciais parou: os tipos de atividades de dados de pontuação não correspondem aos dados de treinamento. |
| 408 | ERRO 408. O pipeline de AI de clientes potenciais parou: a taxa de falta é demasiado elevada para funcionalidades de atividade. Taxa em falta: {}. |
| 409 | ERRO 409. O pipeline de AI de clientes potenciais parou: o auc do teste é muito baixo. Auc do teste: {}. |
| 410 | ERRO 410. O pipeline de AI de clientes potenciais parou: o teste de auc é muito baixo após o ajuste do parâmetro. Auc do teste: {}. |
| 411º | ERRO 411. O pipeline de AI de clientes potenciais parou: os dados de treinamento não têm conversões suficientes para produzir um modelo confiável. Conversões: {}. |
| 412 | ERRO 412. O pipeline de AI de clientes potenciais parou: os dados de teste não têm conversão para calcular AUC-ROC. |

| Código de aviso/informação | Mensagem |
| --- | --- |
| 100 | INFORMAÇÕES 100. Leia a verificação de qualidade de AI: a contagem de contas é: {}. |
| 101 | INFORMAÇÕES 101. Leia a verificação de qualidade de AI: a contagem de contatos é: {}. |
| 102 | INFORMAÇÕES 102. Leia a verificação de qualidade de AI: a contagem de oportunidades é: {}. |
| 103 | INFORMAÇÕES 103. Leia a verificação de qualidade de AI: o teste de auc está baixo. Inicie o ajuste do parâmetro. Testando auc: {}. |
| 200 | AVISO 200. Leia a verificação de qualidade de AI: a taxa de utilização dos elementos de primeira grafia é: {}. |
| 201 | AVISO 201. Leia a verificação de qualidade de AI: a taxa ausente dos recursos da atividade é: {}. |

## Próximas etapas

Ao seguir este tutorial, agora é possível criar e gerenciar pontuações com êxito. Consulte os seguintes documentos para obter mais detalhes:

* [Lead preditivo e pontuação de conta](/help/rtcdp/b2b-ai-ml-services/predictive-lead-and-account-scoring.md)
* [Monitorar trabalhos preditivos de lead e pontuação de conta](/help/dataflows/ui/b2b/monitor-profile-enrichment.md)
