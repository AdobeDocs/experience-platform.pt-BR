---
title: Visão geral da extensão do Mailchimp
description: Use o encaminhamento de eventos para acionar emails do Mailchimp.
type: Documentation
feature: Data Collection, Event Forwarding
level: Beginner
role: User, Developer, Admin
topic: Integrations
exl-id: a52870c4-10e6-45a0-a502-f48da3398f3f
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1251'
ht-degree: 5%

---

# Visão geral da extensão de encaminhamento de eventos do Mailchimp

>[!NOTE]
>  
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleta de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](https://experienceleague.adobe.com/docs/experience-platform/tags/term-updates.html?lang=pt-BR) para obter uma referência consolidada das alterações de terminologia.

A extensão [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) do Mailchimp envia eventos para a API de marketing do Mailchimp que podem acionar emails para campanhas de marketing, jornadas ou transações do Mailchimp.

Este documento aborda como definir a extensão e configurar regras usando a ação Adicionar evento.

## Pré-requisitos

Este documento supõe que você esteja familiarizado com os produtos Mailchimp relevantes aproveitados pela extensão. Para obter mais informações, consulte a documentação de ajuda do Mailchimp para [campanhas](https://mailchimp.com/help/getting-started-with-campaigns/), [jornadas](https://mailchimp.com/help/about-customer-journeys/) e [transações](https://mailchimp.com/help/transactional/).

Uma conta do Mailchimp é necessária para usar esta extensão. Você pode se inscrever para obter uma conta [aqui](https://login.mailchimp.com/signup/). No painel de contas do Mailchimp, anote os seguintes valores para uso neste guia:

- Seu prefixo de domínio do Mailchimp
- Sua chave de API
- A ID do público-alvo
- O endereço de email padrão &quot;de&quot;

Dependendo do seu plano de conta do Mailchimp, você pode ter acesso limitado às ferramentas de Jornada ao cliente do Mailchimp.

>[!TIP]
>  
>Se você estiver usando automações do Mailchimp, como emails transacionais ou Jornadas do cliente, as etapas e telas poderão ser um pouco diferentes daquelas listadas aqui. No entanto, você ainda precisa das mesmas informações para usar essa extensão, conforme descrito acima. Consulte a [Central de Ajuda do Mailchimp](https://mailchimp.com/help/) para obter detalhes sobre cada um desses valores para sua conta e seu plano específicos.

### Prefixo do domínio

Depois de fazer logon no Mailchimp e acessar a exibição de Painel, a barra de endereços do navegador deve exibir uma URL como `https://us11.admin.mailchimp.com` ou apenas `us11.admin.mailchimp.com`. Neste exemplo, o prefixo `us11` é apenas um espaço reservado e seu valor será diferente. Registre seu URL com seu prefixo para uma etapa posterior.

### Chave de API

Para localizar a chave de API da sua conta, selecione o ícone de perfil na interface do usuário do Mailchimp e, em seguida, selecione **Perfil**. Você deve ver uma URL como `https://us11.admin.mailchimp.com/account/profile/`, mas com **seu** prefixo em vez de `us11`.

Selecione **Extras**, depois **Chaves de API**:

![Menu Extras, link de chaves de API](../../../images/extensions/server/mailchimp/menu-API-keys.png)

Em **Suas chaves de API**, você pode escolher uma chave existente ou selecionar **Criar uma Chave** para criar uma nova. Você pode criar uma nova chave para usar especificamente com essa extensão. Copie a chave de API e salve-a para uma etapa posterior. Para obter mais detalhes, consulte a documentação do Mailchimp sobre como [gerar sua chave de API](https://mailchimp.com/developer/marketing/guides/quick-start/#generate-your-api-key).

### ID de público-alvo e endereço do remetente

Selecione **Público-alvo** na navegação à esquerda e **Painel de público-alvo**. Em seguida, selecione o público-alvo que deseja usar com essa extensão. Para saber mais, consulte o documento Mailchimp sobre [criação de um público-alvo](https://mailchimp.com/help/create-audience/).

Com seu público criado e selecionado, selecione a lista suspensa **Gerenciar público-alvo** e escolha **Configurações**. Esta tela mostra várias configurações para o seu público-alvo.

Na parte inferior da tela Configurações, você deve ver `Unique id for audience [audience name]`, onde `[audience name]` é o nome do seu público-alvo real. Copie a ID de público-alvo e salve-a para uma etapa posterior.

Selecione o **nome e padrões do público-alvo** e confirme se o **Padrão do endereço de email** tem o valor correto para suas campanhas. Observe que a ID de público-alvo também está listada na parte superior desta página e tem o mesmo valor copiado na última etapa.

## Automações do Mailchimp

Dependendo do seu plano do Mailchimp e se você usa emails transacionais, Jornadas do cliente ou outras automações do Mailchimp, suas configurações específicas de jornada podem variar.

>[!IMPORTANT]
>  
>O nome do evento que você escolheu para acionar sua automação ou jornada no Mailchimp é o mesmo nome de evento que deve ser enviado com essa extensão. Observe o nome do evento na automação do Mailchimp e salve-o para uma etapa posterior.

## Instalação e configuração

Esta seção lista as etapas para instalar e configurar a extensão. Para salvar com segurança a chave de API do Mailchimp, você deve usar os [segredos](../../../ui/event-forwarding/secrets.md) do encaminhamento de eventos.

### Criar um segredo e um elemento de dados

Em uma propriedade de encaminhamento de eventos, [crie um [!UICONTROL Token] segredo](../../../ui/event-forwarding/secrets.md#token) chamado `Mailchimp API Key`.

Em seguida, [crie um elemento de dados](../../../ui/managing-resources/data-elements.md#create-a-data-element) usando a extensão [!UICONTROL Core] e um tipo de elemento de dados [!UICONTROL Secret] para fazer referência ao segredo `Mailchimp API Key` que você acabou de criar. Digite `Mailchimp Token` como o nome do elemento de dados.

### Instalar e configurar a extensão

Na mesma propriedade de encaminhamento de eventos, selecione **[!UICONTROL Extensions],** e **[!UICONTROL Catalog]** para exibir as extensões disponíveis para instalação. Aqui, pesquise a extensão Mailchimp e selecione **[!UICONTROL Install]**.

![Instalar extensão do Mailchimp](../../../images/extensions/server/mailchimp/install.png)

A tela de configuração é exibida. Em **[!UICONTROL Mailchimp Server Prefix Domain Name]**, insira o domínio que você copiou anteriormente da sua conta do Mailchimp, incluindo o prefixo de domínio exclusivo.

>[!IMPORTANT]
>
>Não inclua `http://` ou `https://` neste campo.

![Configuração de extensão](../../../images/extensions/server/mailchimp/mailchimp-domain.png)

Em **[!UICONTROL Mailchimp token]**, selecione o ícone de elemento de dados e escolha o elemento de dados `Mailchimp Token` criado anteriormente. Selecione **[!UICONTROL Save]** para salvar as alterações.

A extensão agora está instalada e configurada para uso na propriedade.

## Coleção de dados

Ao usar esta extensão em uma [regra](../../../ui/managing-resources/rules.md), há vários valores de dados que a extensão envia para o Mailchimp com cada evento. Para uma implementação típica, você pode configurar a [extensão do Adobe Experience Platform Web SDK](../../client/web-sdk/overview.md) para enviar esses dados a [!DNL Experience Platform Edge Network] para serem usados pela extensão na propriedade de encaminhamento de eventos.

Os dados exigidos por essa extensão podem ser enviados do Web SDK como dados XDM (usando o objeto [`xdm`](/help/collection/js/commands/sendevent/xdm.md)) ou dados não XDM (usando o objeto [`data`](/help/collection/js/commands/sendevent/data.md)).

Por exemplo, se um cliente fizer uma compra ou se registrar para um evento em seu site, você poderá enviar um email de confirmação por meio do Mailchimp com essa extensão. Depois de enviar as informações necessárias do Web SDK para a Edge Network, a extensão acionará o email com o Mailchimp.

![Adicionar configuração de ação de evento](../../../images/extensions/server/mailchimp/action-configurations.png)

### Elementos de dados

A captura de tela na seção anterior mostra os dados que você pode enviar com cada evento desta extensão para o Mailchimp. Depois de configurar o Web SDK para enviar esses dados para a Edge Network, você pode criar elementos de dados na propriedade de encaminhamento de eventos para que a extensão possa acessar esses valores.

A tabela abaixo fornece mais detalhes para cada valor possível.

| Nome | Exemplo de caminho | Tipo | Descrição | Obrigatório | Limites |
|:---|:---:|:---:|:---|:---:|:---|
| `email` | `arc.event.xdm._tenant.emailId`<br /> ou<br /> `arc.event.data._tenant.emailId` | String | O endereço que recebe o email | **Sim** | Deve existir no Público do Mailchimp |
| `listId` | `arc.event.xdm._tenant.listId`<br /> ou<br /> `arc.event.data._tenant.listid` | String | ID do público-alvo | **Sim** | Deve corresponder a uma ID de público-alvo existente |
| `name` | `arc.event.xdm._tenant.name`<br /> ou<br /> `arc.event.data._tenant.name` | String | O nome do evento | **Sim** | 2-30 caracteres de comprimento |
| `properties` | `arc.event.xdm._tenant.properties`<br /> ou<br /> `arc.event.data._tenant.properties` | Objeto | Uma lista opcional de propriedades no formato JSON com detalhes sobre o evento | Não |  |
| `isSyncing` | `arc.event.xdm._tenant.isSyncing`<br /> ou<br /> `arc.event.data._tenant.isSyncing` | booleano | Eventos criados com `is_syncing` definido como `true` **não** acionarão automações | Não |  |
| `occurredAt` | `arc.event.xdm._tenant.occuredAt`<br /> ou `arc.event.data._tenant.occuredAt` | String | Um carimbo de data e hora ISO 8601 de quando o evento ocorreu | Não |  |

{style="table-layout:auto"}

>[!IMPORTANT]
>  
>Os valores **Caminho de exemplo** acima são apenas exemplos. Os nomes de campos e os [caminhos](../../../ui/event-forwarding/overview.md#data-element-path) referenciados nesses elementos de dados podem ser diferentes na propriedade, dependendo de como você nomeou e configurou o Web SDK nas etapas acima.

Na propriedade de encaminhamento de eventos, você pode criar um elemento de dados para cada um dos campos descritos acima. Depois de criado, você pode fazer referência aos elementos de dados na ação [!UICONTROL Add Event] dessa extensão.

![Adicionar configuração de ação de evento](../../../images/extensions/server/mailchimp/action-configurations.png)

Agora você pode usar essa extensão e a ação Adicionar evento para acionar emails do Mailchimp para seus públicos.

## Validação de dados

Ao trabalhar com extensões de encaminhamento de eventos, o [Adobe Experience Platform Debugger](https://chrome.google.com/webstore/detail/adobe-experience-platform/bfnnokhpnncpkdmbokanobigaccjkpob) é muito útil. Na seção Logs, em Logs do Edge, você pode ver as solicitações feitas pelas regras de encaminhamento de eventos depois de serem acionadas. As capturas de tela a seguir mostram uma solicitação que está sendo feita à API do Mailchimp pela extensão.

![Adobe Experience Platform Debugger](../../../images/extensions/server/mailchimp/debugger-edge-logs.png)

No painel do Mailchimp, na exibição Feed de atividades do seu Público ou Membro de público, uma lista de eventos é fornecida para esse Público ou Membro de público. Ele deve corresponder aos eventos enviados pela extensão e mostrar todos os dados opcionais enviados, juntamente com o email ou a campanha recebida. Consulte os [Guias de ajuda de Automação do Mailchimp](https://mailchimp.com/help/automation/) para obter mais detalhes.
