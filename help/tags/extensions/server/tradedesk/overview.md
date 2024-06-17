---
title: Visão geral da extensão da API de conversões em tempo real do Trade Desk
description: Saiba mais sobre a extensão da API de conversões em tempo real do Trade Desk para encaminhamento de eventos no Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: d9d185685106ac160dcbefc5e9567a85c8302a73
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 2%

---

# [!DNL The Trade Desk Real-Time Conversions API] visão geral da extensão

Você pode usar o [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi) extensão para enviar dados do Edge Network Adobe Experience Platform para o [!DNL The Trade Desk] utilizando os recursos da API em seu [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) regras.

Usar [!DNL The Trade Desk Real-Time Conversions API] você pode aproveitar os recursos da API em sua [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) regras para enviar dados para [!DNL The Trade Desk] do Edge Network Adobe Experience Platform.

Leia este documento para saber como instalar a extensão e usar seus recursos em um encaminhamento de eventos [regra](../../../ui/managing-resources/rules.md).

>[!NOTE]
>
>Esta extensão e página de documentação são mantidas pela [!DNL The Trade Desk] equipe. Para quaisquer consultas ou solicitações de atualização, entre em contato diretamente com eles.

## Pré-requisitos {#prerequisites}

Você deve ter uma ID de anunciante, uma ID UPixel e uma ID do rastreador relevantes em seu [!DNL The Trade Desk] para configurar a variável [[!DNL The Trade Desk Real-Time Conversions API]](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi).

>[!INFO]
>
>Se você for um comerciante, também precisará obter sua ID do comerciante.

## Instale e configure o [!DNL The Trade Desk] API de conversões em tempo real {#install}

