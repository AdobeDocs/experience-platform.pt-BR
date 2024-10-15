---
title: Insights do perfil da conta
description: Descubra o SQL que potencializa os insights do Perfil da conta e use essas consultas para gerar insights personalizados que exploram ainda mais seus clientes e as experiências do consumidor.
badgeB2B: label="Edição B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edição B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: a953dd56-7dd8-4cd0-baa0-85f92d192789
source-git-commit: ddf886052aedc025ff125c03ab63877cb049583d
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 1%

---

# Insights do perfil da conta

[Perfis de conta](../../rtcdp/accounts/account-profile-overview.md) são usados para consolidar informações de conta de várias fontes, incluindo vários canais de marketing e sistemas organizacionais. Essa visualização unificada permite uma compreensão abrangente das contas dos clientes, aprimorando as campanhas de marketing B2B. Os insights derivados da análise do seu modelo de dados tornam os seus dados B2B do Adobe Real-time Customer Data Platform mais acessíveis, compreensíveis e impactantes para a tomada de decisões.

Com acesso ao SQL que capacita seus insights, é possível entender melhor seus dados B2B e gerar seus próprios insights reutilizáveis altamente personalizados para explorar ainda mais as informações de conta do cliente. Transforme seus dados brutos em novos insights acionáveis usando o SQL modelo de dados do Real-Time CDP existente como inspiração para criar consultas para suas necessidades comerciais exclusivas.

<!-- Add link to new generate insights with SQL workflow doc after April release.-->

Os seguintes insights estão todos disponíveis para você usar como parte do [painel de Perfis de Conta](../guides/account-profiles.md) ou de um [painel personalizado](../standard-dashboards.md). Consulte a [visão geral da personalização](../customize/overview.md) para obter instruções sobre como personalizar seu painel ou [criar e editar novos widgets](../customize/custom-widgets.md) na biblioteca de widgets e no [painel definido pelo usuário](../standard-dashboards.md#create-widget).

## Perfis de conta adicionados {#account-profiles-added}

Perguntas respondidas por este insight:

- Quantos perfis de conta foram adicionados em um determinado período?

+++Selecione para revelar o SQL que gera esse insight

```sql
WITH accounts_by_mm_dd AS
(
          SELECT    d.date_key,
                    COALESCE(Sum(a.counts), 0) AS account_counts
          FROM      adwh_b2b_date d
          LEFT JOIN adwh_fact_account a
          ON        d.date_key = a.accounts_created_date
          WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
          GROUP BY  d.date_key)
SELECT   date_key,
         account_counts
FROM     accounts_by_mm_dd
ORDER BY date_key limit 5000;
```

+++

## Novas contas por setor {#accounts-by-industry}

Perguntas respondidas por este insight:

- Quais são os cinco principais setores aos quais os perfis de conta pertencem?

+++Selecione para revelar o SQL que gera esse insight

```sql
WITH rankedindustries AS
(
           SELECT     i.industry,
                      Sum(f.counts)                                   AS total_accounts,
                      Row_number() OVER (ORDER BY Sum(f.counts) DESC) AS industry_rank
           FROM       adwh_fact_account f
           INNER JOIN adwh_dim_industry i
           ON         f.industry_id = i.industry_id
           WHERE      f.accounts_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           GROUP BY   i.industry )
SELECT
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END                 AS industry_group,
         Sum(total_accounts) AS total_accounts
FROM     rankedindustries
GROUP BY
         CASE
                  WHEN industry_rank <= 5 THEN industry
                  ELSE 'Others'
         END
ORDER BY total_accounts DESC limit 5000;
```

+++

## Novas contas por tipo {#accounts-by-type}

Perguntas respondidas por este insight:

- Qual é a contagem de contas por seu tipo?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT t.account_type,
       Sum(f.counts) AS account_count
FROM   adwh_fact_account f
       JOIN adwh_dim_account_type t
         ON f.account_type_id = t.account_type_id
WHERE  accounts_created_date BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                                     Upper(
                                     Coalesce('$END_DATE', ''))
GROUP  BY t.account_type
LIMIT  5000; 
```

+++

## Oportunidades adicionadas {#opportunities-added}

Perguntas respondidas por este insight:

- Quantas oportunidades foram adicionadas em um determinado período?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT d.date_key,
       Coalesce(Sum(o.counts), 0) AS opportunity_counts
FROM   adwh_b2b_date d
       LEFT JOIN adwh_fact_opportunity o
              ON d.date_key = o.opportunities_created_date
WHERE  d.date_key BETWEEN Upper(Coalesce('$START_DATE', '')) AND
                          Upper(Coalesce('$END_DATE', ''))
GROUP  BY d.date_key
ORDER  BY d.date_key
LIMIT  5000; 
```

+++

## Novas oportunidades por função de pessoa {#opportunities-by-person-role}

Perguntas respondidas por este insight:

- Qual é o tamanho relativo e a contagem das várias funções em uma oportunidade?

+++Selecione para revelar o SQL que gera esse insight

```sql
SELECT p.person_role,
       Sum(f.counts) AS opportunity_counts
FROM   adwh_fact_opportunity_person f
       JOIN adwh_dim_person_role p
         ON f.person_role_id = p.person_role_id
WHERE  f.opportunity_person_created_date BETWEEN
       Upper(Coalesce('$START_DATE', '')) AND Upper(Coalesce('$END_DATE', ''))
GROUP  BY p.person_role
LIMIT  5000; 
```

+++

## Novas oportunidades por receita {#opportunities-by-revenue}

Perguntas respondidas por este insight:

- Quais são as 20 principais oportunidades classificadas por sua receita (em dólares americanos)?

+++Selecione para revelar o SQL que gera esse insight

```sql
WITH ranked_opportunities AS
(
           SELECT     n.opportunity_name,
                      a.expected_revenue,
                      t.source_type,
                      Row_number() OVER (ORDER BY a.expected_revenue DESC) AS rank
           FROM       adwh_opportunity_amount a
           INNER JOIN adwh_dim_opportunity_name n
           ON         a.name_id = n.name_id
           INNER JOIN adwh_dim_opportunity_source_type t
           ON         n.source_type_id = t.source_type_id
           WHERE      a.opportunity_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND        Upper(COALESCE('$END_DATE', ''))
           AND        a.isclosed='false' )
SELECT
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END                   AS opportunity_name,
         Sum(expected_revenue) AS total_expected_revenue
FROM     ranked_opportunities
GROUP BY
         CASE
                  WHEN rank <= 20 THEN opportunity_name
                  ELSE 'Others'
         END,
         source_type
ORDER BY total_expected_revenue DESC limit 5000;
```

+++

## Novas oportunidades por status e estágio {#opportunities-by-status-and-stage}

Perguntas respondidas por este insight:

- Quais são as oportunidades abertas e em que estágio do funil de vendas ou marketing elas estão?
- Quais oportunidades fechadas existem e em que estágio do funil de vendas ou marketing elas estão?

+++Selecione para revelar o SQL que gera esse insight

```sql
WITH opportunities_by_isclosed AS
(
         SELECT   f.isclosed,
                  Sum(f.counts)             AS opportunity_counts,
                  COALESCE(s.stage, 'null') AS stage
         FROM     adwh_fact_opportunity f
         JOIN     adwh_dim_opportunity_stage s
         ON       f.stage_id = s.stage_id
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY f.isclosed,
                  s.stage)
SELECT
       CASE
              WHEN isclosed='true' THEN 'Closed'
              ELSE 'Open'
       END AS opportunity_closed,
       stage,
       opportunity_counts
FROM   opportunities_by_isclosed limit 5000;
```

+++

## Novas oportunidades conquistadas {#opportunities-won}

Perguntas respondidas por este insight:

- Qual é a contagem de oportunidades que foram fechadas ou finalizadas com sucesso?

+++Selecione para revelar o SQL que gera esse insight

```sql
WITH opportunities_by_iswon AS
(
         SELECT   iswon,
                  Sum(counts) AS opportunity_counts
         FROM     adwh_fact_opportunity
         WHERE    opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY iswon)
SELECT
       CASE
              WHEN iswon ='true' THEN 'True'
              ELSE 'False'
       END AS opportunity_won,
       opportunity_counts
FROM   opportunities_by_iswon limit 5000;
```

+++

## Oportunidades conquistadas (gráfico de linhas) {#opportunities-won-line-graph}

<!-- Q) Can we change this name? -->

