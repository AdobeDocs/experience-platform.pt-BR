---
keywords: Experience Platform;página inicial;tópicos populares;Editor de consultas;editor de consultas;Serviço de consulta;serviço de consulta;
solution: Experience Platform
title: Guia da interface do Editor de consultas
description: O Editor de consultas é uma ferramenta interativa fornecida pelo Serviço de consultas da Adobe Experience Platform, que permite gravar, validar e executar consultas para dados de experiência do cliente na interface do usuário do Experience Platform. O Editor de consultas é compatível com o desenvolvimento de consultas para análise e exploração de dados, e permite executar consultas interativas para fins de desenvolvimento, bem como consultas não interativas para preencher conjuntos de dados no Experience Platform.
exl-id: d7732244-0372-467d-84e2-5308f42c5d51
source-git-commit: e30942aec6c66aeed8375d6221b454725f5a958d
workflow-type: tm+mt
source-wordcount: '1901'
ht-degree: 3%

---

# [!DNL Query Editor] Guia da interface do usuário

[!DNL Query Editor] é uma ferramenta interativa fornecida pelo Adobe Experience Platform [!DNL Query Service], que permite gravar, validar e executar consultas para dados de experiência do cliente na [!DNL Experience Platform] interface do usuário. [!DNL Query Editor] O oferece suporte ao desenvolvimento de consultas para análise e exploração de dados e permite executar consultas interativas para fins de desenvolvimento, bem como consultas não interativas para preencher conjuntos de dados no [!DNL Experience Platform].

Para obter mais informações sobre os conceitos e recursos do [!DNL Query Service], consulte o [Visão geral do Serviço de consulta](../home.md). Para saber mais sobre como navegar na interface do usuário do Serviço de consulta em [!DNL Platform], consulte o [Visão geral da interface do usuário do serviço de consulta](./overview.md).

## Introdução {#getting-started}

[!DNL Query Editor] oferece execução flexível de consultas conectando-se a [!DNL Query Service], e as consultas só serão executadas enquanto essa conexão estiver ativa.

### Conectando ao [!DNL Query Service] {#connecting-to-query-service}

[!DNL Query Editor] demora alguns segundos para inicializar e se conectar ao [!DNL Query Service] quando for aberto. O console informa quando está conectado, conforme mostrado abaixo. Se você tentar executar uma consulta antes que o editor se conecte, a execução será atrasada até que a conexão seja concluída.

![A saída do console do Editor de consultas na conexão inicial.](../images/ui/query-editor/connect.png)

### Como as consultas são executadas a partir de [!DNL Query Editor] {#run-a-query}

Consultas executadas a partir de [!DNL Query Editor] executar interativamente, o que significa que se você fechar o navegador ou sair, a consulta será cancelada. O mesmo é verdadeiro para consultas feitas para gerar conjuntos de dados a partir de saídas de consulta.

## Criação de consulta usando [!DNL Query Editor] {#query-authoring}

Usar [!DNL Query Editor], você pode gravar, executar e salvar consultas para dados de experiência do cliente. Todas as consultas executadas ou salvas em [!DNL Query Editor] estão disponíveis para todos os usuários em sua organização com acesso ao [!DNL Query Service].

### Acessar o [!DNL Query Editor] {#accessing-query-editor}

No [!DNL Experience Platform] Interface, selecione **[!UICONTROL Consultas]** no menu de navegação esquerdo, para abrir a [!DNL Query Service] espaço de trabalho. Em seguida, para começar a gravar consultas, selecione **[!UICONTROL Criar consulta]** na parte superior direita da tela. Esse link está disponível em qualquer uma das páginas no [!DNL Query Service] espaço de trabalho.

![A guia de visão geral do espaço de trabalho Consultas com Create query realçado.](../images/ui/query-editor/create-query.png)

### Alternância do Editor de Consulta Aprimorado {#enhanced-editor-toggle}

>[!CONTEXTUALHELP]
>id="platform_queryService_queryEditor_enhancedEditorToggle"
>title="Botão de alternância do editor aprimorado"
>abstract="Alterne entre a versão herdada e a versão aprimorada do Editor de consultas. A versão herdada é habilitada por padrão, embora a versão aprimorada forneça melhor acessibilidade e compatibilidade com multitemas. Para saber mais sobre essas alterações, consulte a documentação."

