---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem PayPal na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 2162c66b1664ecaaf0b609fe3f7ccf58c4a5d31d
workflow-type: tm+mt
source-wordcount: '489'
ht-degree: 1%

---


# Criar um conector de origem PayPal na interface do usuário

> [!NOTE]
> O conector PayPal está em beta. Os recursos e a documentação estão sujeitos a alterações.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para a criação de um conector de origem PayPal usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

* [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
* [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conexão base PayPal, poderá ignorar o restante deste documento e prosseguir para o tutorial sobre como [configurar um fluxo de dados](../../dataflow/payments.md)

### Reunir credenciais obrigatórias

Para acessar a plataforma de conta PayPal, forneça os seguintes valores:

| Credencial | Descrição |
| ---------- | ----------- |
| `host` | O URL da instância do PayPal. |
| `clientID` | A ID do cliente associada ao aplicativo PayPal. |
| `clientSecret` | O segredo do cliente associado ao aplicativo PayPal. |

Para obter mais informações sobre a introdução, consulte este documento [PayPal](https://developer.paypal.com/docs/api/overview/#get-credentials)

## Conecte sua conta do PayPal

Depois de reunir as credenciais necessárias, siga as etapas abaixo para criar uma nova conexão básica de entrada para vincular sua conta PayPal à Plataforma.

Faça logon na <a href="https://platform.adobe.com" target="_blank">Adobe Experience Platform</a> e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A tela *Catálogo* exibe várias fontes com as quais você pode criar conexões base de entrada e cada fonte mostra o número de conexões base existentes associadas a elas.

Na categoria *CRM* , selecione **PayPal** para exibir uma barra de informações no lado direito da tela. A barra de informações fornece uma breve descrição para a fonte selecionada, bem como opções para se conectar à fonte ou à sua documentação de visualização. Para criar uma nova conexão básica de entrada, selecione Origem **do** Connect.

![catálogo](../../../../images/tutorials/create/paypal/catalog.png)

A página *Conectar-se ao PayPal* é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **Nova conta**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais do PayPal à conexão básica. Quando terminar, selecione **Connect** e aguarde algum tempo para a nova conexão básica ser estabelecida.

![connect](../../../../images/tutorials/create/paypal/connect.png)

### Conta existente

Para conectar uma conta existente, selecione a conta PayPal com a qual você deseja se conectar e selecione **Avançar** para continuar.

![existente](../../../../images/tutorials/create/paypal/existing.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão básica com sua conta PayPal. Agora você pode continuar com o próximo tutorial e [configurar um fluxo de dados para trazer dados CRM para a Plataforma](../../dataflow/payments.md).