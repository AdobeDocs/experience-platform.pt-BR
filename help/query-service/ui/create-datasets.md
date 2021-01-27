---
keywords: Experience Platform;home;popular topics;query service;Query service;generate datasets;generate dataset;create dataset;
solution: Experience Platform
title: Gerar conjuntos de dados a partir dos resultados do query
topic: queries
type: Tutorial
description: 'O Serviço de query permite a criação de conjuntos de dados da interface do usuário. Depois que um conjunto de dados é criado, ele pode ser acessado como qualquer outro conjunto de dados no Data Lake e usado para diversos casos de uso. '
translation-type: tm+mt
source-git-commit: 0ba4e26927cdc96855f35d72a8a6de55f4a34bfa
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 1%

---


# Gerar conjuntos de dados a partir dos resultados do query

A verdadeira potência de [!DNL Query Service] é revelada quando query são usados para gerar conjuntos de dados em [!DNL Data Lake] para serem usados como entrada em mais query ou em outros serviços, como [!DNL Data Science Workspace], [!DNL Real-time Customer Profile] ou [!DNL Analysis Workspace].

[!DNL Query Service] permite a criação de conjuntos de dados da interface do usuário. Siga estas etapas:

1. Grave seu query usando um cliente conectado e valide a saída.
2. Faça logon na interface do usuário [!DNL Platform] e vá para Query.
3. Encontre seu query na lista e passe o mouse sobre a linha.
4. Clique em **[!UICONTROL Criar conjunto de dados]**. ![Imagem](../images/ui/output-dataset.png)
5. Insira um nome de conjunto de dados, anexado à sua ID LDAP (não precisa ser exclusivo ou seguro para SQL); o sistema gera um &quot;nome de tabela&quot; com base no nome fornecido aqui).
6. Insira uma descrição do conjunto de dados e clique em **[!UICONTROL Executar Query]**.![Imagem](../images/ui/run-query.png)
7. Observe o query ser concluído e vá para a página de lista do conjunto de dados para ver o conjunto de dados que você acabou de criar.

Depois que um conjunto de dados é criado, ele pode ser acessado como qualquer outro conjunto de dados no [!DNL Data Lake] e usado para vários casos de uso.

>[!NOTE]
>
>Em uma implementação em tempo real, você deve aplicar rótulos [!DNL Data Governance] após a criação do conjunto de dados.

## Gerar conjuntos de dados com um schema [!DNL Experience Data Model] predefinido

Para gerar um conjunto de dados com um schema [!DNL Experience Data Model] (XDM) predefinido, é necessário usar a sintaxe SQL. Para obter mais informações sobre qual sintaxe você deve usar, leia o [Guia de sintaxe SQL](../sql/syntax.md#create-table-as-select).

## Conjuntos de dados de saída

Os conjuntos de dados criados por meio dessa funcionalidade são gerados com um schema ad hoc que corresponde à estrutura dos dados de saída, conforme definido na instrução SQL. Alguns serviços downstream exigem conjuntos de dados com schemas específicos [!DNL Experience Data Model] (XDM). Verifique os requisitos de formatação de dados para serviços downstream antes de gravar seus query.