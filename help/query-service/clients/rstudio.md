---
keywords: Experience Platform;início;tópicos populares;Serviço de consulta;serviço de consulta;RStudio;rstudio;conectar ao serviço de consulta;
solution: Experience Platform
title: Conectar o RStudio ao Serviço de consulta
description: Este documento aborda as etapas para conectar o R Studio ao Adobe Experience Platform Query Service.
exl-id: 8dd82bad-6ffb-4536-9c27-223f471a49c6
source-git-commit: 668b2624b7a23b570a3869f87245009379e8257c
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 0%

---

# Conectar [!DNL RStudio] para o Serviço de consulta

Este documento aborda as etapas de conexão [!DNL RStudio] com o Adobe Experience Platform [!DNL Query Service].

>[!NOTE]
>
> [!DNL RStudio] agora foi reformulado como [!DNL Posit]. [!DNL RStudio] Os produtos do foram renomeados para [!DNL Posit Connect], [!DNL Posit Workbench], [!DNL Posit Package] Gerente, [!DNL Posit Cloud], e [!DNL Posit Academy].
>
> Este guia supõe que você já tenha acesso ao [!DNL RStudio] e estão familiarizados com como usá-lo. Mais informações sobre [!DNL RStudio] pode ser encontrado no [oficial [!DNL RStudio] documentação](https://rstudio.com/products/rstudio/).
> 
> Além disso, para usar [!DNL RStudio] com o Serviço de consulta, é necessário instalar o [!DNL PostgreSQL] Driver JDBC 4.2. Você pode baixar o driver JDBC no [[!DNL PostgreSQL] site oficial](https://jdbc.postgresql.org/download/).

## Criar um [!DNL Query Service] conexão no [!DNL RStudio] interface

Após a instalação [!DNL RStudio], é necessário instalar o pacote RJDBC. Instruções sobre como [conectar um banco de dados por meio da linha de comando](https://solutions.posit.co/connections/db/best-practices/drivers/#connecting-to-a-database-in-r) podem ser encontradas na documentação oficial do Post.

Se estiver usando um sistema operacional Mac, você pode selecionar **[!UICONTROL Ferramentas]** na barra de menus, seguida por **[!UICONTROL Instalar pacotes]** no menu suspenso. Como alternativa, selecione o **[!DNL Packages]** na interface do usuário do RStudio e selecione **[!DNL Install]**.

Um pop-up é exibido, mostrando a **[!DNL Install Packages]** tela. Assegure que **[!DNL Repository (CRAN)]** está selecionado para o **[!DNL Install from]** seção. O valor de **[!DNL Packages]** deve ser `RJDBC`. Assegurar **[!DNL Install dependencies]** está selecionada. Após confirmar que todos os valores estão corretos, selecione **[!DNL Install]** para instalar os pacotes. Agora que o pacote RJDBC foi instalado, reinicie [!DNL RStudio] para concluir o processo de instalação.

Depois [!DNL RStudio] foi reiniciado, agora é possível conectar-se ao Serviço de consulta. Selecione o **[!DNL RJDBC]** pacote no **[!DNL Packages]** e digite o seguinte comando no console:

```console
pgsql <- JDBC("org.postgresql.Driver", "{PATH TO THE POSTGRESQL JDBC JAR}", "`")
```

Onde `{PATH TO THE POSTGRESQL JDBC JAR}` representa o caminho para o [!DNL PostgreSQL] JAR JDBC que foi instalado no computador.

Agora, você pode criar sua conexão com o Serviço de consulta. Digite o seguinte comando no console:

```console
qsconnection <- dbConnect(pgsql, "jdbc:postgresql://{HOSTNAME}:{PORT}/{DATABASE_NAME}?user={USERNAME}&password={PASSWORD}&sslmode=require")
```

>[!IMPORTANT]
>
>Consulte a [[!DNL Query Service] Documentação do SSL](./ssl-modes.md) para saber mais sobre o suporte SSL para conexões de terceiros ao Adobe Experience Platform Query Service e como se conectar usando `verify-full` Modo SSL.

Para obter mais informações sobre como localizar o nome do banco de dados, o host, a porta e as credenciais de logon, leia a [guia de credenciais](../ui/credentials.md). Para encontrar suas credenciais, faça logon no [!DNL Platform]e selecione **[!UICONTROL Consultas]**, seguido por **[!UICONTROL Credenciais]**.

Uma mensagem na saída do console confirma a conexão com o Serviço de consulta.

## Gravação de consultas

Agora que você se conectou ao [!DNL Query Service], você pode gravar consultas para executar e editar instruções SQL. Por exemplo, você pode usar `dbGetQuery(con, sql)` para executar consultas, onde `sql` é a consulta SQL que você deseja executar.

A consulta a seguir usa um conjunto de dados que contém [Eventos de experiência](../../xdm/classes/experienceevent.md) e cria um histograma de exibições de página de um site, dada a altura da tela do dispositivo.

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

Para obter mais informações sobre como gravar e executar consultas, leia o manual no [execução de consultas](../best-practices/writing-queries.md).
