---
keywords: Experience Platform;JupyterLab;notebooks;Data Science Workspace;popular topics
solution: Experience Platform
title: Serviço de Query em Jupyter notebook
topic: Tutorial
translation-type: tm+mt
source-git-commit: d0596dc3c744e192c4d2ad04d6365846a0115371

---


# Serviço de Query em Jupyter notebook

A plataforma Adobe Experience permite que você use a Linguagem de Query Estruturada (SQL) na Área de Trabalho da Data Science, integrando o Serviço de Query ao JúpiterLab como um recurso padrão.

Este tutorial demonstra os seguintes query SQL de amostra para casos de uso comuns para explorar, transformar e analisar dados do Adobe Analytics:

- [Acesso ao JupyterLab e ao serviço de Query](#access-jupyterlab-and-query-service)
- [Query de seus dados](#query-your-data)
   - [Contagem horária de visitantes](#hourly-visitor-count)
   - [Contagem de atividades por hora](#hourly-activity-count)
   - [Número de eventos por sessão de visitante](#number-of-events-per-visitor-session)
   - [Páginas populares de um determinado dia](#popular-pages-for-a-given-day)
   - [Usuários ativos em um determinado dia](#active-users-for-a-given-day)
   - [Cidades ativas por atividade do usuário](#active-cities-by-user-activity)

## Introdução

Antes de iniciar este tutorial, você deve ter os seguintes pré-requisitos:

- Acesso à Adobe Experience Platform. Se você não tiver acesso a uma organização IMS na plataforma Experience, fale com o administrador do sistema antes de continuar

- Um conjunto de dados do Adobe Analytics

- Um entendimento prático dos seguintes conceitos-chave usados neste tutorial:
   - [Modelo de dados de experiência (XDM) e sistema XDM](../../xdm/home.md)
   - [Serviço de Query](../../query-service/home.md)
   - [Sintaxe SQL do Query Service](../../query-service/sql/overview.md)
   - Adobe Analytics

## Acesso ao JupyterLab e ao serviço de Query

1. Na Plataforma [de experiência](https://platform.adobe.com), navegue até **Modelos** na coluna de navegação esquerda. Clique em **Notebooks** no cabeçalho superior para abrir JupyterLab. Aguarde um momento para o JupyterLab carregar.

   ![](../images/jupyterlab/query/notebook_ui.png)

   > [!NOTE] Se uma nova guia Iniciador não for exibida automaticamente, abra uma nova guia Iniciador clicando em **Arquivo > Novo Iniciador**.

2. Na guia Iniciador, clique no ícone **Em branco** em um ambiente Python 3 para abrir um bloco de anotações vazio.

   ![](../images/jupyterlab/query/blank_notebook.png)

   > [!NOTE] O Python 3 é atualmente o único ambiente suportado para o Serviço de Query nos notebooks.

3. No painel de seleção esquerdo, clique no ícone **Dados** e no duplo clique no diretório **Conjuntos** de dados para lista de todos os conjuntos de dados.

   ![](../images/jupyterlab/query/dataset.png)

4. Encontre um conjunto de dados do Adobe Analytics para explorar e clique com o botão direito do mouse na listagem. Clique em Dados do **Query no Bloco de Notas** para gerar query SQL no bloco de notas vazio.

5. Clique na primeira célula gerada que contém a função `qs_connect()` e execute-a clicando no botão Reproduzir. Essa função cria uma conexão entre a instância do seu notebook e o Serviço de Query.

   ![](../images/jupyterlab/query/execute.png)

6. Copie o nome do conjunto de dados do Adobe Analytics do segundo query SQL gerado, ele será o valor depois `FROM`.

   ![](../images/jupyterlab/query/dataset_name.png)

7. Insira uma nova célula do bloco de anotações clicando no botão **+** .

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

   - `target_table` : Nome do conjunto de dados do Adobe Analytics.
   - `target_year` : Ano específico a partir do qual se baseiam os dados do público alvo.
   - `target_month` : Mês específico do qual o público alvo é originário.
   - `target_day` : Dia específico do qual os dados do público alvo são originários.
   >[!NOTE] É possível alterar esses valores a qualquer momento. Ao fazer isso, certifique-se de executar a célula de variáveis para que as alterações sejam aplicadas.

## Query de seus dados

Insira os seguintes query SQL em células individuais do bloco de notas. Execute um query clicando em sua célula e depois clicando no botão **reproduzir** . Os resultados do query bem-sucedidos ou os registros de erros são exibidos abaixo da célula executada.

Quando um notebook está inativo por um longo período de tempo, a conexão entre o serviço de notebook e o serviço de Query pode falhar. Nesses casos, reinicie o JupyterLab clicando no botão **Liga/desliga** localizado no canto superior direito.

![](../images/jupyterlab/query/restart_button.png)

O kernel do notebook será redefinido, mas as células permanecerão, execute novamente **todas** as células para continuar onde você parou.

### Contagem horária de visitantes

O query a seguir retorna a contagem de visitantes por hora para uma data especificada:

#### Consulta

```sql
%%read_sql hourly_visitor -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                               AS Day,
       Substring(timestamp, 12, 2)                               AS Hour, 
       Count(DISTINCT concat(enduserids._experience.aaid.id, 
                             _experience.analytics.session.num)) AS Visit_Count 
FROM   {target_table}
WHERE _acp_year = {target_year} 
      AND _acp_month = {target_month}  
      AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

No query acima, o público alvo `_acp_year` na cláusula `WHERE` é definido como o valor de `target_year`. Inclua variáveis em query SQL, contendo-as entre chaves (`{}`).

A primeira linha do query contém a variável opcional `hourly_visitor`. Os resultados do Query serão armazenados nessa variável como um dataframe de Pandas. Armazenar resultados em um dataframe permite visualizar posteriormente os resultados do query usando um pacote Python desejado. Execute o seguinte código Python em uma nova célula para gerar um gráfico de barras:

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

### Contagem de atividades por hora

O query a seguir retorna a contagem de ações por hora para uma data especificada:

#### Consulta <!-- omit in toc -->

```sql
%%read_sql hourly_actions -d -c QS_CONNECTION
SELECT Substring(timestamp, 1, 10)                        AS Day,
       Substring(timestamp, 12, 2)                        AS Hour, 
       Count(concat(enduserids._experience.aaid.id, 
                    _experience.analytics.session.num,
                    _experience.analytics.session.depth)) AS Count 
FROM   {target_table}
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP  BY Day, Hour
ORDER  BY Hour;
```

A execução do query acima armazenará os resultados `hourly_actions` como um dataframe. Execute a seguinte função em uma nova célula para pré-visualização dos resultados:

```python
hourly_actions.head()
```

O query acima pode ser modificado para retornar a contagem de ações por hora para um intervalo de datas especificado usando operadores lógicos na cláusula **WHERE** :

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

A execução do query modificado armazenará os resultados `hourly_actions_date_range` como um dataframe. Execute a seguinte função em uma nova célula para pré-visualização dos resultados:

```python
hourly_actions_date_rage.head()
```

### Número de eventos por sessão de visitante

O query a seguir retorna o número de eventos por sessão de visitante para uma data especificada:

#### Consulta <!-- omit in toc -->

```sql
%%read_sql events_per_session -c QS_CONNECTION
SELECT concat(enduserids._experience.aaid.id, 
              '-#', 
              _experience.analytics.session.num) AS aaid_sess_key, 
       Count(timestamp)                          AS Count 
FROM   {target_table}
WHERE  _acp_year = {target_year} 
       AND _acp_month = {target_month}  
       AND _acp_day = {target_day}
GROUP BY aaid_sess_key
ORDER BY Count DESC;
```

Execute o seguinte código Python para gerar um histograma para o número de eventos por sessão de visita:

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

### Páginas populares de um determinado dia

O query a seguir retorna as dez páginas mais populares para uma data especificada:

#### Consulta <!-- omit in toc -->

```sql
%%read_sql popular_pages -c QS_CONNECTION
SELECT web.webpagedetails.name                 AS Page_Name, 
       Sum(web.webpagedetails.pageviews.value) AS Page_Views 
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY web.webpagedetails.name 
ORDER  BY page_views DESC 
LIMIT  10;
```

### Usuários ativos em um determinado dia

O query a seguir retorna os dez usuários mais ativos para uma data especificada:

#### Consulta <!-- omit in toc -->

```sql
%%read_sql active_users -c QS_CONNECTION
SELECT enduserids._experience.aaid.id AS aaid, 
       Count(timestamp)               AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY aaid
ORDER  BY Count DESC
LIMIT  10;
```

### Cidades ativas por atividade do usuário

O query a seguir retorna as dez cidades que estão gerando a maioria das atividades do usuário para uma data especificada:

#### Consulta <!-- omit in toc -->

```sql
%%read_sql active_cities -c QS_CONNECTION
SELECT concat(placeContext.geo.stateProvince, ' - ', placeContext.geo.city) AS state_city, 
       Count(timestamp)                                                     AS Count
FROM   {target_table}
WHERE  _acp_year = {target_year}
       AND _acp_month = {target_month}
       AND _acp_day = {target_day}
GROUP  BY state_city
ORDER  BY Count DESC
LIMIT  10;
```

## Próximas etapas <!-- omit in toc -->

Este tutorial demonstrou alguns casos de uso do Serviço de Query em notebooks de Júpiter. Siga o tutorial [Analisar seus dados usando Notebooks](./analyze-your-data.md) de Júpiter para ver como operações semelhantes são executadas usando o SDK de Acesso a Dados.