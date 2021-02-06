---
keywords: Experience Platform;arquivos de origem do pacote;Data Science Workspace;popular topics;Docker;docker image;package source files;Data Science Workspace;popular topics;Docker;docker image
solution: Experience Platform
title: Arquivos de origem do pacote em uma receita
topic: tutorial
type: Tutorial
description: Este tutorial fornece instruções sobre como disponibilizar os arquivos de origem de amostra de Vendas de varejo fornecidos em um arquivo de arquivamento, que pode ser usado para criar uma fórmula no Adobe Experience Platform Data Science Workspace seguindo o fluxo de trabalho de importação da fórmula na interface do usuário ou usando a API.
translation-type: tm+mt
source-git-commit: f6cfd691ed772339c888ac34fcbd535360baa116
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---


# Empacotar arquivos de origem em uma fórmula

Este tutorial fornece instruções sobre como você pode disponibilizar os arquivos de origem de amostra de Vendas de varejo fornecidos em um arquivo de arquivamento, que pode ser usado para criar uma fórmula no Adobe Experience Platform [!DNL Data Science Workspace] seguindo o fluxo de trabalho de importação da fórmula na interface do usuário ou usando a API.

Conceitos para entender:

- **Receitas**: Uma receita é um termo para uma especificação de modelo e um container de nível superior representando um aprendizado de máquina específico, algoritmo de inteligência artificial ou conjunto de algoritmos, lógica de processamento e configuração necessários para criar e executar um modelo e, portanto, ajudar a resolver problemas específicos da empresa.
- **Arquivos** de origem: Arquivos individuais em seu projeto que contêm a lógica de uma fórmula.

## Pré-requisitos

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Criação de receita

Receba start de criação com arquivos de origem de empacotamento para criar um arquivo. Os arquivos de origem definem a lógica e os algoritmos de aprendizado da máquina usados para resolver um problema específico em mãos e são escritos em [!DNL Python], R, PySpark ou Scala. Os arquivos de arquivamento criados assumem a forma de uma imagem Docker. Depois de criado, o arquivo de arquivamento empacotado é importado para [!DNL Data Science Workspace] para criar uma fórmula [na interface do usuário](./import-packaged-recipe-ui.md) ou [usando a API](./import-packaged-recipe-api.md).

### Criação de modelo com base em docking {#docker-based-model-authoring}

Uma imagem do Docker permite que um desenvolvedor empacote um aplicativo com todas as partes de que precisa, como bibliotecas e outras dependências, e envie-o como um pacote.

A imagem do Docker criada é enviada para o Registro de Container do Azure usando as credenciais fornecidas a você durante o fluxo de trabalho de criação da receita.

