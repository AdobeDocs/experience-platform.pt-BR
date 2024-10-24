---
solution: Experience Platform
title: Tipo de dados do campo de consentimento genérico
description: Saiba mais sobre o tipo de dados XDM do campo de consentimento genérico.
exl-id: f1f14eb7-21dd-45ca-8fb4-68f397cfa697
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '583'
ht-degree: 1%

---

# Tipo de dados [!UICONTROL Campo de consentimento genérico]

[!UICONTROL Campo de Consentimento Genérico] é um tipo de dados XDM padrão que descreve a seleção de um cliente para uma preferência de consentimento específica.

>[!NOTE]
>
>Este tipo de dados deve ser usado para personalizar a estrutura dos esquemas de consentimento de sua organização usando o grupo de campos [[!UICONTROL Consentimentos e Preferências]](../field-groups/profile/consents.md) como linha de base.

![](../images/data-types/consent-field.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `val` | String | A opção de consentimento fornecida pelo cliente para este caso de uso. Consulte a tabela abaixo para obter os valores e as definições aceitos. |

{style="table-layout:auto"}

A tabela a seguir descreve os valores aceitos para `val`:

| Valor | Título | Descrição |
| --- | --- | --- |
| `y` | Sim (aceitação) | O cliente optou pelo consentimento. Em outras palavras, eles **consentem** o uso de seus dados conforme indicado pelo consentimento em questão. |
| `n` | Não (recusar) | O cliente recusou o consentimento. Em outras palavras, eles **não** consentiram com a utilização de seus dados conforme indicado pelo consentimento em questão. |
| `p` | Verificação pendente | O sistema ainda não recebeu um valor de consentimento final. Isso é usado com mais frequência como parte de um consentimento que requer verificação em duas etapas. Por exemplo, se um cliente optar por receber emails, esse consentimento será definido como `p` até que ele selecione um link em um email para verificar se forneceu o endereço de email correto. Nesse momento, o consentimento será atualizado para `y`.<br><br>Se este consentimento não usar um processo de verificação de dois conjuntos, a opção `p` poderá ser usada para indicar que o cliente ainda não respondeu ao prompt de consentimento. Por exemplo, você pode definir automaticamente o valor como `p` na primeira página de um site, antes que o cliente tenha respondido ao prompt de consentimento. Em jurisdições que não exigem consentimento explícito, você também pode usá-lo para indicar que o cliente não recusou explicitamente (em outras palavras, o consentimento é presumido). |
| `u` | Desconhecido | As informações de consentimento do cliente são desconhecidas. |
| `dy` | Padrão de Sim (aceitação) | O cliente não forneceu um valor de consentimento e é tratado como uma aceitação (&quot;Sim&quot;) por padrão. Em outras palavras, o consentimento é presumido até que o cliente indique o contrário.<br><br>Observe que, se leis ou alterações na política de privacidade da sua empresa resultarem em alterações nos padrões de alguns ou de todos os usuários, será necessário atualizar manualmente todos os perfis que contenham valores padrão. |
| `dn` | Padrão de Não (recusar) | O cliente não forneceu um valor de consentimento e é tratado como uma opção de não participação (&quot;Não&quot;) por padrão. Em outras palavras, presume-se que o cliente tenha negado o consentimento até que indique o contrário.<br><br>Observe que, se leis ou alterações na política de privacidade da sua empresa resultarem em alterações nos padrões de alguns ou de todos os usuários, será necessário atualizar manualmente todos os perfis que contenham valores padrão. |
| `LI` | Interesse legítimo | O interesse comercial legítimo de coletar e processar esses dados para a finalidade especificada supera o dano potencial que eles representam para o indivíduo. |
| `CT` | Contrato | A coleta de dados para a finalidade especificada é necessária para cumprir obrigações contratuais com o indivíduo. |
| `CP` | Cumprimento de uma obrigação legal | A coleta de dados para a finalidade especificada é necessária para atender às obrigações legais da empresa. |
| `VI` | Interesse vital do indivíduo | A recolha de dados para os fins especificados é necessária para proteger os interesses vitais do indivíduo. |
| `PI` | Interesse público | A recolha de dados para os fins especificados é necessária para executar uma missão de interesse público ou para o exercício da autoridade pública. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/consent/consent-field.schema.json)
