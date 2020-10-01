---
keywords: Experience Platform;home;popular topics;map csv;map csv file;map csv file to xdm;map csv to xdm;ui guide;
solution: Experience Platform
title: Mapear um arquivo CSV para um schema XDM
topic: tutorial
type: Tutorial
description: Este tutorial aborda como mapear um arquivo CSV para um schema XDM usando a interface do usuário do Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: 7adf18e4251f377fee586c8a0f23b89acd75afca
workflow-type: tm+mt
source-wordcount: '886'
ht-degree: 1%

---


# Mapear um arquivo CSV para um schema XDM

Para assimilar dados CSV, [!DNL Adobe Experience Platform]os dados devem ser mapeados para um schema [!DNL Experience Data Model] (XDM). Este tutorial aborda como mapear um arquivo CSV para um schema XDM usando a interface do [!DNL Platform] usuário.

Além disso, o apêndice deste tutorial fornece mais informações sobre o uso de funções [de](#mapping-functions)mapeamento.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do [!DNL Platform]:

- [[!DNL Experience Data Model (Sistema XDM)]](../../xdm/home.md): A estrutura padronizada pela qual [!DNL Platform] organiza os dados de experiência do cliente.
- [[!DNL ingestão em lote]](../batch-ingestion/overview.md): O método pelo qual [!DNL Platform] ingere dados de arquivos de dados fornecidos pelo usuário.

Este tutorial também requer que você já tenha criado um conjunto de dados para assimilar seus dados CSV. Para obter etapas sobre como criar um conjunto de dados na interface do usuário, consulte o tutorial [de assimilação de](./ingest-batch-data.md)dados.

## Escolher um destino

Faça logon em [[!DNL Adobe Experience Platform]](https://platform.adobe.com) e selecione **[!UICONTROL Workflows]** na barra de navegação esquerda para acessar a área de trabalho de **[!UICONTROL Workflows]** .

Na tela **[!UICONTROL Workflows]** , selecione **[!UICONTROL Mapear o schema]** CSV para XDM na seção de ingestão **[!UICONTROL de]** dados e selecione **[!UICONTROL Iniciar]**.

![](../images/tutorials/map-a-csv-file/workflows.png)

O fluxo de trabalho **[!UICONTROL Mapear CSV para schema]** XDM é exibido, começando na etapa **[!UICONTROL Destino]** . Escolha um conjunto de dados para os dados de entrada a serem ingeridos. Você pode usar um conjunto de dados existente ou criar um novo.

**Usar um conjunto de dados existente**

Para assimilar seus dados CSV em um conjunto de dados existente, selecione **[!UICONTROL Usar conjunto de dados]** existente. Você pode recuperar um conjunto de dados existente usando a função de pesquisa ou percorrendo a lista de conjuntos de dados existentes no painel.

![](../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Para assimilar seus dados CSV em um novo conjunto de dados, selecione **[!UICONTROL Criar novo conjunto de dados]** e insira um nome e uma descrição para o conjunto de dados nos campos fornecidos. Selecione um schema usando a função de pesquisa ou percorrendo a lista dos schemas fornecidos. Selecione **[!UICONTROL Avançar]** para continuar.

![](../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Adicionar dados

A etapa **[!UICONTROL Adicionar dados]** é exibida. Arraste e solte o arquivo CSV no espaço fornecido ou selecione **[!UICONTROL Escolher arquivos]** para inserir manualmente o arquivo CSV.

![](../images/tutorials/map-a-csv-file/add-data.png)

A seção Dados **[!UICONTROL de]** amostra é exibida assim que o arquivo é carregado, mostrando as primeiras dez linhas de dados. Depois de confirmar que os dados foram carregados como esperado, selecione **[!UICONTROL Avançar]**.

![](../images/tutorials/map-a-csv-file/sample-data.png)

## Mapear campos CSV para campos de schema XDM

A etapa **[!UICONTROL Mapeamento]** é exibida. As colunas do arquivo CSV são listadas em Campo **[!UICONTROL de]** origem, com seus campos de schema XDM correspondentes listados em Campo **[!UICONTROL de]** Público alvo. Os campos de público alvo não selecionados são contornados em vermelho. Você pode usar a opção de filtrar campos para restringir a lista dos campos de origem disponíveis.

>[!TIP]
>
>[!DNL Platform] fornece recomendações inteligentes para campos mapeados automaticamente com base no schema ou conjunto de dados do público alvo selecionado. É possível ajustar manualmente as regras de mapeamento para atender aos casos de uso.

Para mapear uma coluna CSV para um campo XDM, selecione o ícone de schema ao lado do campo de público alvo correspondente da coluna.

![](../images/tutorials/map-a-csv-file/mapping.png)

A janela **[!UICONTROL Selecionar campo]** schema é exibida. Aqui, você pode navegar pela estrutura do schema XDM e localizar o campo para o qual deseja mapear a coluna CSV. Clique em um campo XDM para selecioná-lo e, em seguida, clique em **[!UICONTROL Selecionar]**.

![](../images/tutorials/map-a-csv-file/select-schema-field.png)

Depois de concluir as etapas para os campos de origem não mapeados restantes, a tela **[!UICONTROL Mapeamento]** será exibida novamente com o campo XDM selecionado que agora aparece em Campo **[!UICONTROL de]** Público alvo.

![](../images/tutorials/map-a-csv-file/field-mapped.png)

Ao mapear campos, também é possível incluir funções para calcular valores com base nos campos de origem de entrada. Consulte a seção de funções [de](#mapping-functions) mapeamento no apêndice para obter mais informações.

### Adicionar campo calculado

Campos calculados permitem que valores sejam criados com base nos atributos no schema de entrada. Esses valores podem ser atribuídos aos atributos no schema do público alvo e receber um nome e uma descrição para facilitar a referência.

Selecione o botão **[!UICONTROL Adicionar campo]** calculado para continuar.

![](../images/tutorials/map-a-csv-file/add-calculate-field.png)

O painel **[!UICONTROL Criar campo]** calculado é exibido. A caixa de diálogo esquerda contém os campos, as funções e os operadores suportados nos campos calculados. Selecione uma das guias para adicionar funções, campos ou operadores ao editor de expressões.

![](../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabulação | Descrição |
| --------- | ----------- |
| Campos | A guia campos lista campos e atributos disponíveis no schema de origem. |
| Funções | A guia funções lista as funções disponíveis para transformar os dados. |
| Operadores | A guia operadores lista os operadores disponíveis para transformar os dados. |

É possível adicionar manualmente campos, funções e operadores usando o editor de expressão no centro. Selecione o editor para criar uma expressão no start.

![](../images/tutorials/map-a-csv-file/expression-editor.png)

Selecione **[!UICONTROL Salvar]** para continuar.

A tela de mapeamento reaparece com o campo de origem recém-criado. Aplique o campo de público alvo correspondente apropriado e selecione **[!UICONTROL Concluir]** para concluir o mapeamento.

![](../images/tutorials/map-a-csv-file/new-field.png)

## Monitore seu fluxo de dados

Depois que o arquivo CSV for mapeado e criado, você poderá monitorar os dados que estão sendo assimilados por meio dele. Para obter mais informações sobre como monitorar fluxos de dados, consulte o tutorial sobre como [monitorar fluxos de dados](../../ingestion/quality/monitor-data-flows.md)de transmissão contínua.

## Uso de funções de mapeamento

Para usar uma função, digite-a em Campo **[!UICONTROL de]** origem com a sintaxe e as entradas apropriadas.

Por exemplo, para concatenar campos CSV de **cidade** e **país** e atribuí-los ao campo XDM de **cidade** , defina o campo de origem como `concat(city, ", ", county)`.

![](../images/tutorials/map-a-csv-file/mapping-function.png)

Para saber mais sobre como mapear colunas para campos XDM, leia o guia sobre como [usar funções](../../data-prep/functions.md)de Prep de dados (Mapeador).

## Próximas etapas

Ao seguir este tutorial, você mapeou com êxito um arquivo CSV simples para um schema XDM e o assimilou [!DNL Platform]. Esses dados agora podem ser usados por [!DNL Platform] serviços de downstream, como [!DNL Real-time Customer Profile]. Consulte a visão geral do [[!DNL Real-time Customer Perfil]](../../profile/home.md) para obter mais informações.
