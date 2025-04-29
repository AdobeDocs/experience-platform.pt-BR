---
title: Criar públicos-alvo usando SQL
description: Saiba como usar a extensão de público-alvo SQL no Data Distiller do Adobe Experience Platform para criar, gerenciar e publicar públicos-alvo usando comandos SQL. Este guia aborda todos os aspectos do ciclo de vida do público-alvo, incluindo a criação, atualização e exclusão de perfis e o uso de definições de público-alvo orientadas por dados para direcionar destinos baseados em arquivos.
exl-id: c35757c1-898e-4d65-aeca-4f7113173473
source-git-commit: 9e16282f9f10733fac9f66022c521684f8267167
workflow-type: tm+mt
source-wordcount: '1833'
ht-degree: 2%

---

# Criar públicos-alvo usando SQL

Use a extensão de público-alvo SQL para criar públicos-alvo com dados do data lake, incluindo quaisquer entidades de dimensão existentes (como atributos do cliente ou informações do produto).

Usar essa extensão SQL melhora sua capacidade de criar públicos, pois você não precisa de dados brutos em seus perfis ao definir segmentos de público. Os públicos-alvo criados usando esse método são registrados automaticamente no espaço de trabalho Público-alvo, onde você pode direcioná-los ainda mais para destinos baseados em arquivo.

![Infográfico que mostra o fluxo de trabalho da extensão de público-alvo do SQL. As etapas incluem: criar públicos-alvo com o Serviço de Consulta usando comandos SQL, gerenciando-os na interface do usuário do Experience Platform, para ativá-los em destinos baseados em arquivo.](../images/data-distiller/sql-audiences/sql-audience-extension-workflow.png)

Este documento aborda como usar a extensão de público-alvo SQL no Data Distiller da Adobe Experience Platform para criar, gerenciar e publicar públicos-alvo usando comandos SQL.

## Ciclo de vida de criação de público-alvo no Data Distiller {#audience-creation-lifecycle}

Siga estas etapas para criar, gerenciar e ativar públicos. Os públicos-alvo criados se integram perfeitamente ao &quot;fluxo de público-alvo&quot;, de modo que você possa criar segmentos a partir de públicos-alvo básicos e destinos baseados em arquivos de destino (por exemplo, uploads de CSV ou locais de armazenamento em nuvem) para alcance do cliente. &quot;Fluxo de público-alvo&quot; refere-se ao processo completo de criação, gerenciamento e ativação de públicos-alvo, garantindo uma integração perfeita entre os destinos.

