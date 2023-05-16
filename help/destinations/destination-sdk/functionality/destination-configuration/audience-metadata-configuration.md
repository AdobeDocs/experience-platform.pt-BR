---
description: Saiba como definir as configurações de metadados do público-alvo para destinos criados com o Destination SDK.
title: Configuração de metadados de público-alvo
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 2%

---


# Configuração de metadados de público-alvo

Ao exportar dados do Experience Platform para seu destino, você pode precisar que metadados de público-alvo específicos, como nomes de segmento ou IDs de segmento, sejam compartilhados entre o Experience Platform e seu destino.

O Destination SDK oferece ferramentas que você pode usar para criar, atualizar ou excluir públicos-alvo de forma programática na plataforma de destino.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou consulte o guia sobre como [use o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-destination-configuration).

Você pode configurar o modelo de metadados de público-alvo por meio da variável `/authoring/audience-templates` endpoint . Depois de criar a configuração dos metadados do público-alvo, você pode usar o `/authoring/destinations` endpoint para configurar a variável `audienceMetadataConfig` seção. Esta seção informa ao destino quais metadados de segmento devem ser mapeados para o modelo de público-alvo.

Consulte as páginas de referência da API a seguir para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)
* [Criar um modelo de público-alvo](../../metadata-api/create-audience-template.md)
* [Atualizar um modelo de público-alvo](../../metadata-api/update-audience-template.md)

>[!IMPORTANT]
>
>Todos os nomes de parâmetros e valores suportados pelo Destination SDK são **distinção entre maiúsculas e minúsculas**. Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações oferecem suporte à funcionalidade descrita nesta página.

| Tipo de integração | Oferece suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (em lote) | Sim |

## Parâmetros compatíveis {#supported-parameters}

Ao criar a configuração dos metadados do público-alvo, você pode usar os parâmetros descritos na tabela abaixo para definir as configurações de mapeamento de segmentos.

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
| `mapExperiencePlatformSegmentName` | Booleano | Indica se a variável [[!UICONTROL ID de mapeamento]](../../../ui/activate-segment-streaming-destinations.md#scheduling) no fluxo de trabalho de ativação de destino deve ser o nome do segmento Experience Platform. |
| `mapExperiencePlatformSegmentId` | Booleano | Indica se a variável [[!UICONTROL ID de mapeamento]](../../../ui/activate-segment-streaming-destinations.md#scheduling) no fluxo de trabalho de ativação de destino deve ser a ID de segmento de Experience Platform. |
| `mapUserInput` | Booleano | Ativa ou desativa a entrada do usuário para a variável [[!UICONTROL ID de mapeamento]](../../../ui/activate-segment-streaming-destinations.md#scheduling) no workflow de ativação de destino. Se estiver definido como `true`, `audienceTemplateId` não pode estar presente. |
| `audienceTemplateId` | Booleano | O `instanceId` do [modelo de metadados de público-alvo](../../metadata-api/create-audience-template.md) usado para o seu destino. |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Após ler este artigo, você deve ter uma melhor compreensão de como pode configurar os metadados do público-alvo para o seu destino.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Configuração de autenticação do cliente](customer-authentication.md)
* [Autenticação OAuth2](oauth2-authentication.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Atributos da interface do usuário](ui-attributes.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento suportadas](supported-mapping-configurations.md)
* [Delivery de destino](destination-delivery.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações de perfil histórico](historical-profile-qualifications.md)