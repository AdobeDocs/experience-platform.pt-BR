---
title: Criar públicos-alvo usando SQL
description: Saiba como usar a extensão de público-alvo SQL no Data Distiller do Adobe Experience Platform para criar, gerenciar e publicar públicos-alvo usando comandos SQL. Este guia aborda todos os aspectos do ciclo de vida do público-alvo, incluindo a criação, atualização e exclusão de perfis e o uso de definições de público-alvo orientadas por dados para direcionar destinos baseados em arquivos.
source-git-commit: fbfd232c4e101f29ae01328c33763786a0e4a8cb
workflow-type: tm+mt
source-wordcount: '1267'
ht-degree: 1%

---

# Criar públicos-alvo usando SQL

Este documento aborda como usar a extensão de público-alvo SQL no Data Distiller da Adobe Experience Platform para criar, gerenciar e publicar públicos-alvo usando comandos SQL.

Use a extensão de público-alvo SQL para criar públicos-alvo com dados do data lake, incluindo quaisquer entidades de dimensão existentes. Essa extensão permite definir segmentos de público-alvo diretamente usando o SQL, oferecendo flexibilidade sem precisar de dados brutos em seus perfis. Os públicos-alvo criados usando esse método são registrados automaticamente no espaço de trabalho Público-alvo, onde você pode direcioná-los ainda mais para destinos baseados em arquivo.