Como parte do &#39;fluxo de público-alvo&#39;, use os seguintes comandos SQL para [criar](#create-audience), [modificar](#add-profiles-to-audience) e [excluir](#delete-audience) públicos-alvo no Adobe Experience Platform.

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
| `identity_namespace` | Namespace da identidade. Você pode usar um namespace existente ou criar um novo. Para ver os namespaces disponíveis, use o comando `SHOW NAMESPACES`. Para criar um novo namespace, use `CREATE NAMESPACE`. Por exemplo: `CREATE NAMESPACE lumaCrmId WITH (code='testns', TYPE='Email')`. |
| `select_query` | Uma instrução SELECT que define o público-alvo. A sintaxe da consulta SELECT pode ser encontrada na seção [consultas SELECT](../sql/syntax.md#select-queries). |

{style="table-layout:auto"}

>[!NOTE]
>
>Para fornecer maior flexibilidade para estruturas de dados complexas, é possível aninhar atributos enriquecidos ao definir públicos. Atributos enriquecidos, como `orders`, `total_revenue`, `recency`, `frequency` e `monetization`, podem ser usados para filtrar públicos conforme necessário.

**Exemplo:**

O exemplo a seguir demonstra como estruturar sua consulta de criação de público-alvo de SQL:

```sql
CREATE Audience aud_test
WITH (primary_identity=userId, identity_namespace=lumaCrmId)
AS SELECT userId, orders, total_revenue, recency, frequency, monetization FROM profile_dim_customer;
```

Neste exemplo, a coluna `userId` é identificada como a coluna de identidade e um namespace apropriado (`lumaCrmId`) é atribuído. As colunas restantes (`orders`, `total_revenue`, `recency`, `frequency` e `monetization`) são atributos enriquecidos que fornecem contexto adicional para o público-alvo.

**Limitações:**

Esteja ciente das seguintes limitações ao usar o SQL para criação de público-alvo:

- A coluna de identidade primária **deve** estar no nível mais alto do conjunto de dados, sem estar aninhada dentro de outros atributos ou categorias.
- Os públicos-alvo externos criados com comandos SQL têm um período de retenção de 30 dias. Após 30 dias, esses públicos-alvo são excluídos automaticamente, o que é uma consideração importante para o planejamento de estratégias de gerenciamento de público-alvo.

### Adicionar perfis a um público existente {#add-profiles-to-audience}

Use o comando `INSERT INTO` para adicionar perfis (ou públicos inteiros) a um público existente.

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
SELECT userId, orders, total_revenue, recency, frequency, monetization FROM customer_ds;
```

### Substituir dados do público-alvo (INSERIR SUBSTITUIR) {#replace-audience}

Use o comando `INSERT OVERWRITE INTO` para substituir todos os perfis existentes em um público-alvo pelos resultados de uma nova consulta SQL. Esse comando é útil para gerenciar segmentos de público-alvo dinâmicos, permitindo atualizar totalmente o conteúdo de um público-alvo em uma única etapa.

>[!AVAILABILITY]
>
>O comando `INSERT OVERWRITE INTO` está disponível somente para clientes do Data Distiller. Para saber mais sobre o complemento Data Distiller, entre em contato com o representante da Adobe.

Ao contrário de [`INSERT INTO`](#add-profiles-to-audience), que adiciona ao público-alvo atual, `INSERT OVERWRITE INTO` remove todos os membros existentes do público-alvo e insere somente aqueles retornados pela consulta. Isso proporciona maior controle e flexibilidade ao gerenciar públicos-alvo que exigem atualizações frequentes ou completas.

Use o modelo de sintaxe a seguir para substituir um público-alvo por um novo conjunto de perfis:

```sql
INSERT OVERWRITE INTO audience_name
SELECT select_query
```

**Parâmetros**

A tabela abaixo explica os parâmetros necessários para o comando `INSERT OVERWRITE INTO`:

| Parâmetro | Descrição |
|-----------|-------------|
| `audience_name` | O nome do público criado com o comando `CREATE AUDIENCE`. |
| `select_query` | Uma instrução `SELECT` que define os perfis a serem incluídos no público. |

**Exemplo:**

Neste exemplo, o público-alvo `audience_monthly_refresh` é completamente substituído pelos resultados da query. Todos os perfis não retornados pelo query são removidos do público-alvo.

>[!NOTE]
>
>Deve haver apenas um upload de lote associado ao público-alvo para que as operações de substituição funcionem corretamente.

```sql
INSERT OVERWRITE INTO audience_monthly_refresh
SELECT user_id FROM latest_transaction_summary WHERE total_spend > 100;
```

#### Comportamento de substituição de público-alvo no Perfil do cliente em tempo real

Ao substituir um público-alvo, o Perfil do cliente em tempo real aplica a seguinte lógica para atualizar a associação do perfil:

- Os perfis que aparecem somente no novo lote são marcados como inseridos.
- Os perfis que existiam somente no lote anterior são marcados como encerrados.
- Os perfis presentes em ambos os lotes são deixados inalterados (nenhuma operação é executada).

Isso garante que as atualizações de público sejam refletidas com precisão nos sistemas e fluxos de trabalho downstream.

**Exemplo de cenário**

Se uma audiência `A1` originalmente contém:

| ID | NOME |
|----|------|
| A | Tomada |
| B | John |
| C | Martha |

E a consulta de substituição retorna:

| ID | NOME |
|----|------|
| A | Stewart |
| C | Martha |

Em seguida, o público-alvo atualizado conterá:

| ID | NOME |
|----|------|
| A | Stewart |
| C | Martha |

O perfil B é removido, o perfil A é atualizado e o perfil C permanece inalterado.

Se a consulta de substituição incluir um novo perfil:

| ID | NOME |
|----|------|
| A | Stewart |
| C | Martha |
| D | Chris |

Então, o público final será:

| ID | NOME |
|----|------|
| A | Stewart |
| C | Martha |
| D | Chris |

### Exemplo de público-alvo do modelo RFM {#rfm-model-audience-example}

O exemplo a seguir demonstra como criar um público-alvo usando o modelo de Recenticidade, Frequência e Monetização (RFM). Este exemplo segmenta os clientes com base em suas pontuações de recenticidade, frequência e monetização para identificar grupos-chave, como clientes fiéis, novos clientes e clientes de alto valor.

<!--  Q) Since the focus of this document is on external audiences, or should I just include this temporarily? We could simply provide a link to the separate RFM modeling documentation rather than including the full example here. (Add link to new RFM document when it is published) -->

A consulta a seguir cria um esquema para o público-alvo de RFM. O demonstrativo configura campos para manter informações do cliente como `userId`, `days_since_last_purchase`, `orders`, `total_revenue`, e assim por diante.

```sql
CREATE Audience adls_rfm_profile
WITH (primary_identity=userId, identity_namespace=lumaCrmId) AS
SELECT
    cast(NULL AS string) userId,
    cast(NULL AS integer) days_since_last_purchase,
    cast(NULL AS integer) orders,
    cast(NULL AS decimal(18,2)) total_revenue,
    cast(NULL AS integer) recency,
    cast(NULL AS integer) frequency,
    cast(NULL AS integer) monetization,
    cast(NULL AS string) rfm_model
WHERE false;
```

Depois de criar o público-alvo, preencha-o com os dados do cliente e segmente os perfis com base em suas pontuações de RFM. A instrução SQL abaixo usa a função `NTILE(4)` para classificar clientes em quartis com base em suas pontuações RFM (Recency, Frequency, Monetização). Essas pontuações categorizam os clientes em seis segmentos, como &quot;Core&quot;, &quot;Loyal&quot; e &quot;Whales&quot;. Os dados segmentados do cliente são então inseridos na tabela de público-alvo `adls_rfm_profile`.&quot;

```sql
INSERT INTO Audience adls_rfm_profile
SELECT
    userId,
    days_since_last_purchase,
    orders,
    total_revenue,
    recency,
    frequency,
    monetization,
    CASE
        WHEN Recency=1 AND Frequency=1 AND Monetization=1 THEN '1. Core - Your Best Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency=1 AND Monetization IN (1,2,3,4) THEN '2. Loyal - Your Most Loyal Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN (1,2,3,4) AND Monetization=1 THEN '3. Whales - Your Highest Paying Customers'
        WHEN Recency IN(1,2,3,4) AND Frequency IN(1,2,3) AND Monetization IN(2,3,4) THEN '4. Promising - Faithful Customers'
        WHEN Recency=1 AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '5. Rookies - Your Newest Customers'
        WHEN Recency IN (2,3,4) AND Frequency=4 AND Monetization IN (1,2,3,4) THEN '6. Slipping - Once Loyal, Now Gone'
    END AS rfm_model
FROM (
    SELECT
        userId,
        days_since_last_purchase,
        orders,
        total_revenue,
        NTILE(4) OVER (ORDER BY days_since_last_purchase) AS recency,
        NTILE(4) OVER (ORDER BY orders DESC) AS frequency,
        NTILE(4) OVER (ORDER BY total_revenue DESC) AS monetization
    FROM (
        SELECT
            userid,
            DATEDIFF(current_date, MAX(purchase_date)) AS days_since_last_purchase,
            COUNT(purchaseid) AS orders,
            CAST(SUM(total_revenue) AS double) AS total_revenue
        FROM (
            SELECT DISTINCT
                ENDUSERIDS._EXPERIENCE.EMAILID.ID AS userid,
                commerce.`ORDER`.purchaseid AS purchaseid,
                commerce.`ORDER`.pricetotal AS total_revenue,
                TO_DATE(timestamp) AS purchase_date
            FROM sample_data_for_ootb_templates
            WHERE commerce.`ORDER`.purchaseid IS NOT NULL
        ) AS b
        GROUP BY userId
    )
);
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

### Registro e disponibilidade automáticos de público {#registration-and-availability}

Os públicos-alvo criados com a extensão SQL são registrados automaticamente na [!UICONTROL Origin] do Data Distiller no espaço de trabalho Público-alvo. Depois de registrados, esses públicos-alvo estão disponíveis para direcionamento em destinos baseados em arquivo, aprimorando a segmentação e as estratégias de direcionamento. Esse processo não requer configuração adicional, o que simplifica o gerenciamento de público-alvo. Para obter mais detalhes sobre como exibir, gerenciar e criar públicos-alvo na interface do Experience Platform, consulte a [Visão geral do Portal de público-alvo](../../segmentation/ui/audience-portal.md).

<!-- Q) Do you know how long it takes for the audience to register? This info would help manage user expectations. -->

