---
solution: Experience Platform
title: Gerar dados de amostra para um esquema XDM na interface do usuário
description: Saiba como gerar dados JSON de amostra com base em um esquema existente na interface do usuário do Adobe Experience Platform.
topic-legacy: user guide
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: d380b4d2a75efb1c34010a30c619649a7b99643c
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Gerar dados de amostra para um esquema XDM na interface do usuário

Para assimilar dados no Adobe Experience Platform, o formato e a estrutura dos dados devem estar em conformidade com um esquema do Experience Data Model (XDM) existente. Dependendo da complexidade do esquema para um conjunto de dados específico, pode ser difícil determinar a forma exata dos dados que o conjunto de dados espera ao assimilar.

Para qualquer esquema definido na interface do usuário do Experience Platform, você pode gerar um objeto JSON de amostra que esteja em conformidade com a estrutura do esquema. Esse objeto pode servir como template para qualquer dado assimilado em conjuntos de dados que empregam o schema em questão.

Na interface do usuário da plataforma, selecione **[!UICONTROL Esquemas]** no painel de navegação esquerdo. Em **[!UICONTROL Procurar]** localize o schema para o qual deseja gerar dados de amostra. Selecione-o na lista e o painel direito é atualizado para mostrar detalhes sobre o esquema. Aqui, selecione **[!UICONTROL Baixar arquivo de amostra]**.

![](../images/ui/sample/sample-data.png)

Um exemplo de arquivo JSON é baixado pelo navegador. Agora você pode usar esse arquivo como referência para estruturar seus dados ao assimilar em conjuntos de dados que empregam esse esquema.

## Próximas etapas

Este guia cobriu como gerar um arquivo JSON de amostra de um esquema XDM na interface do usuário da plataforma. Para saber como gerar dados de amostra usando a API do Registro de Schema, consulte o [guia do endpoint de dados de exemplo](../api/sample-data.md).

Quando estiver pronto para começar a assimilar dados, consulte o tutorial em [mapeamento de um arquivo CSV para XDM](../../ingestion/tutorials/map-csv/overview.md) para saber como mapear um arquivo de dados simples (como um CSV) para um esquema XDM e assimilá-lo na plataforma. Como alternativa, você pode estabelecer uma [conexão de origem](../../sources/home.md) para trazer seus dados de uma fonte externa e mapeá-los para XDM.

Para obter mais informações sobre os recursos da [!UICONTROL Esquemas] na interface do usuário, consulte o [[!UICONTROL Esquemas] visão geral do espaço de trabalho](./overview.md).
