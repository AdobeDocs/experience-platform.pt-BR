---
title: Tipo de dados de detalhes da conta
description: Saiba mais sobre o tipo de dados Detalhes da conta do Experience Data Model (XDM).
exl-id: 17254393-263e-4000-9bd2-815a9e842533
source-git-commit: de8e944cfec3b52d25bb02bcfebe57d6a2a35e39
workflow-type: tm+mt
source-wordcount: '409'
ht-degree: 11%

---

# Tipo de dados [!UICONTROL Detalhes da conta]

[!UICONTROL Detalhes da conta] é um tipo de dados padrão do Experience Data Model (XDM) que descreve detalhes relacionados a uma organização comercial.

![Estrutura de tipo de dados](../images/data-types/account-details.png)

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `annualRevenue` | [[!UICONTROL Moeda]](./currency.md) | A quantidade estimada de receita anual da organização. |
| `DUNSNumber` | String | Número D-U-N-S da Dun &amp; Bradstreet da organização. Este é um número não indicativo de nove dígitos atribuído a cada local de negócios no banco de dados da Dun &amp; Bradstreet com uma operação única, separada e distinta, e é mantido exclusivamente pela Dun &amp; Bradstreet. |
| `NAICSCode` | String | A classificação da organização no Sistema de Classificação da Indústria da América do Norte. |
| `NAICSDescription` | String | Uma breve descrição da linha de negócios de uma organização, com base em seu código NAICS. |
| `SICCode` | String | O código de Classificação Industrial Padrão (SIC) da organização. Este é um código de quatro dígitos que categoriza o setor ao qual as empresas pertencem com base em suas atividades comerciais. |
| `SICDescription` | String | Uma breve descrição da linha de negócios de uma organização, com base em seu código SIC. |
| `companyProductAndServices` | String | Os produtos e serviços com os quais a organização está negociando ou fazendo negócios. |
| `facebookPageUrl` | String | Um link de site para a conta da Facebook da organização. |
| `industry` | String | O setor do qual esta organização faz parte. Este é um campo de forma livre, e é aconselhável usar um valor estruturado para consultas ou usar a propriedade `xdm:classifier`. |
| `jigsaw` | String | A chave Data.com da organização. |
| `linkedinPageUrl` | String | Um link de site para a conta da LinkedIn da organização. |
| `logoUrl` | String | Um caminho a ser combinado com a URL de uma instância do Salesforce (por exemplo, `https://yourInstance.salesforce.com/`) para gerar uma URL para solicitar a imagem do perfil da rede social associada à organização. O URL gerado retorna um redirecionamento HTTP (código 302) para a imagem de perfil da rede social da organização. |
| `marketSegment` | String | O público-alvo de mercado nomeado do qual a organização participa. Este é um campo de forma livre, e é aconselhável usar um valor estruturado para consultas ou usar a propriedade `xdm:identifier`. |
| `numberOfEmployees` | Número inteiro | Número de funcionários na organização. |
| `organizationType` | String | Um rótulo que descreve o tipo de organização. |
| `primaryEmailDomain` | String | O domínio de email principal que a organização usa para sua equipe. |
| `rating` | Duplo | A pontuação calculada ou classificação por estrelas para esta organização. `1` indica a classificação máxima possível, e `0` é a classificação mínima possível. |
| `tickerSymbol` | String | O símbolo do mercado de ações desta conta. Máximo de 20 caracteres. |
| `twitterHandleUrl` | String | Um link de site para o identificador de twitter da organização. |
| `website` | String | O URL do site da organização. |

{style="table-layout:auto"}

Para obter mais detalhes sobre o tipo de dados, consulte o repositório XDM público:

* [Exemplo preenchido](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.example.1.json)
* [Esquema completo](https://github.com/adobe/xdm/blob/master/components/datatypes/b2b/account-organization.schema.json)
