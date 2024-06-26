---
keywords: Experience Platform;modelo de aprendizado de máquina;Espaço de trabalho de ciência de dados;tópicos populares;criar e publicar um modelo
solution: Experience Platform
title: Criar e publicar um modelo de aprendizado de máquina
type: Tutorial
description: O guia a seguir descreve as etapas necessárias para criar e publicar um modelo de aprendizado de máquina.
exl-id: f71e5a17-9952-411e-8e6a-aab46bc4c006
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '1074'
ht-degree: 0%

---


# Criar e publicar um modelo de aprendizado de máquina

O guia a seguir descreve as etapas necessárias para criar e publicar um modelo de aprendizado de máquina. Cada seção contém uma descrição do que será feito e um link para a interface do usuário e a documentação da API para executar a etapa descrita.

## Introdução

Antes de iniciar este tutorial, você deve ter os seguintes pré-requisitos:

- Acesso a [!DNL Adobe Experience Platform]. Se você não tiver acesso a uma organização no [!DNL Experience Platform], entre em contato com o administrador do sistema antes de continuar.

- Todos os tutoriais do Data Science Workspace usam o modelo de propensão Luma. Para acompanhar, você deve ter criado o [Esquemas e conjuntos de dados do modelo de propensão Luma](./create-luma-data.md).

### Explore os dados e entenda os esquemas

