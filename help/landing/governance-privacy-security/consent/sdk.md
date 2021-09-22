---
title: Processar dados de consentimento do cliente usando o SDK da Web da Adobe Experience Platform
topic-legacy: getting started
description: Saiba como integrar o SDK da Web da Adobe Experience Platform para processar os dados de consentimento do cliente no Adobe Experience Platform.
exl-id: 3a53d908-fc61-452b-bec3-af519dfefa41
source-git-commit: 69e510c9a0f477ad7cab530128c6728f68dfdab1
workflow-type: tm+mt
source-wordcount: '1330'
ht-degree: 1%

---

# Integre o SDK da Web da plataforma para processar os dados de consentimento do cliente

O SDK da Web da Adobe Experience Platform permite recuperar sinais de consentimento do cliente gerados pelas CMPs (Consent Management Platforms) e enviá-los para a Adobe Experience Platform sempre que um evento de alteração de consentimento ocorrer.

**O SDK não faz interface com nenhum CMPs pronto para uso**. Cabe a você determinar como integrar o SDK ao seu site, acompanhar as alterações de consentimento no CMP e chamar o comando apropriado. Este documento fornece orientação geral sobre como integrar sua CMP ao SDK da Web da plataforma.

## Pré-requisitos {#prerequisites}

Este tutorial pressupõe que você já tenha determinado como gerar dados de consentimento dentro da CMP e criado um conjunto de dados contendo campos de consentimento em conformidade com o padrão do Adobe ou com o padrão da Estrutura de transparência e consentimento (TCF) 2.0 do IAB. Se ainda não tiver criado esse conjunto de dados, consulte os seguintes tutoriais antes de retornar a este guia:

* [Criar um conjunto de dados usando o padrão Adobe](./adobe/dataset.md)
* [Criar um conjunto de dados usando o padrão TCF 2.0](./iab/dataset.md)

Este guia segue o fluxo de trabalho para configurar o SDK usando a extensão de tag na interface do usuário da coleta de dados. Se você não quiser usar a extensão e preferir incorporar diretamente a versão independente do SDK em seu site, consulte os seguintes documentos em vez deste guia:

* [Configurar um conjunto de dados](../../../edge/fundamentals/datastreams.md)
* [Instalar o SDK](../../../edge/fundamentals/installing-the-sdk.md)
* [Configurar o SDK para comandos de consentimento](../../../edge/consent/supporting-consent.md)

As etapas de instalação neste guia exigem uma compreensão funcional das extensões de tags e como elas são instaladas em aplicativos Web. Consulte a seguinte documentação para obter mais informações:

* [Visão geral das tags](../../../tags/home.md)
* [Manual de início rápido](../../../tags/quick-start/quick-start.md)
* [Visão geral da publicação](../../../tags/ui/publishing/overview.md)

## Configurar um armazenamento de dados

Para que o SDK envie dados para o Experience Platform, primeiro você deve configurar um armazenamento de dados. Na interface do usuário da coleta de dados, selecione **[!UICONTROL Datastreams]** no painel de navegação esquerdo.

Depois de criar um novo armazenamento de dados ou selecionar um existente para editar, selecione o botão de alternância ao lado de **[!UICONTROL Adobe Experience Platform]**. Em seguida, use os valores listados abaixo para preencher o formulário.

![](../../images/governance-privacy-security/consent/adobe/sdk/edge-config.png)

