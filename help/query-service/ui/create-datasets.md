---
keywords: Experience Platform; home; tópicos populares; serviço de consulta; serviço de consulta; gerar conjuntos de dados; gerar conjunto de dados; criar conjunto de dados;
solution: Experience Platform
title: Gerar conjuntos de dados a partir de resultados no serviço de query
topic-legacy: queries
type: Tutorial
description: O Serviço de query do Adobe Experience Platform permite a criação de conjuntos de dados da interface do usuário. Depois que um conjunto de dados é criado, ele pode ser acessado como qualquer outro conjunto de dados no Data Lake e usado para uma variedade de casos de uso.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 0c2cfe9b0bd839bdf662622283a7563c0417c9a9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Gere conjuntos de dados a partir dos resultados em [!DNL Query Service]

[!DNL Query Service] permite usar queries para gerar conjuntos de dados no [!DNL Data Lake]. Esses conjuntos de dados podem ser usados como entrada para mais consultas ou em outros serviços, como [!DNL Data Science Workspace], Perfil do cliente em tempo real ou [!DNL Analysis Workspace].

## Gerar conjuntos de dados da interface do usuário do Adobe Experience Platform

Para criar conjuntos de dados da interface do usuário do Adobe Experience Platform, siga estas etapas:

1. Crie uma consulta usando um cliente conectado e valide a saída. Para saber como gravar consultas usando [!DNL Query Editor]leia a [!DNL Query Editor] Guia da interface do usuário [ao gravar queries](./user-guide.md#writing-queries).

2. Na interface do usuário da plataforma, navegue até **[!UICONTROL Queries]** seguido pelo **[!UICONTROL Procurar]** e selecione a query criada. Para obter mais detalhes sobre como visualizar consultas que foram criadas e salvas para sua organização na interface do usuário da plataforma, leia o [[!DNL Query Service] visão geral](./overview.md#browse).

3. No painel Detalhes da consulta , selecione **[!UICONTROL Conjunto de dados de saída]**.

   ![Selecionar conjunto de dados de saída](../images/ui/create-datasets/output-dataset.png)

4. Na caixa de diálogo exibida, insira um nome de conjunto de dados anexado a sua ID LDAP. O nome do conjunto de dados não precisa ser exclusivo ou seguro para SQL. Observe que o nome da tabela para seu conjunto de dados será gerado com base no nome do conjunto de dados que você criar aqui.

5. Em seguida, insira uma descrição para o conjunto de dados no [!UICONTROL Descrição] e selecione **[!UICONTROL Executar consulta]**.

   ![Executar consulta](../images/ui/create-datasets/run-query.png)

6. Quando a execução da consulta for concluída, navegue até **[!UICONTROL Conjuntos de dados]** para exibir o conjunto de dados criado. Para saber mais sobre como executar ações comuns ao trabalhar com conjuntos de dados na interface do usuário da plataforma, consulte o [Guia da interface do usuário de conjuntos de dados](../../catalog/datasets/user-guide.md).

Depois que um conjunto de dados é criado, ele pode ser acessado como qualquer outro conjunto de dados na [!DNL Data Lake] e utilizados para uma variedade de casos de utilização.

>[!NOTE]
>
>Em uma implementação em tempo real, você deve aplicar rótulos de Governança de dados após a criação do conjunto de dados. Para saber mais sobre como aplicar rótulos de uso de dados a conjuntos de dados, consulte o [Visão geral dos rótulos de uso de dados](../../data-governance/labels/overview.md).

## Gerar conjuntos de dados com um [!DNL Experience Data Model] schema

Use a sintaxe SQL para gerar um conjunto de dados com um [!DNL Experience Data Model] (XDM). Para obter mais informações sobre a sintaxe compatível com [!DNL Query Service]Por favor leia o [Guia de sintaxe SQL](../sql/syntax.md#create-table-as-select).

## Conjuntos de dados de saída

Os conjuntos de dados criados por meio dessa funcionalidade são gerados com um esquema ad hoc que corresponde à estrutura dos dados de saída, conforme definido na instrução SQL. Alguns serviços downstream exigem conjuntos de dados com esquemas XDM específicos. Verifique os requisitos de formatação de dados para serviços downstream antes de gravar suas consultas.

## Próximas etapas

Depois de ler este documento, você deve entender como usar [!DNL Query Service] para gerar conjuntos de dados da interface do usuário da plataforma. Para obter mais informações sobre como acessar, gravar e executar consultas na interface do usuário da plataforma, consulte o [[!DNL Query Service] Visão geral da interface do usuário](./overview.md).
