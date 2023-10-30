---
title: Extensão de encaminhamento de eventos da API de conversões do Linkedin
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform permite medir o desempenho da sua campanha de marketing do Linkedin.
last-substantial-update: 2023-10-25T00:00:00Z
exl-id: 411e7b77-081e-4139-ba34-04468e519ea5
source-git-commit: 308d07cf0c3b4096ca934a9008a13bf425dc30b6
workflow-type: tm+mt
source-wordcount: '758'
ht-degree: 2%

---

# Extensão da API de conversões do [!DNL LinkedIn]

[[!DNL LinkedIn Conversions API]](https://learn.microsoft.com/en-us/linkedin/marketing/integrations/ads-reporting/conversions-api) O é uma ferramenta de rastreamento de conversão que cria uma conexão direta entre os dados de marketing do servidor de um anunciante e [!DNL LinkedIn]. Isso permite que os anunciantes avaliem a eficácia de seus [!DNL LinkedIn] campanhas de marketing independentemente do local da conversão e utilizam essas informações para impulsionar a otimização da campanha. A variável [!DNL LinkedIn Conversions API] Essa extensão pode ajudar a fortalecer o desempenho e reduzir o custo por ação com atribuição mais completa, maior confiabilidade dos dados e melhor otimização da entrega.

## Pré-requisitos {#prerequisites}

Você deve criar uma regra de conversão em seu [!DNL LinkedIn] conta de anúncios de campanha. [!DNL Adobe] A recomenda incluir &quot;CAPI&quot; no início do nome da regra de conversa para separá-lo de outros tipos de regras de conversão que você possa ter configurado.

### Criar um segredo e um elemento de dados

Criar um novo [!DNL LinkedIn] [segredo de encaminhamento de eventos](../../../ui/event-forwarding/secrets.md) e forneça um nome exclusivo que signifique o membro de autenticação. Ele será usado para autenticar a conexão com sua conta, mantendo o valor seguro.

Em seguida, [criar um elemento de dados](../../../ui/managing-resources/data-elements.md#create-a-data-element) usando o [!UICONTROL Núcleo] extensão e um [!UICONTROL Segredo] tipo de elemento de dados para fazer referência ao `LinkedIn` segredo que acabou de criar.

## Instale e configure o [!DNL LinkedIn] extensão {#install}

Para instalar a extensão, [criar uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou selecione uma propriedade existente para editar.

Selecionar **[!UICONTROL Extensões]** no painel de navegação esquerdo. No **[!UICONTROL Catálogo]** , selecione a **[!UICONTROL LinkedIn]** e selecione **[!UICONTROL Instalar]**.

![O catálogo de extensões que mostra o [!DNL LinkedIn] placa de extensão destacando instalar.](../../../images/extensions/server/linkedin/install-extension.png)

Na próxima tela, digite o segredo do elemento de dados criado anteriormente na variável `Access Token` campo. O segredo do elemento de dados conterá seu [!DNL LinkedIn] Token do OAuth 2. Selecione **[!UICONTROL Salvar]** ao concluir.

![A variável [!DNL LinkedIn] página de configuração de extensão com o [!UICONTROL Token de acesso] campo e [!UICONTROL Salvar] destacado.](../../../images/extensions/server/linkedin/configure-extension.png)

## Criar um [!DNL Send Conversion] regra {#tracking-rule}

Depois que todos os elementos de dados forem configurados, você poderá começar a criar regras de encaminhamento de eventos que determinam quando e como seus eventos serão enviados para o [!DNL LinkedIn].

Criar um novo encaminhamento de eventos [regra](../../../ui/managing-resources/rules.md) na propriedade de encaminhamento de eventos. Em **[!UICONTROL Ações]**, adicione uma nova ação e defina a extensão para **[!UICONTROL LinkedIn]**. Em seguida, selecione **[!UICONTROL Enviar conversão da Web]** para o **[!UICONTROL Tipo de ação]**.

![A visualização Regras de propriedade do encaminhamento de eventos, com os campos necessários para adicionar uma configuração de ação de regra de encaminhamento de eventos destacados.](../../../images/extensions/server/linkedin/linkedin-event-action.png)

Após a seleção, controles adicionais são exibidos para configurar ainda mais o evento. Selecionar **[!UICONTROL Manter alterações]** para salvar a regra.

**[!UICONTROL Dados do usuário]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Email] | Endereço de email do contato associado ao evento de conversão. O valor do email será codificado pelo código de extensão em SHA256, a menos que o valor fornecido já seja uma string SHA256. |
| [!UICONTROL UUID de rastreamento de anúncios próprios do linkedIn] | Esta é uma ID de cookie primário. Os anunciantes precisam ativar o rastreamento de conversão aprimorado do [[!DNL LinkedIn Campaign Manager]](https://www.linkedin.com/help/lms/answer/a423304/enable-first-party-cookies-on-a-linkedin-insight-tag) para ativar cookies próprios que anexam um parâmetro de ID de clique `li_fat_id` aos URLs de clique. |
| [!UICONTROL Dados de informações do cliente] | Esse campo contém um objeto JSON com atributos extras que serão enviados junto com a mensagem.<br><br>No **[!UICONTROL Brutos]** , você pode colar o objeto JSON diretamente no campo de texto fornecido ou selecionar o ícone de elemento de dados (![Ícone de conjunto de dados](../../../images/extensions/server/aws/data-element-icon.png)) para selecionar de uma lista de elementos de dados existentes para representar os dados.<br><br>Você também pode usar a variável **[!UICONTROL Editor de pares de valor-chave JSON]** opção para adicionar manualmente cada par de valor-chave por meio de um editor de interface do usuário. Cada valor pode ser representado por uma entrada bruta, ou um elemento de dados pode ser selecionado. Os valores de chave aceitos são: `firstName`, `lastName`, `companyName`, `title` e `country`. |

{style="table-layout:auto"}

![A variável [!DNL User Data] seção que mostra exemplos de entrada de dados nos campos.](../../../images/extensions/server/linkedin/configure-extension-user-data.png)

**[!UICONTROL Dados de conversão]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Conversão] | A ID da regra de conversão criada em [Gerente de campanha do linkedIn](https://www.linkedin.com/help/lms/answer/a1657171) ou por meio de [!DNL LinkedIn Campaign Manager]. |
| [!UICONTROL Tempo de conversão] | Cada carimbo de data e hora em milissegundos em que o evento de conversão aconteceu. <br><br> Observação: se a fonte registrar o carimbo de data e hora de conversão em segundos, insira 000 no final para transformá-lo em milissegundos. |
| [!UICONTROL Moeda] | Código de moeda em formato ISO. |
| [!UICONTROL Quantidade] | Valor da conversão em sequência decimal (por exemplo, &quot;100,05&quot;). |
| [!UICONTROL ID de evento] | A ID exclusiva gerada pelos anunciantes para indicar cada evento. Este campo é opcional e é usado para desduplicação. |

{style="table-layout:auto"}

![A variável [!DNL Conversion Data] seção que mostra dados de exemplo nos campos.](../../../images/extensions/server/linkedin/configure-extension-conversions-data.png)

**[!UICONTROL Substituições de configuração]**

> OBSERVAÇÃO 
>
>A variável [!UICONTROL Substituições de configuração] permite que um usuário defina um campo diferente [!DNL LinkedIn] em cada regra, permitindo que cada regra use um token de acesso que possa ter acesso a diferentes [!DNL LinkedIn] contas de publicidade.

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Token de acesso] | A variável [!DNL LinkedIn] token de acesso. |

![A variável [!DNL Configuration Overrides] seção que mostra exemplos de entrada de dados no campo.](../../../images/extensions/server/linkedin/configure-extension-configuration-override.png)

## Próximas etapas

Este guia abordou como enviar dados para o [!DNL LinkedIn] usando o [!DNL LinkedIn Conversions API] extensão de encaminhamento de eventos. Para obter mais informações sobre os recursos de encaminhamento de eventos do [!DNL Adobe Experience Platform], consulte o [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