Perguntas respondidas por este insight:

- Quantas oportunidades foram fechadas ou finalizadas com êxito (conquistadas) em um determinado período?

+++Selecione para revelar o SQL que gera esse insight

```sql
WITH opportunities_won_counts AS
(
         SELECT   opportunities_created_date,
                  Sum(counts) AS opportunities_counts
         FROM     adwh_fact_opportunity
         WHERE    iswon='true'
         AND      opportunities_created_date BETWEEN Upper(COALESCE('$START_DATE', '')) AND      Upper(COALESCE('$END_DATE', ''))
         GROUP BY opportunities_created_date)
SELECT    d.date_key,
          COALESCE(o.opportunities_counts, 0) AS opportunity_won_counts
FROM      adwh_b2b_date d
LEFT JOIN opportunities_won_counts o
ON        d.date_key = o.opportunities_created_date
WHERE     d.date_key BETWEEN Upper(COALESCE('$START_DATE', '')) AND       Upper(COALESCE('$END_DATE', ''))
ORDER BY  d.date_key limit 5000;
```

+++

## Próximas etapas

Ao ler este documento, você agora entende o SQL que gera insights do painel de perfil da conta e quais perguntas comuns essa análise resolve. Agora você pode editar e iterar no SQL para gerar seus próprios insights.

<!-- Add link above Learn how to [generate insights with SQL](). after April release -->

Você também pode ler e entender o SQL que gera insights para os painéis [Perfis](./profiles.md), [Públicos-alvo](./audiences.md) e [Destinos](./destinations.md).
