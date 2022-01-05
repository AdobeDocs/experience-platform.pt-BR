---
keywords: Experience Platform, modelo de aprendizado de máquina, Data Science Workspace, tópicos populares, criar e publicar um modelo
solution: Experience Platform
title: Criar e publicar um modelo de aprendizado de máquina
topic-legacy: tutorial
type: Tutorial
description: O guia a seguir descreve as etapas necessárias para criar e publicar um modelo de aprendizado de máquina.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: ff8a3612f34d6547577564ba40261052cd78ef01
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 0%

---


# Criar e publicar um modelo de aprendizado de máquina

O guia a seguir descreve as etapas necessárias para criar e publicar um modelo de aprendizado de máquina. Cada seção contém uma descrição do que você fará e um link para a interface do usuário e a documentação da API para executar a etapa descrita.

## Introdução

Antes de iniciar este tutorial, você deve ter os seguintes pré-requisitos:

- Acesso ao [!DNL Adobe Experience Platform]. Se você não tiver acesso a uma Organização IMS no [!DNL Experience Platform], fale com o administrador do sistema antes de continuar.

- Todos os tutoriais do Data Science Workspace usam o modelo de propensão Luma. Para continuar, você deve ter criado a variável [Schemas e conjuntos de dados do modelo de propensão do Luma](./create-luma-data.md).

### Explorar os dados e entender os esquemas

Faça logon em [Adobe Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Conjuntos de dados]** para listar todos os conjuntos de dados existentes e selecionar o conjunto de dados que deseja explorar. Nesse caso, você deve selecionar a variável **Dados da Web do Luma** conjunto de dados.

![selecione o conjunto de dados da Web Luma](../images/models-recipes/model-walkthrough/luma-dataset.png)

A página de atividade do conjunto de dados é aberta, listando as informações relacionadas ao conjunto de dados. Você pode selecionar **[!UICONTROL Visualizar conjunto de dados]** perto do canto superior direito para examinar os registros de amostra. Você também pode exibir o esquema do conjunto de dados selecionado.

![visualizar dados da Web do Luma](../images/models-recipes/model-walkthrough/preview-dataset.png)

Selecione o link do schema no painel direito. Uma energia é exibida, selecionando o link em **[!UICONTROL nome do schema]** abre o schema em uma nova guia.

![visualização do schema de dados da web luma](../images/models-recipes/model-walkthrough/preview-schema.png)

Você pode explorar mais os dados usando o notebook EDA (Exploratory Data Analysis) fornecido. Este notebook pode ser usado para ajudar a entender os padrões nos dados do Luma, verificar a integridade dos dados e resumir os dados relevantes para o modelo de propensão preditiva. Para saber mais sobre a Análise de dados exploratória, visite o [Documentação EDA](../jupyterlab/eda-notebook.md).

## Criar a receita de propensão do Luma {#author-your-model}

Um componente principal da variável [!DNL Data Science Workspace] o ciclo de vida envolve a criação de Fórmulas e Modelos. O modelo de propensão do Luma foi projetado para gerar uma previsão sobre se os clientes têm alta propensão a comprar um produto do Luma.

Para criar o modelo de propensão de Luma, o modelo do construtor de receita é usado. As receitas são a base de um Modelo, pois contêm algoritmos e lógica de aprendizado de máquina projetados para resolver problemas específicos. Mais importante, as Receitas capacitam você a democratizar o aprendizado de máquina em sua organização, permitindo que outros usuários acessem um Modelo para casos de uso diferentes sem gravar nenhum código.

Siga as [criar um modelo usando notebooks JupyterLab](../jupyterlab/create-a-model.md) tutorial para criar a fórmula do modelo de propensão do Luma, usada em tutoriais subsequentes.

## Importar e empacotar uma receita de fontes externas (*opcional*)

Se quiser importar e empacotar uma receita para uso no Data Science Workspace, deverá empacotar seus arquivos de origem em um arquivo de arquivamento. Siga as [arquivos de origem do pacote em uma receita](./package-source-files-recipe.md) tutorial. Este tutorial mostra como empacotar arquivos de origem em uma receita, que é a etapa prévia para importar uma receita no Data Science Workspace. Quando o tutorial for concluído, você receberá uma imagem Docker em um Registro do Contêiner do Azure, juntamente com a URL de imagem correspondente, em outras palavras, um arquivo de arquivamento.