Efetue logon no [Adobe Experience Platform](https://platform.adobe.com/) e selecione **[!UICONTROL Conjuntos de dados]** para listar todos os conjuntos de dados existentes e selecionar o conjunto de dados que deseja explorar. Nesse caso, você deve selecionar o **Dados da Web do Luma** conjunto de dados.

![selecionar conjunto de dados da Web do Luma](../images/models-recipes/model-walkthrough/luma-dataset.png)

A página de atividade do conjunto de dados é aberta, listando as informações relacionadas ao seu conjunto de dados. É possível selecionar **[!UICONTROL Visualizar conjunto de dados]** próximo ao canto superior direito para examinar registros de amostra. Também é possível visualizar o esquema do conjunto de dados selecionado.

![visualizar dados da Web do Luma](../images/models-recipes/model-walkthrough/preview-dataset.png)

Selecione o link do esquema no painel direito. Um popover é exibido, selecionando o link em **[!UICONTROL nome do esquema]** abre o schema em uma nova guia.

![visualizar o esquema de dados da web do luma](../images/models-recipes/model-walkthrough/preview-schema.png)

Você pode explorar mais os dados usando o bloco de anotações da Análise de Dados Exploratórios (EDA) fornecido. Esse bloco de notas pode ser usado para ajudar a entender os padrões nos dados do Luma, verificar a integridade dos dados e resumir os dados relevantes para o modelo de propensão preditiva. Para saber mais sobre a Análise de Dados Exploratórios, visite o [Documentação EDA](../jupyterlab/eda-notebook.md).

## Criar a fórmula de propensão do Luma {#author-your-model}

Um componente principal da [!DNL Data Science Workspace] O ciclo de vida envolve a criação de Receitas e Modelos. O modelo de propensão da Luma foi projetado para gerar uma previsão sobre se os clientes têm uma alta propensão para comprar um produto da Luma.

Para criar o modelo de propensão Luma, o modelo do construtor de fórmula é usado. Receitas são a base para um Modelo, pois contêm algoritmos de aprendizado de máquina e lógica projetada para resolver problemas específicos. Mais importante ainda, as receitas permitem democratizar o aprendizado de máquina em toda a organização, permitindo que outros usuários acessem um modelo para casos de uso diferentes sem escrever nenhum código.

Siga as [criar um modelo usando o JupyterLab Notebooks](../jupyterlab/create-a-model.md) tutorial para criar a fórmula do modelo de propensão Luma usada em tutoriais subsequentes.

## Importar e empacotar uma fórmula de fontes externas (*opcional*)

Se quiser importar e empacotar uma fórmula para uso no Data Science Workspace, você deve empacotar os arquivos de origem em um arquivo. Siga as [empacotar arquivos de origem em uma fórmula](./package-source-files-recipe.md) tutorial. Este tutorial mostra como empacotar arquivos de código-fonte em uma fórmula, que é a etapa de pré-requisito para importar uma fórmula para o Data Science Workspace. Depois que o tutorial for concluído, você receberá uma imagem do Docker em um Registro de contêiner do Azure, juntamente com a URL da imagem correspondente, ou seja, um arquivo morto.

Esse arquivo pode ser usado para criar uma fórmula no Data Science Workspace seguindo o fluxo de trabalho de importação da fórmula usando o [Fluxo de trabalho da interface do usuário](./import-packaged-recipe-ui.md) ou o [Fluxo de trabalho da API](./import-packaged-recipe-api.md).

## Treinar e avaliar um modelo {#train-and-evaluate-your-model}

Agora que seus dados estão preparados e uma fórmula está pronta, você tem a capacidade de criar, treinar e avaliar ainda mais seu modelo de aprendizado de máquina. Ao usar o Construtor de fórmula, você já deve ter treinado, pontuado e avaliado seu modelo antes de compactá-lo em uma fórmula.

A interface do usuário e a API do Espaço de trabalho de ciência de dados permitem publicar sua fórmula como modelo. Além disso, você pode ajustar ainda mais aspectos específicos do modelo, como adicionar, remover e alterar hiperparâmetros.

### Criar um modelo

Para saber mais sobre como criar um modelo usando a interface do usuário, visite o trem e avalie um modelo no Espaço de trabalho de ciência de dados [Tutorial de interface do usuário](./train-evaluate-model-ui.md) ou [Tutorial de API](./train-evaluate-model-api.md). Este tutorial fornece um exemplo sobre como criar, treinar e atualizar hiperparâmetros para ajustar seu modelo.

>[!NOTE]
>
> Os hiperparâmetros não podem ser aprendidos, portanto, eles devem ser atribuídos antes que ocorram execuções de treinamento. Ajustar os hiperparâmetros pode alterar a precisão do seu modelo treinado. Como a otimização de um modelo é um processo iterativo, várias execuções de treinamento podem ser necessárias antes de uma avaliação satisfatória ser alcançada.

## Pontuar um modelo {#score-a-model}

A próxima etapa na criação e publicação de um modelo é operacionalizar seu modelo para pontuar e consumir insights do data lake e do Perfil do cliente em tempo real.

A pontuação no Espaço de trabalho de ciência de dados pode ser obtida alimentando dados de entrada em um modelo treinado existente. Os resultados da pontuação são armazenados e visualizados em um conjunto de dados de saída especificado como um novo lote.

Para saber como pontuar seu modelo, visite a página pontuação de um modelo [Tutorial de interface do usuário](./score-model-ui.md) ou [Tutorial de API](./score-model-api.md).

## Publicar um modelo com pontuação como um serviço

O Data Science Workspace permite publicar seu modelo treinado como um serviço. Isso permite que os usuários em sua organização pontuem dados sem a necessidade de criar seus próprios modelos.

Para saber como publicar um modelo como um serviço, visite o [Tutorial de interface do usuário](./publish-model-service-ui.md) ou [Tutorial de API](./publish-model-service-api.md).

### Programar treinamento automatizado para um serviço

Depois de publicar um modelo como um serviço, você pode configurar a pontuação programada e as execuções de treinamento para seu serviço de aprendizado de máquina. A automatização do processo de treinamento e de pontuação pode ajudar a manter e melhorar a eficiência de um serviço ao longo do tempo, acompanhando os padrões dos seus dados. Visite o [agendar um modelo na interface do Espaço de trabalho de ciência de dados](./schedule-models-ui.md) tutorial.

>[!NOTE]
>
> Você só pode agendar um modelo para treinamento e pontuação automatizados na interface do usuário do.

## Próximas etapas {#next-steps}

Adobe Experience Platform [!DNL Data Science Workspace] O fornece as ferramentas e os recursos para criar, avaliar e utilizar modelos de aprendizado de máquina para gerar previsões e insights de dados. Quando os insights de aprendizado de máquina são assimilados em um [!DNL Profile]habilitado para, esses mesmos dados também são assimilados como [!DNL Profile] registros que podem ser segmentados usando [!DNL Adobe Experience Platform Segmentation Service].

À medida que os dados de perfil e série temporal são assimilados, o Perfil do cliente em tempo real decide automaticamente incluir ou excluir esses dados dos segmentos por meio de um processo contínuo chamado segmentação por transmissão, antes de mesclá-los com os dados existentes e atualizar a visualização de união. Como resultado, você pode realizar cálculos instantaneamente e tomar decisões para fornecer experiências aprimoradas e individualizadas aos clientes, à medida que eles interagem com sua marca.

Visite o tutorial para [enriquecendo o Perfil do cliente em tempo real com insights de aprendizado de máquina](./enrich-profile.md) para saber mais sobre como você pode utilizar insights de aprendizado de máquina.
