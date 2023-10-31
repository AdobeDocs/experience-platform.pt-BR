---
title: Visão geral da origem do SAP Commerce
description: Saiba como conectar o SAP Commerce ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: b4334b4f73428f94f5a7e5088f98e2459afcaf3c
workflow-type: tm+mt
source-wordcount: '394'
ht-degree: 3%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>A variável [!DNL SAP Commerce] a fonte está na versão beta. Consulte a [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), uma solução de plataforma de comércio eletrônico baseada em nuvem para empresas B2B e B2C está disponível como parte do portfólio SAP Customer Experience. [[!DNL SAP] Cobrança da assinatura](https://www.sap.com/products/financial-management/subscription-billing.html) O é um produto do portfólio e permite o gerenciamento completo do ciclo de vida da assinatura com vendas simplificadas e experiências de pagamento por meio de integrações padronizadas.

A variável [!DNL SAP Commerce] fonte permite assimilar informações de clientes e contatos na Platform da [[!DNL SAP] Cobrança da assinatura](https://www.sap.com/products/financial-management/subscription-billing.html) Endpoints da API de parceiros de negócios abaixo:

* [Clientes](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contatos](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Além disso, se [!DNL SAP Commerce] for executado para recuperar dados do cliente, a variável [Relacionamentos entre Cliente e Contato](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) A API também é chamada para recuperar as informações de contato do cliente.

## LISTA DE PERMISSÕES de endereço IP {#ip-allow-list}

Pode ser necessário adicionar uma lista de endereços IP a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos {#prerequisites}

Antes que você possa trazer seu [!DNL SAP Commerce] dados para o Experience Platform, você deve primeiro garantir que tenha o seguinte:

* A [!DNL SAP Subscription Billing] conta. Se você ainda não tiver uma conta de cobrança válida, entre em contato com o [!DNL SAP] gerente de conta. Consulte a [[!DNL SAP] Configuração da plataforma](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) para obter detalhes adicionais.

* [!DNL SAP] chave de serviço. A variável [!DNL SAP] a chave de serviço permite acessar a variável [!DNL SAP Subscription Billing] API por meio do Experience Platform. O [!DNL SAP Commerce] exige o seguinte:
   * ID do cliente
   * Segredo do cliente
   * URL. O padrão de URL é o seguinte: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Esse valor será usado posteriormente para obter valores para `region` e `tokenEndpoint` quando você [Criar conexão básica](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) usando a API ou quando você [Conecte seu [!DNL SAP Commerce] account](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) por meio da interface do usuário da Platform.

+++Selecione para ver um exemplo da chave de serviço

```json
{ 
    "url": "https://eu10.revenue.cloud.sap/api",
    "uaa": {
        "clientid": "XXX",
        "clientsecret": "XXX",
        "url": "https://subscriptionbilling.authentication.eu10.hana.ondemand.com",
        "identityzone": "subscriptionbilling",
        "identityzoneid": "XXX",
        "tenantid": "XXX",
        "tenantmode": "dedicated",
        "sburl": "https://internal-xsuaa.authentication.eu10.hana.ondemand.com",
        "apiurl": "https://api.authentication.eu10.hana.ondemand.com",
        "verificationkey": "XXX",
        "xsappname": "XXX",
        "subaccountid": "XXX",
        "uaadomain": "authentication.eu10.hana.ondemand.com",
        "zoneid": "XXX",
        "credential-type": "binding-secret"
    },
    "vendor": "SAP"
}
```

+++

## Próximas etapas

A documentação abaixo fornece informações sobre como se conectar [!DNL SAP Commerce] para a Platform usando APIs ou a interface do usuário:

* [Crie uma conexão de origem e um fluxo de dados para trazer [!DNL SAP Commerce] dados para a Platform usando APIs](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Conecte seu [!DNL SAP Commerce] conta para Experience Platform usando a interface do usuário](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Criar um fluxo de dados para uma fonte usando a interface](../../tutorials/ui/dataflow/ecommerce.md)
