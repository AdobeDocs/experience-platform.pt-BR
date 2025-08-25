---
description: Saiba como definir as configurações de entrega de destino para destinos criados com o Destination SDK, para indicar para onde os dados exportados vão e qual regra de autenticação é usada no local onde os dados serão direcionados.
title: Entrega de destino
exl-id: ade77b6b-4b62-4b17-a155-ef90a723a4ad
source-git-commit: 560200a6553a1aae66c608eef7901b3248c886b4
workflow-type: tm+mt
source-wordcount: '641'
ht-degree: 2%

---

# Entrega de destino

Para oferecer mais controle sobre onde os dados exportados chegam ao seu destino, o Destination SDK permite especificar as configurações de entrega de destino.

A seção delivery de destino indica para onde os dados exportados vão e qual regra de autenticação é usada no local onde os dados serão direcionados.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama na documentação das [opções de configuração](../configuration-options.md) ou consulte as seguintes páginas de visão geral da configuração de destino:

* [Usar o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Você pode definir as configurações de entrega de destino por meio do ponto de extremidade `/authoring/destinations`. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as opções de entrega de destino compatíveis que você pode usar para o seu destino.

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

Ao definir as configurações do delivery de destino, você pode usar os parâmetros descritos na tabela abaixo para definir para onde os dados exportados devem ser enviados.

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `authenticationRule` | String | Indica como [!DNL Experience Platform] deve se conectar ao seu destino. Valores compatíveis:<ul><li>`CUSTOMER_AUTHENTICATION`: use esta opção se os clientes da Experience Platform fizerem logon no sistema por meio de qualquer um dos métodos de autenticação descritos [aqui](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: use esta opção se houver um sistema de autenticação global entre o Adobe e seu destino e o cliente do [!DNL Experience Platform] não precisar fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando a configuração da [API de credenciais](../../credentials-api/create-credential-configuration.md) e definir o parâmetro `authenticationId` como o valor da ID do objeto de credencial.</li><li>`NONE`: use essa opção se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `authenticationId` | String | O `instanceId` da ID de configuração do objeto de credencial a ser usada para autenticação. Esse parâmetro só é necessário quando você precisa especificar uma configuração de credenciais específica. |
| `destinationServerId` | String | O `instanceId` do [servidor de destino](../../authoring-api/destination-server/create-destination-server.md) para o qual você deseja exportar dados. |
| `deliveryMatchers.type` | String | <ul><li>Ao configurar a entrega de destino para destinos baseados em arquivo, sempre defina como `SOURCE`.</li><li>Ao configurar a entrega de destino para um destino de streaming, a seção `deliveryMatchers` não é necessária.</li></ul> |
| `deliveryMatchers.value` | String | <ul><li>Ao configurar a entrega de destino para destinos baseados em arquivo, sempre defina como `batch`.</li><li>Ao configurar a entrega de destino para um destino de streaming, a seção `deliveryMatchers` não é necessária.</li></ul> |

{style="table-layout:auto"}

## Configurações de entrega de destino para destinos de streaming {#destination-delivery-streaming}

O exemplo abaixo mostra como as configurações de delivery de destino devem ser definidas para um destino de streaming. Observe que a seção `deliveryMatchers` não é necessária para destinos de streaming.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Configurações de entrega de destino para destinos baseados em arquivo {#destination-delivery-file-based}

O exemplo abaixo mostra como as configurações de entrega de destino devem ser definidas para um destino baseado em arquivo. Observe que a seção `deliveryMatchers` é necessária para destinos baseados em arquivos.

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "deliveryMatchers":[
            {
               "type":"SOURCE",
               "value":[
                  "batch"
               ]
            }
         ],
         "authenticationRule":"CUSTOMER_AUTHENTICATION",
         "destinationServerId":"{{destinationServerId}}"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Configuração de autenticação de plataforma {#platform-authentication}

Ao usar `PLATFORM_AUTHENTICATION`, você deve especificar o parâmetro `authenticationId` para vincular sua configuração de destino à configuração de credenciais.

1. Definir `destinationDelivery.authenticationRule` como `"PLATFORM_AUTHENTICATION"` na configuração de destino
2. [Criar o objeto de credencial](/help/destinations/destination-sdk/credentials-api/create-credential-configuration.md).
3. Defina o parâmetro `authenticationId` para o valor `instanceId` do objeto de credencial.

**Exemplo de configuração com PLATFORM_AUTHENTICATION:**

>[!BEGINSHADEBOX]

```json
{
   "destinationDelivery":[
      {
         "authenticationRule":"PLATFORM_AUTHENTICATION",
         "authenticationId":"<string-here>",
         "destinationServerId":"<string-here>"
      }
   ]
}
```

>[!ENDSHADEBOX]

## Próximas etapas {#next-steps}

Depois de ler este artigo, você deverá entender melhor como configurar os locais onde seu destino deve exportar dados, para destinos com base em arquivo e transmissão.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação do cliente](customer-authentication.md)
* [Autorização OAuth2](oauth2-authorization.md)
* [Atributos da interface](ui-attributes.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento compatíveis](supported-mapping-configurations.md)
* [Configuração de metadados de público](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações do perfil histórico](historical-profile-qualifications.md)