Para instalar a extensão, [criar uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou selecione uma propriedade existente para editar.

Selecionar **[!UICONTROL Extensões]** no painel de navegação esquerdo. No **[!UICONTROL Catálogo]** , selecione a **[!UICONTROL A Trade Desk]** Cartão da API de conversões em tempo real, selecione **[!UICONTROL Instalar]**.

![O catálogo de extensões que mostra o [!DNL The Trade Desk] placa de extensão destacando instalar.](../../../images/extensions/server/tradedesk/install-extension.png)

Na tela seguinte, digite o [!UICONTROL ID do anunciante]e, opcionalmente, um [!UICONTROL ID do comerciante]. Você pode colar as IDs diretamente nessas entradas ou pode usar um elemento de dados. Eles servirão como valores padrão usados ao fazer uma chamada de evento para [!DNL The Trade Desk] API de conversões em tempo real. Selecione **[!UICONTROL Salvar]** ao concluir.

Para saber como criar elementos de dados e disponibilizá-los para extensões na propriedade da tag, siga o [Criar elementos de dados](https://experienceleague.adobe.com/en/docs/platform-learn/data-collection/tags/create-data-elements) tutorial.

![A variável [!DNL The Trade Desk] página de configuração de extensão com o [!UICONTROL ID do anunciante] e [!UICONTROL ID do comerciante] campos realçados.](../../../images/extensions/server/tradedesk/configure-extension.png)

A extensão é instalada e agora você pode empregar seus recursos nas regras de encaminhamento de eventos.

## Configurar uma regra de encaminhamento de eventos {#rule}

Depois de instalar e configurar a extensão, você pode começar a criar regras de encaminhamento de eventos que determinam como e quando os eventos serão enviados para o [!DNL The Trade Desk].

Você deve considerar configurar várias regras para enviar todas as mensagens aceitas [propriedades da solicitação](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) via [!DNL The Trade Desk] e [!DNL The Trade Desk] API de conversões em tempo real.

>[!NOTE]
>
>Os eventos devem ser enviados em tempo real ou o mais próximo possível do tempo real.

Criar um novo encaminhamento de eventos [regra](../../../ui/managing-resources/rules.md) na propriedade de encaminhamento de eventos. Em **[!UICONTROL Ações]**, adicione uma nova ação e defina a extensão para **[!UICONTROL A Trade Desk]**. Em seguida, selecione **[!UICONTROL Conversão em tempo real]** para o **[!UICONTROL Tipo de ação]**.

![A visualização Regras de propriedade do encaminhamento de eventos, com os campos necessários para adicionar uma configuração de ação de regra de encaminhamento de eventos destacados.](../../../images/extensions/server/tradedesk/tradedesk-event-action.png)

Após a seleção, os controles adicionais aparecem para configurar ainda mais os dados do evento que serão enviados para [!DNL The Trade Desk]. Selecionar **[!UICONTROL Manter alterações]** para salvar a regra.

As opções de configuração são divididas em três seções principais, conforme descrito abaixo:

**[!UICONTROL Propriedades básicas de solicitação]**

| Entrada | Descrição |
| --- | --- |
| ID do rastreador | A ID da plataforma do rastreador de eventos. |
| ID UPixel | A ID de pixel universal do evento. |
| URL do referenciador | O URL do site de onde o evento ocorreu, se houver. |
| Nome do evento | O tipo de evento definido pela plataforma do parceiro. |
| Valor | O valor de rastreamento de receita em sequência decimal (por exemplo, &quot;19,98&quot;). |
| Moeda | Código de moeda em formato ISO. |
| IP do cliente | O endereço IP do cliente IPv4 ou IPv6. |
| ID do anúncio | A ID de anúncio exclusiva do evento. |
| Tipo de ID do anúncio | O tipo de ID de publicidade, especificado na propriedade da ID do AD: TDID, IDFA, AAID, DAID, NAID, IDL, EUID ou UID2. |
| impressão | Uma sequência de 36 caracteres (incluindo traços) que serve como o identificador exclusivo da impressão à qual o evento é atribuído. |
| ID do pedido | O identificador de pedido associado do evento. |
| td1-td10 | Dez propriedades dinâmicas personalizadas numeradas sequencialmente que podem ser usadas para fornecer metadados de conversão adicionais. |

{style="table-layout:auto"}

![A variável [!DNL Basic Request Properties] seção que mostra exemplos de entrada de dados nos campos.](../../../images/extensions/server/tradedesk/configure-extension-basic-request-properties.png)

Consulte a [!DNL The Trade Desk] para obter mais informações sobre o [propriedades da solicitação](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties) aceito por [!DNL The Trade Desk] API de conversões em tempo real.

**[!UICONTROL Parâmetros de solicitação de objeto]**

Um objeto JSON que contém mais informações. Você tem a opção de usar um conjunto reduzido de entradas de valores-chave ou fornecer JSON bruto. Além disso, você pode recuperar dados dinâmicos de um elemento de dados selecionando os discos (![Ícone de disco](../../../images/extensions/server/tradedesk/disk-icon.png)à direita.


![A variável [!DNL Object Request Parameters] mostrando os campos disponíveis.](../../../images/extensions/server/tradedesk/configure-object-request-params.png)

Consulte a [Evento de conversões em tempo real](https://partner.thetradedesk.com/v3/portal/data/doc/DataConversionEventsApi#properties-items) para obter mais informações sobre o [!UICONTROL Parâmetros de solicitação de objeto] e suas propriedades.

**[!UICONTROL Substituições de configuração]**

>[!NOTE]
>
>A variável [!UICONTROL Substituições de configuração] permitem que você defina um campo diferente [!DNL Advertiser ID] e/ou [!DNL Merchant ID] em cada regra.

| Entrada | Descrição |
| --- | --- |
| ID de anunciante | Identificador exclusivo do anunciante ao qual este evento está associado. Uma ID do anunciante diferente pode ser fornecida para substituir a ID fornecida na configuração da extensão. |
| ID do comerciante | O identificador exclusivo pelo qual cada comerciante é fornecido [!DNL The Trade Desk] durante todo o procedimento de integração. Uma ID de comerciante diferente pode ser fornecida para substituir a ID fornecida na configuração da extensão. |

![A variável [!DNL Configuration Overrides] mostrando os campos disponíveis.](../../../images/extensions/server/tradedesk/configure-overrides.png)

Quando estiver satisfeito com a regra, selecione **[!UICONTROL Salvar na biblioteca]**. Por fim, publique um novo encaminhamento de eventos [build](../../../ui/publishing/builds.md) para ativar as alterações feitas na biblioteca.

## Próximas etapas

Este guia abordou como enviar dados do evento do lado do servidor para o [!DNL The Trade Desk] usando o [!DNL The Trade Desk] Extensão da API de conversões em tempo real. A partir daqui, é recomendável expandir sua integração criando regras distintas que enviam eventos de conversão específicos, conforme aplicável por campanha. Para obter mais informações sobre os recursos de encaminhamento de eventos do [!DNL Adobe Experience Platform], leia o [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).

Consulte a [!DNL The Trade Desk] documentação sobre [práticas recomendadas para o [!DNL The Trade Desk] API de conversões em tempo real](https://www.facebook.com/business/help/308855623839366?id=818859032317965) para obter mais orientações sobre como implementar efetivamente sua integração.

Para obter detalhes sobre como depurar sua implementação usando o Depurador de Experience Platform e a ferramenta de Monitoramento de encaminhamento de eventos, leia a [visão geral do Adobe Experience Platform Debugger](../../../../debugger/home.md) e [Monitorar atividades no encaminhamento de eventos](../../../ui/event-forwarding/monitoring.md).
