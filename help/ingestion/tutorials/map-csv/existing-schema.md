---
keywords: Experience Platform;página inicial;tópicos populares;mapear csv;mapear arquivo csv;mapear arquivo csv para xdm;mapear csv para xdm;guia da interface do usuário;
solution: Experience Platform
title: Mapear um arquivo CSV para um esquema XDM existente
type: Tutorial
description: Este tutorial aborda como mapear um arquivo CSV para um esquema XDM existente usando a interface do usuário do Adobe Experience Platform.
exl-id: 15f55562-269d-421d-ad3a-5c10fb8f109c
source-git-commit: 15de9351203f6b43653042ab73ede17781486160
workflow-type: tm+mt
source-wordcount: '1018'
ht-degree: 1%

---

# Mapear um arquivo CSV para um esquema XDM existente

>[!NOTE]
>
>Este documento aborda como mapear um arquivo CSV para um esquema XDM existente. Para obter informações sobre como usar a ferramenta de recomendação de esquema gerada por IA (atualmente na versão beta), consulte o documento sobre [mapeamento de um arquivo CSV usando recomendações de aprendizado de máquina](./recommendations.md).

Para assimilar dados CSV em [!DNL Adobe Experience Platform], os dados devem ser mapeados para um esquema [!DNL Experience Data Model] (XDM). Este tutorial aborda como mapear um arquivo CSV para um esquema XDM usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer entendimento prático dos seguintes componentes do [!DNL Platform]:

- [[!DNL Experience Data Model (XDM System)]](../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Platform] organiza os dados de experiência do cliente.
- [Assimilação em lote](../../batch-ingestion/overview.md): o método pelo qual [!DNL Platform] assimila dados de arquivos de dados fornecidos pelo usuário.
- [Preparo de dados do Adobe Experience Platform](../../batch-ingestion/overview.md): um conjunto de recursos que permitem mapear e transformar dados assimilados para estarem em conformidade com esquemas XDM. A documentação sobre [Funções de preparação de dados](../../../data-prep/functions.md) é particularmente relevante para o mapeamento de esquema.

Este tutorial também requer que você já tenha criado um conjunto de dados para assimilar seus dados CSV no. Para obter etapas sobre como criar um conjunto de dados na interface, consulte o [tutorial de assimilação de dados](../ingest-batch-data.md).

## Escolher um destino

Faça logon em [[!DNL Adobe Experience Platform]](https://platform.adobe.com) e selecione **[!UICONTROL Fluxos de Trabalho]** na barra de navegação esquerda para acessar o espaço de trabalho **[!UICONTROL Fluxos de Trabalho]**.

Na tela **[!UICONTROL Workflows]**, selecione **[!UICONTROL Mapear CSV para esquema XDM]** na seção **[!UICONTROL Assimilação de dados]** e selecione **[!UICONTROL Iniciar]**.

![](../../images/tutorials/map-a-csv-file/workflows.png)

O fluxo de trabalho **[!UICONTROL Mapear CSV para esquema XDM]** é exibido, iniciando na etapa **[!UICONTROL Destino]**. Escolha um conjunto de dados para os dados de entrada que serão assimilados. Você pode usar um conjunto de dados existente ou criar um novo.

**Usar um conjunto de dados existente**

Para assimilar seus dados CSV em um conjunto de dados existente, selecione **[!UICONTROL Usar conjunto de dados existente]**. Você pode recuperar um conjunto de dados existente usando a função de pesquisa ou rolando pela lista de conjuntos de dados existentes no painel.

![](../../images/tutorials/map-a-csv-file/use-existing-dataset.png)

Para assimilar seus dados CSV em um novo conjunto de dados, selecione **[!UICONTROL Criar novo conjunto de dados]** e insira um nome e uma descrição para o conjunto de dados nos campos fornecidos. Selecione um esquema usando a função de pesquisa ou rolando pela lista de esquemas fornecida. Selecione **[!UICONTROL Avançar]** para continuar.

![](../../images/tutorials/map-a-csv-file/create-new-dataset.png)

## Adicionar dados

A etapa **[!UICONTROL Adicionar dados]** é exibida. Arraste e solte seu arquivo CSV no espaço fornecido ou selecione **[!UICONTROL Escolher arquivos]** para inserir manualmente seu arquivo CSV.

![](../../images/tutorials/map-a-csv-file/add-data.png)

A seção **[!UICONTROL Dados de amostra]** é exibida quando o arquivo é carregado, mostrando as primeiras dez linhas de dados. Depois de confirmar que os dados foram carregados conforme esperado, selecione **[!UICONTROL Avançar]**.

![](../../images/tutorials/map-a-csv-file/sample-data.png)

## Mapear campos CSV para campos de esquema XDM

A etapa **[!UICONTROL Mapping]** é exibida. As colunas do arquivo CSV estão listadas em **[!UICONTROL Campo Source]**, com seus campos de esquema XDM correspondentes listados em **[!UICONTROL Campo Target]**.

O [!DNL Platform] fornece automaticamente recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions.png)

