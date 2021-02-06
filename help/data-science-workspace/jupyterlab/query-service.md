---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;populares tópicos;serviço de query
solution: Experience Platform
title: Query Service in Jupyter Notebook
topic: tutorial
type: Tutorial
description: A Adobe Experience Platform permite que você use a Linguagem de Query Estruturada (SQL) na Data Science Workspace, integrando o Serviço de Query ao JúpiterLab como um recurso padrão. Este tutorial demonstra query SQL de amostra para casos de uso comuns para explorar, transformar e analisar dados da Adobe Analytics.
translation-type: tm+mt
source-git-commit: 698639d6c2f7897f0eb4cce2a1f265a0f7bb57c9
workflow-type: tm+mt
source-wordcount: '818'
ht-degree: 1%

---


# Query Service in Jupyter Notebook

[!DNL Adobe Experience Platform] permite usar a Linguagem de Query Estruturada (SQL) em  [!DNL Data Science Workspace] integrando- [!DNL Query Service] se  [!DNL JupyterLab] como um recurso padrão.

Este tutorial demonstra query SQL de amostra para casos de uso comuns para explorar, transformar e analisar dados [!DNL Adobe Analytics].

## Introdução

Antes de iniciar este tutorial, você deve ter os seguintes pré-requisitos:

- Acesso a [!DNL Adobe Experience Platform]. Se você não tiver acesso a uma Organização IMS em [!DNL Experience Platform], fale com o administrador do sistema antes de continuar

- Um conjunto de dados [!DNL Adobe Analytics]

- Um entendimento prático dos seguintes conceitos-chave usados neste tutorial:
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## Acesse [!DNL JupyterLab] e [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. Em [[!DNL Experience Platform]](https://platform.adobe.com), navegue até **[!UICONTROL Notebooks]** a partir da coluna de navegação esquerda. Aguarde um momento para o JupyterLab carregar.

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >Se uma nova guia Iniciador não for exibida automaticamente, abra uma nova guia Iniciador clicando em **[!UICONTROL Arquivo]** e selecione **[!UICONTROL Novo Iniciador]**.

2. Na guia Iniciador, clique no ícone **[!UICONTROL Em branco]** em um ambiente Python 3 para abrir um bloco de anotações vazio.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >O Python 3 é atualmente o único ambiente suportado para o Serviço de Query nos notebooks.

3. No painel de seleção esquerdo, clique no ícone **[!UICONTROL Dados]** e no duplo clique no diretório **[!UICONTROL Conjuntos de Dados]** para lista de todos os conjuntos de dados.

   ![](../images/jupyterlab/query/dataset.png)

4. Encontre um conjunto de dados [!DNL Adobe Analytics] para explorar e clique com o botão direito do mouse na lista. Clique em **[!UICONTROL Dados do Query no Bloco de Notas]** para gerar query SQL no bloco de notas vazio.

