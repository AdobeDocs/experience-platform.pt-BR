---
keywords: Experience Platform;arquivos de origem de pacote;Data Science Workspace;tópicos populares;Docker;imagem docker
solution: Experience Platform
title: Compactar arquivos de origem em uma fórmula
type: Tutorial
description: Este tutorial fornece instruções sobre como empacotar os arquivos de origem de amostra de Vendas de varejo em um arquivo, que pode ser usado para criar uma fórmula no Adobe Experience Platform Data Science Workspace seguindo o fluxo de trabalho de importação da fórmula na interface ou usando a API.
exl-id: 199b8127-4f1b-43a4-82e6-58cb70fcdc08
source-git-commit: 86e6924078c115fb032ce39cd678f1d9c622e297
workflow-type: tm+mt
source-wordcount: '1159'
ht-degree: 0%

---

# Compactar arquivos de origem em uma fórmula

Este tutorial fornece instruções sobre como empacotar os arquivos de origem de amostra de Vendas de varejo em um arquivo, que pode ser usado para criar uma fórmula no Adobe Experience Platform [!DNL Data Science Workspace] seguindo o fluxo de trabalho de importação de fórmula na interface ou usando a API.

Conceitos a entender:

- **Receitas**: Uma fórmula é um termo de Adobe para uma especificação de Modelo e é um contêiner de nível superior que representa um aprendizado de máquina específico, algoritmo de inteligência artificial ou conjunto de algoritmos, lógica de processamento e configuração necessários para criar e executar um modelo treinado e, portanto, ajudar a resolver problemas comerciais específicos.
- **Arquivos de origem**: arquivos individuais no projeto que contêm a lógica de uma fórmula.

## Pré-requisitos

