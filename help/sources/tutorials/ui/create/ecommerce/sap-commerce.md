---
title: Criar uma conexão de origem do SAP Commerce na interface
description: Saiba como criar uma conexão de origem do SAP Commerce usando a interface do usuário do Adobe Experience Platform.
exl-id: 6484e51c-77cd-4dbd-9c68-0a4e3372da33
source-git-commit: e402a58f51de49b26f9d279cebf551ec11e4698f
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL SAP Commerce] na interface

O tutorial a seguir orienta você pelas etapas para criar uma conexão de origem do [!DNL SAP Commerce] para trazer contatos de [[!DNL SAP] Faturamento da assinatura](https://www.sap.com/products/financial-management/subscription-billing.html) e dados do cliente usando a interface do usuário do Adobe Experience Platform.

## Introdução {#getting-started}

Este tutorial requer uma compreensão funcional dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conta válida do [!DNL SAP Commerce], ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/ecommerce.md).

### Coletar credenciais necessárias {#gather-credentials}

Para conectar [!DNL SAP Commerce] ao Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| ID de cliente | O valor de `clientId` da chave de serviço. |
| Segredo do cliente | O valor de `clientSecret` da chave de serviço. |
| Endpoint do token | O valor de `url` da chave de serviço será semelhante a `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. |
| Região | O local do data center. A região está presente no `url` e tem um valor semelhante a `eu10` ou `us10`. Por exemplo, se o `url` for `https://eu10.revenue.cloud.sap/api`, você precisará de `eu10`. |

