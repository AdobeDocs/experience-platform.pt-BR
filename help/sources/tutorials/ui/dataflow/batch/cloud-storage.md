---
keywords: Experience Platform;home;popular topics;dataflow;Dataflow
solution: Experience Platform
title: Configurar um fluxo de dados para um conector de lote de Armazenamentos na nuvem na interface do usuário
topic: overview
type: Tutorial
description: Um fluxo de dados é uma tarefa programada que recupera e ingere dados de uma fonte para um conjunto de dados da plataforma. Este tutorial fornece etapas para configurar um novo fluxo de dados usando sua conta de armazenamento em nuvem.
translation-type: tm+mt
source-git-commit: 62266187ed1f3ce2f0acca3f50487fb70cfa7307
workflow-type: tm+mt
source-wordcount: '1898'
ht-degree: 0%

---


# Configurar um fluxo de dados para uma conexão em lote de armazenamentos na nuvem na interface do usuário

Um fluxo de dados é uma tarefa programada que recupera e ingere dados de uma fonte para um conjunto de dados [!DNL Platform]. Este tutorial fornece etapas para configurar um novo fluxo de dados usando sua conta de armazenamento em nuvem.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Além disso, este tutorial requer uma conta de armazenamento em nuvem estabelecida. Uma lista de tutoriais para criar diferentes contas de armazenamento na nuvem na interface do usuário pode ser encontrada na [visão geral dos conectores de origem](../../../../home.md).

### Formatos de arquivo não suportados

[!DNL Experience Platform] oferece suporte aos seguintes formatos de arquivo para serem assimilados de armazenamentos externos:

* Valores separados por delimitador (DSV): Atualmente, o suporte para arquivos de dados formatados em DSV está limitado a valores separados por vírgulas. O valor dos cabeçalhos de campo nos arquivos formatados em DSV deve consistir apenas em caracteres alfanuméricos e sublinhados. O suporte para arquivos DSV gerais será fornecido no futuro.
* [!DNL JavaScript Object Notation] (JSON): Os arquivos de dados formatados JSON devem ser compatíveis com XDM.
* [!DNL Apache Parquet]: Os arquivos de dados formatados em parâmetro devem ser compatíveis com XDM.

## Selecionar dados

Depois de criar sua conta de armazenamento na nuvem, a etapa **[!UICONTROL Selecionar dados]** é exibida, fornecendo uma interface para explorar a hierarquia de arquivos de armazenamento na nuvem.

* A metade esquerda da interface é um navegador de diretório que exibe os arquivos e diretórios do servidor.
* A metade direita da interface permite que você pré-visualização até 100 linhas de dados de um arquivo compatível.

Selecionar uma pasta listada permite que você transfira a hierarquia de pastas para pastas mais profundas. Depois que você tiver um arquivo ou pasta compatível selecionado, a lista suspensa **[!UICONTROL Selecionar formato de dados]** será exibida, onde você pode escolher um formato para exibir os dados na janela de pré-visualização.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data.png)

Selecione o formato de dados apropriado para o arquivo que deseja assimilar e aguarde alguns segundos para que a janela de pré-visualização seja preenchida.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/data-format.png)

Você pode definir um delimitador personalizado ao assimilar arquivos delimitados. Selecione a opção **[!UICONTROL Delimitador]** e selecione um delimitador no menu suspenso. O menu exibe as opções mais usadas para delimitadores, incluindo uma vírgula (`,`), uma guia (`\t`) e uma barra vertical (`|`). Como alternativa, você pode selecionar **[!UICONTROL Personalizado]** e inserir um delimitador personalizado de sua escolha na barra de entrada pop-up.

Depois de selecionar seu formato de dados e definir seu delimitador, selecione **[!UICONTROL Próximo]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/delimiter.png)

### Ingest Parquet ou arquivos JSON

