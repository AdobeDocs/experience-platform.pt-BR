---
description: Saiba como definir as configurações de metadados de público-alvo para destinos criados com o Destination SDK.
title: Configuração de metadados de público
exl-id: ae71df4f-b753-4084-835f-03559b4986cb
source-git-commit: 804370a778a4334603f3235df94edaa91b650223
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 3%

---

# Configuração de metadados de público

Ao exportar dados do Experience Platform para o seu destino, talvez você precise que metadados de público-alvo específicos, como nomes de público-alvo ou IDs de público-alvo, sejam compartilhados entre o Experience Platform e o seu destino.

O Destination SDK oferece ferramentas que você pode usar para criar, atualizar ou excluir públicos-alvo de forma programática na plataforma de destino.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama na documentação de [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [usar o Destination SDK para configurar um destino de streaming](../../guides/configure-destination-instructions.md#create-destination-configuration).

Você pode configurar o modelo de metadados de público por meio do ponto de extremidade `/authoring/audience-templates`. Depois de criar a configuração de metadados de público, você pode usar o terminal `/authoring/destinations` para configurar as seções `segmentMappingConfig` e `audienceMetadataConfig`. Esta seção informa ao destino quais metadados de público-alvo ele deve mapear para o modelo de público-alvo.

Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Criar um modelo de público-alvo](../../metadata-api/create-audience-template.md)
* [Atualizar um modelo de público](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1&rbrace;.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Sim |

## Parâmetros compatíveis {#supported-parameters}

Ao criar a configuração de metadados de público-alvo, você pode usar os parâmetros descritos na tabela abaixo para definir as configurações de mapeamento de público-alvo.

```json
"segmentMappingConfig": {
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
 },
"audienceMetadataConfig":{
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Booleano | Indica se o valor [[!UICONTROL ID de Mapeamento]](../../../ui/activate-segment-streaming-destinations.md#scheduling) no fluxo de trabalho de ativação de destino deve ser o nome de público-alvo do Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Indica se o valor [[!UICONTROL ID de Mapeamento]](../../../ui/activate-segment-streaming-destinations.md#scheduling) no fluxo de trabalho de ativação de destino deve ser a ID de público-alvo da Experience Platform. |
| `mapUserInput` | Booleano | Habilita ou desabilita a entrada do usuário para o valor [[!UICONTROL ID de Mapeamento]](../../../ui/activate-segment-streaming-destinations.md#scheduling) no fluxo de trabalho de ativação de destino. Se definido como `true`, `audienceTemplateId` não pode estar presente. |
| `audienceTemplateId` | String | O `instanceId` do [modelo de metadados de público-alvo](../../metadata-api/create-audience-template.md) usado para o seu destino. |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Depois de ler este artigo, você deve entender melhor como configurar os metadados de público-alvo para o seu destino.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Configuração de autenticação do cliente](customer-authentication.md)
* [Autorização OAuth2](oauth2-authorization.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento compatíveis](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações do perfil histórico](historical-profile-qualifications.md)