![O espaço de trabalho Público-alvo na Adobe Experience Platform, mostrando os públicos-alvo da Data Distiller publicados automaticamente e prontos para uso.](../images/data-distiller/sql-audiences/audiences.png)

## Ativar públicos-alvo para os destinos {#activate-audiences}

Ative seus públicos direcionando-os para qualquer destino baseado em arquivo, como [!DNL Amazon S3], [!DNL SFTP] ou [!DNL Azure Blob]. Os atributos de público-alvo enriquecidos estão disponíveis para refinamento e filtragem adicionais, conforme necessário.

![Fluxograma de tipos de destino do Adobe Experience Platform, mostrando destinos públicos e privados/personalizados, incluindo opções de lote e streaming.](../images/data-distiller/sql-audiences/destination-types.png)

## Esclarecimentos sobre os recursos {#faqs}

Esta seção aborda as perguntas frequentes sobre como criar e gerenciar públicos-alvo externos usando SQL no Data Distiller.

**Perguntas**:

- A criação de públicos-alvo é compatível somente com conjuntos de dados simples?

+++Resposta

Atualmente, a criação de público-alvo é limitada a atributos simples (nível raiz) ao definir o público-alvo.

+++

- A criação do público-alvo resulta em um único conjunto de dados ou em vários conjuntos de dados, ou ela varia de acordo com a configuração?

