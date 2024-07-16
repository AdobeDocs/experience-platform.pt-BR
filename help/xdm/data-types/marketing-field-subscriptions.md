---
solution: Experience Platform
title: Campo de preferência de marketing genérico com tipo de dados de assinaturas
description: Saiba mais sobre o Campo de preferência de marketing genérico com tipo de dados XDM de assinaturas.
exl-id: 170ea6ca-77fc-4b0a-87f9-6d4b6f32d953
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 1%

---

# [!UICONTROL Campo de Preferência de Marketing Genérico com Assinaturas] tipo de dados

O [!UICONTROL Campo de Preferência de Marketing Genérico com Assinaturas] é um tipo de dados XDM padrão que descreve a seleção de um cliente para uma preferência de marketing específica.

>[!NOTE]
>
>Este tipo de dados deve ser usado para personalizar a estrutura dos esquemas de consentimento de sua organização usando o grupo de campos [[!UICONTROL Consentimentos e Preferências]](../field-groups/profile/consents.md) como linha de base.
>
>Se você não precisar de um mapa `subscriptions` para um campo de preferência de marketing específico, poderá usar o [tipo de dados básicos de campo de marketing](./marketing-field.md).

![](../images/data-types/marketing-field-subscriptions.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `reason` | String | Quando um cliente recusa um caso de uso de marketing, esse campo de string representa o motivo pelo qual o cliente recusou. |
| `subscriptions` | Mapa | Um mapa de preferências de marketing do cliente para assinaturas específicas. Consulte a seção sobre [assinaturas](#subscriptions) para obter mais informações. |
| `time` | DateTime | Um carimbo de data e hora ISO 8601 que indica quando a preferência de marketing foi alterada, se aplicável. |
| `val` | String | A opção de preferência fornecida pelo cliente para este caso de uso de marketing. Consulte a [próxima seção](#val) para obter os valores e as definições aceitos. |

{style="table-layout:auto"}

## `val` {#val}

A tabela a seguir descreve os valores aceitos para `val`:

| Valor | Título | Descrição |
| --- | --- | --- |
| `y` | Sim (aceitação) | O cliente optou pela preferência. Em outras palavras, eles **consentem** o uso de seus dados conforme indicado pela preferência em questão. |
| `n` | Não (recusar) | O cliente recusou a preferência. Em outras palavras, **não** consente com o uso de seus dados conforme indicado pela preferência em questão. |
| `p` | Verificação pendente | O sistema ainda não recebeu um valor final de preferência. Isso é usado com mais frequência como parte de um consentimento que requer verificação em duas etapas. Por exemplo, se um cliente optar por receber emails, esse consentimento será definido como `p` até que ele selecione um link em um email para verificar se forneceu o endereço de email correto. Nesse momento, o consentimento será atualizado para `y`.<br><br>Se esta preferência não usar um processo de verificação de dois conjuntos, a opção `p` poderá ser usada para indicar que o cliente ainda não respondeu ao prompt de consentimento. Por exemplo, você pode definir automaticamente o valor como `p` na primeira página de um site, antes que o cliente tenha respondido ao prompt de consentimento. Em jurisdições que não exigem consentimento explícito, você também pode usá-lo para indicar que o cliente não recusou explicitamente (em outras palavras, o consentimento é presumido). |
| `u` | Desconhecido | As informações de preferência do cliente são desconhecidas. |
| `dy` | Padrão de Sim (aceitação) | O cliente não forneceu um valor de consentimento e é tratado como uma aceitação (&quot;Sim&quot;) por padrão. Em outras palavras, o consentimento é presumido até que o cliente indique o contrário.<br><br>Observe que, se leis ou alterações na política de privacidade da sua empresa resultarem em alterações nos padrões de alguns ou de todos os usuários, será necessário atualizar manualmente todos os perfis que contenham valores padrão. |
| `dn` | Padrão de Não (recusar) | O cliente não forneceu um valor de consentimento e é tratado como uma opção de não participação (&quot;Não&quot;) por padrão. Em outras palavras, presume-se que o cliente tenha negado o consentimento até que indique o contrário.<br><br>Observe que, se leis ou alterações na política de privacidade da sua empresa resultarem em alterações nos padrões de alguns ou de todos os usuários, será necessário atualizar manualmente todos os perfis que contenham valores padrão. |
| `LI` | Interesse legítimo | O interesse comercial legítimo de coletar e processar esses dados para a finalidade especificada supera o dano potencial que eles representam para o indivíduo. |
| `CT` | Contrato | A coleta de dados para a finalidade especificada é necessária para cumprir obrigações contratuais com o indivíduo. |
| `CP` | Cumprimento de uma obrigação legal | A coleta de dados para a finalidade especificada é necessária para atender às obrigações legais da empresa. |
| `VI` | Interesse vital do indivíduo | A recolha de dados para os fins especificados é necessária para proteger os interesses vitais do indivíduo. |
| `PI` | Interesse público | A recolha de dados para os fins especificados é necessária para executar uma missão de interesse público ou para o exercício da autoridade pública. |

{style="table-layout:auto"}

## `subscriptions` {#subscriptions}

Algumas empresas permitem que os clientes optem por assinaturas diferentes associadas a um canal de marketing específico. Por exemplo, uma empresa bancária pode permitir que os clientes assinem alertas de telefone para contas com saldo negativo ou recebam chamadas de vendas para ofertas de programa de fidelidade.

O JSON a seguir representa um exemplo de campo de marketing para um canal de marketing por chamada telefônica que contém um mapa `subscriptions`. Cada chave no objeto `subscriptions` representa uma assinatura individual do canal de marketing. Cada assinatura contém um valor de aceitação (`val`).

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
| `val` | O [valor de consentimento](#val) da assinatura. |
| `type` | O tipo de assinatura. Pode ser qualquer string descritiva, desde que tenha 15 caracteres ou menos. |
| `topics` | Uma matriz de strings que representa as áreas de interesse que um cliente assinou, que pode ser usada para enviar conteúdo relevante para ele. |
| `subscribers` | Um campo opcional do tipo mapa que representa um conjunto de identificadores (como endereços de email ou números de telefone) que assinaram uma determinada assinatura. Cada chave nesse objeto representa o identificador em questão e contém duas subpropriedades: <ul><li>`time`: um carimbo de data e hora ISO 8601 de quando a identidade foi assinada, se aplicável.</li><li>`source`: a origem da qual o assinante se originou. Pode ser qualquer string descritiva, desde que tenha 15 caracteres ou menos.</li></ul> |

{style="table-layout:auto"}

## Recursos adicionais

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/marketing-field-basic.schema.json)
