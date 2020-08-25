---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics;jupyterlab
solution: Experience Platform
title: Guia do usuário do JupyterLab
topic: Overview
description: O JupyterLab é uma interface de usuário baseada na Web para o Project Júpitter e está totalmente integrado ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para que os cientistas de dados trabalhem com notebooks, códigos e dados de Júpiter.
translation-type: tm+mt
source-git-commit: 38cb8eeae3ac0a1852c59e433d1cacae82b1c6c0
workflow-type: tm+mt
source-wordcount: '3684'
ht-degree: 11%

---


# [!DNL JupyterLab] guia do usuário

[!DNL JupyterLab] é uma interface de usuário baseada na Web para o [Project Júpiter](https://jupyter.org/) e está totalmente integrada ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para que os cientistas de dados trabalhem com notebooks, códigos e dados de Júpiter.

Este documento fornece uma visão geral de [!DNL JupyterLab] e seus recursos, bem como instruções para executar ações comuns.

## [!DNL JupyterLab] em [!DNL Experience Platform]

A integração com o JByterLab é acompanhada de mudanças arquitetônicas, considerações de design, extensões de notebook personalizadas, bibliotecas pré-instaladas e um tema de Adobe.

A lista a seguir descreve alguns dos recursos exclusivos do JupyterLab na plataforma:

| Recurso | Descrição |
| --- | --- |
| **Kernels** | Os kernels fornecem o notebook e outros [!DNL JupyterLab] front-ends com a capacidade de executar e inserir código em diferentes linguagens de programação. [!DNL Experience Platform] fornece kernels adicionais para suportar o desenvolvimento em [!DNL Python]R, PySpark e [!DNL Spark]. Consulte a seção [kernels](#kernels) para obter mais detalhes. |
| **Acesso aos dados** | Acesse conjuntos de dados existentes diretamente de dentro [!DNL JupyterLab] com suporte total para recursos de leitura e gravação. |
| **[!DNL Platform]integração de serviços** | As integrações incorporadas permitem que você utilize outros [!DNL Platform] serviços diretamente de dentro [!DNL JupyterLab]. Uma lista completa de integrações compatíveis é fornecida na seção [Integração com outros serviços](#service-integration)da plataforma. |
| **Autenticação** | Além do modelo <a href="https://jupyter-notebook.readthedocs.io/en/latest/security.html" target="_blank">de segurança integrado do</a>JupyterLab, todas as interações entre seu aplicativo e o Experience Platform, incluindo a comunicação serviço a serviço da plataforma, são criptografadas e autenticadas pelo <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliotecas de desenvolvimento** | No [!DNL Experience Platform], [!DNL JupyterLab] fornece bibliotecas pré-instaladas para [!DNL Python], R e PySpark. Consulte o [apêndice](#supported-libraries) para obter uma lista completa das bibliotecas suportadas. |
| **Controladora de biblioteca** | Quando as bibliotecas pré-instaladas não atendem às suas necessidades, bibliotecas adicionais podem ser instaladas para Python e R, e são temporariamente armazenadas em container isolados para manter a integridade dos dados [!DNL Platform] e mantê-los seguros. Consulte a seção [kernels](#kernels) para obter mais detalhes. |

>[!NOTE]
>
>As bibliotecas adicionais só estão disponíveis para a sessão em que foram instaladas. É necessário reinstalar as bibliotecas adicionais necessárias ao iniciar novas sessões.

## Integração com outros [!DNL Platform] serviços {#service-integration}

A normalização e a interoperabilidade são conceitos fundamentais subjacentes [!DNL Experience Platform]. A integração do [!DNL JupyterLab] on como um IDE incorporado permite que ele interaja com outros [!DNL Platform] serviços, permitindo que você utilize todo o seu potencial [!DNL Platform] [!DNL Platform] . Os seguintes [!DNL Platform] serviços estão disponíveis em [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Acesse e explore conjuntos de dados com funcionalidades de leitura e gravação.
* **[!DNL Query Service]:** Acesse e explore conjuntos de dados usando SQL, fornecendo custos indiretos de acesso a dados mais baixos ao lidar com grandes quantidades de dados.
* **[!DNL Sensei ML Framework]:** Desenvolvimento de modelo com a capacidade de treinar e pontuar dados, bem como criação de receita com um único clique.
* **[!DNL Experience Data Model (XDM)]:** A normalização e a interoperabilidade são conceitos-chave por trás da Adobe Experience Platform. [O Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en), orientado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

>[!NOTE]
>
>Algumas integrações [!DNL Platform] de serviço em [!DNL JupyterLab] estão limitadas a kernels específicos. Consulte a seção sobre [kernels](#kernels) para obter mais detalhes.

## Principais recursos e operações comuns

As informações sobre os principais recursos [!DNL JupyterLab] e instruções para a realização de operações comuns são fornecidas nas seções abaixo:

* [Access JupyterLab](#access-jupyterlab)
* [Interface JupyterLab](#jupyterlab-interface)
* [Células de código](#code-cells)
* [Kernels](#kernels)
* [Sessões do kernel](#kernel-sessions)
* [Recurso de execução PySpark/Spark](#execution-resource)
* [Iniciador](#launcher)

### Acesso [!DNL JupyterLab] {#access-jupyterlab}

No [Adobe Experience Platform](https://platform.adobe.com), selecione **Notebooks** na coluna de navegação esquerda. Aguarde algum tempo para [!DNL JupyterLab] a inicialização completa.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interface {#jupyterlab-interface}

A [!DNL JupyterLab] interface consiste em uma barra de menus, uma barra lateral esquerda flexível e a área de trabalho principal contendo guias de documentos e atividades.

**Barra de menus**

A barra de menus na parte superior da interface tem menus de nível superior que exibem ações disponíveis em [!DNL JupyterLab] seus atalhos de teclado:

* **Arquivo:** Ações relacionadas a arquivos e diretórios
* **Editar:** Ações relacionadas à edição de documentos e outras atividades
* **Visualização:** Ações que alteram a aparência de [!DNL JupyterLab]
* **Executar:** Ações para executar código em diferentes atividades, como notebooks e consoles de código
* **Kernel:** Ações para gerenciar kernels
* **Guias:** Uma lista de documentos e atividades abertos
* **Configurações:** Configurações comuns e um editor de configurações avançado
* **Ajuda:** Uma lista dos links de ajuda do kernel [!DNL JupyterLab] e do kernel

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

A área de trabalho principal em [!DNL JupyterLab] permite organizar documentos e outras atividades em painéis de guias que podem ser redimensionados ou subdivididos. Arraste uma guia até o centro de um painel de guias para migrar a guia. Divida um painel arrastando uma guia para a esquerda, direita, superior ou inferior do painel:

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

Os kernels notebook são os mecanismos de computação específicos da linguagem para processar células de notebook. Além de [!DNL Python], [!DNL JupyterLab] oferece suporte adicional a idiomas em R, PySpark e [!DNL Spark] (Scala). Quando você abre um documento notebook, o kernel associado é iniciado. Quando uma célula do notebook é executada, o kernel executa o cálculo e produz resultados que podem consumir recursos significativos da CPU e da memória. Observe que a memória alocada não é liberada até que o kernel seja desligado.

Determinados recursos e funcionalidades estão limitados a kernels específicos, conforme descrito no quadro abaixo:

| Kernel | Suporte à instalação da biblioteca | [!DNL Platform] integrações |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sim | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sim | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Não | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sessões do kernel {#kernel-sessions}

Cada notebook ativo ou atividade ativa em [!DNL JupyterLab] utiliza uma sessão de kernel. Todas as sessões ativas podem ser encontradas ao expandir a guia Terminais **em execução e kernels** na barra lateral esquerda. O tipo e o estado do kernel de um notebook podem ser identificados observando a parte superior direita da interface do notebook. No diagrama abaixo, o kernel associado ao notebook é **[!DNL Python]3** e seu estado atual é representado por um círculo cinza à direita. Um círculo oco implica um kernel ocioso e um círculo sólido implica um kernel ocupado.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Se o kernel estiver desligado ou inativo por um período prolongado, então **Nenhum kernel!** com um círculo sólido é mostrado. Ative um kernel clicando no status do kernel e selecionando o tipo de kernel apropriado, conforme demonstrado abaixo:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Iniciador {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

O *Launcher* personalizado fornece modelos de notebook úteis para seus kernels suportados para ajudá-lo a iniciar sua tarefa, incluindo:

| Modelo | Descrição |
| --- | --- |
| Em branco | Um arquivo de bloco de anotações vazio. |
| Início | Um notebook pré-preenchido demonstrando a exploração de dados usando dados de amostra. |
| Vendas a varejo | Um notebook pré-preenchido com a Receita <a href="https://adobe.ly/2wOgO3L" target="_blank">de vendas de</a> varejo usando dados de amostra. |
| Construtor de receita | Um modelo de bloco de anotações para criar uma receita em [!DNL JupyterLab]. Ele é pré-preenchido com código e comentário que demonstra e descreve o processo de criação da receita. Consulte o tutorial <a href="https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en" target="_blank">do</a> notebook para obter uma apresentação detalhada. |
| [!DNL Query Service] | Um notebook pré-preenchido demonstrando o uso de [!DNL Query Service] diretamente em [!DNL JupyterLab] workflows de amostra fornecidos que analisam dados em escala. |
| Eventos XDM | Um notebook pré-preenchido demonstrando a exploração de dados nos dados do Evento da experiência de pós-valor, com foco nos recursos comuns em toda a estrutura de dados. |
| Query XDM | Um notebook pré-preenchido demonstrando query comerciais de amostra sobre os dados do Evento Experience. |
| Agregação | Um notebook pré-preenchido demonstrando workflows de amostra para agregação de grandes quantidades de dados em blocos menores e gerenciáveis. |
| Geração de cluster | Um notebook pré-preenchido demonstrando o processo completo de modelagem de aprendizado de máquina usando algoritmos de cluster. |

Alguns modelos de notebook estão limitados a determinados kernels. A disponibilidade do modelo para cada kernel está mapeada na seguinte tabela:

<table>
    <tr>
        <td></td>
        <th><strong>Em branco</strong></th>
        <th><strong>Início</strong></th>
        <th><strong>Vendas a varejo</strong></th>
        <th><strong>Construtor de receita</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>Eventos XDM</strong></th>
        <th><strong>Query XDM</strong></th>
        <th><strong>Agregação</strong></th>
        <th><strong>Geração de cluster</strong></th>
    </tr>
    <tr>
        <th><strong>[!DNL Python]</strong></th>
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
        <th  ><strong>PySpark 3 ([!DNL Spark] 2.4)</strong></th>
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

### Configuração de GPU e servidor de memória em [!DNL Python]/R

No canto superior direito, [!DNL JupyterLab] selecione o ícone de engrenagem para abrir a configuração *do servidor* Notebook. Você pode ativar a GPU e alocar a quantidade de memória necessária usando o controle deslizante. A quantidade de memória que você pode alocar depende de quanto a sua organização provisionou. Selecione **[!UICONTROL Atualizar configurações]** para salvar.

>[!NOTE]
>Somente uma GPU é provisionada por organização para notebooks. Se a GPU estiver em uso, é necessário aguardar o usuário que reservou a GPU para liberá-la. Isso pode ser feito fazendo logout ou deixando a GPU em estado ocioso por quatro ou mais horas.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

## Acessar [!DNL Platform] dados usando notebooks

Cada kernel suportado fornece funcionalidades incorporadas que permitem ler [!DNL Platform] dados de um conjunto de dados dentro de um notebook. No entanto, o suporte para paginação de dados é limitado a notebooks [!DNL Python] e R.

### Limites de dados do notebook

As informações a seguir definem a quantidade máxima de dados que podem ser lidos, que tipo de dados foram usados e o período estimado de leitura dos dados. Para [!DNL Python] e R, um servidor notebook configurado com 40 GB de RAM foi usado para os benchmarks. Para PySpark e Scala, um cluster de databricks configurado com 64 GB de RAM, 8 núcleos, 2 DBU com um máximo de 4 trabalhadores foi usado para os benchmarks descritos abaixo.

Os dados do schema ExperienceEvent usados variaram de tamanho, começando em mil (1K) linhas que variam de até um bilhão (1B) de linhas. Observe que para as [!DNL Spark] métricas e PySpark, um período de 10 dias foi usado para os dados XDM.

Os dados do schema ad-hoc foram pré-processados usando [!DNL Query Service] Criar Tabela como Selecionar (CTAS). Esses dados também variaram de tamanho a partir de mil linhas (1.000) de até 1 bilhão (1.000 linhas).

#### [!DNL Python] limites de dados do notebook

**Schema XDM ExperienceEvent:** Você deve ser capaz de ler no máximo 2 milhões de linhas (~6,1 GB de dados em disco) de dados XDM em menos de 22 minutos. A adição de linhas adicionais pode resultar em erros.

| Número de linhas | 1K | 10K | 100K | 1M | 2M |
| ----------------------- | ------ | ------ | ----- | ----- | ----- |
| Tamanho no disco (MB) | 18.73 | 187.5 | 308 | 3000 | 6050 |
| SDK (em segundos) | 20.3 | 86.8 | 63 | 659 | 1315 |

**schema ad-hoc:** Você deve ser capaz de ler no máximo 5 milhões de linhas (~5,6 GB de dados em disco) de dados não-XDM (ad-hoc) em menos de 14 minutos. A adição de linhas adicionais pode resultar em erros.

| Número de linhas | 1K | 10K | 100K | 1M | 2M | 3M | 5M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- | ------ |
| Tamanho no disco (em MB) | 1.21 | 11.72 | 115 | 1120 | 2250 | 3380 | 5630 |
| SDK (em segundos) | 7.27 | 9.04 | 27.3 | 180 | 346 | 487 | 819 |

#### Limites de dados do notebook R

**Schema XDM ExperienceEvent:** Você deve ser capaz de ler no máximo 1 milhão de linhas de dados XDM (dados de 3 GB no disco) em menos de 13 minutos.

| Número de linhas | 1K | 10K | 100K | 1M |
| ----------------------- | ------ | ------ | ----- | ----- |
| Tamanho no disco (MB) | 18.73 | 187.5 | 308 | 3000 |
| R Kernel (em segundos) | 14.03 | 69.6 | 86.8 | 775 |

**schema ad-hoc:** Você deve ser capaz de ler no máximo 3 milhões de linhas de dados ad hoc (dados de 293 MB em disco) em aproximadamente 10 minutos.

| Número de linhas | 1K | 10K | 100K | 1M | 2M | 3M |
| ----------------------- | ------- | ------- | ----- | ----- | ----- | ----- |
| Tamanho no disco (em MB) | 0.082 | 0.612 | 9.0 | 91 | 188 | 293 |
| SDK R (em segundos) | 7.7 | 4.58 | 35.9 | 233 | 470.5 | 603 |

#### Limites de dados do notebook PySpark (kernel[!DNL Python] ):

**Schema XDM ExperienceEvent:** No modo Interativo, você deve ser capaz de ler no máximo 5 milhões de linhas (~13,42 GB de dados no disco) de dados XDM em cerca de 20 minutos. O modo interativo suporta apenas até 5 milhões de linhas. Se desejar ler conjuntos de dados maiores, sugerimos que você alterne para o modo Lote. No modo Lote, você deve ser capaz de ler um máximo de 500 milhões de linhas (~1,31 TB de dados no disco) de dados XDM em cerca de 14 horas.

| Número de linhas | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|-------------------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamanho no disco | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| SDK (modo interativo) | 33s | 32.4s | 55.1s | 253.5s | 489.2s | 729.6s | 1206.8s | - | - | - | - |
| SDK (Modo de lote) | 815.8s | 492.8s | 379.1s | 637.4s | 624.5s | 869.2s | 1104.1s | 1786s | 5387.2s | 10624.6s | 50547s |

**schema ad-hoc:** No modo Interativo, você deve ser capaz de ler no máximo 1 bilhão de linhas (~1,05 TB de dados no disco) de dados não XDM em menos de 3 minutos. No modo Lote, você deve ser capaz de ler no máximo 1 bilhão de linhas (~1,05 TB de dados no disco) de dados não XDM em cerca de 18 minutos.

| Número de linhas | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|--------|--------|---------|--------|---------|-------|
| Tamanho no disco | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| Modo interativo do SDK (em segundos) | 28.2s | 18.6s | 20.8s | 20.9s | 23.8s | 21.7s | 24.7s | 22s | 28.4s | 40s | 97.4s | 154.5s |
| Modo de lote do SDK (em segundos) | 428.8s | 578.8s | 641.4s | 538.5s | 630.9s | 467.3s | 411s | 675s | 702s | 719.2s | 1022.1s | 1122.3s |

#### [!DNL Spark] Limites de dados do notebook (kernel Scala):

**Schema XDM ExperienceEvent:** No modo Interativo, você deve ser capaz de ler no máximo 5 milhões de linhas (~13,42 GB de dados no disco) de dados XDM em cerca de 18 minutos. O modo interativo suporta apenas até 5 milhões de linhas. Se desejar ler conjuntos de dados maiores, sugerimos que você alterne para o modo Lote. No modo Lote, você deve ser capaz de ler um máximo de 500 milhões de linhas (~1,31 TB de dados no disco) de dados XDM em cerca de 14 horas.

| Número de linhas | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M |
|---------------|--------|--------|-------|-------|-------|-------|---------|---------|----------|--------|--------|
| Tamanho no disco | 2.93MB | 4.38MB | 29.02 | 2.69GB | 5.39GB | 8.09GB | 13.42GB | 26.82GB | 134.24GB | 268.39GB | 1.31TB |
| Modo interativo do SDK (em segundos) | 37.9s | 22.7s | 45.6s | 231.7s | 444.7s | 660.6s | 1100s | - | - | - | - |
| Modo de lote do SDK (em segundos) | 374.4s | 398.5s | 527s | 487.9s | 588.9s | 829s | 939.1s | 1441s | 5473.2s | 10118.8 | 49207.6 |

**schema ad-hoc:** No modo Interativo, você deve ser capaz de ler no máximo 1 bilhão de linhas (~1,05 TB de dados no disco) de dados não XDM em menos de 3 minutos. No modo Lote, você deve ser capaz de ler no máximo 1 bilhão de linhas (~1,05 TB de dados no disco) de dados não XDM em cerca de 16 minutos.

| Número de linhas | 1K | 10K | 100K | 1M | 2M | 3M | 5M | 10M | 50M | 100M | 500M | 1B |
|--------------|--------|---------|---------|-------|-------|-------|---------|---------|---------|--------|---------|-------|
| Tamanho no disco | 1.12MB | 11.24MB | 109.48MB | 2.69GB | 2.14GB | 3.21GB | 5.36GB | 10.71GB | 53.58GB | 107.52GB | 535.88GB | 1.05TB |
| Modo interativo do SDK (em segundos) | 35.7s | 31s | 19.5s | 25.3s | 23s | 33.2s | 25.5s | 29.2s | 29.7s | 36.9s | 83.5s | 139s |
| Modo de lote do SDK (em segundos) | 448.8s | 459.7s | 519s | 475.8s | 599.9s | 347.6s | 407.8s | 397s | 518.8s | 487.9s | 760.2s | 975.4s |

### Ler de um conjunto de dados em [!DNL Python]/R

[!DNL Python] e os notebooks R permitem paginar dados ao acessar os conjuntos de dados. O código de amostra para ler dados com e sem paginação é demonstrado abaixo.

[//]: # (In the following samples, the first step is currently required but once the SDK is complete, users are no longer required to explicitly define client_context)

#### Leitura de um conjunto de dados em [!DNL Python]/R sem paginação

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

#### Leitura de um conjunto de dados em [!DNL Python]/R com paginação

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

### Leitura de um conjunto de dados no PySpark/[!DNL Spark]/Scala

Com um notebook PySpark ou Scala ativo aberto, expanda a guia **Data Explorer** da barra lateral esquerda e clique em **Conjuntos** de dados para visualização de uma lista de conjuntos de dados disponíveis. Clique com o botão direito do mouse na lista de conjuntos de dados que deseja acessar e clique em **Explorar dados no notebook**. As seguintes células de código são geradas:

#### PySpark ([!DNL Spark] 2.4) {#pyspark2.4}

Com a introdução do Spark 2.4, a magia [`%dataset`](#magic) personalizada é fornecida.

```python
# PySpark 3 (Spark 2.4)

%dataset read --datasetId {DATASET_ID} --dataFrame pd0
pd0.describe()
pd0.show(10, False)
```

#### Scala ([!DNL Spark] 2.4) {#spark2.4}

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

### Usando mágica de %dataset em notebooks PySpark 3 ([!DNL Spark] 2.4) {#magic}

Com a introdução do [!DNL Spark] 2.4, a magia `%dataset` personalizada é fornecida para uso nos novos notebooks PySpark 3 ([!DNL Spark] 2.4) ([!DNL Python] 3 kernel).

**Uso**

`%dataset {action} --datasetId {id} --dataFrame {df}`

**Descrição**

Um comando mágico personalizado [!DNL Data Science Workspace] para ler ou escrever um conjunto de dados a partir de um [!DNL Python] notebook ([!DNL Python] 3 kernel).

* **{action}**: O tipo de ação a ser executada no conjunto de dados. Duas ações estão disponíveis &quot;read&quot; ou &quot;write&quot;.
* **—datasetId {id}**: Usado para fornecer a ID do conjunto de dados para leitura ou gravação. Este é um argumento obrigatório.
* **—dataFrame {df}**: Os pandas dataframe. Este é um argumento obrigatório.
   * Quando a ação é &quot;lida&quot;, {df} é a variável na qual os resultados da operação de leitura do conjunto de dados estão disponíveis.
   * Quando a ação é &quot;write&quot;, esse dataframe {df} é gravado no conjunto de dados.
* **—modo (opcional)**: Os parâmetros permitidos são &quot;batch&quot; e &quot;interative&quot;. Por padrão, o modo é definido como &quot;interativo&quot;. Recomenda-se usar o modo &quot;lote&quot; ao ler grandes quantidades de dados.

**Exemplos**

* **Exemplo** de leitura: `%dataset read --datasetId 5e68141134492718af974841 --dataFrame pd0`
* **Exemplo** de gravação: `%dataset write --datasetId 5e68141134492718af974842 --dataFrame pd0`

### dados do query usando [!DNL Query Service] em [!DNL Python]

[!DNL JupyterLab] on [!DNL Platform] permite que você use o SQL em um [!DNL Python] notebook para acessar dados pelo <a href="https://www.adobe.com/go/query-service-home-en" target="_blank">Adobe Experience Platform Query Service</a>. O acesso aos dados por meio [!DNL Query Service] pode ser útil para lidar com grandes conjuntos de dados devido aos tempos de execução superiores. Observe que consultar dados usando [!DNL Query Service] tem um limite de tempo de processamento de dez minutos.

Antes de usar [!DNL Query Service] em [!DNL JupyterLab], certifique-se de que você tenha uma compreensão funcional da sintaxe <a href="https://www.adobe.com/go/query-service-sql-syntax-en" target="_blank">[!DNL Query Service] do</a>SQL.

A consulta de dados usando [!DNL Query Service] requer que você forneça o nome do conjunto de dados do público alvo. Você pode gerar as células de código necessárias localizando o conjunto de dados desejado usando o **Data Explorer**. Clique com o botão direito do mouse na listagem do conjunto de dados e clique em Dados do **Query no Bloco de notas** para gerar as duas células de código a seguir no seu bloco de notas:


Para poder utilizar [!DNL Query Service] o [!DNL JupyterLab], é necessário primeiro criar uma conexão entre o seu [!DNL Python] notebook de trabalho e o [!DNL Query Service]. Isso pode ser feito executando-se a primeira célula gerada.

```python
qs_connect()
```

Na segunda célula gerada, a primeira linha deve ser definida antes do query SQL. Por padrão, a célula gerada define uma variável opcional (`df0`) que salva os resultados do query como um dataframe de Pandas. <br>O `-c QS_CONNECTION` argumento é obrigatório e instrui o kernel a executar o query SQL contra [!DNL Query Service]. Consulte o [apêndice](#optional-sql-flags-for-query-service) para obter uma lista de argumentos adicionais.

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

### Filtrar dados de ExperienceEvent em [!DNL Python]/R

Para acessar e filtrar um conjunto de dados ExperienceEvent em um bloco de anotações [!DNL Python] ou R, é necessário fornecer a ID do conjunto de dados (`{DATASET_ID}`) juntamente com as regras de filtro que definem um intervalo de tempo específico usando operadores lógicos. Quando um intervalo de tempo é definido, qualquer paginação especificada é ignorada e todo o conjunto de dados é considerado.

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

### Filtrar dados do ExperienceEvent no PySpark/[!DNL Spark]

Acessar e filtrar um conjunto de dados ExperienceEvent em um notebook PySpark ou Scala requer que você forneça a identidade do conjunto de dados (`{DATASET_ID}`), a identidade IMS de sua organização e as regras de filtro que definem um intervalo de tempo específico. Um intervalo de tempo de Filtragem é definido usando a função `spark.sql()`, onde o parâmetro da função é uma string de query SQL.

As células a seguir filtram um conjunto de dados ExperienceEvent para dados existentes exclusivamente entre 1º de janeiro de 2019 e o final de 31 de dezembro de 2019.

#### PySpark 3 ([!DNL Spark] 2.4) {#pyspark3-spark2.4}

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

#### Scala ([!DNL Spark] 2.4) {#scala-spark}

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
>
>
>No Scala, é possível usar `sys.env()` para declarar e retornar um valor de dentro `option`. Isso elimina a necessidade de definir variáveis se você sabe que elas só serão usadas uma única vez. O exemplo a seguir retira `val userToken` do exemplo acima e o declara em linha dentro `option` como uma alternativa:
>
> 
```scala
> .option("user-token", sys.env("PYDASDK_IMS_USER_TOKEN"))
> ```

## Bibliotecas compatíveis {#supported-libraries}

### [!DNL Python] / R

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
| [!DNL jupyterlab] | 1.0.4 |
| pandas_ml | 0.6.1 |
| tensorflow-gpu | 1.14.0 |
| nodejs | 12.3.0 |
| zombaria | 3.0.5 |
| pílula | 0.3.3 |
| fonts-anacond | 1.0 |
| psycopg2 | 2.8.3 |
| azar | 1.3.7 |
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
| [!DNL python] | 3.6.7 |
| mkl-rt | 11.1 |

## Sinalizadores SQL opcionais para [!DNL Query Service] {#optional-sql-flags-for-query-service}

Esta tabela descreve os sinalizadores SQL opcionais que podem ser usados para [!DNL Query Service].

| **Sinalizador** | **Descrição** |
| --- | --- |
| `-h`, `--help` | Mostre a mensagem de ajuda e saia. |
| `-n`, `--notify` | Alternar opção para notificar os resultados do query. |
| `-a`, `--async` | O uso desse sinalizador executa o query de forma assíncrona e pode liberar o kernel enquanto o query está sendo executado. Tenha cuidado ao atribuir resultados de query a variáveis, pois eles podem ser indefinidos se o query não estiver concluído. |
| `-d`, `--display` | O uso desse sinalizador impede que os resultados sejam exibidos. |

