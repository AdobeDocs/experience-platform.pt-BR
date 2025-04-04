---
description: Saiba mais sobre as qualificações de perfil histórico compatíveis com destinos criados com o Destination SDK.
title: Qualificações do perfil histórico
exl-id: 8880cff9-865b-4d45-a24d-a78e77419670
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '214'
ht-degree: 2%

---

# Qualificações do perfil histórico

Todos os destinos criados por meio do Destination SDK oferecem suporte a qualificações de perfil histórico por padrão. Isso significa que quando os usuários configuram um fluxo de dados de ativação para seus destinos pela primeira vez, a primeira exportação contém todos os membros do público-alvo que já se qualificaram para esse segmento.

Esse comportamento é definido pelo parâmetro `"backfillHistoricalProfileData":true` na configuração de destino.

>[!IMPORTANT]
>
>As qualificações de perfil histórico são habilitadas para todos os destinos criados por meio do Destination SDK e o parâmetro `backfillHistoricalProfileData` não é configurável pelo usuário.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Sim |



<!-- 
|Parameter | Type | Description|
|---------|----------|------|
|`backfillHistoricalProfileData` | Boolean | Controls whether historical profile data is exported when audiences are activated to the destination. <br> <ul><li> `true`: [!DNL Experience Platform] sends the historical user profiles that qualified for the audience before the audience is activated. </li><li> `false`: [!DNL Experience Platform] only includes user profiles that qualify for the audience after the audience is activated. </li></ul> |

{style="table-layout:auto"} -->


## Próximas etapas {#next-steps}

Depois de ler este artigo, você deve saber que o Experience Platform exporta automaticamente uma população histórica de todos os perfis que já se qualificaram para um público-alvo ativado quando o público-alvo é exportado pela primeira vez para o destino. Essa opção não pode ser configurada no Destination SDK ou na interface do usuário do Experience Platform.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação do cliente](customer-authentication.md)
* [Autorização OAuth2](oauth2-authorization.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento compatíveis](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Configuração de metadados de público](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
