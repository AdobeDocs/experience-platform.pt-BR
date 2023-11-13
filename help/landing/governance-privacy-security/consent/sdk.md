---
title: Processar dados de consentimento do cliente usando o SDK da Web da Adobe Experience Platform
description: Saiba como integrar o Adobe Experience Platform Web SDK para processar dados de consentimento do cliente no Adobe Experience Platform.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 3d0f2823dcf63f25c3136230af453118c83cdc7e
workflow-type: tm+mt
source-wordcount: '1349'
ht-degree: 2%

---

# Integrar o SDK da Web da Platform para processar dados de consentimento do cliente

O SDK da Web da Adobe Experience Platform permite recuperar os sinais de consentimento do cliente gerados pelas Plataformas de gerenciamento de consentimento (CMPs) e enviá-los à Adobe Experience Platform sempre que ocorrer um evento de alteração de consentimento.

**O SDK não faz interface com nenhum CMP pronto para uso**. Cabe a você determinar como integrar o SDK ao seu site, acompanhar as alterações de consentimento no CMP e chamar o comando apropriado. Este documento fornece orientação geral sobre como integrar sua CMP ao SDK da Web da plataforma.

## Pré-requisitos {#prerequisites}

Este tutorial presume que você já determinou como gerar dados de consentimento no CMP e criou um conjunto de dados contendo campos de consentimento que estão em conformidade com o padrão Adobe ou com o padrão TCF (Estrutura de transparência e consentimento) 2.0 do IAB. Se você ainda não criou esse conjunto de dados, consulte os seguintes tutoriais antes de retornar a este guia:

* [Criar um conjunto de dados usando o padrão Adobe](./adobe/dataset.md)
* [Criar um conjunto de dados usando o padrão TCF 2.0](./iab/dataset.md)

Este guia segue o fluxo de trabalho para configurar o SDK usando a extensão de tag na interface do usuário. Se você não quiser usar a extensão e preferir incorporar diretamente a versão independente do SDK ao seu site, consulte os seguintes documentos em vez deste guia:

