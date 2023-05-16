---
description: Saiba como definir as configurações de entrega de destino para destinos criados com o Destination SDK, para indicar para onde os dados exportados vão e qual regra de autenticação é usada no local onde os dados serão enviados.
title: Delivery de destino
source-git-commit: 118ff85a9fceb8ee81dbafe2c381d365b813da29
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---


# Delivery de destino

Para oferecer mais controle sobre onde os dados exportados para o seu destino chegam, o Destination SDK permite especificar configurações de entrega de destino.

A seção de entrega de destino indica para onde os dados exportados vão e qual regra de autenticação é usada no local onde os dados serão entregues.

<!-- When configuring a destination, you must specify an authentication rule and one or more `destinationServerId` parameters, corresponding to the destination servers that define where the data will be delivered to. In most cases, the authentication rule that you should use is `CUSTOMER_AUTHENTICATION`.  -->

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama no [opções de configuração](../configuration-options.md) ou veja as seguintes páginas de visão geral da configuração de destino:

* [Use o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Use o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Você pode definir configurações de entrega de destino por meio do `/authoring/destinations` endpoint . Consulte as páginas de referência da API a seguir para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todas as opções de entrega de destino compatíveis que podem ser usadas para o seu destino.

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

Ao definir as configurações de delivery de destino, você pode usar os parâmetros descritos na tabela abaixo para definir para onde os dados exportados devem ser enviados.

| Parâmetro | Tipo | Descrição |
|---------|----------|------|
| `authenticationRule` | String | Indica como [!DNL Platform] O deve se conectar ao seu destino. Valores compatíveis:<ul><li>`CUSTOMER_AUTHENTICATION`: Use essa opção se os clientes da Platform fizerem logon em seu sistema por meio de qualquer um dos métodos de autenticação descritos [here](customer-authentication.md).</li><li>`PLATFORM_AUTHENTICATION`: Use essa opção se houver um sistema de autenticação global entre o Adobe e seu destino e o [!DNL Platform] o cliente não precisa fornecer credenciais de autenticação para se conectar ao seu destino. Nesse caso, você deve criar um objeto de credenciais usando o [API de credenciais](../../credentials-api/create-credential-configuration.md) configuração. </li><li>`NONE`: Use essa opção se nenhuma autenticação for necessária para enviar dados para a plataforma de destino. </li></ul> |
| `destinationServerId` | String | O `instanceId` do [servidor de destino](../../authoring-api/destination-server/create-destination-server.md) para o qual você deseja exportar dados. |
| `deliveryMatchers.type` | String | <ul><li>Ao configurar o delivery de destino para destinos com base em arquivo, sempre defina como `SOURCE`.</li><li>Ao configurar o delivery de destino para um destino de transmissão, a variável `deliveryMatchers` não é necessária.</li></ul> |
| `deliveryMatchers.value` | String | <ul><li>Ao configurar o delivery de destino para destinos com base em arquivo, sempre defina como `batch`.</li><li>Ao configurar o delivery de destino para um destino de transmissão, a variável `deliveryMatchers` não é necessária.</li></ul> |

{style="table-layout:auto"}

## Configurações de entrega de destino para destinos de transmissão {#destination-delivery-streaming}

O exemplo abaixo mostra como as configurações de entrega de destino devem ser definidas para um destino de transmissão. Observe que a variável `deliveryMatchers` não é necessária para destinos de transmissão.

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

## Configurações de delivery de destino para destinos com base em arquivo {#destination-delivery-file-based}

O exemplo abaixo mostra como as configurações de entrega de destino devem ser configuradas para um destino baseado em arquivo. Observe que a variável `deliveryMatchers` é necessária para destinos com base em arquivo.

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

## Próximas etapas {#next-steps}

Após a leitura deste artigo, você deve ter uma melhor compreensão de como pode configurar os locais onde seu destino deve exportar dados, tanto para streaming quanto para destinos com base em arquivo.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação do cliente](customer-authentication.md)
* [Autenticação OAuth2](oauth2-authentication.md)
* [Atributos da interface do usuário](ui-attributes.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Configurações de mapeamento suportadas](supported-mapping-configurations.md)
* [Configuração de metadados de público-alvo](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações de perfil histórico](historical-profile-qualifications.md)