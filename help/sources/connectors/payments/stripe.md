---
title: Stripe
description: Saiba como assimilar dados de pagamentos de sua conta Stripe para o Adobe Experience Platform
badge: Beta
source-git-commit: f8df3ddb96ad0810a7a46b0a55125336c427aebd
workflow-type: tm+mt
source-wordcount: '809'
ht-degree: 1%

---

# [!DNL Stripe]

>[!NOTE]
>
>A variável [!DNL Stripe] a fonte está na versão beta. Leia as [visão geral das origens](../../home.md#terms-and-conditions) para obter mais informações sobre o uso de fontes rotuladas como beta.

Milhares de empresas de todos os tamanhos utilizam [!DNL Stripe] on-line e pessoalmente para aceitar pagamentos, gerar novas fontes de receita e expandir globalmente com a ajuda da Adobe Experience Platform, Adobe Commerce e [!DNL Magento Open Source].

Use o [!DNL Stripe] origem no Experience Platform para assimilar dados capturados durante o fluxo de compra pelos clientes. Depois de assimilados, use esses dados para criar ofertas personalizadas e desbloquear insights de negócios mais avançados.

>[!TIP]
>
>Para perguntas sobre o [!DNL Stripe] fonte no Experience Platform, contato [!DNL Stripe] na adobe-partner<span>@stripe.com.

>[!BEGINSHADEBOX]

**Exemplo de caso de uso para o [!DNL Stripe] origem**

Sua empresa permite que os clientes comprem itens em sua loja online com a opção de **comprar agora** e **pagar mais tarde** (usando [!DNL Klarna], [!DNL Afterpay], [!DNL Affirm]ou [!DNL Zip]).

Use o [!DNL Stripe] fonte de dados para analisar o uso de **comprar agora** e **pagar mais tarde** e experimente ofertas personalizadas para esses clientes. Por exemplo, considere recomendar itens complementares para expandir o número de itens em seu carrinho de compras antes do check-out.

>[!ENDSHADEBOX]

Leia o documento abaixo para obter informações sobre como configurar seus [!DNL Stripe] , recupere as credenciais necessárias e crie seus esquemas.

## Pré-requisitos {#prerequisites}

As seções a seguir fornecem informações sobre a configuração de pré-requisitos que você deve concluir antes de conectar [!DNL Stripe] conta para Experience Platform.

### Recupere o token de acesso

* Faça logon no [[!DNL Stripe] painel](https://dashboard.stripe.com/login) usar seu [!DNL Stripe] endereço de e-mail e senha.
* No [!DNL Developers] painel, selecione **[!DNL API keys for developers]**.
* No **Chaves de API** selecione **[!DNL Reveal test key]** para revelar seu token de acesso.
* Agora você pode usar esse token como token de acesso ao conectar [!DNL Stripe] conta para Experience Platform, usando a variável [!DNL Flow Service] API ou a interface do Experience Platform.

### Coletar credenciais necessárias

Para conectar seu [!DNL Stripe] conta para Experience Platform, você deve fornecer valores para as seguintes credenciais de autenticação:

>[!BEGINTABS]

>[!TAB API]

Você deve fornecer as seguintes credenciais ao se conectar ao [!DNL Stripe] conta usando o [!DNL Flow Service] API.

| Credencial | Descrição |
| --- | --- |
| `accessToken` | Seu [!DNL Stripe] Token de autenticação de código de atualização OAuth 2. |
| `connectionSpec.id` | A ID de especificação da conexão do [!DNL Stripe] origem. Essa ID é corrigida como: `cc2c31d6-7b8c-4581-b49f-5c8698aa3ab3`. |

>[!TAB Interface do usuário]

Você deve fornecer as seguintes credenciais ao se conectar ao [!DNL Stripe] usando a interface de usuário do Experience Platform.

| Credencial | Descrição |
| --- | --- |
| Token de acesso | Seu [!DNL Stripe] Token de autenticação de código de atualização OAuth 2. |

>[!ENDTABS]

Para obter mais informações sobre o uso de [!DNL Stripe] APIs, leia as [[!DNL Stripe] documentação sobre chaves de API](https://docs.stripe.com/keys).

### Criar um esquema do Experience Data Model (XDM)

A variável [!DNL Stripe] A origem oferece suporte à assimilação de dados dos seguintes caminhos de recursos:

* Encargos
* Assinaturas
* Reembolsos
* Transações de Saldo
* Clientes
* Preços

É necessário criar um esquema XDM para descrever um conjunto de dados, que possa armazenar os campos e tipos de dados que serão enviados do [!DNL Stripe] para Experience Platform.

>[!BEGINTABS]

>[!TAB Encargos]

Entrada [!DNL Stripe], **encargos** representar tentativas de mover dinheiro para o seu [!DNL Stripe]. Leia o [[!DNL Stripe] Guia de API sobre encargos](https://docs.stripe.com/api/charges) para obter mais informações sobre atributos de encargo específicos.

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

Entrada [!DNL Stripe], você pode usar **assinaturas** para cobrar de forma recorrente de um cliente. Leia o [[!DNL Stripe] Guia de API sobre assinaturas](https://docs.stripe.com/api/subscriptions) para obter mais informações sobre atributos de assinatura específicos.

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

Entrada [!DNL Stripe], você pode usar **reembolsos** para reembolsar um encargo criado anteriormente. Leia o [[!DNL Stripe] Guia de API sobre reembolsos](https://docs.stripe.com/api/refunds) para obter mais informações sobre atributos de restituição específicos.

+++Selecione para exibir o objeto Reembolso de Stripe

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

>[!TAB Transações de Saldo]

Entrada [!DNL Stripe], **transações de saldo** representam o movimento de fundos entre as [!DNL Stripe] contas. Leia o [[!DNL Stripe] Guia de API sobre transações de saldo](https://docs.stripe.com/api/balance_transactions) para obter mais informações sobre atributos de transação de saldo específicos.

+++Selecione para exibir o objeto Transação de Saldo de Stripe

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

Entrada [!DNL Stripe], **clientes** representa um determinado cliente da sua empresa. Para obter informações sobre atributos específicos do cliente, leia o [[!DNL Stripe] Guia de API sobre clientes](https://docs.stripe.com/api/customers) para obter mais informações sobre atributos específicos do cliente.

+++Selecione para exibir o objeto Stripe Customer

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

Entrada [!DNL Stripe], **preços** representa o custo unitário, a moeda e o ciclo de faturamento opcional para compra recorrente e única de produtos. Leia o [[!DNL Stripe] Guia de API sobre preços](https://docs.stripe.com/api/prices) para obter mais informações sobre atributos de preço específicos.

+++Selecione para exibir o objeto Preço do Stripe

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

Uma lista de endereços IP deve ser adicionada a uma lista de permissões antes de trabalhar com conectores de origem. Falha ao adicionar endereços IP específicos da região à lista de permissões pode levar a erros ou ao não desempenho ao usar origens. Consulte a [LISTA DE PERMISSÕES de endereço IP](../../ip-address-allow-list.md) para obter mais informações.

### Configurar permissões no Experience Platform

Você deve ter ambos **[!UICONTROL Exibir fontes]** e **[!UICONTROL Gerenciar fontes]** permissões habilitadas para sua conta para conectar seu [!DNL Stripe] conta para Experience Platform. Entre em contato com o administrador do produto para obter as permissões necessárias. Para obter mais informações, leia a [guia da interface do usuário de controle de acesso](../../../access-control/ui/overview.md).

## Próximas etapas

Após concluir a configuração de pré-requisito, você pode prosseguir para conectar e assimilar seus [!DNL Stripe] dados para Experience Platform. Leia os guias a seguir para saber como assimilar [!DNL Stripe] dados de pagamentos para o Experience Platform usando APIs ou a interface do usuário:

* [Assimilar dados de pagamentos de sua conta Stripe para o Experience Platform usando a API de Serviço de Fluxo](../../tutorials/api/create/payments/stripe.md).
* [Assimilar dados de pagamentos de sua conta Stripe para o Experience Platform usando a interface do usuário](../../tutorials/ui/create/payments/stripe.md).