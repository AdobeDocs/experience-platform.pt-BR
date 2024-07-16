---
title: Visão geral da extensão da API de conversões em tempo real do Trade Desk
description: Saiba mais sobre a extensão da API de conversões em tempo real do Trade Desk para encaminhamento de eventos no Adobe Experience Platform.
hide: true
hidefromtoc: true
exl-id: 1ff32e2b-9ff8-4395-ae44-cba75a2da515
source-git-commit: 161cb8a587026012bb07acce9da67037feb5391c
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 2%

---

# Visão geral da extensão do [!DNL The Trade Desk Real-Time Conversions API]

Você pode usar a extensão [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) para enviar dados do Edge Network Adobe Experience Platform para [!DNL The Trade Desk] utilizando os recursos da API em suas regras de [encaminhamento de eventos](../../../ui/event-forwarding/overview.md).

Usando a extensão [!DNL The Trade Desk Real-Time Conversions API], você pode aproveitar os recursos da API em suas regras de [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) para enviar dados para [!DNL The Trade Desk] do Edge Network Adobe Experience Platform.

Leia este documento para saber como instalar a extensão e usar seus recursos em uma [regra](../../../ui/managing-resources/rules.md) de encaminhamento de eventos.

>[!NOTE]
>
>Esta extensão e página de documentação são mantidas pela equipe do [!DNL The Trade Desk]. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente com eles.

## Pré-requisitos {#prerequisites}

