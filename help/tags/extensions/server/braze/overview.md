---
keywords: extensão de encaminhamento de eventos; criar; extensão de encaminhamento de eventos do braze
title: Extensão de Encaminhamento de Evento Brasileiro
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform envia eventos de rede do Adobe Experience Edge para o Brasil.
source-git-commit: 88e589eb17c249a8bdc82fe7a041a5581a60c7e6
workflow-type: tm+mt
source-wordcount: '1874'
ht-degree: 4%

---


# [!DNL Braze Track Events API] extensão de encaminhamento de eventos

[[!DNL Braze]](https://www.braze.com) é uma plataforma de engajamento do cliente que alimenta as interações centradas no cliente entre consumidores e marcas em tempo real. Usando [!DNL Braze], você pode fazer o seguinte:

- Forneça dados (como mensagens de marketing) aos usuários alvos com base em sua preferência de idioma, preferência de local e muito mais, para aumentar as taxas de conversão e oferecer suporte a objetivos comerciais principais.
- Envie mensagens personalizadas aos clientes em vários canais, incluindo email, notificações por push e mensagens no aplicativo, na hora certa e em seus idiomas preferidos.
- Direcione usuários específicos para campanhas de marketing e promocionais para aumentar o número de clientes recorrentes.
- Estude o comportamento e os padrões do usuário para direcionar públicos-alvo específicos com mensagens personalizadas, o que pode ajudar a aumentar a receita.

O [!DNL Braze Track Events API] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) A extensão permite aproveitar os dados capturados na Rede de borda do Adobe Experience Platform e enviá-los para [!DNL Braze] na forma de eventos do lado do servidor usando o [[!DNL Braze User Identify]](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify) e [[!DNL Braze User Track]](https://www.braze.com/docs/api/endpoints/user_data/post_user_track) APIs.

Este documento aborda os casos de uso da extensão, como instalá-la nas bibliotecas de encaminhamento de eventos e como empregar seus recursos em um encaminhamento de eventos [regra](../../../ui/managing-resources/rules.md).

## Casos de uso

Essa extensão deve ser usada se você quiser usar dados da Edge Network em [!DNL Braze] para aproveitar seus recursos de análise e direcionamento do cliente.

Por exemplo, considere uma organização de varejo que tem uma presença multicanal (site e dispositivo móvel) e está capturando entrada transacional ou conversacional como dados de evento de seu site e plataformas móveis. Usar vários [tag](../../../home.md) , esses dados são enviados para a Edge Network em tempo real. Daqui, o [!DNL Braze] a extensão de encaminhamento de evento envia automaticamente os eventos relevantes para o [!DNL Braze] do lado do servidor.

Depois que os dados forem enviados, as equipes de análise da organização poderão aproveitar [!DNL Braze's] recursos para processar os conjuntos de dados e derivar insights de negócios para gerar gráficos, painéis ou outras visualizações para informar as partes interessadas da empresa. Consulte a [[!DNL Braze] clientes](https://www.braze.com/customers) para obter mais detalhes sobre os vários casos de uso da plataforma.

## [!DNL Braze] pré-requisitos e medidas de proteção {#prerequisites}

Você deve ter um [!DNL Braze] para utilizar as suas tecnologias. Se você não tiver uma conta, navegue até o [Página Introdução](https://www.braze.com/get-started/) on [!DNL Braze] para se conectar a [!DNL Braze Sales] e inicie o processo de criação de conta.

### Medidas de proteção de API

A extensão usa dois de [!DNL Braze]As APIs do e seus limites são descritos abaixo:

| API | Limites de taxa |
| --- | --- |
| [!DNL User Track] | 50.000 solicitações por minuto. <br>Consulte a [[!DNL User Track] Documentação da API](https://www.braze.com/docs/api/endpoints/user_data/post_user_track#rate-limit) para obter detalhes. |
| [!DNL User Identify] | 20.000 solicitações por minuto. <br>Consulte a [[!DNL User Identify] Documentação da API](https://www.braze.com/docs/api/endpoints/user_data/post_user_identify#rate-limit) para obter detalhes. |

>[!NOTE]
>
> Consulte o guia em [[!DNL Braze] Limites da API](https://www.braze.com/docs/api/api_limits/) para mais pormenores sobre os limites impostos.

### Pontos de dados faturáveis

Envio de atributos personalizados adicionais para [!DNL Braze] pode aumentar a sua [!DNL Braze] consumo de ponto de dados. Consulte seu [!DNL Braze] gerente de conta antes de enviar atributos personalizados adicionais. Consulte a [!DNL Braze] documentação sobre [pontos de dados faturáveis](https://www.braze.com/docs/user_guide/onboarding_with_braze/data_points/#billable-data-points) para obter mais informações.

### Obter detalhes de configuração necessários {#configuration-details}

Para conectar a rede Edge à [!DNL Braze], são necessárias as seguintes entradas:

| Tipo de chave | Descrição | Exemplo |
| --- | --- | --- |
| [!DNL Braze] Instância | O endpoint REST associado à variável [!DNL Braze] conta. Consulte a [!DNL Braze] documentação sobre [instâncias](https://www.braze.com/docs/user_guide/administrative/access_braze/braze_instances) para orientação. | `https://rest.iad-03.braze.com` |
| Chave de API | O [!DNL Braze] Chave da API associada à [!DNL Braze] conta. <br/>Consulte a [!DNL Braze] documentação sobre [Chave de API REST](https://www.braze.com/docs/api/basics/#rest-api-key) para orientação. | `YOUR-BRAZE-REST-API-KEY` |

### Criar um segredo

Crie um novo [segredo de encaminhamento de evento](../../../ui/event-forwarding/secrets.md) e defina o valor como [[!DNL Braze] Chave da API](#configuration-details). Isso será usado para autenticar a conexão com sua conta enquanto mantém o valor protegido.

## Instalar e configurar o [!DNL Braze] extensão {#install}

Para instalar a extensão, [criar uma propriedade de encaminhamento de evento](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Selecionar **[!UICONTROL Extensões]** no painel de navegação esquerdo. No **[!UICONTROL Catálogo]** guia , selecione **[!UICONTROL Instalar]** no cartão para o [!DNL Braze] extensão.

![Instale o [!DNL Braze] extensão.](../../../images/extensions/server/braze/install-extension.png)

Na próxima tela, insira o seguinte [valores de configuração](#configuration-details) de que você já se reuniu [!DNL Braze]:

- **[!UICONTROL URL do Rest Endpoint]**: Você pode inserir o valor de [!DNL Braze] URL do ponto de extremidade rest como texto simples na entrada fornecida.
- **[!UICONTROL Chave da API]**: Selecione o [elemento de dados secretos](#create-a-secret) que você criou anteriormente, que contém o [!DNL Braze] Chave da API.

Selecione **[!UICONTROL Salvar]** ao concluir.

![O [!DNL Braze] página de configuração da extensão.](../../../images/extensions/server/braze/configure-extension.png)

## Crie um [!DNL Send Event] regra {#tracking-rule}

Depois de instalar a extensão, crie um novo encaminhamento de evento [regra](../../../ui/managing-resources/rules.md) e configure as condições conforme desejado. Ao configurar as ações para a regra, selecione o **[!UICONTROL Bico]** e selecione **[!UICONTROL Enviar evento]** para o tipo de ação.

![Adicione uma configuração de ação da regra de encaminhamento de eventos.](../../../images/extensions/server/braze/braze-event-action.png)

**[!UICONTROL Identificação do usuário]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL ID de usuário externo] | UUID ou GUID longa, aleatória e bem distribuída. Se você escolher um método diferente para nomear suas IDs de usuário, elas também devem ser longas, aleatórias e bem distribuídas. Saiba mais sobre [convenção de nomenclatura de IDs de usuário sugerida](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL ID de usuário do Brasil] | Identificador de usuário do Brasil. |
| [!UICONTROL Alias do usuário] | Um alias serve como um identificador de usuário exclusivo alternativo. Use aliases para identificar usuários em diferentes dimensões que a ID do usuário principal. <br><br> O objeto alias do usuário consiste em duas partes: um alias_name para o próprio identificador e um alias_label indicando o tipo de alias. Os usuários podem ter vários aliases com rótulos diferentes, mas apenas um alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular o evento a um usuário, é necessário preencher a variável [!UICONTROL ID de usuário externo] ou o [!UICONTROL Identificador de usuário do Brasil] ou o [!UICONTROL Alias do usuário] seção.

**[!UICONTROL Dados do evento]**

| Entrada | Descrição | Obrigatório |
| --- | --- | --- |
| [!UICONTROL Nome do evento &#x200B;] | Nome do evento. | Sim |
| [!UICONTROL Hora do evento ] | Data-hora como string em ISO 8601 ou em `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sim |
| [!UICONTROL Identificador do aplicativo] | O identificador do aplicativo ou <strong>app_id</strong> O é um parâmetro que associa a atividade a um aplicativo específico no seu grupo de aplicativos. Ela designa o aplicativo no grupo de aplicativos com o qual você está interagindo. Saiba mais sobre o [Tipos de identificador de API](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL &#x200B; de Propriedades do Evento] | Um objeto JSON que contém propriedades personalizadas do evento. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> O **[!UICONTROL Evento de envio do Brasil]** a ação requer apenas uma **[!UICONTROL Nome do evento]** e **[!UICONTROL Hora do evento]** a ser especificado, mas você deve incluir o máximo possível de informações no campo de propriedades personalizadas. Para obter detalhes sobre o [!DNL Braze] objeto de evento, consulte a [documentação oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos do usuário]**

Os atributos de usuário podem ser um objeto JSON contendo campos que criarão ou atualizarão um atributo com o nome e o valor fornecidos no perfil de usuário especificado. As seguintes propriedades são compatíveis:

| Atributo do usuário | Descrição |
| --- | --- |
| [!UICONTROL Nome] |  |
| [!UICONTROL Sobrenome] |  |
| [!UICONTROL Telefone] |  |
| [!UICONTROL Email] |  |
| [!UICONTROL Gênero] | Uma das seguintes strings: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (outro), &quot;N&quot; (não aplicável), &quot;P&quot; (preferir não dizer). |
| [!UICONTROL Cidade] |  |
| [!UICONTROL País] | País como uma sequência de caracteres em [ISO-3166-1 alfa-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Idioma] | Idioma como uma sequência de caracteres em [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Data de nascimento] | Sequência de caracteres no formato &quot;AAAA-MM-DD&quot; (por exemplo, 1980-12-21). |
| [!UICONTROL Fuso Horário] | Nome do fuso horário de [Banco de Dados do Fuso Horário IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por exemplo, ’América/Nova_Iorque’ ou ’Hora de Leste (EUA e Canadá)’). |
| [!UICONTROL Facebook] | Hash contendo qualquer id (string), curtidas (matriz de strings), num_friends (número inteiro). |
| [!UICONTROL Twitter] | Hash contendo qualquer um dos id (número inteiro), nome_da_tela (sequência, identificador de Twitter), seguers_count (número inteiro), friends_count (número inteiro), status_count(número inteiro). |

{style="table-layout:auto"}

## Crie um [!DNL Send Purchase Event] regra {#purchase-rule}

Depois de instalar a extensão, crie um novo encaminhamento de evento [regra](../../../ui/managing-resources/rules.md) e configure as condições conforme desejado. Ao configurar as ações para a regra, selecione o **[!UICONTROL Bico]** e selecione **[!UICONTROL Enviar evento de compra]** para o tipo de ação.

![Adicione uma configuração de ação de encaminhamento de regra do tipo de ação de Compra Brasileira.](../../../images/extensions/server/braze/braze-purchase-event-action.png)

**[!UICONTROL Identificação do usuário]**

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL ID de usuário externo] | UUID ou GUID longa, aleatória e bem distribuída. Se você escolher um método diferente para nomear suas IDs de usuário, elas também devem ser longas, aleatórias e bem distribuídas. Saiba mais sobre [convenção de nomenclatura de IDs de usuário sugerida](https://www.braze.com/docs/developer_guide/platform_integration_guides/web/analytics/setting_user_ids#suggested-user-id-naming-convention). |
| [!UICONTROL ID de usuário do Brasil] | Identificador de usuário do Brasil. |
| [!UICONTROL Alias do usuário] | Um alias serve como um identificador de usuário exclusivo alternativo. Use aliases para identificar usuários em diferentes dimensões que a ID do usuário principal. <br><br> O objeto alias do usuário consiste em duas partes: um alias_name para o próprio identificador e um alias_label indicando o tipo de alias. Os usuários podem ter vários aliases com rótulos diferentes, mas apenas um alias_name por alias_label. |

{style="table-layout:auto"}

>[!NOTE]
>
> Para vincular o evento a um usuário, é necessário concluir a [!UICONTROL ID de usuário externo] , o [!UICONTROL Identificador de usuário do Brasil] ou o [!UICONTROL Alias do usuário] seção.

**[!UICONTROL Dados de compra]**

| Entrada | Descrição | Obrigatório |
| --- | --- | --- |
| [!UICONTROL Identificação do produto &#x200B;] | Identificador para a compra. (por exemplo, Nome do produto ou Categoria do produto) | Sim |
| [!UICONTROL Hora de compra ] | Data-hora como string em ISO 8601 ou em `yyyy-MM-dd'T'HH:mm:ss:SSSZ` formato. | Sim |
| [!UICONTROL Moeda &#x200B;] | Moeda como sequência de caracteres em [ISO 4217](https://pt.wikipedia.org/wiki/ISO_4217) Formato do código monetário alfabético. | Sim |
| [!UICONTROL Preço &#x200B;] | Preço. | Sim |
| [!UICONTROL Quantidade &#x200B;] | Se não for fornecido, o valor padrão será 1. O valor máximo deve ser inferior a 100. |  |
| [!UICONTROL Identificador do aplicativo] | O identificador do aplicativo ou <strong>app_id</strong> O é um parâmetro que associa a atividade a um aplicativo específico no seu grupo de aplicativos. Ela designa o aplicativo no grupo de aplicativos com o qual você está interagindo. Saiba mais sobre o [Tipos de identificador de API](https://www.braze.com/docs/api/identifier_types/). |  |
| [!UICONTROL &#x200B; de propriedades de compra] | Um objeto JSON contendo propriedades personalizadas da compra. |  |

{style="table-layout:auto"}

>[!NOTE]
>
> O **[!UICONTROL Evento de envio do Brasil]** a ação requer apenas uma **[!UICONTROL Nome do evento]** e **[!UICONTROL Hora do evento]** a ser especificado, mas você deve incluir o máximo possível de informações no campo de propriedades personalizadas. Para obter detalhes sobre o [!DNL Braze] objeto de evento, consulte a [documentação oficial](https://www.braze.com/docs/api/objects_filters/event_object/).

**[!UICONTROL Atributos do usuário]**

Os atributos de usuário podem ser um objeto JSON contendo campos que criarão ou atualizarão um atributo com o nome e o valor fornecidos no perfil de usuário especificado. As seguintes propriedades são compatíveis:

| Atributo do usuário | Descrição |
| --- | --- |
| [!UICONTROL Nome] |  |
| [!UICONTROL Sobrenome] |  |
| [!UICONTROL Telefone] |  |
| [!UICONTROL Email] |  |
| [!UICONTROL Gênero] | Uma das seguintes strings: &quot;M&quot;, &quot;F&quot;, &quot;O&quot; (outro), &quot;N&quot; (não aplicável), &quot;P&quot; (preferir não dizer). |
| [!UICONTROL Cidade] |  |
| [!UICONTROL País] | País como uma sequência de caracteres em [ISO-3166-1 alfa-2](https://en.wikipedia.org/wiki/ISO_3166-1_alpha-2) formato. |
| [!UICONTROL Idioma] | Idioma como uma sequência de caracteres em [ISO-639-1](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes) formato. |
| [!UICONTROL Data de nascimento] | Sequência de caracteres no formato &quot;AAAA-MM-DD&quot; (por exemplo, 1980-12-21). |
| [!UICONTROL Fuso Horário] | Nome do fuso horário de [Banco de Dados do Fuso Horário IANA](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) (por exemplo, ’América/Nova_Iorque’ ou ’Hora de Leste (EUA e Canadá)’). |
| [!UICONTROL Facebook] | Hash contendo qualquer id (string), curtidas (matriz de strings), num_friends (número inteiro). |
| [!UICONTROL Twitter] | Hash contendo qualquer um dos id (número inteiro), nome_da_tela (sequência, identificador de Twitter), seguers_count (número inteiro), friends_count (número inteiro), status_count(número inteiro). |

{style="table-layout:auto"}

## Validar dados no [!DNL Braze] {#validate}

Se a coleção de eventos e [!DNL Adobe Experience Platform] a integração foi bem-sucedida, você verá os eventos no [!DNL Braze] console ao [visualizar perfis de usuário](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/). Especificamente, os novos dados de evento enviados para o [!DNL Braze] é refletida na variável [!DNL Purchases] seção de um usuário específico [guia visão geral](https://www.braze.com/docs/user_guide/engagement_tools/segments/user_profiles/#overview-tab).

## Próximas etapas

Este guia cobriu como enviar eventos de conversão para o [!DNL Braze] utilizando o encaminhamento de eventos. Para obter mais detalhes sobre aplicativos downstream de dados de eventos enviados para o [!DNL Braze], consulte o [documentação oficial](https://www.braze.com/docs).

Para obter mais informações sobre os recursos de encaminhamento de eventos no Experience Platform, consulte o [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
