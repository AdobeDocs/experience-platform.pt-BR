---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;tópicos populares;jupyterlab
solution: Experience Platform
title: Visão geral da interface do usuário do JupyterLab
description: O JupyterLab é uma interface de usuário baseada na Web para o Projeto Jupyter e está totalmente integrado ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para cientistas de dados trabalharem com notebooks, códigos e dados Jupyter. Este documento fornece uma visão geral do JupyterLab e seus recursos, bem como instruções para executar ações comuns.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1831'
ht-degree: 2%

---

# Visão geral da interface do [!DNL JupyterLab]

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

[!DNL JupyterLab] é uma interface de usuário baseada na Web para o [Projeto Jupyter](https://jupyter.org/) e está totalmente integrada ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para cientistas de dados trabalharem com notebooks, códigos e dados Jupyter.

Este documento fornece uma visão geral do [!DNL JupyterLab] e seus recursos, bem como instruções para executar ações comuns.

## [!DNL JupyterLab] em [!DNL Experience Platform]

A integração do JupyterLab da Experience Platform é acompanhada de alterações de arquitetura, considerações de design, extensões personalizadas de notebooks, bibliotecas pré-instaladas e uma interface com tema Adobe.

A lista a seguir descreve alguns dos recursos exclusivos do JupyterLab no Experience Platform:

| Recurso | Descrição |
| --- | --- |
| **Kernels** | Os kernels fornecem ao notebook e a outros front-ends do [!DNL JupyterLab] a capacidade de executar e introduzir código em diferentes linguagens de programação. O [!DNL Experience Platform] fornece kernels adicionais para dar suporte ao desenvolvimento no [!DNL Python], R, PySpark e [!DNL Spark]. Consulte a seção [kernels](#kernels) para obter mais detalhes. |
| **Acesso aos dados** | Acesse os conjuntos de dados existentes diretamente do [!DNL JupyterLab] com suporte total para recursos de leitura e gravação. |
| **[!DNL Experience Platform]integração de serviço** | As integrações internas permitem que você utilize outros serviços do [!DNL Experience Platform] diretamente de dentro do [!DNL JupyterLab]. Uma lista completa de integrações com suporte é fornecida na seção sobre [Integração com outros serviços da Experience Platform](#service-integration). |
| **Autenticação** | Além do <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">modelo de segurança interno do JupyterLab</a>, todas as interações entre seu aplicativo e a Experience Platform, incluindo a comunicação serviço a serviço da Experience Platform, são criptografadas e autenticadas por meio do <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliotecas de desenvolvimento** | No [!DNL Experience Platform], o [!DNL JupyterLab] fornece bibliotecas pré-instaladas para o [!DNL Python], R e PySpark. Consulte o [apêndice](#supported-libraries) para obter uma lista completa de bibliotecas com suporte. |
| **Controlador de biblioteca** | Quando as bibliotecas pré-instaladas estiverem ausentes para suas necessidades, bibliotecas adicionais poderão ser instaladas para Python e R e são armazenadas temporariamente em contêineres isolados para manter a integridade do [!DNL Experience Platform] e manter seus dados seguros. Consulte a seção [kernels](#kernels) para obter mais detalhes. |

>[!NOTE]
>
>Bibliotecas adicionais só estão disponíveis para a sessão em que foram instaladas. Você deve reinstalar todas as bibliotecas adicionais necessárias ao iniciar novas sessões.

## Integração com outros serviços do [!DNL Experience Platform] {#service-integration}

A padronização e a interoperabilidade são os principais conceitos por trás do [!DNL Experience Platform]. A integração do [!DNL JupyterLab] no [!DNL Experience Platform] como um IDE incorporado permite que ele interaja com outros serviços do [!DNL Experience Platform], permitindo que você utilize o [!DNL Experience Platform] em todo o seu potencial. Os seguintes serviços [!DNL Experience Platform] estão disponíveis em [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Acesse e explore conjuntos de dados com funcionalidades de leitura e gravação.
* **[!DNL Query Service]:** Acesse e explore conjuntos de dados usando SQL, fornecendo menores despesas gerais de acesso aos dados ao lidar com grandes quantidades de dados.
* **[!DNL Sensei ML Framework]:** Desenvolvimento de modelos com a capacidade de treinar e pontuar dados, bem como criação de receitas com um único clique.
* **[!DNL Experience Data Model (XDM)]:** A padronização e a interoperabilidade são os principais conceitos por trás do Adobe Experience Platform. O [Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en), orientado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

>[!NOTE]
>
>Algumas [!DNL Experience Platform] integrações de serviço em [!DNL JupyterLab] estão limitadas a kernels específicos. Consulte a seção sobre [kernels](#kernels) para obter mais detalhes.

## Principais recursos e operações comuns

Informações sobre os principais recursos do [!DNL JupyterLab] e instruções sobre como executar operações comuns são fornecidas nas seções abaixo:

* [Acessar o JupyterLab](#access-jupyterlab)
* [Interface do JupyterLab](#jupyterlab-interface)
* [Células de código](#code-cells)
* [Kernels](#kernels)
* [Sessões de kernel](#kernel-sessions)
* [Iniciador](#launcher)

### Acessar [!DNL JupyterLab] {#access-jupyterlab}

Em [Adobe Experience Platform](https://platform.adobe.com), selecione **[!UICONTROL Notebooks]** na coluna de navegação esquerda. Aguarde algum tempo para que [!DNL JupyterLab] seja totalmente inicializado.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### Interface [!DNL JupyterLab] {#jupyterlab-interface}

A interface [!DNL JupyterLab] consiste em uma barra de menus, uma barra lateral esquerda que pode ser recolhida e a área de trabalho principal que contém guias de documentos e atividades.

**Barra de menus**

A barra de menus na parte superior da interface tem menus de nível superior que expõem as ações disponíveis em [!DNL JupyterLab] com seus atalhos de teclado:

* **Arquivo:** Ações relacionadas a arquivos e diretórios
* **Editar:** Ações relacionadas à edição de documentos e outras atividades
* **Exibir:** Ações que alteram a aparência de [!DNL JupyterLab]
* **Executar:** Ações para executar código em diferentes atividades, como blocos de anotações e consoles de código
* **Kernel:** ações para gerenciar kernels
* **Guias:** Uma lista de documentos e atividades abertos
* **Configurações:** configurações comuns e um editor de configurações avançado
* **Ajuda:** Uma lista de [!DNL JupyterLab] e links de ajuda do kernel

**Barra lateral esquerda**

A barra lateral esquerda contém guias clicáveis que fornecem acesso aos seguintes recursos:

* **Navegador de arquivos:** Uma lista de diretórios e documentos de bloco de anotações salvos
* **Data Explorer:** Navegue, acesse e explore conjuntos de dados e esquemas
* **Executando kernels e terminais:** Uma lista de sessões ativas de kernel e terminal com a capacidade de terminar
* **Comandos:** Uma lista de comandos úteis
* **Inspetor de células:** um editor de células que fornece acesso a ferramentas e metadados úteis para a configuração de um bloco de anotações para fins de apresentação
* **guias:** Uma lista de guias abertas

Selecione uma guia para expor seus recursos ou selecione em uma guia expandida para recolher a barra lateral esquerda, conforme demonstrado abaixo:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Área de trabalho principal**

A área de trabalho principal do [!DNL JupyterLab] permite que você organize documentos e outras atividades em painéis de guias que podem ser redimensionadas ou subdivididas. Arraste uma guia até o centro de um painel de guias para migrá-la. Divida um painel arrastando uma guia para a esquerda, direita, parte superior ou parte inferior do painel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Configuração do servidor de GPU e memória em [!DNL Python]/R

Em [!DNL JupyterLab], selecione o ícone de engrenagem no canto superior direito para abrir a *Configuração do Notebook Server*. Você pode ativar a GPU e alocar a quantidade de memória necessária usando o controle deslizante. A quantidade de memória que você pode alocar depende do quanto sua organização provisionou. Selecione **[!UICONTROL Update configs]** para salvar.

>[!NOTE]
>
>Apenas uma GPU é provisionada por organização para notebooks. Se a GPU estiver em uso, você precisará aguardar o usuário que reservou a GPU para liberá-la. Isso pode ser feito fazendo logout ou deixando a GPU em estado ocioso por quatro horas ou mais.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Encerrar e reiniciar [!DNL JupyterLab]

No [!DNL JupyterLab], você pode encerrar sua sessão para impedir que outros recursos sejam usados. Comece selecionando o **ícone de energia** ![ícone de energia](/help/images/icons/power.png) e selecione **[!UICONTROL Shut Down]** no popover que parece encerrar sua sessão. As sessões de notebook são encerradas automaticamente após 12 horas sem atividade.

Para reiniciar [!DNL JupyterLab], selecione o **ícone de reiniciar** ![ícone de reiniciar](/help/images/icons/restart.png), localizado diretamente à esquerda do ícone de energia, e selecione **[!UICONTROL Restart]** no popover exibido.

![finalizar jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Células de código {#code-cells}

As células de código são o conteúdo principal dos notebooks. Eles contêm código-fonte na linguagem do kernel associado do notebook e a saída como resultado da execução da célula de código. Uma contagem de execução é exibida à direita de cada célula de código que representa sua ordem de execução.

![](../images/jupyterlab/user-guide/code_cell.png)

As ações comuns das células são descritas abaixo:

* **Adicionar uma célula:** Clique no símbolo de mais (**+**) no menu de bloco de anotações para adicionar uma célula vazia. As novas células são colocadas sob a célula com a qual está ocorrendo a interação no momento, ou no final do bloco de anotações se nenhuma célula em particular estiver em foco.

* **Mover uma célula:** Coloque o cursor à direita da célula que deseja mover, clique e arraste a célula para um novo local. Além disso, mover uma célula de um notebook para outro replica a célula junto com seu conteúdo.

* **Execute uma célula:** clique no corpo da célula que deseja executar e clique no ícone **reproduzir** (**▶**) no menu do bloco de anotações. Um asterisco (**\***) é exibido no contador de execução da célula quando o kernel está processando a execução e é substituído por um número inteiro após a conclusão.

* **Excluir uma célula:** clique no corpo da célula que deseja excluir e clique no ícone **tesoura**.

### Kernels {#kernels}

Os kernels notebooks são os mecanismos de computação específicos da linguagem para o processamento de células de notebook. Além do [!DNL Python], o [!DNL JupyterLab] fornece suporte adicional a idiomas no R, PySpark e [!DNL Spark] (Scala). Quando você abre um documento de notebook, o kernel associado é iniciado. Quando uma célula de notebook é executada, o kernel executa o cálculo e produz resultados que podem consumir significantes recursos de CPU e memória. Observe que a memória alocada não é liberada até que o kernel seja desligado.

Certos recursos e funcionalidades são limitados a kernels específicos, conforme descrito na tabela abaixo:

| Kernel | Suporte à instalação da biblioteca | [!DNL Experience Platform] integrações |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sim | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sim | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Escala** | Não | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sessões de kernel {#kernel-sessions}

Cada bloco de anotações ou atividade ativa no [!DNL JupyterLab] usa uma sessão do kernel. Todas as sessões ativas podem ser encontradas expandindo a guia **Terminais e kernels** em execução na barra lateral esquerda. O tipo e o estado do kernel de um notebook podem ser identificados observando-se o canto superior direito da interface do notebook. No diagrama abaixo, o kernel associado do bloco de anotações é **[!DNL Python]3** e seu estado atual é representado por um círculo cinza à direita. Um círculo oco implica um kernel ocioso e um círculo sólido implica um kernel ocupado.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Se o kernel estiver desligado ou inativo por um período prolongado, **Não há kernel!** com um círculo sólido é exibido. Ative um kernel clicando no status do kernel e selecionando o tipo de kernel apropriado como demonstrado abaixo:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Iniciador {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

O *Iniciador* personalizado fornece modelos de bloco de anotações úteis para que os kernels com suporte o ajudem a iniciar sua tarefa, incluindo:

| Modelo | Descrição |
| --- | --- |
| Em branco | Um arquivo de bloco de anotações vazio. |
| Início | Um notebook pré-preenchido demonstrando a exploração de dados usando amostras de dados. |
| Vendas de varejo | Um bloco de anotações pré-preenchido com a [fórmula de vendas de varejo](../pre-built-recipes/retail-sales.md) usando dados de exemplo. |
| Construtor de fórmula | Um modelo de bloco de anotações para criar uma fórmula em [!DNL JupyterLab]. Ele é pré-preenchido com código e comentários que demonstram e descrevem o processo de criação da fórmula. Consulte o [tutorial do bloco de anotações para a fórmula](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) para obter uma apresentação detalhada. |
| [!DNL Query Service] | Um bloco de anotações pré-preenchido demonstrando o uso de [!DNL Query Service] diretamente em [!DNL JupyterLab] com fluxos de trabalho de exemplo fornecidos que analisam dados em escala. |
| Eventos XDM | Um bloco de anotações pré-preenchido que demonstra a exploração de dados em dados de Evento de experiência pós-valor, com foco nos recursos comuns na estrutura de dados. |
| Consultas XDM | Um notebook preenchido previamente demonstrando exemplos de consultas comerciais sobre dados de evento de experiência. |
| Agregação | Um notebook pré-preenchido demonstrando fluxos de trabalho de amostra para agregar grandes quantidades de dados em blocos menores e gerenciáveis. |
| Geração de cluster | Um notebook pré-preenchido demonstrando o processo completo de modelagem de aprendizado de máquina usando algoritmos de cluster. |

Alguns modelos de notebook estão limitados a determinados kernels. A disponibilidade de modelo para cada kernel é mapeada na seguinte tabela:

<table>
    <tr>
        <td></td>
        <th><strong>Em branco</strong></th>
        <th><strong>Início</strong></th>
        <th><strong>Vendas de varejo</strong></th>
        <th><strong>Construtor de fórmula</strong></th>
        <th><strong>[!DNL Query Service]</strong></th>
        <th><strong>Eventos XDM</strong></th>
        <th><strong>Consultas XDM</strong></th>
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

Para abrir um novo *Iniciador*, clique em **Arquivo > Novo Iniciador**. Como alternativa, expanda o **Navegador de arquivos** da barra lateral esquerda e clique no símbolo de mais (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Próximas etapas

Para saber mais sobre cada um dos notebooks compatíveis e como usá-los, visite o [guia do desenvolvedor do acesso aos dados dos notebooks Jupyterlab](./access-notebook-data.md). Este guia tem como foco o uso de notebooks JupyterLab para acessar seus dados, incluindo leitura, gravação e consulta de dados. O guia de acesso a dados também contém informações sobre a quantidade máxima de dados que podem ser lidos por cada notebook suportado.

## Bibliotecas compatíveis {#supported-libraries}

Para obter uma lista de pacotes compatíveis com o Python, R e PySpark, copie e cole `!conda list` em uma nova célula e execute a célula. Uma lista de pacotes suportados é preenchida em ordem alfabética.

![exemplo](../images/jupyterlab/user-guide/libraries.PNG)

Além disso, as seguintes dependências são usadas, mas não listadas:

* CUDA 11.2
* CUDNN 8.1

