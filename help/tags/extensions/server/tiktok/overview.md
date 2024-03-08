---
title: Integração da extensão de API de eventos da Web do Adobe TikTok
description: Essa API de eventos da Web do Adobe Experience Platform permite compartilhar interações do site diretamente com o TikTok.
last-substantial-update: 2023-09-26T00:00:00Z
exl-id: 14b8e498-8ed5-4330-b1fa-43fd1687c201
source-git-commit: 4ee895cb8371646fd2013e2a8f65c2ffdae95850
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 3%

---

# [!DNL TikTok] visão geral da extensão de API de eventos na web

A variável [!DNL TikTok] A API de eventos é uma [API do servidor de rede de borda](/help/server-api/overview.md) que permite compartilhar informações com a [!DNL TikTok] diretamente sobre as ações do usuário em seus sites. Você pode aproveitar as regras de encaminhamento de eventos para enviar dados do [!DNL Adobe Experience Platform Edge Network] para [!DNL TikTok] usando o [!DNL TikTok] Extensão da API de eventos da Web.

## [!DNL TikTok] pré-requisitos {#prerequisites}

Para configurar o [!DNL TikTok] API de eventos da Web para usar o [!DNL TikTok] de eventos, é necessário gerar uma [!DNL TikTok] código de pixel e token de acesso.

