---
title: Processar dados de consentimento do cliente usando o SDK da Web da Adobe Experience Platform
description: Saiba como integrar o Adobe Experience Platform Web SDK para processar dados de consentimento do cliente no Adobe Experience Platform.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 1%

---

# Integrar o SDK da Web da Platform para processar dados de consentimento do cliente

O SDK da Web da Adobe Experience Platform permite recuperar os sinais de consentimento do cliente gerados pelas Plataformas de gerenciamento de consentimento (CMPs) e enviá-los à Adobe Experience Platform sempre que ocorrer um evento de alteração de consentimento.

**O SDK não faz interface com nenhum CMP pronto para uso**. Cabe a você determinar como integrar o SDK ao seu site, acompanhar as alterações de consentimento no CMP e chamar o comando apropriado. Este documento fornece orientação geral sobre como integrar sua CMP ao SDK da Web da plataforma.

## Pré-requisitos {#prerequisites}

Este tutorial presume que você já determinou como gerar dados de consentimento no CMP e criou um conjunto de dados contendo campos de consentimento que estão em conformidade com o padrão Adobe ou com o padrão TCF (Estrutura de transparência e consentimento) 2.0 do IAB. Se você ainda não criou esse conjunto de dados, consulte os seguintes tutoriais antes de retornar a este guia:

* [Criar um conjunto de dados usando o padrão Adobe](./adobe/dataset.md)
* [Criar um conjunto de dados usando o padrão TCF 2.0](./iab/dataset.md)

Este guia segue o fluxo de trabalho para configurar o SDK usando a extensão de tag na interface do usuário. Se você não quiser usar a extensão e preferir incorporar diretamente a versão independente do SDK ao seu site, consulte os seguintes documentos em vez deste guia:

* [Configurar uma sequência de dados](/help/datastreams/overview.md)
* [Instalar o SDK](/help/web-sdk/install/overview.md)
* [Configurar o SDK para comandos de consentimento](/help/web-sdk/commands/configure/defaultconsent.md)

As etapas de instalação neste guia exigem um entendimento prático das extensões de tag e como elas são instaladas em aplicativos web. Consulte a seguinte documentação para obter mais informações:

* [Visão geral das tags](/help/tags/home.md)
* [Manual de início rápido](/help/tags/quick-start/quick-start.md)
* [Visão geral da publicação](/help/tags/ui/publishing/overview.md)

## Configurar um fluxo de dados

Para que o SDK envie dados para o Experience Platform, primeiro você deve configurar um fluxo de dados. Na interface da Coleção de dados ou na interface do Experience Platform, selecione **[!UICONTROL Datastreams]** na navegação à esquerda.

