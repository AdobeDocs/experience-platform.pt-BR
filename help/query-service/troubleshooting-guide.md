---
keywords: Experience Platform;página inicial;tópicos populares;serviço de consulta;serviço de consulta;guia de solução de problemas;perguntas frequentes;solução de problemas;
solution: Experience Platform
title: Perguntas frequentes
description: Este documento contém perguntas e respostas comuns relacionadas ao Serviço de consulta. Os tópicos incluem exportação de dados, ferramentas de terceiros e erros de PSQL.
exl-id: 14cdff7a-40dd-4103-9a92-3f29fa4c0809
source-git-commit: e59def7a05862ad880d0b6ada13b1c69c655ff90
workflow-type: tm+mt
source-wordcount: '4309'
ht-degree: 1%

---

# Perguntas frequentes

Este documento fornece respostas a perguntas frequentes sobre o Serviço de consulta e fornece uma lista de códigos de erro vistos com frequência ao usar o Serviço de consulta. Para perguntas e soluções de problemas relacionados a outros serviços na Adobe Experience Platform, consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

A lista de respostas a seguir para perguntas frequentes está dividida nas seguintes categorias:

- [Geral](#general)
- [Exportar dados](#exporting-data)
- [Ferramentas de terceiros](#third-party-tools)
- [Erros de API PostgreSQL](#postgresql-api-errors)
- [Erros de REST API](#rest-api-errors)

## Perguntas gerais do Serviço de consulta {#general}

Esta seção inclui informações sobre desempenho, limites e processos.

### Posso desativar o recurso de preenchimento automático no Editor do serviço de consulta?

+++Número de resposta No momento, o editor não oferece suporte à desativação do recurso de preenchimento automático.
+++

### Por que o Editor de consultas às vezes fica lento quando digito uma consulta?

+++Resposta Uma causa potencial é o recurso de preenchimento automático. O recurso processa determinados comandos de metadados que podem retardar ocasionalmente o editor durante a edição de consultas.
+++

### Posso usar [!DNL Postman] para a API do Serviço de consulta?

+++Responda Sim, você pode visualizar e interagir com todos os serviços de API do Adobe usando [!DNL Postman] (um aplicativo gratuito de terceiros). Assista ao [[!DNL Postman] guia de configuração](https://video.tv.adobe.com/v/28832) para obter instruções passo a passo sobre como configurar um projeto no Adobe Developer Console e adquirir todas as credenciais necessárias para uso com o [!DNL Postman]. Consulte a documentação oficial para [orientação sobre como iniciar, executar e compartilhar [!DNL Postman] coleções](https://learning.postman.com/docs/running-collections/intro-to-collection-runs/).
+++

### Há um limite para o número máximo de linhas retornadas de uma consulta por meio da interface do usuário?

+++Resposta Sim, o Serviço de consulta aplica internamente um limite de 50.000 linhas, a menos que um limite explícito seja especificado externamente. Consulte as orientações sobre [execução de consulta interativa](./best-practices/writing-queries.md#interactive-query-execution) para obter mais detalhes.
+++

### Posso usar consultas para atualizar linhas?

+++Resposta Em consultas em lote, não há suporte para a atualização de uma linha dentro do conjunto de dados.
+++

### Existe um limite de tamanho de dados para a saída resultante de um query?

+++Número de resposta Não há limite de tamanho de dados, mas há um tempo limite de consulta de 10 minutos de uma sessão interativa. Se a consulta for executada como um CTAS em lote, um tempo limite de 10 minutos não será aplicável. Consulte as orientações sobre [execução de consulta interativa](./best-practices/writing-queries.md#interactive-query-execution) para obter mais detalhes.
+++

### Como ignorar o limite no número de saída de linhas de uma consulta SELECT?

+++Responder Para ignorar o limite da linha de saída, aplique &quot;LIMIT 0&quot; na consulta. Por exemplo:

```sql
SELECT * FROM customers LIMIT 0;
```

+++

### Como faço para impedir que minhas consultas expirem em 10 minutos?

+++Resposta Uma ou mais das seguintes soluções são recomendadas no caso de consultas expirarem.

- [Converter a consulta em uma consulta CTAS](./sql/syntax.md#create-table-as-select) e agendar a execução. A programação de uma execução pode ser feita [por meio da interface](./ui/user-guide.md#scheduled-queries) ou o [API](./api/scheduled-queries.md#create).
- Executar a consulta em uma parte de dados menor aplicando [filtrar condições](https://spark.apache.org/docs/latest/api/sql/index.html#filter).
- [Execute o comando EXPLAIN](./sql/syntax.md#explain) para coletar mais detalhes.
- Revise as estatísticas dos dados no conjunto de dados.
- Converta a consulta em um formulário simplificado e execute-a novamente usando [instruções preparadas](./sql/prepared-statements.md).
+++

### Há algum problema ou impacto no desempenho do Serviço de consulta se várias consultas forem executadas simultaneamente?

+++Número de resposta O Serviço de consulta tem um recurso de dimensionamento automático que garante que as consultas simultâneas não tenham nenhum impacto observável no desempenho do serviço.
+++

### Posso usar palavras-chave reservadas como nome de coluna?

+++Resposta Há determinadas palavras-chave reservadas que não podem ser usadas como nome de coluna, como, `ORDER`, `GROUP BY`, `WHERE`, `DISTINCT`. Se quiser usar essas palavras-chave, você deve omitir essas colunas.
+++

### Como faço para localizar um nome de coluna a partir de um conjunto de dados hierárquico?

+++Resposta As etapas a seguir descrevem como exibir uma exibição em tabelas de um conjunto de dados por meio da interface do usuário, incluindo todos os campos e colunas aninhados em um formulário nivelado.

- Depois de fazer logon no Experience Platform, selecione **[!UICONTROL Conjuntos de dados]** na navegação à esquerda da interface para navegar até [!UICONTROL Conjuntos de dados] painel.
- Os conjuntos de dados [!UICONTROL Procurar] é aberta. Você pode usar a barra de pesquisa para refinar as opções disponíveis. Selecione um conjunto de dados na lista exibida.

![O painel Conjuntos de dados na interface do Platform com a barra de pesquisa e um conjunto de dados destacado.](./images/troubleshooting/dataset-selection.png)

- A variável [!UICONTROL Atividade de conjuntos de dados] é exibida. Selecionar **[!UICONTROL Visualizar conjunto de dados]** para abrir uma caixa de diálogo do esquema XDM e a exibição tabular de dados nivelados do conjunto de dados selecionado. Mais detalhes podem ser encontrados na [visualizar uma documentação do conjunto de dados](../catalog/datasets/user-guide.md#preview-a-dataset)

![A guia Atividade do conjunto de dados do painel Conjuntos de dados com o conjunto de dados Visualização realçado.](./images/troubleshooting/dataset-preview.png)

- Selecione qualquer campo do esquema para exibir seu conteúdo em uma coluna plana. O nome da coluna é exibido acima do conteúdo no lado direito da página. Você deve copiar esse nome para usar ao consultar esse conjunto de dados.

![O esquema XDM e a visualização tabular dos dados nivelados. O nome da coluna de um conjunto de dados aninhado é realçado na interface.](./images/troubleshooting/column-name.png)

Consulte a documentação para obter orientação completa sobre [como trabalhar com estruturas de dados aninhadas](./essential-concepts/nested-data-structures.md) usando o Editor de consultas ou um cliente de terceiros.
+++

### Como acelerar um query em um conjunto de dados que contém arrays?

+++Responder Para melhorar o desempenho de consultas em conjuntos de dados que contêm matrizes, você deve [explodir a matriz](https://spark.apache.org/docs/latest/api/sql/index.html#explode) as a [consulta CTAS](./sql/syntax.md#create-table-as-select) em tempo de execução e depois o explore para obter mais oportunidades de melhorar o tempo de processamento.
+++

### Por que minha consulta CTAS ainda está processando depois de muitas horas para apenas um pequeno número de linhas?

+++Resposta Se a consulta tiver demorado muito tempo em um conjunto de dados muito pequeno, entre em contato com o suporte ao cliente.

Pode haver vários motivos para uma consulta ficar paralisada durante o processamento. Determinar a causa exata requer uma análise detalhada caso a caso. [Entre em contato com o suporte ao cliente do Adobe](#customer-support) para ser esse processo.
+++

### Como entrar em contato com o suporte ao cliente do Adobe? {#customer-support}

+++Resposta
[Uma lista completa dos números de telefone do suporte ao cliente Adobe](https://helpx.adobe.com/ca/contact/phone.html) está disponível na página de ajuda do Adobe. Como alternativa, a ajuda pode ser encontrada online executando as seguintes etapas:

- Navegue até [https://www.adobe.com/](https://www.adobe.com/) no navegador da Web.
- No lado direito da barra de navegação superior, selecione **[!UICONTROL Conectar]**.

![O site do Adobe com Sign in foi destacado.](./images/troubleshooting/adobe-sign-in.png)

- Use sua Adobe ID e senha registradas com sua licença do Adobe.
- Selecionar **[!UICONTROL Ajuda e suporte]** na barra de navegação superior.

![O menu suspenso da barra de navegação superior com Ajuda e suporte, Suporte Enterprise e Fale conosco em destaque.](./images/troubleshooting/help-and-support.png)

Um banner suspenso é exibido contendo um [!UICONTROL Ajuda e suporte] seção. Selecionar **[!UICONTROL Entre em contato]** para abrir o Adobe Customer Care Virtual Assistant ou selecione **[!UICONTROL Suporte Enterprise]** para obter ajuda dedicada para grandes organizações.
+++

### Como implementar uma série sequencial de jobs sem executar jobs subsequentes se o job anterior não for concluído com sucesso?

+++Answer O recurso de bloqueio anônimo permite encadear uma ou mais instruções SQL que são executadas em sequência. Permitem também a opção de tratamento de exceções.

Consulte a [documentação de bloqueio anônimo](./essential-concepts/anonymous-block.md) para obter mais detalhes.
+++

### Como implementar a atribuição personalizada no Serviço de consulta?

+++Resposta Há duas maneiras de implementar a atribuição personalizada:

1. Usar uma combinação de [Funções definidas pelo Adobe](./sql/adobe-defined-functions.md) para identificar se as necessidades do caso de uso foram atendidas.
1. Se a sugestão anterior não atender ao seu caso de uso, use uma combinação de [funções de janela](./sql/adobe-defined-functions.md#window-functions). As funções de janela observam todos os eventos em uma sequência. Elas também permitem que você analise os dados do histórico e podem ser usados em qualquer combinação.
+++

### Posso modelar minhas consultas para reutilizá-las facilmente?

+++Resposta Sim, você pode modelar consultas usando instruções preparadas. As instruções preparadas podem otimizar o desempenho e evitar a reanálise repetitiva de uma consulta. Consulte a [documentação de instruções preparadas](./sql/prepared-statements.md) para obter mais detalhes.
+++

### Como faço para recuperar logs de erros de uma consulta? {#error-logs}

+++Resposta Para recuperar logs de erros de uma consulta específica, primeiro use a API do Serviço de Consulta para obter os detalhes do log de consulta. A resposta HTTP contém as IDs de consulta necessárias para investigar um erro de consulta.

Use o comando GET para recuperar várias consultas. Informações sobre como fazer uma chamada para a API podem ser encontradas na [documentação de chamadas de API de exemplo](./api/queries.md#sample-api-calls).

Na resposta, identifique a consulta que deseja investigar e faça outra solicitação GET usando suas `id` valor. Instruções completas podem ser encontradas no [recuperar uma consulta pela documentação de ID](./api/queries.md#retrieve-a-query-by-id).

Uma resposta bem-sucedida retorna o status HTTP 200 e contém o `errors` matriz. A resposta foi encurtada por questões de brevidade.

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

A variável [Documentação de referência da API do Serviço de consulta](https://www.adobe.io/experience-platform-apis/references/query-service/) O fornece mais informações sobre todos os endpoints disponíveis.
+++

### O que significa &quot;Erro ao validar o esquema&quot;?

+++Responder A mensagem &quot;Erro ao validar o esquema&quot; significa que o sistema não consegue localizar um campo no esquema. Você deve ler o documento de práticas recomendadas para [organização de ativos de dados no Serviço de consulta](./best-practices/organize-data-assets.md) seguido pelo [Documentação Criar tabela como selecionada](./sql/syntax.md#create-table-as-select).

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

+++Responder A [`SNAPSHOT`](./sql/syntax.md#snapshot-clause) A cláusula pode ser usada para ler incrementalmente os dados em uma tabela com base em uma ID de snapshot. Isso é ideal para uso com o [carga incremental](./essential-concepts/incremental-load.md) padrão de design que processa apenas as informações no conjunto de dados que foi criado ou modificado desde a última execução de carregamento. Como resultado, aumenta a eficiência do processamento e pode ser usado com processamento de dados em lote e de transmissão.
+++

### Por que há uma diferença entre os números mostrados na interface do usuário do perfil e os números calculados do conjunto de dados de exportação de perfil?

+++Resposta Os números exibidos no painel do perfil são precisos a partir do último instantâneo. Os números gerados na tabela de exportação de perfis dependem totalmente da consulta de exportação. Como resultado, consultar o número de perfis qualificados para um público específico é uma causa comum para essa discrepância.

>[!NOTE]
>
>A consulta inclui dados históricos, enquanto a interface do usuário exibe somente os dados do perfil atual.

+++

### Por que minha consulta retornou um subconjunto vazio e o que devo fazer?

+++Resposta A causa mais provável é que sua consulta tenha um escopo muito estreito. Você deve remover sistematicamente uma seção da `WHERE` até que você comece a ver alguns dados.

Você também pode confirmar que seu conjunto de dados contém dados usando uma pequena consulta como:

```sql
SELECT count(1) FROM myTableName
```

+++

### Posso obter amostras dos meus dados?

+++Resposta Este recurso está em andamento no momento. Os detalhes serão disponibilizados em [notas de versão](../release-notes/latest/latest.md) e pelas caixas de diálogo da interface do usuário da Platform, quando o recurso estiver pronto para lançamento.
+++

### Quais funções auxiliares são compatíveis com o Serviço de consulta?

+++O Serviço de consulta de resposta fornece várias funções auxiliares de SQL incorporadas para estender a funcionalidade SQL. Consulte o documento para obter uma lista completa dos [Funções SQL suportadas pelo Serviço de consulta](./sql/spark-sql-functions.md).
+++

### São todos nativos [!DNL Spark SQL] há suporte para funções ou os usuários estão restritos apenas ao invólucro [!DNL Spark SQL] funções fornecidas pelo Adobe?

+++Resposta Ainda não, nem todos os arquivos de código aberto [!DNL Spark SQL] As funções do foram testadas nos dados do data lake. Depois de testados e confirmados, eles serão adicionados à lista de itens com suporte. Consulte a [lista de suportados [!DNL Spark SQL] funções](./sql/spark-sql-functions.md) para verificar se há uma função específica.
+++

### Os usuários podem definir suas próprias funções definidas pelo usuário (UDF) que podem ser usadas em outras consultas?

+++Resposta Devido a considerações de segurança de dados, a definição personalizada de UDFs não é permitida.
+++

### O que devo fazer se minha consulta programada falhar?

+++Responda Primeiro, verifique os logs para descobrir os detalhes do erro. A seção de perguntas frequentes sobre [localização de erros em logs](#error-logs) A seção fornece mais informações sobre como fazer isso.

Você também deve consultar a documentação para obter orientação sobre como executar o [consultas agendadas na interface do](./ui/user-guide.md#scheduled-queries) e até [a API](./api/scheduled-queries.md).

Esteja ciente de que, ao usar [!DNL Query Editor] você só pode adicionar um agendamento a uma consulta que já tenha sido criada, salva e executada. Isso não se aplica à [!DNL Query Service] API.
+++

### O que significa o erro &quot;Limite de sessão atingido&quot;?

+++Resposta &quot;Limite de Sessão Atingido&quot; significa que o número máximo de sessões do Serviço de Consulta permitido para sua organização foi atingido. Conecte-se com o administrador do Adobe Experience Platform da sua organização.
+++

### Como o log de consultas lida com consultas relacionadas a um conjunto de dados excluído?

+++O Serviço de consulta de resposta nunca exclui o histórico de consultas. Isso significa que qualquer consulta que faça referência a um conjunto de dados excluído retornaria &quot;Nenhum conjunto de dados válido&quot; como resultado.
+++

### Como posso obter somente os metadados de um query?

+++Resposta Você pode executar uma consulta que retorna zero linhas para obter apenas os metadados na resposta. Este exemplo de consulta retorna somente os metadados da tabela especificada.

```sql
SELECT * FROM <table> WHERE 1=0
```

+++

### Como posso iterar rapidamente em uma consulta CTAS (Create Table As Select) sem materializá-la?

+++Resposta Você pode criar tabelas temporárias para iterar e experimentar rapidamente uma consulta antes de materializá-la para uso. Você também pode usar tabelas temporárias para validar se uma consulta está funcional.

Por exemplo, você pode criar uma tabela temporária:

```sql
CREATE temp TABLE temp_dataset AS
SELECT *
FROM actual_dataset
WHERE 1 = 0;
```

Em seguida, você pode usar a tabela temporária da seguinte maneira:

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

### Como alterar o fuso horário de e para um Carimbo de data e hora UTC?

+++O Adobe Experience Platform de resposta mantém os dados no formato de carimbo de data e hora UTC (Tempo universal coordenado). Um exemplo do formato UTC é `2021-12-22T19:52:05Z`

O Serviço de consulta oferece suporte a funções SQL integradas para converter um determinado carimbo de data/hora de e para o formato UTC. Ambos os `to_utc_timestamp()` e a variável `from_utc_timestamp()` Os métodos usam dois parâmetros: carimbo de data e hora e fuso horário.

| Parâmetro | Descrição |
|-----------|---------------|
| Carimbo de data e hora | O carimbo de data e hora pode ser gravado no formato UTC ou simples `{year-month-day}` formato. Se nenhuma hora for fornecida, o valor padrão será a meia-noite da manhã de um determinado dia. |
| Fuso horário | O fuso horário é gravado em um `{continent/city})` formato. Deve ser um dos códigos de fuso horário reconhecidos, conforme encontrado na [banco de dados TZ de domínio público](https://data.iana.org/time-zones/tz-link.html#tzdb). |

#### Converter para o carimbo de data e hora UTC

A variável `to_utc_timestamp()` O método interpreta os parâmetros fornecidos e os converte **ao carimbo de data e hora de seu fuso horário local** no formato UTC. Por exemplo, o fuso horário em Seul, Coreia do Sul é UTC/GMT +9 horas. Ao fornecer um carimbo de data e hora somente, o método usa um valor padrão de meia-noite da manhã. O carimbo de data e hora e o fuso horário são convertidos no formato UTC da hora dessa região para um carimbo de data e hora UTC de sua região local.

```SQL
SELECT to_utc_timestamp('2021-08-31', 'Asia/Seoul');
```

A consulta retorna um carimbo de data e hora no horário local do usuário. Neste caso, às 15h do dia anterior, enquanto Seul está nove horas à frente.

```
2021-08-30 15:00:00
```

Como outro exemplo, se o carimbo de data e hora fornecido foi `2021-07-14 12:40:00.0` para o `Asia/Seoul` fuso horário, o carimbo de data e hora UTC retornado seria `2021-07-14 03:40:00.0`

A saída do console fornecida na interface do Serviço de consulta é um formato mais legível:

```
8/30/2021, 3:00 PM
```

#### Converter do carimbo de data e hora UTC

A variável `from_utc_timestamp()` O método interpreta os parâmetros fornecidos **do carimbo de data e hora de seu fuso horário local** e fornece o carimbo de data e hora equivalente da região desejada no formato UTC. No exemplo abaixo, a hora é 14h40 no fuso horário local do usuário. O fuso horário de Seul transmitido como uma variável está nove horas à frente do fuso horário local.

```SQL
SELECT from_utc_timestamp('2021-08-31 14:40:00.0', 'Asia/Seoul');
```

A consulta retorna um carimbo de data e hora no formato UTC do fuso horário passado como parâmetro. O resultado é nove horas antes do fuso horário que executou a consulta.

```
8/31/2021, 11:40 PM
```

### Como devo filtrar meus dados de série temporal?

+++Resposta Ao consultar com dados de série temporal, você deve usar o filtro de carimbo de data e hora sempre que possível para uma análise mais precisa.

>[!NOTE]
>
> A string de data **deve** estar no formato `yyyy-mm-ddTHH24:MM:SS`.

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

+++Resposta ao usar o `CAST` operador para converter um carimbo de data e hora, é necessário incluir a data **e** hora.

Por exemplo, a falta do componente de tempo, como mostrado abaixo, resultará em um erro:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021' AS timestamp)
```

O uso correto do `CAST` operador é mostrado abaixo:

```sql
SELECT * FROM ABC
WHERE timestamp = CAST('07-29-2021 00:00:00' AS timestamp)
```

+++

### Devo usar curingas, como *, para obter todas as linhas dos meus conjuntos de dados?

+++Resposta Não é possível usar curingas para obter todos os dados de suas linhas, pois o Serviço de consulta deve ser tratado como um **columnar-store** em vez de um sistema de armazenamento tradicional baseado em linhas.
+++

### Devo usar `NOT IN` em minha consulta SQL?

+++Responder A `NOT IN` O operador geralmente é usado para recuperar linhas que não são encontradas em outra tabela ou instrução SQL. Esse operador pode retardar o desempenho e retornar resultados inesperados se as colunas que estão sendo comparadas aceitarem `NOT NULL`ou você tem muitos registros.

Em vez de usar `NOT IN`, você pode usar `NOT EXISTS` ou `LEFT OUTER JOIN`.

Por exemplo, se você tiver as seguintes tabelas criadas:

```sql
CREATE TABLE T1 (ID INT)
CREATE TABLE T2 (ID INT)
INSERT INTO T1 VALUES (1)
INSERT INTO T1 VALUES (2)
INSERT INTO T1 VALUES (3)
INSERT INTO T2 VALUES (1)
INSERT INTO T2 VALUES (2)
```

Se você estiver usando o `NOT EXISTS` operador, é possível replicar usando o `NOT IN` operador usando a seguinte query:

```sql
SELECT ID FROM T1
WHERE NOT EXISTS
(SELECT ID FROM T2 WHERE T1.ID = T2.ID)
```

Como alternativa, se você estiver usando o `LEFT OUTER JOIN` operador, é possível replicar usando o `NOT IN` operador usando a seguinte query:

```sql
SELECT T1.ID FROM T1
LEFT OUTER JOIN T2 ON T1.ID = T2.ID
WHERE T2.ID IS NULL
```

+++

### Posso criar um conjunto de dados usando uma consulta CTAS com um nome de sublinhado duplo como aqueles exibidos na interface? Por exemplo: `test_table_001`.

+++Resposta Não, essa é uma limitação intencional no Experience Platform que se aplica a todos os serviços da Adobe, incluindo o Serviço de consulta. Um nome com dois sublinhados é aceitável como um esquema e nome de conjunto de dados, mas o nome da tabela do conjunto de dados só pode conter um único sublinhado.
+++

### Quantas consultas simultâneas você pode executar de cada vez?

+++Resposta Não há limite de simultaneidade de consulta, pois as consultas em lote são executadas como trabalhos de back-end. No entanto, há um tempo limite de consulta definido como 24 horas.
+++

### Existe um painel de atividades onde você pode ver as atividades de consulta e o status?

+++Resposta Há recursos de monitoramento e alerta para verificar as atividades e os status de consultas. Consulte a [Integração do log de auditoria do Serviço de consulta](./data-governance/audit-log-guide.md) e a variável [logs de consulta](./ui/overview.md#log) documentos para obter mais informações.
+++

### Há alguma maneira de reverter as atualizações? Por exemplo, se houver um erro ou alguns cálculos precisarem ser reconfigurados ao gravar dados na Platform, como esse cenário deve ser tratado?

+++Responder No momento, não oferecemos suporte a reversões ou atualizações dessa maneira.
+++

### Como você pode otimizar consultas no Adobe Experience Platform?

+++Resposta O sistema não tem índices, pois não é um banco de dados, mas tem outras otimizações em vigor vinculadas ao armazenamento de dados. As seguintes opções estão disponíveis para ajustar as consultas:

- Um filtro com base no tempo em dados de série temporal.
- Forçamento otimizado para o tipo de dados struct.
- Custo otimizado e redução de memória para arrays e tipos de dados de mapa.
- Processamento incremental usando instantâneos.
- Um formato de dados persistente.
+++

### Os logons podem ser restritos a certos aspectos do Serviço de consulta ou é uma solução &quot;tudo ou nada&quot;?

+++O Serviço de consulta de resposta é uma solução &quot;tudo ou nada&quot;. O acesso parcial não pode ser fornecido.
+++

### Posso restringir quais dados o Serviço de consulta pode usar ou ele simplesmente acessa todo o data lake da Adobe Experience Platform?

+++Resposta Sim, você pode restringir a consulta a conjuntos de dados com acesso somente leitura.
+++

### Quais outras opções existem para restringir os dados que o Serviço de consulta pode acessar?

+++Resposta Há três abordagens para restringir o acesso. Elas são as seguintes:

- Use instruções somente SELECT e conceda acesso somente leitura aos conjuntos de dados. Além disso, atribua a permissão gerenciar consulta.
- Use as instruções SELECT/INSERT/CREATE e conceda acesso de gravação aos conjuntos de dados. Além disso, atribua a permissão de gerenciamento de consulta.
- Use uma conta de integração com as sugestões anteriores acima e atribua a permissão de integração de consulta.

+++

### Depois que os dados forem retornados pelo Serviço de consulta, há verificações que podem ser executadas pela Plataforma para garantir que ela não tenha retornado dados protegidos?

- O Serviço de consulta oferece suporte ao controle de acesso baseado em atributos. Você pode restringir o acesso aos dados no nível da coluna/folha e/ou no nível da estrutura. Consulte a documentação para saber mais sobre o controle de acesso baseado em atributos.

### Posso especificar um modo SSL para a conexão com um cliente de terceiros? Por exemplo, posso usar &quot;verify-full&quot; com o Power BI?

+++Responda Sim, os modos SSL são compatíveis. Consulte a [Documentação de modos SSL](./clients/ssl-modes.md) para obter uma discriminação dos diferentes modos SSL disponíveis e o nível de proteção que eles fornecem.
+++

### Usamos o TLS 1.2 para todas as conexões de clientes Power BI com o serviço de consulta?

+++Responda Sim. Os dados em trânsito são sempre compatíveis com HTTPS. A versão atualmente compatível é TLS1.2.
+++

### Uma conexão feita na porta 80 ainda usa https?

+++Responda Sim, uma conexão feita na porta 80 ainda usa SSL. Você também pode usar a porta 5432.
+++

### Posso controlar o acesso a conjuntos de dados e colunas específicos para uma conexão específica? Como isso é configurado?

+++Responda Sim, o controle de acesso baseado em atributo é aplicado se configurado. Consulte a [visão geral do controle de acesso baseado em atributos](../access-control/abac/overview.md) para obter mais informações.
+++

### O Serviço de consulta suporta o comando &quot;INSERT OVERWRITE INTO&quot;?

+++Resposta Não, o Serviço de Consulta não oferece suporte ao comando &quot;INSERT OVERWRITE INTO&quot;.
+++

## Exportar dados {#exporting-data}

Esta seção fornece informações sobre exportação de dados e limites.

### Existe uma maneira de extrair dados do Serviço de consulta após o processamento da consulta e salvar os resultados em um arquivo CSV? {#export-csv}

+++Responda Sim. Os dados podem ser extraídos do Serviço de consulta, e também há a opção de armazenar os resultados no formato CSV por meio de um comando SQL.

Há duas maneiras de salvar os resultados de uma consulta ao usar um cliente PSQL. Você pode usar o `COPY TO` ou crie uma instrução usando o seguinte formato:

```sql
SELECT column1, column2 
FROM <table_name>  
\g <table_name>.out
```

[Orientações sobre a utilização do `COPY TO` comando](./sql/syntax.md#copy) podem ser encontradas na documentação de referência da sintaxe SQL.
+++

### Posso extrair o conteúdo do conjunto de dados final que foi assimilado por meio de queries CTAS (supondo que sejam quantidades maiores de dados, como Terabytes)?

+++Número de resposta No momento, não há nenhum recurso disponível para a extração de dados assimilados.
+++

### Por que o conector de dados do Analytics não retorna dados?

+++Resposta Uma causa comum desse problema é a consulta de dados de série temporal sem um filtro de tempo. Por exemplo:

```sql
SELECT * FROM prod_table LIMIT 1;
```

Deve ser escrito como:

```sql
SELECT * FROM prod_table
WHERE
timestamp >= to_timestamp('2022-07-22')
and timestamp < to_timestamp('2022-07-23');
```

+++

## Ferramentas de terceiros {#third-party-tools}

Esta seção inclui informações sobre o uso de ferramentas de terceiros, como PSQL e Power BI.

### Posso conectar o Serviço de consulta a uma ferramenta de terceiros?

+++Resposta Sim, você pode conectar vários clientes de desktop de terceiros ao Serviço de consulta. Consulte a documentação para [detalhes completos sobre os clientes disponíveis e como conectá-los ao Serviço de consulta](./clients/overview.md).
+++

### Há uma maneira de conectar o Serviço de consulta uma vez para uso contínuo com uma ferramenta de terceiros?

+++Resposta Sim, os clientes de desktop de terceiros podem ser conectados ao Serviço de consulta por meio de uma configuração única de credenciais sem expiração. Credenciais que não expiram podem ser geradas por um usuário autorizado e recebidas em um arquivo JSON baixado automaticamente para a máquina local. Completo [orientação sobre como criar e baixar credenciais sem expiração](./ui/credentials.md#non-expiring-credentials) podem ser encontradas na documentação.
+++

### Por que minhas credenciais sem expiração não estão funcionando?

+++Resposta O valor para credenciais sem expiração são os argumentos concatenados do `technicalAccountID` e a variável `credential` retirada do arquivo JSON de configuração. O valor da senha tem o formato: `{{technicalAccountId}:{credential}}`.
Consulte a documentação para obter mais informações sobre como [conectar-se a clientes externos com credenciais](./ui/credentials.md#using-credentials-to-connect-to-external-clients).
+++

### Que tipo de editores SQL de terceiros posso conectar ao Editor de serviço de consulta?

+++Responder Qualquer editor SQL de terceiros que seja PSQL ou [!DNL Postgres] compatível com o cliente pode ser conectado ao Editor de Serviço de Consulta. Consulte a documentação para [conectar clientes ao Serviço de consulta](./clients/overview.md) para obter uma lista de instruções disponíveis.
+++

### Posso conectar a ferramenta Power BI ao Serviço de consulta?

+++Resposta Sim, você pode conectar o Power BI ao Serviço de consulta. Consulte a documentação para [instruções sobre como conectar o aplicativo de desktop do Power BI ao Serviço de consulta](./clients/power-bi.md).
+++

### Por que os painéis demoram muito para carregar quando conectados ao Serviço de consulta?

+++Resposta Quando o sistema está conectado ao Serviço de consulta, ele é conectado a um mecanismo de processamento interativo ou em lote. Isso pode resultar em tempos de carregamento mais longos para refletir os dados processados.

Se quiser melhorar os tempos de resposta dos painéis, implemente um servidor de Business Intelligence (BI) como uma camada de cache entre o Serviço de consulta e as ferramentas de BI. Geralmente, a maioria das ferramentas de BI tem uma oferta adicional para um servidor.

A finalidade de adicionar a camada do servidor de cache é armazenar os dados em cache do Serviço de consulta e utilizar os mesmos para que os painéis acelerem a resposta. Isso é possível, pois os resultados das consultas executadas seriam armazenados em cache no servidor de BI todos os dias. O servidor de cache fornece esses resultados para qualquer usuário com a mesma consulta para diminuir a latência. Consulte a documentação do utilitário ou ferramenta de terceiros que você está usando para obter esclarecimentos sobre esta configuração.
+++

### É possível acessar o Serviço de consulta usando a ferramenta de conexão pgAdmin?

+++Resposta Não, a conectividade com o pgAdmin não é compatível. A [lista de clientes de terceiros disponíveis e instruções sobre como conectá-los ao Serviço de consulta](./clients/overview.md) podem ser encontradas na documentação.
+++

## Erros de API PostgreSQL {#postgresql-api-errors}

A tabela a seguir fornece códigos de erro PSQL e suas possíveis causas.

| Código de erro | Estado da conexão | Descrição | Causa possível |
|------------|---------------------------|-------------|----------------|
| **08P01** | N/D | Tipo de mensagem incompatível | Tipo de mensagem incompatível |
| **28P01** | Inicialização - autenticação | Senha inválida | Token de autenticação inválido |
| **28000** | Inicialização - autenticação | Tipo de autorização inválido | Tipo de autorização inválido. Deve ser `AuthenticationCleartextPassword`. |
| **42P12** | Inicialização - autenticação | Nenhuma tabela encontrada | Nenhuma tabela encontrada para uso |
| **42601** | Consulta | Erro de sintaxe | Erro de sintaxe ou comando inválido |
| **42P01** | Consulta | Tabela não encontrada | A tabela especificada na consulta não foi encontrada |
| **42P07** | Consulta | A tabela existe | Já existe uma tabela com o mesmo nome (CREATE TABLE) |
| **53400** | Consulta | O LIMITE excede o valor máximo | O usuário especificou uma cláusula LIMIT maior que 100.000 |
| **53400** | Consulta | Tempo limite da instrução | O demonstrativo ao vivo enviado levou mais do que o máximo de 10 minutos |
| **58000** | Consulta | Erro do sistema | Falha interna do sistema |
| **0A000** | Consulta/Comando | Não suportado | O recurso/funcionalidade na consulta/comando não é compatível |
| **42501** | DROP TABLE Query | Tabela de remoção não criada pelo Serviço de consulta | A tabela que está sendo removida não foi criada pelo Serviço de Consulta usando o `CREATE TABLE` instrução |
| **42501** | DROP TABLE Query | Tabela não criada pelo usuário autenticado | A tabela que está sendo removida não foi criada pelo usuário conectado no momento |
| **42P01** | DROP TABLE Query | Tabela não encontrada | A tabela especificada na consulta não foi encontrada |
| **42P12** | DROP TABLE Query | Nenhuma tabela encontrada para `dbName`: verifique a `dbName` | Nenhuma tabela foi encontrada no banco de dados atual |

### Por que recebi um código de erro 58000 ao usar o método history_meta() na tabela?

+++Responder A `history_meta()` é usado para acessar um instantâneo de um conjunto de dados. Anteriormente, se você executasse uma consulta em um conjunto de dados vazio no Azure Data Lake Storage (ADLS), receberia um código de erro 58000 informando que o conjunto de dados não existe. Um exemplo do erro de sistema antigo é exibido abaixo.

```shell
ErrorCode: 58000 Internal System Error [Invalid table your_table_name. historyMeta can be used on datalake tables only.]
```

Este erro ocorreu porque não havia valor de retorno para a consulta. Esse comportamento foi corrigido para retornar a seguinte mensagem:

```text
Query complete in {timeframe}. 0 rows returned. 
```

+++

## Erros de REST API {#rest-api-errors}

A tabela a seguir fornece códigos de erro HTTP e suas possíveis causas.

| Código de status HTTP | Descrição | Possíveis causas |
|------------------|-----------------------|----------------------------|
| 400 | Solicitação inválida | Consulta malformada ou ilegal |
| 401 | Falha na autenticação | Token de autenticação inválido |
| 500 | Erro interno do servidor | Falha interna do sistema |
