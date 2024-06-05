---
title: Edição B2B do Modelo de dados do Real-time Customer Data Platform Insights
description: Saiba como usar consultas SQL com os Modelos de dados do Real-time Customer Data Platform Insights (B2B Edition) para personalizar seus próprios relatórios do Real-Time CDP para seus casos de uso de marketing e KPI.
badgeB2B: label="Edição B2B" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
badgeB2P: label="Edição B2P" type="Informative" url="https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform-b2p-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 7b77ca19-e4c6-4e93-b9e7-c4ef77d6d6d1
source-git-commit: e94343e61e98f69fa28ecd61aec9267460a7f616
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 0%

---

# Edição B2B do modelo de dados do Real-time Customer Data Platform Insights

O modelo de dados do Real-time Customer Data Platform Insights para o B2B Edition expõe os modelos de dados e o SQL que potencializam os insights para [perfis de conta](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/account/account-profile-overview). Você pode personalizar esses modelos de consulta SQL para criar relatórios do Real-Time CDP para seus casos de uso de marketing B2B e KPI (indicador chave de desempenho). Esses insights podem ser usados como widgets personalizados para seus painéis.

>[!AVAILABILITY]
>
>Essa funcionalidade está disponível para clientes que compraram o pacote Real-Time CDP Prime e Ultimate. Consulte a documentação sobre [Edições do Real-Time CDP](../../rtcdp/overview.md#rtcdp-editions) para obter mais informações ou entre em contato com o representante da Adobe.

<!-- 
See the query accelerated store reporting insights documentation to learn [how to build a reporting insights data model through Query Service for use with accelerated store data and user-defined dashboards](../../query-service/data-distiller/customizable-insights/reporting-insights-data-model.md).
 -->

## Pré-requisitos

Este guia requer entendimento prático de painéis personalizados. Leia a documentação em [como criar um painel personalizado](../user-defined-dashboards.md) antes de continuar com este guia.

## Relatórios de insight B2B do Real-Time CDP e casos de uso {#B2B-insight-reports-and-use-cases}

Os relatórios B2B do Real-Time CDP fornecem insights sobre os dados dos perfis de conta e a relação entre contas e oportunidades. Os seguintes modelos de esquema estrela foram desenvolvidos para responder a uma variedade de casos de uso de marketing comuns e cada modelo de dados pode suportar vários casos de uso.

>[!IMPORTANT]
>
>Os dados usados para os relatórios B2B do Real-Time CDP são precisos para uma política de mesclagem escolhida e do instantâneo diário mais recente.

### Modelo de perfil da conta {#account-profile-model}

O modelo de Perfil de conta é composto de oito conjuntos de dados:

- `adwh_dim_industry`
- `adwh_dim_account_name`
- `adwh_dim_geo`
- `adwh_dim_account_type`
- `adwh_fact_account`
- `account_revenue_employee`

O diagrama abaixo exibe os campos de dados relevantes em cada conjunto de dados, seus tipos de dados e as chaves estrangeiras que vinculam os conjuntos de dados.

![O diagrama relacional de entidade para o modelo de Perfil de Conta.](../images/data-models/account-profile-model.png)

#### As novas contas por caso de uso de setor {#accounts-by-industry}

A lógica usada para o [!UICONTROL Novas contas por setor] o insight retorna os cinco principais setores de acordo com o número de perfis de conta e o tamanho relativo entre si. Consulte a [[!UICONTROL Novas contas por setor] documentação do widget](../guides/account-profiles.md#accounts-by-industry) para obter mais informações.

>[!TIP]
>
>Você pode personalizar essa consulta SQL para retornar mais ou menos do que os cinco principais setores.

O SQL que gera a variável [!UICONTROL Novas contas por setor] o insight é visto na seção recolhível abaixo.

Consulta +++SQL

```sql
WITH RankedIndustries AS (
    SELECT
        i.industry,
        SUM(f.counts) AS total_accounts,
        ROW_NUMBER() OVER (ORDER BY SUM(f.counts) DESC) AS industry_rank
    FROM
        adwh_fact_account f
    INNER JOIN adwh_dim_industry i ON f.industry_id = i.industry_id
    WHERE f.accounts_created_date between UPPER(COALESCE('$START_DATE', '')) and UPPER(COALESCE('$END_DATE', ''))
    GROUP BY
        i.industry
)
SELECT
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END AS industry_group,
    SUM(total_accounts) AS total_accounts
FROM
    RankedIndustries
GROUP BY
    CASE
        WHEN industry_rank <= 5 THEN industry
        ELSE 'Others'
    END
ORDER BY
    total_accounts DESC
LIMIT 5000;
```

+++

#### O caso de uso Novas contas por tipo {#accounts-by-type}

A lógica usada para o [!UICONTROL Novas contas por tipo] insight retorna o detalhamento numérico das contas por seu tipo. Este insight pode ajudar a orientar a estratégia e as operações de negócios, incluindo a alocação de recursos ou as estratégias de marketing. Consulte a [[!UICONTROL Novas contas por tipo] documentação do widget](../guides/account-profiles.md#accounts-by-type) para obter mais informações.

O SQL que gera a variável [!UICONTROL Novas contas por tipo] o insight é visto na seção recolhível abaixo.

Consulta +++SQL

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

### Modelo de oportunidade {#opportunity-model}

O modelo de oportunidade é composto de sete conjuntos de dados:

- `adwh_dim_opportunity_stage`
- `adwh_dim_person_role`
- `adwh_dim_opportunity_source_type`
- `adwh_dim_opportunity_name`
- `adwh_fact_opportunity`
- `adwh_opportunity_amount`
- `adwh_fact_opportunity_person`

O diagrama abaixo exibe os campos de dados relevantes em cada conjunto de dados.

![O diagrama relacional da entidade para o Modelo de oportunidade.](../images/data-models/opportunity-model.png)
