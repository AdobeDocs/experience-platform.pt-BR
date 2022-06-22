---
keywords: Experience Platform; JupyterLab; notebooks; Data Science Workspace; tópicos populares; analisar notebooks de dados
solution: Experience Platform
title: Analise seus dados usando notebooks
topic-legacy: tutorial
type: Tutorial
description: Este tutorial foca em como usar notebooks Júpiter, criados no Data Science Workspace, para acessar, explorar e visualizar seus dados.
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: 1e240c710da3fa7ae863377d044308b0bca47c7f
workflow-type: tm+mt
source-wordcount: '1724'
ht-degree: 0%

---

# Analise seus dados usando blocos de anotações

Este tutorial foca em como usar notebooks Júpiter, criados no Data Science Workspace, para acessar, explorar e visualizar seus dados. Ao final deste tutorial, você deve conhecer alguns dos recursos que os notebooks Júpiter oferecem para entender melhor seus dados.

Os seguintes conceitos são introduzidos:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) O é a interface baseada na Web de próxima geração para o Project Júpiter e é totalmente integrada ao [!DNL Adobe Experience Platform].
- **Lotes:** Os conjuntos de dados são compostos de lotes. Um lote é um conjunto de dados coletados durante um período de tempo e processados juntos como uma única unidade. Novos lotes são criados quando os dados são adicionados a um conjunto de dados.
- **SDK de acesso a dados (obsoleto):** O SDK de acesso a dados agora está obsoleto. Use o [[!DNL Platform SDK]](../authoring/platform-sdk.md) guia.

## Explore notebooks no Data Science Workspace

Nesta seção, são explorados dados que foram assimilados anteriormente no schema de vendas de varejo.

O Data Science Workspace permite que os usuários criem [!DNL Jupyter Notebooks] através da [!DNL JupyterLab] plataforma onde podem criar e editar fluxos de trabalho de aprendizado de máquina. [!DNL JupyterLab] O é uma ferramenta de colaboração servidor-cliente que permite aos usuários editar documentos do notebook por meio de um navegador da Web. Esses blocos de anotações podem conter código executável e elementos rich text. Para nossos propósitos, usaremos o Markdown para a descrição da análise e executável [!DNL Python] código para executar exploração e análise de dados.

### Escolha seu espaço de trabalho

Ao iniciar [!DNL JupyterLab], uma interface baseada na Web para notebooks Júpiter é apresentada. Dependendo do tipo de notebook que escolher, um kernel correspondente será iniciado.

