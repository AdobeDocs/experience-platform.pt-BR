---
solution: Experience Platform
title: Campo de preferência de marketing genérico com tipo de dados de assinaturas
topic-legacy: overview
description: Este documento fornece uma visão geral do Campo de Preferência de Marketing Genérico com o tipo de dados XDM de Assinaturas.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: bccf97d85421fcb2f8fe153ad0ddbef4975b6f7e
workflow-type: tm+mt
source-wordcount: '900'
ht-degree: 2%

---

# [!UICONTROL Campo de preferência de marketing genérico com assinaturas] tipo de dados

[!UICONTROL Campo de preferência de marketing genérico com assinaturas] é um tipo de dados XDM padrão que descreve a seleção de um cliente para uma preferência de marketing específica.

>[!NOTE]
>
>Esse tipo de dados deve ser usado para personalizar a estrutura dos esquemas de consentimento de sua organização usando o [[!UICONTROL Consentimentos e preferências] grupo de campos](../field-groups/profile/consents.md) como linha de base.
>
>Se você não exigir uma `subscriptions` mapear para um campo de preferência de marketing específico, é possível usar o [tipo de dados básico do campo de marketing](./marketing-field.md) em vez disso.

![](../images/data-types/marketing-field-subscriptions.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `reason` | String | Quando um cliente recusa um caso de uso de marketing, esse campo de cadeia de caracteres representa o motivo pelo qual o cliente optou por não participar. |
| `subscriptions` | Mapa | Um mapa de preferências de marketing do cliente para assinaturas específicas. Consulte a seção sobre [assinaturas](#subscriptions) para obter mais informações. |
| `time` | DateTime | Um carimbo de data e hora ISO 8601 de quando a preferência de marketing foi alterada, se aplicável. |
| `val` | String | A escolha de preferência fornecida pelo cliente para este caso de uso de marketing. Consulte a [próxima seção](#val) para os valores e definições aceites. |

{style=&quot;table-layout:auto&quot;}

## `val` {#val}

A tabela a seguir descreve os valores aceitos para `val`:

| Valor | Title | Descrição |
| --- | --- | --- |
| `y` | Sim (opt-in) | O cliente optou pela preferência. Em outras palavras, eles **do** consentimento para a utilização dos seus dados, conforme indicado pela preferência em causa. |
| `n` | Não (opt-out) | O cliente recusou a preferência. Em outras palavras, eles **não** consentimento para a utilização dos seus dados, conforme indicado pela preferência em causa. |
| `p` | Verificação pendente | O sistema ainda não recebeu um valor de preferência final. Isso é usado com mais frequência como parte de um consentimento que requer verificação em duas etapas. Por exemplo, se um cliente optar por receber emails, esse consentimento será definido como `p` até selecionarem um link em um email para verificar se forneceram o endereço de email correto, em que o consentimento seria atualizado para `y`.<br><br>Se essa preferência não usar um processo de verificação de dois conjuntos, a variável `p` pode ser usada para indicar que o cliente ainda não respondeu ao prompt de consentimento. Por exemplo, é possível definir automaticamente o valor como `p` na primeira página de um site, antes do cliente responder ao prompt de consentimento. Em jurisdições que não exigem consentimento explícito, você também pode usá-lo para indicar que o cliente não recusou explicitamente (em outras palavras, o consentimento é presumido). |
| `u` | Desconhecido | As informações de preferência do cliente são desconhecidas. |
| `dy` | Padrão de Sim (aceitação) | O cliente não forneceu um valor de consentimento em si e é tratado como uma aceitação (&quot;Sim&quot;) por padrão. Em outras palavras, o consentimento é presumido até que o cliente indique o contrário.<br><br>Observe que, se as leis ou alterações na política de privacidade da sua empresa resultarem em alterações nos padrões de alguns ou de todos os usuários, será necessário atualizar manualmente todos os perfis que contêm valores padrão. |
| `dn` | Padrão de Não (opt out) | O cliente não forneceu um valor de consentimento por si só e é tratado como um opt out (&quot;Não&quot;) por padrão. Em outras palavras, presume-se que o cliente tenha negado o consentimento até que indique o contrário.<br><br>Observe que, se as leis ou alterações na política de privacidade da sua empresa resultarem em alterações nos padrões de alguns ou de todos os usuários, será necessário atualizar manualmente todos os perfis que contêm valores padrão. |
| `LI` | Interesse legítimo | O interesse comercial legítimo em recolher e processar esses dados para a finalidade especificada supera o potencial dano que isso representa para o indivíduo. |
| `CT` | Contrato | A recolha de dados para o fim especificado é necessária para cumprir as obrigações contratuais com o indivíduo. |
| `CP` | Cumprimento de uma obrigação legal | A recolha de dados para a finalidade especificada é necessária para cumprir as obrigações legais da empresa. |
| `VI` | Interesse vital do indivíduo | A recolha de dados para o fim especificado é necessária para proteger os interesses vitais do indivíduo. |
| `PI` | Interesse público | A recolha de dados para o fim especificado é necessária para levar a cabo uma missão de interesse público ou no exercício da autoridade oficial. |

{style=&quot;table-layout:auto&quot;}

## `subscriptions` {#subscriptions}

Algumas empresas permitem que os clientes aceitem assinaturas diferentes associadas a um canal de marketing específico. Por exemplo, uma empresa bancária pode permitir que clientes assinem alertas de telefone para contas com excesso de tempo ou recebam chamadas de vendas para ofertas de programa de fidelidade.

O JSON a seguir representa um exemplo de campo de marketing para um canal de marketing de chamada telefônica que contém um `subscriptions` mapa. Cada tecla na `subscriptions` representa uma assinatura individual para o canal de marketing. Por sua vez, cada assinatura contém um valor de aceitação (`val`).

```json
"email-marketing-field": {
  "val": "y",
  "time": "2019-01-01T15:52:25+00:00",
  "subscriptions": {
    "loyalty-offers": {
      "val": "y",
      "type": "sales",
      "topics": ["discounts", "early-access"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2019-01-01T15:52:25+00:00",
          "source": "website"
        }
      }
    },
    "newsletters": {
      "val": "y",
      "type": "advertising",
      "topics": ["hardware"],
      "subscribers": {
        "jdoe@example.com": {
          "time": "2021-01-01T08:32:53+07:00",
          "source": "website"
        },
        "tparan@example.com": {
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
| `val` | O [valor do consentimento](#val) para a assinatura. |
| `type` | O tipo de assinatura. Pode ser qualquer string descritiva, desde que tenha 15 caracteres ou menos. |
| `topics` | Uma matriz de sequências de caracteres que representam as áreas de interesse para as quais um cliente se inscreveu, e que pode ser usada para enviar a ele conteúdo relevante. |
| `subscribers` | Um campo opcional tipo mapa que representa um conjunto de identificadores (como endereços de email ou números de telefone) que assinaram uma assinatura específica. Cada chave nesse objeto representa o identificador em questão e contém duas subpropriedades: <ul><li>`time`: Um carimbo de data e hora ISO 8601, de quando a identidade é subscrita, se aplicável.</li><li>`source`: A origem do assinante. Pode ser qualquer string descritiva, desde que tenha 15 caracteres ou menos.</li></ul> |

{style=&quot;table-layout:auto&quot;}

## Recursos adicionais

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
