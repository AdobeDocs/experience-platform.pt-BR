---
solution: Experience Platform
title: Campo de preferência de marketing genérico com tipo de dados de assinaturas
topic: overview
description: Este documento fornece uma visão geral do Campo de Preferência de Marketing Genérico com o tipo de dados XDM de Assinaturas.
translation-type: tm+mt
source-git-commit: 8c5ab298bad69305358ae961ebaf7836a90a0eaa
workflow-type: tm+mt
source-wordcount: '712'
ht-degree: 2%

---


# [!UICONTROL Generic Marketing Preference Field with Subscriptions] tipo de dados

[!UICONTROL Generic Marketing Preference Field with Subscriptions] é um tipo de dados XDM padrão que descreve a seleção de um cliente para uma preferência de marketing específica.

>[!NOTE]
>
>Esse tipo de dados deve ser usado para personalizar a estrutura dos esquemas de consentimento de sua organização usando a combinação [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]](../mixins/profile/consents.md) como linha de base.
>
>Se você não precisar de um mapa `subscriptions` para um campo de preferência de marketing específico, poderá usar o [tipo de dados básico do campo de marketing](./marketing-field.md) em vez disso.

![](../images/data-types/marketing-field-subscriptions.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `reason` | String | Quando um cliente recusa um caso de uso de marketing, esse campo de cadeia de caracteres representa o motivo pelo qual o cliente optou por não participar. |
| `subscriptions` | Mapa | Um mapa de preferências de marketing do cliente para assinaturas específicas. Consulte a seção em [subscriptions](#subscriptions) para obter mais informações. |
| `time` | DateTime | Um carimbo de data e hora ISO 8601 de quando a preferência de marketing foi alterada, se aplicável. |
| `val` | String | A escolha de preferência fornecida pelo cliente para este caso de uso de marketing. Consulte a [próxima seção](#val) para obter valores e definições aceitos. |

## `val` {#val}

A tabela a seguir descreve os valores aceitos para `val`:

| Valor | Title | Descrição |
| --- | --- | --- |
| `y` | Sim | O cliente optou pela preferência. Em outras palavras, eles **do** consentiram com o uso de seus dados, conforme indicado pela preferência em questão. |
| `n` | Não | O cliente recusou a preferência. Em outras palavras, eles **não** consentiram com o uso de seus dados, conforme indicado pela preferência em questão. |
| `p` | Verificação pendente | O sistema ainda não recebeu um valor de preferência final. Isso é usado com mais frequência como parte de um consentimento que requer verificação em duas etapas. Por exemplo, se um cliente optar por receber emails, esse consentimento será definido como `p` até que selecione um link em um email para verificar se forneceu o endereço de email correto, momento em que o consentimento seria atualizado para `y`.<br><br>Se essa preferência não usar um processo de verificação de dois conjuntos, a  `p` escolha poderá ser usada para indicar que o cliente ainda não respondeu ao prompt de consentimento. Por exemplo, você pode definir automaticamente o valor para `p` na primeira página de um site, antes que o cliente tenha respondido ao prompt de consentimento. Em jurisdições que não exigem consentimento explícito, você também pode usá-lo para indicar que o cliente não recusou explicitamente (em outras palavras, o consentimento é presumido). |
| `u` | Desconhecido | As informações de preferência do cliente são desconhecidas. |
| `LI` | Interesse legítimo | O interesse comercial legítimo em recolher e processar esses dados para a finalidade especificada supera o potencial dano que isso representa para o indivíduo. |
| `CT` | Contrato | A recolha de dados para o fim especificado é necessária para cumprir as obrigações contratuais com o indivíduo. |
| `CP` | Cumprimento de uma obrigação legal | A recolha de dados para a finalidade especificada é necessária para cumprir as obrigações legais da empresa. |
| `VI` | Interesse vital do indivíduo | A recolha de dados para o fim especificado é necessária para proteger os interesses vitais do indivíduo. |
| `PI` | Interesse público | A recolha de dados para o fim especificado é necessária para levar a cabo uma missão de interesse público ou no exercício da autoridade oficial. |

## `subscriptions` {#subscriptions}

Algumas empresas permitem que os clientes aceitem assinaturas diferentes associadas a um canal de marketing específico. Por exemplo, uma empresa bancária pode permitir que clientes assinem alertas de telefone para contas com excesso de tempo ou recebam chamadas de vendas para ofertas de programa de fidelidade.

O JSON a seguir representa um exemplo de campo de marketing para um canal de marketing de chamada telefônica que contém um mapa `subscriptions`. Cada chave no objeto `subscriptions` representa uma assinatura individual para o canal de marketing. Por sua vez, cada assinatura contém um valor de opt-in (`val`).

```json
"phone-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "subscribers": {
        "123-555-0928": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "overdrawn-account": {
      "val": "y",
      "type": "issues",
      "subscribers": {
        "123-555-0928": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "301-555-1527": {
          "time": "2020-02-03T07:54:21+07:00",
          "source": "call center"
        }
      }
    }
  }
}
```

| Propriedade | Descrição |
| --- | --- |
| `type` | O tipo de assinatura. Pode ser qualquer string descritiva, desde que tenha 15 caracteres ou menos. |
| `subscribers` | Um campo opcional tipo mapa que representa um conjunto de identificadores (como endereços de email ou números de telefone) que assinaram uma assinatura específica. Cada chave nesse objeto representa o identificador em questão e contém duas subpropriedades: <ul><li>`time`: Um carimbo de data e hora ISO 8601, de quando a identidade é subscrita, se aplicável.</li><li>`source`: A origem do assinante. Pode ser qualquer string descritiva, desde que tenha 15 caracteres ou menos.</li></ul> |

## Recursos adicionais

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)