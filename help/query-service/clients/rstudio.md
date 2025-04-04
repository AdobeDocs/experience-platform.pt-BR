---
keywords: Experience Platform;home;tópicos populares;Serviço de consulta;serviço de consulta;RStudio;rstudio;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o RStudio ao Serviço de consulta
description: Este documento aborda as etapas para conectar o R Studio ao Adobe Experience Platform Query Service.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '439'
ht-degree: 0%

---

# Conectar [!DNL RStudio] ao Serviço de consulta

Este documento aborda as etapas para conectar o [!DNL RStudio] ao Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] foi reformulado como [!DNL Posit]. [!DNL RStudio] produtos foram renomeados para [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] Gerente, [!DNL Posit Cloud] e [!DNL Posit Academy].
>
> Este guia supõe que você já tenha acesso ao [!DNL RStudio] e esteja familiarizado com como usá-lo. Mais informações sobre [!DNL RStudio] podem ser encontradas na [documentação [!DNL RStudio] oficial](https://rstudio.com/products/rstudio/).
> 
> Além disso, para usar o [!DNL RStudio] com o Serviço de consulta, é necessário instalar o Driver JDBC 4.2 [!DNL PostgreSQL]. Você pode baixar o driver JDBC no [[!DNL PostgreSQL] site oficial](https://jdbc.postgresql.org/download/).

## Criar uma conexão [!DNL Query Service] na interface [!DNL RStudio]

Após instalar o [!DNL RStudio], é necessário instalar o pacote RJDBC. As instruções sobre como [conectar um banco de dados por meio da linha de comando](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) podem ser encontradas na documentação oficial de Posts.

Se estiver usando um sistema operacional Mac, você pode selecionar **[!UICONTROL Ferramentas]** na barra de menus seguido por **[!UICONTROL Instalar Pacotes]** no menu suspenso. Como alternativa, selecione a guia **[!DNL Packages]** na interface do RStudio e selecione **[!DNL Install]**.

Um pop-up é exibido, mostrando a tela **[!DNL Install Packages]**. Verifique se **[!DNL Repository (CRAN)]** está selecionado para a seção **[!DNL Install from]**. O valor de **[!DNL Packages]** deve ser `RJDBC`. Verifique se **[!DNL Install dependencies]** está selecionado. Depois de confirmar que todos os valores estão corretos, selecione **[!DNL Install]** para instalar os pacotes. Agora que o pacote RJDBC foi instalado, reinicie [!DNL RStudio] para concluir o processo de instalação.

Depois que [!DNL RStudio] for reiniciado, você pode se conectar ao Serviço de Consulta. Selecione o pacote **[!DNL RJDBC]** no painel **[!DNL Packages]** e digite o seguinte comando no console:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Onde `{PATH TO THE POSTGRESQL JDBC JAR}` representa o caminho para o JAR JDBC [!DNL PostgreSQL] que foi instalado em seu computador.

Agora, você pode criar sua conexão com o Serviço de consulta. Digite o seguinte comando no console:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Consulte a [[!DNL Query Service] documentação SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros ao Serviço de Consulta da Adobe Experience Platform e como se conectar usando o modo SSL `verify-full`.

Para obter mais informações sobre como localizar o nome do banco de dados, o host, a porta e as credenciais de logon, leia o [guia de credenciais](../ui/credentials.md). Para encontrar suas credenciais, faça logon em [!DNL Experience Platform] e selecione **[!UICONTROL Consultas]**, seguido de **[!UICONTROL Credenciais]**.

Uma mensagem na saída do console confirma a conexão com o Serviço de consulta.

## Gravação de consultas

Agora que você se conectou a [!DNL Query Service], é possível gravar consultas para executar e editar instruções SQL. Por exemplo, você pode usar `dbGetQuery(con, sql)` para executar consultas, onde `sql` é a consulta SQL que você deseja executar.

A consulta a seguir usa um conjunto de dados contendo [Eventos de Experiência](../../xdm/classes/experienceevent.md) e cria um histograma de exibições de página de um site, dada a altura da tela do dispositivo.

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

Uma resposta bem-sucedida retorna os resultados da consulta:

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

## Próximas etapas

Para obter mais informações sobre como gravar e executar consultas, leia o manual em [executando consultas](../best-practices/writing-queries.md).