* [Configurar uma sequência de dados](../../../datastreams/overview.md)
* [Instalar o SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [Configurar o SDK para comandos de consentimento](../../../edge/consent/supporting-consent.md)

As etapas de instalação neste guia exigem um entendimento prático das extensões de tag e como elas são instaladas em aplicativos web. Consulte a seguinte documentação para obter mais informações:

* [Visão geral das tags](../../../tags/home.md)
* [Manual de início rápido](../../../tags/quick-start/quick-start.md)
* [Visão geral da publicação](../../../tags/ui/publishing/overview.md)

## Configurar um fluxo de dados

Para que o SDK envie dados para o Experience Platform, primeiro você deve configurar um fluxo de dados. Na interface da Coleção de dados ou na interface do Experience Platform, selecione **[!UICONTROL Datastreams]** no painel de navegação esquerdo.

Depois de criar um novo fluxo de dados ou selecionar um existente para editar, selecione o botão de alternância ao lado de **[!UICONTROL Adobe Experience Platform]**. Em seguida, use os valores listados abaixo para preencher o formulário.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Campo de sequência de dados | Valor |
| --- | --- |
| [!UICONTROL Sandbox] | O nome da plataforma [sandbox](../../../sandboxes/home.md) que contém a conexão de transmissão e os conjuntos de dados necessários para configurar o fluxo de dados. |
| [!UICONTROL Conjunto de dados do evento] | Um [!DNL XDM ExperienceEvent] que você planeja enviar dados do evento para usando o SDK. Embora você seja solicitado a fornecer um conjunto de dados de evento para criar um fluxo de dados da plataforma, observe que os dados de consentimento enviados por meio de eventos não são honrados nos fluxos de trabalho de imposição downstream. |
| [!UICONTROL Conjunto de dados do perfil] | A variável [!DNL Profile]Conjunto de dados habilitado para com campos de consentimento do cliente criados por você [anterior](#prerequisites). |

Quando terminar, selecione **[!UICONTROL Salvar]** na parte inferior da tela e continue seguindo os prompts adicionais para concluir a configuração.

## Instalar e configurar o SDK da Web da plataforma

Depois de criar um fluxo de dados conforme descrito na seção anterior, você deve configurar a extensão SDK da Web da plataforma que será implantada no site. Se você não tiver a extensão SDK instalada na propriedade da tag, selecione **[!UICONTROL Extensões]** na navegação à esquerda, seguido pelo botão **[!UICONTROL Catálogo]** guia. Em seguida, selecione **[!UICONTROL Instalar]** na extensão SDK da Platform, na lista de extensões disponíveis.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Ao configurar o SDK, em **[!UICONTROL Configurações do Edge]**, selecione o fluxo de dados criado na etapa anterior.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Selecionar **[!UICONTROL Salvar]** para instalar a extensão.

### Criar um elemento de dados para definir o consentimento padrão

Com a extensão SDK instalada, você tem a opção de criar um elemento de dados para representar o valor de consentimento padrão da coleta de dados (`collect.val`) para seus usuários. Isso pode ser útil se você quiser ter valores padrão diferentes dependendo do usuário, como `pending` para os utilizadores da União Europeia e `in` para usuários da América do Norte.

Nesse caso de uso, você pode implementar o seguinte para definir o consentimento padrão com base na região do usuário:

1. Determine a região do usuário no servidor Web.
1. Antes de `script` (código incorporado) na página da Web, renderize uma tag separada `script` que define uma `adobeDefaultConsent` variável com base na região do usuário.
1. Configure um elemento de dados que use o `adobeDefaultConsent` JavaScript e use esse elemento de dados como o valor de consentimento padrão para o usuário.

Se a região do usuário for determinada por um CMP, você poderá usar as seguintes etapas:

1. Manipular o evento &quot;CMP carregado&quot; na página.
1. No manipulador de eventos, defina uma `adobeDefaultConsent` variável com base na região do usuário e, em seguida, carregue o script da biblioteca de tags usando JavaScript.
1. Configure um elemento de dados que use o `adobeDefaultConsent` JavaScript e use esse elemento de dados como o valor de consentimento padrão para o usuário.

Para criar um elemento de dados na interface do usuário, selecione **[!UICONTROL Elementos de dados]** na navegação à esquerda, selecione **[!UICONTROL Adicionar elemento de dados]** para navegar até a caixa de diálogo de criação do elemento de dados.

Aqui, você deve criar um [!UICONTROL Variável JavaScript] elemento de dados com base em `adobeDefaultConsent`. Selecione **[!UICONTROL Salvar]** ao concluir.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Depois que o elemento de dados é criado, navegue de volta para a página de configuração da extensão SDK da Web. No [!UICONTROL Privacidade] , selecione **[!UICONTROL Fornecido pelo elemento de dados]** e use a caixa de diálogo fornecida para selecionar o elemento de dados de consentimento padrão criado anteriormente.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Implantar a extensão no site

Após concluir a configuração da extensão, ela poderá ser integrada ao seu site. Consulte a [guia de publicação](../../../tags/ui/publishing/overview.md) na documentação de tags, para obter informações detalhadas sobre como implantar a build de biblioteca atualizada.

## Execução de comandos de alteração de consentimento {#commands}

Depois de integrar a extensão SDK ao seu site, você pode começar a usar o SDK da Web da plataforma `setConsent` comando para enviar dados de consentimento à Platform.

A variável `setConsent` O comando executa duas ações:

1. Atualiza os atributos de perfil do usuário diretamente na Loja de perfis. Isso não envia dados para o data lake.
1. Cria um [Evento de experiência](../../../xdm/classes/experienceevent.md) que registra uma conta com carimbo de data e hora do evento de alteração de consentimento. Esses dados são enviados diretamente para o data lake e podem ser usados para rastrear as alterações de preferência de consentimento ao longo do tempo.

### Quando chamar `setConsent`

Há dois cenários em que `setConsent` deve ser chamado em seu site:

1. Quando o consentimento é carregado na página (em outras palavras, em cada carregamento de página)
1. Como parte de um gancho CMP ou ouvinte de eventos que detecta alterações nas configurações de consentimento

### `setConsent` sintaxe

>[!NOTE]
>
>Para obter uma introdução à sintaxe comum para comandos do SDK da Platform, consulte o documento em [execução de comandos](../../../edge/fundamentals/executing-commands.md).

A variável `setConsent` O comando espera dois argumentos:

1. Uma string que indica o tipo de comando (nesse caso, `"setConsent"`)
1. Um objeto de carga que contém uma única propriedade de tipo de matriz: `consent`. A variável `consent` a matriz deve conter pelo menos um objeto que forneça os campos de consentimento necessários para o padrão Adobe.

Os campos de consentimento obrigatórios para o padrão Adobe são mostrados no exemplo a seguir `setConsent` ligue para:

```js
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "2.0",
    value: {
      collect: {
        val: "y"
      },
      share: {
        val: "y"
      },
      personalize: {
        content: {
          val: "y"
        }
      },
      metadata: {
        time: "2020-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Propriedade de carga útil | Descrição |
| --- | --- |
| `standard` | O padrão de consentimento que está sendo usado. Para o padrão Adobe, esse valor deve ser definido como `Adobe`. |
| `version` | O número da versão do padrão de consentimento indicado em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento padrão Adobe. |
| `value` | As informações de consentimento atualizadas do cliente, fornecidas como um objeto XDM que está em conformidade com a estrutura dos campos de consentimento do conjunto de dados habilitado para perfil. |

>[!NOTE]
>
>Se você estiver usando outros padrões de consentimento em conjunto com a `Adobe` (como `IAB TCF`), é possível adicionar outros objetos à `consent` para cada padrão. Cada objeto deve conter valores adequados para `standard`, `version`, e `value` para o padrão de consentimento que representam.

O JavaScript a seguir fornece um exemplo de uma função que lida com alterações de preferência de consentimento em um site, que pode ser usada como um retorno de chamada em um ouvinte de eventos ou em um gancho CMP:

```js
var setConsent = function () {

  // Retrieve the current consent data.
  var categories = getConsentData();

  // If the script is running on a consent change, generate a new timestamp.
  // If the script is running on page load, set the timestamp to when the consent values last changed.
  var now = new Date();
  var collectedAt = consentChanged ? now.toISOString() : categories.collectedAt;

  //  Map the consent values and timestamp to XDM
  var consentXDM = {
    collect: {
      val: categories.collect !== -1 ? "y" : "n"
    },
    personalize: {
      content: {
        val: categories.personalizeContent !== -1 ? "y" : "n"
      }
    },
    share: {
      val: categories.share !== -1 ? "y" : "n"
    },
    metadata: {
      time: collectedAt
    }
  };

  // Pass the XDM object to the Platform Web SDK
  alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: consentXDM
    }]
  });
});
```

## Tratamento de respostas do SDK

Todos [!DNL Platform SDK] Os comandos do retornam promessas que indicam se a chamada foi bem-sucedida ou falhou. Em seguida, você pode usar essas respostas para obter lógica adicional, como exibir mensagens de confirmação ao cliente. Consulte a seção sobre [lidando com sucesso ou falha](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) no guia sobre a execução de comandos do SDK para obter exemplos específicos.

Depois de fazer `setConsent` Chamadas com o SDK, você pode usar o visualizador de perfil na interface do usuário da plataforma para verificar se os dados estão chegando ao armazenamento de perfis. Consulte a seção sobre [procurar perfis por identidade](../../../profile/ui/user-guide.md#browse-identity) para obter mais informações.

## Próximas etapas

Ao seguir este guia, você configurou a extensão SDK da Web da plataforma para enviar dados de consentimento para o Experience Platform. Para obter orientação sobre como testar a implementação, consulte a documentação do padrão de consentimento que você está implementando:

* [Adobe standard](./adobe/overview.md#test)
* [TCF 2.0 padrão](./iab/overview.md#test)
