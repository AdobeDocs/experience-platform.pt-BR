---
solution: Experience Platform
title: Gerar dados de amostra para um Schema XDM na interface do usuário
description: Saiba como gerar dados JSON de amostra com base em um schema existente na interface do usuário do Adobe Experience Platform.
topic: user guide
translation-type: tm+mt
source-git-commit: 87497ef8a0ebf8de8b6c2dff1650c0b982299e8a
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---


# Gerar dados de amostra para um schema XDM na interface do usuário

Para assimilar dados no Adobe Experience Platform, o formato e a estrutura dos dados devem estar em conformidade com um schema do Modelo de Dados de Experiência (XDM) existente. Dependendo da complexidade do schema para um conjunto de dados específico, pode ser difícil determinar a forma exata dos dados que o conjunto de dados espera ao ingerir.

Para qualquer schema definido na interface do usuário do Experience Platform, é possível gerar um objeto JSON de amostra que esteja em conformidade com a estrutura do schema. Esse objeto pode servir de modelo para quaisquer dados ingeridos em conjuntos de dados que empregam o schema em questão.

Na interface do usuário da plataforma, selecione **[!UICONTROL Schemas]** no painel de navegação esquerdo. Na guia **[!UICONTROL Procurar]**, localize o schema para o qual deseja gerar dados de amostra. Selecione-o na lista e o painel direito é atualizado para mostrar detalhes sobre o schema. Aqui, selecione **[!UICONTROL Baixar arquivo de amostra].**

![](../images/ui/sample/sample-data.png)

Um arquivo JSON de amostra é baixado pelo navegador. Agora você pode usar esse arquivo como referência para estruturar seus dados ao ingressar em conjuntos de dados que utilizam esse schema.

## Próximas etapas

Este guia aborda como gerar um arquivo JSON de amostra a partir de um schema XDM na interface do usuário da plataforma. Para saber como gerar dados de amostra usando a API do Registro do Schema, consulte o [guia do endpoint de dados de amostra](../api/sample-data.md).

Quando estiver pronto para a assimilação de dados em start, consulte o tutorial em [mapeamento de um arquivo CSV para XDM](../../ingestion/tutorials/map-a-csv-file.md) para saber como mapear um arquivo de dados simples (como um CSV) para um schema XDM e assimilá-lo à Plataforma. Como alternativa, você pode estabelecer uma [conexão de origem](../../sources/home.md) para trazer seus dados de uma fonte externa e mapeá-los para XDM.

Para obter mais informações sobre os recursos do espaço de trabalho [!UICONTROL Schemas] na interface do usuário, consulte [[!UICONTROL Schemas] visão geral do espaço de trabalho](./overview.md).