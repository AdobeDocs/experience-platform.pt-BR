---
title: Carga incremental no serviço de consulta
description: O recurso de carga incremental usa recursos de instantâneos e blocos anônimos para fornecer uma solução quase em tempo real para mover dados do data lake para o data warehouse, ignorando, ao mesmo tempo, dados correspondentes.
exl-id: 1418d041-29ce-4153-90bf-06bd8da8fb78
source-git-commit: 99cd69234006e6424be604556829b77236e92ad7
workflow-type: tm+mt
source-wordcount: '688'
ht-degree: 0%

---

# Carga incremental no Serviço de consulta

O padrão de design de carga incremental é uma solução para gerenciamento de dados. O padrão processa apenas as informações no conjunto de dados que foi criado ou modificado desde a última execução de carregamento.

A carga incremental usa vários recursos fornecidos pelo Serviço de consulta da Adobe Experience Platform, como blocos anônimos e instantâneos. Esse padrão de design aumenta a eficiência do processamento, pois quaisquer dados já processados da origem são ignorados. Ele pode ser usado com processamento de dados em lote e de transmissão.

Este documento fornece uma série de instruções para criar um padrão de design para processamento incremental. Essas etapas podem ser usadas como um modelo para criar suas próprias consultas de carregamento de dados incrementais.

## Introdução

Os exemplos de SQL neste documento exigem que você tenha uma compreensão dos recursos de bloco e instantâneo anônimos. É recomendável que você leia a documentação das [consultas de exemplo de bloco anônimo](./anonymous-block.md) e também a documentação da [cláusula de instantâneo](../sql/syntax.md#snapshot-clause).

Para orientação sobre qualquer terminologia usada neste guia, consulte o [guia de sintaxe SQL](../sql/syntax.md).

## Carregar dados incrementalmente

As etapas abaixo demonstram como criar e carregar dados de forma incremental usando instantâneos e o recurso de bloqueio anônimo. O padrão de design pode ser usado como um modelo para sua própria sequência de consultas.

1. Crie uma tabela `checkpoint_log` para rastrear o instantâneo mais recente usado para processar dados com êxito. A tabela de rastreamento (`checkpoint_log` neste exemplo) deve primeiro ser inicializada em `null` para processar de forma incremental um conjunto de dados.

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

1. Preencha a tabela `checkpoint_log` com um registro vazio para o conjunto de dados que precisa de processamento incremental. `DIM_TABLE_ABC` é o conjunto de dados a ser processado no exemplo abaixo. Na primeira ocasião do processamento de `DIM_TABLE_ABC`, `last_snapshot_id` é inicializado como `null`. Isso permite processar todo o conjunto de dados na primeira vez e de forma incremental posteriormente.

   ```SQL
   INSERT INTO
      checkpoint_log
      SELECT
         'DIM_TABLE_ABC' process_name,
         'SUCCESSFUL' process_status,
         cast(NULL AS string) last_snapshot_id,
         CURRENT_TIMESTAMP process_timestamp;
   ```

1. Em seguida, inicialize `DIM_TABLE_ABC_Incremental` para conter saída processada de `DIM_TABLE_ABC`. O bloco anônimo na seção de execução **required** do exemplo SQL abaixo, conforme descrito nas etapas de um a quatro, é executado sequencialmente para processar dados de forma incremental.

   1. Defina o `from_snapshot_id` que indica de onde o processamento começa. O `from_snapshot_id` no exemplo é consultado a partir da tabela `checkpoint_log` para uso com `DIM_TABLE_ABC`. Na execução inicial, a ID do instantâneo será `null`, o que significa que todo o conjunto de dados será processado.
   1. Defina `to_snapshot_id` como a ID de instantâneo atual da tabela de origem (`DIM_TABLE_ABC`). No exemplo, isso é consultado a partir da tabela de metadados da tabela de origem.
   1. Use a palavra-chave `CREATE` para criar `DIM_TABLE_ABC_Incremenal` como a tabela de destino. A tabela de destino mantém os dados processados do conjunto de dados de origem (`DIM_TABLE_ABC`). Isso permite que os dados processados da tabela de origem entre `from_snapshot_id` e `to_snapshot_id` sejam acrescentados de forma incremental à tabela de destino.
   1. Atualize a tabela `checkpoint_log` com `to_snapshot_id` para os dados de origem que `DIM_TABLE_ABC` processou com êxito.
   1. Se qualquer uma das consultas executadas sequencialmente do bloco anônimo falhar, a seção de exceção **opcional** será executada. Isso retorna um erro e encerra o processo.

   >[!NOTE]
   >
   >O `history_meta('source table name')` é um método conveniente usado para obter acesso ao instantâneo disponível em um conjunto de dados.

   ```SQL
   $$ BEGIN
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
   END 
   $$;
   ```

1. Use a lógica de carregamento de dados incrementais no exemplo de bloco anônimo abaixo para permitir que quaisquer novos dados do conjunto de dados de origem (desde o carimbo de data e hora mais recente) sejam processados e anexados à tabela de destino em uma cadência regular. No exemplo, as alterações de dados em `DIM_TABLE_ABC` serão processadas e anexadas a `DIM_TABLE_ABC_incremental`.

   >[!NOTE]
   >
   > `_ID` é a Chave Primária em `DIM_TABLE_ABC_Incremental` e `SELECT history_meta('DIM_TABLE_ABC')`.

   ```SQL
   $$ BEGIN
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
   END
   $$;
   ```

Essa lógica pode ser aplicada a qualquer tabela para executar cargas incrementais.

## Instantâneos expirados

>[!IMPORTANT]
>
>Os metadados de instantâneo expiram após **dois** dias. Um instantâneo expirado invalida a lógica do script fornecido acima.

Para resolver o problema de uma ID de snapshot expirada, insira o seguinte comando no início do bloco anônimo. A linha de código a seguir substitui o `@from_snapshot_id` pelo `snapshot_id` mais antigo disponível nos metadados.

```SQL
SET resolve_fallback_snapshot_on_failure=true;
```

O bloco de código inteiro tem a seguinte aparência:

```SQL
$$ BEGIN
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
END
$$;
```

## Próximas etapas

Ao ler este documento, você deve entender melhor como usar os recursos de instantâneos e blocos anônimos para executar cargas incrementais e pode aplicar essa lógica às suas próprias consultas específicas. Para orientação geral sobre execução de consulta, leia o [guia sobre execução de consulta no Serviço de Consulta](../best-practices/writing-queries.md).
