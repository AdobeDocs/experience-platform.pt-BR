---
keywords: Experience Platform, home, tópicos populares, fluxo de dados, fluxo de dados
title: Configure um fluxo de dados para assimilar dados em lote de uma fonte de armazenamento na nuvem na interface do usuário do
description: Este tutorial fornece etapas sobre como configurar um novo fluxo de dados para assimilar dados em lote de uma fonte de armazenamento em nuvem na interface do usuário
exl-id: b327bbea-039d-4c04-afd3-f1d6a5f902a6
source-git-commit: 0910de76d817eea7c7c3cb2b988d81268b3e5812
workflow-type: tm+mt
source-wordcount: '1795'
ht-degree: 1%

---

# Configure um fluxo de dados para assimilar dados em lote de uma fonte de armazenamento em nuvem na interface do usuário do

Este tutorial fornece etapas sobre como configurar um fluxo de dados para trazer dados em lote da fonte de armazenamento na nuvem para o Adobe Experience Platform.

## Introdução

>[!NOTE]
>
>Para criar um fluxo de dados para trazer dados em lote de um armazenamento na nuvem, você já deve ter acesso a uma fonte de armazenamento na nuvem autenticada. Caso não tenha acesso, acesse o [visão geral das fontes](../../../../home.md#cloud-storage) para obter uma lista de fontes de armazenamento em nuvem com as quais você pode criar uma conta.

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

### Formatos de arquivo não compatíveis

As fontes de armazenamento em nuvem para dados em lote oferecem suporte aos seguintes formatos de arquivo para assimilação:

* Valores separados por delimitador (DSV): Qualquer valor de caractere único pode ser usado como delimitador para arquivos de dados formatados em DSV.
* [!DNL JavaScript Object Notation] (JSON): Os arquivos de dados formatados em JSON devem ser compatíveis com XDM.
* [!DNL Apache Parquet]: Os arquivos de dados formatados com parâmetro devem ser compatíveis com XDM.
* Arquivos compactados: JSON e arquivos delimitados podem ser compactados como: `bzip2`, `gzip`, `deflate`, `zipDeflate`, `tarGzip`e `tar`.

## Adicionar dados

Depois de criar a conta de armazenamento em nuvem, a variável **[!UICONTROL Adicionar dados]** será exibida, fornecendo uma interface para explorar sua hierarquia de arquivos de armazenamento na nuvem e selecionar a pasta ou o arquivo específico que deseja trazer para a Platform.

* A parte esquerda da interface é um navegador de diretório, exibindo sua hierarquia de arquivo de armazenamento em nuvem.
* A parte direita da interface permite visualizar até 100 linhas de dados de uma pasta ou arquivo compatível.

![](../../../../images/tutorials/dataflow/cloud-batch/select-data.png)

Selecione a pasta raiz para acessar a hierarquia de pastas. Aqui, você pode selecionar uma única pasta para assimilar todos os arquivos na pasta recursivamente. Ao assimilar uma pasta inteira, você deve garantir que todos os arquivos nessa pasta compartilhem o mesmo formato de dados e esquema.

![](../../../../images/tutorials/dataflow/cloud-batch/folder-directory.png)

Após selecionar uma pasta, a interface correta será atualizada para pré-visualizar o conteúdo e a estrutura do primeiro arquivo na pasta selecionada.

![](../../../../images/tutorials/dataflow/cloud-batch/select-folder.png)

Durante essa etapa, você pode fazer várias configurações aos seus dados, antes de continuar. Primeiro, selecione **[!UICONTROL Formato dos dados]** e, em seguida, selecione o formato de dados apropriado para seu arquivo no painel suspenso exibido.

A tabela a seguir exibe os formatos de dados apropriados para os tipos de arquivos suportados:

| Tipo de arquivo | Formato dos dados |
| --- | --- |
| CSV | [!UICONTROL Delimitado] |
| JSON | [!UICONTROL JSON] |
| Parquet | [!UICONTROL Parqueta XDM] |

![](../../../../images/tutorials/dataflow/cloud-batch/data-format.png)

### Selecione um delimitador de coluna

Após configurar o formato de dados, é possível definir um delimitador de coluna ao assimilar arquivos delimitados. Selecione o **[!UICONTROL Delimitador]** e selecione um delimitador no menu suspenso. O menu exibe as opções mais usadas para delimitadores, incluindo uma vírgula (`,`), uma guia (`\t`) e uma barra vertical (`|`).

![](../../../../images/tutorials/dataflow/cloud-batch/delimiter.png)

Se preferir usar um delimitador personalizado, selecione **[!UICONTROL Personalizado]** e insira um delimitador de caractere único de sua escolha na barra de entrada pop-up.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

### Assimilar arquivos compactados

Também é possível assimilar arquivos compactados JSON ou delimitados especificando o tipo de compactação.

No [!UICONTROL Selecionar dados] selecione um arquivo compactado para assimilação e selecione o tipo de arquivo apropriado e se ele é compatível com XDM ou não. Em seguida, selecione **[!UICONTROL Tipo de compactação]** e selecione o tipo de arquivo compactado apropriado para seus dados de origem.

![](../../../../images/tutorials/dataflow/cloud-batch/custom.png)

Para trazer um arquivo específico para a Platform, selecione uma pasta e depois selecione o arquivo que deseja assimilar. Durante essa etapa, também é possível visualizar o conteúdo de outros arquivos em uma determinada pasta usando o ícone de visualização ao lado do nome do arquivo.

Quando terminar, selecione **[!UICONTROL Próximo]**.

![](../../../../images/tutorials/dataflow/cloud-batch/select-file.png)

## Fornecer detalhes do fluxo de dados

O [!UICONTROL Detalhes do fluxo de dados] permite selecionar se deseja usar um conjunto de dados existente ou um novo conjunto de dados. Durante esse processo, você também pode configurar seus dados para serem assimilados no Perfil e ativar configurações como [!UICONTROL Diagnóstico de erros], [!UICONTROL Ingestão parcial]e [!UICONTROL Alertas].

![](../../../../images/tutorials/dataflow/cloud-batch/dataflow-detail.png)

### Usar um conjunto de dados existente

Para assimilar dados em um conjunto de dados existente, selecione **[!UICONTROL Conjunto de dados existente]**. Você pode recuperar um conjunto de dados existente usando o [!UICONTROL Pesquisa avançada] ou percorrendo a lista de conjuntos de dados existentes no menu suspenso. Depois de selecionar um conjunto de dados, forneça um nome e uma descrição para o seu fluxo de dados.

![](../../../../images/tutorials/dataflow/cloud-batch/existing.png)

### Usar um novo conjunto de dados

Para assimilar em um novo conjunto de dados, selecione **[!UICONTROL Novo conjunto de dados]** e, em seguida, forneça um nome de conjunto de dados de saída e uma descrição opcional. Em seguida, selecione um esquema para mapear usando o [!UICONTROL Pesquisa avançada] ou rolando pela lista de schemas existentes no menu suspenso. Depois de selecionar um esquema, forneça um nome e uma descrição para o seu fluxo de dados.

![](../../../../images/tutorials/dataflow/cloud-batch/new.png)

### Ativar o diagnóstico de perfil e erro

Em seguida, selecione o **[!UICONTROL Conjunto de dados de perfil]** alternar para ativar seu conjunto de dados para Perfil. Isso permite criar uma visualização holística dos atributos e comportamentos de uma entidade. Os dados de todos os conjuntos de dados habilitados para perfil serão incluídos no Perfil e as alterações serão aplicadas quando você salvar o fluxo de dados.

[!UICONTROL Diagnóstico de erros] permite a geração detalhada de mensagens de erro para qualquer registro incorreto que ocorra no seu fluxo de dados, enquanto [!UICONTROL Ingestão parcial] O permite assimilar dados contendo erros, até um determinado limite definido manualmente. Consulte a [visão geral da ingestão parcial de lote](../../../../../ingestion/batch-ingestion/partial.md) para obter mais informações.

![](../../../../images/tutorials/dataflow/cloud-batch/ingestion-configs.png)

### Ativar alertas

Você pode habilitar alertas para receber notificações sobre o status do seu fluxo de dados. Selecione um alerta na lista para assinar e receber notificações sobre o status do seu fluxo de dados. Para obter mais informações sobre alertas, consulte o guia sobre [inscrever-se em alertas de origens usando a interface do usuário](../../alerts.md).

Quando terminar de fornecer detalhes do fluxo de dados, selecione **[!UICONTROL Próximo]**.

![](../../../../images/tutorials/dataflow/cloud-batch/alerts.png)

## Mapear campos de dados para um esquema XDM

O [!UICONTROL Mapeamento] é exibida, fornecendo uma interface para mapear os campos de origem do esquema de origem para os campos XDM de destino apropriados no esquema de destino.

A Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema de destino ou conjunto de dados selecionado. Você pode ajustar manualmente as regras de mapeamento de acordo com seus casos de uso. Com base em suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem em valores calculados ou calculados. Para obter etapas abrangentes sobre o uso da interface do mapeador e dos campos calculados, consulte o [Guia da interface do usuário de preparação de dados](../../../../../data-prep/ui/mapping.md).

Depois que os dados de origem forem mapeados com êxito, selecione **[!UICONTROL Próximo]**.

![](../../../../images/tutorials/dataflow/cloud-batch/mapping.png)

## Agendar execução de ingestão

>[!IMPORTANT]
>
>É altamente recomendável agendar seu fluxo de dados para uma ingestão única ao usar a variável [Origem FTP](../../../../connectors/cloud-storage/ftp.md).

O [!UICONTROL Agendamento] é exibida, permitindo configurar um agendamento de assimilação para assimilar automaticamente os dados de origem selecionados usando os mapeamentos configurados. Por padrão, a programação está definida como `Once`. Para ajustar a frequência de ingestão, selecione **[!UICONTROL Frequência]** e selecione uma opção no menu suspenso.

>[!TIP]
>
>O intervalo e o preenchimento retroativo não são visíveis durante uma ingestão única.

![programação](../../../../images/tutorials/dataflow/cloud-batch/scheduling.png)

Se você definir sua frequência de ingestão como `Minute`, `Hour`, `Day`ou `Week`, é necessário definir um intervalo para estabelecer um intervalo de tempo definido entre cada ingestão. Por exemplo, uma frequência de assimilação definida como `Day` e um intervalo definido como `15` significa que o fluxo de dados está agendado para assimilar dados a cada 15 dias.

Durante essa etapa, também é possível ativar **preenchimento retroativo** e defina uma coluna para a assimilação incremental de dados. O preenchimento retroativo é usado para assimilar dados históricos, enquanto a coluna definida para assimilação incremental permite que novos dados sejam diferenciados dos dados existentes.

Consulte a tabela abaixo para obter mais informações sobre configurações de agendamento.

| Campo | Descrição |
| --- | --- |
| Frequência | A frequência em que ocorre uma ingestão. As frequências selecionáveis incluem `Once`, `Minute`, `Hour`, `Day`e `Week`. |
| Intervalo | Um número inteiro que define o intervalo para a frequência selecionada. O valor do intervalo deve ser um número inteiro diferente de zero e deve ser definido como maior ou igual a 15. |
| Hora de início | Um carimbo de data e hora UTC indicando quando a primeira assimilação está definida para ocorrer. A hora de início deve ser maior ou igual à hora UTC atual. |
| Preenchimento retroativo | Um valor booleano que determina quais dados são assimilados inicialmente. Se o preenchimento retroativo estiver ativado, todos os arquivos atuais no caminho especificado serão assimilados durante a primeira assimilação programada. Se o preenchimento retroativo estiver desativado, somente os arquivos carregados entre a primeira execução da assimilação e a hora de início serão assimilados. Os arquivos carregados antes da hora de início não serão assimilados. |

>[!NOTE]
>
>Para assimilação em lote, cada fluxo de dados subsequente seleciona arquivos a serem assimilados da sua origem com base em seus **última modificação** timestamp. Isso significa que os fluxos de dados em lote selecionam arquivos da origem que são novos ou foram modificados desde a última execução do fluxo. Além disso, você deve garantir que haja um intervalo de tempo suficiente entre o upload do arquivo e uma execução de fluxo agendado, pois os arquivos que não são carregados totalmente na sua conta de armazenamento em nuvem antes do tempo de execução do fluxo agendado podem não ser coletados para assimilação.

Ao concluir a configuração do agendamento de ingestão, selecione **[!UICONTROL Próximo]**.

![](../../../../images/tutorials/dataflow/cloud-batch/scheduling-configs.png)

## Revisar o fluxo de dados

O **[!UICONTROL Revisão]** é exibida, permitindo que você revise o novo fluxo de dados antes de criá-lo. Os detalhes são agrupados nas seguintes categorias:

* **[!UICONTROL Conexão]**: Mostra o tipo de origem, o caminho relevante do arquivo de origem escolhido e a quantidade de colunas dentro desse arquivo de origem.
* **[!UICONTROL Atribuir conjunto de dados e mapear campos]**: Mostra em qual conjunto de dados os dados de origem estão sendo assimilados, incluindo o esquema ao qual o conjunto de dados adere.
* **[!UICONTROL Agendamento]**: Mostra o período ativo, a frequência e o intervalo do agendamento de ingestão.

Depois de revisar o fluxo de dados, clique em **[!UICONTROL Concluir]** e permitir que o fluxo de dados seja criado.

![](../../../../images/tutorials/dataflow/cloud-batch/review.png)


## Próximas etapas

Ao seguir este tutorial, você criou com sucesso um fluxo de dados para trazer dados de um armazenamento externo em nuvem e ganhou informações sobre o monitoramento de conjuntos de dados. Para saber mais sobre como criar fluxos de dados, você pode complementar seu aprendizado assistindo ao vídeo abaixo. Além disso, os dados de entrada agora podem ser usados pelo downstream [!DNL Platform] serviços como [!DNL Real-time Customer Profile] e [!DNL Data Science Workspace]. Consulte os seguintes documentos para obter mais detalhes:

* [[!DNL Real-time Customer Profile] visão geral](../../../../../profile/home.md)
* [[!DNL Data Science Workspace] visão geral](../../../../../data-science-workspace/home.md)

>[!WARNING]
>
> O [!DNL Platform] A interface do usuário exibida no vídeo a seguir está desatualizada. Consulte a documentação acima para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/29695?quality=12&learn=on)

## Apêndice

As seções a seguir fornecem informações adicionais para trabalhar com conectores de origem.

## Monitorar o fluxo de dados

Depois que o fluxo de dados for criado, é possível monitorar os dados que estão sendo assimilados por meio dele para exibir informações sobre taxas de ingestão, sucesso e erros. Para obter mais informações sobre como monitorar o fluxo de dados, visite o tutorial em [monitoramento de contas e fluxos de dados na interface do usuário](../../monitor.md).

## Atualizar o fluxo de dados

Para atualizar as configurações para o agendamento, mapeamento e informações gerais do fluxo de dados, visite o tutorial em [atualização de fluxos de dados de fontes na interface do usuário](../../update-dataflows.md)

## Excluir seu fluxo de dados

É possível excluir os fluxos de dados que não são mais necessários ou foram criados incorretamente usando o **[!UICONTROL Excluir]** disponível na função **[!UICONTROL Fluxos de dados]** espaço de trabalho. Para obter mais informações sobre como excluir fluxos de dados, visite o tutorial em [exclusão de fluxos de dados na interface do usuário](../../delete.md).