As contas de armazenamento em nuvem também suportam arquivos JSON e Parquet. Os arquivos de parâmetro devem ser compatíveis com XDM, enquanto os arquivos JSON não precisam ser compatíveis com XDM. Para assimilar arquivos JSON ou Parquet, selecione o formato de arquivo apropriado no navegador de diretório e aplique o formato de dados compatível na interface correta.

Se o formato de dados estiver no JSON, uma pré-visualização será exibida, mostrando informações sobre os dados no arquivo. Na tela de pré-visualização, você pode selecionar se o JSON é compatível com XDM usando a lista suspensa **[!UICONTROL compatível com XDM]**.

Selecione **[!UICONTROL Próximo]** para prosseguir.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/json-preview.png)

>[!IMPORTANT]
>
>Diferentemente dos tipos de arquivos delimitados e JSON, os arquivos formatados Parquet não estão disponíveis para pré-visualização.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-data-parquet.png)

## Mapear campos de dados para um schema XDM

A etapa **[!UICONTROL Mapping]** é exibida, fornecendo uma interface interativa para mapear os dados de origem para um conjunto de dados [!DNL Platform]. Os arquivos de origem formatados no Parquet devem ser compatíveis com XDM e não exigem que você configure manualmente o mapeamento, enquanto os arquivos CSV exigem que você configure explicitamente o mapeamento, mas permitem que você escolha quais campos de dados de origem serão mapeados. Os arquivos JSON, se marcados como reclamação XDM, não exigem configuração manual. No entanto, se não estiver marcado como compatível com XDM, será necessário configurar explicitamente o mapeamento.

Escolha um conjunto de dados para os dados de entrada a serem ingeridos. Você pode usar um conjunto de dados existente ou criar um novo.

**Usar um conjunto de dados existente**

Para assimilar dados em um conjunto de dados existente, selecione **[!UICONTROL Conjunto de dados existente]** e selecione o ícone do conjunto de dados.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/use-existing-data.png)

A caixa de diálogo **[!UICONTROL Selecionar conjunto de dados]** é exibida. Encontre o conjunto de dados que deseja usar, selecione-o e clique em **[!UICONTROL Continuar]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-existing-dataset.png)

**Usar um novo conjunto de dados**

Para assimilar dados em um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]** e insira um nome e uma descrição para o conjunto de dados nos campos fornecidos. Para adicionar um schema, você pode inserir um nome de schema existente na caixa de diálogo **[!UICONTROL Selecionar schema]**. Como alternativa, você pode selecionar **[!UICONTROL pesquisa avançada do Schema]** para procurar um schema apropriado.

Durante esta etapa, você pode ativar seu conjunto de dados para [!DNL Real-time Customer Profile] e criar uma visualização holística dos atributos e comportamentos de uma entidade. Os dados de todos os conjuntos de dados ativados serão incluídos em [!DNL Profile] e as alterações serão aplicadas quando você salvar seu fluxo de dados.

Alterne o botão **[!UICONTROL conjunto de dados de Perfil]** para ativar o conjunto de dados de público alvo para [!DNL Profile].

![](../../../../images/tutorials/dataflow/cloud-storage/batch/new-dataset.png)

A caixa de diálogo **[!UICONTROL Selecionar schema]** é exibida. Selecione o schema que deseja aplicar ao novo conjunto de dados e selecione **[!UICONTROL Concluído]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/select-schema.png)

Com base em suas necessidades, você pode optar por mapear os campos diretamente ou usar as funções do mapeador para transformar dados de origem para derivar valores calculados ou calculados. Para obter mais informações sobre funções de mapeamento e mapeamento de dados, consulte o tutorial em [mapeamento de dados CSV para campos de schema XDM](../../../../../ingestion/tutorials/map-a-csv-file.md).

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping.png)

Para arquivos JSON, além de mapear campos diretamente para outros campos, é possível mapear objetos diretamente para outros objetos e matrizes para outras matrizes. Também é possível pré-visualização e mapear tipos de dados complexos, como matrizes em arquivos JSON, usando um conector de origem de armazenamento na nuvem.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/source-field-json.png)

