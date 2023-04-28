---
keywords: extensão de encaminhamento de eventos, pinterest, extensão de encaminhamento de eventos do pinterest
title: Extensão de encaminhamento de eventos do pinterest
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform permite assimilar eventos no Pinterest para seus requisitos comerciais.
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 87c76ef4b95bc05a64d9d124d69c2a51b7b77c08
workflow-type: tm+mt
source-wordcount: '1550'
ht-degree: 4%

---

# [!DNL Pinterest] extensão de encaminhamento de eventos

[!DNL Pinterest] é um mecanismo de descoberta visual para encontrar ideias como receitas, decoração doméstica, inspiração de estilo e muito mais. Há bilhões de pinos em [!DNL Pinterest], que também pode ser compartilhado com outras pessoas no [!DNL Pinterest]. Você pode coletar eventos de interação do usuário e aproveitar [!DNL Pinterest Analytics] para entender o comportamento do usuário e executar anúncios direcionados.

O [[!DNL Pinterest] Conversões](https://developers.pinterest.com/docs/conversions/conversion-management/) API [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) A extensão permite aproveitar os dados capturados na Rede de borda do Adobe Experience Platform e enviá-los para [!DNL Pinterest]. Este documento aborda os casos de uso da extensão, como instalá-la e como integrar seus recursos ao encaminhamento do evento [regras](../../../ui/managing-resources/rules.md).

Os tokens de acesso de conversões são o método de autenticação usado por [!DNL Pinterest] ao interagir com o [!DNL Pinterest] API.

## Casos de uso

Essa extensão deve ser usada se você quiser usar dados da Edge Network em [!DNL Pinterest] para aproveitar seus recursos de análise do cliente.

Por exemplo, considere uma equipe de marketing em uma organização. A equipe captura os dados do evento de interação do usuário de seu site e os carrega em [!DNL Pinterest] usar essa extensão de encaminhamento de eventos.

As equipes de marketing e análise podem, então, aproveitar [!DNL Pinterest] Recursos do Analytics para entender as principais interações e comportamentos do usuário, permitindo que você entenda melhor os usuários e os direcione para campanhas de anúncios direcionados.

Para obter mais informações sobre casos de uso específicos de [!DNL Pinterest], consulte o [[!DNL Pinterest] casos de uso](https://business.pinterest.com/en/success-stories) documentação.

## [!DNL Pinterest] pré-requisitos {#prerequisites}

Você deve ter um [!DNL Pinterest] [conta](https://help.pinterest.com/en/business/article/get-a-business-account) para usar essa extensão. Vá para o [[!DNL Pinterest] página de registro](https://www.pinterest.com/business/create/) para registrar e criar uma conta, caso ainda não tenha uma.

Você também precisará de um [!DNL Pinterest] conta do desenvolvedor, que precisará ser associada à [!DNL Pinterest] conta comercial. Para associar sua conta de desenvolvedor a sua conta comercial, consulte [[!DNL Pinterest ] conta do desenvolvedor](https://developers.pinterest.com/account-setup/).

### Obter detalhes de configuração necessários {#configuration-details}

Para conectar o Experience Platform a [!DNL Pinterest], são necessárias as seguintes entradas:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| ID da conta do anúncio | Seu [!DNL Pinterest] ID da conta do anúncio. Consulte a [[!DNL Pinterest] documentação](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) para orientação. | 123456789012 |
| Token de acesso de conversão | Seu [!DNL Pinterest] Token de acesso à conversão. Consulte a [[!DNL Pinterest] API de conversões](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) documento de orientação. <br> **Você só precisará fazer isso uma vez, pois esse token não expira.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Instalar e configurar o [!DNL Pinterest] extensão {#install}

Para instalar a extensão, [criar uma propriedade de encaminhamento de evento](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Na navegação à esquerda, selecione **[!UICONTROL Extensões]**. Selecionar **[!UICONTROL Instalar]** no cartão para o [!DNL Pinterest] na **[!UICONTROL Catálogo]** guia .

![Catálogo que exibe [!DNL Pinterest] extensão com [!UICONTROL Instalar] destacado.](../../../images/extensions/server/pinterest/install.png)

### Configurar a extensão [!DNL Pinterest]

>[!IMPORTANT]
>
>Dependendo das necessidades de implementação, talvez seja necessário criar um esquema, elementos de dados e um conjunto de dados antes de configurar a extensão. Revise todas as etapas de configuração antes de começar para determinar quais entidades você precisa configurar para o caso de uso.

Na navegação à esquerda, selecione **[!UICONTROL Extensões]**. Selecionar **[!UICONTROL Configurar]** no cartão para o [!DNL Pinterest] na [!UICONTROL Instalado]**.

![[!DNL Pinterest] mostrada na [!UICONTROL Instalar] com [!UICONTROL Configurar] destacado.](../../../images/extensions/server/pinterest/configure.png)

Na próxima tela, insira o [!UICONTROL ID da conta do anúncio] e [!UICONTROL Token de acesso de conversão] que você já reuniu na [detalhes da configuração](#configuration-details) seção. Quando terminar, selecione **[!UICONTROL Salvar]**.

![O [!DNL Pinterest] [!UICONTROL Configurar] realce da tela [!UICONTROL ID da conta do anúncio] e [!UICONTROL Token de acesso de conversão] campos de entrada.](../../../images/extensions/server/pinterest/input.png)

## Configurar uma regra de encaminhamento de eventos {#config-rule}

Depois que todos os elementos de dados estiverem configurados, você poderá começar a criar regras de encaminhamento de eventos que determinam quando e como seus eventos serão enviados para o [!DNL Pinterest].

Crie um novo [regra](../../../ui/managing-resources/rules.md) na propriedade de encaminhamento do evento. Em **[!UICONTROL Ações]**, adicione uma nova ação e defina a extensão para **[!UICONTROL Pinterest]**. Para enviar eventos de rede do Adobe Experience Edge para [!DNL Pinterest], defina o **[!UICONTROL Tipo de ação]** para **[!UICONTROL Enviar evento].**

![O [!DNL Pinterest] [!UICONTROL Enviar evento] criação da regra.](../../../images/extensions/server/pinterest/rule.png)

Após a seleção, os controles adicionais são exibidos para configurar ainda mais o evento. Você precisa mapear a variável [!DNL Pinterest] propriedades do evento para os elementos de dados criados anteriormente.

### [!UICONTROL Dados do evento]

Os seguintes dados de evento serão necessários para criar a nova regra:

| Nome do campo | Descrição | Exemplo |
| --- | --- | --- | 
| [!UICONTROL Nome do evento] | O tipo do evento do usuário. No entanto, pode ser qualquer tipo de evento para aproveitar [!DNL Pinterest Analytics] é recomendável usar [[!DNL Pinterest] códigos de evento](https://help.pinterest.com/en/business/article/add-event-codes) | * checkout <br> * add_to_cart <br> * page_visit <br> * inscrição <br> * [Evento definido pelo usuário] |
| [!UICONTROL Fonte da ação] | A fonte que indica onde o evento de conversão ocorreu. | * app_android <br> * app_ios <br> * web <br> * offline |
| [!UICONTROL Hora do evento] | Refere-se à hora do evento. O formato de hora padrão usado é UNIX, no formato `<seconds>.<miliseconds>` dependendo do fuso horário local. Para obter mais informações, consulte [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 indica 1433188255 segundos e 500 milissegundos após a época ou segunda-feira, 1° de junho de 2015, às 7:50:17:00 GMT |
| [!UICONTROL ID do evento] | Uma string de id exclusiva que identifica esse evento e pode ser usada para fazer dedupe entre eventos assimilados por meio da API de conversão e do rastreamento do Pinterest. Sem isso, é provável que os dados do evento sejam contados duas vezes e reportem a inflação da métrica. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Propriedades do evento] | Um objeto JSON que contém propriedades personalizadas do evento. Selecione entre fornecer JSON bruto ou usar um conjunto simplificado de entradas de valor chave. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![O [!DNL Pinterest] [!UICONTROL Dados do evento] destacado na ação da regra.](../../../images/extensions/server/pinterest/event-data.png)

As seguintes propriedades de evento podem ser configuradas:

| Nome do campo | Descrição |
| --- | --- |
| URL de origem do evento | URL do evento de conversão da Web. |
| ID da loja de aplicativos | A ID do aplicativo da loja de aplicativos. |
| Nome do aplicativo | O nome do aplicativo  |
| Application Version | A versão do aplicativo. |
| Marca do dispositivo | Marca do dispositivo que está sendo usado pelo usuário. |
| Operadora de dispositivo | Operadora de celular do usuário para seu dispositivo. |
| Modelo do dispositivo | Modelo do dispositivo do usuário. |
| Device Type | Tipo de dispositivo que está sendo usado pelo usuário. |
| Versão do SO | Versão do sistema operacional do dispositivo. |
| Idioma do usuário | Código de idioma ISO-639-1 de dois caracteres, indicando o idioma do usuário. |

### [!UICONTROL Dados do usuário]

Os seguintes dados de usuário podem ser inseridos por campos não obrigatórios:

| Nome do campo | Descrição | Exemplo |
| --- | --- | --- | 
| [!UICONTROL Email] | Endereço de email do usuário ou hash SHA256 do email de endereço do usuário. | ebd543592...f2b7e1 |
| [!UICONTROL IDs de publicidade móvel] | Hash Sha256 das &quot;IDs de publicidade da Google&quot; (GAIDs) ou &quot;Identificador de  da Apple para anunciantes&quot; (IDFAs) do usuário | ebd543592...f2b7e1 |
| [!UICONTROL Endereço IP do Cliente] | O endereço IP do usuário, que pode estar no formato IPv4 ou IPv6. Usado para correspondência. | 192.168.0.1 |
| [!UICONTROL Agente do usuário cliente] | A sequência de agente do usuário do navegador da Web do usuário. | Mozilla/5.0 (plataforma; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Dados de informações do cliente] | Um objeto JSON contendo outras informações do cliente. Selecione entre fornecer JSON bruto ou usar um conjunto simplificado de entradas de valor chave. | { &quot;ph&quot;: &quot;122333445&quot; } |

![O [!DNL Pinterest] [!UICONTROL Dados do usuário] destacado na ação da regra.](../../../images/extensions/server/pinterest/user-data.png)

As propriedades de informações do cliente que podem ser configuradas são:

| Nome do campo | Descrição |
| --- | --- |
| Telefone | Número de contato do usuário. Somente dígitos são aceitos e devem ser inseridos com código de país, código de área e número. |
| Gênero | O gênero pode ser inserido como &quot;f&quot; para feminino, &quot;m&quot; para masculino ou &quot;n&quot; para não binário. |
| Data de nascimento | Data de nascimento, inserida como ano, mês e dia. |
| Sobrenome | Sobrenome do usuário. |
| Primeiro nome | Nome do usuário. |
| Cidade | Cidade de residência do usuário. Isso é usado principalmente para fins de faturamento. |
| Estado | Estado do usuário, que é fornecido como um código de duas letras em minúsculas. |
| Código postal | CEP do usuário, que é usado principalmente para fins de faturamento. |
| País | Código ISO-3166 de dois caracteres, que indica o país do usuário. |
| ID externa | Id exclusiva do anunciante que identifica um usuário em seu espaço. Por exemplo, ID de usuário, ID de fidelidade e assim por diante. |
| Clique em ID | O identificador exclusivo armazenado no cookie _epik em seu domínio ou parâmetro de consulta &amp;epik= no URL. |

>[!IMPORTANT]
>
>Antes de enviar os dados para a [!DNL Pinterest] endpoint da API, a extensão fará hash e normalizará os valores dos seguintes campos: Email, Número de telefone, Nome, Sobrenome, Gênero, Data de nascimento, Cidade, Estado, CEP, País e ID externa. A extensão não fará hash no valor desses campos se uma string SHA256 já estiver presente.

### [!UICONTROL Dados personalizados]

Os seguintes dados personalizados podem ser inseridos para a regra:

| Nome do campo | Descrição |
| --- | --- |
| Moeda | O código monetário ISO-4217. Se isso não for fornecido, [!DNL Pinterest] será padrão para a moeda do anunciante que foi definida durante a criação da conta. |
| Valor | Valor total do evento. Aceito como uma cadeia de caracteres na solicitação. Isso será analisado em um dígito duplo. |
| Sequência de pesquisa | A string de pesquisa relacionada ao evento de conversão do usuário. |
| ID do pedido | A ID do pedido. Envio `order_id` ajudará [!DNL Pinterest] desduplique os eventos, quando necessário. |
| Número de produtos | Número total de produtos do evento. Por exemplo, o número total de itens comprados em um evento de check-out. |
| IDs de conteúdo | Lista (matriz) de IDs de produtos. |
| Conteúdo | Uma lista (matriz) de objetos que contém informações sobre produtos, como preço e quantidade. |

![O [!DNL Pinterest] [!UICONTROL Dados personalizados] destacado na ação da regra.](../../../images/extensions/server/pinterest/custom-data.png)

## Validar dados no [!DNL Pinterest]

Depois que a regra de encaminhamento de eventos for criada e executada, valide se o evento foi enviado para a [!DNL Pinterest] A API é exibida como esperado na variável [!DNL Pinterest] IU.

Se a coleção de eventos e [!DNL Experience Platform] a integração foi bem-sucedida, você verá os eventos no [!DNL Pinterest] IU.

![O [!DNL Pinterest] gerente de eventos](../../../images/extensions/server/pinterest/event-history.png)

É possível fazer drill-through e exibir a variável [!DNL Pinterest] distribuição de dados do evento.

![O [!DNL Pinterest] distribuição de dados](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Próximas etapas

Este guia abordou como instalar e configurar o [!DNL Pinterest] extensão de encaminhamento de eventos na interface do usuário do . Para obter mais informações, consulte a documentação oficial:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Visão geral da API de conversões](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
