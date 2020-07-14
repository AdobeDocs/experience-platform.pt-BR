---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Configurar um fluxo de dados para um conector de lote de armazenamentos em nuvem na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 168ac3a3ab9f475cb26dc8138cbc90a3e35c836d
workflow-type: tm+mt
source-wordcount: '1226'
ht-degree: 0%

---


# Configurar um fluxo de dados para um conector de lote de armazenamentos em nuvem na interface do usuário

Um fluxo de dados é uma tarefa programada que recupera e ingere dados de uma fonte para um [!DNL Platform] conjunto de dados. Este tutorial fornece etapas para configurar um novo fluxo de dados usando o conector base do armazenamento em nuvem.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Além disso, este tutorial requer que você já tenha criado um conector de armazenamento em nuvem. Uma lista de tutoriais para criar diferentes conectores de armazenamento de nuvem na interface do usuário pode ser encontrada na visão geral [dos conectores de](../../../../home.md)origem.

### Formatos de arquivo não suportados

[!DNL Experience Platform] oferece suporte aos seguintes formatos de arquivo para serem assimilados de armazenamentos externos:

* Valores separados por delimitador (DSV): Atualmente, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgulas. O valor dos cabeçalhos de campo nos arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
* [!DNL JavaScript Object Notation] (JSON): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
* [!DNL Apache Parquet]: Os arquivos de dados formatados em parâmetro devem ser compatíveis com XDM.

## Selecionar dados

Depois de criar o conector de armazenamento em nuvem, a etapa *[!UICONTROL Selecionar dados]* é exibida, fornecendo uma interface interativa para explorar a hierarquia de armazenamentos em nuvem.

* A metade esquerda da interface é um navegador de diretório que exibe os arquivos e diretórios do servidor.
* A metade direita da interface permite que você pré-visualização até 100 linhas de dados de um arquivo compatível.

Clicar em uma pasta listada permite que você transfira a hierarquia de pastas para pastas mais profundas. Depois que você tiver um arquivo ou pasta compatível selecionado, a lista suspensa **[!UICONTROL Selecionar formato]** de dados será exibida, onde você poderá escolher um formato para exibir os dados na janela de pré-visualização.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

Quando a janela pré-visualização for preenchida, você poderá clicar em **[!UICONTROL Avançar]** para fazer upload de todos os arquivos dentro da pasta selecionada. Se desejar fazer upload para um arquivo específico, selecione-o na lista antes de clicar em **[!UICONTROL Avançar]**.

>[!NOTE]
>
>Os formatos de arquivo suportados incluem CSV, JSON e Parquet. Os arquivos JSON e Parquet devem ser compatíveis com XDM.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-next.png)

## Mapear campos de dados para um schema XDM

A etapa *[!UICONTROL Mapeamento]* é exibida, fornecendo uma interface interativa para mapear os dados de origem para um [!DNL Platform] conjunto de dados. Os arquivos de origem formatados em JSON ou Parquet devem ser compatíveis com XDM e não exigem a configuração manual do mapeamento. Os arquivos CSV, inversamente, exigem que você configure explicitamente o mapeamento, mas permitem que você escolha quais campos de dados de origem serão mapeados.

Escolha um conjunto de dados para os dados de entrada a serem ingeridos. Você pode usar um conjunto de dados existente ou criar um novo.

**Usar um conjunto de dados existente**

Para assimilar dados em um conjunto de dados existente, selecione **[!UICONTROL Usar conjunto de dados]** existente e clique no ícone do conjunto de dados.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

A caixa de diálogo _Selecionar conjunto de dados_ é exibida. Encontre o conjunto de dados que deseja usar, selecione-o e clique em **[!UICONTROL Continuar]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-data.png)

**Usar um novo conjunto de dados**

Para assimilar dados em um novo conjunto de dados, selecione **[!UICONTROL Criar novo conjunto de dados]** e insira um nome e uma descrição para o conjunto de dados nos campos fornecidos. Em seguida, clique no ícone schema.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-new-schema.png)

A caixa de diálogo _Selecionar schema_ é exibida. Selecione o schema que deseja aplicar ao novo conjunto de dados e clique em **[!UICONTROL Concluído]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

Com base em suas necessidades, você pode optar por mapear os campos diretamente ou usar as funções do mapeador para transformar dados de origem para derivar valores calculados ou calculados. Para obter mais informações sobre funções de mapeamento e mapeamento de dados, consulte o tutorial sobre como [mapear dados CSV para campos](../../../../../ingestion/tutorials/map-a-csv-file.md)de schema XDM.

Depois que os dados de origem forem mapeados, clique em **[!UICONTROL Avançar]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