![](../../../../images/tutorials/dataflow/cloud-storage/batch/target-field-json.png)

Observe que não é possível mapear tipos diferentes. Por exemplo, não é possível mapear um objeto para uma matriz ou um campo para um objeto.

>[!TIP]
>
>[!DNL Platform] fornece recomendações inteligentes para campos mapeados automaticamente com base no schema ou conjunto de dados do público alvo selecionado. É possível ajustar manualmente as regras de mapeamento para atender aos casos de uso.

Selecione **[!UICONTROL dados de Pré-visualização]** para ver os resultados do mapeamento de até 100 linhas de dados de amostra do conjunto de dados selecionado.

Durante a pré-visualização, a coluna de identidade é priorizada como o primeiro campo, já que são as principais informações necessárias ao validar os resultados do mapeamento.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/mapping-preview.png)

Depois que os dados de origem forem mapeados, selecione **[!UICONTROL Close]**.

## Execuções de ingestão agendada

A etapa **[!UICONTROL Agendamento]** é exibida, permitindo que você configure um agendamento de ingestão para assimilar automaticamente os dados de origem selecionados usando os mapeamentos configurados. A tabela a seguir descreve os diferentes campos configuráveis para programação:

| Campo | Descrição |
| --- | --- |
| Frequência | As frequências selecionáveis incluem `Once`, `Minute`, `Hour`, `Day` e `Week`. |
| Intervalo | Um número inteiro que define o intervalo para a frequência selecionada. |
| hora do start | Um carimbo de data e hora UTC indicando quando a primeira ingestão está definida para ocorrer. |
| Backfill | Um valor booliano que determina quais dados são inicialmente assimilados. Se **[!UICONTROL Backfill]** estiver ativado, todos os arquivos atuais no caminho especificado serão ingeridos durante a primeira ingestão programada. Se **[!UICONTROL Backfill]** estiver desativado, somente os arquivos que forem carregados entre a primeira execução da ingestão e a hora do start serão assimilados. Os arquivos carregados antes da hora do start não serão ingeridos. |

Os fluxos de dados são projetados para assimilar dados automaticamente de acordo com uma programação. Start selecionando a frequência da ingestão. Em seguida, defina o intervalo para designar o período entre duas execuções de fluxo. O valor do intervalo deve ser um número inteiro diferente de zero e deve ser definido como maior ou igual a 15.

Para definir a hora de ingestão do start, ajuste a data e a hora exibidas na caixa da hora do start. Como alternativa, você pode selecionar o ícone de calendário para editar o valor de hora do start. O tempo de start deve ser maior ou igual ao tempo atual em UTC.

Forneça valores para o agendamento e selecione **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-interval-on.png)

### Configurar um fluxo de dados de ingestão única

Para configurar a ingestão única, selecione a seta suspensa de frequência e selecione **[!UICONTROL Once]**. Você pode continuar fazendo edições em um conjunto de fluxo de dados para uma ingestão de frequência única, desde que o tempo de start permaneça no futuro. Depois que a hora do start passar, o valor de frequência única não poderá mais ser editado. **[!UICONTROL O]** Intervaland  **** Backfillare não é visível ao configurar um fluxo de dados de ingestão única.

>[!IMPORTANT]
>
>É altamente recomendável agendar seu fluxo de dados para ingestão única ao usar o [conector FTP](../../../../connectors/cloud-storage/ftp.md).

Depois de fornecer os valores apropriados para o agendamento, selecione **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/scheduling-once.png)

## Fornecer detalhes do fluxo de dados

A etapa **[!UICONTROL Dataflow detail]** é exibida, permitindo que você nomeie e forneça uma breve descrição sobre seu novo dataflow.