- [[!DNL Docker]](https://docs.docker.com/install/#supported-platforms)
- [[!DNL Python 3 and pip]](https://docs.conda.io/en/latest/miniconda.html)
- [[!DNL Scala]](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [[!DNL Maven]](https://maven.apache.org/install.html)

## Criação de fórmula

A criação de fórmula começa com o empacotamento de arquivos de origem para criar um arquivo de arquivamento. Os arquivos de origem definem a lógica e os algoritmos de aprendizado de máquina usados para resolver um problema específico em andamento, e são gravados em [!DNL Python], R, PySpark ou Scala. Os arquivos de arquivamento criados assumem a forma de uma imagem do Docker. Depois de criado, o arquivo compactado é importado para o [!DNL Data Science Workspace] para criar uma fórmula [na interface](./import-packaged-recipe-ui.md) ou [uso da API](./import-packaged-recipe-api.md).

### Criação de modelo baseado no Docker {#docker-based-model-authoring}

Uma imagem Docker permite que um desenvolvedor empacote um aplicativo com todas as partes necessárias, como bibliotecas e outras dependências, e o envie como um pacote.

A imagem do Docker criada é enviada para o Registro de Contêineres do Azure usando as credenciais fornecidas durante o fluxo de trabalho de criação da fórmula.

Para obter as credenciais do Registro de Contêineres do Azure, faça logon no [Adobe Experience Platform](https://platform.adobe.com). Na coluna de navegação à esquerda, navegue até **[!UICONTROL Fluxos de trabalho]**. Selecionar **[!UICONTROL Importar fórmula]** seguido pela seleção **[!UICONTROL Launch]**. Consulte a captura de tela abaixo para referência.

![](../images/models-recipes/package-source-files/import.png)

A variável **[!UICONTROL Configurar]** é aberta. Fornecer uma **[!UICONTROL Nome da fórmula]**, por exemplo, &quot;Receita de vendas de varejo&quot; e, opcionalmente, forneça uma descrição ou URL da documentação. Após a conclusão, clique em **[!UICONTROL Próxima]**.

![](../images/models-recipes/package-source-files/configure.png)

Selecione o apropriado *Tempo de execução*, em seguida, escolha um **[!UICONTROL Classificação]** para *Tipo*. Suas credenciais do Registro do Azure Container são geradas após a conclusão.

>[!NOTE]
>
>*Tipo* é a classe de problema de aprendizado de máquina para a qual a fórmula foi projetada e é usada após o treinamento para ajudar a adaptar a avaliação da execução do treinamento.

>[!TIP]
>
>- Para [!DNL Python] receitas selecione a **[!UICONTROL Python]** tempo de execução.
>- Para receitas R, selecione a **[!UICONTROL R]** tempo de execução.
>- Para receitas do PySpark, selecione o **[!UICONTROL PySpark]** tempo de execução. Um tipo de artefato é preenchido automaticamente.
>- Para receitas Scala, selecione a opção **[!UICONTROL Spark]** tempo de execução. Um tipo de artefato é preenchido automaticamente.


![](../images/models-recipes/package-source-files/docker-creds.png)

Observe os valores para o host Docker, nome de usuário e senha. Eles são usados para criar e enviar seu [!DNL Docker] nos fluxos de trabalho descritos abaixo.

>[!NOTE]
>
>O URL de origem é fornecido após a conclusão das etapas descritas abaixo. O arquivo de configuração é explicado em tutoriais subsequentes encontrados em [próximas etapas](#next-steps).

### Compactar os arquivos de origem

Comece obtendo a base de código de amostra encontrada no <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">Referência do Experience Platform Data Science Workspace</a> repositório.

- [Criar imagem do Python Docker](#python-docker)
- [Criar imagem do R Docker](#r-docker)
- [Criar imagem do PySpark Docker](#pyspark-docker)
- [Criar imagem do Docker Scala (Spark)](#scala-docker)

### Build [!DNL Python] Imagem do Docker {#python-docker}

Se ainda não tiver feito isso, clone o [!DNL GitHub] repositório no sistema local com o seguinte comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue até o diretório `experience-platform-dsw-reference/recipes/python/retail`. Aqui, você encontrará os scripts `login.sh` e `build.sh` usado para fazer logon no Docker e criar o [!DNL Python Docker] imagem. Se você tiver seu [Credenciais do Docker](#docker-based-model-authoring) pronto, insira os seguintes comandos na ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Observe que, ao executar o script de login, você precisa fornecer o host Docker, o nome de usuário e a senha. Ao criar, você deve fornecer o host do Docker e uma tag de versão para o build.

Quando o script de build estiver concluído, você receberá um URL de arquivo de origem Docker na saída do console. Neste exemplo específico, será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copie este URL e vá para a página [próximas etapas](#next-steps).

### Build R [!DNL Docker] imagem {#r-docker}

Se ainda não tiver feito isso, clone o [!DNL GitHub] repositório no sistema local com o seguinte comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue até o diretório `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` no repositório clonado. Aqui, você encontrará os arquivos `login.sh` e `build.sh` que você usará para fazer logon no Docker e criar a imagem do R Docker. Se você tiver seu [Credenciais do Docker](#docker-based-model-authoring) pronto, insira os seguintes comandos na ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Observe que, ao executar o script de login, você precisa fornecer o host Docker, o nome de usuário e a senha. Ao criar, você deve fornecer o host do Docker e uma tag de versão para o build.

Quando o script de build estiver concluído, você receberá um URL de arquivo de origem Docker na saída do console. Neste exemplo específico, será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copie este URL e vá para a página [próximas etapas](#next-steps).

### Criar imagem do PySpark Docker {#pyspark-docker}

Comece clonando o [!DNL GitHub] repositório no sistema local com o seguinte comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue até o diretório `experience-platform-dsw-reference/recipes/pyspark/retail`. Os scripts `login.sh` e `build.sh` estão localizados aqui e são usados para fazer logon no Docker e criar a imagem do Docker. Se você tiver seu [Credenciais do Docker](#docker-based-model-authoring) pronto, insira os seguintes comandos na ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Observe que, ao executar o script de login, você precisa fornecer o host Docker, o nome de usuário e a senha. Ao criar, você deve fornecer o host do Docker e uma tag de versão para o build.

Quando o script de build estiver concluído, você receberá um URL de arquivo de origem Docker na saída do console. Neste exemplo específico, será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-pyspark:{VERSION_TAG}
```

Copie este URL e vá para a página [próximas etapas](#next-steps).

### Criar imagem do Scala Docker {#scala-docker}

Comece clonando o [!DNL GitHub] repositório no sistema local com o seguinte comando no terminal:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Em seguida, navegue até o diretório `experience-platform-dsw-reference/recipes/scala` onde você pode encontrar os scripts `login.sh` e `build.sh`. Esses scripts são usados para fazer logon no Docker e criar a imagem do Docker. Se você tiver seu [Credenciais do Docker](#docker-based-model-authoring) pronto, insira os seguintes comandos no terminal em ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

>[!TIP]
>
>Se você estiver recebendo um erro de permissão ao tentar fazer logon no Docker usando o `login.sh` tente usar o comando `bash login.sh`.

Ao executar o script de login, você precisa fornecer o host Docker, o nome de usuário e a senha. Ao criar, você deve fornecer o host do Docker e uma tag de versão para o build.

Quando o script de build estiver concluído, você receberá um URL de arquivo de origem Docker na saída do console. Neste exemplo específico, será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-spark:{VERSION_TAG}
```

Copie este URL e vá para a página [próximas etapas](#next-steps).

## Próximas etapas {#next-steps}

Este tutorial foi sobre o empacotamento de arquivos de origem em uma fórmula, a etapa de pré-requisito para a importação de uma fórmula para o [!DNL Data Science Workspace]. Agora você deve ter uma imagem do Docker no Registro de contêineres do Azure junto com a URL da imagem correspondente. Agora você está pronto para começar o tutorial sobre a importação de uma fórmula em pacote para o [!DNL Data Science Workspace]. Selecione um dos links de tutorial abaixo para começar:

- [Importar uma fórmula empacotada na interface do usuário](./import-packaged-recipe-ui.md)
- [Importar uma fórmula empacotada usando a API](./import-packaged-recipe-api.md)
