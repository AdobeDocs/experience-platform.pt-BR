---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Gerar conjuntos de dados a partir dos resultados do query
topic: queries
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '298'
ht-degree: 0%

---


# Gerar conjuntos de dados a partir dos resultados do query

O verdadeiro poder do Serviço de Query é revelado quando os query são usados para gerar conjuntos de dados no lago de dados para serem usados como entrada em mais query ou em outros serviços, como Data Science Workspace, Perfil de cliente em tempo real ou Analysis Workspace.

O Serviço de Query permite a criação de conjuntos de dados da interface do usuário. Siga estas etapas:

1. Grave seu query usando um cliente conectado e valide a saída.
2. Faça logon na interface do usuário do Platform e vá para Query.
3. Encontre seu query na lista e passe o mouse sobre a linha.
4. Clique em **Criar conjunto de dados**. ![Imagem](../images/queries/create-datasets/click-create-dataset.png)
5. Insira um nome de conjunto de dados, anexado à sua ID LDAP (não precisa ser exclusivo ou seguro para SQL); o sistema gera um &quot;nome de tabela&quot; com base no nome fornecido aqui).
6. Insira uma descrição do conjunto de dados e clique em **Executar Query**.![Imagem](../images/queries/create-datasets/run-query.png)
7. Observe o query ser concluído e vá para a página de lista do conjunto de dados para ver o conjunto de dados que você acabou de criar.

Depois que um conjunto de dados é criado, ele pode ser acessado como qualquer outro conjunto de dados no lago de dados e usado para diversos casos de uso.

>[!NOTE]
>
>Em uma implementação ativa, você deve aplicar rótulos de controle de dados após a criação do conjunto de dados.

## Gerar conjuntos de dados com um schema do Modelo de dados de experiência predefinido

Para gerar um conjunto de dados com um schema do Experience Data Model (XDM) predefinido, é necessário usar a sintaxe SQL. Para obter mais informações sobre qual sintaxe você deve usar, leia o guia [Sintaxe](../sql/syntax.md#create-table-as-select)SQL.

## Conjuntos de dados de saída

Os conjuntos de dados criados por meio dessa funcionalidade são gerados com um schema ad hoc que corresponde à estrutura dos dados de saída, conforme definido na instrução SQL. Alguns serviços downstream exigem conjuntos de dados com schemas específicos do Modelo de Dados de Experiência (XDM). Verifique os requisitos de formatação de dados para serviços downstream antes de gravar seus query.