Um botão de alternância de interface permite alternar entre a versão herdada e a versão aprimorada do Editor de consultas. A versão herdada é habilitada por padrão, embora a versão aprimorada forneça melhor acessibilidade e compatibilidade com multitemas. Ative a versão aprimorada para acessar as configurações do Editor de consultas.

![O Editor de consultas com a opção aprimorada Editor de consultas está realçado.](../images/ui/query-editor/enhanced-query-editor-toggle.png)

A ativação do botão alterna o editor para o tema claro e melhora a legibilidade da sintaxe. Um ícone de configurações também aparece acima do campo de entrada do Editor de consultas que incorpora a opção de preenchimento automático. No ícone de configurações, é possível ativar o tema escuro ou desativar/ativar o preenchimento automático.

>[!TIP]
>
>Com o Editor de consultas aprimorado, você pode [!UICONTROL Desativar preenchimento automático de sintaxe] ao criar uma consulta sem perder seu progresso. Normalmente, se você desativar o recurso de preenchimento automático durante a edição, todas as alterações no query serão perdidas.

Para ativar temas escuros ou claros, selecione o ícone de configurações (![Um ícone de configurações.](../images/ui/query-editor/settings-icon.png)) seguido pela opção no menu suspenso que é exibida.

![O Editor de consultas com o ícone de configurações e a opção de menu suspenso Ativar tema escuro estão realçados.](../images/ui/query-editor/query-editor-settings.png)

### Gravação de consultas {#writing-queries}

[!UICONTROL Editor de consultas] O é organizado para facilitar ao máximo a criação de consultas. A captura de tela abaixo mostra como o editor aparece na interface do usuário, com o campo de entrada SQL e **Reproduzir** destacado.

![O Editor de consultas com o campo de entrada SQL e Reproduzir realçados.](../images/ui/query-editor/editor.png)

Para minimizar o tempo de desenvolvimento, é recomendável desenvolver as consultas com limites nas linhas retornadas. Por exemplo, `SELECT fields FROM table WHERE conditions LIMIT number_of_rows`. Após verificar que sua consulta produz a saída esperada, remova os limites e execute a consulta com `CREATE TABLE tablename AS SELECT` para gerar um conjunto de dados com a saída.

### Gravando ferramentas em [!DNL Query Editor] {#writing-tools}

- **Realce automático da sintaxe:** Facilita a leitura e a organização do SQL.

![Uma instrução SQL no Editor de consultas demonstrando o realce da cor da sintaxe.](../images/ui/query-editor/syntax-highlight.png)

- **Preenchimento automático de palavra-chave SQL:** Comece a digitar o query, use as teclas de seta para navegar até o termo desejado e pressione **Enter**.

![Alguns caracteres de SQL com o menu suspenso de preenchimento automático fornecendo opções do Editor de consultas.](../images/ui/query-editor/syntax-auto.png)

- **Preenchimento automático de tabela e campo:** Comece a digitar o nome da tabela que deseja `SELECT` do, em seguida, use as teclas de seta para navegar até a tabela que você está procurando e pressione **Enter**. Depois que uma tabela é selecionada, o preenchimento automático reconhece os campos nessa tabela.

![A entrada do Editor de consultas exibindo sugestões de nome de tabela suspensa.](../images/ui/query-editor/tables-auto.png)

### Alternância de configuração da interface de preenchimento automático {#auto-complete}

A variável [!DNL Query Editor] A sugere automaticamente possíveis palavras-chave SQL junto com detalhes de tabela ou coluna para a consulta à medida que ela é escrita. O recurso de preenchimento automático é ativado por padrão e pode ser desativado ou ativado a qualquer momento selecionando o [!UICONTROL Sintaxe de preenchimento automático] Alterne para a parte superior direita do Editor de consultas.

A definição de configuração de preenchimento automático é por usuário e lembrada pelos logons consecutivos desse usuário.

![Editor de consultas com a opção de preenchimento automático de sintaxe realçada.](../images/ui/query-editor/auto-complete-toggle.png)

A desativação desse recurso impede que vários comandos de metadados sejam processados e fornece recomendações que normalmente beneficiam a velocidade do autor ao editar consultas.

