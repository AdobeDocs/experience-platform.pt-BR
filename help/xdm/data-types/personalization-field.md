---
solution: Experience Platform
title: Tipo de dados do campo de preferência Personalização genérica
topic-legacy: overview
description: Este documento fornece uma visão geral do tipo de dados XDM do campo de preferência de personalização genérica.
exl-id: 3f6a3c31-19f3-4bad-921e-9ad33c6b9ac9
source-git-commit: 0f39e9237185b49417f2af8dfc288ab1420cccae
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 2%

---

# [!UICONTROL Campo de preferência Personalização genérica] tipo de dados

[!UICONTROL Campo de preferência Personalização genérica] é um tipo de dados XDM padrão que descreve a seleção de um cliente para uma preferência de personalização específica.

>[!NOTE]
>
>Esse tipo de dados deve ser usado para personalizar a estrutura dos esquemas de consentimento de sua organização usando o [[!UICONTROL Consentimentos e preferências] grupo de campos](../field-groups/profile/consents.md) como linha de base.

![](../images/data-types/personalization-field.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `val` | String | A escolha de preferência fornecida pelo cliente para esse caso de uso de personalização. Consulte a tabela abaixo para obter os valores e as definições aceitos. |

{style=&quot;table-layout:auto&quot;}

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

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.example.1.json)
* [Schema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/personalization-field.schema.json)
