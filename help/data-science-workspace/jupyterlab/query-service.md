---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;tópicos populares;serviço de consulta
solution: Experience Platform
title: Serviço de consulta no Jupyter Notebook
type: Tutorial
description: O Adobe Experience Platform permite usar a Linguagem de consulta estruturada (SQL) no Data Science Workspace ao integrar o Serviço de consulta ao JupyterLab como um recurso padrão. Este tutorial demonstra exemplos de consultas SQL para casos de uso comuns para explorar, transformar e analisar dados do Adobe Analytics.
exl-id: c5ac7d11-a3bd-4ef8-a650-9f496a8bbaa7
source-git-commit: 81f48de908b274d836f551bec5693de13c5edaf1
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 1%

---

# Serviço de consulta no Jupyter Notebook

[!DNL Adobe Experience Platform] permite usar a Linguagem de consulta estruturada (SQL) no [!DNL Data Science Workspace] ao integrar [!DNL Query Service] em [!DNL JupyterLab] como um recurso padrão.

Este tutorial demonstra exemplos de consultas SQL para casos de uso comuns para explorar, transformar e analisar [!DNL Adobe Analytics] dados.

## Introdução

Antes de iniciar este tutorial, você deve ter os seguintes pré-requisitos:

- Acesso a [!DNL Adobe Experience Platform]. Se você não tiver acesso a uma organização no [!DNL Experience Platform], entre em contato com o administrador do sistema antes de continuar

- Um [!DNL Adobe Analytics] conjunto de dados

- Uma compreensão funcional dos seguintes conceitos principais usados neste tutorial:
   - [[!DNL Experience Data Model (XDM) and XDM System]](../../xdm/home.md)
   - [[!DNL Query Service]](../../query-service/home.md)
   - [[!DNL Query Service SQL Syntax]](../../query-service/sql/overview.md)
   - Adobe Analytics

## Access [!DNL JupyterLab] e [!DNL Query Service] {#access-jupyterlab-and-query-service}

