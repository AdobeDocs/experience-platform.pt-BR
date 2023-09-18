---
title: Guia da interface de atributos computados
description: Saiba como criar, exibir e atualizar atributos computados usando a interface do usuário do Adobe Experience Platform.
source-git-commit: 7ed473750b673eefd84b8d727043ad6ea35c3a8e
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 1%

---


# Guia da interface de atributos computados

No Adobe Experience Platform, os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização.

Este documento fornece um guia sobre como criar e atualizar atributos calculados usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este guia de interface do usuário requer uma compreensão dos vários [!DNL Experience Platform] serviços envolvidos no gerenciamento [!DNL Real-Time Customer Profiles]. Antes de ler este guia ou trabalhar na interface do usuário, consulte a documentação dos seguintes serviços:

- [[!DNL Real-Time Customer Profile]](../home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Experience Data Model (XDM) System]](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.

## Exibir atributos calculados {#view}

Na interface do Experience Platform, selecione **[!UICONTROL Perfis]** na navegação à esquerda, seguido por **[!UICONTROL Atributos computados]** para ver uma lista dos atributos calculados disponíveis para sua organização. Isso inclui informações sobre o nome do atributo calculado, a descrição, a data da última avaliação e o status da última avaliação.

![A variável [!UICONTROL Perfil] seção e o [!UICONTROL Atributos computados] as guias são destacadas, mostrando aos usuários como acessar a página de navegação de atributos calculados.](./images/ui/browse.png)

Para selecionar quais campos estarão visíveis, você pode selecionar ![o ícone configurar colunas](./images/ui/configure-icon.png) para adicionar ou remover os campos que devem ser exibidos.

| Campo | Descrição |
| ----- | ----------- |
| [!UICONTROL Nome] | O nome de exibição do atributo calculado. |
| [!UICONTROL Descrição] | A descrição do atributo calculado. |
| [!UICONTROL Método de avaliação] | O método de avaliação do atributo calculado. Neste momento, apenas **lote** é compatível. |
| [!UICONTROL Última avaliação] | Esse carimbo de data e hora representa a última execução de avaliação bem-sucedida. Somente eventos que ocorreram **antes** esse carimbo de data e hora é considerado na última avaliação bem-sucedida. |
| [!UICONTROL Status da última avaliação] | O status que indica se o atributo calculado foi ou não calculado com êxito na última execução de avaliação. Os valores possíveis incluem **[!UICONTROL Sucesso]** ou **[!UICONTROL Failed]**. |
| [!UICONTROL Frequência de atualização] | Uma indicação da frequência com que o atributo calculado deve ser atualizado. Os valores possíveis incluem por hora, dia, semana ou mês. |
| [!UICONTROL Atualização rápida] | Um valor que mostra se a atualização rápida está ou não ativada para este atributo de computação. Se a atualização rápida estiver ativada, o atributo calculado poderá ser atualizado diariamente, em vez de semanalmente, quinzenalmente ou mensalmente. Esse valor só é aplicável para atributos calculados com um período de lookback maior que uma base semanal. |
| [!UICONTROL Status do ciclo de vida] | O status atual do atributo calculado. Há três status possíveis: <ul><li>**[!UICONTROL Rascunho]:** O atributo calculado não **não** já tem um campo criado no esquema. Nesse estado, o atributo calculado pode ser editado. </li><li>**[!UICONTROL Publicado]:** O atributo computado tem um campo criado no esquema e está pronto para ser usado. Nesse estado, o atributo calculado **não é possível** ser editado.</li><li>**[!UICONTROL Inativo]:** O atributo computado está desabilitado. Para obter mais informações sobre o status inativo, leia a [Página de perguntas frequentes](./faq.md#inactive-status). </li> |
| [!UICONTROL Criado] | Um carimbo de data e hora que mostra a data e a hora em que o atributo calculado foi criado. |
| [!UICONTROL Última modificação] | Um carimbo de data e hora que mostra a data e a hora em que o atributo calculado foi modificado pela última vez. |

Você também pode filtrar os atributos calculados exibidos com base no status do ciclo de vida. Selecione o ![funil](./images/ui/filter-icon.png) ícone.

![O ícone de filtro é realçado.](./images/ui/select-filter.png)

Agora é possível optar por filtrar os atributos calculados por status ([!UICONTROL Rascunho], [!UICONTROL Publicado], e [!UICONTROL Inativo]).

![As opções pelas quais você pode filtrar os atributos calculados são destacadas. Essas opções incluem [!UICONTROL Rascunho], [!UICONTROL Publicado], e [!UICONTROL Inativo].](./images/ui/view-filters.png)

Além disso, você pode selecionar um atributo calculado para ver informações mais detalhadas sobre ele. Para obter mais informações sobre a página de detalhes dos atributos calculados, leia a [exibir a seção detalhes de um atributo calculado](#view-details).

## Criar um atributo calculado {#create}

Para criar um novo atributo calculado, selecione **[!UICONTROL Criar atributo calculado]** para inserir o novo fluxo de trabalho de atributo calculado.

![A variável [!UICONTROL Criar atributos computados] é realçado, mostrando aos usuários como acessar a página criar um atributo calculado.](./images/ui/create.png)

A variável **[!UICONTROL Criar atributo calculado]** é exibida. Nesta página, você pode adicionar as informações básicas para o atributo calculado que deseja criar.

| Campo | Descrição |
| ----- | ----------- |
| [!UICONTROL Nome de exibição] | O nome pelo qual o atributo calculado será conhecido. Você deve manter esse nome de exibição exclusivo para cada atributo calculado. Como prática recomendada, esse nome de exibição deve conter identificadores relacionados ao atributo calculado. Por exemplo, &quot;Soma das compras de sapatos nos últimos 7 dias&quot;. |
| [!UICONTROL Nome do campo] | Um nome usado para fazer referência ao atributo calculado em outros serviços downstream. Esse nome é automaticamente derivado do nome de exibição e é gravado em camelCase. |
| [!UICONTROL Descrição] | Uma descrição do atributo calculado que você está tentando criar. |

![A variável [!UICONTROL Informações básicas] seção do [!UICONTROL Criar atributo calculado] é realçada.](./images/ui/basic-information.png)

Depois de adicionar os detalhes do atributo calculado, você pode começar a definir suas regras.

### Especificar condições de filtragem de eventos

Para criar uma regra, selecione primeiro os atributos na **[!UICONTROL Eventos]** para filtrar os eventos nos quais deseja agregar. No momento, somente atributos de evento do tipo não array são compatíveis.

![A variável [!UICONTROL Eventos] é realçada.](./images/ui/events.png)

Após selecionar o atributo a ser usado na definição de atributo calculado, você pode escolher a que esse valor será comparado.

![Os tipos de comparação disponíveis são exibidos.](./images/ui/select-comparison.png)

### Aplicar função de agregação

Agora, você pode aplicar uma função ao campo da saída condicional. Primeiro, selecione o tipo de função de agregação. As opções disponíveis incluem [!UICONTROL Sum], [!UICONTROL Min], [!UICONTROL Máx], [!UICONTROL Contagem], e [!UICONTROL Mais recente]. Mais informações sobre essas funções podem ser encontradas na seção [seção funções](./overview.md#functions) da visão geral dos atributos calculados.

![As funções de atributo computadas são exibidas.](./images/ui/select-function.png)

Após escolher uma função, você pode escolher o campo no qual agregar. Os campos elegíveis a serem escolhidos dependem da função selecionada.

![O campo destacado mostra o atributo no qual você está escolhendo agregar a função.](./images/ui/select-eligible-field.png)

### Duração da pesquisa

Depois de aplicar a função de agregação, será necessário definir o período de lookback do atributo calculado. Esse período de pesquisa especifica o período no qual você deseja agregar eventos. Essa duração da pesquisa pode ser especificada em termos de horas, dias, semanas ou meses.

![A duração da pesquisa é realçada.](./images/ui/select-lookback-duration.png)

### Atualização rápida {#fast-refresh}

>[!CONTEXTUALHELP]
>id="platform_profile_computedAttributes_fastRefresh"
>title="Atualização rápida"
>abstract="A atualização rápida permite manter seus atributos atualizados. Ativar essa opção permite atualizar os atributos calculados diariamente, mesmo por períodos de lookback mais longos, permitindo que você reaja rapidamente às atividades do usuário. Esse valor só é aplicável para atributos calculados com um período de lookback maior que uma base semanal."

Ao aplicar a função de agregação, você poderá ativar a atualização rápida se o período de lookback for maior que uma semana.

![A variável [!UICONTROL Atualização rápida] é realçada.](./images/ui/enable-fast-refresh.png)

A atualização rápida permite manter seus atributos atualizados. Ativar essa opção permite atualizar os atributos calculados diariamente, mesmo por períodos de lookback mais longos, permitindo que você reaja rapidamente às atividades do usuário.

Para obter mais informações sobre atualização rápida, leia a [seção atualização rápida](./overview.md#fast-refresh) da visão geral dos atributos calculados.

Com essas etapas concluídas, agora é possível optar por salvar esse atributo calculado como rascunho ou publicá-lo imediatamente.

![A variável [!UICONTROL Salvar como rascunho] e [!UICONTROL Publish] Os botões são realçados.](./images/ui/draft-or-publish.png)

## Exibir detalhes de um atributo calculado {#view-details}

Para exibir os detalhes de um atributo calculado, selecione o atributo calculado sobre o qual deseja ver detalhes na [!UICONTROL **Procurar**] página.

![Um atributo calculado é realçado.](./images/ui/select.png)

O conteúdo da página é diferente, dependendo se o atributo calculado é **[!UICONTROL Publicado]** ou em **[!UICONTROL Rascunho]**.

### Atributo calculado publicado {#published}

Ao selecionar um atributo calculado publicado, a página de detalhes dos atributos calculados é exibida.

![A página de detalhes do atributo calculado é exibida.](./images/ui/details.png)

Esta página exibe um resumo dos detalhes do atributo calculado, bem como um gráfico mostrando a distribuição do valor e perfis de amostra que se qualificam para o atributo calculado.

>[!NOTE]
>
>A distribuição de valores reflete a distribuição de valores de atributos para perfis no momento do trabalho de amostragem. O valor do atributo calculado no perfil de amostra reflete o valor do perfil mesclado mais recente para alguns perfis de amostra.

### Rascunho do atributo calculado {#draft}

Ao selecionar um rascunho de atributo calculado, a variável **[!UICONTROL Editar atributos computados]** é exibida. Esta página, de forma semelhante à [!UICONTROL Criar atributos computados] permite editar as informações básicas do atributo calculado, bem como sua definição, antes de permitir a atualização do rascunho ou a publicação.

![A variável [!UICONTROL Editar atributos computados] é exibida.](./images/ui/edit.png)

## Uso de atributos computados {#usage}

Depois de criar um atributo calculado, você pode usar **publicado** atributos computados em outros serviços downstream. Como os atributos calculados são campos de atributo de perfil criados no esquema de união de perfis, você pode pesquisar valores de atributo calculados para um Perfil de cliente em tempo real, usá-los em um público-alvo, ativá-los para um destino ou usá-los para personalização no jornada na Adobe Journey Optimizer.

![O Construtor de segmentos é exibido, mostrando um atributo calculado como parte da composição de definição de segmentos.](./images/ui/use-ca.png)

## Próximas etapas

Para saber mais sobre atributos computados, leia a [visão geral dos atributos computados](./overview.md). Para obter informações sobre como criar e configurar atributos computados usando a API, leia os [guia do desenvolvedor de atributos computados](./api.md).