Para obter mais informações, consulte a [[!DNL SAP Commerce] documentação](https://help.sap.com/docs/CLOUD_TO_CASH_OD/987aec876092428f88162e438acf80d6/c5fcaf96daff4c7a8520188e4d8a1843.html).

### Criar um esquema do Experience Platform {#create-platform-schema}

Antes de criar uma conexão de origem [!DNL SAP Commerce], você também deve garantir que primeiro crie um esquema do Experience Platform para usar na sua origem. Consulte o tutorial sobre [criação de um esquema do Experience Platform](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um esquema.

Expanda a seção a seguir para exibir um schema de exemplo.

+++ Exibir exemplo de esquema

```
{
  "_extconndev": {
    "addresses": [
      {
        "addressUUID": "{ADDRESS_UUID}",
        "city": "Burnaby",
        "country": "Canada",
        "email": "chandni@acme.com",
        "houseNumber": "27",
        "isDefault": false,
        "phone": "123-456-7890",
        "postalCode": "V3J 1X9",
        "state": "British Columbia",
        "street": "Beresford"
      }
    ],
    "changedAt": "1687204041",
    "changedBy": "vero@acme.com",
    "contactNumber": "123-456-7980",
    "corporateInfo": {
      "company": "acme"
    },
    "createAt": "1687204041",
    "createdBy": "vero@acme.com",
    "customReferences": [
      {
        "id": "Sample value",
        "typeCode": "Sample value"
      }
    ],
    "customerNumber": "Sample value",
    "customerType": "Sample value",
    "defaultAddress": {
      "addressUUID": "Sample value",
      "city": "North Vancouver",
      "country": "Canada",
      "email": "chandni@acme.come",
      "houseNumber": "34",
      "isDefault": false,
      "phone": "123-456-7890",
      "postalCode": "V7H 2P1",
      "state": "British Columbia",
      "street": "Maple"
    },
    "externalObjectReferences": [
      {
        "externalId": "{EXTERNAL_ID}",
        "externalIdTypeCode": "{EXTERNAL_ID_TYPE_CODE}",
        "externalSystemId": "{EXTERNAL_SYSTEM_ID}"
      }
    ],
    "markets": [
      {
        "active": false,
        "country": "USA",
        "currency": "USD",
        "marketId": "Sample value",
        "priceinfo": {
          "incoterms": "{INCO_TERMS}",
          "incotermsLocation": "{INCO_TERMS_LOCATION}",
          "priceGroup": "{PRICE_GROUP}",
          "priceListType": "{PRICE_LIST_TYPE}"
        },
        "salesArea": {
          "distributionChannel": "{DISTRIBUTION_CHANNEL}",
          "division": "{DIVISION}",
          "salesOrganization": "{SALES_ORGANIZATION}"
        }
      }
    ],
    "personalInfo": {
      "firstName": "Chandni",
      "lastName": "Kaur"
    }
  },
  "_id": "/uri-reference",
  "_repo": {
    "createDate": "2004-10-23T12:00:00-06:00",
    "modifyDate": "2004-10-23T12:00:00-06:00"
  },
  "createdByBatchID": "/uri-reference",
  "modifiedByBatchID": "/uri-reference",
  "personID": "{PERSON_ID}",
  "repositoryCreatedBy": "kevin@acme.com",
  "repositoryLastModifiedBy": "kevin@acme.com"
}
```

+++

## Conectar sua conta do [!DNL SAP Commerce] {#connect-account}

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *comércio eletrônico*, selecione **[!UICONTROL SAP Commerce]** e **[!UICONTROL Adicionar dados]**.

![Captura de tela da interface do Experience Platform para catálogo com o cartão SAP Commerce](../../../../images/tutorials/create/ecommerce/sap-commerce/catalog-card.png)

A página **[!UICONTROL Conectar conta SAP Commerce]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente {#existing-account}

Para usar uma conta existente, selecione a conta [!DNL SAP Commerce] com a qual deseja criar um novo fluxo de dados e clique em **[!UICONTROL Avançar]** para continuar.

![Captura de tela da interface do Experience Platform para conectar a conta SAP Commerce a uma conta existente](../../../../images/tutorials/create/ecommerce/sap-commerce/existing.png)

### Nova conta {#new-account}

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![Captura de tela da interface do Experience Platform para conectar a conta SAP Commerce a uma nova conta](../../../../images/tutorials/create/ecommerce/sap-commerce/new.png)

### Selecionar dados {#select-data}

Finalmente, você deve selecionar o tipo de objeto que deseja assimilar na Experience Platform.

| Tipo de objeto | Descrição |
| --- | --- |
| `Customers` | As entidades que têm assinaturas. |
| `Contacts` | Os detalhes de contato dos clientes. |

>[!BEGINTABS]

>[!TAB Clientes]

Para assimilar dados do cliente, selecione **[!UICONTROL Clientes]** como seu tipo de objeto e selecione **[!UICONTROL Próximo]**.

![Captura de tela da interface do Experience Platform para SAP Commerce mostrando a configuração com a opção Clientes selecionada](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-customers.png)

>[!TAB Contatos]

Para assimilar dados de contato, selecione **[!UICONTROL Contatos]** como seu tipo de objeto e selecione **[!UICONTROL Avançar]**.

![Captura de tela da interface do Experience Platform para SAP Commerce mostrando a configuração com a opção Contatos selecionada](../../../../images/tutorials/create/ecommerce/sap-commerce/configuration-contacts.png)

>[!ENDTABS]

## Próximas etapas {#next-steps}

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL SAP Commerce]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Experience Platform](../../dataflow/ecommerce.md).

## Recursos adicionais {#additional-resources}

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar a origem [!DNL SAP Commerce].

### Mapeamento {#mapping}

O Experience Platform fornece recomendações inteligentes para campos mapeados automaticamente com base no esquema ou conjunto de dados de destino selecionado. Você pode ajustar manualmente as regras de mapeamento para atender aos seus casos de uso. Com base nas suas necessidades, você pode optar por mapear campos diretamente ou usar funções de preparação de dados para transformar dados de origem para derivar valores calculados ou calculados. Para obter etapas abrangentes sobre como usar a interface do mapeador e campos calculados, consulte o [Guia da Interface do Preparo de Dados](../../../../../data-prep/ui/mapping.md).

As configurações de mapeamento para o fluxo de dados serão diferentes dependendo do esquema e do tipo de objeto que você seleciona para assimilar.

>[!BEGINTABS]

>[!TAB Clientes]

Para dados de clientes, o [!DNL SAP Commerce] usa os pontos de extremidade [clientes](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers) e [relações cliente-contatos](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) da API [!DNL SAP Business Partners] para recuperar os dados

Este é um exemplo de configurações de mapeamento para o fluxo de dados [!DNL SAP Commerce] para dados do cliente:

| Campo de público alvo | Descrição |
| --- | --- |
| `customerNumber` | O número do cliente. |
| `corporateInfo` | O número do cliente. |
| `customerType` | O tipo de cliente. |
| `createdAt` | Um carimbo de data e hora indicando quando o cliente foi criado. |
| `changedAt` | Um carimbo de data e hora indicando quando o cliente foi atualizado pela última vez. |
| `markets[*].country` | Os clientes comercializam, recuperados como um objeto de matriz. |
| `addresses[*].email` | Emails associados aos vários endereços do cliente, recuperados como um objeto de matriz. |
| `addresses[*].city` | Cidades associadas aos vários endereços do cliente, recuperadas como um objeto de matriz. |
| `addresses[*].addressUUID` | IDs associadas aos vários endereços do cliente, recuperadas como um objeto de matriz. |
| `externalObjectReferences[*].externalSystemId` | Dados adicionais, recuperados como um objeto de matriz. |
| `externalObjectReferences[*].externalId` | Dados adicionais, recuperados como um objeto de matriz. |
| `customReferences[*].id` | Dados adicionais, recuperados como um objeto de matriz. |
| `customReferences[*].typeCode` | Dados adicionais, recuperados como um objeto de matriz. |

![A etapa de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-customers.png)

>[!TAB Contatos]

Para dados de contato, [!DNL SAP Commerce] usa o ponto de extremidade [contatos](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts) da API [!DNL SAP Business Partners] para recuperar os dados.

Este é um exemplo de configurações de mapeamento para o fluxo de dados [!DNL SAP Commerce] para dados de contato:

| Campo de público alvo | Descrição |
| --- | --- |
| `contactNumber` | O número do contato. |
| `createdAt` | Um carimbo de data e hora indicando quando o contato foi criado. |
| `changedAt` | Um carimbo de data e hora indicando quando o contato foi atualizado pela última vez. |
| `personalInfo.lastName` | O Sobrenome do contato. |
| `personalInfo.firstName` | O Nome do contato. |
| `externalObjectReferences[*].externalSystemId` | Dados adicionais, recuperados como um objeto de matriz. |
| `externalObjectReferences[*].externalId` | Dados adicionais, recuperados como um objeto de matriz. |
| `externalObjectReferences[*].externalIdTypeCode` | Dados adicionais, recuperados como um objeto de matriz. |

![A etapa de mapeamento do fluxo de trabalho de origens.](../../../../images/tutorials/create/ecommerce/sap-commerce/mapping-contacts.png)

>[!ENDTABS]