## Execuções de ingestão agendada

A etapa *[!UICONTROL Agendamento]* é exibida, permitindo que você configure um agendamento de ingestão para assimilar automaticamente os dados de origem selecionados usando os mapeamentos configurados. A tabela a seguir descreve os diferentes campos configuráveis para programação:

| Campo | Descrição |
| --- | --- |
| Frequência | As frequências selecionáveis incluem Minuto, Hora, Dia e Semana. |
| Intervalo | Um número inteiro que define o intervalo para a frequência selecionada. |
| hora do Start | Um carimbo de data e hora UTC para o qual ocorrerá a primeira ingestão. |
| Backfill | Um valor booliano que determina quais dados são inicialmente assimilados. Se o *[!UICONTROL preenchimento retroativo]* estiver ativado, todos os arquivos atuais no caminho especificado serão ingeridos durante a primeira ingestão programada. Se o *[!UICONTROL preenchimento retroativo]* estiver desativado, somente os arquivos carregados entre a primeira execução da ingestão e a hora *[!UICONTROL do]* Start serão assimilados. Os arquivos carregados antes da hora *[!UICONTROL do]* Start não serão ingeridos. |

Os fluxos de dados são projetados para assimilar dados automaticamente de acordo com uma programação. Se desejar ingerir apenas uma vez por meio desse fluxo de trabalho, você pode fazer isso configurando a **[!UICONTROL Frequência]** para &quot;Dia&quot; e aplicando um número muito grande para o **[!UICONTROL Intervalo]**, como 10000 ou semelhante.

Forneça os valores para o agendamento e clique em **Avançar**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling.png)

## Dê um nome ao seu fluxo de dados

A etapa de fluxo *[!UICONTROL de]* Nome é exibida, permitindo que você nomeie e forneça uma breve descrição sobre seu novo fluxo de dados.

Forneça valores para o fluxo de dados e clique em **[!UICONTROL Avançar]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/name-your-dataflow.png)

### Revisar seu fluxo de dados

A etapa *[!UICONTROL Revisar]* é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* *[!UICONTROL Detalhes]* da fonte: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* *[!UICONTROL Detalhes]* do Público alvo: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o schema ao qual o conjunto de dados adere.
* *[!UICONTROL Detalhes]* da programação: Mostra o período ativo, a frequência e o intervalo do agendamento da ingestão.

Depois de revisar seu fluxo de dados, clique em **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Monitore e exclua seu fluxo de dados

Depois que seu fluxo de dados de armazenamento em nuvem for criado, você poderá monitorar os dados que estão sendo assimilados por ele. Para obter mais informações sobre monitoramento e exclusão de fluxos de dados, consulte o tutorial sobre [monitoramento de fluxos de dados](../../../../../ingestion/quality/monitor-data-flows.md).

## Próximas etapas

Ao seguir este tutorial, você criou com êxito um fluxo de dados para trazer dados de um armazenamento de nuvem externo e obteve insight sobre conjuntos de dados de monitoramento. Para saber mais sobre como criar fluxos de dados, você pode complementar seu aprendizado assistindo ao vídeo abaixo. Além disso, os dados de entrada agora podem ser usados por [!DNL Platform] serviços de downstream, como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

* [Visão geral do Perfil do cliente em tempo real](../../../../../profile/home.md)
* [Visão geral da Análise do espaço de trabalho da Data Science](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> A [!DNL Platform] interface do usuário exibida no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Apêndice

As seções a seguir fornecem informações adicionais para trabalhar com conectores de origem.

### Desativar um fluxo de dados

Quando um fluxo de dados é criado, ele imediatamente se torna ativo e ingere dados de acordo com o agendamento que foi fornecido. Você pode desativar um fluxo de dados ativo a qualquer momento seguindo as instruções abaixo.

Na área de trabalho *[!UICONTROL Fontes]* , clique na guia **[!UICONTROL Procurar]** . Em seguida, clique no nome da conta que está associada ao fluxo de dados ativo que você deseja desativar.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

A página *[!UICONTROL atividade]* de origem é exibida. Selecione o fluxo de dados ativo na lista para abrir sua coluna *[!UICONTROL Propriedades]* no lado direito da tela, que contém um botão de alternância **[!UICONTROL Ativado]** . Clique na alternância para desativar o fluxo de dados. A mesma alternância pode ser usada para reativar um fluxo de dados depois que ele for desativado.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Ativar dados de entrada para [!DNL Profile] população

Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher seus [!DNL Real-time Customer Profile] dados. Para obter mais informações sobre como preencher seus [!DNL Profile] dados do cliente real, consulte o tutorial sobre a população [do](../../profile.md)Perfil.
