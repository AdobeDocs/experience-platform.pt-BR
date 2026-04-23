---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Apêndice do guia de API do Privacy Service
description: Este documento contém informações adicionais para trabalhar com a API do Privacy Service.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 36871289743f384207bb149df6e5e1af14d4d371
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 6%

---

# Apêndice do guia de API do Privacy Service

As seções a seguir contêm informações adicionais para trabalhar com a API do Adobe Experience Platform Privacy Service.

## Namespaces de identidade padrão {#standard-namespaces}

Todas as identidades enviadas para [!DNL Privacy Service] devem ser fornecidas em um namespace de identidade específico. Os namespaces de identidade são um componente do [Adobe Experience Platform Identity Service](../../identity-service/home.md) que indica o contexto ao qual uma identidade está relacionada.

A tabela a seguir descreve vários tipos de identidade predefinidos e comumente usados, disponibilizados por [!DNL Experience Platform], juntamente com seus valores `namespace` associados:

| Tipo de identidade | `namespace` | `namespaceId` |
| --- | --- | --- |
| Email | `Email` | `6` |
| Telefone | `Phone` | `7` |
| ADOBE ADVERTISING ID | `AdCloud` | `411` |
| UUID do Adobe Audience Manager | `CORE` | `0` |
| ADOBE EXPERIENCE CLOUD ID | `ECID` | `4` |
| ADOBE TARGET ID | `TNTID` | `9` |
| [!DNL Apple] ID para anunciantes | `IDFA` | `20915` |
| ID do anúncio [!DNL Google] | `GAID` | `20914` |
| [!DNL Windows] AJUDA | `WAID` | `8` |

{style="table-layout:auto"}

>[!NOTE]
>
>Cada tipo de identidade também tem um valor inteiro `namespaceId`, que pode ser usado no lugar da cadeia de caracteres `namespace` ao definir a propriedade `type` da identidade como &quot;namespaceId&quot;. Consulte a seção sobre [qualificadores de namespace](#namespace-qualifiers) para obter mais informações.

Você pode recuperar uma lista de namespaces de identidade em uso por sua organização fazendo uma solicitação GET para o ponto de extremidade `idnamespace/identities` na API [!DNL Identity Service]. Consulte o [guia do desenvolvedor do Serviço de Identidade](../../identity-service/api/getting-started.md) para obter mais informações.

## Qualificadores de namespace {#namespace-qualifiers}

Ao especificar um valor `namespace` na API [!DNL Privacy Service], um **qualificador de namespace** deve ser incluído em um parâmetro `type` correspondente. A tabela a seguir descreve os diferentes qualificadores de namespace aceitos.

| Qualificador | Definição |
| --------- | ---------- |
| `standard` | Um dos namespaces padrão definidos globalmente, não vinculado a um conjunto de dados de organização individual (por exemplo, email, número de telefone etc.). A ID do namespace é fornecida. |
| `custom` | Um namespace exclusivo criado no contexto de uma organização, não compartilhado em [!DNL Experience Cloud]. O valor representa o nome amigável (campo &quot;nome&quot;) a ser pesquisado. A ID do namespace é fornecida. |
| `integrationCode` | Código de integração - semelhante a &quot;personalizado&quot;, mas especificamente definido como o código de integração de uma fonte de dados a ser pesquisada. A ID do namespace é fornecida. |
| `namespaceId` | Indica que o valor é a ID real do namespace que foi criado ou mapeado por meio do serviço de namespace. |
| `unregistered` | Uma cadeia de caracteres de forma livre que não está definida no serviço de namespace e é obtida &quot;como está&quot;. Qualquer aplicativo que manipule esses tipos de namespaces verifica se eles são apropriados para o contexto da empresa e para o conjunto de dados. Nenhuma ID de namespace é fornecida. |
| `analytics` | Um namespace personalizado que é mapeado internamente em [!DNL Analytics], não no serviço de namespace. Isso é transmitido diretamente, conforme especificado pela solicitação original, sem uma ID de namespace |
| `target` | Um namespace personalizado compreendido internamente por [!DNL Target], não no serviço de namespace. Isso é transmitido diretamente, conforme especificado pela solicitação original, sem uma ID de namespace |

{style="table-layout:auto"}

## Valores de produto aceitos {#accepted-product-values}

Esta seção lista os valores de identificador de produto aceitos no atributo `include` ao criar trabalhos do Privacy Service (API ou IU). Use esses valores na matriz `include` de sua solicitação de trabalho.

A tabela a seguir lista os produtos compatíveis, seus nomes de exibição da interface do usuário e seus valores de código correspondentes.

>[!NOTE]
>
>- Os valores do produto não diferenciam maiúsculas de minúsculas; recomenda-se utilizar camel para manter a consistência.
>- Somente os produtos listados acima são compatíveis com a interface e a API. Se um produto não for provisionado para sua organização, ele poderá ser ignorado ou causar um erro de validação. Consulte seu contrato com a Adobe ou a documentação de provisionamento para confirmar os direitos.

| Nome do produto com marca | Nome de exibição da interface do usuário | Valor de `include` |
| ------------------------------------------------------ | -------------------------- | ---------------------------------------- |
| Adobe Analytics | [!UICONTROL Analytics] | `analytics` |
| Adobe Audience Manager | [!UICONTROL Audience Manager] | `audienceManager` |
| Adobe Advertising | [!UICONTROL Ad Cloud] | `adCloud` |
| Adobe Experience Platform (Loja de perfis) | [!UICONTROL Profile] | `profileService` |
| Adobe Experience Platform (data lake) | [!UICONTROL AEP Data Lake] | `aepDataLake` |
| Adobe Campaign | [!UICONTROL Campaign] | `campaign` |
| Adobe Target | [!UICONTROL Target] | `target` |
| Atributos do cliente | [!UICONTROL Customer Attributes (CRS)] | `CRS` |
| Adobe Journey Optimizer | [!UICONTROL Adobe Journey Optimizer] | `cjm` |
| Marketo Engage | [!UICONTROL Marketo Engage / AJO B2B] | `marketo` |
| Serviço de identidade | [!UICONTROL Identity] | `identity` |
| Marketo Measure | [!UICONTROL Marketo Measure] | `marketomeasure` |
| Adobe Commerce | [!UICONTROL Commerce (Personalization)] | `commerceMarketingData` |

{style="table-layout:auto"}