Esse arquivo pode ser usado para criar uma receita no Data Science Workspace seguindo o fluxo de trabalho de importação da receita usando o [Fluxo de trabalho da interface do usuário](./import-packaged-recipe-ui.md) ou [Fluxo de trabalho da API](./import-packaged-recipe-api.md).

## Comboio e avaliação de um modelo {#train-and-evaluate-your-model}

Agora que seus dados estão preparados e uma receita está pronta, você tem a capacidade de criar, treinar e avaliar seu modelo de aprendizado de máquina ainda mais. Ao usar o Construtor de receita, você já deve ter treinado, classificado e avaliado seu modelo antes de empacotá-lo em uma receita.

A interface do usuário e a API do Data Science Workspace permitem publicar sua receita como modelo. Além disso, você pode aprimorar aspectos específicos do modelo, como adicionar, remover e alterar hiperparâmetros.

### Criar um modelo

Para saber mais sobre como criar um modelo usando a interface do usuário, visite o trem e avalie um modelo no Data Science Workspace [Tutorial da interface do usuário](./train-evaluate-model-ui.md) ou [Tutorial de API](./train-evaluate-model-api.md). Este tutorial fornece um exemplo de como criar, treinar e atualizar hiperparâmetros para ajustar o modelo.

>[!NOTE]
>
> Os hiperparâmetros não podem ser aprendidos, portanto, devem ser atribuídos antes que as execuções de treinamento ocorram. Ajustar hiperparâmetros pode alterar a precisão do modelo treinado. Uma vez que a otimização de um modelo é um processo iterativo, poderão ser necessárias várias ações de formação antes de se obter uma avaliação satisfatória.

## Pontuar um modelo {#score-a-model}

A próxima etapa na criação e publicação de um modelo é operacionalizar seu modelo para pontuar e consumir insights do lago de dados e do Perfil do cliente em tempo real.

A pontuação no Data Science Workspace pode ser obtida ao alimentar os dados de entrada em um Modelo treinado existente. Os resultados da pontuação são armazenados e visualizados em um conjunto de dados de saída especificado como um novo lote.

Para saber como pontuar seu modelo, visite a pontuação de um modelo [Tutorial da interface do usuário](./score-model-ui.md) ou [Tutorial de API](./score-model-api.md).

## Publicar um modelo com pontuação como um serviço

O Data Science Workspace permite publicar seu modelo treinado como um serviço. Isso permite que os usuários em sua Organização IMS marquem dados sem a necessidade de criar seus próprios modelos.

Para saber como publicar um modelo como um serviço, visite o [Tutorial da interface do usuário](./publish-model-service-ui.md) ou [Tutorial de API](./publish-model-service-api.md).

### Programar treinamento automatizado para um serviço

Depois de publicar um modelo como um serviço, você pode configurar execuções programadas de pontuação e treinamento para seu serviço de aprendizado de máquina. A automatização do processo de treinamento e pontuação pode ajudar a manter e melhorar a eficiência de um serviço ao longo do tempo, mantendo os padrões em seus dados. Visite o [agendar um modelo na interface do usuário do Data Science Workspace](./schedule-models-ui.md) tutorial.

>[!NOTE]
>
> Você só pode agendar um modelo para treinamento automatizado e pontuação na interface do usuário.

## Próximas etapas {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] O fornece as ferramentas e os recursos para criar, avaliar e utilizar modelos de aprendizado de máquina para gerar previsões e insights de dados. Quando os insights de aprendizado de máquina são assimilados em um [!DNL Profile]conjunto de dados habilitado para , que os mesmos dados também sejam assimilados como [!DNL Profile] registros que podem então ser segmentados usando [!DNL Adobe Experience Platform Segmentation Service].

Conforme os dados do perfil e da série de tempo são assimilados, o Perfil do cliente em tempo real decide automaticamente incluir ou excluir esses dados dos segmentos por meio de um processo contínuo chamado de segmentação de fluxo, antes de mesclá-los com os dados existentes e atualizar a visualização da união. Como resultado, você pode executar instantaneamente os cálculos e tomar decisões para oferecer experiências aprimoradas e individualizadas aos clientes, à medida que eles interagem com a sua marca.

Visite o tutorial para [enriquecimento do Perfil do cliente em tempo real com insights de aprendizado de máquina](./enrich-profile.md) para saber mais sobre como você pode utilizar insights de aprendizado de máquina.
