---
keywords: Experience Platform; JupyterLab; notebooks; Data Science Workspace; tópicos populares; jupyterlab
solution: Experience Platform
title: Visão geral da interface do usuário do JupyterLab
topic-legacy: Overview
description: O JupyterLab é uma interface de usuário baseada na Web para o Project Jupyter e está totalmente integrado ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para os cientistas de dados trabalharem com notebooks, códigos e dados do Júpiter. Este documento fornece uma visão geral do JupyterLab e seus recursos, bem como instruções para executar ações comuns.
exl-id: 13786fbd-ef16-49cd-8bcf-46320c33e902
source-git-commit: 1d3981c67c86f93394acf49b61bd29154e9653e8
workflow-type: tm+mt
source-wordcount: '1820'
ht-degree: 3%

---

# [!DNL JupyterLab] Visão geral da interface do usuário

[!DNL JupyterLab] é uma interface do usuário baseada na Web para [Jupyter do projeto](https://jupyter.org/) e é totalmente integrado ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para os cientistas de dados trabalharem com notebooks, códigos e dados do Júpiter.

Este documento fornece uma visão geral de [!DNL JupyterLab] e seus recursos, bem como instruções para executar ações comuns.

## [!DNL JupyterLab] em [!DNL Experience Platform]

A integração do JupyterLab é acompanhada de alterações de arquitetura, considerações de design, extensões de notebook personalizadas, bibliotecas pré-instaladas e uma interface de Adobe.

A lista a seguir descreve alguns dos recursos exclusivos do JupyterLab na plataforma:

| Recurso | Descrição |
| --- | --- |
| **Kernels** | Kernels fornecem notebook e outros [!DNL JupyterLab] O front-end é a capacidade de executar e inserir código em diferentes linguagens de programação. [!DNL Experience Platform] fornece kernels adicionais para apoiar o desenvolvimento no [!DNL Python], R, PySpark e [!DNL Spark]. Consulte a [kernels](#kernels) para obter mais detalhes. |
| **Acesso aos dados** | Acessar conjuntos de dados existentes diretamente de dentro do [!DNL JupyterLab] com suporte total para recursos de leitura e gravação. |
| **[!DNL Platform]integração de serviço** | Integrações integradas permitem utilizar outros [!DNL Platform] serviços diretamente de dentro [!DNL JupyterLab]. Uma lista completa de integrações compatíveis é fornecida na seção sobre [Integração com outros serviços da plataforma](#service-integration). |
| **Autenticação** | Além de <a href="https://jupyter-notebook.readthedocs.io/en/stable/security.html" target="_blank">Modelo de segurança integrado do JupyterLab</a>, todas as interações entre seu aplicativo e o Experience Platform, incluindo a comunicação entre serviços da plataforma, são criptografadas e autenticadas por meio do <a href="https://www.adobe.io/authentication/auth-methods.html" target="_blank">[!DNL Adobe Identity Management System] (IMS)</a>. |
| **Bibliotecas de desenvolvimento** | Em [!DNL Experience Platform], [!DNL JupyterLab] O fornece bibliotecas pré-instaladas para [!DNL Python], R e PySpark. Consulte a [apêndice](#supported-libraries) para obter uma lista completa das bibliotecas compatíveis. |
| **Controlador de biblioteca** | Quando as bibliotecas pré-instaladas não atendem às suas necessidades, bibliotecas adicionais podem ser instaladas para Python e R e são armazenadas temporariamente em contêineres isolados para manter a integridade do [!DNL Platform] e manter seus dados seguros. Consulte a [kernels](#kernels) para obter mais detalhes. |

>[!NOTE]
>
>Bibliotecas adicionais só estão disponíveis para a sessão em que foram instaladas. Você deve reinstalar as bibliotecas adicionais necessárias ao iniciar novas sessões.

## Integração com outras [!DNL Platform] serviços {#service-integration}

A normalização e a interoperabilidade são conceitos-chave subjacentes [!DNL Experience Platform]. A integração de [!DNL JupyterLab] on [!DNL Platform] como um IDE incorporado permite que ele interaja com outros [!DNL Platform] , permitindo utilizar [!DNL Platform] ao seu pleno potencial. O seguinte [!DNL Platform] estão disponíveis em [!DNL JupyterLab]:

* **[!DNL Catalog Service]:** Acesse e explore conjuntos de dados com funcionalidades de leitura e gravação.
* **[!DNL Query Service]:** Acesse e explore conjuntos de dados usando o SQL, fornecendo custos indiretos de acesso a dados mais baixos ao lidar com grandes quantidades de dados.
* **[!DNL Sensei ML Framework]:** Desenvolvimento de modelo com a capacidade de treinar e pontuar dados, bem como criação de receita com um único clique.
* **[!DNL Experience Data Model (XDM)]:** A padronização e a interoperabilidade são conceitos-chave por trás do Adobe Experience Platform. [Experience Data Model (XDM)](https://www.adobe.com/go/xdm-home-en), impulsionada pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

>[!NOTE]
>
>Algumas [!DNL Platform] integrações de serviço no [!DNL JupyterLab] são limitadas a kernels específicos. Consulte a seção em [kernels](#kernels) para obter mais detalhes.

## Principais recursos e operações comuns

Informações sobre os principais recursos do [!DNL JupyterLab] e as instruções relativas à realização de operações comuns são fornecidas nas seções abaixo:

* [Acesse o JupyterLab](#access-jupyterlab)
* [Interface do JupyterLab](#jupyterlab-interface)
* [Células de código](#code-cells)
* [Kernels](#kernels)
* [Sessões do kernel](#kernel-sessions)
* [Iniciador](#launcher)

### Access [!DNL JupyterLab] {#access-jupyterlab}

Em [Adobe Experience Platform](https://platform.adobe.com), selecione **[!UICONTROL Notebooks]** na coluna de navegação à esquerda. Permitir algum tempo para [!DNL JupyterLab] para inicializar totalmente.

![](../images/jupyterlab/user-guide/access_jupyterlab.png)

### [!DNL JupyterLab] interface {#jupyterlab-interface}

O [!DNL JupyterLab] A interface consiste em uma barra de menu, uma barra lateral esquerda que pode ser recolhida e a área de trabalho principal contendo guias de documentos e atividades.

**Barra de menus**

A barra de menus na parte superior da interface tem menus de nível superior que expõem as ações disponíveis em [!DNL JupyterLab] com os atalhos de teclado:

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

* **Navegador de arquivos:** Uma lista de documentos e diretórios do bloco de anotações salvos
* **Data Explorer:** Navegar, acessar e explorar conjuntos de dados e esquemas
* **Corta e terminais de comando:** Uma lista de sessões ativas do kernel e do terminal com a capacidade de encerrar
* **Comandos:** Uma lista de comandos úteis
* **Inspetor de células:** Um editor de células que fornece acesso a ferramentas e metadados úteis para a configuração de um bloco de notas para fins de apresentação
* **guias:** Uma lista de guias abertas

Selecione uma guia para expor seus recursos ou selecione em uma guia expandida para recolher a barra lateral esquerda, conforme mostrado abaixo:

![](../images/jupyterlab/user-guide/left_sidebar_collapse.gif)

**Área de trabalho principal**

A principal área de trabalho no [!DNL JupyterLab] permite organizar documentos e outras atividades em painéis de guias que podem ser redimensionados ou subdivididos. Arraste uma guia até o centro de um painel de guias para migrar a guia . Divida um painel arrastando uma guia para a esquerda, direita, superior ou inferior do painel:

![](../images/jupyterlab/user-guide/main_work_area.gif)

### Configuração da GPU e do servidor de memória em [!DNL Python]/R

Em [!DNL JupyterLab] selecione o ícone de engrenagem no canto superior direito para abrir *Configuração do servidor de notebook*. Você pode ativar a GPU e alocar a quantidade de memória necessária usando o controle deslizante . A quantidade de memória que você pode alocar depende de quanto sua organização provisionou. Selecionar **[!UICONTROL Atualizar configurações]** para salvar.

>[!NOTE]
>
>Somente uma GPU é provisionada por organização para notebooks. Se a GPU estiver em uso, é necessário aguardar até que o usuário que reservou a GPU no momento a libere. Isso pode ser feito fazendo logoff ou deixando a GPU em um estado inativo por quatro ou mais horas.

![](../images/jupyterlab/user-guide/notebook-gpu-config.png)

### Encerrar e reiniciar [!DNL JupyterLab]

Em [!DNL JupyterLab], você pode encerrar a sessão para impedir que outros recursos sejam usados. Comece selecionando o **ícone de potência** ![ícone de potência](../images/jupyterlab/user-guide/power_button.png), em seguida selecione **[!UICONTROL Desligar]** do fornecedor que parece terminar a sessão. As sessões do notebook terminam automaticamente após 12 horas sem atividade.

Para reiniciar [!DNL JupyterLab], selecione o **ícone reiniciar** ![ícone reiniciar](../images/jupyterlab/user-guide/restart_button.png) localizado diretamente à esquerda do ícone de energia e, em seguida, selecione **[!UICONTROL Reiniciar]** do poder que aparece.

![rescindir o jupyterlab](../images/jupyterlab/user-guide/shutdown-jupyterlab.gif)

### Células de código {#code-cells}

As células de código são o conteúdo principal dos blocos de anotações. Eles contêm o código-fonte no idioma do kernel associado do notebook e a saída como resultado da execução da célula de código. Uma contagem de execução é exibida à direita de cada célula de código que representa sua ordem de execução.

![](../images/jupyterlab/user-guide/code_cell.png)

As ações comuns das células são descritas abaixo:

* **Adicionar uma célula:** Clique no símbolo de mais (**+**) no menu do bloco de anotações para adicionar uma célula vazia. Novas células são colocadas sob a célula com a qual está sendo interagida no momento ou no final do notebook se nenhuma célula específica estiver em foco.

* **Mover uma célula:** Coloque o cursor à direita da célula que deseja mover e clique e arraste a célula para um novo local. Além disso, mover uma célula de um notebook para outro replica a célula junto com seu conteúdo.

* **Executar uma célula:** Clique no corpo da célula que deseja executar e clique no botão **play** ícone (**▶**) no menu do notebook. Um asterisco (**\***) é exibido no contador de execução da célula quando o kernel está processando a execução e é substituído por um inteiro após a conclusão.

* **Excluir uma célula:** Clique no corpo da célula que deseja excluir e clique no botão **tesoura** ícone .

### Kernels {#kernels}

Os kernels de notebook são os mecanismos de computação específicos da linguagem para o processamento de células de notebook. Além de [!DNL Python], [!DNL JupyterLab] fornece suporte adicional de idioma em R, PySpark e [!DNL Spark] (Scala). Quando você abre um documento de notebook, o kernel associado é iniciado. Quando uma célula de notebook é executada, o kernel executa o cálculo e produz resultados que podem consumir recursos significativos de CPU e memória. Observe que a memória alocada não é liberada até que o kernel seja desligado.

Determinados recursos e funcionalidades estão limitados a kernels específicos, conforme descrito na tabela abaixo:

| Kernel | Suporte para instalação de biblioteca | [!DNL Platform] integrações |
| :----: | :--------------------------: | :-------------------- |
| **[!DNL Python]** | Sim | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li><li>[!DNL Query Service]</li></ul> |
| **R** | Sim | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |
| **Scala** | Não | <ul><li>[!DNL Sensei ML Framework]</li><li>[!DNL Catalog Service]</li></ul> |

### Sessões do kernel {#kernel-sessions}

Cada bloco de anotações ativo ou atividade em [!DNL JupyterLab] O usa uma sessão do kernel. Todas as sessões ativas podem ser encontradas expandindo o **Terminais e kernels em funcionamento** na barra lateral esquerda. O tipo e o estado do kernel de um notebook podem ser identificados observando a parte superior direita da interface do notebook. No diagrama abaixo, o kernel associado do notebook é **[!DNL Python]3** e o seu estado atual é representado por um círculo cinza à direita. Um círculo oco implica um kernel em marcha lenta sem carga e um círculo sólido implica um kernel ocupado.

![](../images/jupyterlab/user-guide/kernel_and_state_1.png)

Se o kernel for desligado ou inativo por um período prolongado, **Sem kernel!** com um círculo sólido é mostrado. Ative um kernel clicando no status do kernel e selecionando o tipo de kernel apropriado, conforme mostrado abaixo:

![](../images/jupyterlab/user-guide/switch_kernel.gif)

### Iniciador {#launcher}

[//]: # (Talk about the different Notebooks, introduce that certain starter notebooks are limited to particular kernels)

O *Iniciador* O fornece modelos de notebook úteis para seus kernels suportados para ajudá-lo a iniciar sua tarefa, incluindo:

| Modelo | Descrição |
| --- | --- |
| Em branco | Um arquivo de bloco de notas vazio. |
| Início | Um notebook pré-preenchido demonstrando a exploração de dados usando dados de amostra. |
| Vendas de varejo | Um notebook pré-cheio com a [receita de vendas de varejo](../pre-built-recipes/retail-sales.md) uso de dados de amostra. |
| Criador de receita | Um modelo de bloco de notas para criar uma receita em [!DNL JupyterLab]. Ele é pré-preenchido com código e comentário que demonstra e descreve o processo de criação da receita. Consulte a [tutorial de notebook a receita](https://www.adobe.com/go/data-science-create-recipe-notebook-tutorial-en) para uma apresentação detalhada. |
| [!DNL Query Service] | Um notebook pré-preenchido demonstrando o uso de [!DNL Query Service] diretamente em [!DNL JupyterLab] com fluxos de trabalho de amostra fornecidos que analisam dados em escala. |
| Eventos XDM | Um notebook pré-preenchido que demonstra a exploração de dados em dados de evento de experiência de pós-valor, com foco em recursos comuns na estrutura de dados. |
| Consultas XDM | Um notebook pré-preenchido demonstrando consultas comerciais de amostra em dados de eventos de experiência. |
| Agregação | Um notebook pré-preenchido demonstrando fluxos de trabalho de amostra para agregar grandes quantidades de dados em partes menores e gerenciáveis. |
| Geração de cluster | Um notebook pré-preenchido demonstrando o processo completo de modelagem de aprendizado de máquina usando algoritmos de cluster. |

Alguns modelos de notebook estão limitados a certos kernels. A disponibilidade do modelo para cada kernel é mapeada na tabela a seguir:

<table>
    <tr>
        <td></td>
        <th><strong>Em branco</strong></th>
        <th><strong>Início</strong></th>
        <th><strong>Vendas de varejo</strong></th>
        <th><strong>Criador de receita</strong></th>
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

Para abrir um novo *Iniciador*, clique em **Arquivo > Novo iniciador**. Como alternativa, expanda a **Navegador de arquivos** na barra lateral esquerda e clique no símbolo de mais (**+**):

![](../images/jupyterlab/user-guide/new_launcher.gif)

## Próximas etapas

Para saber mais sobre cada um dos notebooks suportados e como usá-los, visite o [Acesso aos dados dos notebooks Jupyterlab](./access-notebook-data.md) guia do desenvolvedor. Este guia se concentra em como usar os notebooks JupyterLab para acessar seus dados, incluindo leitura, escrita e consulta de dados. O guia de acesso a dados também contém informações sobre a quantidade máxima de dados que podem ser lidos por cada notebook suportado.

## Bibliotecas compatíveis {#supported-libraries}

Para obter uma lista de pacotes compatíveis em Python, R e PySpark, copie e cole `!conda list` em uma nova célula, execute a célula. Uma lista de pacotes suportados é preenchida em ordem alfabética.

![exemplo](../images/jupyterlab/user-guide/libraries.PNG)

Além disso, as seguintes dependências são usadas, mas não listadas:
* CUDA 11.2
* CUDNN 8.1

