---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Apêndice do guia da API do Privacy Service
topic-legacy: developer guide
description: Este documento contém informações adicionais para trabalhar com a API do Privacy Service.
exl-id: 7099e002-b802-486e-8863-0630d66e330f
source-git-commit: 1a84ebfa0ad7801e14896dffd28302f057ae171d
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 7%

---

# Apêndice do guia da API do Privacy Service

As seções a seguir contêm informações adicionais para trabalhar com a API do Adobe Experience Platform Privacy Service.

## Namespaces de identidade padrão {#standard-namespaces}

Todas as identidades enviadas para [!DNL Privacy Service] deve ser fornecido em um namespace de identidade específico. Os namespaces de identidade são um componente do [Serviço de identidade da Adobe Experience Platform](../../identity-service/home.md) que indicam o contexto ao qual uma identidade está relacionada.

A tabela a seguir descreve vários tipos de identidade predefinidos e usados com frequência, disponibilizados por [!DNL Experience Platform], juntamente com os `namespace` valores:

| Tipo de identidade | `namespace` | `namespaceId` |
| --- | --- | --- |
| Email | `Email` | `6` |
| Telefone | `Phone` | `7` |
| Adobe Advertising Cloud ID | `AdCloud` | `411` |
| UUID do Adobe Audience Manager | `CORE` | `0` |
| Adobe Experience Cloud ID | `ECID` | `4` |
| Adobe Target ID | `TNTID` | `9` |
| [!DNL Apple] ID para anunciantes | `IDFA` | `20915` |
| [!DNL Google] ID do anúncio | `GAID` | `20914` |
| [!DNL Windows] AID | `WAID` | `8` |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>Cada tipo de identidade também tem uma `namespaceId` valor inteiro, que pode ser usado no lugar do `namespace` ao definir o `type` para &quot;namespaceId&quot;. Consulte a seção sobre [qualificadores de namespace](#namespace-qualifiers) para obter mais informações.

Você pode recuperar uma lista de namespaces de identidade em uso pela sua organização, fazendo uma solicitação do GET para a `idnamespace/identities` endpoint no [!DNL Identity Service] API. Consulte a [Guia do desenvolvedor do Serviço de identidade](../../identity-service/api/getting-started.md) para obter mais informações.

## Qualificadores de namespace

Ao especificar uma `namespace` na variável [!DNL Privacy Service] API, um **qualificador de namespace** deve ser incluída em um `type` parâmetro. A tabela a seguir descreve os diferentes qualificadores de namespace aceitos.

| Qualificador | Definição |
| --------- | ---------- |
| `standard` | Um dos namespaces padrão definidos globalmente, não vinculado a um conjunto de dados individual da organização (por exemplo, email, número de telefone etc.). A ID de namespace é fornecida. |
| `custom` | Um namespace exclusivo criado no contexto de uma organização, não compartilhado no [!DNL Experience Cloud]. O valor representa o nome amigável (campo &quot;nome&quot;) a ser pesquisado. A ID de namespace é fornecida. |
| `integrationCode` | Código de integração - semelhante ao &quot;personalizado&quot;, mas definido especificamente como o código de integração de uma fonte de dados a ser pesquisada. A ID de namespace é fornecida. |
| `namespaceId` | Indica que o valor é a ID real do namespace que foi criada ou mapeada pelo serviço de namespace. |
| `unregistered` | Uma string de forma livre que não é definida no serviço de namespace e é considerada &quot;como está&quot;. Qualquer aplicativo que manipule esses tipos de namespaces verifica-os e lida, se apropriado, com o contexto da empresa e o conjunto de dados. Nenhuma ID de namespace é fornecida. |
| `analytics` | Um namespace personalizado que é mapeado internamente em [!DNL Analytics], não no serviço de namespace. Isso é transmitido diretamente, conforme especificado pela solicitação original, sem uma ID de namespace |
| `target` | Um namespace personalizado compreendido internamente por [!DNL Target], não no serviço de namespace. Isso é transmitido diretamente, conforme especificado pela solicitação original, sem uma ID de namespace |

{style=&quot;table-layout:auto&quot;}

## Valores do produto aceitos

A tabela a seguir descreve os valores aceitos para especificar um produto de Adobe no `include` de uma solicitação de criação de emprego.

| Produto | Valor para uso na variável `include` atributo |
| --- | --- |
| Adobe Advertising Cloud | `adCloud` |
| Adobe Analytics | `analytics` |
| Adobe Audience Manager | `AudienceManager` |
| Adobe Campaign | `campaign` |
| Adobe Experience Platform (Data Lake) | `aepDataLake` |
| Adobe Experience Platform (Perfil do cliente em tempo real) | `profileService` |
| Autenticação Adobe Primetime | `primetimeAuthentication` |
| Adobe Target | `target` |
| Atributos do cliente (CRS) | `CRS` |
| Identity Service | `identity` |
| Marketo Engage | `marketo` |

{style=&quot;table-layout:auto&quot;}
