---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;tópicos populares;analisar blocos de dados
solution: Experience Platform
title: Analise seus dados usando notebooks
type: Tutorial
description: Este tutorial foca em como usar o Jupyter Notebooks, integrado ao Data Science Workspace, para acessar, explorar e visualizar seus dados.
exl-id: 3b0148d1-9c08-458b-9601-979cb6c7a0fb
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1727'
ht-degree: 0%

---

# Analisar seus dados usando blocos de anotações

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

Este tutorial foca em como usar o Jupyter Notebooks, integrado ao Data Science Workspace, para acessar, explorar e visualizar seus dados. Ao final deste tutorial, você deve entender alguns dos recursos que o Jupyter Notebooks oferece para entender melhor seus dados.

São introduzidos os seguintes conceitos:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) é a interface baseada na Web de próxima geração para o Projeto Jupyter, e está totalmente integrada ao [!DNL Adobe Experience Platform].
- **Lotes:** conjuntos de dados são compostos de lotes. Um lote é um conjunto de dados coletados por um período e processados juntos como uma única unidade. Novos lotes são criados quando dados são adicionados a um conjunto de dados.
- **Data Access SDK (desaprovado):** O Data Access SDK foi descontinuado. Use o guia [[!DNL Experience Platform SDK]](../authoring/platform-sdk.md).

## Explore notebooks no Data Science Workspace

Nesta seção, são explorados os dados que foram assimilados anteriormente no esquema de vendas de varejo.

O Data Science Workspace permite que os usuários criem [!DNL Jupyter Notebooks] por meio da plataforma [!DNL JupyterLab], onde podem criar e editar fluxos de trabalho de aprendizado de máquina. O [!DNL JupyterLab] é uma ferramenta de colaboração servidor-cliente que permite aos usuários editar documentos do bloco de anotações via navegador da Web. Esses blocos de anotações podem conter código executável e elementos rich text. Para nossos propósitos, usaremos o Markdown para descrição de análise e código [!DNL Python] executável para realizar exploração e análise de dados.

### Escolha seu espaço de trabalho

Ao iniciar o [!DNL JupyterLab], nos é apresentada uma interface baseada na Web para o Jupyter Notebooks. Dependendo do tipo de notebook escolhido, o kernel correspondente será iniciado.