Quando você usa o botão para ativar o recurso de preenchimento automático, as sugestões recomendadas para nomes de tabela e coluna, bem como palavras-chave SQL, ficam disponíveis após uma pequena pausa. Uma mensagem de sucesso no console, abaixo do Editor de consultas, indica que o recurso está ativo.

Se você desativar o recurso de preenchimento automático, será necessária uma atualização de página para que o recurso entre em vigor. Uma caixa de diálogo de confirmação é exibida com três opções quando você desativa o [!UICONTROL Sintaxe de preenchimento automático] alternar:

- [!UICONTROL Cancelar]
- [!UICONTROL Salvar alterações e atualizar]
- [!UICONTROL Atualizar sem salvar as alterações]

>[!IMPORTANT]
>
>Se estiver gravando ou editando uma consulta ao desabilitar este recurso, salve as alterações na consulta antes de atualizar a página, caso contrário todo o progresso será perdido.

![A caixa de diálogo de confirmação para desativar o recurso de preenchimento automático.](../images/ui/query-editor/confirmation-dialog.png)

Para desativar o recurso de preenchimento automático, selecione a opção de confirmação apropriada.

### Detecção de erro {#error-detection}

[!DNL Query Editor] valida automaticamente uma consulta à medida que ela é gravada, fornecendo validação de SQL genérica e validação de execução específica. Se um sublinhado vermelho aparecer abaixo da consulta (como mostrado na imagem abaixo), ele representa um erro na consulta.

![A entrada do Editor de consultas exibindo o SQL sublinhado em vermelho para indicar um erro.](../images/ui/query-editor/syntax-error-highlight.png)

Quando erros são detectados, é possível exibir as mensagens de erro específicas ao passar o mouse sobre o código SQL.

![Um diálogo com uma mensagem de erro.](../images/ui/query-editor/linting-error.png)

### Detalhes da consulta {#query-details}

Para exibir uma consulta no Editor de consultas, selecione qualquer modelo salvo na [!UICONTROL Modelos] guia. O painel de detalhes da consulta fornece mais informações e ferramentas para gerenciar a consulta selecionada.

![O Editor de consultas com o painel de detalhes da consulta realçado.](../images/ui/query-editor/query-details.png)

Esse painel permite gerar um conjunto de dados de saída diretamente da interface do usuário, excluir ou nomear a consulta exibida e adicionar um agendamento à consulta.

Esse painel também mostra metadados úteis, como a última vez que a consulta foi modificada e quem a modificou, se aplicável. Para gerar um conjunto de dados, selecione **[!UICONTROL Conjunto de dados de saída]**. A variável **[!UICONTROL Conjunto de dados de saída]** será exibida. Insira um nome e uma descrição, depois selecione **[!UICONTROL Executar consulta]**. O novo conjunto de dados é exibido na **[!UICONTROL Conjuntos de dados]** na guia [!DNL Query Service] interface de usuário ativada [!DNL Platform].

### Consultas programadas {#scheduled-queries}

As consultas que foram salvas como um modelo podem ser agendadas no Editor de consultas. O agendamento de consultas permite automatizar as execuções de consultas em uma cadência personalizada. Você pode agendar consultas com base na frequência, data e hora e também escolher um conjunto de dados de saída para seus resultados, se necessário. Os agendamentos de query também podem ser desativados ou excluídos por meio da interface do usuário.

Os cronogramas são definidos no Editor de consultas. Ao usar o Editor de consultas, você só pode adicionar um agendamento a uma consulta que já tenha sido criada, salva e executada. A mesma limitação não se aplica ao [!DNL Query Service] API:

Consulte a documentação dos cronogramas de consulta para saber como [criar agendamentos de consulta na interface](./query-schedules.md). Como alternativa, para saber como adicionar agendas usando a API, leia o [guia de endpoint de consultas programadas](../api/scheduled-queries.md).

Quaisquer consultas programadas são adicionadas à lista no [!UICONTROL Consultas programadas] guia. Nesse espaço de trabalho, é possível monitorar o status de todos os trabalhos de consulta agendados por meio da interface do usuário. No [!UICONTROL Consultas programadas] você pode encontrar informações importantes sobre as execuções de consulta e assinar alertas. As informações disponíveis incluem status, detalhes da programação e mensagens/códigos de erro se uma execução falhar. Consulte a [Monitorar documento de consultas programadas](./monitor-queries.md) para obter mais informações.

