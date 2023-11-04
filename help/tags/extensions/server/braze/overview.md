---
keywords: extensão de encaminhamento de eventos;braze;extensão de encaminhamento de eventos braze
title: Extensão Braze Event Forwarding
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform envia eventos da Rede de borda para o Brasil.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '1861'
ht-degree: 5%

---

# Extensão de encaminhamento de eventos da [!DNL Braze Track Events API]

[[!DNL Braze]](https://www.braze.com) O é uma plataforma de engajamento do cliente que promove interações centradas no cliente entre consumidores e marcas em tempo real. Usar [!DNL Braze], você pode fazer o seguinte:

- Forneça dados (como mensagens de marketing) para usuários direcionados com base em sua preferência de idioma, preferência de local e muito mais, para aumentar as taxas de conversão e oferecer suporte às principais metas de negócios.
- Envie mensagens personalizadas aos clientes por vários canais, incluindo email, notificações por push e mensagens no aplicativo, na hora certa e nos idiomas de sua preferência.
- Direcione usuários específicos para campanhas de marketing e promocionais para aumentar o número de clientes recorrentes.
- Estudar o comportamento e os padrões do usuário para direcionar públicos específicos com mensagens personalizadas, o que pode ajudar a aumentar a receita.

A variável [!DNL Braze Track Events API] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) permite que você aproveite os dados capturados na Rede de borda da Adobe Experience Platform e os envie para [!DNL Braze] na forma de eventos do lado do servidor usando o [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) API.

Este documento aborda os casos de uso da extensão, como instalá-la nas bibliotecas de encaminhamento de eventos e como empregar seus recursos em um encaminhamento de eventos [regra](../../../ui/managing-resources/rules.md).

## Casos de uso

Essa extensão deve ser usada se você quiser usar dados da Rede de borda no [!DNL Braze] para aproveitar os recursos de análise e direcionamento do cliente.

Por exemplo, considere uma organização de varejo que tenha uma presença multicanal (site e celular) e esteja capturando entradas transacionais ou conversacionais como dados do evento do site e das plataformas móveis. Uso de vários [tag](../../../home.md) regras, esses dados são enviados para a Rede de borda em tempo real. A partir daqui, o [!DNL Braze] a extensão de encaminhamento de eventos envia automaticamente eventos relevantes para o [!DNL Braze] do lado do servidor.

