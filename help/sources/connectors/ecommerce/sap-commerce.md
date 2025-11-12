---
title: Visão geral do SAP Commerce Source
description: Saiba como conectar o SAP Commerce ao Adobe Experience Platform usando APIs ou a interface do usuário.
last-substantial-update: 2023-07-26T00:00:00Z
badge: Beta
exl-id: d2ddfec3-a421-48a7-b765-86ce9162f26f
source-git-commit: 06b2108715ce368ff4ecf5c6c7dd3a327d9f61b1
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 3%

---

# [!DNL SAP Commerce]

>[!NOTE]
>
>A origem [!DNL SAP Commerce] está na versão beta. Consulte a [visão geral das fontes](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes com rótulo beta.

[[!DNL SAP Commerce]](https://www.sap.com/india/products/acquired-brands/what-is-hybris.html), uma solução de plataforma de comércio eletrônico baseada em nuvem para empresas B2B e B2C está disponível como parte do portfólio SAP Customer Experience. O [[!DNL SAP] Cobrança de assinatura](https://www.sap.com/products/financial-management/subscription-billing.html) é um produto do portfólio e permite o gerenciamento completo do ciclo de vida da assinatura com vendas simplificadas e experiências de pagamento por meio de integrações padronizadas.

A fonte [!DNL SAP Commerce] permite assimilar informações de clientes e contatos na Experience Platform dos pontos de extremidade de API dos Parceiros Comerciais [[!DNL SAP] Faturamento de Assinatura](https://www.sap.com/products/financial-management/subscription-billing.html) abaixo:

* [Clientes](https://api.sap.com/api/BusinessPartner_APIs/path/GET_customers)
* [Contatos](https://api.sap.com/api/BusinessPartner_APIs/path/GET_contacts)

Além disso, se [!DNL SAP Commerce] for executado para recuperar dados do cliente, a API de [Relações Cliente-Contato](https://api.sap.com/api/BusinessPartner_APIs/path/GET_relationships-customer-contacts) também será chamada para recuperar as informações de contato do cliente.

## INCLUO NA LISTA DE PERMISSÕES de endereços IP {#ip-allow-list}

Você deve adicionar endereços IP específicos da região ao incluo na lista de permissões antes de conectar suas fontes à Experience Platform. Para obter mais informações, leia o guia sobre [como ler os endereços IP de incluir na lista de permissões para se conectar ao Experience Platform](../../ip-address-allow-list.md) para obter mais informações.

## Pré-requisitos {#prerequisites}

Antes de trazer os dados do [!DNL SAP Commerce] para a Experience Platform, primeiro verifique se você tem o seguinte:

* Uma conta [!DNL SAP Subscription Billing]. Se você ainda não tiver uma conta de cobrança válida, contate o gerente de conta do [!DNL SAP]. Consulte o documento [[!DNL SAP] Configuração da plataforma](https://help.sap.com/doc/5fd179965d5145fbbe7f2a7aa1272338/latest/en-US/PlatformConfiguration.pdf) para obter detalhes adicionais.

* [!DNL SAP] chave de serviço. A chave de serviço [!DNL SAP] permite acessar a API [!DNL SAP Subscription Billing] por meio do Experience Platform. O [!DNL SAP Commerce] exige o seguinte:
   * ID de cliente
   * Segredo do cliente
   * URL. O padrão de URL é: `https://subscriptionbilling.authentication.eu10.hana.ondemand.com`. Este valor será usado posteriormente para obter valores para `region` e `tokenEndpoint` quando você [Criar conexão base](../../tutorials/api/create/ecommerce/sap-commerce.md#base-connection) usando a API ou quando [Conectar sua [!DNL SAP Commerce] conta](../../tutorials/ui/create/ecommerce/sap-commerce.md#connect-account) por meio da interface do usuário do Experience Platform.

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

A documentação abaixo fornece informações sobre como conectar o [!DNL SAP Commerce] ao Experience Platform usando APIs ou a interface do usuário:

* [Crie uma conexão de origem e um fluxo de dados para trazer [!DNL SAP Commerce] dados para a Experience Platform usando APIs](../../tutorials/api/create/ecommerce/sap-commerce.md).
* [Conecte sua conta [!DNL SAP Commerce] à Experience Platform usando a interface](../../tutorials/ui/create/ecommerce/sap-commerce.md).
* [Criar um fluxo de dados para uma fonte usando a interface](../../tutorials/ui/dataflow/ecommerce.md)
