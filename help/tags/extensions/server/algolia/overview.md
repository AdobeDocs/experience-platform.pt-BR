---
title: Visão geral da extensão de encaminhamento de eventos da Algolia
description: Saiba como configurar e usar a extensão de encaminhamento de eventos do Algolia no Adobe Experience Platform. Encaminhe os dados de comportamento do usuário por meio da API do Insights, configure regras, mapeie campos XDM e verifique a entrega do evento.
last-substantial-update: 2025-05-09T00:00:00Z
source-git-commit: d1b641ed0b48357a2f4b78d6829ccab52e4889ca
workflow-type: tm+mt
source-wordcount: '1076'
ht-degree: 0%

---


# Visão geral da extensão de encaminhamento de eventos do [!DNL Algolia] {#overview}

>[!NOTE]
>
>O Adobe Experience Platform Launch agora faz parte das tecnologias de coleta de dados da Adobe Experience Platform. Como resultado, foram feitas atualizações de terminologia na documentação do produto. Para obter uma lista abrangente dessas alterações, consulte o [guia de atualizações de terminologia](../../../../tags/term-updates.md).

Use o [!DNL Algolia] para fornecer experiências de pesquisa rápidas, relevantes e personalizadas. Com a otimização baseada em IA, você pode aprimorar os resultados da pesquisa e as recomendações para ajudar os usuários a encontrar rapidamente os produtos, o conteúdo ou as informações de que precisam.

Use a extensão de encaminhamento de eventos do [!DNL Algolia] para enviar eventos de comportamento de usuário ao [!DNL Algolia] por meio do [!DNL Insights API]. Esses dados comportamentais permitem recomendações alimentadas por IA, experiências personalizadas e recursos de pesquisa inteligentes.

## Pré-requisitos {#prerequisites}

