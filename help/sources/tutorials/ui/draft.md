---
title: Rascunhos de fluxos de dados na interface do
description: Saiba como salvar seus fluxos de dados como rascunho e publicá-los posteriormente, ao usar o espaço de trabalho de fontes.
exl-id: ee00798e-152a-4618-acb3-db40f2f55fae
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '591'
ht-degree: 0%

---

# Rascunhos de fluxos de dados na interface do

Salve o progresso do fluxo de trabalho de assimilação de dados não concluído definindo o fluxo de dados para um status de rascunho. Você pode retomar e concluir seus fluxos de dados de rascunho posteriormente.

Este documento fornece etapas sobre como salvar seus fluxos de dados ao usar o espaço de trabalho de origens na interface do Adobe Experience Platform.

## Introdução

Este documento requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Fontes](../../home.md): o Experience Platform permite que os dados sejam assimilados de várias fontes e, ao mesmo tempo, fornece a capacidade de estruturar, rotular e aprimorar os dados recebidos usando os serviços da plataforma.

## Salvar um fluxo de dados como rascunho

Você pode pausar o progresso da criação do fluxo de dados a qualquer momento depois de selecionar os dados que trará para a Plataforma.

Por exemplo, se você quiser salvar seu progresso durante a etapa de detalhes do fluxo de dados, selecione **[!UICONTROL Salvar como rascunho]**.

![A etapa de detalhes do fluxo de dados do fluxo de trabalho de fontes com Salvar como rascunho selecionado.](../../images/tutorials/draft/save-as-draft.png)

Depois de salvar o rascunho, você será levado para a página da conta, onde poderá ver uma lista dos fluxos de dados existentes, incluindo os rascunhos.

![Uma lista de fluxos de dados para uma determinada conta.](../../images/tutorials/draft/draft-dataflow.png)

>[!TIP]
>
>Os fluxos de dados de rascunho não serão habilitados e terão seu status definido como `draft`.

Para continuar no rascunho, selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Atualizar fluxo de dados]**.

>[!NOTE]
>
>Se o rascunho incluir informações de agendamento, a janela suspensa também oferecerá a opção de **[!UICONTROL Editar agendamento]**.

![Uma janela suspensa com fluxo de dados de atualização selecionado.](../../images/tutorials/draft/update-dataflow.png)

### Acessar seus rascunhos do catálogo de origem

Você também pode acessar seus fluxos de dados de rascunho pelo catálogo de fluxos de dados. Selecione **[!UICONTROL Fluxos de dados]** no cabeçalho superior para acessar o catálogo de fluxos de dados. Aqui, encontre seu rascunho da lista de fluxos de dados existentes em sua organização, selecione as reticências (`...`) ao lado do nome e selecione **[!UICONTROL Atualizar fluxo de dados]**.

![Uma lista de fluxos de dados para uma determinada organização.](../../images/tutorials/draft/catalog-access.png)

## Publish seu fluxo de dados de rascunho

Você retornará à etapa [!UICONTROL Adicionar dados] do fluxo de trabalho de fontes, onde é possível reconfirmar o formato dos dados e continuar o progresso no fluxo de dados.

Depois de confirmar a formatação, o delimitador e o tipo de compactação dos dados, selecione **[!UICONTROL Avançar]** para continuar.

![A etapa de adição de dados do fluxo de trabalho de fontes.](../../images/tutorials/draft/select-data.png)

Em seguida, confirme os detalhes do fluxo de dados. Use a interface de detalhes do fluxo de dados para atualizar as configurações relacionadas ao nome, à descrição, à assimilação parcial, às configurações de diagnóstico de erros e às preferências de alerta do fluxo de dados.

Após concluir as configurações, selecione **[!UICONTROL Avançar]** para continuar.

![A etapa de detalhes do fluxo de dados do fluxo de trabalho de fontes.](../../images/tutorials/draft/dataflow-detail.png)

A etapa [!UICONTROL Mapping] é exibida. Durante essa etapa, você pode reconfigurar as configurações de mapeamento do fluxo de dados. Para obter um guia abrangente sobre as funções de preparação de dados usadas para mapeamento, visite o [guia da interface do usuário de preparação de dados](../../../data-prep/ui/mapping.md).

Depois de concluir a reconfiguração de mapeamento, selecione **[!UICONTROL Avançar]** para continuar.

![A etapa de mapeamento do fluxo de trabalho de origens.](../../images/tutorials/draft/mapping.png)

Use a etapa [!UICONTROL Agendamento] para estabelecer um agendamento de assimilação para seu fluxo de dados. Você pode definir a frequência de assimilação como `once`, `minute`, `hour`, `day` ou `week`. Quando terminar, selecione **[!UICONTROL Avançar]** para continuar.

![A etapa de agendamento do fluxo de trabalho de fontes.](../../images/tutorials/draft/scheduling.png)

Finalmente, revise os detalhes do seu fluxo de dados e selecione **[!UICONTROL Concluir]** para publicar seu rascunho.

![A etapa de revisão do fluxo de trabalho de fontes.](../../images/tutorials/draft/review.png)

Depois de salvar e publicar um rascunho, o fluxo de dados será ativado e você não poderá mais redefini-lo como rascunho.

## Próximas etapas

Seguindo este tutorial, você aprendeu a salvar seu progresso e definir um fluxo de dados como rascunho. Para obter mais informações sobre origens, visite a [visão geral das origens](../../home.md).