Durante esse processo, você também pode ativar **[!UICONTROL A ingestão parcial]** e **[!UICONTROL Diagnósticos de erro]**. Habilitar **[!UICONTROL A ingestão parcial]** oferece a capacidade de assimilar dados que contêm erros, até um certo limite que você pode definir. Habilitar **[!UICONTROL Diagnósticos de erro]** fornecerá detalhes sobre quaisquer dados incorretos armazenados em lote separadamente. Para obter mais informações, consulte a [visão geral da ingestão parcial de lote](../../../../../ingestion/batch-ingestion/partial.md).

Forneça valores para o fluxo de dados e selecione **[!UICONTROL Next]**.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/dataflow-detail.png)

## Revisar seu fluxo de dados

A etapa **[!UICONTROL Revisar]** é exibida, permitindo que você revise seu novo fluxo de dados antes de ele ser criado. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas nesse arquivo de origem.
* **[!UICONTROL Atribuir campos]** do conjunto de dados e mapear: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o schema ao qual o conjunto de dados adere.
* **[!UICONTROL Agendamento]**: Mostra o período ativo, a frequência e o intervalo do agendamento da ingestão.

Depois de revisar seu fluxo de dados, clique em **[!UICONTROL Concluir]** e aguarde algum tempo para que o fluxo de dados seja criado.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/review.png)

## Monitore seu fluxo de dados

Depois que seu fluxo de dados for criado, você poderá monitorar os dados que estão sendo assimilados por ele para ver informações sobre taxas de ingestão, sucesso e erros. Para obter mais informações sobre como monitorar o fluxo de dados, consulte o tutorial em [contas de monitoramento e fluxos de dados na interface do usuário](../../monitor.md).

## Excluir seu fluxo de dados

Você pode excluir fluxos de dados que não são mais necessários ou foram criados incorretamente usando a função **[!UICONTROL Delete]** disponível na área de trabalho **[!UICONTROL Fluxos de dados]**. Para obter mais informações sobre como excluir fluxos de dados, consulte o tutorial em [excluir fluxos de dados na interface do usuário](../../delete.md).

## Próximas etapas

Ao seguir este tutorial, você criou com êxito um fluxo de dados para trazer dados de um armazenamento de nuvem externo e obteve insight sobre conjuntos de dados de monitoramento. Para saber mais sobre como criar fluxos de dados, você pode complementar seu aprendizado assistindo ao vídeo abaixo. Além disso, os dados de entrada agora podem ser usados por serviços downstream [!DNL Platform], como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

* [[!DNL Real-time Customer Profile] visão geral](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] visão geral](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> A interface do usuário [!DNL Platform] mostrada no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Apêndice

As seções a seguir fornecem informações adicionais para trabalhar com conectores de origem.

### Desativar um fluxo de dados

Quando um fluxo de dados é criado, ele imediatamente se torna ativo e ingere dados de acordo com o agendamento que foi fornecido. Você pode desativar um fluxo de dados ativo a qualquer momento seguindo as instruções abaixo.

Na área de trabalho **[!UICONTROL Origens]**, clique na guia **[!UICONTROL Procurar]**. Em seguida, clique no nome da conta que está associada ao fluxo de dados ativo que você deseja desativar.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

A página **[!UICONTROL atividade de origem]** é exibida. Selecione o fluxo de dados ativo na lista para abrir sua coluna **[!UICONTROL Propriedades]** no lado direito da tela, que contém um botão de alternância **[!UICONTROL Ativado]**. Clique na alternância para desativar o fluxo de dados. A mesma alternância pode ser usada para reativar um fluxo de dados depois que ele for desativado.

![](../../../../images/tutorials/dataflow/cloud-storage/batch/disable-source.png)

### Ativar dados de entrada para a população [!DNL Profile]

Os dados de entrada do seu conector de origem podem ser usados para enriquecer e preencher seus dados [!DNL Real-time Customer Profile]. Para obter mais informações sobre como preencher seus dados [!DNL Real-time Customer Profile], consulte o tutorial em [preenchimento do Perfil](../../profile.md).
