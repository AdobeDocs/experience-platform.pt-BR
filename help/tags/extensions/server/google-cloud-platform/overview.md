---
title: Extensão de encaminhamento de eventos da Google Cloud Platform
description: Essa extensão de encaminhamento de eventos do Adobe Experience Platform envia eventos Edge Network para a Google Cloud Platform.
last-substantial-update: 2023-06-21T00:00:00Z
exl-id: c5da1889-f917-42aa-b3a4-9557c31d6ee8
source-git-commit: c2832821ea6f9f630e480c6412ca07af788efd66
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 2%

---

# Extensão de encaminhamento de eventos da [!DNL Google Cloud Platform]

[[!DNL Google Cloud Platform]](https://cloud.google.com/) é uma plataforma de computação em nuvem que oferece uma grande variedade de serviços, como computação distribuída, armazenamento de banco de dados, entrega de conteúdo e serviços de integração de software como um serviço (SaaS) para CRM (gerenciamento de relacionamento com o cliente) e ERP (planejamento de recursos corporativos).

A extensão [!DNL Google Cloud Platform] [encaminhamento de eventos](../../../ui/event-forwarding/overview.md) aproveita [[!DNL Cloud Pub/Sub]](https://cloud.google.com/pubsub) para enviar eventos do Edge Network Adobe Experience Platform para o [!DNL Google Cloud Platform] para processamento adicional. Este guia aborda como instalar a extensão e empregar seus recursos em uma regra de encaminhamento de eventos.

## Pré-requisitos

Para usar esta extensão, você deve ter uma conta [!DNL Google Cloud Platform] com um tópico [!DNL Cloud Pub/Sub] existente. Se você não tiver um tópico pré-existente, consulte a documentação do [[!DNL Google Cloud Platform]](https://cloud.google.com/pubsub/docs/create-topic) sobre criação e gerenciamento de tópicos.

### Criar um segredo e um elemento de dados

Primeiro, crie um novo `Google OAuth 2` [segredo de encaminhamento de eventos](../../../ui/event-forwarding/secrets.md), que será usado para autenticar a conexão com sua conta enquanto mantém o valor seguro.

Em seguida, [crie um elemento de dados](../../../ui/managing-resources/data-elements.md#create-a-data-element) usando a extensão **[!UICONTROL Core]** e um tipo de elemento de dados **[!UICONTROL Secret]** para fazer referência ao segredo `Google OAuth 2` que você acabou de criar.

## Instalar e configurar a extensão [!DNL Google Cloud Platform] {#install}

Para instalar a extensão, [crie uma propriedade de encaminhamento de eventos](../../../ui/event-forwarding/overview.md#properties) ou escolha uma propriedade existente para editar.

Selecione **[!UICONTROL Extensões]** na navegação à esquerda. Na guia **[!UICONTROL Catálogo]**, selecione **[!UICONTROL Instalar]** no cartão para a extensão [!DNL Google Cloud Platform].

![Instalação do realce de extensão [!DNL Google Cloud Platform] do catálogo.](../../../images/extensions/server/google-cloud-platform/install-extension.png)

Na tela de configuração, digite a senha do elemento de dados criado anteriormente no campo **[!UICONTROL Token de Acesso]**. A senha do elemento de dados conterá seu token OAuth 2 do [!DNL Google Cloud Platform]. Selecione **[!UICONTROL Salvar]** ao concluir.

![A página de configuração de extensão [!DNL Google Cloud Platform].](../../../images/extensions/server/google-cloud-platform/configure-extension.png)

## Criar uma regra [!DNL Send Data to Cloud Pub/Sub] {#tracking-rule}

Depois que a extensão for instalada, crie uma nova [regra](../../../ui/managing-resources/rules.md) de encaminhamento de eventos e configure suas condições conforme desejado. Ao configurar as ações para a regra, selecione a extensão **[!UICONTROL Google Cloud Platform]** e selecione **[!UICONTROL Enviar Dados para Cloud Pub/Sub]** para o tipo de ação.

![O modo de exibição de configuração da ação para [!UICONTROL Google Cloud Platform], com a ação realçada e [!UICONTROL Enviar Dados para Cloud Pub/Sub].](../../../images/extensions/server/google-cloud-platform/event-action.png)

| Entrada | Descrição |
| --- | --- |
| [!UICONTROL Tópico] | O tópico que receberá os eventos do encaminhamento de eventos. O valor deve ter o formato `projects/{projectName}/topics/{topicName}`. |
| [!UICONTROL Dados] | Este campo contém os dados a serem encaminhados ao tópico [!DNL Cloud Pub/Sub] em formato JSON.<br><br>Na opção **[!UICONTROL Raw]**, você pode colar o objeto JSON diretamente no campo de texto fornecido ou selecionar o ícone de elemento de dados (![ícone de Conjunto de Dados](/help/images/icons/database.png)) para selecionar de uma lista de elementos de dados existentes para representar os dados.<br><br>Você também pode usar a opção **[!UICONTROL Editor de pares de valores-chave JSON]** para adicionar manualmente cada par de valores-chave por meio de um editor de interface do usuário. Cada valor pode ser representado por uma entrada bruta, ou um elemento de dados pode ser selecionado. |
| [!UICONTROL Atributos] | Esse campo contém o objeto JSON com atributos extras a serem enviados junto com a mensagem.<br><br>Na opção **[!UICONTROL Raw]**, você pode colar o objeto JSON diretamente no campo de texto fornecido ou selecionar o ícone de elemento de dados (![ícone de Conjunto de Dados](/help/images/icons/database.png)) para selecionar de uma lista de elementos de dados existentes para representar os dados.<br><br>Você também pode usar a opção **[!UICONTROL Editor de pares de valores-chave JSON]** para adicionar manualmente cada par de valores-chave por meio de um editor de interface do usuário. Cada valor pode ser representado por uma entrada bruta, ou um elemento de dados pode ser selecionado. |

{style="table-layout:auto"}

## Próximas etapas

Este guia aborda como enviar dados para [!DNL Cloud Pub/Sub] usando a extensão de encaminhamento de eventos [!DNL Google Cloud Platform]. Para obter mais informações sobre os recursos de encaminhamento de eventos do Experience Platform, consulte a [visão geral do encaminhamento de eventos](../../../ui/event-forwarding/overview.md).