1. Entrada [[!DNL Experience Platform]](https://platform.adobe.com), navegue até **[!UICONTROL Notebooks]** na coluna de navegação à esquerda. Aguarde um momento para o JupyterLab carregar.

   ![](../images/jupyterlab/query/jupyterlab-launcher.png)

   >[!NOTE]
   >
   >Se uma nova guia Iniciador não for exibida automaticamente, abra uma nova guia Iniciador clicando em **[!UICONTROL Arquivo]** e selecione **[!UICONTROL Novo inicializador]**.

2. Na guia Iniciador, clique na guia **[!UICONTROL Em branco]** em um ambiente Python 3 para abrir um bloco de anotações vazio.

   ![](../images/jupyterlab/query/blank_notebook.png)

   >[!NOTE]
   >
   >No momento, o Python 3 é o único ambiente compatível com o Serviço de consulta em notebooks.

3. No painel de seleção esquerdo, clique no link **[!UICONTROL Dados]** e clique duas vezes no ícone **[!UICONTROL Conjuntos de dados]** diretório para listar todos os conjuntos de dados.

   ![](../images/jupyterlab/query/dataset.png)

4. Encontrar um [!DNL Adobe Analytics] para explorar e clicar com o botão direito do mouse na lista, clique em **[!UICONTROL Consultar Dados no Notebook]** para gerar consultas SQL no bloco de notas vazio.

5. Clique na primeira célula gerada que contém a função `qs_connect()` e execute-o clicando no botão play. Essa função cria uma conexão entre a instância do bloco de anotações e o [!DNL Query Service].

   ![](../images/jupyterlab/query/execute.png)

6. Copie para baixo o [!DNL Adobe Analytics] nome do conjunto de dados da segunda consulta SQL gerada, será o valor depois de `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Insira uma nova célula do bloco de anotações clicando no **+** botão.

   ![](../images/jupyterlab/query/insert_cell.gif)

8. Copie, cole e execute as seguintes instruções de importação em uma nova célula. Estas instruções serão usadas para visualizar seus dados:

   ```python
   import plotly.plotly as py
   import plotly.graph_objs as go
   from plotly.offline import iplot
   ```

9. Em seguida, copie e cole as seguintes variáveis em uma nova célula. Modifique os valores conforme necessário e execute-os.

   ```python
   target_table = "your Adobe Analytics dataset name"
   target_year = "2019"
   target_month = "04"
   target_day = "01"
   ```

   - `target_table`: Nome do seu [!DNL Adobe Analytics] conjunto de dados.
   - `target_year`: ano específico de onde os dados do target são.
   - `target_month`: mês específico em que o target é.
   - `target_day`: dia específico em que os dados do público-alvo são.

   >[!NOTE]
   >
   >É possível alterar esses valores a qualquer momento. Ao fazer isso, certifique-se de executar a célula das variáveis para que as alterações sejam aplicadas.

## Consultar seus dados {#query-your-data}

Insira as seguintes consultas SQL em células individuais do bloco de anotações. Execute uma query selecionando em sua célula, seguida pela seleção da variável **[!UICONTROL play]** botão. Resultados de consulta bem-sucedidos ou logs de erro são exibidos abaixo da célula executada.

Quando um notebook fica inativo por um longo período de tempo, a conexão entre o notebook e [!DNL Query Service] pode quebrar. Nesses casos, reinicie o [!DNL JupyterLab] selecionando o **Restart** botão ![botão reiniciar](../images/jupyterlab/user-guide/restart_button.png) localizado no canto superior direito próximo ao botão liga/desliga.

O kernel do notebook é redefinido, mas as células permanecerão, execute novamente todas as células para continuar de onde você parou.

### Contagem horária de visitantes {#hourly-visitor-count}

A consulta a seguir retorna a contagem horária de visitantes de uma data especificada:

#### Consulta

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

Na consulta acima, o carimbo de data e hora no `WHERE` está definida como o valor de `target_year`. Incluir variáveis em consultas SQL, contendo-as em chaves (`{}`).

A primeira linha da query contém a variável opcional `hourly_visitor`. Os resultados da consulta serão armazenados nessa variável como um quadro de dados Pandas. O armazenamento de resultados em um quadro de dados permite visualizar os resultados da consulta posteriormente usando um [!DNL Python] pacote. Execute o seguinte [!DNL Python] em uma nova célula para gerar um gráfico de barras:

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

A consulta a seguir retorna a contagem de ações por hora para uma data especificada:

#### Consulta <!-- omit in toc -->

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

A execução da consulta acima armazenará os resultados em `hourly_actions` como um quadro de dados. Execute a seguinte função em uma nova célula para visualizar os resultados:

```python
hourly_actions.head()
```

A consulta acima pode ser modificada para retornar a contagem de ações por hora para um intervalo de datas especificado usando operadores lógicos na variável **ONDE** cláusula:

#### Consulta <!-- omit in toc -->

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

A execução da consulta modificada armazena os resultados em `hourly_actions_date_range` como um quadro de dados. Execute a seguinte função em uma nova célula para visualizar os resultados:

```python
hourly_actions_date_rage.head()
```

### Número de eventos por sessão de visitante {#number-of-events-per-visitor-session}

A consulta a seguir retorna o número de eventos por sessão de visitante para uma data especificada:

#### Consulta <!-- omit in toc -->

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

Execute o seguinte [!DNL Python] código para gerar um histograma para o número de eventos por sessão de visita:

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

A consulta a seguir retorna as dez páginas mais populares para uma data especificada:

#### Consulta <!-- omit in toc -->

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

### Usuários ativos de um determinado dia {#active-users-for-a-given-day}

A consulta a seguir retorna os dez usuários mais ativos para uma data especificada:

#### Consulta <!-- omit in toc -->

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

A consulta a seguir retorna as dez cidades que estão gerando a maioria das atividades do usuário para uma data especificada:

#### Consulta <!-- omit in toc -->

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

Este tutorial demonstrou alguns casos de uso de exemplo para utilizar [!DNL Query Service] in [!DNL Jupyter] notebooks. Siga as [Analise seus dados usando o Jupyter Notebooks](./analyze-your-data.md) tutorial para ver como operações semelhantes são executadas usando o SDK do Data Access.
