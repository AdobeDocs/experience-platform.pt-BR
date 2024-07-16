---
keywords: extensão de encaminhamento de eventos;braze;extensão de encaminhamento de eventos braze
title: Extensão Braze Event Forwarding
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform envia eventos Edge Network para o Braze.
last-substantial-update: 2023-03-29T00:00:00Z
exl-id: 297f48f8-2c3b-41c2-8820-35f4558c67b3
source-git-commit: d81c4c8630598597ec4e253ef5be9f26c8987203
workflow-type: tm+mt
source-wordcount: '1692'
ht-degree: 2%

---

# Extensão de encaminhamento de eventos da [!DNL Braze Track Events API]

[[!DNL Braze]](https://www.braze.com) é uma plataforma de envolvimento do cliente que possibilita interações centradas no cliente entre consumidores e marcas em tempo real. Usando o [!DNL Braze], você pode fazer o seguinte:

- Forneça dados (como mensagens de marketing) para usuários direcionados com base em sua preferência de idioma, preferência de local e muito mais, para aumentar as taxas de conversão e oferecer suporte às principais metas de negócios.
- Envie mensagens personalizadas aos clientes por vários canais, incluindo email, notificações por push e mensagens no aplicativo, na hora certa e nos idiomas de sua preferência.
- Direcione usuários específicos para campanhas de marketing e promocionais para aumentar o número de clientes recorrentes.
- Estudar o comportamento e os padrões do usuário para direcionar públicos específicos com mensagens personalizadas, o que pode ajudar a aumentar a receita.

A extensão [!DNL Braze Track Events API] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) permite aproveitar os dados capturados no Edge Network do Adobe Experience Platform e enviá-los para [!DNL Braze] na forma de eventos do lado do servidor usando a API [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track).

Este documento aborda os casos de uso da extensão, como instalá-la nas bibliotecas de encaminhamento de eventos e como empregar seus recursos em uma [regra](../../../ui/managing-resources/rules.md) de encaminhamento de eventos.

## Casos de uso

Essa extensão deve ser usada se você quiser usar dados do Edge Network em [!DNL Braze] para aproveitar seus recursos de análise e direcionamento de clientes.

Por exemplo, considere uma organização de varejo que tenha uma presença multicanal (site e celular) e esteja capturando entradas transacionais ou conversacionais como dados do evento do site e das plataformas móveis. Usando várias regras de [tag](../../../home.md), esses dados são enviados para o Edge Network em tempo real. Daqui, a extensão de encaminhamento de eventos do [!DNL Braze] envia automaticamente eventos relevantes do lado do servidor para o [!DNL Braze].