Para aceitar todos os valores de mapeamento gerados automaticamente, marque a caixa de seleção denominada &quot;[!UICONTROL Aceitar todos os campos de destino]&quot;.

![](../../images/tutorials/map-a-csv-file/filled-mapping-with-suggestions.png)

Às vezes, mais de uma recomendação está disponível para o esquema de origem. Quando isso acontece, o cartão de mapeamento exibe a recomendação mais proeminente, seguida por um círculo azul que contém o número de recomendações adicionais disponíveis. Selecionar o ícone de lâmpada mostrará uma lista das recomendações adicionais. Você pode escolher uma das recomendações alternativas marcando a caixa de seleção ao lado da recomendação para a qual deseja mapear.

![](../../images/tutorials/map-a-csv-file/multiple-recommendations.png)

Como alternativa, você pode optar por mapear manualmente o esquema de origem para o esquema de destino. Passe o mouse sobre o schema de origem que deseja mapear e selecione o ícone de adição.

![](../../images/tutorials/map-a-csv-file/mapping-with-suggestions-and-buttons.png)

O popover **[!UICONTROL Mapear campo de origem para campo de destino]** é exibido. Aqui, você pode selecionar qual campo deseja mapear, seguido de **[!UICONTROL Salvar]** para adicionar o novo mapeamento.

![](../../images/tutorials/map-a-csv-file/manual-mapping.png)

Se quiser remover um dos mapeamentos, passe o mouse sobre esse mapeamento e selecione o ícone de subtração.

### Adicionar campo calculado {#add-calculated-field}

Os campos calculados permitem que valores sejam criados com base nos atributos no esquema de entrada. Esses valores podem ser atribuídos a atributos no esquema de destino e receber um nome e uma descrição para facilitar a referência.

Selecione o botão **[!UICONTROL Adicionar campo calculado]** para continuar.

![](../../images/tutorials/map-a-csv-file/add-calculated-field.png)

O painel **[!UICONTROL Criar campo calculado]** é exibido. A caixa de diálogo à esquerda contém os campos, funções e operadores compatíveis com os campos calculados. Selecione uma das guias para começar a adicionar funções, campos ou operadores ao editor de expressão.

![](../../images/tutorials/map-a-csv-file/create-calculated-fields.png)

| Tabulação | Descrição |
| --------- | ----------- |
| Campos | A guia fields lista campos e atributos disponíveis no schema de origem. |
| Funções | A guia functions lista as funções disponíveis para transformar os dados. Para saber mais sobre as funções que você pode usar em campos calculados, leia o guia em [usando funções de Preparo de Dados (Mapeador)](../../../data-prep/functions.md). |
| Operadores | A guia operators lista os operadores disponíveis para transformar os dados. |

Você pode adicionar campos, funções e operadores manualmente usando o editor de expressão no centro. Selecione o editor para começar a criar uma expressão.

![](../../images/tutorials/map-a-csv-file/create-calculated-field.png)

Selecione **[!UICONTROL Salvar]** para continuar.

A tela de mapeamento é exibida novamente com o campo de origem recém-criado. Aplique o campo de destino correspondente apropriado e selecione **[!UICONTROL Concluir]** para concluir o mapeamento.

![](../../images/tutorials/map-a-csv-file/new-calculated-field.png)

## Monitorar assimilação de dados

Depois que o arquivo CSV for mapeado e criado, você poderá monitorar os dados que estão sendo assimilados por meio dele. Para obter mais informações sobre monitoramento da assimilação de dados, consulte o tutorial em [monitoramento da assimilação de dados](../../../ingestion/quality/monitor-data-ingestion.md).

## Próximas etapas

Ao seguir este tutorial, você mapeou com êxito um arquivo CSV simples para um esquema XDM e o assimilou em [!DNL Platform]. Esses dados agora podem ser usados por serviços [!DNL Platform] downstream, como [!DNL Real-Time Customer Profile]. Consulte a visão geral de [[!DNL Real-Time Customer Profile]](../../../profile/home.md) para obter mais informações.

>[!TIP]
>
>Você também pode usar algoritmos de aprendizado de máquina (ML) para **gerar um esquema a partir de dados de exemplo** do espaço de trabalho Esquema. Esse fluxo de trabalho cria automaticamente um novo esquema com base na estrutura e no conteúdo do arquivo, garantindo que o esquema corresponda ao formato dos dados. Isso economiza tempo e aumenta a precisão ao definir a estrutura, os campos e os tipos de dados para grandes conjuntos de dados complexos. Consulte o [Guia de criação de esquema com assistência de ML](../../../xdm/ui/ml-assisted-schema-creation.md) para obter mais informações sobre este fluxo de trabalho.
