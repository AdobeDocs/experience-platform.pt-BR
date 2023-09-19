---
keywords: extensão de encaminhamento de eventos;extensão de encaminhamento de eventos do pinterest;pinterest
title: Extensão de encaminhamento de eventos do pinterest
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform permite assimilar eventos no Pinterest para atender aos requisitos da empresa.
last-substantial-update: 2023-04-27T00:00:00Z
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1548'
ht-degree: 5%

---

# Extensão de encaminhamento de eventos da [!DNL Pinterest]

[!DNL Pinterest] O é um mecanismo de descoberta visual para encontrar ideias como receitas, decoração de casas, inspiração de estilo e muito mais. Há bilhões de pinos em [!DNL Pinterest], que também podem ser compartilhadas com outras pessoas no [!DNL Pinterest]. É possível agrupar os eventos de interação do usuário e aproveitar [!DNL Pinterest Analytics] para entender o comportamento do usuário e executar anúncios direcionados.

A variável [[!DNL Pinterest] Conversões](https://developers.pinterest.com/docs/conversions/conversion-management/) API [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) permite que você aproveite os dados capturados na Rede de borda da Adobe Experience Platform e os envie para [!DNL Pinterest]. Este documento aborda os casos de uso da extensão, como instalá-la e como integrar seus recursos ao encaminhamento de eventos [regras](../../../ui/managing-resources/rules.md).

Os tokens de acesso de conversões são o método de autenticação usado pelo [!DNL Pinterest] ao interagir com o [!DNL Pinterest] API.

## Casos de uso

Essa extensão deve ser usada se você quiser usar dados da Rede de borda no [!DNL Pinterest] para aproveitar os recursos de análise do cliente.

Por exemplo, considere uma equipe de marketing em uma organização. A equipe captura os dados do evento de interação do usuário do site e os carrega em [!DNL Pinterest] usar esta extensão de encaminhamento de eventos.

As equipes de marketing e análise podem aproveitar [!DNL Pinterest] Recursos do Analytics para entender as principais interações e comportamento do usuário, permitindo que você entenda melhor os usuários e os direcione para campanhas de anúncios direcionadas.

Para obter mais informações sobre casos de uso específicos do [!DNL Pinterest], consulte o [[!DNL Pinterest] casos de uso](https://business.pinterest.com/en/success-stories) documentação.

## [!DNL Pinterest] pré-requisitos {#prerequisites}

Você deve ter um válido [!DNL Pinterest] [conta comercial](https://help.pinterest.com/en/business/article/get-a-business-account) para usar essa extensão. Vá para a [[!DNL Pinterest] página de registro](https://www.pinterest.com/business/create/) para registrar e criar uma conta se ainda não tiver uma.

Você também precisará de um [!DNL Pinterest] conta de desenvolvedor, que precisará ser associada à [!DNL Pinterest] conta comercial. Para associar a conta de desenvolvedor à conta comercial, consulte o [[!DNL Pinterest ] conta do desenvolvedor](https://developers.pinterest.com/account-setup/).

### Coletar detalhes de configuração necessários {#configuration-details}

Para conectar o Experience Platform a [!DNL Pinterest], as seguintes entradas são necessárias:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| ID da conta de anúncios | Seu [!DNL Pinterest] ID da conta do Ads. Consulte a [[!DNL Pinterest] documentação](https://help.pinterest.com/en/business/article/find-ids-in-ads-manager) para obter orientação. | 123456789012 |
| Token de acesso de conversão | Seu [!DNL Pinterest] Token de acesso de conversão. Consulte a [[!DNL Pinterest] API de conversões](https://developers.pinterest.com/docs/conversions/conversions/#Get%20the%20conversion%20token) documento de orientação. <br> **Você só precisará fazer isso uma vez, pois esse token não expira.** | {YOUR_PINTEREST_BEARER_TOKEN} |

## Instale e configure o [!DNL Pinterest] extensão {#install}

Para instalar a extensão, [criar uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Na navegação à esquerda, selecione **[!UICONTROL Extensões]**. Selecionar **[!UICONTROL Instalar]** no cartão para o [!DNL Pinterest] extensão no **[!UICONTROL Catálogo]** guia.

![Catálogo que exibe o [!DNL Pinterest] extensão com [!UICONTROL Instalar] destacado.](../../../images/extensions/server/pinterest/install.png)

### Configurar a extensão [!DNL Pinterest]

>[!IMPORTANT]
>
>Dependendo das suas necessidades de implementação, talvez seja necessário criar um esquema, elementos de dados e um conjunto de dados antes de configurar a extensão. Revise todas as etapas de configuração antes de começar para determinar quais entidades você precisa configurar para seu caso de uso.

Na navegação à esquerda, selecione **[!UICONTROL Extensões]**. Selecionar **[!UICONTROL Configurar]** no cartão para o [!DNL Pinterest] extensão no [!UICONTROL Instalado]**.

![[!DNL Pinterest] extensão mostrada no [!UICONTROL Instalar] guia com [!UICONTROL Configurar] destacado.](../../../images/extensions/server/pinterest/configure.png)

Na próxima tela, insira o [!UICONTROL ID da conta de anúncios] e [!UICONTROL Token de acesso de conversão] que você reuniu anteriormente na [detalhes da configuração](#configuration-details) seção. Quando terminar, selecione **[!UICONTROL Salvar]**.

![A variável [!DNL Pinterest] [!UICONTROL Configurar] tela destacando o [!UICONTROL ID da conta de anúncios] e [!UICONTROL Token de acesso de conversão] campos de entrada.](../../../images/extensions/server/pinterest/input.png)

## Configurar uma regra de encaminhamento de eventos {#config-rule}

Depois que todos os elementos de dados forem configurados, você poderá começar a criar regras de encaminhamento de eventos que determinam quando e como seus eventos serão enviados para o [!DNL Pinterest].

Criar um novo [regra](../../../ui/managing-resources/rules.md) na propriedade de encaminhamento de eventos. Em **[!UICONTROL Ações]**, adicione uma nova ação e defina a extensão para **[!UICONTROL Pinterest]**. Para enviar eventos da Rede de borda para o [!DNL Pinterest], defina o **[!UICONTROL Tipo de ação]** para **[!UICONTROL Enviar evento].**

![A variável [!DNL Pinterest] [!UICONTROL Enviar evento] criação da regra.](../../../images/extensions/server/pinterest/rule.png)

Após a seleção, controles adicionais são exibidos para configurar ainda mais o evento. Você precisa mapear o [!DNL Pinterest] para os elementos de dados criados anteriormente.

### [!UICONTROL Dados do evento]

Os seguintes dados de evento serão necessários para criar a nova regra:

| Nome do campo | Descrição | Exemplo |
| --- | --- | --- | 
| [!UICONTROL Nome do evento] | O tipo de evento do usuário. No entanto, isso pode ser qualquer tipo de evento para aproveitar [!DNL Pinterest Analytics] é recomendável usar [[!DNL Pinterest] códigos de evento](https://help.pinterest.com/en/business/article/add-event-codes) | * check-out <br> * add_to_cart <br> * page_visit <br> * inscrição <br> * [Evento definido pelo usuário] |
| [!UICONTROL Origem da ação] | A origem que indica onde o evento de conversão ocorreu. | * app_android <br> * app_ios <br> * web <br> * offline |
| [!UICONTROL Hora do Evento] | Refere-se à hora do evento. O formato de hora padrão usado é UNIX, no formato `<seconds>.<miliseconds>` dependendo do fuso horário local. Para obter mais informações, consulte [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/#operation/events/create). | 1433188255.500 indica 1433188255 segundos e 500 milissegundos após a época ou segunda-feira, 1 de junho de 2015, às 7:50:17H GMT. |
| [!UICONTROL ID de evento] | Uma sequência de ID exclusiva que identifica esse evento e pode ser usada para desduplicação entre eventos assimilados por meio da API de conversão e do rastreamento do Pinterest. Sem isso, os dados do evento provavelmente serão contados duas vezes e relatarão a inflação de métrica. | ba7816bf8f01cfea414140de5dae2223b00361a396177a9cb410ff61f20015ad |
| [!UICONTROL Propriedades do evento] | Um objeto JSON que contém propriedades personalizadas do evento. Escolha entre fornecer JSON bruto ou usar um conjunto simplificado de entradas de valores-chave. | { &quot;event_source_url&quot;: &quot;http://site.com&quot; } |

![A variável [!DNL Pinterest] [!UICONTROL Dados do evento] destacado na ação regra.](../../../images/extensions/server/pinterest/event-data.png)

As seguintes propriedades de evento podem ser configuradas:

| Nome do campo | Descrição |
| --- | --- |
| URL de origem do evento | URL do evento de conversão da Web. |
| ID da loja de aplicativos | A ID do aplicativo da app store. |
| Nome do aplicativo | O nome do aplicativo  |
| Application Version | A versão do aplicativo. |
| Marca do dispositivo | Marca do dispositivo sendo usado pelo usuário. |
| Operadora do dispositivo | Operadora de celular do usuário para o dispositivo. |
| Modelo do dispositivo | Modelo do dispositivo do usuário. |
| Device Type | Tipo de dispositivo sendo usado pelo usuário. |
| Versão do SO | Versão do sistema operacional do dispositivo. |
| Idioma do usuário | Código de idioma ISO-639-1 de dois caracteres indicando o idioma do usuário. |

### [!UICONTROL Dados do usuário]

Os seguintes dados do usuário podem ser inseridos por não são campos obrigatórios:

| Nome do campo | Descrição | Exemplo |
| --- | --- | --- | 
| [!UICONTROL Email] | Endereço de email do usuário ou um hash SHA256 do email do endereço do usuário. | ebd543592.f2b7e1 |
| [!UICONTROL IDs de anúncios móveis] | Hashes Sha256 das &quot;IDs de publicidade da Google&quot; (GAIDs) ou do &quot;Identificador da Apple para anunciantes&quot; (IDFAs) do usuário | ebd543592.f2b7e1 |
| [!UICONTROL Endereço IP do cliente] | O endereço IP do usuário, que pode estar no formato IPv4 ou IPv6. Usado para correspondência. | 192.168.0.1 |
| [!UICONTROL Agente de usuário cliente] | A sequência de agente do usuário do navegador da Web do usuário. | Mozilla/5.0 (platform; rv:geckoversion) Gecko/geckotrail Firefox/firefoxversion |
| [!UICONTROL Dados de informações do cliente] | Um objeto JSON que contém outras informações do cliente. Escolha entre fornecer JSON bruto ou usar um conjunto simplificado de entradas de valores-chave. | { &quot;ph&quot;: &quot;122333445&quot; } |

![A variável [!DNL Pinterest] [!UICONTROL Dados do usuário] destacado na ação regra.](../../../images/extensions/server/pinterest/user-data.png)

As propriedades de informações do cliente que podem ser configuradas são:

| Nome do campo | Descrição |
| --- | --- |
| Telefone | Número de contato do usuário. Somente dígitos são aceitos e devem ser inseridos com código do país, código de área e número. |
| Gênero | O gênero pode ser inserido como &quot;f&quot; para feminino, &quot;m&quot; para masculino ou &quot;n&quot; para não binário. |
| Data de nascimento | Data de nascimento, inserida como ano, mês e dia. |
| Sobrenome | Sobrenome do usuário. |
| Primeiro nome | Nome do usuário. |
| Cidade | Cidade de residência do usuário. Isso é usado principalmente para fins de faturamento. |
| Estado | Estado do usuário, que é fornecido como um código de duas letras em minúsculas. |
| Código postal | Código postal do usuário, usado principalmente para fins de faturamento. |
| País | Código de país ISO-3166 de dois caracteres indicando o país do usuário. |
| ID externa | Identificador exclusivo do anunciante que identifica um usuário em seu espaço. Por exemplo, id de usuário, id de fidelidade e assim por diante. |
| ID do clique | O identificador exclusivo armazenado no cookie _epik no seu domínio ou no parâmetro de consulta &amp;epik= no URL. |

>[!IMPORTANT]
>
>Antes de enviar os dados para o [!DNL Pinterest] No endpoint da API, a extensão aplicará hash e normalizará os valores dos seguintes campos: Email, Número de telefone, Nome, Sobrenome, Gênero, Data de nascimento, Cidade, Estado, CEP, País e ID externa. A extensão não aplicará hash ao valor desses campos se uma string SHA256 já estiver presente.

### [!UICONTROL Dados personalizados]

Os seguintes dados personalizados podem ser inseridos para a regra:

| Nome do campo | Descrição |
| --- | --- |
| Moeda | O código de moeda ISO-4217. Se isso não for fornecido, [!DNL Pinterest] assumirá como padrão a moeda do anunciante que foi definida durante a criação da conta. |
| Valor | Valor total do evento. Aceito como uma cadeia de caracteres na solicitação. Isso será analisado em um dígito duplo. |
| Pesquisar string | A sequência de pesquisa relacionada ao evento de conversão do usuário. |
| ID do pedido | A ID do pedido. Enviando `order_id` ajudará [!DNL Pinterest] elimine a duplicação de eventos quando necessário. |
| Número de produtos | Número total de produtos do evento. Por exemplo, o número total de itens comprados em um evento de check-out. |
| IDs de conteúdo | Lista (matriz) de IDs de produtos. |
| Conteúdo | Uma lista (matriz) de objetos que contém informações sobre produtos, como preço e quantidade. |

![A variável [!DNL Pinterest] [!UICONTROL Dados personalizados] destacado na ação regra.](../../../images/extensions/server/pinterest/custom-data.png)

## Validar dados no [!DNL Pinterest]

Depois que a regra de encaminhamento de eventos tiver sido criada e executada, valide se o evento enviado para o [!DNL Pinterest] A API é exibida conforme esperado no [!DNL Pinterest] IU.

Se a coleção de eventos e a [!DNL Experience Platform] integração foram bem-sucedidas, você verá eventos no [!DNL Pinterest] IU.

![A variável [!DNL Pinterest] gerenciador de eventos](../../../images/extensions/server/pinterest/event-history.png)

É possível fazer drill-through e exibir a [!DNL Pinterest] distribuição de dados do evento.

![A variável [!DNL Pinterest] distribuição de dados](../../../images/extensions/server/pinterest/event-history-distribution.png)

## Próximas etapas

Este guia abordou como instalar e configurar o [!DNL Pinterest] extensão de encaminhamento de eventos na interface do. Para obter mais informações, consulte a documentação oficial:

* [[!DNL Pinterest] API](https://developers.pinterest.com/docs/api/v5/)
* [[!DNL Pinterest] Visão geral da API de conversões](https://help.pinterest.com/en/business/article/the-pinterest-api-for-conversions)