Depois que os dados forem enviados, as equipes de análise da organização poderão aproveitar os recursos do [!DNL Braze's] para processar os conjuntos de dados e obter insights comerciais para gerar gráficos, painéis ou outras visualizações para informar as partes interessadas. Consulte a página [[!DNL Braze] clientes](https://www.braze.com/customers) para obter mais detalhes sobre os vários casos de uso da plataforma.

## [!DNL Braze] pré-requisitos e medidas de proteção {#prerequisites}

É necessário ter uma conta [!DNL Braze] para usar suas tecnologias. Se você não tiver uma conta, navegue até a [Página Introdução](https://www.braze.com/get-started/) em [!DNL Braze] para se conectar a [!DNL Braze Sales] e iniciar o processo de criação da conta.

### Medidas de proteção de API

A extensão usa duas APIs de [!DNL Braze] e seus limites são descritos abaixo:

| API | Limites de taxa |
| --- | --- |
| [!DNL User Track] | 50.000 solicitações por minuto <br>Consulte a [[!DNL User Track] documentação da API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) para obter detalhes. |
| [!DNL User Identify] | 20.000 solicitações por minuto <br>Consulte a [[!DNL User Identify] documentação da API](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) para obter detalhes. |

>[!NOTE]
>
> Consulte o manual sobre [[!DNL Braze] limites de API](https://www.braze.com/docs/api/api_limits/) para obter mais detalhes sobre os limites impostos.

### Pontos de dados faturáveis

Enviar atributos personalizados adicionais para [!DNL Braze] pode aumentar seu consumo de ponto de dados de [!DNL Braze]. Consulte seu gerente de conta do [!DNL Braze] antes de enviar outros atributos personalizados. Consulte a documentação [!DNL Braze] em [pontos de dados faturáveis](https://www.braze.com/docs/user_guide/data_and_analytics/data_points/?tab=billable) para obter mais informações.

### Coletar detalhes de configuração necessários {#configuration-details}

Para conectar o Edge Network a [!DNL Braze], as seguintes entradas são necessárias:

| Tipo de chave | Descrição | Exemplo |
| --- | --- | --- |
| [!DNL Braze] Instância | O ponto de extremidade REST associado à conta [!DNL Braze]. Consulte a documentação [!DNL Braze] em [instâncias](https://www.braze.com/docs/user_guide/administrative/access_braze/sdk_endpoints) para obter orientação. | `https://rest.iad-03.braze.com` |
| Chave de API | A Chave de API [!DNL Braze] associada à conta [!DNL Braze]. <br/>Consulte a documentação [!DNL Braze] sobre a [chave da API REST](https://www.braze.com/docs/api/basics/#rest-api-key) para obter orientação. | `YOUR-BRAZE-REST-API-KEY` |

### Criar um segredo

Crie um novo [segredo de encaminhamento de eventos](../../../ui/event-forwarding/secrets.md) e defina o valor para sua [[!DNL Braze] Chave de API](#configuration-details). Ele será usado para autenticar a conexão com sua conta, mantendo o valor seguro.

## Instalar e configurar a extensão [!DNL Braze] {#install}

Para instalar a extensão, [crie uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Selecione **[!UICONTROL Extensões]** na navegação à esquerda. Na guia **[!UICONTROL Catálogo]**, selecione **[!UICONTROL Instalar]** no cartão para a extensão [!DNL Braze].

![Instalar a extensão [!DNL Braze].](../../../images/extensions/server/braze/install-extension.png)

Na próxima tela, insira os [valores de configuração](#configuration-details) a seguir, coletados anteriormente de [!DNL Braze]:

- **[!UICONTROL Resumir URL do Ponto de Extremidade]**: Você pode inserir o valor da sua URL do ponto de extremidade [!DNL Braze] como texto sem formatação na entrada fornecida.
- **[!UICONTROL Chave de API]**: selecione o [elemento de dados secreto](#create-a-secret) criado anteriormente, que contém sua chave de API [!DNL Braze].

Selecione **[!UICONTROL Salvar]** ao concluir.

![A página de configuração de extensão [!DNL Braze].](../../../images/extensions/server/braze/configure-extension.png)

## Criar uma regra [!DNL Send Event] {#tracking-rule}

Após instalar a extensão, crie uma nova [regra](../../../ui/managing-resources/rules.md) para o encaminhamento de eventos e configure suas condições conforme desejado. Ao configurar as ações para a regra, selecione a extensão **[!UICONTROL Braze]** e selecione **[!UICONTROL Enviar evento]** para o tipo de ação.

![Adicionar uma configuração de ação de regra de encaminhamento de eventos.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Identificação de usuário]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL ID de Usuário Externo] | UUID ou GUID longo, aleatório e bem distribuído. Se você escolher um método diferente para nomear suas IDs de usuário, elas também deverão ser longas, aleatórias e bem distribuídas. Saiba mais sobre a [convenção de nomenclatura de ID de usuário sugerida](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze ID de Usuário] | Identificador de usuário brasileiro. |
| [!UICONTROL Alias de usuário] | Um alias serve como um identificador de usuário exclusivo alternativo. Use aliases para identificar usuários em dimensões diferentes da ID de usuário principal. <br><br> O objeto alias do usuário consiste em duas partes: um alias_name para o próprio identificador e um alias_label indicando o tipo de alias. Os usuários podem ter vários aliases com rótulos diferentes, mas somente um alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular o evento a um usuário, é necessário preencher o campo [!UICONTROL ID de Usuário Externo], o campo [!UICONTROL Identificador de Usuário Brasileiro] ou a seção [!UICONTROL Alias de Usuário].

**[!UICONTROL Dados do evento]**

| Entrada | Descrição | Obrigatório |
| --- | --- | --- |
| [!UICONTROL Nome do Evento &#x200B;] | Nome do evento. | Sim |
| [!UICONTROL Hora do Evento] | Data e hora como cadeia de caracteres no formato ISO 8601 ou `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Sim |
| [!UICONTROL Identificador do aplicativo] | O Identificador de Aplicativo ou <strong>app_id</strong> é um parâmetro que associa uma atividade a um aplicativo específico no seu grupo de aplicativos. Ele designa com qual aplicativo do grupo de aplicativos você está interagindo. Saiba mais sobre os [tipos de identificador de API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Propriedades do Evento &#x200B;] | Um objeto JSON que contém propriedades personalizadas do evento. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> A ação **[!UICONTROL Enviar Evento do Brasil]** exige que apenas um **[!UICONTROL Nome do Evento]** e um **[!UICONTROL Horário do Evento]** sejam especificados, mas você deve incluir o máximo possível de informações no campo de propriedades personalizadas. Para obter detalhes sobre o objeto de evento [!DNL Braze], consulte a [documentação oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos de usuário]**

Os atributos do usuário podem ser um objeto JSON que contém campos que criarão ou atualizarão um atributo com o nome e o valor fornecidos no perfil do usuário especificado. As seguintes propriedades são compatíveis:

| Atributo do usuário | Descrição |
| --- | --- |
| [!UICONTROL Nome] | |
| [!UICONTROL Sobrenome] | |
| [!UICONTROL Telefone] | |
| [!UICONTROL Email] | |
| [!UICONTROL Gênero] | Uma das seguintes sequências de caracteres: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (outro), &quot;N&quot; (não aplicável), &quot;P&quot; (prefere não dizer). |
| [!UICONTROL Cidade] | |
| [!UICONTROL Country] | País como uma cadeia de caracteres no formato [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |
| [!UICONTROL Idioma] | Idioma como uma cadeia de caracteres no formato [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Data de nascimento] | Sequência de caracteres no formato &quot;AAAA-MM-DD&quot; (por exemplo, 1980-12-21). |
| [!UICONTROL Fuso Horário] | Nome do fuso horário do [Banco de Dados de Fuso Horário IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por exemplo, &#39;América/Nova_York&#39; ou &#39;Hora do Leste (EUA e Canadá)&#39;). |
| [!UICONTROL Facebook] | Hash que contém qualquer um de id (cadeia de caracteres), curtidas (matriz de cadeias de caracteres), num_friends (inteiro). |
| [!UICONTROL Twitter] | Hash que contém qualquer um de id (inteiro), screen_name (sequência de caracteres, identificador de Twitter), seguidores_count (inteiro), friends_count (inteiro), statuses_count(inteiro). |

{style="table-layout:auto"}

## Criar uma regra [!DNL Send Purchase Event] {#purchase-rule}

Após instalar a extensão, crie uma nova [regra](../../../ui/managing-resources/rules.md) para o encaminhamento de eventos e configure suas condições conforme desejado. Ao configurar as ações para a regra, selecione a extensão **[!UICONTROL Braze]** e selecione **[!UICONTROL Enviar Evento de Compra]** para o tipo de ação.

![Adicionar uma configuração de ação de regra de encaminhamento de eventos do tipo de ação de compra brasileira.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Identificação de usuário]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL ID de Usuário Externo] | UUID ou GUID longo, aleatório e bem distribuído. Se você escolher um método diferente para nomear suas IDs de usuário, elas também deverão ser longas, aleatórias e bem distribuídas. Saiba mais sobre a [convenção de nomenclatura de ID de usuário sugerida](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL Braze ID de Usuário] | Identificador de usuário brasileiro. |
| [!UICONTROL Alias de usuário] | Um alias serve como um identificador de usuário exclusivo alternativo. Use aliases para identificar usuários em dimensões diferentes da ID de usuário principal. <br><br> O objeto alias do usuário consiste em duas partes: um alias_name para o próprio identificador e um alias_label indicando o tipo de alias. Os usuários podem ter vários aliases com rótulos diferentes, mas somente um alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular o evento a um usuário, você deve concluir o campo [!UICONTROL ID de Usuário Externo], o campo [!UICONTROL Identificador de Usuário Brasileiro] ou a seção [!UICONTROL Alias de Usuário].

**[!UICONTROL Dados de compra]**

| Entrada | Descrição | Obrigatório |
| --- | --- | --- |
| [!UICONTROL ID do produto &#x200B;] | Identificador da compra. (por exemplo, Nome do produto ou Categoria do produto) | Sim |
| [!UICONTROL Tempo de Compra] | Data e hora como cadeia de caracteres no formato ISO 8601 ou `yyyy-MM-dd'T'HH:mm:ss:SSSZ`. | Sim |
| [!UICONTROL Moeda &#x200B;] | Moeda como cadeia de caracteres no formato de Código de Moeda Alfabético [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217). | Sim |
| [!UICONTROL Preço &#x200B;] | Preço. | Sim |
| [!UICONTROL Quantidade &#x200B;] | Se não for fornecido, o valor padrão será 1. O valor máximo deve ser inferior a 100. | |
| [!UICONTROL Identificador do aplicativo] | O Identificador de Aplicativo ou <strong>app_id</strong> é um parâmetro que associa uma atividade a um aplicativo específico no seu grupo de aplicativos. Ele designa com qual aplicativo do grupo de aplicativos você está interagindo. Saiba mais sobre os [tipos de identificador de API](https://www.braze.com/docs/api/identifier_types/). | |
| [!UICONTROL Comprar Propriedades &#x200B;] | Um objeto JSON que contém propriedades personalizadas da compra. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> A ação **[!UICONTROL Enviar Evento do Brasil]** exige que apenas um **[!UICONTROL Nome do Evento]** e **[!UICONTROL Tempo do Evento]** sejam especificados, mas você deve incluir o máximo possível de informações no campo de propriedades personalizadas. Para obter detalhes sobre o objeto de evento [!DNL Braze], consulte a [documentação oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos de usuário]**

Os atributos do usuário podem ser um objeto JSON que contém campos que criarão ou atualizarão um atributo com o nome e o valor fornecidos no perfil do usuário especificado. As seguintes propriedades são compatíveis:

| Atributo do usuário | Descrição |
| --- | --- |
| [!UICONTROL Nome] | |
| [!UICONTROL Sobrenome] | |
| [!UICONTROL Telefone] | |
| [!UICONTROL Email] | |
| [!UICONTROL Gênero] | Uma das seguintes sequências de caracteres: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (outro), &quot;N&quot; (não aplicável), &quot;P&quot; (prefere não dizer). |
| [!UICONTROL Cidade] | |
| [!UICONTROL Country] | País como uma cadeia de caracteres no formato [ISO-3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2). |
| [!UICONTROL Idioma] | Idioma como uma cadeia de caracteres no formato [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes). |
| [!UICONTROL Data de nascimento] | Sequência de caracteres no formato &quot;AAAA-MM-DD&quot; (por exemplo, 1980-12-21). |
| [!UICONTROL Fuso Horário] | Nome do fuso horário do [Banco de Dados de Fuso Horário IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por exemplo, &#39;América/Nova_York&#39; ou &#39;Hora do Leste (EUA e Canadá)&#39;). |
| [!UICONTROL Facebook] | Hash que contém qualquer um de id (cadeia de caracteres), curtidas (matriz de cadeias de caracteres), num_friends (inteiro). |
| [!UICONTROL Twitter] | Hash que contém qualquer um de id (inteiro), screen_name (sequência de caracteres, identificador de Twitter), seguidores_count (inteiro), friends_count (inteiro), statuses_count(inteiro). |

{style="table-layout:auto"}

## Validar dados em [!DNL Braze] {#validate}

Se a coleção de eventos e a integração do [!DNL Adobe Experience Platform] tiverem sido bem-sucedidas, você verá eventos no console do [!DNL Braze] ao [exibir perfis de usuário](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Especificamente, os novos dados do evento enviados para [!DNL Braze] são refletidos na seção [!DNL Purchases] da [guia de visão geral](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab) de um usuário específico.

## Próximas etapas

Este guia abordou como enviar eventos de conversão para [!DNL Braze] usando o encaminhamento de eventos. Para obter mais detalhes sobre aplicativos downstream para dados de eventos enviados para [!DNL Braze], consulte a [documentação oficial](https://www.braze.com/docs).

Para obter mais informações sobre os recursos de encaminhamento de eventos do Experience Platform, consulte a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
