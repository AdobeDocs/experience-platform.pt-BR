---
title: Fluxo SQL simplificado para atributos derivados
description: O SQL do Serviço de Consulta foi estendido para fornecer suporte contínuo a atributos derivados. Saiba como usar esta extensão SQL para criar um atributo derivado que esteja ativado para o perfil e como usar o atributo para o Perfil do cliente em tempo real e o Serviço de segmentação.
exl-id: bb1a1d8d-4662-40b0-857a-36efb8e78746
source-git-commit: 6202b1a5956da83691eeb5422d3ebe7f3fb7d974
workflow-type: tm+mt
source-wordcount: '1238'
ht-degree: 1%

---

# Fluxo SQL simplificado para atributos derivados

O SQL do Serviço de Consulta foi estendido para fornecer suporte contínuo a atributos derivados. Isso fornece um método alternativo eficiente para criar atributos derivados para seus casos de uso de negócios do Perfil do cliente em tempo real.

Este documento descreve várias extensões SQL convenientes que geram um atributo derivado para uso com o Perfil do cliente em tempo real. O fluxo de trabalho simplifica o processo que você teria que concluir por meio de várias chamadas de API ou interações da interface do usuário da plataforma.

Geralmente, gerar e publicar um atributo para o Perfil do cliente em tempo real envolveria as seguintes etapas:

* Crie um namespace de identidade, se ele ainda não existir.
* Crie o tipo de dados para armazenar o atributo derivado, se necessário.
* Crie um grupo de campos com esse tipo de dados para armazenar as informações do atributo derivado.
* Crie ou atribua uma coluna de identidade primária com o namespace criado anteriormente.
* Crie um schema usando o grupo de campos e o tipo de dados criados anteriormente.
* Crie um novo conjunto de dados usando seu esquema e ative-o para o perfil, se necessário.
* Como opção, marque um conjunto de dados como habilitado para perfil.

Após concluir as etapas mencionadas acima, você estará pronto para preencher o conjunto de dados. Se você ativou o conjunto de dados para o perfil, também pode criar segmentos que se referem ao novo atributo e começar a produzir insights.

O Serviço de Consulta permite executar todas as ações listadas acima usando consultas SQL. Isso inclui fazer alterações em seus conjuntos de dados e grupos de campos, se necessário.

## Criar uma tabela com uma opção para habilitá-la para o perfil {#enable-dataset-for-profile}

>[!NOTE]
>
>A consulta SQL fornecida abaixo assume o uso de um namespace pré-existente.

Use uma consulta Criar tabela como seleção (CTAS) para criar um conjunto de dados, atribuir tipos de dados, definir uma identidade primária, criar um esquema e marcá-lo como habilitado para perfil. O exemplo da instrução SQL abaixo cria atributos e a disponibiliza para o Perfil de dados do cliente em tempo real (Real-Time CDP). Sua consulta SQL seguirá o formato mostrado no exemplo abaixo:

```sql
CREATE TABLE <your_table_name> [IF NOT EXISTS] (fieldname <your_data_type> primary identity namespace <your_namespace>, [field_name2 <your_data_type>]) [WITH(LABEL='PROFILE')];
```

Os tipos de dados compatíveis são: booleano, data, datetime, texto, flutuante, bigint, número inteiro, mapa, matriz e struct/linha.

O codeblock do SQl abaixo fornece exemplos para definir tipos de dados de estrutura/linha, mapa e matriz. A primeira linha demonstra a sintaxe da linha. A linha dois demonstra a sintaxe do mapa e a linha três, a sintaxe do storage.

```sql {line-numbers="true"}
ROW (Column_name <data_type> [, column name <data_type> ]*)
MAP <data_type, data_type>
ARRAY <data_type>
```

