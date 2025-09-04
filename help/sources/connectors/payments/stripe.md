---
title: Stripe
description: Saiba como assimilar dados de pagamentos de sua conta do Stripe para o Adobe Experience Platform
exl-id: 191d217e-036d-491a-b7dd-abcad74625ba
source-git-commit: 40c3745920204983f5388de6cba1402d87eda71c
workflow-type: tm+mt
source-wordcount: '791'
ht-degree: 1%

---

# [!DNL Stripe]

Milhares de empresas de todos os portes utilizam o [!DNL Stripe], seja online ou pessoalmente, para aceitar pagamentos, gerar novas fontes de receita e expandir-se globalmente com a ajuda da Adobe Experience Platform, Adobe Commerce e [!DNL Magento Open Source].

Use a fonte [!DNL Stripe] no Experience Platform para assimilar dados capturados pelos clientes durante o fluxo de compra. Depois de assimilados, use esses dados para criar ofertas personalizadas e desbloquear insights de negócios mais avançados.

>[!TIP]
>
>Para perguntas sobre a origem [!DNL Stripe] no Experience Platform, contate [!DNL Stripe] em adobe-partner<span>@stripe.com.

>[!BEGINSHADEBOX]

**Exemplo de caso de uso para a [!DNL Stripe] origem**

Sua empresa permite que os clientes comprem itens em sua loja online com a opção de **comprar agora** e **pagar depois** (usando o [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm] ou [!DNL Zip]).

Use a fonte de dados [!DNL Stripe] para analisar o uso das opções **comprar agora** e **pagar mais tarde** e experimentar ofertas personalizadas para esses clientes. Por exemplo, considere recomendar itens complementares para expandir o número de itens em seu carrinho de compras antes do check-out.

>[!ENDSHADEBOX]

Leia o documento abaixo para obter informações sobre como configurar sua conta de origem do [!DNL Stripe], recuperar as credenciais necessárias e criar seus esquemas.

## Pré-requisitos {#prerequisites}

As seções a seguir fornecem informações sobre a configuração de pré-requisitos que você deve concluir antes de conectar sua conta do [!DNL Stripe] ao Experience Platform.

### Recupere o token de acesso