Antes de instalar a extensão, verifique se você tem uma conta do [!DNL Algolia] com acesso ao [!DNL Insights API]. Se você não tiver uma conta, [inscreva-se](https://dashboard.algolia.com/users/sign_up) e habilite o acesso à API.

Verifique também se você entende como usar o [!DNL Algolia] [!DNL Insights API]. Para obter uma visão geral de como enviar eventos, consulte o [envio de eventos com a API de Insights](https://www.algolia.com/doc/guides/sending-events/getting-started/).

Obtenha os seguintes valores do painel da conta do [!DNL Algolia]:
- **[!UICONTROL ID do Aplicativo]**
- **[!UICONTROL Chave de API de Pesquisa]**
- **[!UICONTROL Nome do Índice]**

## Instalar a extensão {#install}

Para instalar a extensão [!DNL Algolia], siga estas etapas:

Navegue até **[!UICONTROL Coleção de Dados]** em [!DNL Adobe Experience Platform]. Selecione a guia **[!UICONTROL Extensões]**.

Abra o **[!UICONTROL Catálogo]**, localize a extensão **[!UICONTROL Encaminhamento de Eventos da Algolia]** e selecione **[!UICONTROL Instalar]**.

![O processo de instalação da extensão Algolia Event Forwarding no Adobe Experience Platform](../../../images/extensions/server/algolia/install-extension.png)

### Configurar a extensão {#configure-extension}

Para configurar a extensão de encaminhamento de eventos do [!DNL Algolia], navegue até a guia **[!UICONTROL Extensões]**, selecione a extensão **[!UICONTROL Algólia]** e selecione **[!UICONTROL Configurar]**.

![Tela de configuração para a extensão de encaminhamento de eventos da Algólia no Adobe Experience Platform](../../../images/extensions/server/algolia/configure.png)

| Propriedade | Descrição |
|----------|-------------|
| **[!UICONTROL Application ID]** | Insira a [!UICONTROL ID do Aplicativo] encontrada no Painel da Algólia na seção [Chaves da API](https://www.algolia.com/account/api-keys/all). |
| **[!UICONTROL Chave de API de Pesquisa]** | Insira a [!UICONTROL Chave de API de Pesquisa] encontrada no Painel da Algólia na seção [Chaves de API](https://www.algolia.com/account/api-keys/all). |
| **[!UICONTROL Nome do Índice]** | Digite o [!UICONTROL Nome do Índice] que contém seus produtos ou conteúdo. Esse índice é usado como valor padrão. |

{style="table-layout:auto"}

## [!DNL Algolia] tipos de ação de extensão do encaminhamento de eventos {#action-types}

A extensão de encaminhamento de eventos [!DNL Algolia] oferece um único tipo de ação que pode ser usado na seção **[!UICONTROL Then]** de uma regra:

### Enviar evento {#send-event}

Configure a ação **[!UICONTROL Enviar evento]** para encaminhar eventos para [!DNL Algolia]:

Selecione **[!UICONTROL Regras]** > **[!UICONTROL Adicionar regra]** ou selecione uma regra existente. Na parte **[!UICONTROL Then]** da regra, adicione uma ação e selecione **[!UICONTROL Extensão]**: [!DNL Algolia] Encaminhamento de Eventos > **[!UICONTROL Tipo de Ação]**: **[!UICONTROL Enviar Eventos]**.

![Configuração da ação Enviar Evento na extensão de encaminhamento de eventos da Algólia.](../../../images/extensions/server/algolia/send-event.png)

## Implementar o grupo de campos de evento [!DNL Algolia] {#algolia-field-group}

Adicione o grupo de campos de eventos [!DNL Algolia] ao esquema antes de usar a extensão de encaminhamento de eventos [!DNL Algolia]. É um dos grupos de campos padrão fornecidos pelo Experience Platform.

![Configuração do grupo de campos de evento da Algólia](../../../images/extensions/server/algolia/algolia-field-groups.png)

### Adicionar o grupo de campos de evento [!DNL Algolia] ao esquema {#add-algolia-field-group}

Para adicionar o grupo de campos de evento [!DNL Algolia]:

Navegue até **[!UICONTROL Esquemas]** e selecione **[!UICONTROL Procurar]**.

Adicione um novo esquema ou atualize um esquema existente usado para enviar eventos da Web e passe o mouse sobre o ícone **[!UICONTROL Adicionar]**. Digite *[!DNL Algolia]* na caixa de pesquisa para restringir os resultados.

Selecione o **[!DNL Algolia]Detalhes do evento** grupo de campos > **[!UICONTROL Botão Adicionar grupo de campos]** > **[!UICONTROL Salvar]**.

![Configuração do grupo de campos de perfil da Algólia no Experience Platform](../../../images/extensions/server/algolia/algolia-profile-field-group.png)

### Mapear e enviar dados usando a marca [!UICONTROL Coleção de dados]

A extensão de encaminhamento de eventos do [!DNL Algolia] pode ser usada com o **[!DNL Adobe Experience Platform Web SDK]** para enviar dados do seu site para o [!DNL Algolia]. Isso é feito criando uma propriedade de marca, mapeando dados para o objeto [!DNL XDM] e configurando regras para enviar eventos.

#### Etapa 1: criar uma propriedade de tag com o SDK da Web

1. Crie uma propriedade de tag.
2. Instale a extensão [!DNL Adobe Experience Platform Web SDK].
3. Use esta extensão para mapear dados do HTML para o grupo de campos **[!DNL Algolia]Evento**.

![Exemplo de um conjunto de dados do HTML que está sendo mapeado para o grupo de campos de evento da Algolia](../../../images/extensions/server/algolia/html-dataset.png)

#### Etapa 2: Criar um elemento de dados para mapeamento de [!DNL XDM]

1. Criar um [!UICONTROL Elemento de Dados] usando o **[!DNL Adobe Experience Platform Web SDK]**.
2. Selecione **[!UICONTROL objeto XDM]** como o tipo de elemento de dados.
3. Mapeie seus dados para os campos [!DNL XDM] apropriados, garantindo que os campos específicos de [!DNL Algolia] sejam preenchidos.

![](../../../images/extensions/server/algolia/xdm-mapping.png)

#### Etapa 3: criar uma regra para enviar eventos

1. Crie uma nova regra na propriedade da tag.
2. Adicione os acionadores de evento necessários, como carregamento de página ou eventos de clique.
3. Adicionar uma ação usando **[!DNL Adobe Experience Platform Web SDK]**.
4. Selecione **[!UICONTROL Enviar evento]** como o tipo de ação.
5. Configure a ação para usar seu elemento de dados [!DNL XDM].

![Exemplo de configuração de uma ação de regra na extensão de encaminhamento de eventos da Algolia](../../../images/extensions/server/algolia/rule-action.png)

#### Etapa 4: publicar e testar

1. Publique as alterações nas regras e na extensão do seu ambiente de destino.
2. Use o [!DNL Adobe Experience Platform Debugger] para verificar se os dados foram enviados ao Adobe Experience Platform e encaminhados a [!DNL Algolia].

![Configurar uma regra para enviar eventos usando a extensão Algolia](../../../images/extensions/server/algolia/adobe-debugger.png)

### Verificar eventos em [!DNL Algolia]

Após configurar a extensão de encaminhamento de eventos do [!DNL Algolia], verifique se os eventos estão sendo enviados e recebidos corretamente seguindo estas etapas:

Navegue até o painel [!DNL Algolia] e vá até **[!UICONTROL Fontes de Dados > Eventos > Depurador]**.

Selecione o evento que corresponde ao evento enviado da extensão de encaminhamento de eventos de [!DNL Algolia] e verifique se os dados esperados estão presentes no evento.

![Verificar eventos no Algolia Debugger](../../../images/extensions/server/algolia/algolia-debugger.png)

## Cenários comuns de implementação

Use a extensão de encaminhamento de eventos do [!DNL Algolia] para capturar e enviar dados de interação do usuário para vários casos de uso, melhorando a relevância da pesquisa e a personalização.

### Rastrear exibições de produto ou conteúdo

Use a extensão para monitorar quando os usuários exibem páginas de produto ou conteúdo, ajudando [!DNL Algolia] a entender os interesses dos usuários.

### Rastrear eventos de conversão

Rastreie eventos de adição ao carrinho, compras e outros eventos de conversão para otimizar as recomendações habilitadas por IA do [!DNL Algolia].

## Solução de problemas

Se você encontrar problemas ao implementar a extensão de encaminhamento de eventos do [!DNL Algolia], considere as seguintes etapas de solução de problemas:

### Eventos não aparecem em [!DNL Algolia]

Se os eventos não aparecerem em [!DNL Algolia], verifique o seguinte:

- **Verificar Credenciais da API**: certifique-se de que a **[!UICONTROL ID do Aplicativo]** e a **[!UICONTROL Chave da API]** correspondam aos valores no painel [!DNL Algolia].
- **Verificar Depurador de Eventos**: Use o [!DNL Algolia] Depurador de Eventos para confirmar se os eventos estão sendo recebidos. Caso contrário, verifique a configuração da regra de encaminhamento de eventos.
- **Inspecionar Mapeamento XDM**: certifique-se de que todos os campos obrigatórios no esquema [!DNL Algolia] estejam mapeados corretamente no objeto [!DNL XDM].

### Dados de evento incorretos

- Certifique-se de que o elemento de dados do objeto [!DNL XDM] esteja mapeado com precisão para o esquema [!DNL Algolia], com todos os campos obrigatórios.
- Confirme se os parâmetros de evento correspondem ao formato e à estrutura esperados descritos na documentação da API do Insights do [!DNL Algolia].

## Próximas etapas

Este guia abordou como enviar dados para [!DNL Algolia] usando o [!DNL Algolia Event Forwarding Extension]. Para obter mais informações sobre os recursos de encaminhamento de eventos do [!DNL Adobe Experience Platform], leia a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).

Para obter detalhes sobre como depurar sua implementação usando o Depurador da Experience Platform e a ferramenta de Monitoramento de Encaminhamento de Eventos, leia a [Visão geral da Adobe Experience Platform Debugger](../../../../debugger/home.md) e as [Atividades de Monitor no encaminhamento de eventos](../../../ui/event-forwarding/monitoring.md).

## Recursos adicionais

- [[!DNL Algolia] Documentação da API do Insights](https://www.algolia.com/doc/rest-api/insights/)
- [[!DNL Algolia] Documentação de eventos](https://www.algolia.com/doc/guides/sending-events/getting-started/)
- [[!DNL Adobe Experience Platform] Documentação de encaminhamento de eventos](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html?lang=pt-BR)
- [[!DNL Algolia] Visão geral dos recursos de IA](https://www.algolia.com/products/ai-search/)
