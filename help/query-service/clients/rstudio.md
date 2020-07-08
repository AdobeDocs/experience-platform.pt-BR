---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conectar-se com o RStudio
topic: connect
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 2%

---


# Conectar-se com o RStudio

Este documento percorre as etapas para conectar o R Studio ao serviço de Query.

Depois de instalar o RStudio, na tela do *Console* que é exibida, primeiro será necessário preparar seu script R para usar o PostgreSQL.

```r
install.packages("RPostgreSQL")
install.packages("rstudioapi")
require("RPostgreSQL")
require("rstudioapi")
```

Depois de preparar seu script R para usar o PostgreSQL, agora é possível conectar o RStudio ao Query Service carregando o driver PostgreSQL.

```r
drv <- dbDriver("PostgreSQL")
con <- dbConnect(drv, 
 dbname = "{DATABASE_NAME}",
 host="{HOST_NUMBER}",
 port={PORT_NUMBER},
 user="{USERNAME}",
 password="{PASSWORD}")
```

| Propriedade | Descrição |
| -------- | ----------- |
| `{DATABASE_NAME}` | O nome do banco de dados que será usado. |
| `{HOST_NUMBER` e `{PORT_NUMBER}` | O terminal do host e sua porta para o Serviço de Query. |
| `{USERNAME}` e `{PASSWORD}` | As credenciais de logon que serão usadas. O nome de usuário assume a forma de `ORG_ID@AdobeOrg`. |

>[!NOTE]
>
>Para obter mais informações sobre como localizar o nome do banco de dados, o host, a porta e as credenciais de logon, visite a página de [credenciais no Platform](https://platform.adobe.com/query/configuration). Para localizar suas credenciais, faça logon no Platform, clique em **Query** e, em seguida, clique em **Credenciais**.

## Próximas etapas

Agora que você se conectou ao Serviço de Query, é possível gravar query para executar e editar instruções SQL. Por exemplo, você pode usar `dbGetQuery(con, sql)` para executar query, onde `sql` é o query SQL que deseja executar.

O query a seguir usa um conjunto de dados contendo [ExperienceEvents](../creating-queries/experience-event-queries.md) e cria um histograma das visualizações de página de um site, dada a altura de tela do dispositivo.

```sql
df_pageviews <- dbGetQuery(con,
"SELECT t.range AS buckets, 
 Count(*) AS pageviews 
FROM (SELECT CASE 
 WHEN device.screenheight BETWEEN 0 AND 99 THEN '0 - 99' 
 WHEN device.screenheight BETWEEN 100 AND 199 THEN '100-199' 
 WHEN device.screenheight BETWEEN 200 AND 299 THEN '200-299' 
 WHEN device.screenheight BETWEEN 300 AND 399 THEN '300-399' 
 WHEN device.screenheight BETWEEN 400 AND 499 THEN '400-499' 
 WHEN device.screenheight BETWEEN 500 AND 599 THEN '500-599' 
 ELSE '600-699' 
 end AS range 
 FROM aa_post_vals_3) t 
GROUP BY t.range 
ORDER BY buckets 
LIMIT 1000000")
```

Uma resposta bem-sucedida retorna os resultados do query:

```r
df_pageviews
 buckets pageviews
1 0 - 99 198985
2 500-599 67138
3 300-399 2147
4 200-299 354
5 400-499 6947
6 100-199 4415
7 600-699 3097040
```

Para obter mais informações sobre como gravar e executar query, leia o guia [de query](../creating-queries/creating-queries.md)em execução.