---
title: Modelos
description: Gerenciamento do ciclo de vida do modelo com a extensão SQL do Data Distiller. Saiba como criar, treinar e gerenciar modelos estatísticos avançados usando o SQL, incluindo processos importantes, como controle de versão, avaliação e previsão de modelos, para obter insights acionáveis de seus dados.
role: Developer
exl-id: c609a55a-dbfd-4632-8405-55e99d1e0bd8
source-git-commit: 6a61900b19543f110c47e30f4d321d0016b65262
workflow-type: tm+mt
source-wordcount: '1229'
ht-degree: 1%

---

# Modelos

>[!AVAILABILITY]
>
>Essa funcionalidade está disponível para clientes que compraram o complemento Data Distiller. Para obter mais informações, entre em contato com o(a) representante da Adobe.

O Serviço de consulta agora oferece suporte aos processos principais de criação e implantação de um modelo. Você pode usar o SQL para treinar o modelo usando seus dados, avaliar sua precisão e aplicar o modelo de treinamento para fazer previsões sobre novos dados. Você pode usar o modelo para generalizar seus dados anteriores e tomar decisões informadas sobre cenários do mundo real.

As três etapas do ciclo de vida do modelo para gerar insights acionáveis são:

1. **Treinamento**: o modelo aprende padrões com o conjunto de dados fornecido. (criar ou substituir modelo)
2. **Teste/Avaliação**: o desempenho do modelo é avaliado usando um conjunto de dados separado. (`model_evaluate`)
3. **Previsão**: o modelo treinado é usado para fazer previsões sobre dados novos e inéditos.

Use a extensão SQL do modelo, adicionada à gramática SQL existente, para gerenciar o ciclo de vida do modelo de acordo com suas necessidades comerciais. Este documento aborda o SQL necessário para criar ou substituir um modelo, treinar, avaliar, treinar novamente quando necessário e prever insights.

## Criação de modelos e treinamento {#create-and-train}

Saiba como definir, configurar e treinar um modelo de aprendizado de máquina usando comandos SQL. O SQL abaixo demonstra como criar um modelo, aplicar transformações de engenharia de recursos e iniciar o processo de treinamento para garantir que o modelo seja configurado corretamente para uso futuro. Os seguintes comandos SQL detalham diferentes opções para a criação e o gerenciamento do modelo:

- **CREATE MODEL**: cria e treina um novo modelo em um conjunto de dados especificado. Se um modelo com o mesmo nome já existir, esse comando retornará um erro.
- **CRIAR MODELO SE NÃO EXISTIR**: cria e treina um novo modelo apenas se um modelo com o mesmo nome ainda não existir no conjunto de dados especificado.
- **CRIAR OU SUBSTITUIR MODELO**: cria e treina um modelo, substituindo a versão mais recente de um modelo existente pelo mesmo nome no conjunto de dados especificado.

```sql
CREATE MODEL | CREATE MODEL IF NOT EXISTS | CREATE OR REPLACE MODEL}
model_alias
[TRANSFORM (select_list)]
[OPTIONS(model_option_list)]
[AS {select_query}]
 
model_option_list:
    MODEL_TYPE = { 'LINEAR_REG' |
                   'LOGISTIC_REG' |
                   'KMEANS' }
  [, MAX_ITER = int64_value ]
 [, LABEL = string_array ]
[, REG_PARAM = float64_value ]
```

**Exemplo**

```sql
CREATE MODEL churn_model
TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features) 
OPTIONS(MODEL_TYPE='linear_reg', LABEL='churn_rate') 
AS
SELECT *
FROM churn_with_rate
ORDER BY period;
```

Para ajudá-lo a entender os principais componentes e configurações no processo de criação e treinamento do modelo, as notas a seguir explicam a finalidade e a função de cada elemento no exemplo SQL acima.

