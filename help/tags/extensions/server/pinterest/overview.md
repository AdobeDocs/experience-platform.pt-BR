---
keywords: extensão de encaminhamento de eventos;pinterest;extensão de encaminhamento de eventos pinterest
title: Extensão de encaminhamento de eventos do Pinterest
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform permite assimilar eventos no Pinterest para atender aos requisitos da empresa.
last-substantial-update: 2023-04-27T00:00:00Z
exl-id: 44f38a9b-0a28-4b51-bead-ee460eb8405e
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1427'
ht-degree: 3%

---

# Extensão de encaminhamento de eventos da [!DNL Pinterest]

O [!DNL Pinterest] é um mecanismo de descoberta visual para encontrar ideias como receitas, decoração da casa, inspiração de estilo e muito mais. Há bilhões de pins no [!DNL Pinterest], que também podem ser compartilhados com outras pessoas no [!DNL Pinterest]. Você pode agrupar os eventos de interação do usuário e aproveitar o [!DNL Pinterest Analytics] para entender o comportamento do usuário e executar anúncios direcionados.

A extensão [[!DNL Pinterest] Conversões](https://developers.pinterest.com/docs/conversions/conversion-management/) do [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) da API permite que você aproveite os dados capturados no Adobe Experience Platform Edge Network e os envie para [!DNL Pinterest]. Este documento aborda os casos de uso da extensão, como instalá-la e como integrar seus recursos ao encaminhamento de eventos [regras](../../../ui/managing-resources/rules.md).

Os tokens de acesso de conversões são o método de autenticação usado por [!DNL Pinterest] ao interagir com a API [!DNL Pinterest].

## Casos de uso

Essa extensão deve ser usada se você quiser usar dados da Edge Network no [!DNL Pinterest] para aproveitar seus recursos de análise do cliente.

Por exemplo, considere uma equipe de marketing em uma organização. A equipe captura dados do evento de interação do usuário de seu site e os carrega no [!DNL Pinterest] usando esta extensão de encaminhamento de eventos.

As equipes de marketing e análise podem aproveitar os recursos do Analytics [!DNL Pinterest] para entender as principais interações e comportamento dos usuários, permitindo que você entenda melhor os usuários e os direcione para campanhas de anúncios direcionadas.

Para obter mais informações sobre casos de uso específicos do [!DNL Pinterest], consulte a documentação dos [[!DNL Pinterest] casos de uso](https://business.pinterest.com/en/success-stories).

## [!DNL Pinterest] pré-requisitos {#prerequisites}

Você deve ter uma [!DNL Pinterest] [conta comercial](https://help.pinterest.com/en/business/article/get-a-business-account) válida para usar esta extensão. Vá para a [[!DNL Pinterest] página de registro](https://www.pinterest.com/business/create/) para se registrar e criar uma conta, caso ainda não tenha uma.

Você também precisará de uma conta de desenvolvedor [!DNL Pinterest], que precisará ser associada à sua conta comercial [!DNL Pinterest]. Para associar a conta de desenvolvedor à conta comercial, consulte a [[!DNL Pinterest ] conta de desenvolvedor](https://developers.pinterest.com/account-setup/).

### Coletar detalhes de configuração necessários {#configuration-details}

Para conectar o Experience Platform a [!DNL Pinterest], as seguintes entradas são necessárias:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| ID da conta de anúncios | A Id Da Conta Do [!DNL Pinterest] Ads. Consulte a [[!DNL Pinterest] documentação](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) para obter orientação. | 123456789012 |
| Token de acesso de conversão | Seu Token De Acesso De Conversão Do [!DNL Pinterest]. Consulte o documento [[!DNL Pinterest] API de conversões](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) para obter orientação. <br> **Você só precisará fazer isso uma vez, pois esse token não expira.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Instalar e configurar a extensão [!DNL Pinterest] {#install}

Para instalar a extensão, [crie uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Na navegação à esquerda, selecione **[!UICONTROL Extensions]**. Selecione **[!UICONTROL Install]** no cartão para a extensão [!DNL Pinterest] na guia **[!UICONTROL Catalog]**.

![Catálogo exibindo a extensão [!DNL Pinterest] com [!UICONTROL Install] realçado.](../../../images/extensions/server/pinterest/install.png)

### Configurar a extensão [!DNL Pinterest]

>[!IMPORTANT]
>
>Dependendo das suas necessidades de implementação, talvez seja necessário criar um esquema, elementos de dados e um conjunto de dados antes de configurar a extensão. Revise todas as etapas de configuração antes de começar para determinar quais entidades você precisa configurar para seu caso de uso.

Na navegação à esquerda, selecione **[!UICONTROL Extensions]**. Selecione **[!UICONTROL Configure]** no cartão para a extensão [!DNL Pinterest] na guia [!UICONTROL Installed]**.

Extensão ![[!DNL Pinterest] mostrada na guia [!UICONTROL Install] com [!UICONTROL Configure] realçada.](../../../images/extensions/server/pinterest/configure.png)

Na próxima tela, insira os [!UICONTROL Ads Account Id] e [!UICONTROL Conversion Access Token] coletados anteriormente na seção [detalhes de configuração](#configuration-details). Quando terminar, selecione **[!UICONTROL Save]**.

![A tela [!DNL Pinterest] [!UICONTROL Configure] destacando os campos de entrada [!UICONTROL Ads Account Id] e [!UICONTROL Conversion Access Token].](../../../images/extensions/server/pinterest/input.png)

## Configurar uma regra de encaminhamento de eventos {#config-rule}

Depois que todos os seus elementos de dados estiverem configurados, você poderá começar a criar regras de encaminhamento de eventos que determinam quando e como seus eventos serão enviados para [!DNL Pinterest].

Crie uma nova [regra](../../../ui/managing-resources/rules.md) na propriedade de encaminhamento de eventos. Em **[!UICONTROL Actions]**, adicione uma nova ação e defina a extensão como **[!UICONTROL Pinterest]**. Para enviar eventos do Edge Network para [!DNL Pinterest], defina **[!UICONTROL Action Type]** como **[!UICONTROL Send Event].**

![A [!DNL Pinterest] [!UICONTROL Send Event] criação de regra.](../../../images/extensions/server/pinterest/rule.png)

Após a seleção, controles adicionais são exibidos para configurar ainda mais o evento. Você precisa mapear as propriedades de evento [!DNL Pinterest] para os elementos de dados criados anteriormente.

### [!UICONTROL Event Data]

Os seguintes dados de evento serão necessários para criar a nova regra:

| Nome do campo | Descrição | Exemplo |
| --- | --- | --- | 
| [!UICONTROL Event Name] | O tipo de evento do usuário. Isso pode ser qualquer tipo de evento. No entanto, para aproveitar [!DNL Pinterest Analytics], é recomendável usar [[!DNL Pinterest] códigos de evento](https://help.pinterest.com/en/business/article/add-event-codes) | &amp;ast; check-out <br> &amp;ast; add_to_cart <br> &amp;ast; visita_página <br> &amp;ast; inscrição <br> &amp;ast; [Evento definido pelo usuário] |
| [!UICONTROL Action Source] | A origem que indica onde o evento de conversão ocorreu. | &amp;ast; app_android <br> &amp;ast; app_ios <br> &amp;ast; web <br> &amp;ast; offline |
| [!UICONTROL Event Time] | Refere-se à hora do evento. O formato de hora padrão usado é UNIX, no formato `<seconds>.<miliseconds>`, dependendo do fuso horário local. Para obter mais informações, consulte a [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 indica 1433188255 segundos e 500 milissegundos após a época, ou segunda-feira, 1 de junho de 2015, às 19h55 GMT.:50: |
| [!UICONTROL Event ID] | Uma sequência de ID exclusiva que identifica esse evento e pode ser usada para desduplicação entre eventos assimilados por meio da API de conversão e do rastreamento do Pinterest. Sem isso, os dados do evento provavelmente serão contados duas vezes e relatarão a inflação de métrica. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Event Properties] | Um objeto JSON que contém propriedades personalizadas do evento. Escolha entre fornecer JSON bruto ou usar um conjunto simplificado de entradas de valores-chave. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![O [!DNL Pinterest] [!UICONTROL Event Data] realçado na ação de regra.](../../../images/extensions/server/pinterest/event-data.png)

As seguintes propriedades de evento podem ser configuradas:

| Nome do campo | Descrição |
| --- | --- |
| URL do Source do evento | URL do evento de conversão da Web. |
| ID da loja de aplicativos | A ID do aplicativo da app store. |
| Nome do aplicativo | O nome do aplicativo. |
| Application Version | A versão do aplicativo. |
| Marca do dispositivo | Marca do dispositivo sendo usado pelo usuário. |
| Operadora do dispositivo | Operadora de celular do usuário para o dispositivo. |
| Modelo do dispositivo | Modelo do dispositivo do usuário. |
| Device Type | Tipo de dispositivo sendo usado pelo usuário. |
| Versão do SO | Versão do sistema operacional do dispositivo. |
| Idioma do usuário | Código de idioma ISO-639-1 de dois caracteres indicando o idioma do usuário. |

### [!UICONTROL User Data]

Os seguintes dados do usuário podem ser inseridos por não são campos obrigatórios:

| Nome do campo | Descrição | Exemplo |
| --- | --- | --- | 
| [!UICONTROL Email] | Endereço de email do usuário ou um hash SHA256 do email do endereço do usuário. | ebd543592.f2b7e1 |
| [!UICONTROL Mobile Adverstising IDs] | Hashes Sha256 das &quot;IDs do Google Advertising&quot; (GAIDs) ou do &quot;Identificador da Apple para anunciantes&quot; (IDFAs) do usuário | ebd543592.f2b7e1 |
| [!UICONTROL Client IP Address] | O endereço IP do usuário, que pode estar no formato IPv4 ou IPv6. Usado para correspondência. | 192.168.0.1 |
| [!UICONTROL Client User Agent] | A sequência de agente do usuário do navegador da Web do usuário. | Mozilla/5.0 (platform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Customer information data] | Um objeto JSON que contém outras informações do cliente. Escolha entre fornecer JSON bruto ou usar um conjunto simplificado de entradas de valores-chave. | { &quot;ph&quot;: &quot;122333445&quot; } |

![O [!DNL Pinterest] [!UICONTROL User Data] realçado na ação de regra.](../../../images/extensions/server/pinterest/user-data.png)

As propriedades de informações do cliente que podem ser configuradas são:

| Nome do campo | Descrição |
| --- | --- |
| Telefone | Número de contato do usuário. Somente dígitos são aceitos e devem ser inseridos com código do país, código de área e número. |
| Gênero | O gênero pode ser inserido como &quot;f&quot; para feminino, &quot;m&quot; para masculino ou &quot;n&quot; para não binário. |
| Data de nascimento | Data de nascimento, inserida como ano, mês e dia. |
| Sobrenome | Sobrenome do usuário. |
| Nome | Nome do usuário. |
| Cidade | Cidade de residência do usuário. Isso é usado principalmente para fins de faturamento. |
| Estado | Estado do usuário, que é fornecido como um código de duas letras em minúsculas. |
| Código postal | Código postal do usuário, usado principalmente para fins de faturamento. |
| País | Código de país ISO-3166 de dois caracteres indicando o país do usuário. |
| ID externa | Identificador exclusivo do anunciante que identifica um usuário em seu espaço. Por exemplo, id de usuário, id de fidelidade e assim por diante. |
| ID do clique | O identificador exclusivo armazenado no cookie _epik no seu domínio ou no parâmetro de consulta &amp;epik= no URL. |

>[!IMPORTANT]
>
>Antes de enviar os dados para o ponto de extremidade da API [!DNL Pinterest], a extensão aplicará hash e normalizará os valores dos seguintes campos: Email, Número de Telefone, Nome, Sobrenome, Gênero, Data de Nascimento, Cidade, Estado, CEP, País e ID Externa. A extensão não aplicará hash ao valor desses campos se uma string SHA256 já estiver presente.

### [!UICONTROL Custom Data]

Os seguintes dados personalizados podem ser inseridos para a regra:

| Nome do campo | Descrição |
| --- | --- |
| Currency | O código de moeda ISO-4217. Se isso não for fornecido, [!DNL Pinterest] assumirá como padrão a moeda do anunciante que foi definida durante a criação da conta. |
| Valor | Valor total do evento. Aceito como uma cadeia de caracteres na solicitação. Isso será analisado em um dígito duplo. |
| Pesquisar string | A sequência de pesquisa relacionada ao evento de conversão do usuário. |
| ID do pedido | A ID do pedido. O envio de `order_id` ajudará [!DNL Pinterest] a desduplicar eventos quando necessário. |
| Número de produtos | Número total de produtos do evento. Por exemplo, o número total de itens comprados em um evento de check-out. |
| IDs de conteúdo | Lista (matriz) de IDs de produtos. |
| Conteúdo | Uma lista (matriz) de objetos que contém informações sobre produtos, como preço e quantidade. |

![O [!DNL Pinterest] [!UICONTROL Custom Data] realçado na ação de regra.](../../../images/extensions/server/pinterest/custom-data.png)

## Validar dados em [!DNL Pinterest]

Depois que a regra de encaminhamento de eventos for criada e executada, valide se o evento enviado para a API [!DNL Pinterest] é exibido conforme esperado na interface do usuário [!DNL Pinterest].

Se a coleção de eventos e a integração do [!DNL Experience Platform] tiverem sido bem-sucedidas, você verá eventos na interface do usuário do [!DNL Pinterest].

![O [!DNL Pinterest] gerenciador de eventos](../../../images/extensions/server/pinterest/event-history.png)

Você pode detalhar e visualizar a distribuição de dados do evento [!DNL Pinterest].

![A [!DNL Pinterest] distribuição de dados](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Próximas etapas

Este guia abordou como instalar e configurar a extensão de encaminhamento de eventos do [!DNL Pinterest] na interface do usuário. Para obter mais informações, consulte a documentação oficial:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Visão geral da API de conversões](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