Depois que os dados forem enviados, as equipes de análise da organização poderão aproveitar [!DNL Braze's] recursos para processar os conjuntos de dados e obter insights de negócios para gerar gráficos, painéis ou outras visualizações para informar as partes interessadas de negócios. Consulte a [[!DNL Braze] clientes](https://www.braze.com/customers) para obter mais detalhes sobre os vários casos de uso da plataforma.

## [!DNL Braze] pré-requisitos e medidas de proteção {#prerequisites}

Você deve ter um [!DNL Braze] para utilizar as suas tecnologias. Se você não tiver uma conta, navegue até a [Página Introdução](https://www.braze.com/get-started/) em [!DNL Braze] para se conectar a [!DNL Braze Sales] e inicie o processo de criação de conta.

### Medidas de proteção de API

A extensão usa dois de [!DNL Braze]As APIs do e seus limites são descritos abaixo:

| API | Limites de taxa |
| --- | --- |
| [!DNL User Track] | 50.000 solicitações por minuto <br>Consulte a [[!DNL User Track] Documentação da API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) para obter detalhes. |
| [!DNL User Identify] | 20.000 solicitações por minuto <br>Consulte a [[!DNL User Identify] Documentação da API](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) para obter detalhes. |

>[!NOTE]
>
> Consulte o guia em [[!DNL Braze] Limites da API](https://www.braze.com/docs/api/api_limits/) para obter mais informações sobre os limites que impõem.

### Pontos de dados faturáveis

Envio de atributos personalizados adicionais para o [!DNL Braze] pode aumentar o [!DNL Braze] consumo de ponto de dados. Consulte seu [!DNL Braze] gerente de conta antes de enviar atributos personalizados adicionais. Consulte a [!DNL Braze] documentação sobre [pontos de dados faturáveis](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) para obter mais informações.

### Coletar detalhes de configuração necessários {#configuration-details}

Para conectar a rede de borda ao [!DNL Braze], as seguintes entradas são necessárias:

| Tipo de chave | Descrição | Exemplo |
| --- | --- | --- |
| [!DNL Braze] Instância | O endpoint REST associado à variável [!DNL Braze] conta. Consulte a [!DNL Braze] documentação sobre [instâncias](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) para obter orientação. | `https://rest.iad-03.braze.com` |
| Chave de API | A variável [!DNL Braze] Chave de API associada à [!DNL Braze] conta. <br/>Consulte a [!DNL Braze] documentação sobre o [Chave de API REST](https://www.braze.com/docs/api/basics/#rest-api-key) para obter orientação. | `YOUR-BRAZE-REST-API-KEY` |

### Criar um segredo

Criar um novo [segredo de encaminhamento de eventos](../../../ui/event-forwarding/secrets.md) e defina o valor como seu [[!DNL Braze] Chave de API](#configuration-details). Ele será usado para autenticar a conexão com sua conta, mantendo o valor seguro.

## Instale e configure o [!DNL Braze] extensão {#install}

Para instalar a extensão, [criar uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Selecionar **[!UICONTROL Extensões]** no painel de navegação esquerdo. No **[!UICONTROL Catálogo]** selecione **[!UICONTROL Instalar]** no cartão para o [!DNL Braze] extensão.

![Instale o [!DNL Braze] extensão.](../../../images/extensions/server/braze/install-extension.png)

Na tela seguinte, insira [valores de configuração](#configuration-details) que você coletou anteriormente [!DNL Braze]:

- **[!UICONTROL URL de Ponto de Extremidade Rest Brasileiro]**: Você pode inserir o valor de seu [!DNL Braze] rest endpoint URL como texto sem formatação na entrada fornecida.
- **[!UICONTROL Chave de API]**: selecione a variável [elemento de dados secreto](#create-a-secret) que você criou anteriormente, e que contém seu [!DNL Braze] Chave da API.

Selecione **[!UICONTROL Salvar]** ao concluir.

![A variável [!DNL Braze] página de configuração de extensão.](../../../images/extensions/server/braze/configure-extension.png)

## Criar um [!DNL Send Event] regra {#tracking-rule}

Depois de instalar a extensão, crie um novo encaminhamento de eventos [regra](../../../ui/managing-resources/rules.md) e configure suas condições conforme desejado. Ao configurar as ações para a regra, selecione a variável **[!UICONTROL Braze]** e selecione **[!UICONTROL Enviar evento]** para o tipo de ação.

![Adicione uma configuração de ação de regra de encaminhamento de eventos.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Identificação do usuário]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL ID de usuário externo] | UUID ou GUID longo, aleatório e bem distribuído. Se você escolher um método diferente para nomear suas IDs de usuário, elas também deverão ser longas, aleatórias e bem distribuídas. Saiba mais sobre [convenção de nomenclatura de ID de usuário sugerida](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL ID de usuário do Braze] | Identificador de usuário brasileiro. |
| [!UICONTROL Alias do usuário] | Um alias serve como um identificador de usuário exclusivo alternativo. Use aliases para identificar usuários em dimensões diferentes da ID de usuário principal. <br><br> O objeto alias do usuário consiste em duas partes: um alias_name para o próprio identificador e um alias_label indicando o tipo de alias. Os usuários podem ter vários aliases com rótulos diferentes, mas somente um alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular o evento a um usuário, é necessário preencher a [!UICONTROL ID de usuário externo] ou o campo [!UICONTROL Identificador de usuário brasileiro] ou a variável [!UICONTROL Alias do usuário] seção.

**[!UICONTROL Dados do evento]**

| Entrada | Descrição | Obrigatório |
| --- | --- | --- |
| [!UICONTROL Nome do evento &#x200B;] | Nome do evento. | Sim |
| [!UICONTROL Hora do Evento] | Data e hora como string em ISO 8601 ou em `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sim |
| [!UICONTROL Identificador do aplicativo] | O Identificador do Aplicativo ou <strong>app_id</strong> é um parâmetro que associa uma atividade a um aplicativo específico no seu grupo de aplicativos. Ele designa com qual aplicativo do grupo de aplicativos você está interagindo. Saiba mais sobre o [Tipos de identificador de API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL &#x200B; Propriedades do evento] | Um objeto JSON que contém propriedades personalizadas do evento. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> A variável **[!UICONTROL Evento de envio do Braze]** uma ação requer somente um **[!UICONTROL Nome do evento]** e **[!UICONTROL Hora do Evento]** para ser especificado, mas você deve incluir o máximo de informações possível no campo de propriedades personalizadas. Para obter detalhes sobre a [!DNL Braze] objeto de evento, consulte o [documentação oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos do usuário]**

Os atributos do usuário podem ser um objeto JSON que contém campos que criarão ou atualizarão um atributo com o nome e o valor fornecidos no perfil do usuário especificado. As seguintes propriedades são compatíveis:

| Atributo do usuário | Descrição |
| --- | --- |
| [!UICONTROL Nome] | |
| [!UICONTROL Sobrenome] | |
| [!UICONTROL Telefone] | |
| [!UICONTROL Email] | |
| [!UICONTROL Gênero] | Uma das seguintes sequências de caracteres: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (outro), &quot;N&quot; (não aplicável), &quot;P&quot; (prefere não dizer). |
| [!UICONTROL Cidade] | |
| [!UICONTROL País] | País como uma sequência de caracteres em [ISO-3166-1 alfa-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Idioma] | Idioma como uma cadeia de caracteres em [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Data de nascimento] | Sequência de caracteres no formato &quot;AAAA-MM-DD&quot; (por exemplo, 1980-12-21). |
| [!UICONTROL Fuso Horário] | Nome do fuso horário de [Banco de Dados de Fuso Horário IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por exemplo, &#39;América/Nova_York&#39; ou &#39;Hora do Leste (EUA e Canadá)&#39;). |
| [!UICONTROL Facebook] | Hash que contém qualquer um de id (cadeia de caracteres), curtidas (matriz de cadeias de caracteres), num_friends (inteiro). |
| [!UICONTROL Twitter] | Hash que contém qualquer um de id (inteiro), screen_name (sequência de caracteres, identificador de Twitter), seguidores_count (inteiro), friends_count (inteiro), statuses_count(inteiro). |

{style="table-layout:auto"}

## Criar um [!DNL Send Purchase Event] regra {#purchase-rule}

Depois de instalar a extensão, crie um novo encaminhamento de eventos [regra](../../../ui/managing-resources/rules.md) e configure suas condições conforme desejado. Ao configurar as ações para a regra, selecione a variável **[!UICONTROL Braze]** e selecione **[!UICONTROL Enviar evento de compra]** para o tipo de ação.

![Adicione uma configuração de ação de regra de encaminhamento de eventos do tipo de ação Desenvolver compra.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Identificação do usuário]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL ID de usuário externo] | UUID ou GUID longo, aleatório e bem distribuído. Se você escolher um método diferente para nomear suas IDs de usuário, elas também deverão ser longas, aleatórias e bem distribuídas. Saiba mais sobre [convenção de nomenclatura de ID de usuário sugerida](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL ID de usuário do Braze] | Identificador de usuário brasileiro. |
| [!UICONTROL Alias do usuário] | Um alias serve como um identificador de usuário exclusivo alternativo. Use aliases para identificar usuários em dimensões diferentes da ID de usuário principal. <br><br> O objeto alias do usuário consiste em duas partes: um alias_name para o próprio identificador e um alias_label indicando o tipo de alias. Os usuários podem ter vários aliases com rótulos diferentes, mas somente um alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular o evento a um usuário, você deve concluir a [!UICONTROL ID de usuário externo] , a variável [!UICONTROL Identificador de usuário brasileiro] ou o campo [!UICONTROL Alias do usuário] seção.

**[!UICONTROL Dados de compra]**

| Entrada | Descrição | Obrigatório |
| --- | --- | --- |
| [!UICONTROL Identificação do produto &#x200B;] | Identificador da compra. (por exemplo, Nome do produto ou Categoria do produto) | Sim |
| [!UICONTROL Tempo de Compra] | Data e hora como string em ISO 8601 ou em `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sim |
| [!UICONTROL Moeda &#x200B;] | Moeda como sequência de caracteres em [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) Formato alfabético de código monetário. | Sim |
| [!UICONTROL Preço &#x200B;] | Preço. | Sim |
| [!UICONTROL Quantidade &#x200B;] | Se não for fornecido, o valor padrão será 1. O valor máximo deve ser inferior a 100. | |
| [!UICONTROL Identificador do aplicativo] | O Identificador do Aplicativo ou <strong>app_id</strong> é um parâmetro que associa uma atividade a um aplicativo específico no seu grupo de aplicativos. Ele designa com qual aplicativo do grupo de aplicativos você está interagindo. Saiba mais sobre o [Tipos de identificador de API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Propriedades de compra &#x200B;] | Um objeto JSON que contém propriedades personalizadas da compra. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> A variável **[!UICONTROL Evento de envio do Braze]** uma ação requer somente um **[!UICONTROL Nome do evento]** e **[!UICONTROL Hora do Evento]** para ser especificado, mas você deve incluir o máximo de informações possível no campo de propriedades personalizadas. Para obter detalhes sobre a [!DNL Braze] objeto de evento, consulte o [documentação oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos do usuário]**

Os atributos do usuário podem ser um objeto JSON que contém campos que criarão ou atualizarão um atributo com o nome e o valor fornecidos no perfil do usuário especificado. As seguintes propriedades são compatíveis:

| Atributo do usuário | Descrição |
| --- | --- |
| [!UICONTROL Nome] | |
| [!UICONTROL Sobrenome] | |
| [!UICONTROL Telefone] | |
| [!UICONTROL Email] | |
| [!UICONTROL Gênero] | Uma das seguintes sequências de caracteres: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (outro), &quot;N&quot; (não aplicável), &quot;P&quot; (prefere não dizer). |
| [!UICONTROL Cidade] | |
| [!UICONTROL País] | País como uma sequência de caracteres em [ISO-3166-1 alfa-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Idioma] | Idioma como uma cadeia de caracteres em [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Data de nascimento] | Sequência de caracteres no formato &quot;AAAA-MM-DD&quot; (por exemplo, 1980-12-21). |
| [!UICONTROL Fuso Horário] | Nome do fuso horário de [Banco de Dados de Fuso Horário IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por exemplo, &#39;América/Nova_York&#39; ou &#39;Hora do Leste (EUA e Canadá)&#39;). |
| [!UICONTROL Facebook] | Hash que contém qualquer um de id (cadeia de caracteres), curtidas (matriz de cadeias de caracteres), num_friends (inteiro). |
| [!UICONTROL Twitter] | Hash que contém qualquer um de id (inteiro), screen_name (sequência de caracteres, identificador de Twitter), seguidores_count (inteiro), friends_count (inteiro), statuses_count(inteiro). |

{style="table-layout:auto"}

## Validar dados no [!DNL Braze] {#validate}

Se a coleção de eventos e a [!DNL Adobe Experience Platform] integração foram bem-sucedidas, você verá eventos no [!DNL Braze] console quando [exibição de perfis de usuário](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Especificamente, os novos dados do evento enviados para o [!DNL Braze] é refletida na variável [!DNL Purchases] de um usuário específico [guia visão geral](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Próximas etapas

Este guia abordou como enviar eventos de conversão para o [!DNL Braze] usando o encaminhamento de eventos. Para obter mais detalhes sobre aplicativos downstream para dados de eventos enviados para o [!DNL Braze], consulte o [documentação oficial](https://www.braze.com/docs).

Para obter mais informações sobre os recursos de encaminhamento de eventos no Experience Platform, consulte [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