Você deve ter um válido [!DNL TikTok] para uma conta comercial para criar um [!DNL TikTok] pixel usando a configuração do parceiro. Vá para a [[!DNL TikTok] para página de registro comercial](https://www.tiktok.com/business/en-US/solutions/business-account) para registrar e criar uma conta se ainda não tiver uma.

Você precisa estar conectado à sua conta comercial para configurar [!DNL TikTok] Pixel usando configuração de parceiro. Para fazer isso, siga as etapas abaixo:

1. Navegue até a **[!UICONTROL Assets]** e selecione **[!UICONTROL Evento]**.
2. Em Eventos da Web, selecione **[!UICONTROL Gerenciar]**.
3. Selecionar **[!UICONTROL Configurar eventos da Web]**.
4. Selecionar **[!UICONTROL Configuração do Parceiro]** como seu método de conexão.

Consulte a [Introdução ao Pixel](https://ads.tiktok.com/help/article/get-started-pixel) guia para obter mais informações sobre como configurar o [!DNL TikTok] pixel.

Você pode gerar um token de acesso depois que o pixel for criado com êxito. Para fazer isso, navegue até o Pixel e selecione a variável **[!UICONTROL Configurações]** guia. Em API de eventos, selecione **[!UICONTROL Gerar token de acesso]**.

Consulte a [[!DNL TikTok] guia de introdução](https://business-api.tiktok.com/portal/docs?id=1739584855420929) para obter mais informações sobre como configurar o código de pixel e o token de acesso.

## Instale e configure o [!DNL TikTok] extensão da API de eventos da web {#install}

Para instalar a extensão, selecione **[!UICONTROL Extensões]** no painel de navegação esquerdo. No **[!UICONTROL Catálogo]** , selecione a **[!UICONTROL Extensão da API de eventos da Web do TikTok]** e selecione **[!UICONTROL Instalar]**.

![O catálogo de extensões que mostra o [!DNL TikTok] placa de extensão destacando instalar.](../../../images/extensions/server/tiktok/install-extension.png)

Na próxima tela, insira os seguintes valores de configuração gerados anteriormente [!DNL TikTok] Gerenciador de anúncios:

* **[!UICONTROL Código de pixel]**
* **[!UICONTROL Token de acesso]**

Quando terminar, selecione **[!UICONTROL Salvar]**.

![[!DNL TikTok] tela de configuração para o [!DNL TikTok] extensão da API de eventos da Web.](../../../images/extensions/server/tiktok/configure.png)

## Configurar uma regra de encaminhamento de eventos {#config-rule}

Depois que todos os elementos de dados forem configurados, você poderá começar a criar regras de encaminhamento de eventos que determinam quando e como seus eventos serão enviados para o [!DNL TikTok].

Criar um novo [regra](../../../ui/managing-resources/rules.md) na propriedade de encaminhamento de eventos. Em **[!UICONTROL Ações]**, adicione uma nova ação e defina a extensão para **[!UICONTROL Extensão da API de eventos da Web do TikTok]**. Para enviar eventos da Rede de borda para o [!DNL TikTok], defina o **[!UICONTROL Tipo de ação]** para **[!UICONTROL Enviar evento de API de eventos da Web do TikTok].**

![A variável [!UICONTROL Enviar evento de API de eventos da Web do TikTok] tipo de ação que está sendo selecionado para um [!DNL TikTok] na interface da Coleção de dados.](../../../images/extensions/server/tiktok/select-action.png)

Após a seleção, controles adicionais aparecem para configurar ainda mais o evento, conforme descrito abaixo. Após a conclusão, selecione **[!UICONTROL Manter alterações]** para salvar a regra.

**[!UICONTROL Eventos e parâmetros da Web]**

Os eventos e parâmetros da Web contêm informações gerais sobre o evento. Eventos padrão são compatíveis com o [!DNL TikTok] ferramentas de integração e podem ser usadas para relatórios, otimização para conversões e criação de públicos-alvo.

| Entrada | Descrição |
| --- | --- |
| Nome do evento | O nome do evento. Essas são ações com nomes predefinidos criadas por [!DNL TikTok] e é um campo obrigatório. Consulte a [[!DNL TikTok] API de marketing](https://business-api.tiktok.com/portal/docs?id=1741601162187777) para obter mais informações sobre eventos compatíveis. |
| Hora do Evento | Data e hora como string em ISO 8601 ou em `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. Este campo é obrigatório. |
| ID de evento | A ID exclusiva gerada pelos anunciantes para indicar cada evento. Este campo é opcional e é usado para desduplicação. |

{style="table-layout:auto"}

![A variável [!DNL Web Events and Parameters] seção que mostra exemplos de entrada de dados nos campos.](../../../images/extensions/server/tiktok/configure-web-events-parameters.png)

**[!UICONTROL Parâmetros de Contexto do Usuário]**

Os parâmetros de contexto do usuário contêm informações do cliente usadas para corresponder eventos de visitantes da Web com [!DNL TikTok] usuários. A inclusão de vários tipos de dados correspondentes permite aumentar a precisão dos modelos de direcionamento e otimização.

| Entrada | Descrição |
| --- | --- |
| Endereço IP | Endereço IP público sem hash do navegador. O suporte é fornecido para endereços IPv4 e IPv6. As formas completa e compactada de endereços IPv6 são reconhecidas. |
| Agente do usuário | O agente de usuário sem hash do dispositivo do usuário. |
| Email | Endereço de email do contato associado ao evento de conversão. |
| Telefone | O número de telefone deve estar no formato E164 [+][código do país][código de área][local phone number] antes do hash. |
| ID de cookies | Se estiver usando o Pixel, o SDK salvará automaticamente um identificador exclusivo na `_ttp` cookie, se os cookies estiverem ativados. A variável `_ttp` pode ser extraído e usado para este campo. |
| ID externa | Qualquer identificador exclusivo, como IDs de usuário, IDs de cookie externo e assim por diante, deve ter hash com SHA256. |
| ID de cliques do TikTok | A variável `ttclid` que é adicionado ao URL da landing page sempre que um anúncio é selecionado em [!DNL TikTok]. |
| URL da página | O URL da página no momento do evento. |
| URL do referenciador de página | O URL do referenciador de página. |

{style="table-layout:auto"}

![A variável [!DNL User Context Parameters] seção que mostra exemplos de entrada de dados nos campos.](../../../images/extensions/server/tiktok/configure-user-context-parameters.png)

**[!UICONTROL Parâmetros de propriedades]**

Use os parâmetros de propriedades para configurar outras propriedades compatíveis.

| Entrada | Descrição |
| --- | --- |
| Preço | O custo de um único item. |
| Quantidade | O número de itens sendo comprados no evento. Deve ser um número positivo maior que 0. |
| Tipo de conteúdo | Um valor de `product` ou `product_group` deve ser atribuído à propriedade de objeto content_type, dependendo de como você configurará o feed de dados ao configurar o catálogo de produtos. |
| ID de conteúdo | Um identificador exclusivo do item de produto. |
| Categoria de conteúdo | Categoria da página/produto. |
| Nome do conteúdo | Nome da página/produto. |
| Moeda | A moeda dos itens que estão sendo comprados no evento. Isso é expresso em ISO-4217. |
| Valor | O preço total do pedido. Esse valor será igual ao preço * quantidade. |
| Descrição | Uma descrição do item ou da página. |
| Consulta | A sequência de caracteres de texto que foi usada para pesquisar um produto. |
| Status | O status de um pedido, item ou serviço. Por exemplo, &quot;enviado&quot;. |

{style="table-layout:auto"}

![A variável [!DNL Properties Parameters] seção que mostra exemplos de entrada de dados nos campos.](../../../images/extensions/server/tiktok/configure-properties-parameters.png)

## Desduplicação de eventos {#deduplication}

[!DNL TikTok] pixel precisará ser configurado para desduplicação se você usar o [!DNL TikTok] pixel SDK e o [!DNL TikTok] extensão da API de eventos da Web para enviar os mesmos eventos para o [!DNL TikTok].

A desduplicação não é necessária se tipos de evento distintos estiverem sendo enviados do cliente e do servidor sem qualquer sobreposição. Para garantir que seus relatórios não sejam afetados negativamente, verifique se qualquer evento único compartilhado pela [!DNL TikTok] pixel SDK e o [!DNL TikTok] a extensão da API de eventos da web está desduplicada.

Ao enviar eventos compartilhados, verifique se todos os eventos incluem uma ID de pixel, uma ID de evento e um nome. Os eventos duplicados que chegarem dentro de cinco minutos um do outro serão mesclados. Se o campo de dados estiver ausente do primeiro evento, ele será combinado com o evento subsequente. Qualquer evento duplicado recebido em 48 horas será removido.

Consulte a [!DNL TikTok] documentação sobre [Desduplicação de eventos](https://ads.tiktok.com/help/article/event-deduplication) para obter mais detalhes sobre esse processo.

## Próximas etapas

Este guia abordou como enviar dados do evento do lado do servidor para o [!DNL TikTok] usando o [!DNL TikTok] extensão da API de eventos da Web. Para obter mais informações sobre os recursos de encaminhamento de eventos do [!DNL Adobe Experience Platform], consulte o [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
