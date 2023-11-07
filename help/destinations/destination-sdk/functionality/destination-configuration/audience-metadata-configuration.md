---
description: Saiba como definir as configurações de metadados de público-alvo para destinos criados com o Destination SDK.
title: Configuração de metadados de público
exl-id: ae71df4f-b753-4084-835f-03559b4986cb
source-git-commit: 8f430fa3949c19c22732ff941e8c9b07adb37e1f
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 3%

---

# Configuração de metadados de público

Ao exportar dados do Experience Platform para o seu destino, talvez seja necessário que metadados de público-alvo específicos, como nomes de público-alvo ou IDs de público-alvo, sejam compartilhados entre o Experience Platform e o seu destino.

O Destination SDK oferece ferramentas que você pode usar para criar, atualizar ou excluir públicos-alvo de forma programática na plataforma de destino.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [usar o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-destination-configuration).

É possível configurar o modelo de metadados de público-alvo por meio da `/authoring/audience-templates` terminal. Depois de criar a configuração de metadados do público, você pode usar o `/authoring/destinations` endpoint para configurar o `audienceMetadataConfig` seção. Esta seção informa ao destino quais metadados de público-alvo ele deve mapear para o modelo de público-alvo.

Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Criar um modelo de público-alvo](../../metadata-api/create-audience-template.md)
* [Atualizar um modelo de público](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros compatíveis com o Destination SDK são **diferencia maiúsculas de minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Sim |

## Parâmetros compatíveis {#supported-parameters}

Ao criar a configuração de metadados de público-alvo, você pode usar os parâmetros descritos na tabela abaixo para definir as configurações de mapeamento de público-alvo.

```json
  "audienceMetadataConfig":{
   "mapExperiencePlatformSegmentName":false,
   "mapExperiencePlatformSegmentId":false,
   "mapUserInput":false,
   "audienceTemplateId":"YOUR_AUDIENCE_TEMPLATE_ID"
}
```

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `mapExperiencePlatformSegmentName` | Booleano | Indica se a variável [[!UICONTROL ID do mapeamento]](../../../ui/activate-segment-streaming-destinations.md#scheduling) no workflow de ativação de destino deve ser o nome do público-alvo Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Indica se a variável [[!UICONTROL ID do mapeamento]](../../../ui/activate-segment-streaming-destinations.md#scheduling) no workflow de ativação de destino deve ser a ID de público-alvo do Experience Platform. |
| `mapUserInput` | Booleano | Ativa ou desativa a entrada do usuário para o [[!UICONTROL ID do mapeamento]](../../../ui/activate-segment-streaming-destinations.md#scheduling) no workflow de ativação de destino. Se definida como `true`, `audienceTemplateId` não pode estar presente. |
| `audienceTemplateId` | Booleano | A variável `instanceId` do [modelo de metadados de público](../../metadata-api/create-audience-template.md) usado para o seu destino. |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Depois de ler este artigo, você deve entender melhor como configurar os metadados de público-alvo para o seu destino.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Configuração de autenticação do cliente](customer-authentication.md)
* [Autenticação OAuth2](oauth2-authorization.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento compatíveis](supported-mapping-configurations.md)
* [Entrega de destino](destination-delivery.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações do perfil histórico](historical-profile-qualifications.md)
