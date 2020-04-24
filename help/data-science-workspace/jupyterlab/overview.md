---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Guia do usuário do JupyterLab
topic: Overview
translation-type: tm+mt
source-git-commit: 19823c7cf0459e045366f0baae2bd8a98416154c

---


# Guia do usuário do JupyterLab

O JupyterLab é uma interface de usuário baseada na Web para o <a href="https://jupyter.org/" target="_blank">Project Júpitter</a> e é totalmente integrado à Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para que os cientistas de dados trabalhem com notebooks, códigos e dados de Júpiter.

Este documento fornece uma visão geral do JupyterLab e seus recursos, bem como instruções para executar ações comuns.

## JupyterLab na plataforma Experience

A integração do JupyterLab da plataforma Experience é acompanhada de mudanças arquitetônicas, considerações de design, extensões personalizadas de notebook, bibliotecas pré-instaladas e uma interface temática da Adobe.

A lista a seguir descreve alguns dos recursos exclusivos do JupyterLab na plataforma:

| Recurso | Descrição |
| --- | --- |
| **Kernels** | Os kernels fornecem notebook e outros front-ends do JupyterLab, a habilidade de executar e inserir código em diferentes linguagens de programação. A plataforma Experience fornece kernels adicionais para suportar o desenvolvimento em Python, R, PySpark e Spark. Consulte a seção [kernels](#kernels) para obter mais detalhes. |
| **Acesso aos dados** | Acesse conjuntos de dados existentes diretamente do JupyterLab com suporte total para recursos de leitura e gravação. |
| **Integração do serviço da plataforma** | As integrações integradas permitem utilizar outros serviços da plataforma diretamente do JupyterLab. Uma lista completa de integrações compatíveis é fornecida na seção [Integração com outros serviços](#service-integration)da plataforma. |
| **Autenticação** | Além do modelo <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">de segurança integrado do</a>JupyterLab, todas as interações entre seu aplicativo e a Plataforma de experiência, incluindo a comunicação serviço a serviço da plataforma, são criptografadas e autenticadas pelo <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">Adobe Identity Management System (IMS)</a>. |
| **Bibliotecas de desenvolvimento** | Na plataforma Experience, o JupyterLab fornece bibliotecas pré-instaladas para Python, R e PySpark. Consulte o [apêndice](#supported-libraries) para obter uma lista completa das bibliotecas suportadas. |
| **Controladora de biblioteca** | Quando as bibliotecas pré-instaladas não atendem às suas necessidades, bibliotecas adicionais podem ser instaladas para Python e R, e são temporariamente armazenadas em container isolados para manter a integridade da Plataforma e seus dados protegidos. Consulte a seção [kernels](#kernels) para obter mais detalhes. |

>[!NOTE] As bibliotecas adicionais só estão disponíveis para a sessão em que foram instaladas. É necessário reinstalar as bibliotecas adicionais necessárias ao iniciar novas sessões.

## Integração com outros serviços da plataforma {#service-integration}

A normalização e a interoperabilidade são conceitos-chave por trás da plataforma da experiência. A integração do JupyterLab na plataforma como um IDE incorporado permite que ele interaja com outros serviços da plataforma, permitindo que você utilize a plataforma ao seu potencial total. Os seguintes serviços da plataforma estão disponíveis no JupyterLab:

* **Serviço de catálogo:** Acesse e explore conjuntos de dados com funcionalidades de leitura e gravação.
* **Serviço de Query:** Acesse e explore conjuntos de dados usando SQL, fornecendo custos indiretos de acesso a dados mais baixos ao lidar com grandes quantidades de dados.
* **Sensei ML Framework:** Desenvolvimento de modelo com a capacidade de treinar e pontuar dados, bem como criação de receita com um único clique.

>[!NOTE] Algumas integrações de serviço da plataforma no JupyterLab estão limitadas a kernels específicos. Consulte a seção sobre [kernels](#kernels) para obter mais detalhes.

## Principais recursos e operações comuns

As informações sobre os principais recursos do JupyterLab e as instruções para executar operações comuns são fornecidas nas seções abaixo:

* [Access JupyterLab](#access-jupyterlab)
* [Interface JupyterLab](#jupyterlab-interface)
* [Células de código](#code-cells)
* [Kernels](#kernels)
* [Sessões do kernel](#kernel-sessions)
* [Recurso de execução PySpark/Spark](#execution-resource)
* [Iniciador](#launcher)

### Access JupyterLab {#access-jupyterlab}

Na plataforma [](https://platform.adobe.com)Adobe Experience, selecione **Notebooks** na coluna de navegação esquerda. Aguarde até que o JupyterLab inicialize completamente.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### Interface JupyterLab {#jupyterlab-interface}

A interface do JupyterLab consiste em uma barra de menus, uma barra lateral esquerda flexível e a área de trabalho principal contendo guias de documentos e atividades.

**Barra de menus**

A barra de menus na parte superior da interface tem menus de nível superior que expõem as ações disponíveis no JupyterLab com seus atalhos de teclado:

* **Arquivo:** Ações relacionadas a arquivos e diretórios
* **Editar:** Ações relacionadas à edição de documentos e outras atividades
* **Visualização:** Ações que alteram a aparência de JupyterLab
* **Executar:** Ações para executar código em diferentes atividades, como notebooks e consoles de código
* **Kernel:** Ações para gerenciar kernels
* **Guias:** Uma lista de documentos e atividades abertos
* **Configurações:** Configurações comuns e um editor de configurações avançado
* **Ajuda:** Uma lista dos links de ajuda do JupyterLab e do kernel

**Barra lateral esquerda**

A barra lateral esquerda contém guias clicáveis que fornecem acesso aos seguintes recursos:

* **Navegador de arquivos:** Uma lista de documentos e diretórios de notebook salvos
* **Explorador de dados:** Procurar, acessar e explorar schemas e conjuntos de dados
* **Corredores e terminais:** Uma lista de sessões ativas de kernel e terminal com a capacidade de encerrar
* **Comandos:** Uma lista de comandos úteis
* **Inspetor de células:** Um editor de células que fornece acesso a ferramentas e metadados úteis para configurar um bloco de anotações para fins de apresentação
* **guias:** Uma lista de guias abertas

Clique em uma guia para expor seus recursos, ou clique em uma guia expandida para recolher a barra lateral esquerda, como demonstrado abaixo:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Principal área de trabalho**

A área de trabalho principal no JupyterLab permite organizar documentos e outras atividades em painéis de guias que podem ser redimensionados ou subdivididos. Arraste uma guia até o centro de um painel de guias para migrar a guia. Divida um painel arrastando uma guia para a esquerda, direita, superior ou inferior do painel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Células de código {#code-cells}

As células de código são o conteúdo principal dos notebooks. Eles contêm o código fonte no idioma do kernel associado do notebook e a saída como resultado da execução da célula de código. Uma contagem de execução é exibida à direita de cada célula de código que representa sua ordem de execução.

![](../images/jupyterlab/user-guide/code_cell.png)

As ações celulares comuns estão descritas abaixo:

* **Adicionar uma célula:** Clique no sinal de mais (**+**) no menu do bloco de anotações para adicionar uma célula vazia. Novas células são colocadas sob a célula que está sendo interagida atualmente com, ou no final do notebook se nenhuma célula específica estiver em foco.

* **Mover uma célula:** Posicione o cursor à direita da célula que deseja mover e clique e arraste a célula para um novo local. Além disso, mover uma célula de um notebook para outro replica a célula junto com seu conteúdo.

* **Executar uma célula:** Clique no corpo da célula que deseja executar e clique no ícone **reproduzir** (**▶**) no menu do notebook. Um asterisco (**\***) é exibido no contador de execução da célula quando o kernel processa a execução e é substituído por um número inteiro após a conclusão.

* **Excluir uma célula:** Clique no corpo da célula que deseja excluir e clique no ícone da **tesoura** .

### Kernels {#kernels}

Os kernels notebook são os mecanismos de computação específicos da linguagem para processar células de notebook. Além de Python, o JupyterLab fornece suporte adicional para idiomas em R, PySpark e Spark. Quando você abre um documento notebook, o kernel associado é iniciado. Quando uma célula do notebook é executada, o kernel executa o cálculo e produz resultados que podem consumir recursos significativos da CPU e da memória. Observe que a memória alocada não é liberada até que o kernel seja desligado.

>[!IMPORTANT] JupyterLab Launcher atualizado do Spark 2.3 para o Spark 2.4. Os kernels Spark e PySpark não são mais compatíveis com os notebooks Spark 2.4.

Determinados recursos e funcionalidades estão limitados a kernels específicos, conforme descrito no quadro abaixo:

| Kernel | Suporte à instalação da biblioteca | Integrações de plataforma |
| :----: | :--------------------------: | :-------------------- |
| **Python** | Sim | <ul><li>Sensei ML Framework</li><li>Serviço de catálogo</li><li>Serviço de Query</li></ul> |
| **R** | Sim | <ul><li>Sensei ML Framework</li><li>Serviço de catálogo</li></ul> |
| **PySpark - obsoleto** | Não | <ul><li>Sensei ML Framework</li><li>Serviço de catálogo</li></ul> |
| **Spark - obsoleto** | Não | <ul><li>Sensei ML Framework</li><li>Serviço de catálogo</li></ul> |
| **Scala** | Não | <ul><li>Sensei ML Framework</li><li>Serviço de catálogo</li></ul> |

### Sessões do kernel {#kernel-sessions}

Cada notebook ativo ou atividade no JupyterLab utiliza uma sessão de kernel. Todas as sessões ativas podem ser encontradas ao expandir a guia Terminais **em execução e kernels** na barra lateral esquerda. O tipo e o estado do kernel de um notebook podem ser identificados observando a parte superior direita da interface do notebook. No diagrama abaixo, o kernel associado ao notebook é o **Python 3** e seu estado atual é representado por um círculo cinza à direita. Um círculo oco implica um kernel ocioso e um círculo sólido implica um kernel ocupado.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Se o kernel estiver desligado ou inativo por um período prolongado, então **Nenhum kernel!** com um círculo sólido é mostrado. Ative um kernel clicando no status do kernel e selecionando o tipo de kernel apropriado, conforme demonstrado abaixo:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Recurso de execução PySpark/Spark {#execution-resource}

>[!IMPORTANT]
>Com a transição do Spark 2.3 para o Spark 2.4, os kernels Spark e PySpark estão obsoletos.
>
>Os novos notebooks PySpark 3 (Spark 2.4) usam o kernel Python3. Consulte o guia sobre a conversão do [Pyspark 3 (Spark 2.3) em PySpark 3 (Spark 2.4)](../recipe-notebook-migration.md) para obter um tutorial detalhado sobre a atualização dos notebooks existentes.
>
>Os novos notebooks Spark devem utilizar o kernel Scala. Consulte o guia sobre a conversão do [Spark 2.3 em Scala (Spark 2.4)](../recipe-notebook-migration.md) para obter um tutorial detalhado sobre a atualização dos notebooks existentes.

Os kernels PySpark e Spark permitem que você configure os recursos do cluster Spark no seu notebook PySpark ou Spark usando o comando configure (`%%configure`) e fornecendo uma lista de configurações. Idealmente, essas configurações são definidas antes da inicialização do aplicativo Spark. A modificação das configurações enquanto o aplicativo Spark está ativo requer um sinalizador de força adicional após o comando (`%%configure -f`) que reiniciará o aplicativo para que as alterações sejam aplicadas, como mostrado abaixo:

>[!CAUTION]
>Com os notebooks PySpark 3 (Spark 2.4) e Scala (Spark 2.4), `%%` a magia de faísca não é mais suportada. As seguintes operações não podem mais ser utilizadas:
* `%%help`
* `%%info`
* `%%cleanup`
* `%%delete`
* `%%configure`
* `%%local`

```python
%%configure -f 
{
    "numExecutors": 10,
    "executorMemory": "8G",
    "executorCores":4,
    "driverMemory":"2G",
    "driverCores":2,
    "conf": {
        "spark.cores.max": "40"
    }
}
```

Todas as propriedades configuráveis estão listadas na tabela abaixo:

| Propriedade | Descrição | Tipo |
| :------- | :---------- | :-----:|
| gênero | O tipo de sessão (obrigatório) | `session kind`_ |
| proxyUser | O usuário para representar que executará esta sessão (por exemplo bob) | string |
| jars | Arquivos a serem colocados no java `classpath` | lista de caminhos |
| pyFiles | Os arquivos a serem colocados no `PYTHONPATH` | lista de caminhos |
| arquivos | Arquivos a serem colocados no diretório de trabalho do executor | lista de caminhos |
| driverMemory | Memória para driver em megabytes ou gigabytes (por exemplo, 1000M, 2G) | string |
| driverCores | Número de núcleos usados pelo driver (somente no modo YARN) | int |
| executeMemory | Memória para executor em megabytes ou gigabytes (por exemplo, 1000M, 2G) | string |
| executorCores | Número de núcleos usados pelo executor | int |
| numExecutors | Número de executores (apenas no modo YARN) | int |
| arquivos | Arquivos a serem descompactados no diretório de trabalho do executor (somente no modo YARN) | lista de caminhos |
| fila | A fila YARN para enviar também (somente no modo YARN) | string |
| name | Nome do pedido | string |
| conf | Propriedade de configuração Spark | Mapa de key=val |

### Iniciador {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

O *Launcher* personalizado fornece modelos de notebook úteis para seus kernels suportados para ajudá-lo a iniciar sua tarefa, incluindo:

| Modelo | Descrição |
| --- | --- |
| Em branco | Um arquivo de bloco de anotações vazio. |
| Início | Um notebook pré-preenchido demonstrando a exploração de dados usando dados de amostra. |
| Vendas a varejo | Um notebook pré-preenchido com a Receita <a href="https://adobe.ly/2wOgO3L" target="_blank">de vendas de</a> varejo usando dados de amostra. |
| Construtor de receita | Um modelo de notebook para a criação de uma receita no JupyterLab. Ele é pré-preenchido com código e comentário que demonstra e descreve o processo de criação da receita. Consulte o tutorial <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">do</a> notebook para obter uma apresentação detalhada. |
| Serviço de Query | Um notebook pré-preenchido demonstrando o uso do Serviço de Query diretamente no JupyterLab com workflows de amostra fornecidos que analisam dados em escala. |
| Eventos XDM | Um notebook pré-preenchido demonstrando a exploração de dados nos dados do Evento da experiência de pós-valor, com foco nos recursos comuns em toda a estrutura de dados. |
| Query XDM | Um notebook pré-preenchido demonstrando query comerciais de amostra sobre os dados do Evento Experience. |
| Agregação | Um notebook pré-preenchido demonstrando workflows de amostra para agregação de grandes quantidades de dados em blocos menores e gerenciáveis. |
| Agrupamento | Um notebook pré-preenchido demonstrando o processo completo de modelagem de aprendizado de máquina usando algoritmos de cluster. |

Alguns modelos de notebook estão limitados a determinados kernels. A disponibilidade do modelo para cada kernel está mapeada na seguinte tabela:

<table>
    <tr>
        <td></td>
        <th><strong>Em branco</strong></th>
        <th><strong>Início</strong></th>
        <th><strong>Vendas a varejo</strong></th>
        <th><strong>Construtor de receita</strong></th>
        <th><strong>Serviço de Query</strong></th>
        <th><strong>Eventos XDM</strong></th>
        <th><strong>Query XDM</strong></th>
        <th><strong>Agregação</strong></th>
        <th><strong>Agrupamento</strong></th>
    </tr>
    <tr>
        <th><strong>Python</strong></th>
        <td >sim</td>
        <td >sim</td>
        <td >sim</td>
        <td >sim</td>
        <td >sim</td>
        <td >sim</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
    </tr>
    <tr>
        <th ><strong>R</strong></th>
        <td >sim</td>
        <td >sim</td>
        <td >sim</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
    </tr>
    <tr>
        <th  ><strong>PySpark 3 (Spark 2.3 - obsoleto)</strong></th>
        <td >sim</td>
        <td >sim</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >sim</td>
        <td >sim</td>
        <td >não</td>
    </tr>
    <tr>
        <th ><strong>Spark (Spark 2.3 - obsoleto)</strong></th>
        <td >sim</td>
        <td >sim</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >sim</td>
    </tr>
      <tr>
        <th  ><strong>PySpark 3 (Spark 2.4)</strong></th>
        <td >não</td>
        <td >sim</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >sim</td>
        <td >sim</td>
        <td >não</td>
    </tr>
    <tr>
        <th ><strong>Scala</strong></th>
        <td >sim</td>
        <td >sim</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >não</td>
        <td >sim</td>
    </tr>
</table>

Para abrir um novo *Iniciador*, clique em **Arquivo > Novo Iniciador**. Como alternativa, expanda o navegador **** Arquivo na barra lateral esquerda e clique no símbolo de mais (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Acesse dados da plataforma usando notebooks

Cada kernel suportado fornece funcionalidades incorporadas que permitem ler dados da plataforma a partir de um conjunto de dados dentro de um notebook. Entretanto, o suporte para paginação de dados está limitado aos notebooks Python e R.

### Leitura de um conjunto de dados em Python/R

Os notebooks Python e R permitem paginar dados ao acessar os conjuntos de dados. O código de amostra para ler dados com e sem paginação é demonstrado abaixo.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### Leitura de um conjunto de dados em Python/R sem paginação

A execução do código a seguir lerá todo o conjunto de dados. Se a execução for bem-sucedida, os dados serão salvos como um dataframe de Pandas referenciado pela variável `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader
dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.read()
df.head()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT
DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$read() 
df
```

* `{DATASET_ID}`: A identidade exclusiva do conjunto de dados a ser acessado

#### Leitura de um conjunto de dados em Python/R com paginação

A execução do código a seguir lerá os dados do conjunto de dados especificado. A paginação é alcançada pela limitação e compensação de dados por meio das funções `limit()` e `offset()` , respectivamente. A limitação de dados refere-se ao número máximo de pontos de dados a serem lidos, enquanto a compensação se refere ao número de pontos de dados a serem ignorados antes da leitura dos dados. Se a operação de leitura for executada com êxito, os dados serão salvos como um dataframe de Pandas referenciado pela variável `df`.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.limit(100).offset(10).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$limit(100L)$offset(10L)$read() 
```

* `{DATASET_ID}`: A identidade exclusiva do conjunto de dados a ser acessado

### Leitura de um conjunto de dados em PySpark/Spark/Scala

>[!IMPORTANT]
>Com a transição do Spark 2.3 para o Spark 2.4, os kernels Spark e PySpark estão obsoletos.
>
>Os novos notebooks PySpark 3 (Spark 2.4) usam o kernel Python3. Consulte o guia sobre a conversão do [Pyspark 3 (Spark 2.3) em PySpark 3 (Spark 2.4)](../recipe-notebook-migration.md) se desejar converter o código do Spark 2.3 existente. Os novos notebooks devem seguir o exemplo [PySpark 3 (Spark 2.4)](#pyspark2.4) abaixo.
>
>Os novos notebooks Spark devem utilizar o kernel Scala. Consulte o guia sobre a conversão do [Spark 2.3 em Scala (Spark 2.4)](../recipe-notebook-migration.md) se desejar converter o código do Spark 2.3 existente. Os novos notebooks devem seguir o exemplo [Scala (Spark 2.4)](#spark2.4) abaixo.

Com um notebook ativo PySpark ou Spark aberto, expanda a guia **Data Explorer** da barra lateral esquerda e clique em **Conjuntos** de dados para visualização de uma lista de conjuntos de dados disponíveis. Clique com o botão direito do mouse na lista de conjuntos de dados que deseja acessar e clique em **Explorar dados no notebook**. As seguintes células de código são geradas:

#### PySpark (Spark 2.3 - obsoleto)

```python
# PySpark 3 (Spark 2.3 - deprecated)

pd0 = spark.read.format("com.adobe.platform.dataset").\
    option('orgId', "YOUR_IMS_ORG_ID@AdobeOrg").\
    load("{DATASET_ID}")
pd0.describe()
pd0.show(10, False)
```

#### PySpark (Spark 2.4) {#pyspark2.4}

Com a introdução do Spark 2.4, a magia [`%dataset`](#magic) personalizada é fornecida.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Spark (Spark 2.3 - obsoleto)

```scala
// Spark (Spark 2.3 - deprecated)

import com.adobe.platform.dataset.DataSetOptions
val dataFrame = spark.read.
    format("com.adobe.platform.dataset").
    option(DataSetOptions.orgId, "YOUR_IMS_ORG_ID@AdobeOrg").
    load("{DATASET_ID}")
dataFrame.printSchema()
dataFrame.show()
```

#### Scala (Spark 2.4) {#spark2.4}

```scala
// Scala (Spark 2.4)

// initialize the session
import org.apache.spark.sql.{Dataset, SparkSession}
val spark = SparkSession.builder().master("local").getOrCreate()

val dataFrame = spark.read.format("com.adobe.platform.query")
    .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
    .option("ims-org", sys.env("IMS_ORG_ID"))
    .option("api-key", sys.env("PYDASDK_IMS_CLIENT_ID"))
    .option("service-token", sys.env("PYDASDK_IMS_SERVICE_TOKEN"))
    .option("mode", "batch")
    .option("dataset-id", "{DATASET_ID}")
    .load()
dataFrame.printSchema()
dataFrame.show()
```

>[!TIP]
>No Scala, é possível usar `sys.env()` para declarar e retornar um valor de dentro `option`.

### Usando a mágica de %dataset em notebooks PySpark 3 (Spark 2.4) {#magic}

Com a introdução do Spark 2.4, a magia `%dataset` personalizada é fornecida para uso nos novos notebooks PySpark 3 (Spark 2.4) (kernel Python 3).

**Uso**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Descrição**

Um comando mágico personalizado da Data Science Workspace para ler ou escrever um conjunto de dados de um notebook Python (kernel Python 3).

* **{action}**: O tipo de ação a ser executada no conjunto de dados. Duas ações estão disponíveis &quot;read&quot; ou &quot;write&quot;.
* **—datasetId {id}**: Usado para fornecer a ID do conjunto de dados para leitura ou gravação. Este é um argumento obrigatório.
* **—dataFrame {df}**: Os pandas dataframe. Este é um argumento obrigatório.
   * Quando a ação é &quot;lida&quot;, {df} é a variável na qual os resultados da operação de leitura do conjunto de dados estão disponíveis.
   * Quando a ação é &quot;write&quot;, esse dataframe {df} é gravado no conjunto de dados.
* **—modo (opcional)**: Os parâmetros permitidos são &quot;batch&quot; e &quot;interative&quot;. Por padrão, o modo é definido como &quot;interativo&quot;. Recomenda-se usar o modo &quot;lote&quot; ao ler grandes quantidades de dados.

**Exemplos**

* **Exemplo** de leitura: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **Exemplo** de gravação: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### Dados do Query usando o serviço de Query em Python

O JupyterLab on Platform permite que você use o SQL em um notebook Python para acessar dados por meio do Serviço <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">de Query da plataforma</a>Adobe Experience. O acesso aos dados pelo Serviço de Query pode ser útil para lidar com grandes conjuntos de dados devido aos seus tempos de execução superiores. Observe que a consulta de dados usando o Serviço de Query tem um limite de tempo de processamento de dez minutos.

Antes de usar o Serviço de Query no JupyterLab, certifique-se de que você tenha uma compreensão funcional da sintaxe <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">SQL do Serviço de</a>Query.

A consulta de dados usando o Serviço de Query requer que você forneça o nome do conjunto de dados do público alvo. Você pode gerar as células de código necessárias localizando o conjunto de dados desejado usando o **Data Explorer**. Clique com o botão direito do mouse na listagem do conjunto de dados e clique em Dados do **Query no Bloco de notas** para gerar as duas células de código a seguir no seu bloco de notas:


Para utilizar o serviço de Query no JupyterLab, é necessário primeiro criar uma conexão entre o notebook Python e o serviço de Query em funcionamento. Isso pode ser feito executando-se a primeira célula gerada.

```python
qs_connect()
```

Na segunda célula gerada, a primeira linha deve ser definida antes do query SQL. Por padrão, a célula gerada define uma variável opcional (`df0`) que salva os resultados do query como um dataframe de Pandas. <br>O `-c QS_CONNECTION` argumento é obrigatório e instrui o kernel a executar o query SQL em relação ao Query Service. Consulte o [apêndice](#optional-sql-flags-for-query-service) para obter uma lista de argumentos adicionais.

```python
%%read_sql df0 -c QS_CONNECTION
SELECT *
FROM name_of_the_dataset
LIMIT 10
/* Querying table "name_of_the_dataset" (datasetId: {DATASET_ID})*/
```

As variáveis Python podem ser referenciadas diretamente em um query SQL usando uma sintaxe formatada em sequência e vinculando as variáveis entre chaves (`{}`), como mostra o exemplo a seguir:

```python
table_name = 'name_of_the_dataset'
table_columns = ','.join(['col_1','col_2','col_3'])
```

```python
%%read_sql demo -c QS_CONNECTION
SELECT {table_columns}
FROM {table_name}
```

### Filtrar dados de ExperienceEvent em Python/R

Para acessar e filtrar um conjunto de dados ExperienceEvent em um notebook Python ou R, é necessário fornecer a ID do conjunto de dados (`{DATASET_ID}`) juntamente com as regras de filtro que definem um intervalo de tempo específico usando operadores lógicos. Quando um intervalo de tempo é definido, qualquer paginação especificada é ignorada e todo o conjunto de dados é considerado.

Uma lista de operadores de filtragem está descrita abaixo:

* `eq()`: Equal to
* `gt()`: Greater than
* `ge()`: Greater than or equal to
* `lt()`: Less than
* `le()`: Less than or equal to
* `And()`: Operador AND lógico
* `Or()`: Operador OR lógico

As células a seguir filtram um conjunto de dados ExperienceEvent para dados existentes exclusivamente entre 1º de janeiro de 2019 e o final de 31 de dezembro de 2019.

```python
# Python

client_context = PLATFORM_SDK_CLIENT_CONTEXT
from platform_sdk.dataset_reader import DatasetReader

dataset_reader = DatasetReader(client_context, "{DATASET_ID}")
df = dataset_reader.\
    where(dataset_reader["timestamp"].gt("2019-01-01 00:00:00").\
    And(dataset_reader["timestamp"].lt("2019-12-31 23:59:59"))\
).read()
```

```R
# R

library(reticulate)
use_python("/usr/local/bin/ipython")
psdk <- import("platform_sdk")
py_run_file("../.ipython/profile_default/startup/platform_sdk_context.py")
client_context <- py$PLATFORM_SDK_CLIENT_CONTEXT

DatasetReader <- psdk$dataset_reader$DatasetReader
dataset_reader <- DatasetReader(client_context, "{DATASET_ID}") 
df <- dataset_reader$
    where(dataset_reader["timestamp"]$gt("2019-01-01 00:00:00")$
    And(dataset_reader["timestamp"]$lt("2019-12-31 23:59:59"))
)$read()
```

### Filtrar dados do ExperienceEvent no PySpark/Spark

>[!IMPORTANT]
>Com a transição do Spark 2.3 para o Spark 2.4, os kernels Spark e PySpark estão obsoletos.
>
>Os novos notebooks PySpark 3 (Spark 2.4) usam o kernel Python3. Consulte o guia sobre a conversão do [Pyspark 3 (Spark 2.3) em PySpark 3 (Spark 2.4)](../recipe-notebook-migration.md) para obter mais informações sobre a conversão do código existente. Se você estiver criando um novo notebook PySpark, use o [exemplo PySpark 3 (spark 2.4)](#pyspark3-spark2.4) para filtrar os dados do ExperienceEvent.
>
>Os novos notebooks Spark devem utilizar o kernel Scala. Consulte o guia sobre a conversão do [Spark 2.3 em Scala (Spark 2.4)](../recipe-notebook-migration.md) para obter mais informações sobre a conversão do código existente. Se você estiver criando um novo notebook Spark, use o [exemplo Scala (spark 2.4)](#scala-spark) para filtrar os dados do ExperienceEvent.

Acessar e filtrar um conjunto de dados ExperienceEvent em um notebook PySpark ou Spark requer que você forneça a identidade do conjunto de dados (`{DATASET_ID}`), a identidade IMS de sua organização e as regras de filtro que definem um intervalo de tempo específico. Um intervalo de tempo de Filtragem é definido usando a função `spark.sql()`, onde o parâmetro da função é uma string de query SQL.

As células a seguir filtram um conjunto de dados ExperienceEvent para dados existentes exclusivamente entre 1º de janeiro de 2019 e o final de 31 de dezembro de 2019.

#### PySpark 3 (Spark 2.3 - obsoleto)

```python
# PySpark 3 (Spark 2.3 - deprecated)

pd = spark.read.format("com.adobe.platform.dataset").\
    option("orgId", "YOUR_IMS_ORG_ID@AdobeOrg").\
    load("{DATASET_ID}")

pd.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
```

#### PySpark 3 (Spark 2.4) {#pyspark3-spark2.4}

```python
# PySpark 3 (Spark 2.4)

from pyspark.sql import SparkSession
spark = SparkSession.builder.getOrCreate()

%dataset read --datasetId {DATASET_ID} --dataFrame df

df.createOrReplaceTempView("event")
timepd = spark.sql("""
    SELECT *
    FROM event
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timepd.show()
```

#### Spark (Spark 2.3 - obsoleto)

```scala
// Spark (Spark 2.3 - deprecated)

import com.adobe.platform.dataset.DataSetOptions
val dataFrame = spark.read.
    format("com.adobe.platform.dataset").
    option(DataSetOptions.orgId, "YOUR_IMS_ORG_ID@AdobeOrg").
    load("{DATASET_ID}")

dataFrame.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
```

#### Scala (Spark 2.4) {#scala-spark}

```scala
// Spark (Spark 2.4)

// Turn off extra logging
import org.apache.log4j.{Level, Logger}
Logger.getLogger("org").setLevel(Level.OFF)
Logger.getLogger("com").setLevel(Level.OFF)

import org.apache.spark.sql.{Dataset, SparkSession}
val spark = org.apache.spark.sql.SparkSession.builder().appName("Notebook")
  .master("local")
  .getOrCreate()

// Stage Exploratory
val dataSetId: String = "{DATASET_ID}"
val orgId: String = sys.env("IMS_ORG_ID")
val clientId: String = sys.env("PYDASDK_IMS_CLIENT_ID")
val userToken: String = sys.env("PYDASDK_IMS_USER_TOKEN")
val serviceToken: String = sys.env("PYDASDK_IMS_SERVICE_TOKEN")
val mode: String = "batch"

var df = spark.read.format("com.adobe.platform.query")
  .option("user-token", userToken)
  .option("ims-org", orgId)
  .option("api-key", clientId)
  .option("mode", mode)
  .option("dataset-id", dataSetId)
  .option("service-token", serviceToken)
  .load()
df.createOrReplaceTempView("event")
val timedf = spark.sql("""
    SELECT * 
    FROM event 
    WHERE timestamp > CAST('2019-01-01 00:00:00.0' AS TIMESTAMP)
    AND timestamp < CAST('2019-12-31 23:59:59.9' AS TIMESTAMP)
""")
timedf.show()
```

>[!TIP]
>No Scala, é possível usar `sys.env()` para declarar e retornar um valor de dentro `option`. Isso elimina a necessidade de definir variáveis se você sabe que elas só serão usadas uma única vez. O exemplo a seguir retira `val userToken` do exemplo acima e o declara em linha dentro `option` como uma alternativa:
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

## Bibliotecas compatíveis {#supported-libraries}

### Python / R

| Biblioteca | Versão |
| :------ | :------ |
| notebook | 6.0.0 |
| solicitações | 2.22.0 |
| total | 4.0.0 |
| fólio | 0.10.0 |
| ipywidgets | 7.5.1 |
| bokeh | 1.3.1 |
| genismo | 3.7.3 |
| ipyparalelo | 0.5.2 |
| jq | 1.6 |
| keras | 2.2.4 |
| nltk | 3.2.5 |
| pandas | 0.22.0 |
| pandasql | 0.7.3 |
| travesseiro | 6.0.0 |
| scikit-image | 0.15.0 |
| scikit-learn | 0.21.3 |
| cifra | 1.3.0 |
| sutura | 1.3.0 |
| seaborna | 0.9.0 |
| stats models | 0.10.1 |
| elástico | 5.1.0.17 |
| conspiração | 0.11.5 |
| py-xgover | 0.90 |
| opencv | 3.4.1 |
| parque | 2.4.3 |
| pirâmide | 1.0.1 |
| wxpython | 4.0.6 |
| colorida | 0.3.0 |
| geopandas | 0.5.1 |
| piranha | 2.1.0 |
| forma | 1.6.4 |
| rpy2 | 2.9.4 |
| essenciais | 3.6 |
| r-arules | 1.6_3 |
| r-fpc | 2.2_3 |
| r-e1071 | 1.7_2 |
| r-gam | 1.16.1 |
| r-gbm | 2.1.5 |
| r-ggems | 4.2.0 |
| r-ggvis | 0.4.4 |
| r-igraph | 1.2.4.1 |
| saltos de r | 3.0 |
| manipular novamente | 1.0.1 |
| r-rocr | 1.0_7 |
| r-rmysql | 0.10.17 |
| r-rodbc | 1.3_15 |
| r-rsqlite | 2.1.2 |
| r-rstan | 2.19.2 |
| r-sqldf | 0.4_11 |
| sobrevivência | 2.44_1.1 |
| r-zoo | 1.8_6 |
| r-stringdist | 0.9.5.2 |
| r-quadprog | 1.5_7 |
| r-rjson | 0.2.20 |
| re-previsão | 8.7 |
| r-rsolnp | 1.16 |
| r-reticulado | 1.12 |
| r-mlr | 2.14.0 |
| r-viridis | 0.5.1 |
| rondagem | 0.84 |
| r-fnn | 1.1.3 |
| r-lubridate | 1.7.4 |
| r-randomforest | 4.6_14 |
| r-tidyverse | 1.2.1 |
| r-tree | 1.0_39 |
| pímono | 3.8.0 |
| pifleta | 0.14.1 |
| boto3 | 1.9.199 |
| ipyvolume | 0.5.2 |
| fast parquet | 0.3.2 |
| piritão | 0.5.4 |
| ipywebrtc | 0.5.0 |
| jupyter_client | 5.3.1 |
| wordcloud | 1.5.0 |
| grafite | 2.40.1 |
| piton-grafviz | 0.11.1 |
| azure-armazenamento | 0.36.0 |
| jupyterlab | 1.0.4 |
| pandas_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| zombaria | 3.0.5 |
| pílula | 0.3.3 |
| fonts-anacond | 1.0 |
| psycopg2 | 2.8.3 |
| nariz | 1.3.7 |
| autovizwidget | 0.12.9 |
| altair | 3.1.0 |
| vega_datasets | 0.7.0 |
| papelaria | 1.0.1 |
| sql_mágica | 0.0.4 |
| iso3166 | 1.0 |
| nbimportador | 0.3.1 |

### PySpark

| Biblioteca | Versão |
| :------ | :------ |
| solicitações | 2.18.4 |
| genismo | 2.3.0 |
| keras | 2.0.6 |
| nltk | 3.2.4 |
| pandas | 0.20.1 |
| pandasql | 0.7.3 |
| travesseiro | 5.3.0 |
| scikit-image | 0.13.0 |
| scikit-learn | 0.19.0 |
| cifra | 0.19.1 |
| sutura | 1.3.3 |
| stats models | 0.8.0 |
| elástico | 4.0.30.44 |
| py-xgover | 0.60 |
| opencv | 3.1.0 |
| pifleta | 0.8.0 |
| boto3 | 1.5.18 |
| azure-armazenamento-blob | 1.4.0 |
| pitão | 3.6.7 |
| mkl-rt | 11.1 |

## Sinalizadores SQL opcionais para o Serviço de Query {#optional-sql-flags-for-query-service}

Esta tabela descreve os sinalizadores SQL opcionais que podem ser usados para o Serviço de Query.

| **Sinalizador** | **Descrição** |
| --- | --- |
| `-h`, `--help` | Mostre a mensagem de ajuda e saia. |
| `-n`, `--notify` | Alternar opção para notificar os resultados do query. |
| `-a`, `--async` | O uso desse sinalizador executa o query de forma assíncrona e pode liberar o kernel enquanto o query está sendo executado. Tenha cuidado ao atribuir resultados de query a variáveis, pois eles podem ser indefinidos se o query não estiver concluído. |
| `-d`, `--display` | O uso desse sinalizador impede que os resultados sejam exibidos. |