| Campo de fluxo de dados | Valor |
| --- | --- |
| [!UICONTROL Sandbox] | O nome da plataforma [sandbox](../../../sandboxes/home.md) que contém a conexão de transmissão e os conjuntos de dados necessários para configurar o conjunto de dados. |
| [!UICONTROL Entrada de transmissão] | Uma conexão de transmissão válida para Experience Platform. Consulte o tutorial em [criar uma conexão de transmissão](../../../ingestion/tutorials/create-streaming-connection-ui.md) se você não tiver uma entrada de transmissão existente. |
| [!UICONTROL Conjunto de dados do evento] | Um conjunto de dados [!DNL XDM ExperienceEvent] que você planeja enviar dados do evento para o usando o SDK. Embora seja necessário fornecer um conjunto de dados de evento para criar um conjunto de dados da plataforma, observe que os dados de consentimento enviados por eventos não são honrados em workflows de imposição de downstream. |
| [!UICONTROL Conjunto de dados de perfil] | O conjunto de dados habilitado para [!DNL Profile] com campos de consentimento do cliente que você criou [anteriormente](#prerequisites). |

Quando terminar, selecione **[!UICONTROL Save]** na parte inferior da tela e continue a seguir quaisquer prompts adicionais para concluir a configuração.

## Instalar e configurar o SDK da Web da plataforma

Depois de criar um conjunto de dados conforme descrito na seção anterior, você deve configurar a extensão SDK da Web da plataforma que será implantada no site. Se não tiver a extensão SDK instalada na propriedade da tag, selecione **[!UICONTROL Extensões]** na navegação à esquerda, seguida pela guia **[!UICONTROL Catálogo]**. Em seguida, selecione **[!UICONTROL Install]** na extensão do SDK da plataforma na lista de extensões disponíveis.

![](../../images/governance-privacy-security/consent/adobe/sdk/install.png)

Ao configurar o SDK, em **[!UICONTROL Edge Configurations]**, selecione o conjunto de dados criado na etapa anterior.

![](../../images/governance-privacy-security/consent/adobe/sdk/config-sdk.png)

Selecione **[!UICONTROL Save]** para instalar a extensão.

### Criar um elemento de dados para definir o consentimento padrão

Com a extensão SDK instalada, você tem a opção de criar um elemento de dados para representar o valor de consentimento padrão da coleta de dados (`collect.val`) para seus usuários. Isso pode ser útil se você quiser ter valores padrão diferentes dependendo do usuário, como `pending` para usuários da União Europeia e `in` para usuários da América do Norte.

Nesse caso de uso, você pode implementar o seguinte para definir o consentimento padrão com base na região do usuário:

1. Determine a região do usuário no servidor da Web.
1. Antes da tag `script` (código incorporado) na página da Web, renderize uma tag `script` separada que defina uma variável `adobeDefaultConsent` com base na região do usuário.
1. Configure um elemento de dados que use a variável `adobeDefaultConsent` do JavaScript e use esse elemento de dados como o valor de consentimento padrão para o usuário.

Se a região do usuário for determinada por uma CMP, você poderá usar as seguintes etapas:

1. Manipule o evento &quot;CMP loaded&quot; na página.
1. No manipulador de eventos, defina uma variável `adobeDefaultConsent` com base na região do usuário e carregue o script da biblioteca de tags usando JavaScript.
1. Configure um elemento de dados que use a variável `adobeDefaultConsent` do JavaScript e use esse elemento de dados como o valor de consentimento padrão para o usuário.

Para criar um elemento de dados na interface do usuário da Coleta de dados, selecione **[!UICONTROL Elementos de dados]** na navegação à esquerda e selecione **[!UICONTROL Adicionar elemento de dados]** para navegar até a caixa de diálogo de criação do elemento de dados.

Aqui, você deve criar um elemento de dados [!UICONTROL Variável JavaScript] com base em `adobeDefaultConsent`. Selecione **[!UICONTROL Salvar]** ao concluir.

![](../../images/governance-privacy-security/consent/adobe/sdk/data-element.png)

Depois que o elemento de dados é criado, navegue de volta para a página de configuração da extensão do SDK da Web. Na seção [!UICONTROL Privacy], selecione **[!UICONTROL Fornecido pelo elemento de dados]** e use a caixa de diálogo fornecida para selecionar o elemento de dados de consentimento padrão criado anteriormente.

![](../../images/governance-privacy-security/consent/adobe/sdk/default-consent.png)

### Implantar a extensão no site

Quando terminar de configurar a extensão, ela poderá ser integrada ao seu site. Consulte o [guia de publicação](../../../tags/ui/publishing/overview.md) na documentação de tags para obter informações detalhadas sobre como implantar sua build de biblioteca atualizada.

## Comandos de alteração de consentimento {#commands}

Depois de integrar a extensão SDK ao seu site, você pode começar a usar o comando Plataforma Web SDK `setConsent` para enviar dados de consentimento para a Plataforma.

>[!IMPORTANT]
>
>O comando `setConsent` atualiza somente os dados diretamente no armazenamento do Perfil e não envia dados ao Data Lake.

Há dois cenários em que `setConsent` deve ser chamado no site:

1. Quando o consentimento é carregado na página (em outras palavras, em cada carregamento de página)
1. Como parte de um gancho ou ouvinte de evento da CMP que detecta alterações nas configurações de consentimento

>[!NOTE]
>
>Para obter uma introdução à sintaxe comum para comandos do SDK da plataforma, consulte o documento em [executar comandos](../../../edge/fundamentals/executing-commands.md).

O comando `setConsent` espera dois argumentos:

1. Uma string que indica o tipo de comando (nesse caso, `"setConsent"`)
1. Um objeto de carga que contém uma única propriedade do tipo matriz: `consent`. A matriz `consent` deve conter pelo menos um objeto que forneça os campos de consentimento necessários para o padrão Adobe.

Os campos de consentimento necessários para o padrão do Adobe são mostrados na seguinte chamada de exemplo `setConsent`:

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

| Propriedade da carga útil | Descrição |
| --- | --- |
| `standard` | O padrão de consentimento que está sendo usado. Para o padrão Adobe, esse valor deve ser definido como `Adobe`. |
| `version` | O número da versão do padrão de consentimento indicado em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento padrão do Adobe. |
| `value` | As informações de consentimento atualizadas do cliente, fornecidas como um objeto XDM que está em conformidade com a estrutura dos campos de consentimento do conjunto de dados habilitado para perfil. |

>[!NOTE]
>
>Se estiver usando outros padrões de consentimento em conjunto com `Adobe` (como `IAB TCF`), poderá adicionar objetos adicionais à matriz `consent` para cada padrão. Cada objeto deve conter valores apropriados para `standard`, `version` e `value` para o padrão de consentimento que representa.

O JavaScript a seguir fornece um exemplo de uma função que lida com as alterações de preferência de consentimento em um site, que pode ser usado como um retorno de chamada em um ouvinte de evento ou um gancho de CMP:

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

Todos os comandos [!DNL Platform SDK] retornam promessas que indicam se a chamada foi bem-sucedida ou falhou. Em seguida, você pode usar essas respostas para obter uma lógica adicional, como exibir mensagens de confirmação para o cliente. Consulte a seção [manuseando o sucesso ou a falha](../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) no guia sobre a execução de comandos do SDK para obter exemplos específicos.

Depois de fazer chamadas `setConsent` com êxito com o SDK, você pode usar o visualizador de perfil na interface do usuário da plataforma para verificar se os dados estão chegando no armazenamento de perfil. Consulte a seção em [navegar pelos perfis por identidade](../../../profile/ui/user-guide.md#browse-identity) para obter mais informações.

## Próximas etapas

Ao seguir este guia, você configurou a extensão SDK da Web da plataforma para enviar dados de consentimento ao Experience Platform. Para obter orientação sobre como testar sua implementação, consulte a documentação do padrão de consentimento que você está implementando:

* [Adobe standard](./adobe/overview.md#test)
* [TCF 2.0 padrão](./iab/overview.md#test)
