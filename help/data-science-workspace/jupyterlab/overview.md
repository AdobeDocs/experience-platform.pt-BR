---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;tópicos populares;jupyterlab
solution: Experience Platform
title: Visão geral da interface do usuário do JupyterLab
description: O JupyterLab é uma interface de usuário baseada na Web para o Projeto Jupyter e está totalmente integrado ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para cientistas de dados trabalharem com notebooks, códigos e dados Jupyter. Este documento fornece uma visão geral do JupyterLab e seus recursos, bem como instruções para executar ações comuns.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 3%

---

# [!DNL JupyterLab] Visão geral da interface

[!DNL JupyterLab] é uma interface de usuário baseada na Web para [Projeto Jupyter](https://jupyter.org/) e está totalmente integrado ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para cientistas de dados trabalharem com notebooks, códigos e dados Jupyter.

Este documento fornece uma visão geral de [!DNL JupyterLab] e seus recursos, bem como instruções para executar ações comuns.

## [!DNL JupyterLab] em [!DNL Experience Platform]

A integração do Experience Platform JupyterLab é acompanhada de alterações de arquitetura, considerações de design, extensões personalizadas de notebooks, bibliotecas pré-instaladas e uma interface com tema Adobe.

A lista a seguir descreve alguns dos recursos exclusivos do JupyterLab na plataforma:

| Recurso | Descrição |
| --- | --- |
| **Kernels** | Os kernels fornecem notebook e outros [!DNL JupyterLab] O front-end é a capacidade de executar e introduzir código em diferentes linguagens de programação. [!DNL Experience Platform] O fornece kernels adicionais para suportar o desenvolvimento no [!DNL Python], R, PySpark e [!DNL Spark]. Consulte a [kernels](#kernels) para obter mais detalhes. |
| **Acesso aos dados** | Acessar conjuntos de dados existentes diretamente do [!DNL JupyterLab] com suporte total para recursos de leitura e gravação. |
| **[!DNL Platform]integração de serviços** | As integrações integradas permitem utilizar outros [!DNL Platform] serviços diretamente de dentro [!DNL JupyterLab]. Uma lista completa de integrações compatíveis é fornecida na seção sobre [Integração com outros serviços da plataforma](#service-integration). |
| **Autenticação** | Além de <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">Modelo de segurança integrado do JupyterLab</a>, todas as interações entre seu aplicativo e o Experience Platform, incluindo a comunicação serviço-a-serviço da Platform, são criptografadas e autenticadas por meio da <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliotecas de desenvolvimento** | Entrada [!DNL Experience Platform], [!DNL JupyterLab] O fornece bibliotecas pré-instaladas para [!DNL Python], R e PySpark. Consulte a [apêndice](#supported-libraries) para obter uma lista completa de bibliotecas compatíveis. |
| **Controlador de biblioteca** | Quando as bibliotecas pré-instaladas estiverem ausentes para suas necessidades, bibliotecas adicionais poderão ser instaladas para Python e R e são armazenadas temporariamente em contêineres isolados para manter a integridade do [!DNL Platform] e mantenha seus dados seguros. Consulte a [kernels](#kernels) para obter mais detalhes. |

>[!NOTE]
>
>Bibliotecas adicionais só estão disponíveis para a sessão em que foram instaladas. Você deve reinstalar todas as bibliotecas adicionais necessárias ao iniciar novas sessões.

## Integração com outros [!DNL Platform] serviços {#service-integration}

A normalização e a interoperabilidade são conceitos fundamentais [!DNL Experience Platform]. A integração do [!DNL JupyterLab] em [!DNL Platform] como um IDE incorporado permite interagir com outros [!DNL Platform] serviços, permitindo utilizar [!DNL Platform] potencial. As seguintes [!DNL Platform] Os serviços do estão disponíveis em [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Acesse e explore conjuntos de dados com funcionalidades de leitura e gravação.
* **[!DNL Query Service]:** Acesse e explore conjuntos de dados usando SQL, fornecendo menores despesas gerais de acesso aos dados ao lidar com grandes quantidades de dados.
* **[!DNL Sensei ML Framework]:** Desenvolvimento de modelos com a capacidade de treinar e pontuar dados, bem como criação de receitas com um único clique.
* **[!DNL Experience Data Model (XDM)]:** A padronização e a interoperabilidade são os principais conceitos por trás da Adobe Experience Platform. [Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en)O, impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

>[!NOTE]
>
>Alguns [!DNL Platform] integrações de serviço ativadas [!DNL JupyterLab] são limitados a kernels específicos. Consulte a seção sobre [kernels](#kernels) para obter mais detalhes.

## Principais recursos e operações comuns

Informações sobre os principais recursos do [!DNL JupyterLab] As instruções sobre a execução de operações comuns são fornecidas nas seções abaixo:

* [Acessar o JupyterLab](#access-jupyterlab)
* [Interface do JupyterLab](#jupyterlab-interface)
* [Células de código](#code-cells)
* [Kernels](#kernels)
* [Sessões de kernel](#kernel-sessions)
* [Iniciador](#launcher)

### Access [!DNL JupyterLab] {#access-jupyterlab}

Entrada [Adobe Experience Platform](https://platform.adobe.com), selecione **[!UICONTROL Notebooks]** na coluna de navegação à esquerda. Permita algum tempo para [!DNL JupyterLab] para inicializar totalmente.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interface {#jupyterlab-interface}

A variável [!DNL JupyterLab] A interface do consiste em uma barra de menus, uma barra lateral esquerda que pode ser recolhida e a área de trabalho principal que contém guias de documentos e atividades.

**Barra de menus**

A barra de menus na parte superior da interface tem menus de nível superior que expõem as ações disponíveis no [!DNL JupyterLab] com os atalhos de teclado:

* **Arquivo:** Ações relacionadas a arquivos e diretórios
* **Editar:** Ações relacionadas à edição de documentos e outras atividades
* **Exibir:** Ações que alteram a aparência de [!DNL JupyterLab]
* **Executar:** Ações para executar código em diferentes atividades, como blocos de anotações e consoles de código
* **Kernel:** Ações para gerenciar kernels
* **Guias:** Uma lista de documentos e atividades abertos
* **Configurações:** Configurações comuns e um editor de configurações avançado
* **Ajuda:** Uma lista de [!DNL JupyterLab] e links de ajuda do kernel

**Barra lateral esquerda**

A barra lateral esquerda contém guias clicáveis que fornecem acesso aos seguintes recursos:

* **Navegador de arquivos:** Uma lista de diretórios e documentos do bloco de anotações salvos
* **Data Explorer:** Navegue, acesse e explore conjuntos de dados e esquemas
* **Caroços e terminais:** Uma lista de kernel ativo e sessões de terminal com a capacidade de terminar
* **Comandos:** Uma lista de comandos úteis
* **Inspetor de células:** Um editor de células que fornece acesso a ferramentas e metadados úteis para a configuração de um bloco de anotações para fins de apresentação
* **guias:** Uma lista de guias abertas

Selecione uma guia para expor seus recursos ou selecione em uma guia expandida para recolher a barra lateral esquerda, conforme demonstrado abaixo:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Área de trabalho principal**

A principal área de trabalho em [!DNL JupyterLab] permite que você organize documentos e outras atividades em painéis de guias que podem ser redimensionadas ou subdivididas. Arraste uma guia até o centro de um painel de guias para migrá-la. Divida um painel arrastando uma guia para a esquerda, direita, parte superior ou parte inferior do painel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Configuração do servidor de GPU e memória no [!DNL Python]/R

Entrada [!DNL JupyterLab] selecione o ícone de engrenagem no canto superior direito para abrir *Configuração do servidor Notebook*. Você pode ativar a GPU e alocar a quantidade de memória necessária usando o controle deslizante. A quantidade de memória que você pode alocar depende do quanto sua organização provisionou. Selecionar **[!UICONTROL Atualizar configurações]** para salvar.

>[!NOTE]
>
>Apenas uma GPU é provisionada por organização para notebooks. Se a GPU estiver em uso, aguarde o usuário que a reservou para liberá-la. Isso pode ser feito fazendo logout ou deixando a GPU em estado ocioso por quatro horas ou mais.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Encerrar e reiniciar [!DNL JupyterLab]

Entrada [!DNL JupyterLab], você pode encerrar sua sessão para impedir que mais recursos sejam usados. Comece selecionando o **ícone de energia** ![ícone de energia](../images/jupyterlab/user-guide/power_button.png)e selecione **[!UICONTROL Desligar]** do popover que parece encerrar a sessão. As sessões de notebook são encerradas automaticamente após 12 horas sem atividade.

Para reiniciar [!DNL JupyterLab], selecione o **ícone de reinicialização** ![ícone de reinicialização](../images/jupyterlab/user-guide/restart_button.png) localizado diretamente à esquerda do ícone de energia e, em seguida, selecione **[!UICONTROL Restart]** do popover exibido.

![finalizar jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Células de código {#code-cells}

As células de código são o conteúdo principal dos notebooks. Eles contêm código-fonte na linguagem do kernel associado do notebook e a saída como resultado da execução da célula de código. Uma contagem de execução é exibida à direita de cada célula de código que representa sua ordem de execução.

![](../images/jupyterlab/user-guide/code_cell.png)

As ações comuns das células são descritas abaixo:

* **Adicionar uma célula:** Clique no sinal de mais (**+**) no menu do bloco de notas para adicionar uma célula vazia. As novas células são colocadas sob a célula com a qual está ocorrendo a interação no momento, ou no final do bloco de anotações se nenhuma célula em particular estiver em foco.

* **Mover uma célula:** Coloque o cursor à direita da célula que deseja mover, clique e arraste a célula para um novo local. Além disso, mover uma célula de um notebook para outro replica a célula junto com seu conteúdo.

* **Executar uma célula:** Clique no corpo da célula que deseja executar e clique no **play** ícone (****) no menu do notebook. Um asterisco (**\***) é exibido no contador de execução da célula quando o kernel está processando a execução e é substituído por um número inteiro após a conclusão.

* **Excluir uma célula:** Clique no corpo da célula que deseja excluir e clique no link **tesoura** ícone.

### Kernels {#kernels}

Os kernels notebooks são os mecanismos de computação específicos da linguagem para o processamento de células de notebook. Além de [!DNL Python], [!DNL JupyterLab] O oferece suporte adicional a idiomas no R, PySpark e [!DNL Spark] (Scala). Quando você abre um documento de notebook, o kernel associado é iniciado. Quando uma célula de notebook é executada, o kernel executa o cálculo e produz resultados que podem consumir recursos significativos da CPU e da memória. Observe que a memória alocada não é liberada até que o kernel seja desligado.

Certos recursos e funcionalidades são limitados a kernels específicos, conforme descrito na tabela abaixo:

| Kernel | Suporte à instalação da biblioteca | [!DNL Platform] integrações |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sim | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sim | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Não | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sessões de kernel {#kernel-sessions}

Cada bloco de anotações ou atividade ativa em [!DNL JupyterLab] O utiliza uma sessão do kernel. Todas as sessões ativas podem ser encontradas expandindo o **Terminais e kernels circulantes** na barra lateral esquerda. O tipo e o estado do kernel de um notebook podem ser identificados observando-se o canto superior direito da interface do notebook. No diagrama abaixo, o kernel associado do notebook é **[!DNL Python]3** e o seu estado atual é representado por um círculo cinza à direita. Um círculo oco implica um kernel ocioso e um círculo sólido implica um kernel ocupado.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Se o kernel for desligado ou ficar inativo por um período prolongado, **Sem Kernel!** com um círculo sólido é exibido. Ative um kernel clicando no status do kernel e selecionando o tipo de kernel apropriado como demonstrado abaixo:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Iniciador {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

O personalizado *Iniciador* O fornece modelos de bloco de anotações úteis para que os kernels suportados o ajudem a iniciar sua tarefa, incluindo:

| Modelo | Descrição |
| --- | --- |
| Em branco | Um arquivo de bloco de anotações vazio. |
| Início | Um notebook pré-preenchido demonstrando a exploração de dados usando amostras de dados. |
| Vendas de varejo | Um notebook pré-preenchido com o [receita de vendas de varejo](../pre-built-recipes/retail-sales.md) usando dados de amostra. |
| Construtor de fórmula | Um modelo de bloco de anotações para criar uma fórmula no [!DNL JupyterLab]. Ele é pré-preenchido com código e comentários que demonstram e descrevem o processo de criação da fórmula. Consulte a [tutorial do bloco de anotações para a receita](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) para obter uma apresentação detalhada. |
| [!DNL Query Service] | Um bloco de anotações pré-preenchido que demonstre a utilização de [!DNL Query Service] diretamente no [!DNL JupyterLab] com fluxos de trabalho de amostra fornecidos que analisam dados em escala. |
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

Para abrir um novo *Iniciador*, clique em **Arquivo > Novo inicializador**. Como alternativa, expanda a variável **Navegador de arquivos** na barra lateral esquerda e clique no sinal de mais (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Próximas etapas

Para saber mais sobre cada um dos notebooks suportados e como usá-los, visite o [Acesso aos dados dos notebooks Jupyterlab](./access-notebook-data.md) guia do desenvolvedor. Este guia tem como foco o uso de notebooks JupyterLab para acessar seus dados, incluindo leitura, gravação e consulta de dados. O guia de acesso a dados também contém informações sobre a quantidade máxima de dados que podem ser lidos por cada notebook suportado.

## Bibliotecas compatíveis {#supported-libraries}

Para obter uma lista de pacotes compatíveis com o Python, R e PySpark, copie e cole `!conda list` em uma nova célula, em seguida, execute a célula. Uma lista de pacotes suportados é preenchida em ordem alfabética.

![exemplo](../images/jupyterlab/user-guide/libraries.PNG)

Além disso, as seguintes dependências são usadas, mas não listadas:
* CUDA 11.2
* CUDNN 8.1