Você deve ter uma ID de Anunciante, uma ID de UPixel e uma ID de Rastreador relevantes na sua conta do [!DNL The Trade Desk] para configurar o [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>Se você for um comerciante, também precisará obter sua ID do comerciante.

## Instalar e configurar a API de Conversões em Tempo Real do [!DNL The Trade Desk] {#install}

Para instalar a extensão, [crie uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou selecione uma propriedade existente para editar.

Selecione **[!UICONTROL Extensões]** na navegação à esquerda. Na guia **[!UICONTROL Catálogo]**, selecione o cartão de API **[!UICONTROL A Trade Desk]** de Conversões em Tempo Real, depois selecione **[!UICONTROL Instalar]**.

![O catálogo de extensões que mostra a instalação do destaque do cartão de extensão [!DNL The Trade Desk].](../../../images/extensions/server/tradedesk/install-extension.png)

Na próxima tela, insira a [!UICONTROL ID do anunciante] e, opcionalmente, uma [!UICONTROL ID do comerciante]. Você pode colar as IDs diretamente nessas entradas ou pode usar um elemento de dados. Eles servirão como valores padrão usados ao fazer uma chamada de evento para a API de conversões em tempo real [!DNL The Trade Desk]. Selecione **[!UICONTROL Salvar]** ao concluir.

Para saber como criar elementos de dados e disponibilizá-los para extensões na propriedade da tag, siga o tutorial [Criar elementos de dados](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements).

![A página de configuração de extensão [!DNL The Trade Desk] com os campos [!UICONTROL ID de Anunciante] e [!UICONTROL ID de Comerciante] destacados.](../../../images/extensions/server/tradedesk/configure-extension.png)

A extensão é instalada e agora você pode empregar seus recursos nas regras de encaminhamento de eventos.

## Configurar uma regra de encaminhamento de eventos {#rule}

Depois de instalar e configurar a extensão, você pode começar a criar regras de encaminhamento de eventos que determinam como e quando seus eventos serão enviados para [!DNL The Trade Desk].

Você deve considerar a configuração de várias regras para enviar todas as [propriedades de solicitação](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) aceitas via [!DNL The Trade Desk] e API de Conversões em Tempo Real [!DNL The Trade Desk].

>[!NOTE]
>
>Os eventos devem ser enviados em tempo real ou o mais próximo possível do tempo real.

Crie uma nova [regra](../../../ui/managing-resources/rules.md) de encaminhamento de eventos na propriedade de encaminhamento de eventos. Em **[!UICONTROL Ações]**, adicione uma nova ação e defina a extensão como **[!UICONTROL A Trade Desk]**. Em seguida, selecione **[!UICONTROL Conversão em Tempo Real]** para o **[!UICONTROL Tipo de Ação]**.

![A exibição de Regras de Propriedade de Encaminhamento de Eventos, com os campos necessários para adicionar uma configuração de ação de regra de encaminhamento de eventos realçada.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Após a seleção, controles adicionais aparecem para configurar ainda mais os dados do evento que serão enviados para [!DNL The Trade Desk]. Selecione **[!UICONTROL Manter alterações]** para salvar a regra.

As opções de configuração são divididas em três seções principais, conforme descrito abaixo:

**[!UICONTROL Propriedades básicas da solicitação]**

| Entrada | Descrição |
| --- | --- |
| ID do rastreador | A ID da plataforma do rastreador de eventos. |
| ID UPixel | A ID de pixel universal do evento. |
| URL do referenciador | O URL do site de onde o evento ocorreu, se houver. |
| Nome do evento | O tipo de evento definido pela plataforma do parceiro. |
| Valor | O valor de rastreamento de receita em sequência decimal (por exemplo, &quot;19,98&quot;). |
| Currency | Código de moeda em formato ISO. |
| IP do cliente | O endereço IP do cliente IPv4 ou IPv6. |
| ID do anúncio | A ID de anúncio exclusiva do evento. |
| Tipo de ID do anúncio | O tipo de ID de publicidade, especificado na propriedade da ID do AD: TDID, IDFA, AAID, DAID, NAID, IDL, EUID ou UID2. |
| impressão | Uma sequência de 36 caracteres (incluindo traços) que serve como o identificador exclusivo da impressão à qual o evento é atribuído. |
| ID do pedido | O identificador de pedido associado do evento. |
| td1-td10 | Dez propriedades dinâmicas personalizadas numeradas sequencialmente que podem ser usadas para fornecer metadados de conversão adicionais. |

{style="table-layout:auto"}

![A seção [!DNL Basic Request Properties] que mostra exemplos de entrada de dados nos campos.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Consulte a documentação do desenvolvedor [!DNL The Trade Desk] para obter mais informações sobre as [propriedades de solicitação](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) aceitas pela API de Conversões em Tempo Real do [!DNL The Trade Desk].

**[!UICONTROL Parâmetros de Solicitação de Objetos]**

Um objeto JSON que contém mais informações. Você tem a opção de usar um conjunto reduzido de entradas de valores-chave ou fornecer JSON bruto. Além disso, você pode recuperar dados dinâmicos de um elemento de dados selecionando os discos (![Ícone de Disco](../../../images/extensions/server/tradedesk/disk-icon.png)) à direita.


![A seção [!DNL Object Request Parameters] mostrando os campos disponíveis.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Consulte a documentação do [Evento de conversões em tempo real](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) para obter mais informações sobre os [!UICONTROL Parâmetros de solicitação de objeto] e suas propriedades.

**[!UICONTROL Substituições de configuração]**

>[!NOTE]
>
>Os campos [!UICONTROL Substituições de Configuração] permitem que você defina um [!DNL Advertiser ID] e/ou [!DNL Merchant ID] diferente em cada regra.

| Entrada | Descrição |
| --- | --- |
| ID de anunciante | Identificador exclusivo do anunciante ao qual este evento está associado. Uma ID do anunciante diferente pode ser fornecida para substituir a ID fornecida na configuração da extensão. |
| ID do comerciante | O identificador exclusivo que cada comerciante é fornecido por [!DNL The Trade Desk] durante todo o procedimento de integração. Uma ID de comerciante diferente pode ser fornecida para substituir a ID fornecida na configuração da extensão. |

![A seção [!DNL Configuration Overrides] mostrando os campos disponíveis.](../../../images/extensions/server/tradedesk/configure-overrides.png)

Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**. Finalmente, publique um novo encaminhamento de eventos [build](../../../ui/publishing/builds.md) para habilitar as alterações feitas na biblioteca.

## Próximas etapas

Este guia aborda como enviar dados do evento do lado do servidor para o [!DNL The Trade Desk] usando a extensão de API de Conversões em Tempo Real do [!DNL The Trade Desk]. A partir daqui, é recomendável expandir sua integração criando regras distintas que enviam eventos de conversão específicos, conforme aplicável por campanha. Para obter mais informações sobre os recursos de encaminhamento de eventos do [!DNL Adobe Experience Platform], leia a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).

Consulte a documentação do [!DNL The Trade Desk] sobre [práticas recomendadas da [!DNL The Trade Desk] API de conversões em tempo real](https://www.facebook.com/business/help/308855623839366?id=818859032317965) para obter mais orientações sobre como implementar efetivamente sua integração.

Para obter detalhes sobre como depurar sua implementação usando o Depurador de Experience Platform e a ferramenta de Monitoramento de Encaminhamento de Eventos, leia a [Visão geral de Adobe Experience Platform Debugger](../../../../debugger/home.md) e [Monitorar atividades no encaminhamento de eventos](../../../ui/event-forwarding/monitoring.md).
