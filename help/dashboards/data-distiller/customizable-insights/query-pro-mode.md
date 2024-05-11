---
title: Modo Query Pro
description: Saiba como usar consultas SQL na interface do usuário do Adobe Experience Platform para gerar gráficos para seus painéis personalizados.
source-git-commit: 17ad52864bbca09844c0241b6451e6811bd8f413
workflow-type: tm+mt
source-wordcount: '1060'
ht-degree: 0%

---

# Modo pro da consulta {#query-pro-mode}

O modo profissional de consulta é um fluxo de trabalho baseado no editor SQL que orienta você pelo processo de geração de insights com consultas SQL personalizadas na interface do Adobe Experience Platform. Antes de gerar insights com consultas SQL personalizadas, primeiro você deve [criar um painel](./overview.md#create-custom-dashboard).

## Compor SQL {#compose-sql}

Depois de criar um painel com o modo query pro, a variável **[!UICONTROL Inserir SQL]** será exibida. Selecione um banco de dados (modelo de dados do insights) para consultar no menu suspenso e insira uma consulta adequada para seu conjunto de dados no editor do query pro.

>[!NOTE]
>
>O modo Query pro está disponível somente para usuários que compraram o SKU do Data Distiller. A variável [[!UICONTROL Modo de design guiado]](../../user-defined-dashboards.md) O está disponível a todos os usuários para criar insights de um modelo de dados existente.

Consulte a [Guia do usuário do Editor de consultas](../../../query-service/ui/user-guide.md#query-authoring) para obter informações sobre os elementos da interface.

![A variável [!UICONTROL Inserir SQL] com o menu suspenso do conjunto de dados e o ícone de executar destacado, a caixa de diálogo tem uma consulta SQL preenchida e a guia de parâmetros de consulta exibida.](../../images/customizable-insights/enter-sql-database-dropdown.png)

### Parâmetros de consulta {#query-parameters}

Para incluir [global](./filters/global-filter.md) ou [filtros de data](./filters/date-filter.md) sua consulta **deve** usar parâmetros de consulta. Ao compor sua instrução no modo query pro, você deve fornecer valores de amostra se sua consulta usar parâmetros de consulta. Os valores de amostra permitem executar a instrução SQL e criar o gráfico. Observe que os valores de amostra fornecidos ao compor a instrução são substituídos pelos valores reais selecionados para o filtro de data ou global no tempo de execução.



>[!IMPORTANT]
>
>Se quiser usar um filtro global, você deve colocar um parâmetro de consulta em seu SQL e, em seguida, vincular esse parâmetro de consulta ao filtro global no compositor de widgets. Na captura de tela abaixo, `CONSENT_VALUE_FILTER` é usado no SQL como um parâmetro de consulta para um filtro global. Consulte a [documentação do filtro global](./filters/global-filter.md#enable-global-filter) para obter mais informações sobre como fazer isso.

Para executar o query, selecione o ícone executar (![O ícone de execução.](../../images/customizable-insights/run-icon.png)). O Editor de consultas exibe a guia resultados. Em seguida, para confirmar sua configuração e abrir o widget composer, selecione **[!UICONTROL Selecionar]**.

>[!TIP]
>
>Se sua consulta usa parâmetros de consulta, execute a consulta uma vez para preencher previamente todas as chaves de parâmetros de consulta usadas. A consulta falhará, mas a interface do usuário exibirá automaticamente a guia Parâmetros de consulta e listará todas as chaves incluídas. Adicione os valores apropriados para suas chaves.

![A variável [!UICONTROL Inserir SQL] com entrada SQL, a guia results exibida e Select realçado.](../../images/customizable-insights/enter-sql-select.png)

## Preencher widget {#populate-widget}

O widget composer agora é preenchido com as colunas do SQL executado. O tipo de painel é indicado no canto superior esquerdo, nesse caso, é [!UICONTROL Entrada Manual de SQL]. Selecione o ícone de lápis (![Um lápis.](../../images/customizable-insights/edit-icon.png)) para editar o SQL a qualquer momento.

>[!TIP]
>
>Os atributos disponíveis são colunas retiradas do SQL executado.

Para criar o widget, use os atributos listados na [!UICONTROL Atributos] coluna. Você pode usar a barra de pesquisa para procurar atributos ou rolar a lista.

![O compositor de widgets com o método de criação e a coluna de atributos realçados.](../../images/customizable-insights/creation-method-and-attribute-column.png)

### Adicionar atributos {#add-attributes}

Para adicionar um atributo ao widget, selecione o ícone de adição (![Um ícone de adição.](../../images/customizable-insights/add-icon.png)) ao lado de um nome de atributo. O menu suspenso exibido permite adicionar um atributo ao gráfico a partir das opções determinadas pelo seu SQL. Tipos de gráficos diferentes têm opções diferentes, como uma lista suspensa dos eixos X e Y.

Neste exemplo de gráfico de rosca, as opções são tamanho e cor. A cor detalha os resultados do gráfico de rosca e o tamanho é a métrica real usada. Adicionar um atributo à variável [!UICONTROL Cor] para dividir os resultados em cores diferentes com base em sua composição desse atributo.

>[!TIP]
>
>Selecione o ícone de seta para cima e para baixo (![O ícone de seta para cima e para baixo.](../../images/customizable-insights/switch-axis-icon.png)) para alternar a disposição dos eixos X e Y em gráficos de barras ou de linhas.

![O compositor de widgets com a lista suspensa de ícones adicionar e as setas de alternância realçadas.](../../images/customizable-insights/add-icon-and-switch-arrows.png)

Para alterar o tipo de gráfico do seu widget, selecione uma das opções disponíveis do [!UICONTROL Marcas] lista suspensa. As opções incluem [!UICONTROL Linha], [!UICONTROL Rosca], [!UICONTROL Número grande], e [!UICONTROL Barra]. Uma vez selecionado, uma visualização prévia das configurações atuais do seu widget é gerada.

![O compositor de widgets com a visualização do widget realçada.](../../images/customizable-insights/widget-preview.png)

## Propriedades do widget {#properties}

Selecione o ícone de propriedades (![O ícone de propriedades.](../../images/customizable-insights/properties-icon.png)) no painel direito para abrir o painel de propriedades. No [!UICONTROL Propriedades] insira um nome para o widget na caixa **[!UICONTROL Título do widget]** campo de texto. Também é possível renomear vários aspectos do gráfico.

>[!NOTE]
>
>Os campos específicos disponíveis na barra lateral de propriedades variam de acordo com o tipo de gráfico que você está editando.

![O compositor de widgets com o ícone de propriedades e o campo Título do widget realçados.](../../images/customizable-insights/widget-properties-title-text.png)

## Salve o widget {#save-widget}

Salvar no widget composer salva o widget localmente no painel. Para salvar seu trabalho e retomar o trabalho mais tarde, selecione **[!UICONTROL Salvar]**. Um ícone de marca de verificação abaixo do nome do widget indica que o widget foi salvo. Como alternativa, quando estiver satisfeito com o widget, selecione **[!UICONTROL Salvar e fechar]** para disponibilizar o widget para todos os outros usuários com acesso ao painel. Selecione Cancelar para abandonar o trabalho e retornar ao painel personalizado.

![O compositor de widgets com Salvar, Widget salvo e Salvar e fechar realçado.](../../images/customizable-insights/insight-saved.png)

## Editar seu painel e gráficos {#edit}

Selecionar **[!UICONTROL Editar]** para editar todo o painel ou qualquer um dos insights. No modo de edição, você pode redimensionar widgets, editar o SQL ou criar e aplicar filtros globais e temporais. Esses filtros restringem os dados exibidos nos widgets do painel. É uma maneira conveniente de atualizar e ajustar rapidamente seus insights para casos de uso diferentes.

![Um painel personalizado com Editar realçado.](../../images/customizable-insights/edit-dashboard.png)

Selecionar **[!UICONTROL Adicionar filtro]** para criar um [[!UICONTROL Filtro de data]](#create-date-filter) ou um [[!UICONTROL Filtro global]](#create-global-filter). Depois de criados, todos os filtros globais e de data ficam disponíveis no [o ícone de filtro](#select-global-filter) (![Um ícone de filtro.](../../images/customizable-insights/filter.png)) do seu painel.

![Um painel personalizado com o menu suspenso Adicionar filtro realçado.](../../images/customizable-insights/add-filter.png)

## Editar, duplicar ou excluir um insight

Consulte o guia Painel personalizado para obter instruções sobre como [editar, duplicar ou excluir um widget existente](../../user-defined-dashboards.md#duplicate).

## Próximas etapas

Depois de ler este documento, agora você sabe como gravar consultas SQL na interface do usuário do Adobe Experience Platform para gerar gráficos para seus painéis personalizados. Em seguida, você deve aprender a enriquecer ainda mais seus dados [criação de um filtro de datas](./filters/date-filter.md)ou [criação de um filtro global](./filters/global-filter.md).

Você também pode saber mais sobre outros recursos do Insights personalizados, incluindo [as diferentes opções de exibição para seus dados analisados por SQL](./view-more.md) ou como [visualizar o SQL por trás de seus insights personalizados](./view-sql.md).