![Infográfico que mostra o fluxo de trabalho da extensão de público-alvo do SQL. As etapas incluem: criar públicos-alvo com o Serviço de Consulta usando comandos SQL, gerenciando-os na interface da Platform, para ativá-los em destinos baseados em arquivo.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

## Ciclo de vida de criação de público-alvo no Data Distiller {#audience-creation-lifecycle}

Siga estas etapas para gerenciar efetivamente seus públicos-alvo. Os públicos-alvo criados se integram perfeitamente ao fluxo de público-alvo, permitindo criar segmentos a partir desses públicos-alvo básicos e direcionar destinos baseados em arquivos para o direcionamento do cliente. Use os seguintes comandos SQL para [criar](#create-audience), [modificar](#add-profiles-to-audience) e [excluir](#delete-audience) públicos-alvo no Adobe Experience Platform.

### Criar um público-alvo {#create-audience}

Use o comando `CREATE AUDIENCE AS SELECT` para definir um novo público-alvo. O público-alvo criado é salvo em um conjunto de dados e registrado no espaço de trabalho [!UICONTROL Públicos-alvo] na Data Distiller.

```sql
CREATE AUDIENCE table_name  
WITH (primary_identity='IdentitycolName', identity_namespace='Namespace for the identity used', [schema='target_schema_title']) 
AS (select_query)
```

**Parâmetros**

Use estes parâmetros para definir sua consulta de criação de público-alvo SQL:

| Parâmetro | Descrição |
|--------------------|------------------------------------------------------------------|
| `schema` | Opcional. Define o esquema XDM para o conjunto de dados criado pela consulta. |
| `table_name` | Nome da tabela e público-alvo. |
| `primary_identity` | Especifica a coluna de identidade primária para o público-alvo. |
| `identity_namespace` | Namespace da identidade. |
| `select_query` | Uma instrução SELECT que define o público-alvo. A sintaxe da consulta SELECT pode ser encontrada na seção [consultas SELECT](../sql/syntax.md#select-queries). |

{style="table-layout:auto"}

**Exemplo:**

O exemplo a seguir demonstra como estruturar sua consulta de criação de público-alvo de SQL:

```sql
CREATE Audience aud_test 
WITH (primary_identity=month, identity_namespace=queryService) 
AS SELECT month FROM profile_dim_date LIMIT 5;
```

**Limitações:**

Esteja ciente das seguintes limitações ao usar o SQL para criação de público-alvo:

- A coluna de identidade primária **deve** estar no nível raiz.
- Novos lotes substituem conjuntos de dados existentes; a funcionalidade de acréscimo não é compatível no momento.
- Atributos aninhados não são suportados no momento.

### Adicionar perfis a um público-alvo existente {#add-profiles-to-audience}

Use o comando `INSERT INTO` para adicionar perfis a um público existente.

```sql
INSERT INTO table_name 
SELECT select_query
```

**Parâmetros**

A tabela abaixo explica os parâmetros necessários para o comando `INSERT INTO`:

| Parâmetro | Descrição |
|----------------|--------------------------------------------------------------------------------|
| `table_name` | O nome da tabela criada como parte do comando create audience. |
| `select_query` | Uma instrução SELECT. A sintaxe da consulta SELECT pode ser encontrada na seção de consultas SELECT. |

{style="table-layout:auto"}

**Exemplo:**

O exemplo a seguir demonstra como adicionar perfis a um público-alvo existente com o comando `INSERT INTO`:

```sql
INSERT INTO Audience aud_test 
SELECT month FROM profile_dim_date LIMIT 10;
```

### Excluir um público (SOLTAR PÚBLICO) {#delete-audience}

Use o comando `DROP AUDIENCE` para excluir um público existente. Se o público-alvo não existir, uma exceção ocorrerá, a menos que `IF EXISTS` seja especificado.

```sql
DROP AUDIENCE [IF EXISTS] [db_name.]table_name
```

**Parâmetros**

A tabela contém os parâmetros necessários para o comando `DROP AUDIENCE`:

| Parâmetro | Descrição |
|----------------|----------------------------------------------------------------------------------------|
| `IF EXISTS` | Opcional. Se especificado, caso a tabela não seja encontrada, nenhuma exceção será gerada. |
| `db_name` | Especifica o grupo de dados usado para qualificar o conjunto de dados de público-alvo. |
| `table_name` | O nome da tabela criada como parte do comando create audience. |

{style="table-layout:auto"}

**Exemplo:**

O exemplo a seguir demonstra como excluir um público-alvo usando o comando DROP AUDIENCE:

```sql
DROP AUDIENCE IF EXISTS aud_test;
```

### Publicar públicos automaticamente {#auto-publish-audiences}

Os públicos-alvo criados usando a extensão SQL são registrados automaticamente no Data Distiller no espaço de trabalho do Público-alvo. Depois de registrados, esses públicos-alvo estão disponíveis para direcionamento e podem ser usados em destinos baseados em arquivos, aprimorando sua segmentação e estratégias de direcionamento.

![O espaço de trabalho Público-alvo na Adobe Experience Platform, mostrando os públicos-alvo da Data Distiller publicados automaticamente e prontos para uso.](../images/data-distiller/sql-audiences/audiences.png)

## Ativar públicos para destinos {#activate-audiences}

Ative seus públicos direcionando-os para qualquer destino baseado em arquivo, como [!DNL Amazon S3], [!DNL SFTP] ou [!DNL Azure Blob]. Os atributos de público-alvo enriquecidos estão disponíveis para refinamento e filtragem adicionais, conforme necessário.

![Fluxograma de tipos de destino do Adobe Experience Platform, mostrando destinos públicos e privados/personalizados, incluindo opções de lote e streaming.](../images/data-distiller/sql-audiences/destination-types.png)

## Esclarecimentos sobre os recursos {#faqs}

Esta seção aborda as perguntas frequentes sobre como criar e gerenciar públicos-alvo externos usando SQL no Data Distiller.

+++Selecione para revelar perguntas e respostas

- A criação de públicos-alvo é compatível somente com conjuntos de dados simples?
- Conjuntos de dados aninhados também são compatíveis, mas somente atributos simples estão disponíveis no público-alvo.

- A criação do público-alvo resulta em um único conjunto de dados ou em vários conjuntos de dados, ou ela varia de acordo com a configuração?
- Há um mapeamento um para um entre um público-alvo e um conjunto de dados.

- O conjunto de dados criado durante a criação de público-alvo está marcado para o Perfil?
- Não, o conjunto de dados criado durante a criação do público-alvo não está marcado para o Perfil.

- O conjunto de dados foi criado no data lake?
- Sim, o conjunto de dados é criado no data lake.

- Os atributos no público-alvo estão restritos a serem usados apenas em destinos baseados em arquivos em lote de empresas? (Sim ou Não)
- Sim, os atributos no público-alvo são restritos a serem usados somente em destinos baseados em arquivos em lote de empresas.

- Posso criar um público-alvo que use um público-alvo do Data Distiller?
- Sim, você pode criar um público-alvo que use um público-alvo do Data Distiller.

- Esses públicos-alvo aparecem no Adobe Journey Optimizer? Caso contrário, o que acontece quando crio um novo público-alvo no construtor de regras que inclui todos os membros desse público-alvo?
- Os públicos-alvo do destilador de dados não estão disponíveis no Adobe Journey Optimizer no momento. Você deve criar um novo público-alvo no construtor de regras do Adobe Journey Optimizer para que ele fique disponível no Adobe Journey Optimizer.

- Como devo criar dois públicos-alvo do Data Distiller com programações diferentes? Quantos conjuntos de dados são criados e estão marcados para Perfil?
- Dois conjuntos de dados serão criados, pois cada público tem um conjunto de dados subjacente. No entanto, esses conjuntos de dados não estão marcados para Perfil. Os dois conjuntos de dados são gerenciados em suas próprias programações individuais.

- Como excluir um público-alvo?
- Para excluir um público-alvo, você pode usar o [`DROP AUDIENCE` comando](#delete-audience) na interface de linha de comando ou usar as [ações rápidas do espaço de trabalho de públicos-alvo](../../segmentation/ui/audience-portal.md#quick-actions). OBSERVAÇÃO: públicos-alvo usados em destinos downstream ou que são dependentes em outros públicos-alvo não podem ser excluídos.

- Quando publico um público-alvo no Perfil, quando ele fica disponível na interface do construtor de segmentos e quando ele fica disponível nos Destinos?
- Quando a exportação do instantâneo do perfil for concluída, os perfis poderão ser vistos no público-alvo.

- Os públicos-alvo da Data Distiller são excluídos a cada 30 dias, já que são públicos-alvo externos?
- Sim, os públicos-alvo da Data Distiller são excluídos a cada 30 dias, pois são públicos-alvo externos.

- Os públicos-alvo da Data Distiller aparecem no inventário de públicos-alvo?
- Sim, os Públicos-alvo da Data Distiller aparecem no inventário de Públicos-alvo com o nome de origem &quot;Data Distiller&quot;.

+++

## Próximas etapas

Depois de ler este documento, você aprendeu a usar a extensão de público-alvo SQL no Data Distiller para criar, gerenciar e publicar públicos-alvo com eficiência usando comandos SQL. Agora é possível personalizar as definições de público-alvo com base nos requisitos exclusivos de sua empresa e ativá-las em vários destinos, otimizando suas estratégias de marketing e decisões orientadas por dados.

Em seguida, você pode ler a documentação a seguir para desenvolver e otimizar ainda mais suas estratégias de gerenciamento de público-alvo da Platform:

- **Explorar avaliação de público-alvo**: saiba mais sobre os [métodos de avaliação de público-alvo no Adobe Experience Platform](../../segmentation/home.md#evaluate-segments): segmentação por transmissão para atualizações em tempo real, segmentação em lote para processamento agendado ou sob demanda e segmentação de borda para avaliação instantânea no Edge Network.
- **Integração com Destinos**: leia o guia sobre como [exportar arquivos sob demanda para destinos em lote](../../destinations/ui/export-file-now.md) usando a interface do usuário de Destinos da Platform.
- **Revisar desempenho do público-alvo**: analise o desempenho de seus públicos definidos pelo SQL em diferentes canais. Use insights de dados para ajustar e melhorar as definições de público-alvo e as estratégias de direcionamento. Leia o documento em [Insights do público-alvo](../../dashboards/insights/audiences.md) para saber como acessar e adaptar as consultas SQL para insights do público-alvo no Adobe Real-time Customer Data Platform. Em seguida, você pode criar seus próprios insights e transformar dados brutos em informações acionáveis personalizando o painel Públicos-alvo para visualizar e usar esses insights com eficiência para melhorar a tomada de decisões.
