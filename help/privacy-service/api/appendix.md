---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: namespaces de identidade e qualificadores aceitos
topic: developer guide
translation-type: tm+mt
source-git-commit: d0fcae6b1b75584a2c26d6eee5b47e0d60a142ba

---


# Apêndice

## namespaces de identidade padrão

Todas as identidades enviadas ao Privacy Service devem ser fornecidas sob uma namespace de identidade específica. As namespaces de identidade são um componente do Serviço [de identidade da plataforma](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_services_architectural_overview/identity_services_architectural_overview.md) Adobe Experience que indica o contexto ao qual uma identidade está relacionada.

A tabela a seguir descreve vários tipos de identidade predefinidos e comumente usados, disponibilizados pela plataforma de experiência, juntamente com seus `namespace` valores associados:

| Tipo de identidade | `namespace` | `namespaceId` |
| --- | --- | --- |
| Email | Email | 6 |
| Telefone | Telefone | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| UUID do Adobe Audiência Manager | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| ID do Público alvo da Adobe | TNTID | 9 |
| Apple ID para anunciantes | IDFA | 20915 |
| ID do Google Ad | GAID | 20914 |
| Windows AID | WAID | 8 |

>[!NOTE] Cada tipo de identidade também tem um valor `namespaceId` inteiro, que pode ser usado no lugar da `namespace` string ao definir a `type` propriedade da identidade como &quot;namespaceId&quot;. Consulte a seção sobre qualificadores [de](#namespace-qualifiers) namespace para obter mais informações.

Você pode recuperar uma lista de namespaces de identidade em uso pela sua organização, fazendo uma solicitação GET para o `idnamespace/identities` endpoint na API do Serviço de Identidade. Consulte o guia [do desenvolvedor do Serviço de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_services_architectural_overview/identity_services_api.md) identidade para obter mais informações.

## Qualificadores de Namespace

Ao especificar um `namespace` valor na API do Privacy Service, um qualificador **de** namespace deve ser incluído em um `type` parâmetro correspondente. A tabela a seguir descreve os diferentes qualificadores de namespace aceitos.

| Qualificador | Definição |
| --------- | ---------- |
| padrão | Uma das namespaces padrão definidas globalmente, não vinculada a um conjunto de dados de organização individual (por exemplo, email, número de telefone etc.). ID da Namespace fornecida. |
| custom | Uma namespace exclusiva criada no contexto de uma organização, não compartilhada na Experience Cloud. O valor representa o nome amigável (campo &quot;nome&quot;) a ser pesquisado. ID da Namespace fornecida. |
| integrationCode | Código de integração - semelhante ao &quot;personalizado&quot;, mas definido especificamente como o código de integração de uma fonte de dados a ser pesquisada. ID da Namespace fornecida. |
| namespaceId | Indica que o valor é a ID real da namespace que foi criada ou mapeada pelo serviço de namespace. |
| não registrado | Uma string de forma livre que não é definida no serviço de namespace e é tomada &quot;como está&quot;. Qualquer aplicativo que manipule esses tipos de namespaces verifica e lida com eles se for apropriado para o contexto da empresa e o conjunto de dados. Nenhuma ID de namespace é fornecida. |
| analytics | Uma namespace personalizada que é mapeada internamente no Analytics, não no serviço de namespace. Isso é passado diretamente conforme especificado pela solicitação original, sem uma ID de namespace |
| target | Uma namespace personalizada entendida internamente pelo Público alvo, não pelo serviço de namespace. Isso é passado diretamente conforme especificado pela solicitação original, sem uma ID de namespace |

## Valores do produto aceitos

A tabela a seguir descreve os valores aceitos para especificar um produto da Adobe no `include` atributo de uma solicitação de criação de trabalho.

| Produto | Valor para uso no `include` atributo |
--- | ---
| Adobe Advertizing Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Autenticação do Adobe Primetime | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| Serviço de Registro do Cliente | &quot;CRS&quot; |
| Perfil do cliente em tempo real | &quot;ProfileService&quot; |