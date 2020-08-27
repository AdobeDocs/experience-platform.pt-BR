---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;analyze data notebooks
solution: Experience Platform
title: Analise seus dados usando notebooks
topic: Tutorial
description: Este tutorial foca em como usar notebooks Júpiter, criados na Data Science Workspace, para acessar, explorar e visualizar seus dados.
translation-type: tm+mt
source-git-commit: 43d568a401732a753553847dee1b4a924fcc24fd
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 0%

---


# Analise seus dados usando notebooks

Este tutorial foca em como usar notebooks Júpiter, criados na Data Science Workspace, para acessar, explorar e visualizar seus dados. Até o final deste tutorial, você deve conhecer alguns dos recursos da oferta de notebooks Júpiter para entender melhor seus dados.

São introduzidos os seguintes conceitos:

- **[!DNL JupyterLab]:** [[!DNL JupyterLab]](https://blog.jupyter.org/jupyterlab-is-ready-for-users-5a6f039b8906) é a interface baseada na Web da próxima geração do Project Júpitter e está totalmente integrado ao Project [!DNL Adobe Experience Platform].
- **Lotes:** Os conjuntos de dados são compostos de lotes. Um lote é um conjunto de dados coletados durante um período de tempo e processados juntos como uma única unidade. Novos lotes são criados quando os dados são adicionados a um conjunto de dados.
- **SDK de acesso a dados (obsoleto):** O SDK de acesso a dados agora está obsoleto. Use o guia [[!DNL Platform SDK]](../authoring/platform-sdk.md) .

## Explore notebooks na Data Science Workspace

Nesta seção, são explorados dados que foram ingeridos anteriormente no schema de vendas de varejo.

A Data Science Workspace permite que os usuários criem [!DNL Jupyter Notebooks] por meio da [!DNL JupyterLab] plataforma, onde podem criar e editar workflows de aprendizado de máquina. [!DNL JupyterLab] é uma ferramenta de colaboração cliente-servidor que permite que os usuários editem documentos de notebook por meio de um navegador da Web. Esses notebooks podem conter código executável e elementos Rich Text. Para nossos propósitos, usaremos o Markdown para descrição da análise e código executável [!DNL Python] para realizar a exploração e a análise de dados.

### Escolher a área de trabalho

Ao inicializar [!DNL JupyterLab], nos é apresentada uma interface baseada na Web para notebooks Júpiter. Dependendo do tipo de notebook escolhido, um kernel correspondente será iniciado.

Ao comparar qual ambiente usar, devemos considerar as limitações de cada serviço. Por exemplo, se estivermos usando a biblioteca de [pandas](https://pandas.pydata.org/) com [!DNL Python], como usuário comum, o limite de RAM é de 2 GB. Mesmo como um usuário avançado, estaríamos limitados a 20 GB de RAM. Se você estiver lidando com computadores maiores, faria sentido usar [!DNL Spark] quais ofertas de 1,5 TB são compartilhadas com todas as instâncias de notebook.

Por padrão, a fórmula do Tensorflow funciona em um cluster de GPU e o Python é executado em um cluster de CPU.

### Criar um novo bloco de anotações

Na [!DNL Adobe Experience Platform] interface do usuário, clique na guia Data Science no menu superior para levá-lo à Data Science Workspace. Nesta página, clique na [!DNL JupyterLab] guia que abrirá o [!DNL JupyterLab] iniciador. Você deve ver uma página semelhante a esta.

![](../images/jupyterlab/analyze-data/jupyterlab_launcher.png)

Em nosso tutorial, estaremos usando o [!DNL Python] 3 no notebook de Júpiter para mostrar como acessar e explorar os dados. Na página Iniciador, há exemplos de notebooks fornecidos. Usaremos a receita de vendas de varejo para [!DNL Python] 3.

![](../images/jupyterlab/analyze-data/retail_sales.png)

A receita de vendas de varejo é um exemplo independente que usa o mesmo conjunto de dados de vendas de varejo para mostrar como os dados podem ser explorados e visualizados no notebook de Júpiter. Além disso, o notebook vai mais fundo com o treinamento e a verificação. Mais informações sobre este notebook específico podem ser encontradas nesta [apresentação](../walkthrough.md).

### Dados de acesso

>[!NOTE]
>
>O `data_access_sdk_python` está obsoleto e não é mais recomendado. Consulte o tutorial de [conversão do SDK de acesso aos dados para SDK](../authoring/platform-sdk.md) da plataforma para converter seu código. As mesmas etapas abaixo ainda se aplicam a este tutorial.

Nós iremos acessar dados internamente de [!DNL Adobe Experience Platform] e dados externamente. Usaremos a `data_access_sdk_python` biblioteca para acessar dados internos, como conjuntos de dados e schemas XDM. Para dados externos, usaremos a biblioteca de [!DNL Python] pandas.

#### Dados externos

Com o bloco de anotações Vendas de varejo aberto, localize o cabeçalho &quot;Carregar dados&quot;. O [!DNL Python] código a seguir usa a estrutura `DataFrame` de dados dos pandas e a função [read_csv()](https://pandas.pydata.org/pandas-docs/stable/generated/pandas.read_csv.html#pandas.read_csv) para ler o CSV hospedado [!DNL Github] no DataFrame:

![](../images/jupyterlab/analyze-data/read_csv.png)

A estrutura de dados DataFrame dos painéis é uma estrutura de dados identificada em duas dimensões. Para ver rapidamente as dimensões dos nossos dados, podemos usar o `df.shape`. Isso retorna uma tupla que representa a dimensionalidade do DataFrame:

![](../images/jupyterlab/analyze-data/df_shape.png)

Finalmente, podemos dar uma olhada em como são os nossos dados. Podemos usar `df.head(n)` para visualização das primeiras `n` linhas do DataFrame:

![](../images/jupyterlab/analyze-data/df_head.png)

#### [!DNL Experience Platform] dados

Agora, vamos voltar a acessar [!DNL Experience Platform] os dados.

##### Por ID do conjunto de dados

Para esta seção, estamos usando o conjunto de dados de Vendas de varejo que é o mesmo conjunto de dados usado no notebook de amostra de Vendas de varejo.

Em nosso notebook de Júpiter, podemos acessar nossos dados na guia **Dados** à esquerda. Ao clicar na guia, você poderá ver uma lista de conjuntos de dados.

![](../images/jupyterlab/analyze-data/dataset_tab.png)

Agora, no diretório Conjuntos de dados, poderemos ver todos os conjuntos de dados assimilados. Observe que pode levar um minuto para carregar todas as entradas se o diretório estiver muito preenchido com conjuntos de dados.

Como o conjunto de dados é o mesmo, queremos substituir os dados de carregamento da seção anterior que usa dados externos. Selecione o bloco de código em **Carregar dados** e pressione duas vezes a tecla **&#39;d&#39;** no teclado. Verifique se o foco está no bloco e não no texto. Você pode pressionar **&#39;esc&#39;** para escapar do foco do texto antes de pressionar **&#39;d&#39;** duas vezes.

Agora, podemos clicar com o botão direito do mouse no `Retail-Training-<your-alias>` conjunto de dados e selecionar a opção &quot;Explorar dados no notebook&quot; na lista suspensa. Uma entrada de código executável será exibida no seu notebook.

>[!TIP]
>
>consulte o guia [[!DNL Platform SDK]](../authoring/platform-sdk.md) para converter seu código.

```PYTHON
from data_access_sdk_python.reader import DataSetReader
from datetime import date
reader = DataSetReader()
df = reader.load(data_set_id="xxxxxxxx", ims_org="xxxxxxxx@AdobeOrg")
df.head()
```

Se você estiver trabalhando em outros kernels diferentes [!DNL Python], consulte [esta página](https://github.com/adobe/acp-data-services-dsw-reference/wiki/Accessing-Data-on-the-Platform) para acessar os dados no [!DNL Adobe Experience Platform].

Selecionar a célula executável e pressionar o botão reproduzir na barra de ferramentas executará o código executável. A saída para `head()` será uma tabela com as chaves do conjunto de dados como colunas e as primeiras n linhas do conjunto de dados. `head()` aceita um argumento inteiro para especificar quantas linhas serão geradas. Por padrão, é 5.

![](../images/jupyterlab/analyze-data/datasetreader_head.png)

Se você reiniciar o kernel e executar todas as células novamente, você deverá obter as mesmas saídas que antes.

![](../images/jupyterlab/analyze-data/restart_kernel_run.png)


### Explore seus dados

Agora que podemos acessar seus dados, vamos focar nos próprios dados usando estatísticas e visualização. O conjunto de dados que estamos usando é um conjunto de dados de varejo que fornece informações diversas sobre 45 lojas diferentes em um determinado dia. Algumas características de um determinado `date` e `store` incluem:
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

Podemos aproveitar a biblioteca de [!DNL Python's] pandas para obter o tipo de dados de cada atributo. A saída da chamada a seguir nos fornecerá informações sobre o número de entradas e o tipo de dados para cada uma das colunas:

```PYTHON
df.info()
```

![](../images/jupyterlab/analyze-data/df_info.png)

Essas informações são úteis, pois conhecer o tipo de dados para cada coluna permitirá que saibamos como tratar os dados.

Agora vamos olhar para o resumo estatístico. Somente os tipos de dados numéricos serão exibidos, portanto `date`, `storeType`e não `isHoliday` serão enviados:

```PYTHON
df.describe()
```

![](../images/jupyterlab/analyze-data/df_describe.png)

Com isso, podemos ver que existem 6.435 instâncias para cada característica. Além disso, são fornecidas informações estatísticas como média, desvio padrão (std), mín., máx. e interquartis. Isso nos fornece informações sobre o desvio dos dados. Na próxima seção, nós iremos ver a visualização que funciona junto com esta informação para nos dar uma boa compreensão dos nossos dados.

Analisando os valores mínimo e máximo para `store`, podemos ver que existem 45 armazenamentos exclusivos que os dados representam. Há também `storeTypes` que diferenciam o que é uma loja. Podemos ver a distribuição do `storeTypes` ao fazer o seguinte:

![](../images/jupyterlab/analyze-data/df_groupby.png)

Isso significa que 22 lojas são de `storeType` 6, 17 são `A`, e 6 são `storeType``B``storeType` `C`.

#### Visualização de dados

Agora que conhecemos nossos valores de quadro de dados, queremos complementá-los com visualizações para tornar as coisas mais claras e fáceis de identificar padrões. Os gráficos também são úteis ao transmitir resultados para uma audiência. Algumas [!DNL Python] bibliotecas úteis para a visualização incluem:
- [Matplotlib](https://matplotlib.org/)
- [pandas](https://pandas.pydata.org/)
- [seaborna](https://seaborn.pydata.org/)
- [conspiração](https://ggplot2.tidyverse.org/)

Nesta seção, iremos analisar rapidamente algumas vantagens do uso de cada biblioteca.

[Matplotlib](https://matplotlib.org/) é o pacote de [!DNL Python] visualização mais antigo. O objetivo deles é tornar &quot;coisas fáceis e difíceis possíveis&quot;. Isso tende a ser verdade, já que o pacote é extremamente poderoso, mas também vem com complexidade. Nem sempre é fácil obter um gráfico com uma aparência razoável, sem precisar de muito tempo e esforço.

[Os painéis](https://pandas.pydata.org/) são usados principalmente para seu objeto DataFrame, que permite a manipulação de dados com indexação integrada. No entanto, os pandas também incluem uma funcionalidade integrada de plotagem, que é baseada em matplotlib.

[seaborn](https://seaborn.pydata.org/) é uma compilação de pacote sobre o matplotlib. Seu principal objetivo é tornar os gráficos padrão mais atraentes visualmente e simplificar a criação de gráficos complicados.

[ggpload](https://ggplot2.tidyverse.org/) é um pacote também construído sobre o matplotlib. Mas a principal diferença é que a ferramenta é uma porta de diagrama2 para R. Semelhante ao seaborn, o objetivo é melhorar o matplotlib. Os usuários que estiverem familiarizados com o ggpload2 for R devem considerar esta biblioteca.


##### Gráficos de variação única

Gráficos de variação única são gráficos de uma variável individual. Um gráfico univariado comum é usado para visualizar seus dados é a caixa e o gráfico de uísque.

Usando nosso conjunto de dados de varejo de antes, podemos gerar a caixa e o gráfico de uísque para cada uma das 45 lojas e suas vendas semanais. O gráfico é gerado usando a `seaborn.boxplot` função.

![](../images/jupyterlab/analyze-data/box_whisker.png)

Um gráfico de caixa e uísque é usado para mostrar a distribuição de dados. As linhas exteriores da parcela mostram os quartis superior e inferior, enquanto a caixa se estende pelo intervalo interquartil. A linha na caixa marca a mediana. Quaisquer pontos de dados mais de 1,5 vezes o quartil superior ou inferior são marcados como um círculo. Estes pontos são considerados exceções.

##### Gráficos multivariados

Os gráficos multivariados são usados para ver a interação entre variáveis. Com a visualização, os cientistas de dados podem ver se há correlações ou padrões entre as variáveis. Um gráfico multivariado comum usado é uma matriz de correlação. Com uma matriz de correlação, as dependências entre várias variáveis são quantificadas com o coeficiente de correlação.

Usando o mesmo conjunto de dados de varejo, podemos gerar a matriz de correlação.

![](../images/jupyterlab/analyze-data/correlation_1.png)

Observe a diagonal de 1 ao centro. Isso mostra que ao comparar uma variável com ela mesma, ela tem uma correlação positiva completa. Uma forte correlação positiva terá uma magnitude mais próxima de 1, enquanto correlações fracas estarão mais próximas de 0. A correlação negativa é mostrada com um coeficiente negativo que mostra uma tendência inversa.


## Próximas etapas

Este tutorial abordou como criar um novo notebook Júpiter na Data Science Workspace e como acessar dados externamente e de [!DNL Adobe Experience Platform]. Especificamente, passamos pelos seguintes passos:
- Crie um novo notebook Jupyter
- Acessar conjuntos de dados e schemas
- Explorar conjuntos de dados

Agora você está pronto para ir para a [próxima seção](../models-recipes/package-source-files-recipe.md) para disponibilizar uma receita e importá-la para a Data Science Workspace.