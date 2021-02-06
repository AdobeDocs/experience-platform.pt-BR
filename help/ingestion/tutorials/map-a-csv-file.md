---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Mapear um arquivo CSV para um Schema XDM
topic: tutorial
type: Tutorial
description: Este tutorial aborda como mapear um arquivo CSV para um schema XDM usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 089a4d517476b614521d1db4718966e3ebb13064
workflow-type: tm+mt
source-wordcount: '882'
ht-degree: 1%

---


# Mapear um arquivo CSV para um schema XDM

Para assimilar dados CSV em [!DNL Adobe Experience Platform], os dados devem ser mapeados para um schema [!DNL Experience Data Model] (XDM). Este tutorial aborda como mapear um arquivo CSV para um schema XDM usando a interface do usuário [!DNL Platform].

Além disso, o apêndice deste tutorial fornece mais informações sobre o uso de [funções de mapeamento](#mapping-functions).

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes de [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente.
- [[!DNL Batch ingestion]](../batch-ingestion/overview.md): O método pelo qual  [!DNL Platform] ingere dados de arquivos de dados fornecidos pelo usuário.

Este tutorial também requer que você já tenha criado um conjunto de dados para assimilar seus dados CSV. Para obter etapas sobre como criar um conjunto de dados na interface do usuário, consulte o [tutorial de assimilação de dados](./ingest-batch-data.md).

## Escolher um destino

Faça logon em [[!DNL Adobe Experience Platform]](https://platform.adobe.com) e selecione **[!UICONTROL Workflows]** na barra de navegação esquerda para acessar a área de trabalho **[!UICONTROL Workflows]**.

Na tela **[!UICONTROL Workflows]**, selecione **[!UICONTROL Mapear CSV para schema XDM]** na seção **[!UICONTROL Inclusão de dados]** e selecione **[!UICONTROL Iniciar]**.

![](../images/tutorials/map-a-csv-file/workflows.png)

O fluxo de trabalho **[!UICONTROL Mapear CSV para schema XDM]** é exibido, começando na etapa **[!UICONTROL Destino]**. Escolha um conjunto de dados para os dados de entrada a serem ingeridos. Você pode usar um conjunto de dados existente ou criar um novo.

**Usar um conjunto de dados existente**

Para assimilar seus dados CSV em um conjunto de dados existente, selecione **[!UICONTROL Usar conjunto de dados existente]**. Você pode recuperar um conjunto de dados existente usando a função de pesquisa ou percorrendo a lista de conjuntos de dados existentes no painel.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Para assimilar seus dados CSV em um novo conjunto de dados, selecione **[!UICONTROL Criar novo conjunto de dados]** e insira um nome e uma descrição para o conjunto de dados nos campos fornecidos. Selecione um schema usando a função de pesquisa ou percorrendo a lista dos schemas fornecidos. Selecione **[!UICONTROL Próximo]** para prosseguir.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Adicionar dados

A etapa **[!UICONTROL Adicionar dados]** é exibida. Arraste e solte o arquivo CSV no espaço fornecido ou selecione **[!UICONTROL Escolher arquivos]** para inserir manualmente o arquivo CSV.

![](../images/tutorials/map-a-csv-file/add-data.png)

A seção **[!UICONTROL Dados de amostra]** aparece assim que o arquivo é carregado, mostrando as primeiras dez linhas de dados. Depois de confirmar que os dados foram carregados conforme esperado, selecione **[!UICONTROL Next]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Mapear campos CSV para campos de schema XDM

A etapa **[!UICONTROL Mapeamento]** é exibida. As colunas do arquivo CSV são listadas em **[!UICONTROL Campo de origem]**, com seus campos de schema XDM correspondentes listados em **[!UICONTROL Campo de Público alvo]**.

[!DNL Platform] fornece recomendações inteligentes para campos mapeados automaticamente com base no schema ou conjunto de dados do público alvo selecionado. É possível ajustar manualmente as regras de mapeamento para atender aos casos de uso.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Para aceitar todos os valores de mapeamento de geração automática, marque a caixa de seleção &quot;[!UICONTROL Aceitar todos os campos de público alvo]&quot;.

![](../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

Às vezes, mais de uma recomendação está disponível para o schema de origem. Quando isso ocorre, o cartão de mapeamento exibe a recomendação mais destacada, seguida por um círculo azul que contém o número de recomendações adicionais disponíveis. Selecionar o ícone da lâmpada mostrará uma lista das recomendações adicionais. Você pode escolher uma das recomendações alternativas marcando a caixa de seleção ao lado da recomendação para a qual deseja mapear.

![](../images/tutorials/map-a-csv-file/multiple-recommendations.png)

Como alternativa, você pode optar por mapear manualmente o schema de origem para o schema do público alvo. Passe o mouse sobre o schema de origem que deseja mapear e selecione o ícone de adição.

![](../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

A janela **[!UICONTROL Mapear origem para campo de público alvo]** é exibida. Aqui, você pode selecionar qual campo deseja ser mapeado, seguido por **[!UICONTROL Salvar]** para adicionar seu novo mapeamento.

![](../images/tutorials/map-a-csv-file/manual-mapping.png)

Se desejar remover um dos mapeamentos, passe o mouse sobre esse mapeamento e selecione o ícone de menos.

### Adicionar campo calculado

Campos calculados permitem que valores sejam criados com base nos atributos no schema de entrada. Esses valores podem ser atribuídos aos atributos no schema do público alvo e receber um nome e uma descrição para facilitar a referência.

Selecione o botão **[!UICONTROL Adicionar campo calculado]** para continuar.

![](../images/tutorials/map-a-csv-file/add-calculated-field.png)

O painel **[!UICONTROL Criar campo calculado]** é exibido. A caixa de diálogo esquerda contém os campos, as funções e os operadores suportados nos campos calculados. Selecione uma das guias para adicionar funções, campos ou operadores ao editor de expressões.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabulação | Descrição |
| --------- | ----------- |
| Campos | A guia campos lista campos e atributos disponíveis no schema de origem. |
| Funções | A guia funções lista as funções disponíveis para transformar os dados. Para saber mais sobre as funções que você pode usar nos campos calculados, leia o guia em [usando as funções de Prep de dados (Mapeador)](../../data-prep/functions.md). |
| Operadores | A guia operadores lista os operadores disponíveis para transformar os dados. |

É possível adicionar manualmente campos, funções e operadores usando o editor de expressão no centro. Selecione o editor para criar uma expressão no start.

![](../images/tutorials/map-a-csv-file/create-calculated-field.png)

Selecione **[!UICONTROL Salvar]** para continuar.

A tela de mapeamento reaparece com o campo de origem recém-criado. Aplique o campo de público alvo correspondente apropriado e selecione **[!UICONTROL Finalizar]** para concluir o mapeamento.

![](../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Monitorar ingestão de dados

Depois que o arquivo CSV for mapeado e criado, você poderá monitorar os dados que estão sendo assimilados por meio dele. Para obter mais informações sobre como monitorar a ingestão de dados, consulte o tutorial em [monitorando a ingestão de dados](../../ingestion/quality/monitor-data-ingestion.md).

## Próximas etapas

Ao seguir este tutorial, você mapeou com êxito um arquivo CSV simples para um schema XDM e o assimilou em [!DNL Platform]. Esses dados agora podem ser usados por serviços downstream [!DNL Platform], como [!DNL Real-time Customer Profile]. Consulte a visão geral de [[!DNL Real-time Customer Profile]](../../profile/home.md) para obter mais informações.