### Salvamento de consultas {#saving-queries}

A variável [!DNL Query Editor] O fornece uma função salvar que permite salvar uma consulta e trabalhar nela posteriormente. Para salvar uma consulta, selecione **[!UICONTROL Salvar]** no canto superior direito de [!DNL Query Editor]. Para que uma consulta possa ser salva, um nome deve ser fornecido para ela usando o **[!UICONTROL Detalhes da consulta]** painel.

>[!NOTE]
>
>Consultas nomeadas e salvas no usando o Editor de consultas estão disponíveis como modelos no painel Consulta [!UICONTROL Modelos] guia. Consulte a [documentação de modelos](./query-templates.md) para obter mais informações.

### Como encontrar consultas anteriores {#previous-queries}

Todas as consultas executadas de [!DNL Query Editor] são capturados na tabela Log. Você pode usar a funcionalidade de pesquisa no **[!UICONTROL Log]** para localizar execuções de consulta. As consultas salvas estão listadas no **[!UICONTROL Modelos]** guia.

Se um query foi agendado, a variável [!UICONTROL Consultas programadas] fornece visibilidade aprimorada por meio da interface para esses trabalhos de consulta. Consulte a [documentação de monitoramento de consultas](./monitor-queries.md) para obter mais informações.

>[!NOTE]
>
>As consultas que não são executadas não são salvas pelo Log. Para que a consulta esteja disponível no [!DNL Query Service], ela deve ser executada ou salva em [!DNL Query Editor].

## Execução de consultas usando o Editor de consultas {#executing-queries}

Para executar uma consulta no [!DNL Query Editor], você poderá inserir o SQL no editor ou carregar uma consulta anterior do **[!UICONTROL Log]** ou **[!UICONTROL Modelos]** e selecione **Reproduzir**. O status da execução da consulta é exibido no **[!UICONTROL Console]** e os dados de saída serão mostrados na guia **[!UICONTROL Resultados]** guia.

### Console {#console}

O console fornece informações sobre o status e a operação do [!DNL Query Service]. O console exibe o status da conexão para [!DNL Query Service], operações de consulta que estão sendo executadas e qualquer mensagem de erro que resultar dessas consultas.

![A guia Console do console do Editor de consultas.](../images/ui/query-editor/console.png)

>[!NOTE]
>
>O console mostra apenas os erros que resultaram da execução de um query. Ele não mostra os erros de validação de consulta que ocorrem antes da execução de uma consulta.

### Resultados da consulta {#query-results}

Após a conclusão de um query, os resultados são exibidos no **[!UICONTROL Resultados]** , ao lado da guia **[!UICONTROL Console]** guia. Essa visualização mostra a saída tabular do query, exibindo até 100 linhas. Essa visualização permite verificar se sua consulta produz a saída esperada. Para gerar um conjunto de dados com sua consulta, remova os limites nas linhas retornadas e execute a consulta com `CREATE TABLE tablename AS SELECT` para gerar um conjunto de dados com a saída. Consulte a [tutorial sobre geração de conjuntos de dados](./create-datasets.md) para obter instruções sobre como gerar um conjunto de dados a partir dos resultados da consulta em [!DNL Query Editor].

![A guia Resultados do console do Editor de consultas exibindo os resultados de uma execução de consulta.](../images/ui/query-editor/query-results.png)

## Executar consultas com [!DNL Query Service] vídeo tutorial {#query-tutorial-video}

O vídeo a seguir mostra como executar queries na interface do Adobe Experience Platform e em um cliente PSQL. O vídeo também demonstra o uso de propriedades individuais em um objeto XDM, funções definidas por Adobe e como usar consultas CREATE TABLE AS SELECT (CTAS).

>[!VIDEO](https://video.tv.adobe.com/v/29796?quality=12&learn=on)

## Próximas etapas

Agora que você sabe quais recursos estão disponíveis no [!DNL Query Editor] e como navegar no aplicativo, você pode começar a criar suas próprias consultas diretamente no [!DNL Platform]. Para obter mais informações sobre a execução de consultas SQL em conjuntos de dados na [!DNL Data Lake], consulte o guia sobre [execução de consultas](../best-practices/writing-queries.md).