5. Clique na primeira célula gerada que contém a função `qs_connect()` e execute-a clicando no botão play. Essa função cria uma conexão entre a sua instância do notebook e [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. Copie o nome do conjunto de dados [!DNL Adobe Analytics] do segundo query SQL gerado, ele será o valor após `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Insira uma nova célula do bloco de anotações clicando no botão **+**.

   ![](../images/jupyterlab/query/insert_cell.gif)

8. Copie, cole e execute as seguintes instruções de importação em uma nova célula. Essas instruções serão usadas para visualizar seus dados:

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. Em seguida, copie e cole as seguintes variáveis em uma nova célula. Modifique seus valores conforme necessário e execute-os.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table` : Nome do seu  [!DNL Adobe Analytics] conjunto de dados.
   - `target_year` : Ano específico a partir do qual se baseiam os dados do público alvo.
   - `target_month` : Mês específico do qual o público alvo é originário.
   - `target_day` : Dia específico do qual os dados do público alvo são originários.

   >[!NOTE]
   >
   >É possível alterar esses valores a qualquer momento. Ao fazer isso, certifique-se de executar a célula de variáveis para que as alterações sejam aplicadas.

## Query de seus dados {#query-your-data}

Insira os seguintes query SQL em células individuais do bloco de notas. Execute um query clicando em sua célula e depois clicando no botão **[!UICONTROL play]**. Os resultados do query bem-sucedidos ou os registros de erros são exibidos abaixo da célula executada.

Quando um notebook está inativo por um longo período de tempo, a conexão entre o notebook e [!DNL Query Service] pode falhar. Nesses casos, reinicie [!DNL JupyterLab] clicando no botão **[!UICONTROL Power]** localizado no canto superior direito.

![](../images/jupyterlab/query/restart_button.png)

O kernel do notebook será redefinido, mas as células permanecerão, execute novamente **todas** as células para continuar onde você parou.

### Contagem horária de visitantes {#hourly-visitor-count}

O query a seguir retorna a contagem de visitantes por hora para uma data especificada:

#### Query

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

No query acima, o carimbo de data e hora na cláusula `WHERE` é definido para ser o valor de `target_year`. Inclua variáveis em query SQL, contendo-as entre chaves (`{}`).

A primeira linha do query contém a variável opcional `hourly_visitor`. Os resultados do query serão armazenados nessa variável como um dataframe de Pandas. Armazenar resultados em um dataframe permite visualizar posteriormente os resultados do query usando um pacote [!DNL Python] desejado. Execute o seguinte código [!DNL Python] em uma nova célula para gerar um gráfico de barras:

```python
trace = go.Bar(
    x = hourly_visitor['Hour'],
    y = hourly_visitor['Visit_Count'],
    name = "Visitor Count"
)
layout = go.Layout(
    title = 'Visit Count by Hour of Day',
    width = 1200,
    height = 600,
    xaxis = dict(title = 'Hour of Day'),
    yaxis = dict(title = 'Count')
)
fig = go.Figure(data = [trace], layout = layout)
iplot(fig)
```

### Contagem de atividades por hora {#hourly-activity-count}

O query a seguir retorna a contagem de ações por hora para uma data especificada:

#### Query <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

A execução do query acima armazenará os resultados em `hourly_actions` como um dataframe. Execute a seguinte função em uma nova célula para pré-visualização dos resultados:

```python
hourly_actions.head()
```

O query acima pode ser modificado para retornar a contagem de ações por hora para um intervalo de datas especificado usando operadores lógicos na cláusula **WHERE**:

#### Query <!-- omit in toc -->

```sql
%%read_sql hourly_actions_date_range -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  timestamp >= TO_TIMESTAMP('2019-06-01 00', 'YYYY-MM-DD HH')
       AND timestamp <= TO_TIMESTAMP('2019-06-02 23', 'YYYY-MM-DD HH')
GROUP  BY Day, Hour
ORDER  BY Hour;
```

A execução do query modificado armazenará os resultados em `hourly_actions_date_range` como um dataframe. Execute a seguinte função em uma nova célula para pré-visualização dos resultados:

```python
hourly_actions_date_rage.head()
```

### Número de eventos por sessão de visitante {#number-of-events-per-visitor-session}

O query a seguir retorna o número de eventos por sessão de visitante para uma data especificada:

#### Query <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

Execute o seguinte código [!DNL Python] para gerar um histograma para o número de eventos por sessão de visita:

```python
data = [go.Histogram(x = events_per_session['Count'])]

layout = go.Layout(
    title = 'Histogram of Number of Events per Visit Session',
    xaxis = dict(title = 'Number of Events'),
    yaxis = dict(title = 'Count')
)

fig = go.Figure(data = data, layout = layout)
iplot(fig)
```

### Páginas populares para um determinado dia {#popular-pages-for-a-given-day}

O query a seguir retorna as dez páginas mais populares para uma data especificada:

#### Query <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### Usuários ativos em um determinado dia {#active-users-for-a-given-day}

O query a seguir retorna os dez usuários mais ativos para uma data especificada:

#### Query <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### Cidades ativas por atividade do usuário {#active-cities-by-user-activity}

O query a seguir retorna as dez cidades que estão gerando a maioria das atividades do usuário para uma data especificada:

#### Query <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE TIMESTAMP = to_timestamp('{target_year}-{target_month}-{target_day}')
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## Próximas etapas

Este tutorial demonstrou alguns casos de uso de exemplo para utilizar [!DNL Query Service] em notebooks [!DNL Jupyter]. Siga o tutorial [Analisar seus dados usando Notebooks de Júpiter](./analyze-your-data.md) para ver como operações semelhantes são executadas usando o SDK de Acesso a Dados.