+++Resposta

Há um mapeamento um para um entre um público-alvo e um conjunto de dados.

+++

- O conjunto de dados criado durante a criação de público-alvo está marcado para o Perfil?

+++Resposta

Não, o conjunto de dados criado durante a criação do público-alvo não está marcado para o Perfil.

+++

- O conjunto de dados foi criado no data lake?

+++Resposta

Sim, o conjunto de dados associado ao público-alvo é criado no data lake. Os atributos desse conjunto de dados estão disponíveis no Audience Composer e no fluxo de destino como atributos enriquecidos.

+++

- Os atributos no público-alvo estão restritos aos destinos baseados em arquivos em lote corporativo? (Sim ou Não)

+++Resposta

Não. Atributos enriquecidos no público-alvo estão disponíveis para uso em lotes corporativos e destinos baseados em arquivo. Se você encontrar um erro como &quot;As seguintes IDs de segmento têm namespaces que não são permitidos para esse destino: e917f626-a038-42f7-944c-xyxyx&quot;, crie um novo segmento no Data Distiller e use-o com qualquer destino disponível.

+++

- Posso criar um público-alvo que use um público-alvo do Data Distiller?

+++Resposta

Sim, você pode criar um público-alvo que use um público-alvo do Data Distiller.

+++

- Esses públicos-alvo aparecem no Adobe Journey Optimizer? Caso contrário, o que acontece quando crio um novo público-alvo no construtor de regras que inclui todos os membros desse público-alvo?

+++Resposta

Os públicos-alvo da Data Distiller também estão disponíveis no Adobe Journey Optimizer. Você pode usar os públicos-alvo da Data Distiller no Adobe Journey Optimizer e filtrar os resultados com base nos atributos enriquecidos.

+++

- Os públicos-alvo da Data Distiller são excluídos a cada 30 dias, já que são públicos-alvo externos?

+++Resposta

Sim, os públicos-alvo da Data Distiller são excluídos a cada 30 dias, pois são públicos-alvo externos.

+++

## Próximas etapas

Depois de ler este documento, você aprendeu a usar a extensão de público-alvo SQL no Data Distiller para criar, gerenciar e publicar públicos-alvo com eficiência usando comandos SQL. Agora é possível personalizar as definições de público-alvo com base nos requisitos exclusivos de sua empresa e ativá-las em vários destinos, otimizando suas estratégias de marketing e decisões orientadas por dados.

Em seguida, você pode ler a documentação a seguir para desenvolver e otimizar ainda mais suas estratégias de gerenciamento de público-alvo do Experience Platform:

- **Explorar avaliação de público-alvo**: saiba mais sobre os [métodos de avaliação de público-alvo no Adobe Experience Platform](../../segmentation/home.md#evaluate-segments): segmentação por transmissão para atualizações em tempo real, segmentação em lote para processamento agendado ou sob demanda e segmentação de borda para avaliação instantânea no Edge Network.
- **Integração com Destinos**: leia o guia sobre como [exportar arquivos sob demanda para destinos em lote](../../destinations/ui/export-file-now.md) usando a interface do usuário de Destinos do Experience Platform.
- **Revisar desempenho do público-alvo**: analise o desempenho de seus públicos definidos pelo SQL em diferentes canais. Use insights de dados para ajustar e melhorar as definições de público-alvo e as estratégias de direcionamento. Leia o documento em [Insights do público-alvo](../../dashboards/insights/audiences.md) para saber como acessar e adaptar as consultas SQL para insights do público-alvo no Adobe Real-Time CDP. Em seguida, você pode criar seus próprios insights e transformar dados brutos em informações acionáveis personalizando o painel Públicos-alvo para visualizar e usar esses insights com eficiência para melhorar a tomada de decisões.