Para obter suas credenciais do Registro de Container do Azure, faça logon em [Adobe Experience Platform](https://platform.adobe.com). Na coluna de navegação esquerda, navegue até **[!UICONTROL Workflows]**. Selecione **[!UICONTROL Importar receita]** seguido de selecionar **[!UICONTROL Iniciar]**. Consulte a captura de tela abaixo para obter referência.

![](../images/models-recipes/package-source-files/import.png)

A página **[!UICONTROL Configurar]** é aberta. Forneça um **[!UICONTROL Nome da Receita]** apropriado, por exemplo, &quot;Fórmula de Vendas de Varejo&quot; e, opcionalmente, forneça uma descrição ou um URL de documentação. Depois de concluído, clique em **[!UICONTROL Próximo]**.

![](../images/models-recipes/package-source-files/configure.png)

Selecione o *Runtime* apropriado e escolha um **[!UICONTROL Classificação]** para *Tipo*. Suas credenciais do Registro de Container do Azure são geradas uma vez concluídas.

>[!NOTE]
>
>*O* Typeé a classe de problema de aprendizado de máquina para a qual a receita foi projetada e é usada após o treinamento para ajudar a avaliar a execução do treinamento.

>[!TIP]
>
>- Para [!DNL Python] receitas, selecione o tempo de execução **[!UICONTROL Python]**.
>- Para receitas R, selecione o tempo de execução **[!UICONTROL R]**.
>- Para fórmulas PySpark, selecione o tempo de execução **[!UICONTROL PySpark]**. Um tipo de artefato preenche automaticamente.
>- Para fórmulas Scala, selecione o tempo de execução **[!UICONTROL Spark]**. Um tipo de artefato preenche automaticamente.


![](../images/models-recipes/package-source-files/docker-creds.png)

Anote os valores para host, nome de usuário e senha do Docker. Eles são usados para criar e mover sua imagem [!DNL Docker] nos workflows descritos abaixo.

>[!NOTE]
>
>O URL de origem é fornecido após concluir as etapas descritas abaixo. O arquivo de configuração é explicado em tutoriais subsequentes encontrados em [próximas etapas](#next-steps).

### Empacotar os arquivos de origem

Start obtendo a base de códigos de amostra encontrada no repositório <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace Reference</a>.

- [Criar imagem do Docker Python](#python-docker)
- [Imagem do Docker Build R](#r-docker)
- [Criar imagem PySpark Docker](#pyspark-docker)
- [Criar imagem Docker Scala (Spark)](#scala-docker)

### Criar [!DNL Python] imagem do Docker {#python-docker}

Se você não tiver feito isso, clone o repositório [!DNL GitHub] no sistema local com o seguinte comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue até o diretório `experience-platform-dsw-reference/recipes/python/retail`. Aqui, você encontrará os scripts `login.sh` e `build.sh` usados para fazer logon no Docker e para criar a imagem [!DNL Python Docker]. Se você tiver suas [credenciais do Docker](#docker-based-model-authoring) prontas, digite os seguintes comandos na ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Observe que ao executar o script de login, é necessário fornecer o host do Docker, o nome de usuário e a senha. Ao criar, é necessário fornecer o host do Docker e uma tag de versão para a compilação.

Quando o script de compilação for concluído, você receberá um URL de arquivo de origem do Docker na saída do console. Para este exemplo específico, ele será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copie esse URL e vá para as [próximas etapas](#next-steps).

### Criar imagem R [!DNL Docker] {#r-docker}

Se você não tiver feito isso, clone o repositório [!DNL GitHub] no sistema local com o seguinte comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue até o diretório `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` dentro do repositório clonado. Aqui, você encontrará os arquivos `login.sh` e `build.sh` que serão usados para fazer logon no Docker e para criar a imagem R Docker. Se você tiver suas [credenciais do Docker](#docker-based-model-authoring) prontas, digite os seguintes comandos na ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Observe que ao executar o script de login, é necessário fornecer o host do Docker, o nome de usuário e a senha. Ao criar, é necessário fornecer o host do Docker e uma tag de versão para a compilação.

Quando o script de compilação for concluído, você receberá um URL de arquivo de origem do Docker na saída do console. Para este exemplo específico, ele será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copie esse URL e vá para as [próximas etapas](#next-steps).

### Criar imagem do Docker PySpark {#pyspark-docker}

Start clonando o repositório [!DNL GitHub] em seu sistema local com o seguinte comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue até o diretório `experience-platform-dsw-reference/recipes/pyspark/retail`. Os scripts `login.sh` e `build.sh` estão localizados aqui e são usados para fazer logon no Docker e para criar a imagem do Docker. Se você tiver suas [credenciais do Docker](#docker-based-model-authoring) prontas, digite os seguintes comandos na ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Observe que ao executar o script de login, é necessário fornecer o host do Docker, o nome de usuário e a senha. Ao criar, é necessário fornecer o host do Docker e uma tag de versão para a compilação.

Quando o script de compilação for concluído, você receberá um URL de arquivo de origem do Docker na saída do console. Para este exemplo específico, ele será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Copie esse URL e vá para as [próximas etapas](#next-steps).

### Criar imagem Scala Docker {#scala-docker}

Start clonando o repositório [!DNL GitHub] no sistema local com o seguinte comando no terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Em seguida, navegue até o diretório `experience-platform-dsw-reference/recipes/scala`, onde você pode encontrar os scripts `login.sh` e `build.sh`. Esses scripts são usados para fazer logon no Docker e criar a imagem do Docker. Se você tiver suas [credenciais do Docker](#docker-based-model-authoring) prontas, digite os seguintes comandos para o terminal em ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Se você estiver recebendo um erro de permissão ao tentar fazer login no Docker usando o script `login.sh`, tente usar o comando `bash login.sh`.

Ao executar o script de login, é necessário fornecer o host do Docker, o nome de usuário e a senha. Ao criar, é necessário fornecer o host do Docker e uma tag de versão para a compilação.

Quando o script de compilação for concluído, você receberá um URL de arquivo de origem do Docker na saída do console. Para este exemplo específico, ele será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copie esse URL e vá para as [próximas etapas](#next-steps).

## Próximas etapas {#next-steps}

Este tutorial passou do empacotamento de arquivos de origem para uma Receita, a etapa de pré-requisito para importar uma Receita para [!DNL Data Science Workspace]. Agora você deve ter uma imagem do Docker no Registro de Container do Azure junto com o URL da imagem correspondente. Agora você está pronto para iniciar o tutorial sobre como importar uma receita empacotada para [!DNL Data Science Workspace]. Selecione um dos links do tutorial abaixo para começar:

- [Importar uma receita empacotada na interface do usuário](./import-packaged-recipe-ui.md)
- [Importar uma Receita empacotada usando a API](./import-packaged-recipe-api.md)