Como alternativa, os conjuntos de dados também podem ser ativados para perfil por meio da interface do usuário da plataforma. Para obter mais informações sobre como marcar um conjunto de dados como ativado para o perfil, consulte o [ativar um conjunto de dados para a documentação do Perfil do cliente em tempo real](../../../catalog/datasets/user-guide.md#enable-profile).

No exemplo de query abaixo, a variável `decile_table` o conjunto de dados é criado com `id` como a coluna de identidade primária e tem o namespace `IDFA`. Também tem um campo chamado `decile1Month` do tipo de dados de mapa. A tabela criada (`decile_table`) está ativado para perfil.

```sql
CREATE TABLE decile_table (id text PRIMARY KEY NAMESPACE 'IDFA', 
            decile1Month map<text, integer>) WITH (label='PROFILE');
```

Ao executar com sucesso o query, a ID do conjunto de dados é retornada ao console, como mostrado no exemplo abaixo.

```console
Created Table DataSet Id
>
637fd84969ba291e62dba79f
(1 row)
```

Use `label='PROFILE'` em um `CREATE TABLE` para criar um conjunto de dados habilitado para perfil. O `upsert` está ativada por padrão. O `upsert` pode ser substituída usando o `ALTER` , conforme demonstrado no exemplo abaixo.

```sql
ALTER TABLE <your_table_name> DROP label upsert;
```

Consulte a documentação da sintaxe do SQl para obter mais informações sobre o uso da variável [ALTERAR TABELA](../../sql/syntax.md#alter-table) e [como parte de uma consulta CTAS](../../sql/syntax.md#create-table-as-select).

## Constrói para ajudar no gerenciamento de atributos derivados por meio do SQL

Os recursos descritos abaixo são de grande benefício ao gerenciar atributos derivados por meio do SQL.

### Alterar conjuntos de dados existentes para serem habilitados para o perfil {#enable-existing-dataset-for-profile}

A construção ALTER TABLE SQL pode ser usada para tornar os conjuntos de dados existentes ativados para o perfil. Isso requer que uma tag ativada por perfil seja adicionada ao esquema e ao conjunto de dados correspondente.

```sql
ALTER TABLE your_decile_table ADD label 'PROFILE';
```

>[!NOTE]
>
>Na execução bem-sucedida do `ALTER TABLE` , o console retorna `ALTER SUCCESS`.

### Adicionar uma identidade primária a um conjunto de dados existente {#add-primary-identity}

Marcar uma coluna existente em um conjunto de dados como um conjunto de identidades primário; caso contrário, resultará em um erro. Para definir uma identidade primária usando SQL, use o formato de consulta exibido abaixo.

```sql
ALTER TABLE <your_table_name> ADD CONSTRAINT primary identity NAMESPACE
```

Por exemplo:

```sql
ALTER TABLE test1_dataset ADD CONSTRAINT PRIMARY KEY(id2) NAMESPACE 'IDFA';
```

No exemplo fornecido, `id2` é uma coluna existente em `test1_dataset`.

### Desativar um conjunto de dados para o perfil {#disable-dataset-for-profile}

Se quiser desativar a tabela para usos de perfil, use o comando DROP. Um exemplo de instrução SQL que usa `DROP` é visto abaixo.

```sql
ALTER TABLE table_name DROP LABEL 'PROFILE';
```

Por exemplo:

```sql
ALTER TABLE decile_table DROP label 'PROFILE';
```

Esta instrução SQL fornece um método alternativo eficiente para usar uma chamada de API. Para obter mais informações, consulte a documentação sobre como [desativar um conjunto de dados para usar com o Real-Time CDP usando a API de conjuntos de dados](../../../catalog/datasets/enable-upsert.md#disable-the-dataset-for-profile).

### Permitir atualização e inserir funcionalidade em seu conjunto de dados {#enable-upsert-functionality-for-dataset}

O comando UPSERT permite inserir um novo registro ou atualizar dados existentes em uma tabela. Especificamente, isso permite atualizar uma linha existente se um valor especificado já existir em uma tabela ou inserir uma nova linha se o valor especificado ainda não existir.

Um exemplo de declaração que usa o formato correto é visto abaixo.

```sql
ALTER TABLE table_name ADD LABEL 'UPSERT';
```

Por exemplo:

```sql
ALTER TABLE table_with_a_decile ADD label 'UPSERT';
```

Esta instrução SQL fornece um método alternativo eficiente para usar uma chamada de API. Para obter mais informações, consulte a documentação sobre como [ativar um conjunto de dados para uso com o Real-Time CDP e o UPSERT usando a API de conjuntos de dados](../../../catalog/datasets/enable-upsert.md#enable-the-dataset).

### Desativar a funcionalidade de atualização e inserção do conjunto de dados {#disable-upsert-functionality-for-dataset}

Esse comando desativa a capacidade de atualizar e inserir linhas no conjunto de dados.

Um exemplo de declaração que usa o formato correto é visto abaixo.

```sql
ALTER TABLE table_name DROP LABEL 'UPSERT';
```

Por exemplo:

```sql
ALTER TABLE table_with_a_decile DROP label 'UPSERT';
```

### Mostrar informações adicionais da tabela associadas a cada tabela {#show-labels-for-tables}

Metadados adicionais são mantidos para conjuntos de dados habilitados para perfil. Use o `SHOW TABLES` comando para exibir um extra `labels` coluna que fornece informações em qualquer rótulo associado a tabelas.

Um exemplo da saída deste comando pode ser visto abaixo:

```sql
       name          |        dataSetId         |     dataSet    | description | labels 
---------------------+--------------------------+----------------+-------------+----------
 luma_midvalues      | 5bac030c29bb8d12fa992e58 | Luma midValues |             | false
 luma_postvalues     | 5c86b896b3c162151785b43c | Luma midValues |             | false
 table_with_a_decile | 5c86b896b3c162151785b43c | Luma midValues |             | 'UPSERT', 'PROFILE'
(3 rows)
```

Você pode ver pelo exemplo que `table_with_a_decile` foi ativado para o perfil e aplicado com rótulos como [&#39;UPSERT&#39;](#enable-upsert-functionality-for-dataset), [&#39;PERFIL&#39;](#enable-existing-dataset-for-profile) conforme descrito anteriormente.

### Criar um grupo de campos com SQL

Os grupos de campos agora podem ser criados por meio do uso do SQL. Isso fornece uma alternativa ao uso do Editor de esquema na interface do usuário da plataforma ou à realização de uma chamada de API para o registro do esquema.

Um exemplo de instrução para criar um grupo de campos pode ser visto abaixo.

```sql
CREATE FIELDGROUP <field_group_name> [IF NOT EXISTS]  (field_name <data_type> primary identity namespace <namespace>, [field_name_2 >data_type>]) [ WITH(LABEL='PROFILE') ];
```

>[!IMPORTANT]
>
>A criação do grupo de campos por meio do SQL falhará se a variável `label` O sinalizador não é fornecido na instrução ou se o grupo de campos já existir.
>Certifique-se de que o query inclua uma `IF NOT EXISTS` para evitar que a consulta falhe porque o grupo de campos já existe.

Um exemplo do mundo real pode aparecer de forma semelhante ao visto abaixo.

```sql
CREATE FIELDGROUP field_group_for_test123 (decile1Month map<text, integer>, decile3Month map<text, integer>, decile6Month map<text, integer>, decile9Month map<text, integer>, decile12Month map<text, integer>, decilelietime map<text, integer>) WITH (LABEL-'PROFILE');
```

A execução bem-sucedida dessa instrução retorna a ID do grupo de campos criada. Por exemplo `c731a1eafdfdecae1683c6dca197c66ed2c2b49ecd3a9525`.

Consulte a documentação sobre como [criar um novo grupo de campos no Editor de esquemas](../../../xdm/ui/resources/field-groups.md#create) ou usando a [API do Registro de Esquema](../../../xdm/api/field-groups.md#create) para obter mais informações sobre métodos alternativos.

### Soltar um grupo de campos

Ocasionalmente, pode ser necessário remover um grupo de campos do Registro de Schema. Isso é feito executando o `DROP FIELDGROUP` com a ID do grupo de campos.

```sql
DROP FIELDGROUP [IF EXISTS] <your_field_group_id>;
```

Por exemplo:

```sql
DROP FIELDGROUP field_group_for_test123;
```

>[!IMPORTANT]
>
>A exclusão de um grupo de campos por meio do SQL falhará se o grupo de campos não existir. Certifique-se de que a instrução inclua um `IF EXISTS` para evitar a falha da consulta.

### Mostrar todos os nomes e IDs de grupos de campos para suas tabelas

O `SHOW FIELDGROUPS` retorna uma tabela que contém o nome, fieldgroupId e o proprietário das tabelas.

Um exemplo da saída deste comando pode ser visto abaixo:

```sql
       name                      |        fieldgroupId                             |     owner      |
---------------------------------+-------------------------------------------------+-----------------
 AEP Mobile Lifecycle Details    | _experience.aep-mobile-lifecycle-details        | Luma midValues |
 AEP Web SDK ExperienceEvent     | _experience.aep-web-sdk-experienceevent         | Luma midValues |
 AJO Classification Fields       | _experience.journeyOrchestration.classification | Luma midValues |
 AJO Entity Fields               | _experience.customerJourneyManagement.entities  | Luma midValues |
(4 rows)
```

## Próximas etapas

Após a leitura deste documento, você tem uma melhor compreensão de como usar o SQL para criar um perfil e um conjunto de dados habilitado para atualização com base em atributos derivados. Agora você está pronto para usar esse conjunto de dados com fluxos de trabalho de assimilação em lote para fazer atualizações nos dados do perfil. Para saber mais sobre como assimilar dados no Adobe Experience Platform, comece lendo o [visão geral da assimilação de dados](../../../ingestion/home.md).
