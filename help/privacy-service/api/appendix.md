---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Apêndice do guia de API do Privacy Service
description: Este documento contém informações adicionais para trabalhar com a API Privacy Service.
role: Developer
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 644e85fe5c9b1a37f69c75755713e929736c2e89
workflow-type: tm+mt
source-wordcount: '496'
ht-degree: 5%

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
| ADOBE ADVERTISING CLOUD ID | `AdCloud` | `411` |
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

## Qualificadores de namespace

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

## Valores de produto aceitos

A tabela a seguir descreve os valores aceitos para especificar um produto Adobe no atributo `include` de uma solicitação de criação de trabalho.

>[!NOTE]
>
>Os valores da lista de produtos não diferenciam maiúsculas de minúsculas. Camel-case é recomendado, mas não é aplicado.

| Produto | Valor para uso no atributo `include` |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `audienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (data lake) | `aepDataLake` |
| Adobe Experience Platform (Perfil do cliente em tempo real) | `profileService` |
| Adobe Pass Authentication | `primetimeAuthentication` |
| Adobe Target | `target` |
| Atributos do cliente (CRS) | `CRS` |
| Gerenciamento de Jornada do cliente | `cjm` |
| Serviço de identidade | `identity` |
| Marketo Engage | `marketo` |
| Marketo Measure | `marketomeasure` |

{style="table-layout:auto"}
