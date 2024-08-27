---
title: Visão geral do modo Query Pro
description: Saiba como usar consultas SQL na interface do usuário do Adobe Experience Platform para gerar gráficos para seus painéis personalizados.
exl-id: 15c664c4-8546-4e04-b81d-c78bf83500d3
source-git-commit: 0970fd8fbea86115d92dc78cdba753da69cc2ee6
workflow-type: tm+mt
source-wordcount: '1062'
ht-degree: 0%

---

# Visão geral do modo Query pro {#query-pro-mode}

O modo profissional de consulta é um fluxo de trabalho baseado no editor SQL que orienta você pelo processo de geração de insights com consultas SQL personalizadas na interface do Adobe Experience Platform. Antes de gerar insights com consultas SQL personalizadas, primeiro você deve [criar um painel](./overview.md#create-custom-dashboard).

## Compor SQL {#compose-sql}

Depois que você optar por criar um painel com o modo query pro, a caixa de diálogo **[!UICONTROL Inserir SQL]** será exibida. Selecione um banco de dados (modelo de dados do insights) para consultar no menu suspenso e insira uma consulta adequada para seu conjunto de dados no editor do query pro.

>[!NOTE]
>
>O modo Query pro está disponível somente para usuários que compraram o SKU do Data Distiller. O [[!UICONTROL Modo de design guiado]](../../user-defined-dashboards.md) está disponível a todos os usuários para criar insights de um modelo de dados existente.

Consulte o [Guia do usuário do Editor de Consultas](../../../query-service/ui/user-guide.md#query-authoring) para obter informações sobre seus elementos de interface.

![A caixa de diálogo [!UICONTROL Inserir SQL] com o menu suspenso do conjunto de dados e o ícone de execução foram realçados. A caixa de diálogo tem uma consulta SQL preenchida e a guia de parâmetros de consulta é exibida.](../../images/sql-insights/enter-sql-database-dropdown.png)

### Parâmetros de consulta {#query-parameters}

Para incluir [filtros globais](./filters/global-filter.md) ou [filtros de data](./filters/date-filter.md), sua consulta **deve** usar parâmetros de consulta. Ao compor sua instrução no modo query pro, você deve fornecer valores de amostra se sua consulta usar parâmetros de consulta. Os valores de amostra permitem executar a instrução SQL e criar o gráfico. Observe que os valores de amostra fornecidos ao compor a instrução são substituídos pelos valores reais selecionados para o filtro de data ou global no tempo de execução.

>[!IMPORTANT]
>
>Se quiser usar um filtro global, você deve colocar um parâmetro de consulta em seu SQL e, em seguida, vincular esse parâmetro de consulta ao filtro global no compositor de widgets. Na captura de tela abaixo, `CONSENT_VALUE_FILTER` é usado no SQL como um parâmetro de consulta para um filtro global. Consulte a [documentação do filtro global](./filters/global-filter.md#enable-global-filter) para obter mais informações sobre como fazer isso.

Para executar a consulta, selecione o ícone executar (![O ícone executar.](/help/images/icons/play.png)). O Editor de consultas exibe a guia resultados. Em seguida, para confirmar sua configuração e abrir o widget composer, selecione **[!UICONTROL Selecionar]**.

>[!TIP]
>
>Se sua consulta usa parâmetros de consulta, execute a consulta uma vez para preencher previamente todas as chaves de parâmetros de consulta usadas. A consulta falhará, mas a interface do usuário exibirá automaticamente a guia Parâmetros de consulta e listará todas as chaves incluídas. Adicione os valores apropriados para suas chaves.

![A caixa de diálogo [!UICONTROL Inserir SQL] com entrada SQL, a guia de resultados exibida e Selecionar realçado.](../../images/sql-insights/enter-sql-select.png)

## Preencher widget {#populate-widget}

O widget composer agora é preenchido com as colunas do SQL executado. O tipo de painel é indicado no canto superior esquerdo; neste caso, é [!UICONTROL Entrada de SQL Manual]. Selecione o ícone de lápis (![Um ícone de lápis.](/help/images/icons/edit.png)) para editar o SQL a qualquer momento.

>[!TIP]
>
>Os atributos disponíveis são colunas retiradas do SQL executado.

Para criar o widget, use os atributos listados na coluna [!UICONTROL Atributos]. Você pode usar a barra de pesquisa para procurar atributos ou rolar a lista.

![O widget composer com o método de criação e a coluna de atributo realçados.](../../images/sql-insights/creation-method-and-attribute-column.png)

### Adicionar atributos {#add-attributes}

Para adicionar um atributo ao seu widget, selecione o ícone de adição (![Um ícone de adição.](/help/images/icons/add-circle.png)) ao lado de um nome de atributo. O menu suspenso exibido permite adicionar um atributo ao gráfico a partir das opções determinadas pelo seu SQL. Tipos de gráficos diferentes têm opções diferentes, como uma lista suspensa dos eixos X e Y.

Neste exemplo de gráfico de rosca, as opções são tamanho e cor. A cor detalha os resultados do gráfico de rosca e o tamanho é a métrica real usada. Adicione um atributo ao campo [!UICONTROL Cor] para dividir os resultados em cores diferentes com base em sua composição desse atributo.

>[!TIP]
>
>Selecione o ícone de seta para cima e para baixo (![O ícone de seta para cima e para baixo.](/help/images/icons/switch.png)) para alternar a disposição dos eixos X e Y em gráficos de barras ou de linhas.

![O widget composer com o ícone de adição suspenso e as setas de alternância realçadas.](../../images/sql-insights/add-icon-and-switch-arrows.png)

Para alterar o tipo de gráfico do seu widget, selecione uma das opções disponíveis na lista suspensa [!UICONTROL Marcas]. As opções incluem [!UICONTROL Linha], [!UICONTROL Rosca], [!UICONTROL Número grande] e [!UICONTROL Barra]. Uma vez selecionado, uma visualização prévia das configurações atuais do seu widget é gerada.

![O compositor de widget com a visualização de widget realçada.](../../images/sql-insights/widget-preview.png)

## Propriedades do dispositivo {#properties}

Selecione o ícone de propriedades (![O ícone de propriedades.](/help/images/icons/properties.png)) no painel direito para abrir o painel de propriedades. No painel [!UICONTROL Propriedades], digite um nome para o widget no campo de texto **[!UICONTROL Título do widget]**. Também é possível renomear vários aspectos do gráfico.

>[!NOTE]
>
>Os campos específicos disponíveis na barra lateral de propriedades variam de acordo com o tipo de gráfico que você está editando.

![O widget composer com o ícone de propriedades e o campo Título do widget realçados.](../../images/sql-insights/widget-properties-title-text.png)

## Salve o widget {#save-widget}

Salvar no widget composer salva o widget localmente no painel. Para salvar seu trabalho e retomá-lo mais tarde, selecione **[!UICONTROL Salvar]**. Um ícone de marca de verificação abaixo do nome do widget indica que o widget foi salvo. Como alternativa, quando estiver satisfeito com o widget, selecione **[!UICONTROL Salvar e fechar]** para disponibilizá-lo para todos os outros usuários com acesso ao painel. Selecione Cancelar para abandonar o trabalho e retornar ao painel personalizado.

![O widget composer com Salvar, Widget salvo e Salvar e fechar realçado.](../../images/sql-insights/insight-saved.png)

## Editar seu painel e gráficos {#edit}

Selecione **[!UICONTROL Editar]** para editar todo o painel ou qualquer um dos seus insights. No modo de edição, você pode redimensionar widgets, editar o SQL ou criar e aplicar filtros globais e temporais. Esses filtros restringem os dados exibidos nos widgets do painel. É uma maneira conveniente de atualizar e ajustar rapidamente seus insights para casos de uso diferentes.

![Um painel personalizado com a opção Editar realçada.](../../images/sql-insights/edit-dashboard.png)

Selecione **[!UICONTROL Adicionar filtro]** para criar um [[!UICONTROL filtro de datas]](#create-date-filter) ou um [[!UICONTROL filtro global]](#create-global-filter). Depois de criado, todos os filtros globais e de data estarão disponíveis no [ícone de filtro](#select-global-filter) (![ícone de filtro.](/help/images/icons/filter.png)) do seu painel.

![Um painel personalizado com o menu suspenso Adicionar filtro realçado.](../../images/query-pro-mode/add-filter.png)

## Editar, duplicar ou excluir um insight

Consulte o guia Painel Personalizado para obter instruções sobre como [editar, duplicar ou excluir um widget existente](../../user-defined-dashboards.md#duplicate).

## Próximas etapas

Depois de ler este documento, agora você sabe como gravar consultas SQL na interface do usuário do Adobe Experience Platform para gerar gráficos para seus painéis personalizados. Em seguida, saiba como enriquecer ainda mais seus dados [criando um filtro de datas](./filters/date-filter.md) ou [criando um filtro global](./filters/global-filter.md).

Você também pode saber mais sobre outros recursos de Insights Personalizados, incluindo [as diferentes opções de exibição para seus dados analisados por SQL](./view-more.md) ou como [exibir o SQL por trás de seus insights personalizados](./view-sql.md).
