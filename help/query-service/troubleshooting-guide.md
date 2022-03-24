---
keywords: Experience Platform, home, tópicos populares, serviço de consulta, serviço de consulta, guia de solução de problemas, perguntas frequentes, solução de problemas;
solution: Experience Platform
title: Guia de solução de problemas do serviço de query
topic-legacy: troubleshooting
description: Este documento contém informações sobre códigos de erro comuns encontrados e as possíveis causas.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: a6924a1018d5dd4e3f03b3d8b6375cacb450a4f5
workflow-type: tm+mt
source-wordcount: '3413'
ht-degree: 1%

---

# [!DNL Query Service] guia de solução de problemas

Este documento fornece respostas a perguntas frequentes sobre o Serviço de query e fornece uma lista de códigos de erro vistos com frequência ao usar o Serviço de query. Para dúvidas e solução de problemas relacionados a outros serviços na Adobe Experience Platform, consulte a [Guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

A lista de respostas a perguntas frequentes a seguir está dividida nas seguintes categorias:

- [Geral](#general)
- [Exportar dados](#exporting-data)
- [Ferramentas de terceiros](#third-party-tools)
- [Erros da API PostgreSQL](#postgresql-api-errors)
- [Erros da API REST](#rest-api-errors)

## Perguntas gerais sobre o Serviço de query {#general}

Esta seção inclui informações sobre desempenho, limites e processos.

### Posso desativar o recurso de preenchimento automático no Editor do serviço de consulta?

+++Nº Resposta No momento, a desativação do recurso de preenchimento automático não é compatível com o editor.
+++

### Por que o Editor de consultas às vezes fica lento quando eu digito em uma consulta?

+++Resposta Uma causa potencial é o recurso de preenchimento automático. O recurso processa determinados comandos de metadados que podem, ocasionalmente, atrasar o editor durante a edição da consulta.
+++

### Posso usar o Postman para a API do serviço de consulta?

+++Responda Sim, você pode visualizar e interagir com todos os serviços de API do Adobe usando o Postman (um aplicativo gratuito de terceiros). Observe a [Guia de configuração do Postman](https://video.tv.adobe.com/v/28832) para obter instruções passo a passo sobre como configurar um projeto no Console do desenvolvedor do Adobe e adquirir todas as credenciais necessárias para uso com o Postman. Veja a documentação oficial para [orientação sobre como iniciar, executar e compartilhar coleções de Postman](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### Existe um limite para o número máximo de linhas retornadas de um query por meio da interface do usuário?

+++Responder Sim, o Serviço de Consulta aplica internamente um limite de 50.000 linhas, a menos que um limite explícito seja especificado externamente. Veja as orientações em [execução de query interativa](./best-practices/writing-queries.md#interactive-query-execution) para obter mais detalhes.
+++

### Existe um limite de tamanho de dados para a saída resultante de um query?

+++Nº Resposta Não há limite para o tamanho dos dados, mas há um limite de tempo limite de consulta de 10 minutos de uma sessão interativa. Se a consulta for executada como CTAS em lote, não será aplicável um tempo limite de 10 minutos. Veja as orientações em [execução de query interativa](./best-practices/writing-queries.md#interactive-query-execution) para obter mais detalhes.
+++

### Como eu ignoro o limite no número de saída de linhas de uma consulta SELECT?

+++Resposta Para ignorar o limite da linha de saída, aplique &quot;LIMITE 0&quot; na query. Por exemplo:

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### Como impedir que minhas consultas atinjam o tempo limite em 10 minutos?

+++Responda Uma ou mais das seguintes soluções são recomendadas no caso de consultas expirarem.

- [Converter a consulta em uma consulta CTAS](./sql/syntax.md#create-table-as-select) e agendar a execução. O agendamento de uma execução pode ser feito [por meio da interface do usuário](./ui/user-guide.md#scheduled-queries) ou [API](./api/scheduled-queries.md#create).
- Execute o query em um bloco de dados menor aplicando [condições de filtro](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [Execute o comando EXPLAIN](./sql/syntax.md#explain) para obter mais detalhes.
- Revise as estatísticas dos dados no conjunto de dados.
- Converta a consulta em um formulário simplificado e execute novamente usando [instruções preparadas](./sql/prepared-statements.md).
+++

### Existe algum problema ou impacto no desempenho do Serviço de query se várias consultas forem executadas simultaneamente?

+++Nº Resposta O Serviço de query tem um recurso de dimensionamento automático que garante que as consultas simultâneas não tenham impacto notório no desempenho do serviço.
+++

### Como faço para encontrar um nome de coluna em um conjunto de dados hierárquico?

+++Resposta As etapas a seguir descrevem como exibir uma visualização tabular de um conjunto de dados por meio da interface do usuário, incluindo todos os campos e colunas aninhados em um formulário nivelado.

- Depois de fazer logon no Experience Platform, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda da interface do usuário para navegar até [!UICONTROL Conjuntos de dados] painel.
- Os conjuntos de dados [!UICONTROL Procurar] será aberta. Use a barra de pesquisa para refinar as opções disponíveis. Selecione um conjunto de dados na lista exibida.

![Um conjunto de dados destacado na interface do usuário da plataforma.](./images/troubleshooting/dataset-selection.png)

- O [!UICONTROL Atividade dos conjuntos de dados] será exibida. Selecionar [!UICONTROL Visualizar conjunto de dados] para abrir uma caixa de diálogo do esquema XDM e exibição tabular de dados nivelados do conjunto de dados selecionado. Mais detalhes podem ser encontrados no [visualizar uma documentação do conjunto de dados](../catalog/datasets/user-guide.md#preview-a-dataset)

![O esquema XDM e a exibição tabular dos dados nivelados.](./images/troubleshooting/dataset-preview.png)

- Selecione qualquer campo do esquema para exibir seu conteúdo em uma coluna nivelada. O nome da coluna é exibido acima de seu conteúdo no lado direito da página. Você deve copiar esse nome para usar para consultar esse conjunto de dados.

![O nome da coluna de um conjunto de dados aninhado destacado na interface do usuário.](./images/troubleshooting/column-name.png)

Consulte a documentação para obter orientação completa sobre [como trabalhar com estruturas de dados aninhadas](./best-practices/nested-data-structures.md) usando o Editor de consultas ou um cliente de terceiros.
+++

### Como acelerar um query em um conjunto de dados que contém arrays?

+++Resposta Para melhorar o desempenho de consultas em conjuntos de dados que contêm matrizes, você deve [explodir o storage](https://spark.apache.org/docs/latest/api/sql/index.html#explode) como [Consulta CTAS](./sql/syntax.md#create-table-as-select) no tempo de execução e, em seguida, explorá-lo para obter mais oportunidades de melhorar seu tempo de processamento.
+++

### Por que meu query CTAS ainda está processando após muitas horas por apenas um pequeno número de linhas?

+++Resposta Se a consulta tiver demorado muito tempo em um conjunto de dados muito pequeno, entre em contato com o suporte ao cliente.

Pode haver vários motivos para uma consulta ficar paralisada durante o processamento. Para determinar a causa exata, é necessária uma análise detalhada, caso a caso. [Entre em contato com o suporte ao cliente Adobe](#customer-support) para ser esse processo.
+++

### Como entrar em contato com o suporte ao cliente do Adobe? {#customer-support}

+++Resposta
[Uma lista completa dos números de telefone do suporte ao cliente do Adobe](https://helpx.adobe.com/ca/contact/phone.html) está disponível na página de ajuda do Adobe. Como alternativa, a ajuda pode ser encontrada online, completando as seguintes etapas:

- Navegar para [https://www.adobe.com/](https://www.adobe.com/) no navegador da Web.
- No lado direito da barra de navegação superior, selecione **[!UICONTROL Fazer logon]**.

![O site do Adobe com logon foi destacado.](./images/troubleshooting/adobe-sign-in.png)

- Use a Adobe ID e a senha registradas com a licença do Adobe.
- Selecionar **[!UICONTROL Ajuda e suporte]** na barra de navegação superior.

![O menu suspenso da barra de navegação superior com ajuda e suporte destacado.](./images/troubleshooting/help-and-support.png)

Um banner suspenso é exibido contendo um [!UICONTROL Ajuda e suporte] seção. Selecionar **[!UICONTROL Entre em contato conosco]** para abrir o Adobe Customer Care Virtual Assistant ou selecione **[!UICONTROL Suporte empresarial]** para obter ajuda dedicada para grandes organizações.
+++

### Como implementar uma série sequencial de tarefas, sem executar tarefas subsequentes se o trabalho anterior não for concluído com êxito?

+++Answer O recurso de bloco anônimo permite encadear uma ou mais instruções SQL que são executadas em sequência. Permitem também a opção de tratamento de exceções.

Consulte a [documentação de bloco anônimo](./best-practices/anonymous-block.md) para obter mais detalhes.
+++

### Como implementar atribuição personalizada no Serviço de query?

+++Resposta Há duas maneiras de implementar a atribuição personalizada:

1. Usar uma combinação de [Funções definidas por Adobe](./sql/adobe-defined-functions.md) para identificar se as necessidades do caso de uso são atendidas.
1. Se a sugestão anterior não atender ao seu caso de uso, você deve usar uma combinação de [funções da janela](./sql/adobe-defined-functions.md#window-functions). As funções de janela observam todos os eventos em uma sequência. Eles também permitem revisar os dados históricos e podem ser usados em qualquer combinação.
+++

### Posso modelar minhas consultas para poder reutilizá-las facilmente?

+++Responder Sim, você pode modelar consultas usando instruções preparadas. As instruções preparadas podem otimizar o desempenho e evitar a reanálise repetitiva de uma consulta. Consulte a [documentação de instruções preparadas](./sql/prepared-statements.md) para obter mais detalhes.
+++

### Como faço para recuperar registros de erros para uma consulta? {#error-logs}

+++Resposta Para recuperar os registros de erro de uma consulta específica, primeiro use a API do Serviço de Consulta para buscar os detalhes do log de consulta. A resposta HTTP contém as IDs de consulta necessárias para investigar um erro de consulta.

Use o comando GET para recuperar várias consultas. Informações sobre como fazer uma chamada para a API podem ser encontradas no [exemplo de documentação de chamadas de API](./api/queries.md#sample-api-calls).

Na resposta, identifique a consulta que deseja investigar e faça outra solicitação do GET usando seu `id` valor. Instruções completas podem ser encontradas no [recuperar uma consulta por documentação de ID](./api/queries.md#retrieve-a-query-by-id).

Uma resposta bem-sucedida retorna o status HTTP 200 e contém a variável `errors` matriz. A resposta foi resumida por brevidade.

```json
{
    "isInsertInto": false,
    "request": {
                "dbName": "prod:all",
                "sql": "SELECT *\nFROM\n  accounts\nLIMIT 10\n"
            },
    "clientId": "8c2455819a624534bb665c43c3759877",
    "state": "SUCCESS",
    "rowCount": 0,
    "errors": [{
      'code': '58000', 
      'message': 'Batch query execution gets : [failed reason ErrorCode: 58000 Batch query execution gets : [Analysis error encountered. Reason: [sessionId: f055dc73-1fbd-4c9c-8645-efa609da0a7b Function [varchar] not defined.]]]', 
      'errorType': 'USER_ERROR'
      }],
    "isCTAS": false,
    "version": 1,
    "id": "343388b0-e0dd-4227-a75b-7fc945ef408a",
}
```

O [Documentação de referência da API do Serviço de query](https://www.adobe.io/experience-platform-apis/references/query-service/) O fornece mais informações sobre todos os endpoints disponíveis.
+++

### O que significa &quot;Erro ao validar esquema&quot;?

+++Answer A mensagem &quot;Erro ao validar esquema&quot; significa que o sistema não consegue localizar um campo dentro do esquema. Você deve ler o documento de práticas recomendadas para [organização de ativos de dados no Serviço de query](./best-practices/organize-data-assets.md) seguido pelo [Criar tabela como documentação selecionada](./sql/syntax.md#create-table-as-select).

O exemplo a seguir demonstra o uso de uma sintaxe CTAS e um tipo de dados struct:

```sql
CREATE TABLE table_name WITH (SCHEMA='schema_name')

AS SELECT '1' as _id,

 STRUCT

  ('2021-02-17T15:39:29.0Z' AS taskActualCompletionDate,

    '2020-09-09T21:21:16.0Z' AS taskActualStartDate,

    'Consulting' AS taskdescription,

    '5f6527c10011e09b89666c52d9a8c564' AS taskguide,

    'Stakeholder Consulting Engagement' AS taskname, 

    '2020-09-09T15:00:00.0Z' AS taskPlannedStartDate,

    '2021-02-15T11:00:00.0Z' AS taskPlannedCompletionDate

  ) AS _workfront ;
```

+++

### Como posso processar rapidamente os novos dados que entram no sistema todos os dias?

+++Responda O [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) A cláusula pode ser usada para ler dados de forma incremental em uma tabela com base em uma ID de instantâneo. Isso é ideal para ser usado com o [carga incremental](./best-practices/incremental-load.md) padrão de design que processa apenas as informações no conjunto de dados que foram criadas ou modificadas desde a última execução do carregamento. Como resultado, ele aumenta a eficiência do processamento e pode ser usado com streaming e processamento de dados em lote.
+++

### Por que há uma diferença entre os números mostrados na interface do usuário do perfil e os números calculados do conjunto de dados de exportação do perfil?

+++Resposta Os números exibidos no painel de perfil são precisos a partir do último instantâneo. Os números gerados na tabela de exportação de perfil dependem totalmente do query de exportação. Como resultado, consultar o número de perfis qualificados para um segmento específico é uma causa comum para essa discrepância.

>[!NOTE]
>
>A consulta inclui dados históricos, enquanto a interface do usuário exibe apenas os dados de perfil atuais.

+++

### Por que minha query retornou um subconjunto vazio e o que devo fazer?

+++Resposta A causa mais provável é que sua consulta é de escopo muito restrito. Você deve remover sistematicamente uma seção da variável `WHERE` até começar a ver alguns dados.

Também é possível confirmar se o conjunto de dados contém dados usando uma pequena query como:

```sql
SELECT count(1) FROM myTableName
```

+++

### Posso obter uma amostra dos meus dados?

+++Resposta No momento, esse recurso está em andamento. Os detalhes serão disponibilizados em [notas de versão](../release-notes/latest/latest.md) e por meio de caixas de diálogo da interface do usuário da plataforma, assim que o recurso estiver pronto para lançamento.
+++

### Quais funções auxiliares são suportadas pelo Serviço de Consulta?

+++Answer Query Service fornece várias funções auxiliares SQL incorporadas para estender a funcionalidade SQL. Consulte o documento para obter uma lista completa dos [Funções SQL suportadas pelo Serviço de Consulta](./sql/spark-sql-functions.md).
+++

### O que devo fazer se minha consulta agendada falhar?

+++Responda primeiro, marque os logs para descobrir os detalhes do erro. A seção de perguntas frequentes sobre [detecção de erros nos logs](#error-logs) O fornece mais informações sobre como fazer isso.

Você também deve verificar a documentação para obter orientação sobre como executar o [consultas agendadas na interface do usuário](./ui/user-guide.md#scheduled-queries) e [a API](./api/scheduled-queries.md).
+++

### O que significa o erro &quot;Limite de sessão atingido&quot;?

+++Responder &quot;Limite de Sessão Atingido&quot; significa que o número máximo de sessões do Serviço de Consulta permitido para sua organização foi atingido. Entre em contato com o administrador da Adobe Experience Platform de sua organização.
+++

### Como o log de consultas lida com consultas relacionadas a um conjunto de dados excluído?

+++Answer Query Service nunca exclui o histórico de consultas. Isso significa que qualquer query que referencie um conjunto de dados excluído retornaria &quot;Nenhum conjunto de dados válido&quot; como resultado.
+++

### Como posso obter apenas os metadados para um query?

+++Resposta Você pode executar uma consulta que retorna zero linhas para obter apenas os metadados em resposta. Esse exemplo de query retorna somente os metadados da tabela especificada.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### Como posso iterar rapidamente em uma consulta CTAS (Criar Tabela Como Selecionar) sem materializá-la?

+++Resposta Você pode criar tabelas temporárias para iterar e experimentar rapidamente em uma consulta antes de materializá-la para uso. Você também pode usar tabelas temporárias para validar se um query é funcional.

Por exemplo, é possível criar uma tabela temporária:

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

Em seguida, é possível usar a tabela temporária da seguinte maneira:

```sql
INSERT INTO temp_dataset
SELECT a._company AS _company,
a._id AS _id,
a.timestamp AS timestamp
FROM actual_dataset a
WHERE timestamp >= TO_TIMESTAMP('2021-01-21 12:00:00')
AND timestamp < TO_TIMESTAMP('2021-01-21 13:00:00')
LIMIT 100;
```

+++

### Como faço para alterar o fuso horário de e para um carimbo de data e hora UTC?

+++Answer Adobe Experience Platform persiste dados no formato de carimbo de data e hora UTC (Tempo Universal Coordenado). Um exemplo do formato UTC é `2021-12-22T19:52:05Z`

O Serviço de Consulta suporta funções SQL incorporadas para converter um determinado carimbo de data e hora para e a partir do formato UTC. Ambos os `to_utc_timestamp()` e `from_utc_timestamp()` os métodos utilizam dois parâmetros: carimbo de data e hora e fuso horário.

| Parâmetro | Descrição |
|-----------|---------------|
| Carimbo de data e hora | O carimbo de data e hora pode ser gravado no formato UTC ou em formato simples `{year-month-day}` formato. Se nenhuma hora for fornecida, o valor padrão será meia-noite na manhã do dia em questão. |
| Fuso horário | O fuso horário é gravado em um `{continent/city})` formato. Ele deve ser um dos códigos de fuso horário reconhecidos, conforme encontrado no [banco de dados TZ de domínio público](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### Converter para o carimbo de data e hora UTC

O `to_utc_timestamp()` O método interpreta os parâmetros fornecidos e os converte **para o carimbo de data e hora do fuso horário local** no formato UTC. Por exemplo, o fuso horário em Seul, Coreia do Sul é UTC/GMT +9 horas. Ao fornecer um carimbo de data e hora somente, o método usa um valor padrão de meia-noite de manhã. O carimbo de data e hora e o fuso horário são convertidos no formato UTC do momento dessa região para um carimbo de data e hora UTC da região local.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

O query retorna um carimbo de data e hora no horário local do usuário. Nesse caso, 15:00 PM no dia anterior como Seul está nove horas à frente.

```
2021-08-30 15:00:00
```

Como outro exemplo, se o carimbo de data e hora especificado foi `2021-07-14 12:40:00.0` para `Asia/Seoul` fuso horário, o carimbo de data e hora UTC retornado seria `2021-07-14 03:40:00.0`

A saída do console fornecida na interface do usuário do Serviço de query é um formato mais legível:

```
8/30/2021, 3:00 PM
```

#### Converter a partir do carimbo de data e hora UTC

O `from_utc_timestamp()` O método interpreta os parâmetros fornecidos **no carimbo de data e hora do fuso horário local** e fornece o carimbo de data e hora equivalente da região desejada no formato UTC. No exemplo abaixo, a hora é 2:40 PM no fuso horário local do usuário. O fuso horário de Seul passado como uma variável está nove horas antes do fuso horário local.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

O query retorna um carimbo de data e hora em formato UTC para o fuso horário passado como parâmetro. O resultado é nove horas antes do fuso horário que executou o query.

```
8/31/2021, 11:40 PM
```

### Como devo filtrar os dados das séries de tempo?

+++Resposta Ao consultar os dados da série de tempo, você deve usar o filtro de carimbo de data e hora sempre que possível para obter uma análise mais precisa.

>[!NOTE]
>
> A string de data **must** estar no formato `yyyy-mm-ddTHH24:MM:SS`.

Um exemplo de uso do filtro de carimbo de data e hora pode ser visto abaixo:

```sql
SELECT a._company  AS _company,
       a._id       AS _id,
       a.timestamp AS timestamp
FROM   dataset a
WHERE  timestamp >= To_timestamp('2021-01-21 12:00:00')
       AND timestamp < To_timestamp('2021-01-21 13:00:00')
```

+++

### Como usar corretamente a variável `CAST` operador para converter meus carimbos de data e hora em consultas SQL?

+++Responder ao usar o `CAST` para converter um carimbo de data e hora, é necessário incluir a data **e** hora.

Por exemplo, a falta do componente de tempo, como mostrado abaixo, resultará em um erro:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

O uso correto da variável `CAST` O operador é mostrado abaixo:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### Devo usar curingas, como *, para obter todas as linhas dos meus conjuntos de dados?

+++Resposta Não é possível usar curingas para obter todos os dados de suas linhas, pois o Serviço de query deve ser tratado como um **columnar-store** em vez de um sistema de armazenamento tradicional baseado em linha.
+++

### Devo usar `NOT IN` na minha consulta SQL?

+++Responda O `NOT IN` O operador é frequentemente usado para recuperar linhas que não são encontradas em outra tabela ou instrução SQL. Esse operador pode retardar o desempenho e retornar resultados inesperados se as colunas que estão sendo comparadas aceitarem `NOT NULL`ou você tiver grandes números de registros.

Em vez de usar `NOT IN`, você pode usar `NOT EXISTS` ou `LEFT OUTER JOIN`.

Por exemplo, se você tiver criado as seguintes tabelas:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Se estiver usando o `NOT EXISTS` , você pode replicar usando o `NOT IN` usando a seguinte query:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Como alternativa, se estiver usando o `LEFT OUTER JOIN` , você pode replicar usando o `NOT IN` usando a seguinte query:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

## Exportar dados {#exporting-data}

Esta seção fornece informações sobre exportação de dados e limites.

### Existe uma maneira de extrair dados do Serviço de query após o processamento de query e salvar os resultados em um arquivo CSV?

+++Resposta Sim. Os dados podem ser extraídos do Serviço de query e também há a opção de armazenar os resultados no formato CSV por meio de um comando SQL.

Há duas maneiras de salvar os resultados de um query ao usar um cliente PSQL. Você pode usar o `COPY TO` ou crie uma instrução usando o seguinte formato:

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[Orientações sobre a utilização da `COPY TO` comando](./sql/syntax.md#copy) pode ser encontrado na documentação de referência da sintaxe SQL.
+++

### Posso extrair o conteúdo do conjunto de dados final que foi assimilado por meio de consultas CTAS (supondo que sejam quantidades maiores de dados, como Terabytes)?

+++Nº Resposta No momento, não há nenhum recurso disponível para a extração de dados assimilados.
+++

## Ferramentas de terceiros {#third-party-tools}

Esta seção inclui informações sobre o uso de ferramentas de terceiros, como PSQL e Power BI.

### Posso conectar o Serviço de Consulta a uma ferramenta de terceiros?

+++Responda Sim, você pode conectar vários clientes de desktop de terceiros ao Serviço de query. Consulte a documentação para [detalhes completos sobre os clientes disponíveis e como conectá-los ao serviço Query](./clients/overview.md).
+++

### Existe uma maneira de conectar o Serviço de query uma vez para uso contínuo com uma ferramenta de terceiros?

+++Responda Sim, os clientes de desktop de terceiros podem ser conectados ao Serviço de query por meio de uma configuração única de credenciais que não estão expirando. As credenciais que não expiram podem ser geradas por um usuário autorizado e as receberão em um arquivo JSON baixado em sua máquina local. Total [orientação sobre como criar e baixar credenciais que não expiram](./ui/credentials.md#non-expiring-credentials) pode ser encontrada na documentação do .
+++

### Que tipo de editores SQL de terceiros posso conectar ao Editor do Serviço de Consultas?

+++Answer Qualquer editor SQL de terceiros que seja PSQL ou [!DNL Postgres] A conformidade com o cliente pode ser conectada ao Editor do Serviço de Consulta. Consulte a documentação para [conectando clientes ao Serviço de query](./clients/overview.md) para obter uma lista de instruções disponíveis.
+++

### Posso conectar a ferramenta Power BI ao Serviço de query?

+++Responda Sim, você pode conectar o Power BI ao Serviço de Consulta. Consulte a documentação para [instruções sobre como conectar o aplicativo de desktop do Power BI ao Serviço de query](./clients/power-bi.md).
+++

### Por que os painéis levam muito tempo para serem carregados quando conectados ao Serviço de query?

+++Resposta Quando o sistema está conectado ao Serviço de Consulta, ele é conectado a um mecanismo de processamento interativo ou em lote. Isso pode resultar em tempos de carregamento mais longos para refletir os dados processados.

Se quiser melhorar os tempos de resposta dos painéis, é necessário implementar um servidor do Business Intelligence (BI) como uma camada de armazenamento em cache entre o Serviço de query e as ferramentas de BI. Geralmente, a maioria das ferramentas de BI tem uma oferta adicional para um servidor.

A finalidade de adicionar a camada do servidor de cache é armazenar os dados em cache do Serviço de query e utilizar o mesmo para os painéis para acelerar a resposta. Isso é possível, pois os resultados de consultas que são executadas seriam armazenados em cache no servidor BI todos os dias. O servidor de cache fornece esses resultados para qualquer usuário com a mesma consulta para diminuir a latência. Consulte a documentação do utilitário ou da ferramenta de terceiros que você está usando para obter esclarecimentos sobre essa configuração.
+++

### É possível acessar o Serviço de query usando a ferramenta de conexão pgAdmin?

+++Nº da resposta, a conectividade pgAdmin não é suportada. A [lista de clientes de terceiros disponíveis e instruções sobre como conectá-los ao Serviço de query](./clients/overview.md) pode ser encontrada na documentação do .
+++

## Erros da API PostgreSQL {#postgresql-api-errors}

A tabela a seguir fornece códigos de erro PSQL e suas possíveis causas.

| Código de erro | Estado da conexão | Descrição | Causa possível |
|------------|---------------------------|-------------|----------------|
| **08P01** | N/D | Tipo de mensagem não suportado | Tipo de mensagem não suportado |
| **28P01** | Iniciar - autenticação | Senha inválida | Token de autenticação inválido |
| **28000** | Iniciar - autenticação | Tipo de autorização inválido | Tipo de autorização inválido. Deve ser `AuthenticationCleartextPassword`. |
| **42P12** | Iniciar - autenticação | Nenhuma tabela encontrada | Nenhuma tabela encontrada para uso |
| **42601** | Consulta | Erro de sintaxe | Comando ou erro de sintaxe inválido |
| **42P01** | Consulta | Tabela não encontrada | A tabela especificada na consulta não foi encontrada |
| **42P07** | Consulta | Tabela existe | Já existe uma tabela com o mesmo nome (CRIAR TABELA) |
| **53400** | Consulta | LIMITE excede o valor máximo | O usuário especificou uma cláusula LIMIT superior a 100.000 |
| **53400** | Consulta | Tempo limite do demonstrativo | A declaração ao vivo enviada demorou mais de 10 minutos |
| **58000** | Consulta | Erro do sistema | Falha do sistema interno |
| **0A000** | Query/Comando | Não suportado | Não há suporte para o recurso/funcionalidade no query/comando |
| **42501** | Consulta DROP TABLE | Eliminar tabela não criada pelo Serviço de Consulta | A tabela que está sendo solta não foi criada pelo Serviço de Consulta usando o `CREATE TABLE` declaração |
| **42501** | Consulta DROP TABLE | Tabela não criada pelo usuário autenticado | A tabela que está sendo solta não foi criada pelo usuário conectado no momento |
| **42P01** | Consulta DROP TABLE | Tabela não encontrada | A tabela especificada na consulta não foi encontrada |
| **42P12** | Consulta DROP TABLE | Nenhuma tabela encontrada para `dbName`: verifique o `dbName` | Nenhuma tabela foi encontrada no banco de dados atual |

### Por que recebi um código de erro 58000 ao usar o método history_meta() na minha tabela?

+++Responda O `history_meta()` é usado para acessar um instantâneo de um conjunto de dados. Anteriormente, se você executasse uma consulta em um conjunto de dados vazio no Armazenamento Azure Data Lake (ADLS), você receberia um código de erro 58000 informando que o conjunto de dados não existe. Um exemplo do erro de sistema antigo é exibido abaixo.

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

Este erro ocorreu porque não havia um valor de retorno para a consulta. Esse comportamento foi corrigido para retornar a seguinte mensagem:

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## Erros da API REST {#rest-api-errors}

A tabela a seguir fornece códigos de erro HTTP e suas possíveis causas.

| Código do status HTTP | Descrição | Possíveis causas |
|------------------|-----------------------|----------------------------|
| 400 | Solicitação inválida | Consulta malformada ou ilegal |
| 401° | Falha na autenticação | Token de autenticação inválido |
| 500 | Erro interno do servidor | Falha do sistema interno |