Ao comparar qual ambiente usar, devemos considerar as limitações de cada serviço. Por exemplo, se estivermos usando a variável [pandas](https://pandas.pydata.org/) biblioteca com [!DNL Python], como usuário regular, o limite de RAM é de 2 GB. Mesmo como um usuário avançado, estaríamos limitados a 20 GB de RAM. Se estiver lidando com computações maiores, faria sentido usar [!DNL Spark] que oferece 1,5 TB compartilhados com todas as instâncias de notebook.

Por padrão, a fórmula do Tensorflow funciona em um cluster da GPU e o Python é executado em um cluster da CPU.

### Criar um novo bloco de notas

No [!DNL Adobe Experience Platform] UI, selecione [!UICONTROL Ciência de dados] no menu superior para levá-lo ao Data Science Workspace. Nesta página, selecione [!DNL JupyterLab] para abrir o [!DNL JupyterLab] iniciador. Você deve ver uma página semelhante a esta.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

Em nosso tutorial, estaremos usando [!DNL Python] 3 no notebook Júpiter para mostrar como acessar e explorar os dados. Na página do Launcher, há amostras de blocos de anotações fornecidos. Usaremos a receita de vendas de varejo para [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

A receita de Vendas de varejo é um exemplo independente que usa o mesmo conjunto de dados de Vendas de varejo para mostrar como os dados podem ser explorados e visualizados no Notebook de Júpiter. Além disso, o notebook vai mais fundo com treinamento e verificação. Mais informações sobre este notebook específico podem ser encontradas neste [explicação passo a passo](../walkthrough.md).

### Acessar dados

>[!NOTE]
>
>O `data_access_sdk_python` for descontinuado e não for mais recomendado. Consulte a [conversão do SDK de acesso aos dados para o SDK da plataforma](../authoring/platform-sdk.md) tutorial para converter seu código. As mesmas etapas abaixo ainda se aplicam a este tutorial.

Vamos acessar os dados internamente a partir de [!DNL Adobe Experience Platform] e dados externamente. Usaremos o `data_access_sdk_python` para acessar dados internos, como conjuntos de dados e esquemas XDM. Para dados externos, usaremos os pandas [!DNL Python] biblioteca.

#### Dados externos

Com o bloco de anotações Vendas de varejo aberto, localize o cabeçalho &quot;Carregar dados&quot;. O seguinte [!DNL Python] o código usa pandas&#39; `DataFrame` estrutura de dados e [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) para ler o CSV hospedado em [!DNL Github] no DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

A estrutura de dados DataFrame dos painéis é uma estrutura de dados bidimensional rotulada como. Para ver rapidamente as dimensões de nossos dados, podemos usar o `df.shape`. Isso retorna uma tupla que representa a dimensionalidade do DataFrame:

![](../images/jupyterlab/analyze-data/df_shape.png)

Por fim, podemos dar uma espiada na aparência dos nossos dados. Podemos usar `df.head(n)` para visualizar o primeiro `n` linhas do DataFrame:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] dados

Agora, vamos voltar a acessar [!DNL Experience Platform] dados.

##### Por ID de conjunto de dados

Para esta seção, estamos usando o conjunto de dados de Vendas de varejo que é o mesmo conjunto de dados usado no bloco de notas de amostra de Vendas de varejo.

No notebook Júpiter, você pode acessar seus dados a partir do **Dados** guia ![guia dados](../images/jupyterlab/analyze-data/dataset-tab.png) à esquerda. Ao selecionar a guia , duas pastas são fornecidas. Selecione o **[!UICONTROL Conjuntos de dados]** pasta.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Agora, no diretório Conjuntos de dados, você pode ver todos os conjuntos de dados assimilados. Observe que pode levar um minuto para carregar todas as entradas se o diretório estiver amplamente preenchido com conjuntos de dados.

Como o conjunto de dados é o mesmo, queremos substituir os dados de carregamento da seção anterior que usa dados externos. Selecione o bloco de código em **Carregar dados** e pressione a tecla **&quot;d&quot;** duas vezes no teclado. Verifique se o foco está no bloco e não no texto. Pode pressionar **&#39;esc&#39;** para escapar do foco do texto antes de pressionar **&quot;d&quot;** duas vezes.

Agora, podemos clicar com o botão direito do mouse no `Retail-Training-<your-alias>` conjunto de dados e selecione a opção &quot;Explorar dados no notebook&quot; na lista suspensa. Uma entrada de código executável será exibida no seu notebook.

>[!TIP]
>
>Consulte a [[!DNL Platform SDK]](../authoring/platform-sdk.md) para converter seu código.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Se você estiver trabalhando em outros kernels diferentes de [!DNL Python], consulte [esta página](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) para acessar dados no [!DNL Adobe Experience Platform].

Selecionar a célula executável e pressionar o botão Reproduzir na barra de ferramentas executará o código executável. A saída para `head()` será uma tabela com as chaves do conjunto de dados como colunas e as primeiras n linhas no conjunto de dados. `head()` aceita um argumento inteiro para especificar quantas linhas serão geradas. Por padrão, é 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Se você reiniciar o kernel e executar todas as células novamente, você deverá obter os mesmos resultados de antes.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Explorar seus dados

Agora que podemos acessar seus dados, vamos nos concentrar nos próprios dados usando estatísticas e visualização. O conjunto de dados que estamos usando é um conjunto de dados de varejo que fornece informações diversas sobre 45 lojas diferentes em um determinado dia. Algumas características de um determinado `date` e `store` Incluir o seguinte:
- `storeType`
- `weeklySales`
- `storeSize`
- `temperature`
- `regionalFuelPrice`
- `markDown`
- `cpi`
- `unemployment`
- `isHoliday`

#### Resumo estatístico

Podemos aproveitar [!DNL Python's] biblioteca de painéis para obter o tipo de dados de cada atributo. A saída da chamada a seguir fornecerá informações sobre o número de entradas e o tipo de dados para cada uma das colunas:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Essas informações são úteis, pois conhecer o tipo de dados de cada coluna nos permitirá saber como tratar os dados.

Agora vamos olhar para o resumo estatístico. Somente os tipos de dados numéricos serão exibidos, portanto `date`, `storeType`e `isHoliday` não terá saída:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

Com isso, podemos ver que há 6.435 instâncias para cada característica. Além disso, são fornecidas informações estatísticas como média, desvio padrão (std), mín, máx e interquartis. Isso nos fornece informações sobre o desvio dos dados. Na próxima seção, analisaremos a visualização que funciona junto com essas informações para nos dar uma boa compreensão de nossos dados.

Analisando os valores mínimo e máximo para `store`, podemos ver que há 45 armazenamentos exclusivos que os dados representam. Há também `storeTypes` que diferenciam o que é uma loja. Podemos ver a distribuição de `storeTypes` fazendo o seguinte:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Isso significa que 22 lojas são de `storeType` `A`, 17 são `storeType` `B`e 6 são `storeType` `C`.

#### Visualização de dados

Agora que conhecemos nossos valores do quadro de dados, queremos complementar com visualizações para tornar as coisas mais claras e fáceis de identificar padrões. Os gráficos também são úteis ao transmitir resultados para um público-alvo. Algumas [!DNL Python] as bibliotecas que são úteis para visualização incluem:
- [Matplotlib](https://matplotlib.org/)
- [pandas](https://pandas.pydata.org/)
- [seaborn](https://seaborn.pydata.org/)
- [gráfico](https://ggplot2.tidyverse.org/)

Nesta seção, rapidamente analisaremos algumas vantagens do uso de cada biblioteca.

[Matplotlib](https://matplotlib.org/) é o mais antigo [!DNL Python] pacote de visualização. O objetivo deles é tornar &quot;coisas fáceis e difíceis possíveis&quot;. Isto tende a ser verdade, uma vez que o pacote é extremamente poderoso, mas também vem com complexidade. Nem sempre é fácil obter um gráfico razoável sem se gastar um tempo e um esforço consideráveis.

[Pandas](https://pandas.pydata.org/) é usada principalmente para seu objeto DataFrame, que permite a manipulação de dados com indexação integrada. No entanto, os pandas também incluem uma funcionalidade de plotamento integrada, baseada em matplotlib.

[seaborn](https://seaborn.pydata.org/) é uma build de pacote na parte superior do matplotlib. Seu principal objetivo é tornar os gráficos padrão mais atraentes visualmente e simplificar a criação de gráficos complicados.

[gráfico](https://ggplot2.tidyverse.org/) O é um pacote também criado sobre o matplotlib. No entanto, a principal diferença é que a ferramenta é uma porta de ggplot2 para R. Semelhante à seaborn, o objetivo é melhorar com o matplotlib. Os usuários familiarizados com o ggplot2 for R devem considerar esta biblioteca.


##### Gráficos Univariáveis

Gráficos de variação única são gráficos de uma variável individual. Um gráfico universal comum é usado para visualizar seus dados é a caixa e o gráfico de uísque.

Usando nosso conjunto de dados de varejo de antes, podemos gerar a caixa e o gráfico de uísque para cada uma das 45 lojas e suas vendas semanais. O gráfico é gerado usando o `seaborn.boxplot` .

![](../images/jupyterlab/analyze-data/box_whisker.png)

Um gráfico de caixa e uísque é usado para mostrar a distribuição de dados. As linhas externas do gráfico mostram os quartis superior e inferior, enquanto a caixa se estende pelo intervalo interquartil. A linha na caixa marca a mediana. Quaisquer pontos de dados mais de 1,5 vezes o quartil superior ou inferior são marcados como um círculo. Esses pontos são considerados outliers.

##### Gráficos multivariados

Os gráficos multivariados são usados para ver a interação entre variáveis. Com a visualização, os cientistas de dados podem ver se há correlações ou padrões entre as variáveis. Um gráfico multivariado comum usado é uma matriz de correlação. Com uma matriz de correlação, as dependências entre várias variáveis são quantificadas com o coeficiente de correlação.

Usando o mesmo conjunto de dados de varejo, podemos gerar a matriz de correlação.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Observe a diagonal de 1&#39;s no centro. Isso mostra que, ao comparar uma variável a si mesma, ela tem uma correlação positiva completa. Uma correlação positiva forte terá uma magnitude mais próxima de 1, enquanto correlações fracas estarão mais próximas de 0. A correlação negativa é mostrada com um coeficiente negativo que mostra uma tendência inversa.


## Próximas etapas

Este tutorial foi sobre como criar um novo Notebook Júpiter no Data Science Workspace e como acessar dados externamente e do [!DNL Adobe Experience Platform]. Especificamente, nós passamos pelas seguintes etapas:
- Criar um novo notebook Jupyter
- Acessar conjuntos de dados e esquemas
- Explorar conjuntos de dados

Agora você está pronto para ir para a [próxima seção](../models-recipes/package-source-files-recipe.md) para empacotar uma receita e importá-la para o Data Science Workspace.
