---
keywords: Experience Platform;home;popular topics;query service;Query service;datasets;tables;schemas;
solution: Experience Platform
title: Conjuntos de dados vs tabelas e schemas
topic: queries
translation-type: tm+mt
source-git-commit: c5d3be4706ca6d6a30e203067db6ddc894b9bfb4
workflow-type: tm+mt
source-wordcount: '181'
ht-degree: 1%

---


# Conjuntos de dados vs tabelas e schemas

Revise a lista de conjuntos de dados disponíveis na interface do usuário [do](https://platform.adobe.com/datasets)Adobe Experience Platform, observando os nomes dos conjuntos de dados.
>[!NOTE]
>
>Alguns nomes de conjuntos de dados têm espaços e podem não ser seguros para SQL.

![](../images/queries/datasets-and-tables/dataset-names.png)


Revise a estrutura hierárquica do schema Conjunto de Dados na interface do usuário clicando em um nome de schema na tabela do conjunto de dados.

![](../images/queries/datasets-and-tables/schema-information.png)

Abra a linha de comando PSQL e use os detalhes da conexão aqui: [https://platform.adobe.com/query/configuration](https://platform.adobe.com/query/configuration).

![](../images/clients/psql/connect-bi.png)

Para visualização das tabelas disponíveis com [!DNL Platform] SQL, você pode usar `\d` ou `SHOW TABLES;`.


`\d` exibe a visualização PostgreSQL padrão

```sql
             List of relations
 Schema |       Name      | Type  |  Owner   
--------+-----------------+-------+----------
 public | luma_midvalues  | table | postgres
 public | luma_postvalues | table | postgres
(2 rows)
```

`SHOW TABLES;` é um comando personalizado que fornece uma visualização mais detalhada e apresenta a tabela, bem como o nome do conjunto de dados encontrado na [!DNL Platform] interface do usuário.

```sql
       name      |        dataSetId         |     dataSet    | description | resolved 
-----------------+--------------------------+----------------+-------------+----------
 luma_midvalues  | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues | 5c86b896b3c162151785b43c | Luma midValues |             | false
(2 rows)
```

Para visualização do schema raiz de uma tabela, use o `\d table_name` comando.

>[!NOTE]
>
>O schema apresentado mostra os campos raiz, a maioria complexos, referenciados a um tipo de Objeto na interface do usuário do schema do Conjunto de Dados.

`\d luma_midvalues`

```sql
                         Table "public.luma_midvalues"
      Column       |             Type            | Collation | Nullable | Default 
-------------------+-----------------------------+-----------+----------+---------
 timestamp         | timestamp                   |           |          | 
 _id               | text                        |           |          | 
 productlistitems  | anyarray                    |           |          | 
 commerce          | luma_midvalues_commerce     |           |          | 
 receivedtimestamp | timestamp                   |           |          | 
 enduserids        | luma_midvalues_enduserids   |           |          | 
 datasource        | datasource                  |           |          | 
 web               | luma_midvalues_web          |           |          | 
 placecontext      | luma_midvalues_placecontext |           |          | 
 identitymap       | anymap                      |           |          | 
 marketing         | marketing                   |           |          | 
 environment       | luma_midvalues_environment  |           |          | 
 _experience       | luma_midvalues__experience  |           |          | 
 device            | device                      |           |          | 
 search            | search                      |           |          | 
```

Para ir mais longe no schema, use sublinhados (`_`) para declarar a coluna na tabela que você deseja descrever. Por exemplo, `\d table_name_column`

`\d luma_midvalues_web`

```sql
                 Composite type "public.luma_midvalues_web"
     Column     |               Type                | Collation | Nullable | Default 
----------------+-----------------------------------+-----------+----------+---------
 webpagedetails | luma_midvalues_web_webpagedetails |           |          | 
 webreferrer    | web_webreferrer                   |           |          | 
```
