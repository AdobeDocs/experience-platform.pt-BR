---
keywords: Experience Platform;package source files;Data Science Workspace;popular topics
solution: Experience Platform
title: Empacotar arquivos de origem em uma fórmula
topic: Tutorial
translation-type: tm+mt
source-git-commit: 91c7b7e285a4745da20ea146f2334510ca11b994

---


# Empacotar arquivos de origem em uma fórmula

Este tutorial fornece instruções sobre como disponibilizar os arquivos de origem de amostra de Vendas de varejo fornecidos em um arquivo de arquivamento, que pode ser usado para criar uma fórmula na Adobe Experience Platform Data Science Workspace seguindo o fluxo de trabalho de importação da fórmula na interface do usuário ou usando a API.

Conceitos para entender:

- **Receitas**: Uma fórmula é o termo da Adobe para uma especificação de Modelo e é um container de nível superior que representa um aprendizado de máquina específico, algoritmo de inteligência artificial ou conjunto de algoritmos, lógica de processamento e configuração necessários para criar e executar um modelo treinado e, portanto, ajudar a resolver problemas específicos da empresa.
- **Arquivos** de origem: Arquivos individuais em seu projeto que contêm a lógica de uma fórmula.

## Pré-requisitos

- [Docker](https://docs.docker.com/install/#supported-platforms)
- [Python 3 e pip](https://docs.conda.io/en/latest/miniconda.html)
- [Scala](https://www.scala-sbt.org/download.html?_ga=2.42231906.690987621.1558478883-2004067584.1558478883)
- [Maven](https://maven.apache.org/install.html)

## Criação de receita

Receba start de criação com arquivos de origem de empacotamento para criar um arquivo. Os arquivos de origem definem a lógica e os algoritmos de aprendizado da máquina usados para resolver um problema específico em mãos e são escritos em Python, R, PySpark ou Scala Spark. Dependendo do idioma no qual os arquivos de origem são gravados, os arquivos de arquivamento criados serão uma imagem do Docker ou um arquivo binário. Depois de criado, o arquivo de arquivamento empacotado é importado para a Data Science Workspace para criar uma fórmula [na interface do usuário](./import-packaged-recipe-ui.md) ou [usando a API](./import-packaged-recipe-api.md).

### Criação de modelo baseado em Docker

Uma imagem do Docker permite que um desenvolvedor empacote um aplicativo com todas as partes de que precisa, como bibliotecas e outras dependências, e envie-o como um pacote.

A imagem do Docker criada será encaminhada para o Registro de Container do Azure usando as credenciais fornecidas a você durante o fluxo de trabalho de criação da fórmula.

>[!NOTE] Somente os arquivos de origem gravados no **Python**, **R** e **Tensorflow** exigem credenciais do Registro de Container do Azure.

Para obter suas credenciais do Registro de Container do Azure, faça logon na <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a>. Na coluna de navegação esquerda, navegue até **Workflows**. Selecione **Importar receita do arquivo** de origem e **Iniciar** um novo procedimento de importação. Consulte a captura de tela abaixo para obter referência.

![](../images/models-recipes/package-source-files/workflow_ss.png)

Forneça um Nome **de** Receita apropriado, por exemplo, &quot;Fórmula de Vendas de Varejo&quot; e, opcionalmente, forneça uma descrição ou um URL de documentação. Depois de concluído, clique em **Avançar**.

![](../images/models-recipes/package-source-files/recipe_info.png)

Selecione o **Tempo** de execução apropriado e escolha **Classificação** para **Tipo**. Suas credenciais do Registro de Container do Azure serão geradas.

![](../images/models-recipes/package-source-files/recipe_workflow_recipe_source.png)

Observe os valores para Host **do** Docker, **Nome** de usuário e **Senha**. Eles serão usados mais tarde para criar e encaminhar sua imagem do Docker.

Depois de enviado, você e outros usuários podem acessar a imagem via URL. O campo Arquivo **de** origem espera esse URL como uma entrada.

### Criação de modelo com base em binários

Para arquivos de origem gravados em Scala ou PySpark, um arquivo binário será gerado. A criação do arquivo binário é tão simples quanto executar o script de compilação fornecido.
>[!NOTE] Somente os arquivos de origem gravados no ScalaSpark ou no PySpark gerarão um arquivo binário ao executar o script de compilação.

### Empacotar os arquivos de origem

Start obtendo a base de códigos de amostra encontrada no repositório de referência <a href="https://github.com/adobe/experience-platform-dsw-reference" target="_blank">da</a> Experience Platform Data Science. Dependendo da linguagem de programação na qual os arquivos de origem de amostra estão gravados, a criação de seus respectivos arquivos de arquivamento difere no procedimento.

- [Criar imagem do Docker Python](#build-python-docker-image)
- [Imagem do Docker Build R](#build-r-docker-image)
- [Criar binários do PySpark](#build-pyspark-binaries)
- [Criar binários Scala](#build-scala-binaries)

#### Criar imagem do Docker Python

Se você não tiver feito isso, clone o repositório github no sistema local com o seguinte comando:

```shell
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navigate to the directory `experience-platform-dsw-reference/recipes/python/retail`. Aqui, você encontrará os scripts `login.sh` e os `build.sh` quais usará para fazer logon no Docker e para criar a imagem python Docker. Se as credenciais [do](#docker-based-model-authoring) Docker estiverem prontas, digite os seguintes comandos na ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for building Docker image
./build.sh
```

Observe que ao executar o script de login, você precisará fornecer o host do Docker, o nome de usuário e a senha. Ao criar, é necessário fornecer o host do Docker e uma tag de versão para a compilação.

Quando o script de compilação for concluído, você receberá um URL de arquivo de origem do Docker na saída do console. Para este exemplo específico, ele será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retailsales-python:{VERSION_TAG}
```

Copie esse URL e siga para as [próximas etapas](#next-steps).

#### Imagem do Docker Build R

Se você não tiver feito isso, clone o repositório github no sistema local com o seguinte comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue até o diretório `experience-platform-dsw-reference/recipes/R/Retail - GradientBoosting` dentro do repositório clonado. Aqui, você encontrará os arquivos `login.sh` e `build.sh` os quais usará para fazer logon no Docker e para criar a imagem do R Docker. Se as credenciais [do](#docker-based-model-authoring) Docker estiverem prontas, digite os seguintes comandos na ordem:

```BASH
# for logging in to Docker
./login.sh
 
# for build Docker image
./build.sh
```

Observe que ao executar o script de login, você precisará fornecer o host do Docker, o nome de usuário e a senha. Ao criar, é necessário fornecer o host do Docker e uma tag de versão para a compilação.

Quando o script de compilação for concluído, você receberá um URL de arquivo de origem do Docker na saída do console. Para este exemplo específico, ele será semelhante a:

```BASH
# URL format: 
{DOCKER_HOST}/ml-retail-r:{VERSION_TAG}
```

Copie esse URL e siga para as [próximas etapas](#next-steps).

#### Criar binários do PySpark

Se você não tiver feito isso, clone o repositório github no sistema local com o seguinte comando:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Navegue até o repositório clonado no sistema local e execute os seguintes comandos para criar o arquivo necessário `.egg` para importar uma receita do PySpark:

```BASH
cd recipes/pyspark
./build.sh
```

O `.egg` arquivo é gerado na `dist` pasta.

Agora você pode seguir para as [próximas etapas](#next-steps).

#### Criar binários Scala

Se você ainda não tiver feito isso, execute o seguinte comando para clonar o repositório Github para seu sistema local:

```BASH
git clone https://github.com/adobe/experience-platform-dsw-reference.git
```

Para criar o `.jar` artefato usado para importar uma receita do Scala, navegue até o repositório clonado e siga as etapas abaixo:

```BASH
cd recipes/scala/
./build.sh
```

O `.jar` artefato gerado com dependências é encontrado no `/target` diretório.

Agora você pode seguir para as [próximas etapas](#next-steps).

## Próximas etapas

Este tutorial passou do empacotamento de arquivos de origem para uma Receita, a etapa pré-requisito para importar uma Receita na Área de trabalho da Data Science. Agora você deve ter uma imagem do Docker no Registro de Container do Azure junto com o URL de imagem correspondente ou um arquivo binário armazenado localmente no seu sistema de arquivos. Agora você está pronto para iniciar o tutorial sobre como **Importar uma receita empacotada para a Data Science Workspace**. Selecione um dos links do tutorial abaixo para começar.

- [Importar uma receita empacotada na interface do usuário](./import-packaged-recipe-ui.md)
- [Importar uma Receita empacotada usando a API](./import-packaged-recipe-api.md)