---
title: Grupo de campos de esquema de cobertura
description: Saiba mais sobre o grupo de campos Esquema de cobertura.
badgePrivateBeta: label="Private Beta" type="Informative"
hide: true
hidefromtoc: true
source-git-commit: 7d33c5474629b2b02c19e752cdf2cb0a2ba19f19
workflow-type: tm+mt
source-wordcount: '759'
ht-degree: 6%

---

# Grupo de campos de esquema [!UICONTROL Cobertura]

[!UICONTROL Cobertura] é um grupo de campos de esquema padrão para [[!DNL Plan] classe](../../classes/plan.md). Ele fornece um único campo de tipo de objeto `healthcareCoverage` que se destina a fornecer os identificadores e descritores de alto nível de um plano de seguro, normalmente as informações que apareceriam em um cartão de seguro, que podem ser usadas para pagar, em parte ou no todo, pela oferta de produtos e serviços de saúde.

![Estrutura do grupo de campos](../../images/field-groups/healthcare-coverage/coverage.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Beneficiário do Plano] | `beneficiary` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | A parte que se beneficia da cobertura do seguro e o paciente quando os produtos ou serviços são fornecidos. |
| [!UICONTROL Classe] | `class` | Matriz de objetos | Um conjunto de classificadores específicos de subscritor. Consulte a [seção abaixo](#class) para obter mais informações. |
| [!UICONTROL Contato] | `contract` | Matriz de [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | A(s) apólice(s) que constituem esta cobertura de seguro. |
| [!UICONTROL Custo Para O Beneficiário] | `costToBeneficiary` | Matriz de objetos | Um conjunto de códigos indicando a categoria de custo e o valor associado que foram detalhados na política e podem ter sido incluídos no cartão de integridade. Consulte a [seção abaixo](#cost-to-beneficiary) para obter mais informações. |
| [!UICONTROL Exceção] | `exception` | Matriz de objetos | Um conjunto de códigos que indica exceções ou reduções nos custos do paciente e seus períodos efetivos. Consulte a [seção abaixo](#exception) para obter mais informações. |
| [!UICONTROL Identificador] | `identifier` | Matriz de [[!UICONTROL Identificador]](../../data-types/healthcare/identifier.md) | O identificador da cobertura conforme emitido pela seguradora. |
| [!UICONTROL Plano de seguro] | `insurancePlan` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | Os detalhes, benefícios e custos do plano de seguro que constituem esta cobertura de seguro. |
| [!UICONTROL Seguradora] | `insurer` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | O subscritor do programa ou plano, pagador ou seguradora. |
| [!UICONTROL Pagamento por] | `paymentBy` | Matriz de objetos | A ligação ao pagador e, opcionalmente, o que este será responsável pelo pagamento. Consulte a [seção abaixo](#payment-by) para obter mais informações. |
| [!UICONTROL Datas De Início E Término Da Cobertura] | `period` | [[!UICONTROL Período]](../../data-types/healthcare/period.md) | O período durante o qual a cobertura está ativa. Uma data de início ausente indica que a data de início não é conhecida. Uma data de término ausente significa que a cobertura está em andamento. |
| [!UICONTROL Detentor da Política] | `policyHolder` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | A parte que detém a apólice de seguro. |
| [!UICONTROL Relacionamento do beneficiário] | `relationship` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O relacionamento do beneficiário com o assinante. |
| [!UICONTROL Assinante] | `subscriber` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | A parte que detém a relação contratual com a apólice. |
| [!UICONTROL Identificador do Assinante] | `subscriberId` | Matriz de [[!UICONTROL Identificador]](../../data-types/healthcare/identifier.md) | A ID atribuída pela seguradora do assinante. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O tipo de cobertura. |
| [!UICONTROL Número do Dependente] | `dependent` | String | O designador de um dependente sob a cobertura. |
| [!UICONTROL Tipo] | `kind` | String | O tipo de cobertura. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `insurance` </li> <li> `self-pay` </li> <li> `other` </li> |
| [!UICONTROL Rede de seguradoras] | `network` | String | A rede de fornecedores à qual o beneficiário pode solicitar um tratamento que será coberto pela taxa na rede, caso contrário aplicam-se os termos e condições fora da rede. |
| [!UICONTROL Ordem de Cobertura] | `order` | Número inteiro | A ordem relativa da cobertura, com um valor mínimo de `0`. |
| [!UICONTROL Status] | `status` | String | O status da cobertura. O valor dessa propriedade deve ser igual a um dos seguintes valores de enumeração conhecidos. <li> `active` </li> <li> `cancelled` </li> <li> `draft` </li> <li> `entered-in-error` </li> |
| [!UICONTROL Sub-rogação] | `subrogation` | Booleano | Quando `true`, esta instância de seguro foi incluída não para adjudicação, mas para fornecer às seguradoras os detalhes para recuperar os custos. |

Para obter mais detalhes sobre o grupo de campos, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/extensions/industry/healthcare/fhir/fieldgroups/coverage.schema.json)

## `class` {#class}

`class` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![Estrutura de classe](../../images/field-groups/healthcare-coverage/class.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Tipo] | `type` | Matriz de [[!UICONTROL Conceito Codificável]](../../data-types/healthcare/codeable-concept.md) | O tipo de classificação para o qual um rótulo de classe específico da seguradora, ou número e nome opcional, é fornecido. Por exemplo, o tipo pode ser usado para identificar uma classe de cobertura, grupo de empregadores, política ou plano. |
| [!UICONTROL Valor] | `value` | [[!UICONTROL Identificador]](../../data-types/healthcare/identifier.md) | O identificador alfanumérico associado ao rótulo emitido pela seguradora. |
| [!UICONTROL Nome] | `name` | String | Uma descrição curta para a classe. |

## `costToBeneficiary` {#cost-to-beneficiary}

`costToBeneficiary` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![Custo para a estrutura do beneficiário](../../images/field-groups/healthcare-coverage/cost-to-beneficiary.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Categoria] | `category` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O código para identificar o tipo geral de benefícios sob os quais os produtos e serviços são fornecidos. |
| [!UICONTROL Rede] | `network` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O código para indicar se os benefícios se referem a provedores na rede ou fora da rede. |
| [!UICONTROL Termo] | `term` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O prazo dos valores, como benefício vitalício máximo. |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | A categoria de custos centrados no paciente associados ao tratamento. |
| [!UICONTROL Unidade] | `unit` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | Indica se as prestações se aplicam a um indivíduo ou família. |

## `exception` {#exception}

`exception` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![Estrutura de exceção](../../images/field-groups/healthcare-coverage/exception.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Tipo] | `type` | [[!UICONTROL Conceito codificável]](../../data-types/healthcare/codeable-concept.md) | O código da exceção específica. |
| [!UICONTROL Período] | `period` | [[!UICONTROL Período]](../../data-types/healthcare/period.md) | O período em que a exceção está ativa. |

## `paymentBy` {#payment-by}

`paymentBy` é fornecido como uma matriz de objetos. A estrutura de cada objeto é descrita abaixo.

![Pagamento por estrutura](../../images/field-groups/healthcare-coverage/payment-by.png)

| Nome de exibição | Propriedade | Tipo de dados | Descrição |
| --- | --- | --- | --- |
| [!UICONTROL Festa] | `party` | [[!UICONTROL Referência]](../../data-types/healthcare/reference.md) | A lista das partes que fornecem pagamentos não relacionados com seguros para os custos do tratamento. |
| [!UICONTROL Responsabilidade] | `responsibility` | String | A descrição da responsabilidade financeira. |
