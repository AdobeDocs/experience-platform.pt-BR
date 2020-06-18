---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem do Google AdWords na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: b9e9207741044f118d53ab8eb3d3d6cd7451132d
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 0%

---


# Criar um conector de origem do Google AdWords na interface do usuário

>[!NOTE]
>O conector Google AdWords está em beta. Consulte a visão geral [das](../../../../home.md#terms-and-conditions) Fontes para obter mais informações sobre o uso de conectores com rótulo beta.

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem do Google AdWords usando a interface do usuário do Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão Google AdWords, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/payments.md)

### Reunir credenciais obrigatórias

Para acessar sua conta do Google AdWords Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `clientCustomerId` | A ID do cliente do cliente da conta AdWords. |
| `developerToken` | O token do desenvolvedor associado à conta do gerente. |
| `refreshToken` | O token de atualização obtido do Google para autorizar o acesso ao AdWords. |
| `clientId` | A ID do cliente do aplicativo Google usada para adquirir o token de atualização. |
| `clientSecret` | O segredo do cliente do aplicativo google usado para adquirir o token de atualização. |

Para obter mais informações sobre a introdução, consulte este documento [do](https://developers.google.com/adwords/api/docs/guides/authentication)Google AdWords.

## Conecte sua conta do Google AdWords

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conexão básica de entrada para vincular sua conta do Google AdWords à Platform.

Faça logon no [Adobe Experience Platform](https://platform.adobe.com) e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A tela *Catálogo* exibe várias fontes com as quais você pode criar conexões base de entrada e cada fonte mostra o número de conexões base existentes associadas a elas.

Na categoria *Publicidade* , selecione **Google AdWords** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão básica de entrada, selecione Origem **do** Connect.

![catálogo](../../../../images/tutorials/create/ads/catalog.png)

A página *Conectar-se ao Google AdWords* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **Nova conta**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do Google AdWords à conexão básica. Quando terminar, selecione **Connect** e aguarde algum tempo para a nova conexão básica ser estabelecida.

![connect](../../../../images/tutorials/create/ads/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta do Google AdWords com a qual você deseja se conectar e selecione **Avançar** para continuar.

![existente](../../../../images/tutorials/create/ads/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão básica com sua conta do Google AdWords. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados de publicidade para o Platform](../../dataflow/advertising.md).