- `<model_alias>`: o alias do modelo é um nome reutilizável atribuído ao modelo, que pode ser referenciado posteriormente. É necessário dar um nome ao seu modelo.
- `transform`: a cláusula de transformação é usada para aplicar transformações de engenharia de recursos (por exemplo, codificação one-hot e indexação de cadeia de caracteres) ao conjunto de dados antes de treinar o modelo. A última cláusula da instrução `TRANSFORM` deve ser uma `vector_assembler` com uma lista de colunas que comporiam os recursos para treinamento de modelo, ou um tipo derivado de `vector_assembler` (como `max_abs_scaler(feature)`, `standard_scaler(feature)` e assim por diante). Somente as colunas mencionadas na última cláusula serão usadas para treinamento; todas as outras colunas, mesmo se incluídas na consulta `SELECT`, serão excluídas.
- `label = <label-COLUMN>`: a coluna de rótulo no conjunto de dados de treinamento que especifica o destino ou resultado que o modelo pretende prever.
- `training-dataset`: essa sintaxe seleciona os dados usados para treinar o modelo.
- `type = 'LogisticRegression'`: esta sintaxe especifica o tipo de algoritmo de aprendizado de máquina a ser usado. As opções incluem `LinearRegression`, `LogisticRegression` e `KMeans`.
- `options`: esta palavra-chave fornece um conjunto flexível de pares de valor-chave para configurar o modelo.
   - `Key model_type`: `model_type = '<supported algorithm>'`: especifica o tipo de algoritmo de aprendizado de máquina a ser usado. As opções suportadas incluem `LinearRegression`, `LogisticRegression` e `KMeans`.
   - `Key label`: `label = <label_COLUMN>`: Define a coluna de rótulo no conjunto de dados de treinamento, que indica o destino ou resultado que o modelo pretende prever.

Use o SQL para referenciar o conjunto de dados usado para treinamento.

## Atualizar um modelo {#update}

Saiba como atualizar um modelo existente de aprendizado de máquina aplicando novas transformações de engenharia de recursos e configurando opções como o tipo de algoritmo e a coluna de rótulo. Cada atualização cria uma nova versão do modelo, incrementada a partir da última versão. Isso garante que as alterações sejam rastreadas e que o modelo possa ser reutilizado em etapas futuras de avaliação ou previsão.

O exemplo a seguir demonstra a atualização de um modelo com novas transformações e opções:

```sql
UPDATE MODEL <model_alias> TRANSFORM (vector_assembler(array(current_customers, previous_customers)) features)  OPTIONS(MODEL_TYPE='logistic_reg', LABEL='churn_rate')  AS SELECT * FROM churn_with_rate ORDER BY period;
```

**Exemplo**

Para entender o processo de controle de versão, considere o seguinte comando:

```sql
UPDATE MODEL model_vdqbrja OPTIONS(MODEL_TYPE='logistic_reg', LABEL='Survived') AS SELECT * FROM titanic_e2e_dnd;
```

Depois que esse comando é executado, o modelo tem uma nova versão, conforme mostrado na tabela abaixo:

| ID de modelo atualizada | Modelo atualizado | Nova versão |
|--------------------------------------------|---------------|-------------|
| a8f6a254-8f28-42ec-8b26-94edeb4698e8 | model_vdqbrja | 2 |

As notas a seguir explicam os principais componentes e opções no fluxo de trabalho de atualização de modelo.

- `UPDATE model <model_alias>`: o comando de atualização manipula o controle de versão e cria uma nova versão de modelo incrementada a partir da última versão.
- `version`: Uma palavra-chave opcional usada apenas durante atualizações para especificar explicitamente que uma nova versão deve ser criada. Se omitida, o sistema incrementa automaticamente a versão.


## Avaliar modelos {#evaluate-model}

Para garantir resultados confiáveis, avalie a precisão e a eficácia do modelo antes de implantá-lo para previsões com a palavra-chave `model_evaluate`. A instrução SQL abaixo especifica um conjunto de dados de teste, colunas específicas e a versão do modelo para testar o modelo avaliando seu desempenho.

```sql
SELECT *
FROM   model_evaluate(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   test -dataset)
```

