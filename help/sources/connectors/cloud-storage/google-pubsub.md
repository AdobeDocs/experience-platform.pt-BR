---
title: Visão geral do Google PubSub Source
description: Saiba como conectar o Google PubSub ao Adobe Experience Platform usando APIs ou a interface do usuário.
badgeUltimate: label="Ultimate" type="Positive"
exl-id: 7c78173d-2639-47cb-8935-77fb7841a121
source-git-commit: c8fc447631f5382d49022b525a10edeadbd5ab46
workflow-type: tm+mt
source-wordcount: '827'
ht-degree: 0%

---

# [!DNL Google PubSub] origem

>[!IMPORTANT]
>
>A origem [!DNL Google PubSub] está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem como [!DNL AWS], [!DNL Google Cloud Platform] e [!DNL Azure], permitindo que você traga dados desses sistemas para a Plataforma para uso em serviços e destinos downstream.

As fontes de armazenamento na nuvem podem trazer seus dados para a Platform sem a necessidade de baixar, formatar ou carregar. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de origens. A Platform permite trazer dados de [!DNL Google PubSub] em tempo real.

## Pré-requisitos {#prerequisites}

Esta seção descreve os pré-requisitos configurados que você deve concluir antes de conectar sua conta do [!DNL Google PubSub] ao Experience Platform.

### Criar conta de serviço {#create-service-account}

Uma **conta de serviço** é um tipo de conta frequentemente usada por um aplicativo ou carga de trabalho de computação, em vez de uma pessoa. Uma conta de serviço é identificada por seu endereço de email, que é exclusivo da conta.

* Por um lado, as contas de serviço são **principais** - você pode conceder acesso às contas de serviço aos recursos [!DNL Google Cloud]. Por exemplo, você pode conceder a uma conta de serviço a função de Administrador de Computação `(roles/compute.admin)` em um determinado projeto. Dessa forma, a conta de serviço poderá gerenciar os recursos do Mecanismo de computação nesse projeto específico.
* Por outro lado, as contas de serviço também são recursos - você pode dar permissão a outras entidades para acessar a conta de serviço. Por exemplo, você pode conceder a um usuário a função de Usuário da Conta de Serviço `(roles/iam.serviceAccountUser)` em uma conta de serviço para permitir que o usuário anexe essa conta de serviço aos recursos. Como alternativa, você pode conceder a um usuário a função de Administrador de Conta de Serviço `(roles/iam.serviceAccountAdmin)` para permitir que o usuário conclua tarefas como exibir, editar, desabilitar e excluir a conta de serviço.

Para obter mais informações sobre como determinar o tipo de autenticação correto para seu caso de uso, leia o [[!DNL Google] guia sobre métodos de autenticação](https://cloud.google.com/docs/authentication).

Siga as etapas descritas abaixo para criar uma conta de serviço:

Primeiro, navegue até a página [!DNL IAM] de [!DNL Google Developer Console] e selecione **[!DNL Create Service Account]**.

![A janela de criação de conta de serviço no Google Developer Console](../../images/tutorials/create/google-pubsub/create-service-account.png)

Em seguida, digite um nome para exibição e uma ID para a conta de serviço e selecione **[!DNL Create and Continue]**.

![Os detalhes da conta de serviço no Google Developer Console](../../images/tutorials/create/google-pubsub/service-account-details.png)

### Gerar chaves de conta de serviço {#generate-service-account-keys}

Para gerar chaves para sua conta de serviço, selecione o cabeçalho keys na página de contas de serviço. Ali, selecione **[!DNL Add key]** e depois selecione **[!DNL Create new key]** no menu suspenso. Você também pode usar esse painel para fazer upload de uma chave existente.

![A janela de adição de chave no Google Developer Console](../../images/tutorials/create/google-pubsub/add-key.png)

Depois de bem-sucedido, você receberá uma mensagem indicando que a chave privada foi salva no computador e que um arquivo será baixado. Em seguida, você pode usar o conteúdo desse arquivo como credenciais ao criar sua conta do [!DNL Google PubSub] no Experience Platform.

### Conceder permissões no nível de tópico e assinatura {#grant-permissions}

Para conceder permissões no nível de assinatura e tópico, navegue até a página do console de tópicos e selecione **[!DNL Show info panel]**. Em seguida, na guia [!DNL Permissions], selecione [!DNL Add Principal] e adicione a entidade de conta de serviço juntamente com as permissões.

![A janela pop-up no Google Developer Console em que você pode conceder permissões no nível de tópico e assinatura](../../images/tutorials/create/google-pubsub/add-principal.png)

## Configurações para o ideal [!DNL Google PubSub usage] {#optimal-configurations}

Esta seção descreve as configurações recomendadas para otimizar o uso da fonte [!DNL Google PubSub] no Experience Platform.

### Propriedades da assinatura {#subscription-properties}

Use o [!DNL Google Developer Console] para **aumentar o prazo de confirmação**. Isso permite que o [!DNL Google Publisher] aguarde de acordo com o tempo que você configura antes de enviar a mensagem novamente. Esse atraso ajuda na redução de carga desnecessária no nível do assinante.

![A interface do prazo de confirmação no Google Developer Console.](../../images/tutorials/create/google-pubsub/acknowledgement-deadline.png)

Habilitar **[!DNL exactly one delivery]**. Essa configuração informa o [!DNL Google Publisher] para garantir que as mensagens enviadas à assinatura não sejam reenviadas antes que o prazo de confirmação expire. Você pode usar essa configuração para garantir que as mensagens de confirmação não sejam reenviadas para a assinatura.

![A exatamente uma página de configuração de entrega no Google Developer Console.](../../images/tutorials/create/google-pubsub/exactly-one-delivery.png)

Você pode habilitar **[!DNL Retry after exponential backoff delay]** para reduzir o risco de sobrecarregar ainda mais o servidor. Você pode habilitar essa configuração no [!DNL Google Developer Console] para atenuar melhor as falhas transitórias (erros temporários que normalmente se resolvem), dando ao sistema mais tempo para se recuperar antes de tentar outra conexão.

![A janela de política Repetir no Google Developer Console.](../../images/tutorials/create/google-pubsub/retry-policy.png)

Você deve **definir a duração de retenção da mensagem da sua assinatura para 24 horas ou mais** para garantir que dados não confirmados não sejam perdidos durante picos de carga. Além disso, **habilite um tópico de letra morta** para garantir que a perda de dados não ocorra mesmo durante casos de borda raros.

>[!IMPORTANT]
>
>Você só pode criar um fluxo de dados de origem por assinatura [!DNL Google PubSub]. A reutilização de uma assinatura, mesmo em sandboxes, resulta em perda de dados.

## Conectar [!DNL Google PubSub] ao Experience Platform

A documentação abaixo fornece informações sobre como conectar o [!DNL Google PubSub] à Plataforma usando APIs ou a interface do usuário:

### Uso de APIs

* [Crie uma conexão de origem Google PubSub usando a API do Serviço de fluxo](../../tutorials/api/create/cloud-storage/google-pubsub.md)
* [Coletar dados de transmissão usando a API de Serviço de Fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface

* [Criar uma conexão de origem Google PubSub na interface](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
* [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
