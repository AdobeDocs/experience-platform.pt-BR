---
title: Integração da extensão de API de eventos da Web do Adobe TikTok
description: Essa API de eventos da Web do Adobe Experience Platform permite compartilhar interações do site diretamente com o TikTok.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '1044'
ht-degree: 2%

---

# Visão geral da extensão de API de eventos da Web do [!DNL TikTok]

A API de eventos do [!DNL TikTok] é uma interface segura da [API do Edge Network](https://developer.adobe.com/data-collection-apis/docs/) que permite compartilhar informações com o [!DNL TikTok] diretamente sobre as ações do usuário em seus sites. Você pode aproveitar as regras de encaminhamento de eventos para enviar dados de [!DNL Adobe Experience Platform Edge Network] para [!DNL TikTok] usando a extensão de API de Eventos da Web [!DNL TikTok].

## [!DNL TikTok] pré-requisitos {#prerequisites}

Para configurar a API de eventos da Web do [!DNL TikTok] para usar a API de eventos do [!DNL TikTok], é necessário gerar um código de pixel e token de acesso [!DNL TikTok].

Você deve ter um [!DNL TikTok] válido para a conta comercial para criar um pixel de [!DNL TikTok] usando a configuração do parceiro. Vá para a [[!DNL TikTok] página de registro comercial](https://www.tiktok.com/business/en-US/solutions/business-account) para se registrar e criar uma conta, caso ainda não tenha uma.

Você precisa estar conectado à sua conta comercial para configurar o Pixel do [!DNL TikTok] usando a configuração de parceiro. Para fazer isso, siga as etapas abaixo:

1. Navegue até a guia **[!UICONTROL Assets]** e selecione **[!UICONTROL Event]**.
2. Em Eventos da Web, selecione **[!UICONTROL Manage]**.
3. Selecione **[!UICONTROL Set Up Web Events]**.
4. Selecione **[!UICONTROL Partner Setup]** como seu método de conexão.

Consulte o guia [Introdução ao Pixel](https://ads.tiktok.com/help/article/get-started-pixel) para obter mais informações sobre como configurar o pixel [!DNL TikTok].

Você pode gerar um token de acesso depois que o pixel for criado com êxito. Para fazer isso, navegue até Pixel e selecione a guia **[!UICONTROL Settings]**. Em API de Eventos, selecione **[!UICONTROL Generate Access Token]**.

Consulte o [[!DNL TikTok] guia de introdução](https://business-api.tiktok.com/portal/docs?id=1739584855420929) para obter mais informações sobre como configurar o código de pixel e o token de acesso.

## Instalar e configurar a extensão de API de eventos Web do [!DNL TikTok] {#install}

Para instalar a extensão, selecione **[!UICONTROL Extensions]** na navegação à esquerda. Na guia **[!UICONTROL Catalog]**, selecione o **[!UICONTROL TikTok Web Events API Extension]** e selecione **[!UICONTROL Install]**.

![O catálogo de extensões que mostra a instalação do destaque do cartão de extensão [!DNL TikTok].](../../../images/extensions/server/tiktok/install-extension.png)

Na próxima tela, insira os seguintes valores de configuração que você gerou anteriormente do [!DNL TikTok] Ads Manager:

* **[!UICONTROL Pixel Code]**
* **[!UICONTROL Access Token]**

Quando terminar, selecione **[!UICONTROL Save]**.

Tela de configuração ![[!DNL TikTok] para a extensão de API de eventos da Web [!DNL TikTok].](../../../images/extensions/server/tiktok/configure.png)

## Configurar uma regra de encaminhamento de eventos {#config-rule}

Depois que todos os seus elementos de dados estiverem configurados, você poderá começar a criar regras de encaminhamento de eventos que determinam quando e como seus eventos serão enviados para [!DNL TikTok].

Crie uma nova [regra](../../../ui/managing-resources/rules.md) na propriedade de encaminhamento de eventos. Em **[!UICONTROL Actions]**, adicione uma nova ação e defina a extensão como **[!UICONTROL TikTok Web Events API Extension]**. Para enviar eventos do Edge Network para [!DNL TikTok], defina **[!UICONTROL Action Type]** como **[!UICONTROL Send TikTok Web Events API Event].**

![O tipo de ação [!UICONTROL Send TikTok Web Events API Event] que está sendo selecionado para uma regra [!DNL TikTok] na interface da Coleção de Dados.](../../../images/extensions/server/tiktok/select-action.png)

Após a seleção, controles adicionais aparecem para configurar ainda mais o evento, conforme descrito abaixo. Após a conclusão, selecione **[!UICONTROL Keep Changes]** para salvar a regra.

**[!UICONTROL Web Events and Parameters]**

Os eventos e parâmetros da Web contêm informações gerais sobre o evento. Os eventos padrão têm suporte nas ferramentas de integração do [!DNL TikTok] e podem ser usados para relatórios, otimização de conversões e criação de públicos.

| Entrada | Descrição |
| --- | --- |
| Nome do evento | O nome do evento. Estas são ações com nomes predefinidos criados por [!DNL TikTok] e é um campo obrigatório. Consulte a documentação da [[!DNL TikTok] API de marketing](https://business-api.tiktok.com/portal/docs?id=1741601162187777) para obter mais informações sobre eventos com suporte. |
| Hora do Evento | Data e hora como cadeia de caracteres no formato ISO 8601 ou `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. Este campo é obrigatório. |
| ID de evento | A ID exclusiva gerada pelos anunciantes para indicar cada evento. Este campo é opcional e é usado para desduplicação. |

{style="table-layout:auto"}

![A seção [!DNL Web Events and Parameters] que mostra exemplos de entrada de dados nos campos.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL User Context Parameters]**

Os parâmetros de contexto de usuário contêm informações de cliente que são usadas para corresponder eventos de visitante da Web com [!DNL TikTok] usuários. A inclusão de vários tipos de dados correspondentes permite aumentar a precisão dos modelos de direcionamento e otimização.

| Entrada | Descrição |
| --- | --- |
| Endereço IP | Endereço IP público sem hash do navegador. O suporte é fornecido para endereços IPv4 e IPv6. As formas completa e compactada de endereços IPv6 são reconhecidas. |
| Agente do usuário | O agente de usuário sem hash do dispositivo do usuário. |
| Email | Endereço de email do contato associado ao evento de conversão. |
| Telefone | O número de telefone deve estar no formato E164 `[+][country code][area code][local phone number]` antes do hash. |
| ID do cookie | Se você estiver usando o Pixel, o SDK salvará automaticamente um identificador exclusivo no cookie `_ttp`, se os cookies estiverem habilitados. O valor `_ttp` pode ser extraído e usado para este campo. |
| ID externa | Qualquer identificador exclusivo, como IDs de usuário, IDs de cookie externo e assim por diante, deve ter hash com SHA256. |
| ID de cliques do TikTok | O `ttclid` que é adicionado à URL da página de aterrissagem sempre que um anúncio é selecionado em [!DNL TikTok]. |
| URL da página | O URL da página no momento do evento. |
| URL do referenciador de página | O URL do referenciador de página. |

{style="table-layout:auto"}

![A seção [!DNL User Context Parameters] que mostra exemplos de entrada de dados nos campos.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Properties Parameters]**

Use os parâmetros de propriedades para configurar outras propriedades compatíveis.

| Entrada | Descrição |
| --- | --- |
| Preço | O custo de um único item. |
| Quantidade | O número de itens sendo comprados no evento. Deve ser um número positivo maior que 0. |
| Tipo de conteúdo | Um valor de `product` ou `product_group` deve ser atribuído à propriedade de objeto content_type, dependendo de como você configurará seu feed de dados ao configurar seu catálogo de produtos. |
| ID de conteúdo | Um identificador exclusivo do item de produto. |
| Categoria de conteúdo | Categoria da página/produto. |
| Nome do conteúdo | Nome da página/produto. |
| Currency | A moeda dos itens que estão sendo comprados no evento. Isso é expresso em ISO-4217. |
| Valor | O preço total do pedido. Esse valor será igual ao preço * quantidade. |
| Descrição | Uma descrição do item ou da página. |
| Consulta | A sequência de caracteres de texto que foi usada para pesquisar um produto. |
| Status | O status de um pedido, item ou serviço. Por exemplo, &quot;enviado&quot;. |

{style="table-layout:auto"}

![A seção [!DNL Properties Parameters] que mostra exemplos de entrada de dados nos campos.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Desduplicação de eventos {#deduplication}

O pixel [!DNL TikTok] precisará ser configurado para desduplicação se você usar o SDK de [!DNL TikTok] pixels e a extensão de API de eventos da Web [!DNL TikTok] para enviar os mesmos eventos para [!DNL TikTok].

A desduplicação não é necessária se tipos de evento distintos estiverem sendo enviados do cliente e do servidor sem qualquer sobreposição. Para garantir que seus relatórios não sejam afetados negativamente, verifique se qualquer evento compartilhado pelo SDK de [!DNL TikTok] pixels e pela extensão de API de eventos da Web do [!DNL TikTok] foi desduplicado.

Ao enviar eventos compartilhados, verifique se todos os eventos incluem uma ID de pixel, uma ID de evento e um nome. Os eventos duplicados que chegarem dentro de cinco minutos um do outro serão mesclados. Se o campo de dados estiver ausente do primeiro evento, ele será combinado com o evento subsequente. Qualquer evento duplicado recebido em 48 horas será removido.

Consulte a documentação [!DNL TikTok] em [Eliminação de Duplicação de Eventos](https://ads.tiktok.com/help/article/event-deduplication) para obter mais detalhes sobre esse processo.

## Próximas etapas

Este guia aborda como enviar dados de eventos do lado do servidor para o [!DNL TikTok] usando a extensão de API de eventos da Web do [!DNL TikTok]. Para obter mais informações sobre os recursos de encaminhamento de eventos do [!DNL Adobe Experience Platform], consulte a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
