---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Apêndice do Guia API do Privacy Service
topic: developer guide
description: Este documento contém informações adicionais para trabalhar com a API Privacy Service.
translation-type: tm+mt
source-git-commit: b395535cbe7e4030606ee2808eb173998f5c32e0
workflow-type: tm+mt
source-wordcount: '501'
ht-degree: 9%

---


# apêndice do guia da API Privacy Service

As seções a seguir contêm informações adicionais para trabalhar com a API do Adobe Experience Platform Privacy Service.

## Namespaces de identidade padrão {#standard-namespaces}

Todas as identidades enviadas para [!DNL Privacy Service] devem ser fornecidas em uma namespace de identidade específica. As namespaces de identidade são um componente do [Adobe Experience Platform Identity Service](../../identity-service/home.md) que indica o contexto ao qual uma identidade está relacionada.

A tabela a seguir descreve vários tipos de identidade predefinidos e comumente usados, disponibilizados por [!DNL Experience Platform], juntamente com seus valores associados de `namespace`:

| Tipo de identidade | `namespace` | `namespaceId` |
| --- | --- | --- |
| Email | Email | 6 |
| Telefone | Telefone | 7 |
| Adobe Advertising Cloud ID | AdCloud | 411 |
| Adobe Audience Manager UUUID | CORE | 0 |
| Adobe Experience Cloud ID | ECID | 4 |
| Adobe Target ID | TNTID | 9 |
| [!DNL Apple] ID para anunciantes | IDFA | 2015 |
| [!DNL Google] ID do anúncio | GAID | 2014 |
| [!DNL Windows] auxílio | WAID | 8 |

>[!NOTE]
>
>Cada tipo de identidade também tem um valor inteiro `namespaceId`, que pode ser usado no lugar da string `namespace` ao definir a propriedade `type` da identidade como &quot;namespaceId&quot;. Consulte a seção sobre [qualificadores de namespace](#namespace-qualifiers) para obter mais informações.

Você pode recuperar uma lista de namespaces de identidade em uso pela sua organização, fazendo uma solicitação de GET para o terminal `idnamespace/identities` na API [!DNL Identity Service]. Consulte o [Guia do desenvolvedor do Serviço de Identidade](../../identity-service/api/getting-started.md) para obter mais informações.

## Qualificadores de namespace

Ao especificar um valor `namespace` na API [!DNL Privacy Service], um qualificador **de namespace** deve ser incluído em um parâmetro `type` correspondente. A tabela a seguir descreve os diferentes qualificadores de namespace aceitos.

| Qualificador | Definição |
| --------- | ---------- |
| padrão | Uma das namespaces padrão definidas globalmente, não vinculada a um conjunto de dados de organização individual (por exemplo, email, número de telefone etc.). ID da namespace fornecida. |
| custom | Uma namespace exclusiva criada no contexto de uma organização, não compartilhada em [!DNL Experience Cloud]. O valor representa o nome amigável (campo &quot;nome&quot;) a ser pesquisado. ID da namespace fornecida. |
| integrationCode | Código de integração - semelhante ao &quot;personalizado&quot;, mas definido especificamente como o código de integração de uma fonte de dados a ser pesquisada. ID da namespace fornecida. |
| namespaceId | Indica que o valor é a ID real da namespace que foi criada ou mapeada pelo serviço de namespace. |
| não registrado | Uma string de forma livre que não é definida no serviço de namespace e é tomada &quot;como está&quot;. Qualquer aplicativo que manipule esses tipos de namespaces verifica e lida com eles se for apropriado para o contexto da empresa e o conjunto de dados. Nenhuma ID de namespace é fornecida. |
| analytics | Uma namespace personalizada que é mapeada internamente em [!DNL Analytics], não no serviço de namespace. Isso é passado diretamente conforme especificado pela solicitação original, sem uma ID de namespace |
| target | Uma namespace personalizada compreendida internamente por [!DNL Target], não no serviço de namespace. Isso é passado diretamente conforme especificado pela solicitação original, sem uma ID de namespace |

## Valores do produto aceitos

A tabela a seguir descreve os valores aceitos para especificar um Adobe no atributo `include` de uma solicitação de criação de trabalho.

| Produto | Valor para uso no atributo `include` |
--- | ---
| Adobe Advertising Cloud | &quot;AdCloud&quot; |
| Adobe Analytics | &quot;Analytics&quot; |
| Adobe Audience Manager | &quot;AudienceManager&quot; |
| Adobe Campaign | &quot;Campaign&quot; |
| Adobe Experience Platform | &quot;aepDataLake&quot; |
| Autenticação Adobe Primetime | &quot;primetimeAuthentication&quot; |
| Adobe Target | &quot;Target&quot; |
| Serviço de Registro do Cliente | &quot;CRS&quot; |
| Perfil do cliente em tempo real | &quot;ProfileService&quot; |