Ao comparar qual ambiente usar, devemos considerar as limitações de cada serviço. Por exemplo, se estamos usando a biblioteca [pandas](https://pandas.pydata.org/) com [!DNL Python], como usuário comum, o limite de RAM é de 2 GB. Mesmo sendo um usuário avançado, estaríamos limitados a 20 GB de RAM. Se estiver lidando com computações maiores, faria sentido usar [!DNL Spark] que oferece 1,5 TB que é compartilhado com todas as instâncias do bloco de anotações.

Por padrão, a fórmula Tensorflow funciona em um cluster GPU e o Python é executado em um cluster CPU.

### Criar um novo bloco de anotações

Na interface do usuário do [!DNL Adobe Experience Platform], selecione [!UICONTROL Data Science] no menu superior para direcionar você ao Data Science Workspace. Nesta página, selecione [!DNL JupyterLab] para abrir o inicializador [!DNL JupyterLab]. Você deverá ver uma página semelhante a esta.

![](../images/jupyterlab/analyze-data/jupyterlab-launcher-new.png)

Em nosso tutorial, usaremos o [!DNL Python] 3 no Jupyter Notebook para mostrar como acessar e explorar os dados. Na página do Iniciador, há blocos de anotações de exemplo fornecidos. Vamos usar a receita de Vendas a Varejo para [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

A fórmula de Vendas de varejo é um exemplo independente que usa o mesmo conjunto de dados de Vendas de varejo para mostrar como os dados podem ser explorados e visualizados no Jupyter Notebook. Além disso, o notebook aprofunda-se em treinamento e verificação. Mais informações sobre este bloco de anotações específico podem ser encontradas nesta [apresentação](../walkthrough.md).

### Acessar dados

>[!NOTE]
>
>O `data_access_sdk_python` está obsoleto e não é mais recomendado. Consulte o tutorial [conversão de acesso a dados do SDK para o Experience Platform SDK](../authoring/platform-sdk.md) para converter seu código. As mesmas etapas abaixo ainda se aplicam a este tutorial.

Acessaremos os dados internamente de [!DNL Adobe Experience Platform] e os dados externamente. Usaremos a biblioteca `data_access_sdk_python` para acessar dados internos, como conjuntos de dados e esquemas XDM. Para dados externos, usaremos a biblioteca [!DNL Python] de pandas.

#### Dados externos

Com o bloco de anotações Vendas de varejo aberto, localize o cabeçalho &quot;Carregar dados&quot;. O código [!DNL Python] a seguir usa a estrutura de dados `DataFrame` dos pandas e a função [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) para ler o CSV hospedado em [!DNL Github] no DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

A estrutura de dados DataFrame de Pandas é uma estrutura de dados rotulada bidimensional. Para ver rapidamente as dimensões de nossos dados, podemos usar o `df.shape`. Isso retorna uma tupla que representa a dimensionalidade do DataFrame:

![](../images/jupyterlab/analyze-data/df_shape.png)

Por fim, podemos dar uma olhada em como são nossos dados. Podemos usar `df.head(n)` para exibir as primeiras `n` linhas do DataFrame:

![](../images/jupyterlab/analyze-data/df_head.png)

#### Dados de [!DNL Experience Platform]

Agora, vamos acessar os dados de [!DNL Experience Platform].

##### Por ID do conjunto de dados

Para esta seção, estamos usando o conjunto de dados de Vendas de varejo, que é o mesmo conjunto de dados usado no bloco de anotações de amostra Vendas de varejo.

No Jupyter Notebook, você pode acessar os dados da **guia Dados** ![guia Dados](../images/jupyterlab/analyze-data/dataset-tab.png) à esquerda. Ao selecionar a guia, duas pastas são fornecidas. Selecione a pasta **[!UICONTROL Datasets]**.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Agora, no diretório Conjuntos de dados, você pode ver todos os conjuntos de dados assimilados. Observe que pode levar um minuto para carregar todas as entradas se o diretório estiver muito preenchido com conjuntos de dados.

Como o conjunto de dados é o mesmo, queremos substituir os dados de carregamento da seção anterior que usa dados externos. Selecione o bloco de código em **Carregar Dados** e pressione a tecla **&#39;d&#39;** duas vezes no teclado. Verifique se o foco está no bloco e não no texto. Você pode pressionar **&#39;esc&#39;** para escapar do foco de texto antes de pressionar **&#39;d&#39;** duas vezes.

Agora, podemos clicar com o botão direito do mouse no conjunto de dados `Retail-Training-<your-alias>` e selecionar a opção &quot;Explorar dados no Bloco de Anotações&quot; na lista suspensa. Uma entrada de código executável será exibida no bloco de anotações.

>[!TIP]
>
>Consulte o guia [[!DNL Experience Platform SDK]](../authoring/platform-sdk.md) para converter seu código.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Se você estiver trabalhando em outros kernels além de [!DNL Python], consulte [esta página](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) para acessar dados sobre [!DNL Adobe Experience Platform].

Selecionar a célula executável e pressionar o botão Reproduzir na barra de ferramentas executará o código executável. A saída para `head()` será uma tabela com as chaves do seu conjunto de dados como colunas e as primeiras n linhas no conjunto de dados. `head()` aceita um argumento inteiro para especificar quantas linhas serão geradas. Por padrão, é 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Se você reiniciar seu kernel e executar todas as células novamente, você deve obter os mesmos resultados de antes.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Explore seus dados

Agora que podemos acessar seus dados, vamos nos concentrar nos próprios dados usando estatísticas e visualização. O conjunto de dados que estamos usando é um conjunto de dados de varejo que fornece informações diversas sobre 45 lojas diferentes em um determinado dia. Algumas características para um determinado `date` e `store` incluem o seguinte:

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

Podemos usar a biblioteca de pandas do [!DNL Python's] para obter o tipo de dados de cada atributo. A saída da chamada a seguir fornecerá informações sobre o número de entradas e o tipo de dados para cada uma das colunas:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Essas informações são úteis, pois conhecer o tipo de dados de cada coluna nos permitirá saber como tratar os dados.

Agora vamos olhar o resumo estatístico. Somente os tipos de dados numéricos serão exibidos, portanto, `date`, `storeType` e `isHoliday` não serão gerados:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

Com isso, podemos ver que há 6.435 ocorrências para cada característica. Além disso, informações estatísticas como média, desvio padrão (padrão), mín, máx e interquartis são fornecidas. Isso nos fornece informações sobre o desvio dos dados. Na próxima seção, veremos a visualização que funciona junto com essas informações para nos dar uma boa compreensão de nossos dados.

Observando os valores mínimo e máximo para `store`, podemos ver que há 45 armazenamentos únicos que os dados representam. Há também `storeTypes` que diferenciam o que é um armazenamento. Podemos ver a distribuição de `storeTypes` fazendo o seguinte:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Isso significa que 22 lojas são de `storeType` `A`, 17 são `storeType` `B` e 6 são `storeType` `C`.

#### Visualização de dados

Agora que conhecemos os valores de quadro de dados, queremos complementar isso com visualizações para tornar as coisas mais claras e fáceis de identificar padrões. Os gráficos também são úteis ao transmitir resultados para um público-alvo. Algumas bibliotecas do [!DNL Python] que são úteis para visualização incluem:

- [Matplotlib](https://matplotlib.org/)
- [pandas](https://pandas.pydata.org/)
- [seaborn](https://seaborn.pydata.org/)
- [gráfico](https://ggplot2.tidyverse.org/)

Nesta seção, abordaremos rapidamente algumas vantagens do uso de cada biblioteca.

[Matplotlib](https://matplotlib.org/) é o pacote de visualização [!DNL Python] mais antigo. Seu objetivo é tornar &quot;coisas fáceis e difíceis possíveis&quot;. Isso tende a ser verdade, pois o pacote é extremamente eficiente, mas também vem com complexidade. Nem sempre é fácil obter um gráfico de aparência razoável sem tomar uma quantidade considerável de tempo e esforço.

[Pandas](https://pandas.pydata.org/) é usado principalmente para seu objeto DataFrame, que permite manipulação de dados com indexação integrada. No entanto, pandas também inclui uma funcionalidade de plotagem incorporada que é baseada em matplotlib.

[seaborn](https://seaborn.pydata.org/) é uma compilação de pacote sobre matplotlib. Seu principal objetivo é tornar os gráficos padrão mais visualmente atraentes e simplificar a criação de gráficos complicados.

[ggplot](https://ggplot2.tidyverse.org/) é um pacote que também foi criado sobre matplotlib. No entanto, a principal diferença é que a ferramenta é uma porta de gplot2 para R. Semelhante a seaborn, o objetivo é melhorar em matplotlib. Os usuários familiarizados com o ggplot2 para R devem considerar essa biblioteca.


##### Gráficos univariados

Gráficos univariados são gráficos de uma variável individual. Um gráfico univariado comum é usado para visualizar seus dados na plotagem de caixa e bigode.

Usando nosso conjunto de dados de varejo de antes, podemos gerar o gráfico de caixa e bigode para cada uma das 45 lojas e suas vendas semanais. O gráfico é gerado usando a função `seaborn.boxplot`.

![](../images/jupyterlab/analyze-data/box_whisker.png)

Um gráfico de caixa e bigode é usado para mostrar a distribuição de dados. As linhas externas do gráfico mostram os quartis superior e inferior, enquanto a caixa abrange o intervalo interquartil. A linha na caixa marca a mediana. Quaisquer pontos de dados maiores que 1,5 vez o quartil superior ou inferior são marcados como um círculo. Esses pontos são considerados outliers.

##### Gráficos multivariado

Gráficos multivariados são usados para ver a interação entre variáveis. Com a visualização, os cientistas de dados podem ver se há correlações ou padrões entre as variáveis. Um gráfico multivariado comum usado é uma matriz de correlação. Com uma matriz de correlação, as dependências entre múltiplas variáveis são quantificadas com o coeficiente de correlação.

Usando o mesmo conjunto de dados de varejo, podemos gerar a matriz de correlação.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Observe a diagonal de 1&#39;s abaixo do centro. Isso mostra que, ao comparar uma variável com ela mesma, ela tem uma correlação positiva completa. Correlação positiva forte terá uma magnitude mais próxima de 1, enquanto correlações fracas estarão mais próximas de 0. A correlação negativa é mostrada com um coeficiente negativo mostrando uma tendência inversa.


## Próximas etapas

Este tutorial abordou como criar um novo Jupyter Notebook no Data Science Workspace e como acessar dados externamente e do [!DNL Adobe Experience Platform]. Especificamente, analisamos as seguintes etapas:

- Criar um novo Jupyter Notebook
- Acessar conjuntos de dados e esquemas
- Explorar conjuntos de dados

Agora você está pronto para seguir para a [próxima seção](../models-recipes/package-source-files-recipe.md) para empacotar uma fórmula e importar para o Data Science Workspace.