A função `model_evaluate` usa `model-alias` como seu primeiro argumento e uma instrução `SELECT` flexível como seu segundo argumento. Primeiro, o Serviço de Consulta executa a instrução `SELECT` e mapeia os resultados para a ADF (Função Definida por Adobe) `model_evaluate`. O sistema espera que os nomes das colunas e os tipos de dados no resultado da instrução `SELECT` correspondam aos usados na etapa de treinamento. Esses nomes de colunas e tipos de dados são tratados como dados de teste e dados de rótulo para avaliação.

>[!IMPORTANT]
>
>Ao avaliar (`model_evaluate`) e prever (`model_predict`), as transformações realizadas no momento do treinamento são usadas.

## Predicar {#predict}

Em seguida, use a palavra-chave `model_predict` para aplicar o modelo e a versão especificados a um conjunto de dados e gerar previsões para as colunas selecionadas. O SQL abaixo demonstra esse processo, mostrando como prever resultados usando o alias e a versão do modelo.

```sql
SELECT *
FROM   model_predict(model-alias, version-number,SELECT col1,
       col2,
       label-COLUMN
FROM   dataset)
```

`model_predict` aceita o alias do modelo como o primeiro argumento e uma instrução `SELECT` flexível como o segundo argumento. Primeiro, o Serviço de Consulta executa a instrução `SELECT` e mapeia os resultados para o ADF `model_predict`. O sistema espera que os nomes das colunas e os tipos de dados no resultado da instrução `SELECT` correspondam aos da etapa de treinamento. Esses dados são usados para pontuação e geração de previsões.

>[!IMPORTANT]
>
>Ao avaliar (`model_evaluate`) e prever (`model_predict`), as transformações realizadas no momento do treinamento são usadas.

## Avalie e gerencie seus modelos

Use o comando `SHOW MODELS` para listar todos os modelos disponíveis que você criou. Use-o para exibir os modelos que foram treinados e estão disponíveis para avaliação ou previsão. Quando consultadas, as informações são buscadas no repositório do modelo, que é atualizado durante a criação do modelo. Os detalhes retornados são: ID do modelo, nome do modelo, versão, conjunto de dados de origem, detalhes do algoritmo, opções/parâmetros, hora de criação/atualização e o usuário que criou o modelo.

```sql
SHOW MODELS;
```

Os resultados aparecem em uma tabela semelhante à mostrada abaixo:

| model-id | model-name | version | source-dataset | tipo | opções | transformar | campos | criado | atualizado | criado POR |
|--------------------|---------------|---------|------------------|-----------------------|------------------------------|---------------------------------------------------------------------------|----------------------|---------------------|---------------------|------------|
| `model-84362-mdunj` | `SalesModel` | 1,0 | `sales_data_2023` | `LogisticRegression` | `{"label": "label-field"}` | `one_hot_encoder(name)`, `ohe_name`, `string_indexer(gender)`, `genderSI` | \[&quot;name&quot;, &quot;gender&quot;\] | 2024-08-14 10:30 AM | 2024-08-14 11:00 AM | `JohnSnow@adobe.com` |

## Limpar e manter seus modelos

Use o comando `DROP MODELS` para excluir os modelos criados do registro de modelos. Você pode usá-lo para remover modelos desatualizados, não utilizados ou indesejados. Isso libera recursos e garante que somente os modelos relevantes sejam mantidos. Você também pode incluir um nome de modelo opcional para melhorar a especificidade. Isso somente descarta o modelo com a versão de modelo fornecida.

```sql
DROP MODEL IF EXISTS modelName
DROP MODEL IF EXISTS modelName modelVersion ;
```

## Próximas etapas

Depois de ler este documento, agora você entende a sintaxe básica do SQL necessária para criar, treinar e gerenciar modelos confiáveis usando o Data Distiller. Em seguida, explore o [documento Implementar modelos estatísticos avançados](./implement-models/implement-models.md) para saber mais sobre os vários modelos confiáveis disponíveis e como implementá-los efetivamente em seus fluxos de trabalho SQL. Caso ainda não o tenha feito, revise o documento [Engenharia de Recursos](./feature-engineering.md) para garantir que seus dados estejam preparados de forma ideal para o treinamento de modelos.
