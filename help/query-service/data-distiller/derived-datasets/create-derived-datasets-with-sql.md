---
title: Criar conjuntos de dados derivados com SQL
description: Saiba como usar o SQL para criar um conjunto de dados derivado que esteja ativado para o perfil e como usar o conjunto de dados para o Perfil do cliente em tempo real e o Serviço de segmentação.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 1%

---

# Criar conjuntos de dados derivados com SQL

Saiba como usar consultas SQL para manipular e transformar dados de conjuntos de dados existentes para criar um conjunto de dados derivado que esteja habilitado para o Perfil. Esse fluxo de trabalho fornece um método alternativo eficiente para criar conjuntos de dados derivados para seus casos de uso de negócios do Perfil do cliente em tempo real.

Este documento descreve várias extensões SQL convenientes que geram um conjunto de dados derivado para uso com o Perfil do cliente em tempo real. O fluxo de trabalho simplifica o processo que você teria que concluir por meio de várias chamadas de API ou interações da interface do Experience Platform.

Normalmente, gerar e publicar um conjunto de dados derivado para o Perfil do cliente em tempo real envolveria as seguintes etapas:

* Criar um namespace de identidade, se ainda não existir um.
* Crie o tipo de dados para armazenar o conjunto de dados derivado, se necessário.
* Crie um grupo de campos com esse tipo de dados para armazenar as informações do conjunto de dados derivado.
* Crie ou atribua uma coluna de identidade primária com o namespace criado anteriormente.
* Crie um esquema usando o grupo de campos e o tipo de dados criados anteriormente.
* Crie um novo conjunto de dados usando seu esquema e ative-o para o perfil, se necessário.
* Opcionalmente, marque um conjunto de dados como habilitado para perfil.

Depois de concluir as etapas mencionadas acima, você estará pronto para preencher o conjunto de dados. Se você ativou o conjunto de dados para o perfil, também é possível criar segmentos que se referem ao novo conjunto de dados e começar a produzir insights.

O Serviço de consulta permite executar todas as ações listadas acima usando consultas SQL. Isso inclui fazer alterações nos conjuntos de dados e grupos de campos, se necessário.

## Criar uma tabela com uma opção para habilitá-la para o perfil {#enable-dataset-for-profile}

>[!NOTE]
>
>A consulta SQL fornecida abaixo presume o uso de um namespace pré-existente.

Use uma consulta Criar tabela como seleção (CTAS) para criar um conjunto de dados, atribuir tipos de dados, definir uma identidade principal, criar um esquema e marcá-lo como habilitado para perfil. A instrução SQL de exemplo abaixo cria um conjunto de dados e o disponibiliza para o Real-Time Customer Data Platform (Real-Time CDP). Sua consulta SQL seguirá o formato mostrado no exemplo abaixo:

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

Os tipos de dados compatíveis são: boolean, date, datetime, text, float, bigint, integer, map, array e struct/row.

O bloco de código SQL abaixo fornece exemplos para definir tipos de dados de estrutura/linha, mapa e matriz. A linha um demonstra a sintaxe da linha. A linha dois demonstra a sintaxe do mapa, e a linha três, a sintaxe da matriz.

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