Depois de criar uma nova sequência de dados ou selecionar uma existente para editar, selecione o botão de alternância ao lado de **[!UICONTROL Adobe Experience Platform]**. Em seguida, use os valores listados abaixo para preencher o formulário.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Campo de sequência de dados | Valor |
| --- | --- |
| [!UICONTROL Sandbox] | O nome da Platform [sandbox](../../../sandboxes/home.md) que contém a conexão de transmissão e os conjuntos de dados necessários para configurar a sequência de dados. |
| [!UICONTROL Conjunto de dados do evento] | Um conjunto de dados [!DNL XDM ExperienceEvent] que você planeja enviar dados do evento para usando o SDK. Embora você seja solicitado a fornecer um conjunto de dados de evento para criar um fluxo de dados da plataforma, observe que os dados de consentimento enviados por meio de eventos não são honrados nos fluxos de trabalho de imposição downstream. |
| [!UICONTROL Conjunto de dados do perfil] | O conjunto de dados habilitado para [!DNL Profile] com campos de consentimento do cliente que você criou [anteriormente](#prerequisites). |

Quando terminar, selecione **[!UICONTROL Salvar]** na parte inferior da tela e continue seguindo os avisos adicionais para concluir a configuração.

## Instalar e configurar o SDK da Web da plataforma

Depois de criar um fluxo de dados conforme descrito na seção anterior, você deve configurar a extensão SDK da Web da plataforma que será implantada no site. Se você não tiver a extensão SDK instalada na propriedade da marca, selecione **[!UICONTROL Extensões]** na navegação à esquerda, seguido da guia **[!UICONTROL Catálogo]**. Em seguida, selecione **[!UICONTROL Instalar]** na extensão SDK da plataforma, na lista de extensões disponíveis.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Ao configurar o SDK, em **[!UICONTROL Configurações do Edge]**, selecione a sequência de dados criada na etapa anterior.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Selecione **[!UICONTROL Salvar]** para instalar a extensão.

### Criar um elemento de dados para definir o consentimento padrão

Com a extensão SDK instalada, você tem a opção de criar um elemento de dados para representar o valor de consentimento da coleta de dados padrão (`collect.val`) para seus usuários. Isso pode ser útil se você quiser ter valores padrão diferentes dependendo do usuário, como `pending` para usuários da União Europeia e `in` para usuários da América do Norte.

Nesse caso de uso, você pode implementar o seguinte para definir o consentimento padrão com base na região do usuário:

1. Determine a região do usuário no servidor Web.
1. Antes da marca `script` (código de inserção) na página da Web, renderize uma marca `script` separada que defina uma variável `adobeDefaultConsent` com base na região do usuário.
1. Configure um elemento de dados que use a variável JavaScript `adobeDefaultConsent` e use esse elemento de dados como o valor de consentimento padrão para o usuário.

Se a região do usuário for determinada por um CMP, você poderá usar as seguintes etapas:

1. Manipular o evento &quot;CMP carregado&quot; na página.
1. No manipulador de eventos, defina uma variável `adobeDefaultConsent` com base na região do usuário e carregue o script da biblioteca de tags usando o JavaScript.
1. Configure um elemento de dados que use a variável JavaScript `adobeDefaultConsent` e use esse elemento de dados como o valor de consentimento padrão para o usuário.

Para criar um elemento de dados na interface, selecione **[!UICONTROL Elementos de Dados]** na navegação à esquerda e **[!UICONTROL Adicionar Elemento de Dados]** para navegar até a caixa de diálogo de criação do elemento de dados.

Aqui, você deve criar um elemento de dados [!UICONTROL Variável JavaScript] com base em `adobeDefaultConsent`. Selecione **[!UICONTROL Salvar]** ao concluir.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Depois que o elemento de dados é criado, navegue de volta para a página de configuração da extensão SDK da Web. Na seção [!UICONTROL Privacidade], selecione **[!UICONTROL Fornecido pelo elemento de dados]** e use a caixa de diálogo fornecida para selecionar o elemento de dados de consentimento padrão criado anteriormente.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Implantar a extensão no site

Após concluir a configuração da extensão, ela poderá ser integrada ao seu site. Consulte o [guia de publicação](../../../tags/ui/publishing/overview.md) na documentação de tags para obter informações detalhadas sobre como implantar sua build de biblioteca atualizada.

## Execução de comandos de alteração de consentimento {#commands}

Depois de integrar a extensão SDK ao seu site, você pode começar a usar o comando `setConsent` do SDK da Web da plataforma para enviar dados de consentimento à plataforma.

O comando `setConsent` executa duas ações:

1. Atualiza os atributos de perfil do usuário diretamente na Loja de perfis. Isso não envia dados para o data lake.
1. Cria um [Evento de experiência](../../../xdm/classes/experienceevent.md) que registra uma conta com carimbo de data/hora do evento de alteração de consentimento. Esses dados são enviados diretamente para o data lake e podem ser usados para rastrear as alterações de preferência de consentimento ao longo do tempo.

### Quando ligar para `setConsent`

Há dois cenários em que `setConsent` deve ser chamado no site:

1. Quando o consentimento é carregado na página (em outras palavras, em cada carregamento de página)
1. Como parte de um gancho CMP ou ouvinte de eventos que detecta alterações nas configurações de consentimento

### Sintaxe de `setConsent`

O comando [`setConsent`](/help/web-sdk/commands/setconsent.md) espera um objeto de carga que contenha uma única propriedade de tipo de matriz: `consent`. A matriz `consent` deve conter pelo menos um objeto que forneça os campos de consentimento necessários para o padrão Adobe.

Os campos de consentimento obrigatórios para o padrão Adobe são mostrados na seguinte chamada de exemplo `setConsent`:

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
        time: "YYYY-10-12T15:52:25+00:00"
      }
    }
  }]
});
```

| Propriedade de carga útil | Descrição |
| --- | --- |
| `standard` | O padrão de consentimento que está sendo usado. Para o padrão Adobe, esse valor deve ser definido como `Adobe`. |
| `version` | O número da versão do padrão de consentimento indicado em `standard`. Este valor deve ser definido como `2.0` para o processamento de consentimento padrão Adobe. |
| `value` | As informações de consentimento atualizadas do cliente, fornecidas como um objeto XDM que está em conformidade com a estrutura dos campos de consentimento do conjunto de dados habilitado para perfil. |

>[!NOTE]
>
>Se você estiver usando outros padrões de consentimento em conjunto com `Adobe` (como `IAB TCF`), poderá adicionar outros objetos à matriz `consent` para cada padrão. Cada objeto deve conter valores apropriados para `standard`, `version` e `value` para o padrão de consentimento que representam.

O JavaScript a seguir fornece um exemplo de uma função que lida com alterações de preferência de consentimento em um site, que pode ser usada como um retorno de chamada em um ouvinte de eventos ou um gancho CMP:

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

Todos os comandos [!DNL Platform SDK] retornam promessas que indicam se a chamada teve êxito ou falhou. Em seguida, você pode usar essas respostas para obter lógica adicional, como exibir mensagens de confirmação ao cliente. Consulte [Respostas de comando](/help/web-sdk/commands/command-responses.md) para obter mais informações.

Depois de fazer `setConsent` chamadas com o SDK com êxito, você pode usar o visualizador de perfil na interface do usuário da plataforma para verificar se os dados estão chegando ao repositório de perfis. Consulte a seção sobre [procura de perfis por identidade](../../../profile/ui/user-guide.md#browse-identity) para obter mais informações.

## Próximas etapas

Ao seguir este guia, você configurou a extensão SDK da Web da plataforma para enviar dados de consentimento para o Experience Platform. Para obter orientação sobre como testar a implementação, consulte a documentação do padrão de consentimento que você está implementando:

* [Adobe standard](./adobe/overview.md#test)
* [TCF 2.0 padrão](./iab/overview.md#test)
