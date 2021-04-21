---
keywords: Experience Platform, arquivos de origem do pacote, Data Science Workspace, tópicos populares, Docker, imagem do docker
solution: Experience Platform
title: Arquivos de origem do pacote em uma receita
topic-legacy: tutorial
type: Tutorial
description: Este tutorial fornece instruções sobre como empacotar os arquivos de origem da amostra de Vendas de varejo fornecidos em um arquivo de arquivamento, que pode ser usado para criar uma receita no Adobe Experience Platform Data Science Workspace seguindo o fluxo de trabalho de importação da receita na interface do usuário ou usando a API.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '1146'
ht-degree: 0%

---

# Compactar arquivos de origem em uma receita

Este tutorial fornece instruções sobre como empacotar os arquivos de origem da amostra de Vendas de varejo fornecidos em um arquivo de arquivamento, que pode ser usado para criar uma receita no Adobe Experience Platform [!DNL Data Science Workspace] seguindo o fluxo de trabalho de importação da receita na interface do usuário ou usando a API.

Conceitos a serem compreendidos:

- **Receitas**: Uma receita é um termo treinado para uma especificação de modelo e um contêiner de nível superior que representa um aprendizado de máquina específico, algoritmo de inteligência artificial ou conjunto de algoritmos, lógica de processamento e configuração necessários para criar e executar um modelo e, portanto, ajudar a resolver problemas específicos de negócios.
- **Arquivos** de origem: Arquivos individuais no seu projeto que contêm a lógica de uma receita.

## Pré-requisitos

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Criação de receita

A criação de receita começa com arquivos de origem de empacotamento para criar um arquivo de arquivamento. Os arquivos de origem definem a lógica e os algoritmos de aprendizado de máquina usados para resolver um problema específico em mãos e são escritos em [!DNL Python], R, PySpark ou Scala. Os arquivos de arquivamento incorporados assumem a forma de uma imagem Docker. Uma vez criado, o arquivo de arquivamento empacotado é importado para [!DNL Data Science Workspace] para criar uma receita [na interface do usuário](./import-packaged-recipe-ui.md) ou [usando a API](./import-packaged-recipe-api.md).

### Criação de modelo baseado em Docker {#docker-based-model-authoring}

Uma imagem do Docker permite que um desenvolvedor empacote um aplicativo com todas as partes necessárias, como bibliotecas e outras dependências, e envie-o como um único pacote.

A imagem do Docker criada é enviada para o Registro do Contêiner do Azure usando credenciais fornecidas para você durante o fluxo de trabalho de criação da receita.