Como alternativa, os conjuntos de dados também podem ser habilitados para o perfil por meio da interface do usuário do Experience Platform. Para obter mais informações sobre como marcar um conjunto de dados como habilitado para o perfil, consulte a [documentação Habilitar um conjunto de dados para o Perfil do Cliente em Tempo Real](../../../catalog/datasets/user-guide.md#enable-profile).

Na consulta de exemplo abaixo, o conjunto de dados `decile_table` é criado com `id` como a coluna de identidade primária e tem o namespace `IDFA`. Ele também tem um campo chamado `decile1Month` do tipo de dados do mapa. A tabela criada (`decile_table`) está habilitada para o perfil.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

Após a execução bem-sucedida do query, a ID do conjunto de dados é retornada ao console, como pode ser visto no exemplo abaixo.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

Use `label='PROFILE'` em um comando `CREATE TABLE` para criar um conjunto de dados habilitado para perfil. O recurso `upsert` está ativado por padrão. A capacidade `upsert` pode ser substituída usando o comando `ALTER`, conforme demonstrado no exemplo abaixo.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Consulte a documentação da sintaxe SQL para obter mais informações sobre o uso do comando [ALTER TABLE](../../sql/syntax.md#alter-table) e do rótulo [como parte de uma consulta CTAS](../../sql/syntax.md#create-table-as-select).

## Construções para ajudar no gerenciamento de conjuntos de dados derivados por meio do SQL

Os recursos descritos abaixo são de grande benefício ao gerenciar conjuntos de dados derivados por meio do SQL.

### Alterar conjuntos de dados existentes para que sejam ativados para o perfil {#enable-existing-dataset-for-profile}

A construção ALTER TABLE SQL pode ser usada para tornar os conjuntos de dados existentes habilitados para o perfil. Isso requer que uma tag ativada por perfil seja adicionada ao esquema e ao conjunto de dados correspondente.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>Na execução bem-sucedida do comando `ALTER TABLE`, o console retorna `ALTER SUCCESS`.

### Adicionar uma identidade principal a um conjunto de dados existente {#add-primary-identity}

Marcar uma coluna existente em um conjunto de dados como um conjunto de identidades principal; caso contrário, ela resultará em um erro. Para definir uma identidade primária usando SQL, use o formato de consulta exibido abaixo.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Por exemplo:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

No exemplo fornecido, `id2` é uma coluna existente em `test1_dataset`.

### Desativar um conjunto de dados para o perfil {#disable-dataset-for-profile}

Se quiser desativar a tabela para uso de perfil, use o comando DROP. Um exemplo de instrução SQL que USA `DROP` é visto abaixo.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Por exemplo:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Esta instrução SQL fornece um método alternativo eficiente para usar uma chamada de API. Para obter mais informações, consulte a documentação sobre como [desabilitar um conjunto de dados para uso com o Real-Time CDP usando a API de conjuntos de dados](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### Permitir a funcionalidade de atualização e inserção para o conjunto de dados {#enable-upsert-functionality-for-dataset}

O comando UPSERT permite inserir um novo registro ou atualizar dados existentes em uma tabela. Especificamente, permite atualizar uma linha existente se um valor especificado já existir em uma tabela, ou inserir uma nova linha se o valor especificado ainda não existir.

Um exemplo de instrução que usa o formato correto é visto abaixo.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

Por exemplo:

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

Esta instrução SQL fornece um método alternativo eficiente para usar uma chamada de API. Para obter mais informações, consulte a documentação sobre como [habilitar um conjunto de dados para uso com o Real-Time CDP e UPSERT usando a API de conjuntos de dados](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### Desative a funcionalidade de atualização e inserção para o conjunto de dados {#disable-upsert-functionality-for-dataset}

Esse comando desativa a capacidade de atualizar e inserir linhas no conjunto de dados.

Um exemplo de instrução que usa o formato correto é visto abaixo.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

Por exemplo:

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### Mostrar informações adicionais da tabela associadas a cada tabela {#show-labels-for-tables}

Os metadados adicionais são mantidos para conjuntos de dados habilitados para perfis. Use o comando `SHOW TABLES` para exibir uma coluna `labels` extra que forneça informações sobre rótulos associados a tabelas.

Um exemplo da saída desse comando pode ser visto abaixo:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
|---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

Você pode ver no exemplo que `table_with_a_decile` foi habilitado para perfil e aplicado com rótulos como [&#39;SUBSTITUIR&#39;](#enable-upsert-functionality-for-dataset), [&#39;PERFIL&#39;](#enable-existing-dataset-for-profile) conforme descrito anteriormente.

### Criar um grupo de campos com SQL

Os grupos de campos agora podem ser criados por meio do SQL. Isso fornece uma alternativa ao uso do Editor de esquemas na interface do Experience Platform ou à realização de uma chamada de API para o registro do esquema.

Um exemplo de instrução para criar um grupo de campos pode ser visto abaixo.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>A criação do grupo de campos por meio do SQL falhará se o sinalizador `label` não for fornecido na instrução ou se o grupo de campos já existir.
>&#x200B;>Certifique-se de que a consulta inclua uma cláusula `IF NOT EXISTS` para evitar a falha da consulta porque o grupo de campos já existe.

Um exemplo real pode parecer semelhante ao mostrado abaixo.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

A execução bem-sucedida dessa instrução retorna a ID do grupo de campos criada. Por exemplo `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Consulte a documentação sobre como [criar um novo grupo de campos no Editor de Esquemas](../../../xdm/ui/resources/field-groups.md#create) ou usar a [API do Registro de esquemas](../../../xdm/api/field-groups.md#create) para obter mais informações sobre métodos alternativos.

### Soltar um grupo de campos

Ocasionalmente, pode ser necessário remover um grupo de campos do Registro de esquemas. Isso é feito executando o comando `DROP FIELDGROUP` com a ID do grupo de campos.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Por exemplo:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>A exclusão de um grupo de campos por meio do SQL falhará se o grupo de campos não existir. Certifique-se de que a instrução inclua uma cláusula `IF EXISTS` para evitar a falha da consulta.

### Mostrar todos os nomes e IDs de grupos de campos das tabelas

O comando `SHOW FIELDGROUPS` retorna uma tabela que contém o nome, fieldgroupId e o proprietário das tabelas.

Um exemplo da saída desse comando pode ser visto abaixo:

```sql
       name                      |        fieldgroupId                             |     owner      |
|---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## Próximas etapas

Depois de ler este documento, você compreenderá melhor como usar o SQL para criar um perfil e um conjunto de dados habilitado para upsert com base em conjuntos de dados derivados. Agora você está pronto para usar esse conjunto de dados com fluxos de trabalho de assimilação em lote para fazer atualizações nos dados do perfil. Para saber mais sobre assimilação de dados na Adobe Experience Platform, comece lendo a [visão geral da assimilação de dados](../../../ingestion/home.md).
