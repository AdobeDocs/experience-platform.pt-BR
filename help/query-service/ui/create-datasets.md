---
keywords: Experience Platform;início;tópicos populares;serviço de consulta;serviço de consulta;gerar conjuntos de dados;gerar conjunto de dados;criar conjunto de dados;
solution: Experience Platform
title: Gerar conjuntos de dados de saída a partir dos resultados da consulta
type: Tutorial
description: O Serviço de consulta da Adobe Experience Platform permite a criação de conjuntos de dados pela interface do usuário. Depois que um conjunto de dados é criado, ele pode ser acessado como qualquer outro conjunto de dados no Data Lake e usado para uma variedade de casos de uso.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
source-git-commit: 59d2d74b2d77f3bbaca381af908de5295af24e5b
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 0%

---

# Gerar conjuntos de dados de saída a partir dos resultados da consulta

[!DNL Query Service] permite usar consultas para gerar conjuntos de dados no [!DNL Data Lake]. Esses conjuntos de dados podem ser usados como entrada para mais consultas ou em outros serviços, como o [!DNL Data Science Workspace], o Perfil de Cliente em Tempo Real ou o [!DNL Analysis Workspace].

## Gerar conjuntos de dados a partir da interface do usuário do Adobe Experience Platform

Para criar conjuntos de dados na interface do usuário (UI) do Adobe Experience Platform, siga estas etapas:

1. Crie uma consulta usando um cliente conectado e valide a saída. Para saber como gravar consultas usando o [!DNL Query Editor], leia o [guia da interface do usuário do [!DNL Query Editor] sobre como gravar consultas](./user-guide.md#writing-queries).

2. Na interface da Platform, navegue até **[!UICONTROL Consultas]**, seguido da guia **[!UICONTROL Modelos]** e selecione a consulta criada. Para obter mais detalhes sobre como visualizar consultas que foram criadas e salvas para sua organização na interface do usuário da Platform, leia a [[!DNL Query Service] visão geral](./overview.md#browse).

3. No painel Detalhes da consulta, selecione **[!UICONTROL Executar como CTAS]**.

   ![A guia [!UICONTROL Modelos] do espaço de trabalho de Consultas com o realce Select [!UICONTROL Run as CTAS].](../images/ui/create-datasets/run-as-ctas.png)

4. Na caixa de diálogo exibida, digite um nome de conjunto de dados anexado à sua ID LDAP. O nome do conjunto de dados não precisa ser exclusivo ou seguro para SQL. Observe que o nome da tabela do conjunto de dados será gerado com base no nome do conjunto de dados criado aqui.

5. Em seguida, insira uma descrição para seu conjunto de dados no campo [!UICONTROL Descrição] e selecione **[!UICONTROL Executar como CTAS]**.

   ![A caixa de diálogo Conjunto de dados de saída com os detalhes do conjunto de dados e [!UICONTROL Executar como CTAS] destacados](../images/ui/create-datasets/run-query.png)

6. Depois que a execução da consulta for concluída, navegue até **[!UICONTROL Conjuntos de dados]** para exibir o conjunto de dados criado. Para saber mais sobre como executar ações comuns ao trabalhar com conjuntos de dados na interface da Platform, consulte o [guia da interface do usuário de conjuntos de dados](../../catalog/datasets/user-guide.md).

Depois que um conjunto de dados é criado, ele pode ser acessado como qualquer outro conjunto de dados no [!DNL Data Lake] e usado para uma variedade de casos de uso.

>[!NOTE]
>
>Em uma implementação em tempo real, você deve aplicar rótulos de Governança de dados após a criação do conjunto de dados. Para saber mais sobre como aplicar rótulos de uso de dados a conjuntos de dados, consulte a [Visão geral dos rótulos de uso de dados](../../data-governance/labels/overview.md).

## Gerar conjuntos de dados com um esquema [!DNL Experience Data Model] predefinido

Use a sintaxe SQL para gerar um conjunto de dados com um esquema [!DNL Experience Data Model] (XDM) predefinido. Para obter mais informações sobre a sintaxe à qual o [!DNL Query Service] dá suporte, leia o [Guia de Sintaxe do SQL](../sql/syntax.md#create-table-as-select).

## Conjuntos de dados de saída

Os conjuntos de dados criados por meio dessa funcionalidade são gerados com um esquema ad hoc que corresponde à estrutura dos dados de saída conforme definido na instrução SQL. Alguns serviços downstream exigem conjuntos de dados com esquemas XDM específicos. Verifique os requisitos de formatação de dados para serviços downstream antes de gravar suas consultas.

## Próximas etapas

Depois de ler este documento, você deverá entender como usar o [!DNL Query Service] para gerar conjuntos de dados da interface do usuário da Platform. Para obter mais informações sobre como acessar, gravar e executar consultas na interface do Platform, consulte a [[!DNL Query Service] visão geral da interface do usuário](./overview.md).