* Faça logon no [[!DNL Stripe] painel](https://dashboard.stripe.com/login) usando seu email e senha do [!DNL Stripe].
* No painel [!DNL Developers], selecione **[!DNL API keys for developers]**.
* Na guia **Chaves de API**, selecione **[!DNL Reveal test key]** para revelar seu token de acesso.
* Agora você pode usar este token como seu token de acesso ao conectar sua conta do [!DNL Stripe] à Experience Platform, usando a API do [!DNL Flow Service] ou a interface do usuário do Experience Platform.

### Coletar credenciais necessárias

Para conectar sua conta do [!DNL Stripe] à Experience Platform, você deve fornecer valores para as seguintes credenciais de autenticação:

>[!BEGINTABS]

>[!TAB API]

Você deve fornecer as credenciais a seguir ao conectar sua conta do [!DNL Stripe] usando a API do [!DNL Flow Service].

| Credencial | Descrição |
| --- | --- |
| `accessToken` | Seu token de autenticação de código de atualização OAuth 2 do [!DNL Stripe]. |
| `connectionSpec.id` | A ID de especificação da conexão da origem [!DNL Stripe]. Esta ID foi corrigida como: `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB IU]

Você deve fornecer as credenciais a seguir ao conectar sua conta do [!DNL Stripe] usando a interface do usuário do Experience Platform.

| Credencial | Descrição |
| --- | --- |
| Token de acesso | Seu token de autenticação de código de atualização OAuth 2 do [!DNL Stripe]. |

>[!ENDTABS]

Para obter mais informações sobre como usar as APIs do [!DNL Stripe], leia a [[!DNL Stripe] documentação sobre chaves de API](https://docs.stripe.com/keys).

### Criar um esquema do Experience Data Model (XDM)

A origem [!DNL Stripe] oferece suporte à assimilação de dados dos seguintes caminhos de recursos:

* Encargos
* Assinaturas
* Reembolsos
* Transações de Saldo
* Clientes
* Preços

Você deve criar um esquema XDM para descrever um conjunto de dados, que pode armazenar os campos e tipos de dados que serão enviados de [!DNL Stripe] para o Experience Platform.

>[!BEGINTABS]

>[!TAB Encargos]

Em [!DNL Stripe], **encargos** representam tentativas de mover dinheiro para seu [!DNL Stripe]. Leia o [[!DNL Stripe] guia de API sobre encargos](https://docs.stripe.com/api/charges) para obter mais informações sobre atributos de encargos específicos.

+++Selecione para exibir o objeto Stripe Charge  

```json
{
  "id": "ch_3MmlLrLkdIwHu7ix0snN0B15",
  "object": "charge",
  "amount": 1099,
  "amount_captured": 1099,
  "amount_refunded": 0,
  "application": null,
  "application_fee": null,
  "application_fee_amount": null,
  "balance_transaction": "txn_3MmlLrLkdIwHu7ix0uke3Ezy",
  "billing_details": {
    "address": {
      "city": null,
      "country": null,
      "line1": null,
      "line2": null,
      "postal_code": null,
      "state": null
    },
    "email": null,
    "name": null,
    "phone": null
  },
  "calculated_statement_descriptor": "Stripe",
  "captured": true,
  "created": 1679090539,
  "currency": "usd",
  "customer": null,
  "description": null,
  "disputed": false,
  "failure_balance_transaction": null,
  "failure_code": null,
  "failure_message": null,
  "fraud_details": {},
  "invoice": null,
  "livemode": false,
  "metadata": {},
  "on_behalf_of": null,
  "outcome": {
    "network_status": "approved_by_network",
    "reason": null,
    "risk_level": "normal",
    "risk_score": 32,
    "seller_message": "Payment complete.",
    "type": "authorized"
  },
  "paid": true,
  "payment_intent": null,
  "payment_method": "card_1MmlLrLkdIwHu7ixIJwEWSNR",
  "payment_method_details": {
    "card": {
      "brand": "visa",
      "checks": {
        "address_line1_check": null,
        "address_postal_code_check": null,
        "cvc_check": null
      },
      "country": "US",
      "exp_month": 3,
      "exp_year": 2024,
      "fingerprint": "mToisGZ01V71BCos",
      "funding": "credit",
      "installments": null,
      "last4": "4242",
      "mandate": null,
      "network": "visa",
      "three_d_secure": null,
      "wallet": null
    },
    "type": "card"
  },
  "receipt_email": null,
  "receipt_number": null,
  "receipt_url": "https://pay.stripe.com/receipts/payment/CAcaFwoVYWNjdF8xTTJKVGtMa2RJd0h1N2l4KOvG06AGMgZfBXyr1aw6LBa9vaaSRWU96d8qBwz9z2J_CObiV_H2-e8RezSK_sw0KISesp4czsOUlVKY",
  "refunded": false,
  "review": null,
  "shipping": null,
  "source_transfer": null,
  "statement_descriptor": null,
  "statement_descriptor_suffix": null,
  "status": "succeeded",
  "transfer_data": null,
  "transfer_group": null
}
```

+++

>[!TAB Subscrições]

No [!DNL Stripe], você pode usar **assinaturas** para cobrar de um cliente de forma recorrente. Leia o [[!DNL Stripe] guia de API sobre assinaturas](https://docs.stripe.com/api/subscriptions) para obter mais informações sobre atributos de assinatura específicos.

+++Selecione para exibir o objeto de Assinatura do Stripe

```json
{
  "id": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
  "object": "subscription",
  "application": null,
  "application_fee_percent": null,
  "automatic_tax": {
    "enabled": false,
    "liability": null
  },
  "billing_cycle_anchor": 1679609767,
  "billing_thresholds": null,
  "cancel_at": null,
  "cancel_at_period_end": false,
  "canceled_at": null,
  "cancellation_details": {
    "comment": null,
    "feedback": null,
    "reason": null
  },
  "collection_method": "charge_automatically",
  "created": 1679609767,
  "currency": "usd",
  "current_period_end": 1682288167,
  "current_period_start": 1679609767,
  "customer": "cus_Na6dX7aXxi11N4",
  "days_until_due": null,
  "default_payment_method": null,
  "default_source": null,
  "default_tax_rates": [],
  "description": null,
  "discount": null,
  "ended_at": null,
  "invoice_settings": {
    "issuer": {
      "type": "self"
    }
  },
  "items": {
    "object": "list",
    "data": [
      {
        "id": "si_Na6dzxczY5fwHx",
        "object": "subscription_item",
        "billing_thresholds": null,
        "created": 1679609768,
        "metadata": {},
        "plan": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "plan",
          "active": true,
          "aggregate_usage": null,
          "amount": 1000,
          "amount_decimal": "1000",
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "interval": "month",
          "interval_count": 1,
          "livemode": false,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "tiers_mode": null,
          "transform_usage": null,
          "trial_period_days": null,
          "usage_type": "licensed"
        },
        "price": {
          "id": "price_1MowQULkdIwHu7ixraBm864M",
          "object": "price",
          "active": true,
          "billing_scheme": "per_unit",
          "created": 1679609766,
          "currency": "usd",
          "custom_unit_amount": null,
          "livemode": false,
          "lookup_key": null,
          "metadata": {},
          "nickname": null,
          "product": "prod_Na6dGcTsmU0I4R",
          "recurring": {
            "aggregate_usage": null,
            "interval": "month",
            "interval_count": 1,
            "trial_period_days": null,
            "usage_type": "licensed"
          },
          "tax_behavior": "unspecified",
          "tiers_mode": null,
          "transform_quantity": null,
          "type": "recurring",
          "unit_amount": 1000,
          "unit_amount_decimal": "1000"
        },
        "quantity": 1,
        "subscription": "sub_1MowQVLkdIwHu7ixeRlqHVzs",
        "tax_rates": []
      }
    ],
    "has_more": false,
    "total_count": 1,
    "url": "/v1/subscription_items?subscription=sub_1MowQVLkdIwHu7ixeRlqHVzs"
  },
  "latest_invoice": "in_1MowQWLkdIwHu7ixuzkSPfKd",
  "livemode": false,
  "metadata": {},
  "next_pending_invoice_item_invoice": null,
  "on_behalf_of": null,
  "pause_collection": null,
  "payment_settings": {
    "payment_method_options": null,
    "payment_method_types": null,
    "save_default_payment_method": "off"
  },
  "pending_invoice_item_interval": null,
  "pending_setup_intent": null,
  "pending_update": null,
  "quantity": 1,
  "schedule": null,
  "start_date": 1679609767,
  "status": "active",
  "test_clock": null,
  "transfer_data": null,
  "trial_end": null,
  "trial_settings": {
    "end_behavior": {
      "missing_payment_method": "create_invoice"
    }
  },
  "trial_start": null
}
```

+++

>[!TAB Reembolsos]

Em [!DNL Stripe], você pode usar **reembolsos** para reembolsar um encargo criado anteriormente. Leia o [[!DNL Stripe] Guia de API sobre reembolsos](https://docs.stripe.com/api/refunds) para obter mais informações sobre atributos de reembolso específicos.

+++Selecione para exibir o objeto Reembolso do Stripe

```json
{
  "id": "re_1Nispe2eZvKYlo2Cd31jOCgZ",
  "object": "refund",
  "amount": 1000,
  "balance_transaction": "txn_1Nispe2eZvKYlo2CYezqFhEx",
  "charge": "ch_1NirD82eZvKYlo2CIvbtLWuY",
  "created": 1692942318,
  "currency": "usd",
  "destination_details": {
    "card": {
      "reference": "123456789012",
      "reference_status": "available",
      "reference_type": "acquirer_reference_number",
      "type": "refund"
    },
    "type": "card"
  },
  "metadata": {},
  "payment_intent": "pi_1GszsK2eZvKYlo2CfhZyoZLp",
  "reason": null,
  "receipt_number": null,
  "source_transfer_reversal": null,
  "status": "succeeded",
  "transfer_reversal": null
}
```

+++

>[!TAB Transações de saldo]

Em [!DNL Stripe], **transações de saldo** representam o movimento de fundos entre suas contas do [!DNL Stripe]. Leia o [[!DNL Stripe] guia de API sobre transações de saldo](https://docs.stripe.com/api/balance_transactions) para obter mais informações sobre atributos de transação de saldo específicos.

+++Selecione para exibir o objeto Transação de Saldo do Stripe

```json
{
  "id": "txn_1MiN3gLkdIwHu7ixxapQrznl",
  "object": "balance_transaction",
  "amount": -400,
  "available_on": 1678043844,
  "created": 1678043844,
  "currency": "usd",
  "description": null,
  "exchange_rate": null,
  "fee": 0,
  "fee_details": [],
  "net": -400,
  "reporting_category": "transfer",
  "source": "tr_1MiN3gLkdIwHu7ixNCZvFdgA",
  "status": "available",
  "type": "transfer"
}
```

+++

>[!TAB Clientes]

No [!DNL Stripe], os **clientes** representam um determinado cliente da sua empresa. Para obter informações sobre atributos específicos do cliente, leia o [[!DNL Stripe] guia de API sobre clientes](https://docs.stripe.com/api/customers) para obter mais informações sobre atributos específicos do cliente.

+++Selecione para exibir o objeto Cliente do Stripe

```json
{
  "id": "cus_NffrFeUfNV2Hib",
  "object": "customer",
  "address": null,
  "balance": 0,
  "created": 1680893993,
  "currency": null,
  "default_source": null,
  "delinquent": false,
  "description": null,
  "discount": null,
  "email": "jennyrosen@example.com",
  "invoice_prefix": "0759376C",
  "invoice_settings": {
    "custom_fields": null,
    "default_payment_method": null,
    "footer": null,
    "rendering_options": null
  },
  "livemode": false,
  "metadata": {},
  "name": "Jenny Rosen",
  "next_invoice_sequence": 1,
  "phone": null,
  "preferred_locales": [],
  "shipping": null,
  "tax_exempt": "none",
  "test_clock": null
}
```

+++

>[!TAB Preços]

Em [!DNL Stripe], os **preços** representam o custo unitário, a moeda e o ciclo de cobrança opcional para compra recorrente e única de produtos. Leia o [[!DNL Stripe] guia de API sobre preços](https://docs.stripe.com/api/prices) para obter mais informações sobre atributos de preço específicos.

+++Selecione para exibir o objeto de preço do Stripe

```json
{
  "id": "price_1MoBy5LkdIwHu7ixZhnattbh",
  "object": "price",
  "active": true,
  "billing_scheme": "per_unit",
  "created": 1679431181,
  "currency": "usd",
  "custom_unit_amount": null,
  "livemode": false,
  "lookup_key": null,
  "metadata": {},
  "nickname": null,
  "product": "prod_NZKdYqrwEYx6iK",
  "recurring": {
    "aggregate_usage": null,
    "interval": "month",
    "interval_count": 1,
    "trial_period_days": null,
    "usage_type": "licensed"
  },
  "tax_behavior": "unspecified",
  "tiers_mode": null,
  "transform_quantity": null,
  "type": "recurring",
  "unit_amount": 1000,
  "unit_amount_decimal": "1000"
}
```

+++

>[!ENDTABS]


### LISTA DE PERMISSÕES de endereço IP

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a página [lista de permissões de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

### Configurar permissões no Experience Platform

Você deve ter as permissões **[!UICONTROL Exibir Fontes]** e **[!UICONTROL Gerenciar Fontes]** habilitadas para sua conta a fim de conectar sua conta do [!DNL Stripe] à Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia o [guia da interface do usuário de controle de acesso](../../../access-control/ui/overview.md).

## Próximas etapas

Após concluir a configuração de pré-requisito, você pode continuar a conectar e assimilar os dados do [!DNL Stripe] na Experience Platform. Leia os guias a seguir para saber como assimilar dados de pagamentos do [!DNL Stripe] para a Experience Platform usando APIs ou a interface do usuário:

* [Assimilar dados de pagamentos de sua conta do Stripe para a Experience Platform usando a API de Serviço de Fluxo](../../tutorials/api/create/payments/stripe.md).
* [Assimilar dados de pagamentos de sua conta do Stripe para a Experience Platform usando a interface de usuário](../../tutorials/ui/create/payments/stripe.md).