Para obter suas credenciais do Registro do Contêiner do Azure, faça logon em [Adobe Experience Platform](https://platform.adobe.com). Na coluna de navegação à esquerda, navegue até **[!UICONTROL Workflows]**. Selecione **[!UICONTROL Import Recipe]** seguido por selecionar **[!UICONTROL Launch]**. Veja a captura de tela abaixo para referência.

![](../images/models-recipes/package-source-files/import.png)

A página **[!UICONTROL Configure]** é aberta. Forneça um **[!UICONTROL Recipe Name]** apropriado, por exemplo, &quot;receita de vendas de varejo&quot; e, opcionalmente, forneça uma descrição ou um URL de documentação. Depois de concluir, clique em **[!UICONTROL Next]**.

![](../images/models-recipes/package-source-files/configure.png)

Selecione o *Tempo de Execução* apropriado e escolha um **[!UICONTROL Classification]** para *Tipo*. As credenciais do Registro do Contêiner do Azure são geradas após a conclusão.

>[!NOTE]
>
>** Tipo é a classe de problema de aprendizado de máquina para a qual a receita foi projetada e é usada após o treinamento para ajudar a avaliar a execução do treinamento.

>[!TIP]
>
>- Para [!DNL Python] receitas, selecione o **[!UICONTROL Python]** tempo de execução.
>- Para receitas R, selecione o tempo de execução **[!UICONTROL R]**.
>- Para fórmulas PySpark, selecione o tempo de execução **[!UICONTROL PySpark]**. Um tipo de artefato é preenchido automaticamente.
>- Para fórmulas Scala, selecione o tempo de execução **[!UICONTROL Spark]**. Um tipo de artefato é preenchido automaticamente.


![](../images/models-recipes/package-source-files/docker-creds.png)

Observe os valores para Host Docker, nome de usuário e senha. Eles são usados para criar e mover sua imagem [!DNL Docker] nos fluxos de trabalho descritos abaixo.

>[!NOTE]
>
>O URL de origem é fornecido após concluir as etapas descritas abaixo. O arquivo de configuração é explicado em tutoriais subsequentes encontrados em [próximas etapas](#next-steps).

### Compacte os arquivos de origem

Comece obtendo a base de código de amostra encontrada no repositório <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Experience Platform Data Science Workspace Reference</a>.

- [Criar imagem do Docker Python](#python-docker)
- [Criar imagem Docker R](#r-docker)
- [Criar imagem do Docker PySpark](#pyspark-docker)
- [Criar imagem do Docker Scala (Spark)](#scala-docker)

### Criar [!DNL Python] Imagem do Docker {#python-docker}

Se ainda não tiver feito isso, clone o repositório [!DNL GitHub] no sistema local com o seguinte comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue até o diretório `experience-platform-dsw-reference/recipes/python/retail`. Aqui, você encontrará os scripts `login.sh` e `build.sh` usados para fazer logon no Docker e criar a imagem [!DNL Python Docker]. Se você tiver suas [credenciais do Docker](#docker-based-model-authoring) prontas, insira os seguintes comandos em ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Observe que, ao executar o script de login, você precisa fornecer o host do Docker, nome de usuário e senha. Ao criar, é necessário fornecer o host Docker e uma tag de versão para a build.

Quando o script de compilação for concluído, você receberá um URL de arquivo de origem Docker na saída do console. Para este exemplo específico, será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copie esse URL e vá para as [próximas etapas](#next-steps).

### Criar imagem R [!DNL Docker] {#r-docker}

Se ainda não tiver feito isso, clone o repositório [!DNL GitHub] no sistema local com o seguinte comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue até o diretório `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` dentro do repositório clonado. Aqui, você encontrará os arquivos `login.sh` e `build.sh` que usará para fazer logon no Docker e para criar a imagem R Docker. Se você tiver suas [credenciais do Docker](#docker-based-model-authoring) prontas, insira os seguintes comandos em ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Observe que, ao executar o script de login, você precisa fornecer o host do Docker, nome de usuário e senha. Ao criar, é necessário fornecer o host Docker e uma tag de versão para a build.

Quando o script de compilação for concluído, você receberá um URL de arquivo de origem Docker na saída do console. Para este exemplo específico, será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copie esse URL e vá para as [próximas etapas](#next-steps).

### Criar imagem do Docker PySpark {#pyspark-docker}

Comece clonando o repositório [!DNL GitHub] em seu sistema local com o seguinte comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue até o diretório `experience-platform-dsw-reference/recipes/pyspark/retail`. Os scripts `login.sh` e `build.sh` estão localizados aqui e são usados para fazer logon no Docker e para criar a imagem do Docker. Se você tiver suas [credenciais do Docker](#docker-based-model-authoring) prontas, insira os seguintes comandos em ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Observe que, ao executar o script de login, você precisa fornecer o host do Docker, nome de usuário e senha. Ao criar, é necessário fornecer o host Docker e uma tag de versão para a build.

Quando o script de compilação for concluído, você receberá um URL de arquivo de origem Docker na saída do console. Para este exemplo específico, será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Copie esse URL e vá para as [próximas etapas](#next-steps).

### Criar imagem do Docker Scala {#scala-docker}

Comece clonando o repositório [!DNL GitHub] em seu sistema local com o seguinte comando no terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Em seguida, navegue até o diretório `experience-platform-dsw-reference/recipes/scala`, onde é possível encontrar os scripts `login.sh` e `build.sh`. Esses scripts são usados para fazer logon no Docker e criar a imagem Docker. Se você tiver suas [credenciais do Docker](#docker-based-model-authoring) prontas, insira os seguintes comandos para terminal em ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Se você estiver recebendo um erro de permissão ao tentar fazer logon no Docker usando o script `login.sh`, tente usar o comando `bash login.sh`.

Ao executar o script de login, você precisa fornecer o host do Docker, nome de usuário e senha. Ao criar, é necessário fornecer o host Docker e uma tag de versão para a build.

Quando o script de compilação for concluído, você receberá um URL de arquivo de origem Docker na saída do console. Para este exemplo específico, será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copie esse URL e vá para as [próximas etapas](#next-steps).

## Próximas etapas {#next-steps}

Este tutorial foi empacotando arquivos de origem em uma Receita, a etapa de pré-requisito para importar uma Receita em [!DNL Data Science Workspace]. Agora, você deve ter uma imagem do Docker no Registro do Contêiner do Azure junto com o URL da imagem correspondente. Agora você está pronto para iniciar o tutorial sobre importação de uma receita empacotada para [!DNL Data Science Workspace]. Selecione um dos links tutoriais abaixo para começar:

- [Importar uma Receita empacotada na interface do usuário](./import-packaged-recipe-ui.md)
- [Importar uma Receita empacotada usando a API](./import-packaged-recipe-api.md)
