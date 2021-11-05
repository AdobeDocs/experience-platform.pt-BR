---
title: Exemplos de consultas de carga incremental
description: O recurso de carregamento incremental usa recursos anônimos de bloco e instantâneo para fornecer uma solução quase em tempo real para mover dados do lago de dados para o data warehouse, ignorando os dados correspondentes.
source-git-commit: fb464c6e6b1972f5a2653872385517749936691a
workflow-type: tm+mt
source-wordcount: '685'
ht-degree: 0%

---

# Exemplos de consultas incrementais de carregamento de dados

O padrão de design de carga incremental é uma solução para gerenciar dados. O padrão processa apenas as informações no conjunto de dados que foram criadas ou modificadas desde a última execução do carregamento.

A carga incremental usa vários recursos fornecidos pelo Serviço de query da Adobe Experience Platform, como blocos anônimos e instantâneos. Esse padrão de design aumenta a eficiência do processamento, pois todos os dados já processados da fonte são ignorados. Ele pode ser usado com processamento de dados em lote e streaming.

Este documento fornece uma série de instruções para criar um padrão de design para processamento incremental. Essas etapas podem ser usadas como um template para criar seus próprios queries de carregamento de dados incrementais.

## Introdução

Os exemplos de SQL neste documento exigem uma compreensão dos recursos anônimos de bloco e snapshot. Recomenda-se que leia a [exemplo de consultas de bloco anônimas](./anonymous-block.md) e também a [cláusula de instantâneo](../sql/syntax.md#snapshot-clause) documentação.

Para obter orientação sobre qualquer terminologia usada neste guia, consulte [Guia de sintaxe SQL](../sql/syntax.md).

## Etapas

As etapas abaixo demonstram como criar e carregar dados incrementalmente usando instantâneos e o recurso de bloco anônimo. O padrão de design pode ser usado como um modelo para sua própria sequência de consultas.

1. Crie um `checkpoint_log` tabela para rastrear o instantâneo mais recente usado para processar dados com êxito. A tabela de rastreamento (`checkpoint_log` neste exemplo) deve primeiro ser inicializado para `null` para processar um conjunto de dados de forma incremental.

```SQL
DROP TABLE IF EXISTS checkpoint_log;
CREATE TABLE  checkpoint_log AS
SELECT
   cast(NULL AS string) process_name,
   cast(NULL AS string) process_status,
   cast(NULL AS string) last_snapshot_id,
   cast(NULL AS TIMESTAMP) process_timestamp
   WHERE false;
```

1. Preencha o `checkpoint_log` tabela com um registro vazio para o conjunto de dados que precisa de processamento incremental. `DIM_TABLE_ABC` é o conjunto de dados a ser processado no exemplo abaixo. Na primeira transformação `DIM_TABLE_ABC`, o `last_snapshot_id` é inicializado como `null`. Isso permite processar todo o conjunto de dados na primeira vez e de forma incremental a partir de então.

```SQL
INSERT INTO
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
       cast(NULL AS string) last_snapshot_id,
       CURRENT_TIMESTAMP process_timestamp;
```

1. Em seguida, inicializar `DIM_TABLE_ABC_Incremental` para conter a saída processada de `DIM_TABLE_ABC`. O bloco anônimo no **obrigatório** a seção de execução do exemplo SQL abaixo, conforme descrito nas etapas um a quatro, é executada sequencialmente para processar dados de forma incremental.

   1. Defina as `from_snapshot_id` que indica de onde o processamento começa. O `from_snapshot_id` no exemplo é consultado a partir do `checkpoint_log` tabela para uso com `DIM_TABLE_ABC`. Na execução inicial, a ID do instantâneo será `null` o que significa que todo o conjunto de dados será processado.
   2. Defina as `to_snapshot_id` como a ID de instantâneo atual da tabela de origem (`DIM_TABLE_ABC`). No exemplo, isso é consultado na tabela de metadados da tabela de origem.
   3. Use o `CREATE` palavra-chave para criar `DIM_TABLE_ABC_Incremenal` como a tabela de destino. A tabela de destino mantém os dados processados do conjunto de dados de origem (`DIM_TABLE_ABC`). Isso permite que os dados processados da tabela de origem entre `from_snapshot_id` e `to_snapshot_id`, para ser anexado de forma incremental à tabela de destino.
   4. Atualize o `checkpoint_log` com a `to_snapshot_id` para os dados de origem que `DIM_TABLE_ABC` processado com êxito.
   5. Se qualquer uma das consultas executadas sequencialmente do bloco anônimo falhar, a variável **opcional** a seção de exceção é executada. Isso retorna um erro e encerra o processo.

>[!NOTE]
>
>O `history_meta('source table name')` é um método conveniente usado para obter acesso ao instantâneo disponível em um conjunto de dados.

```SQL
$$
BEGIN
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                ON a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    CREATE TABLE DIM_TABLE_ABC_Incremental AS
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id ;
 
INSERT INTO
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
 
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
 END$$;
```

1. Use a lógica de carregamento de dados incremental no exemplo de bloco anônimo abaixo para permitir que quaisquer novos dados do conjunto de dados de origem (desde o carimbo de data e hora mais recente) sejam processados e anexados à tabela de destino em uma cadência regular. No exemplo, os dados são alterados para `DIM_TABLE_ABC` será processada e anexada a `DIM_TABLE_ABC_incremental`.

>[!NOTE]
>
> `_ID` é a chave primária em ambos `DIM_TABLE_ABC_Incremental` e `SELECT history_meta('DIM_TABLE_ABC')`.

```SQL
$$
BEGIN
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a join
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                ON a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
 
INSERT INTO
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
 
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
 END$$;
```

Essa lógica pode ser aplicada a qualquer tabela para executar cargas incrementais.

## Instantâneos expirados

>[!IMPORTANT]
>
>Metadados de instantâneo expiram após **two** dias. Um instantâneo expirado invalida a lógica do script fornecido acima.

Para resolver o problema de uma ID de instantâneo expirada, insira o seguinte comando no início do bloco anônimo. A linha de código a seguir substitui a variável `@from_snapshot_id` com o mais antigo disponível `snapshot_id` de metadados.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

O bloco de código inteiro tem a seguinte aparência:

```SQL
$$
BEGIN
    SET resolve_fallback_snapshot_on_failure=true;
    SET @from_snapshot_id = SELECT coalesce(last_snapshot_id, 'HEAD') FROM checkpoint_log a JOIN
                            (SELECT MAX(process_timestamp)process_timestamp FROM checkpoint_log
                                WHERE process_name = 'DIM_TABLE_ABC' AND process_status = 'SUCCESSFUL' )b
                                on a.process_timestamp=b.process_timestamp;
    SET @to_snapshot_id = SELECT snapshot_id FROM (SELECT history_meta('DIM_TABLE_ABC')) WHERE  is_current = true;
    SET @last_updated_timestamp= SELECT CURRENT_TIMESTAMP;
    INSERT INTO DIM_TABLE_ABC_Incremental
     SELECT  *  FROM DIM_TABLE_ABC SNAPSHOT BETWEEN @from_snapshot_id AND @to_snapshot_id WHERE NOT EXISTS (SELECT _id FROM DIM_TABLE_ABC_Incremental a WHERE _id=a._id);
 
Insert Into
   checkpoint_log
   SELECT
       'DIM_TABLE_ABC' process_name,
       'SUCCESSFUL' process_status,
      cast( @to_snapshot_id AS string) last_snapshot_id,
      cast( @last_updated_timestamp AS TIMESTAMP) process_timestamp;
EXCEPTION
  WHEN OTHER THEN
    SELECT 'ERROR';
 END$$;
```

## Próximas etapas

Ao ler este documento, você deve ter uma melhor compreensão de como usar os recursos de bloco e instantâneo anônimos para executar cargas incrementais e pode aplicar essa lógica a seus próprios queries específicos. Para obter orientações gerais sobre a execução da consulta, leia a [guia sobre a execução de query no Serviço de query](./writing-queries.md).
