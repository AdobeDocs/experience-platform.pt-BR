---
keywords: Experience Platform; home; tópicos populares; serviço de consulta; serviço de consulta; gerar conjuntos de dados; gerar conjunto de dados; criar conjunto de dados;
solution: Experience Platform
title: Gerar conjuntos de dados a partir de resultados no serviço de query
topic-legacy: queries
type: Tutorial
description: O Serviço de query do Adobe Experience Platform permite a criação de conjuntos de dados da interface do usuário. Depois que um conjunto de dados é criado, ele pode ser acessado como qualquer outro conjunto de dados no Data Lake e usado para uma variedade de casos de uso.
exl-id: 6f6c049d-f19f-4161-aeb4-3a01eca7dc75
translation-type: tm+mt
source-git-commit: d2f19cc97082f75e66cf38e54b5bdb89482930ed
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Gerar conjuntos de dados a partir de resultados no Serviço de query

O verdadeiro poder de [!DNL Query Service] é revelado quando as consultas são usadas para gerar conjuntos de dados no [!DNL Data Lake] a ser usado como entrada em mais queries ou em outros serviços, como [!DNL Data Science Workspace], [!DNL Real-time Customer Profile] ou [!DNL Analysis Workspace].

[!DNL Query Service] permite a criação de conjuntos de dados da interface do usuário. Siga estas etapas:

1. Escreva sua consulta usando um cliente conectado e valide a saída.
2. Faça logon na interface do usuário [!DNL Platform] e acesse Consultas.
3. Encontre seu query na lista e passe o mouse sobre a linha.
4. Selecione **[!UICONTROL Create Dataset]**. ![Imagem](../images/ui/create-datasets/output-dataset.png)
5. Insira um nome de conjunto de dados, anexado à sua ID LDAP (não precisa ser exclusiva ou segura para SQL; o sistema gera um &quot;nome de tabela&quot; com base no nome fornecido aqui).
6. Insira uma descrição do conjunto de dados e selecione **[!UICONTROL Run Query]**.![Imagem](../images/ui/create-datasets/run-query.png)
7. Observe a consulta ser concluída e, em seguida, vá para a página de lista do conjunto de dados para ver o conjunto de dados que você acabou de criar.

Depois que um conjunto de dados é criado, ele pode ser acessado como qualquer outro conjunto de dados no [!DNL Data Lake] e usado para uma variedade de casos de uso.

>[!NOTE]
>
>Em uma implementação em tempo real, você deve aplicar rótulos [!DNL Data Governance] após a criação do conjunto de dados.

## Gerar conjuntos de dados com um esquema [!DNL Experience Data Model] predefinido

Para gerar um conjunto de dados com um esquema [!DNL Experience Data Model] (XDM) predefinido, é necessário usar a sintaxe SQL. Para obter mais informações sobre qual sintaxe você deve usar, leia o [Guia de sintaxe SQL](../sql/syntax.md#create-table-as-select).

## Conjuntos de dados de saída

Os conjuntos de dados criados por meio dessa funcionalidade são gerados com um esquema ad hoc que corresponde à estrutura dos dados de saída, conforme definido na instrução SQL. Alguns serviços downstream exigem conjuntos de dados com esquemas específicos [!DNL Experience Data Model] (XDM). Verifique os requisitos de formatação de dados para serviços downstream antes de gravar suas consultas.
