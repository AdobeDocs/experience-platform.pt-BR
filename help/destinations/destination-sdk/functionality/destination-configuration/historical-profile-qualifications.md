---
description: Saiba mais sobre as qualificações de perfil históricas compatíveis com destinos criados com o Destination SDK.
title: Qualificações do perfil histórico
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 1%

---


# Qualificações do perfil histórico

Todos os destinos criados por Destination SDK oferecem suporte a qualificações de perfil históricas por padrão. Isso significa que quando os usuários configuram um fluxo de dados de ativação para seus destinos pela primeira vez, a primeira exportação contém todos os membros do segmento que já se qualificaram para esse segmento.

Esse comportamento é definido pela variável `"backfillHistoricalProfileData":true` parâmetro na configuração de destino.

>[!IMPORTANT]
>
>As qualificações de perfil histórico são habilitadas para todos os destinos criados por meio do Destination SDK e do `backfillHistoricalProfileData` parâmetro não configurável pelo usuário.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Sim |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when segments are activated to the destination. <br> <ul><li> `true`: [!DNL Platform] sends the historical user profiles that qualified for the segment before the segment is activated. </li><li> `false`: [!DNL Platform] only includes user profiles that qualify for the segment after the segment is activated. </li></ul> |

{style="table-layout:auto"} -->


## Próximas etapas {#next-steps}

Depois de ler este artigo, você deve saber que o Experience Platform exporta automaticamente uma população histórica de todos os perfis que já se qualificaram para um segmento ativado quando o segmento é exportado pela primeira vez para o destino. Essa opção não é configurável no Destination SDK ou na interface do usuário do Experience Platform.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação do cliente](customer-authentication.md)
* [Autenticação OAuth2](oauth2-authentication.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface](ui-attributes.md)
* [Configuração de esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento compatíveis](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuração de metadados de público](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)