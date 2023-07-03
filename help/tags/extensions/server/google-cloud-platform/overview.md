---
title: Extensão de encaminhamento de eventos da Google Cloud Platform
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform envia eventos da Rede de borda do Adobe Experience para a Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
source-git-commit: 7e26ebe6d40796174ca48367f826c7c6f1512abf
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 2%

---

# Extensão de encaminhamento de eventos da [!DNL Google Cloud Platform]

[[!DNL Google Cloud Platform]](https://cloud.google.com/) O é uma plataforma de computação em nuvem que oferece uma grande variedade de serviços, como computação distribuída, armazenamento de banco de dados, entrega de conteúdo e serviços de integração de software como um serviço (SaaS) para gerenciamento de relacionamento com o cliente (CRM) e planejamento de recursos corporativos (ERP).

A variável [!DNL Google Cloud Platform] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) aproveitamentos de extensão [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) para enviar eventos da Rede de borda da Adobe Experience Platform para a [!DNL Google Cloud Platform] para processamento posterior. Este guia aborda como instalar a extensão e empregar seus recursos em uma regra de encaminhamento de eventos.

## Pré-requisitos

Para usar essa extensão, você deve ter um [!DNL Google Cloud Platform] conta com um existente [!DNL Cloud Pub/Sub] tópico. Se você não tiver um tópico pré-existente, consulte o [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) documentação sobre criação e gerenciamento de tópicos.

### Criar um segredo e um elemento de dados

Primeiro, crie um novo `Google OAuth 2` [segredo de encaminhamento de eventos](../../../ui/event-forwarding/secrets.md), que será usado para autenticar a conexão com sua conta, mantendo o valor seguro.

Em seguida, [criar um elemento de dados](../../../ui/managing-resources/data-elements.md#create-a-data-element) usando o **[!UICONTROL Núcleo]** extensão e um **[!UICONTROL Segredo]** tipo de elemento de dados para fazer referência ao `Google OAuth 2` segredo que acabou de criar.

## Instale e configure o [!DNL Google Cloud Platform] extensão {#install}

Para instalar a extensão, [criar uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Selecionar **[!UICONTROL Extensões]** no painel de navegação esquerdo. No **[!UICONTROL Catálogo]** selecione **[!UICONTROL Instalar]** no cartão para o [!DNL Google Cloud Platform] extensão.

![O catálogo [!DNL Google Cloud Platform] realce da extensão instalar.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Na tela de configuração, digite o segredo do elemento de dados criado anteriormente na variável **[!UICONTROL Token de acesso]** campo. O segredo do elemento de dados conterá seu [!DNL Google Cloud Platform] Token do OAuth 2. Selecione **[!UICONTROL Salvar]** ao concluir.

![A variável [!DNL Google Cloud Platform] página de configuração de extensão.](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Criar um [!DNL Send Data to Cloud Pub/Sub] regra {#tracking-rule}

Depois que a extensão for instalada, crie um novo encaminhamento de eventos [regra](../../../ui/managing-resources/rules.md) e configure suas condições conforme desejado. Ao configurar as ações para a regra, selecione a variável **[!UICONTROL Google Cloud Platform]** e selecione **[!UICONTROL Enviar dados para o Cloud Pub/Sub]** para o tipo de ação.

![A visualização da configuração de ação para [!UICONTROL Google Cloud Platform], com a ação destacada e [!UICONTROL Enviar dados para o Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Tópico] | O tópico que receberá os eventos do encaminhamento de eventos. O valor deve ter o formato `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Dados] | Este campo contém os dados a serem encaminhados para o [!DNL Cloud Pub/Sub] tópico no formato JSON.<br><br>No **[!UICONTROL Brutos]** , você pode colar o objeto JSON diretamente no campo de texto fornecido ou selecionar o ícone de elemento de dados (![Ícone de conjunto de dados](../../../images/extensions/server/aws/data-element-icon.png)) para selecionar de uma lista de elementos de dados existentes para representar os dados.<br><br>Você também pode usar a variável **[!UICONTROL Editor de pares de valor-chave JSON]** opção para adicionar manualmente cada par de valor-chave por meio de um editor de interface do usuário. Cada valor pode ser representado por uma entrada bruta, ou um elemento de dados pode ser selecionado. |
| [!UICONTROL Atributos] | Esse campo contém o objeto JSON com atributos extras a serem enviados junto com a mensagem.<br><br>No **[!UICONTROL Brutos]** , você pode colar o objeto JSON diretamente no campo de texto fornecido ou selecionar o ícone de elemento de dados (![Ícone de conjunto de dados](../../../images/extensions/server/aws/data-element-icon.png)) para selecionar de uma lista de elementos de dados existentes para representar os dados.<br><br>Você também pode usar a variável **[!UICONTROL Editor de pares de valor-chave JSON]** opção para adicionar manualmente cada par de valor-chave por meio de um editor de interface do usuário. Cada valor pode ser representado por uma entrada bruta, ou um elemento de dados pode ser selecionado. |

{style="table-layout:auto"}

## Próximas etapas

Este guia aborda como enviar dados para o [!DNL Cloud Pub/Sub] usando o [!DNL Google Cloud Platform] extensão de encaminhamento de eventos. Para obter mais informações sobre os recursos de encaminhamento de eventos no Experience Platform, consulte [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).