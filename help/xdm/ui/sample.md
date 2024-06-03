---
solution: Experience Platform
title: Gerar dados de amostra para um esquema XDM na interface do
description: Saiba como gerar dados JSON de amostra com base em um esquema existente na interface do usuário do Adobe Experience Platform.
exl-id: e60eedb2-2245-42cd-b574-43caf9e3426c
source-git-commit: 19a9341a9f53559fe3f619b2f157015e53b25b64
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 1%

---

# Gerar dados de amostra para um esquema XDM na interface do {#generate-sample-data-for-an-xdm-schema}

>[!CONTEXTUALHELP]
>id="platform_xdm_downloadsamplefile"
>title="Baixar arquivo de amostra"
>abstract="Gere um objeto JSON de amostra que esteja em conformidade com a estrutura do esquema escolhido. Esse objeto pode servir como modelo para garantir que os dados estejam formatados corretamente para assimilação em conjuntos de dados que utilizam esse esquema. O arquivo JSON de amostra será baixado pelo seu navegador."

Para assimilar dados na Adobe Experience Platform, o formato e a estrutura dos dados devem estar em conformidade com um esquema existente do Experience Data Model (XDM). Dependendo da complexidade do esquema para um conjunto de dados específico, pode ser difícil determinar a forma exata dos dados que o conjunto de dados espera após a assimilação.

Para qualquer esquema definido na interface do usuário do Experience Platform, você pode gerar um objeto JSON de amostra que esteja em conformidade com a estrutura do esquema. Esse objeto pode servir como modelo para quaisquer dados assimilados em conjuntos de dados que utilizam o esquema em questão.

Na interface do usuário da Platform, selecione **[!UICONTROL Esquemas]** no painel de navegação esquerdo. No **[!UICONTROL Procurar]** localize o esquema para o qual deseja gerar dados de amostra. Selecione-a na lista e o painel direito é atualizado para mostrar detalhes sobre o esquema. Aqui, selecione **[!UICONTROL Baixar arquivo de amostra]**.

![A guia Procurar do espaço de trabalho Esquemas com um esquema selecionado e o arquivo de amostra de download destacado.](../images/ui/sample/sample-data.png)

Um exemplo de arquivo JSON é baixado pelo navegador. Agora você pode usar esse arquivo como uma referência para estruturar seus dados ao assimilar em conjuntos de dados que empregam esse esquema.

## Próximas etapas

Este guia abordou como gerar um arquivo JSON de amostra de um esquema XDM na interface do usuário da plataforma. Para saber como gerar dados de amostra usando a API do registro de esquema, consulte a [exemplo de manual de endpoint de dados](../api/sample-data.md).

Quando estiver pronto para começar a assimilar dados, consulte o tutorial sobre [mapeamento de um arquivo CSV para XDM](../../ingestion/tutorials/map-csv/overview.md) para saber como mapear um arquivo de dados simples (como um CSV) para um esquema XDM e assimilá-lo na Platform. Como alternativa, você pode estabelecer uma [conexão de origem](../../sources/home.md) para trazer seus dados de uma fonte externa e mapeá-los para o XDM.

Para obter mais informações sobre os recursos do [!UICONTROL Esquemas] na interface do usuário, consulte a seção [[!UICONTROL Esquemas] visão geral do espaço de trabalho](./overview.md).
