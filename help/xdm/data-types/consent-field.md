---
solution: Experience Platform
title: Tipo de dados do campo de consentimento genérico
topic: visão geral
description: Este documento fornece uma visão geral do tipo de dados XDM do campo de consentimento genérico.
translation-type: tm+mt
source-git-commit: ebcd8900687b6e91d3f06690a9db0e118bbc3b58
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 2%

---


# [!UICONTROL Generic Consent Field] tipo de dados

[!UICONTROL Generic Consent Field] é um tipo de dados XDM padrão que descreve a seleção de um cliente para uma preferência de consentimento específica.

>[!NOTE]
>
>Esse tipo de dados deve ser usado para personalizar a estrutura dos esquemas de consentimento de sua organização usando a combinação [[!UICONTROL Privacy/Personalization/Marketing Preferences (Consents)]](../mixins/profile/consents.md) como linha de base.

![](../images/data-types/consent-field.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `val` | String | A opção de consentimento fornecida pelo cliente para esse caso de uso. Consulte a tabela abaixo para obter os valores e as definições aceitos. |

A tabela a seguir descreve os valores aceitos para `val`:

| Valor | Title | Descrição |
| --- | --- | --- |
| `y` | Sim | O cliente aceitou o consentimento. Em outras palavras, eles **do** consentiram com o uso de seus dados, conforme indicado pelo consentimento em questão. |
| `n` | Não | O cliente recusou o consentimento. Em outras palavras, eles **não** consentiram com o uso de seus dados, conforme indicado pelo consentimento em questão. |
| `p` | Verificação pendente | O sistema ainda não recebeu um valor de consentimento final. Isso é usado com mais frequência como parte de um consentimento que requer verificação em duas etapas. Por exemplo, se um cliente optar por receber emails, esse consentimento será definido como `p` até que selecione um link em um email para verificar se forneceu o endereço de email correto, momento em que o consentimento seria atualizado para `y`.<br><br>Se esse consentimento não usar um processo de verificação de dois conjuntos, a  `p` escolha poderá ser usada para indicar que o cliente ainda não respondeu ao prompt de consentimento. Por exemplo, você pode definir automaticamente o valor para `p` na primeira página de um site, antes que o cliente tenha respondido ao prompt de consentimento. Em jurisdições que não exigem consentimento explícito, você também pode usá-lo para indicar que o cliente não recusou explicitamente (em outras palavras, o consentimento é presumido). |
| `u` | Desconhecido | As informações de consentimento do cliente são desconhecidas. |
| `LI` | Interesse legítimo | O interesse comercial legítimo em recolher e processar esses dados para a finalidade especificada supera o potencial dano que isso representa para o indivíduo. |
| `CT` | Contrato | A recolha de dados para o fim especificado é necessária para cumprir as obrigações contratuais com o indivíduo. |
| `CP` | Cumprimento de uma obrigação legal | A recolha de dados para a finalidade especificada é necessária para cumprir as obrigações legais da empresa. |
| `VI` | Interesse vital do indivíduo | A recolha de dados para o fim especificado é necessária para proteger os interesses vitais do indivíduo. |
| `PI` | Interesse público | A recolha de dados para o fim especificado é necessária para levar a cabo uma missão de interesse público ou no exercício da autoridade oficial. |

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)