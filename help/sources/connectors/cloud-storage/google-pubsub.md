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
>A variável [!DNL Google PubSub] origem está disponível no catálogo de origens para usuários que compraram o Real-time Customer Data Platform Ultimate.

O Adobe Experience Platform fornece conectividade nativa para provedores de nuvem, como [!DNL AWS], [!DNL Google Cloud Platform], e [!DNL Azure], permitindo que você traga dados desses sistemas para a Platform para uso em serviços e destinos downstream.

As fontes de armazenamento na nuvem podem trazer seus dados para a Platform sem a necessidade de baixar, formatar ou carregar. Os dados assimilados podem ser formatados como XDM JSON, XDM Parquet ou delimitados. Cada etapa do processo é integrada ao fluxo de trabalho de origens. A Platform permite trazer dados de [!DNL Google PubSub] em tempo real.

## Pré-requisitos {#prerequisites}

Esta seção descreve os pré-requisitos configurados que você deve concluir antes de conectar [!DNL Google PubSub] conta para Experience Platform.

### Criar conta de serviço {#create-service-account}

A **conta de serviço** é um tipo de conta frequentemente usada por um aplicativo ou carga de trabalho de computação, em vez de uma pessoa. Uma conta de serviço é identificada por seu endereço de email, que é exclusivo da conta.

* Por um lado, as contas **principais** - você pode conceder acesso às contas de serviço do [!DNL Google Cloud] recursos. Por exemplo, você pode conceder a uma conta de serviço a função Administrador de computação `(roles/compute.admin)` em um determinado projeto. Dessa forma, a conta de serviço poderá gerenciar os recursos do Mecanismo de computação nesse projeto específico.
* Por outro lado, as contas de serviço também são recursos - você pode dar permissão a outras entidades para acessar a conta de serviço. Por exemplo, você pode conceder a um usuário a função Usuário da conta de serviço `(roles/iam.serviceAccountUser)` em uma conta de serviço para permitir que o usuário anexe essa conta de serviço aos recursos. Como alternativa, você pode conceder a um usuário a função de Administrador da conta de serviço `(roles/iam.serviceAccountAdmin)` para permitir que o usuário conclua tarefas como exibir, editar, desativar e excluir a conta de serviço.

Para obter mais informações sobre como determinar o tipo de autenticação correto para seu caso de uso, leia o [[!DNL Google] guia sobre métodos de autenticação](https://cloud.google.com/docs/authentication).

Siga as etapas descritas abaixo para criar uma conta de serviço:

Primeiro, navegue até o [!DNL IAM] página do [!DNL Google Developer Console] e selecione **[!DNL Create Service Account]**.

![A janela Criar conta de serviço no Console do desenvolvedor do Google](../../images/tutorials/create/google-pubsub/create-service-account.png)

Em seguida, digite um nome para exibição e uma ID para a conta de serviço e selecione **[!DNL Create and Continue]**.

![Os detalhes da conta de serviço no Console do desenvolvedor do Google](../../images/tutorials/create/google-pubsub/service-account-details.png)

### Gerar chaves de conta de serviço {#generate-service-account-keys}

Para gerar chaves para sua conta de serviço, selecione o cabeçalho keys na página de contas de serviço. Nesse ponto, selecione **[!DNL Add key]** e selecione **[!DNL Create new key]** no menu suspenso. Você também pode usar esse painel para fazer upload de uma chave existente.

![A janela de adição de chave no Console do desenvolvedor do Google](../../images/tutorials/create/google-pubsub/add-key.png)

Depois de bem-sucedido, você receberá uma mensagem indicando que a chave privada foi salva no computador e que um arquivo será baixado. Em seguida, você pode usar o conteúdo desse arquivo como credenciais ao criar [!DNL Google PubSub] conta no Experience Platform.

### Conceder permissões no nível de tópico e assinatura {#grant-permissions}

Para conceder permissões no nível de tópico e de assinatura, navegue até a página do console de tópicos e selecione **[!DNL Show info panel]**. Em seguida, sob o [!DNL Permissions] selecione [!DNL Add Principal] e adicione a entidade de conta de serviço junto com as permissões.

![A janela pop-up no Console do desenvolvedor do Google, onde você pode conceder permissões no nível de tópico e subscrição](../../images/tutorials/create/google-pubsub/add-principal.png)

## Configurações ideais [!DNL Google PubSub usage] {#optimal-configurations}

Esta seção descreve as configurações recomendadas para otimizar o uso do [!DNL Google PubSub] fonte no Experience Platform.

### Propriedades da assinatura {#subscription-properties}

Use o [!DNL Google Developer Console] para **aumentar o prazo de confirmação**. Isso permite que o [!DNL Google Publisher] Aguardar de acordo com o tempo que você configura antes de enviar a mensagem novamente. Esse atraso ajuda na redução de carga desnecessária no nível do assinante.

![A interface do prazo de confirmação no Google Developer Console.](../../images/tutorials/create/google-pubsub/acknowledgement-deadline.png)

Ativar **[!DNL exactly one delivery]**. Essa configuração informa o [!DNL Google Publisher] para garantir que as mensagens enviadas à assinatura não sejam reenviadas antes que o prazo de confirmação expire. Você pode usar essa configuração para garantir que as mensagens de confirmação não sejam reenviadas para a assinatura.

![A página de configuração de delivery exatamente no Console do desenvolvedor do Google.](../../images/tutorials/create/google-pubsub/exactly-one-delivery.png)

Você pode ativar **[!DNL Retry after exponential backoff delay]** para reduzir o risco de sobrecarregar o servidor. Você pode habilitar essa configuração no [!DNL Google Developer Console] para atenuar melhor as falhas transitórias (erros temporários que normalmente se resolvem), fornecendo ao sistema mais tempo para recuperação antes de tentar outra conexão.

![A janela Retry policy no Google Developer Console.](../../images/tutorials/create/google-pubsub/retry-policy.png)

Você deve **defina a duração de retenção da mensagem de sua assinatura para 24 horas ou mais** para garantir que dados não reconhecidos não sejam perdidos durante picos de carga. Além disso, **ativar um tópico de letra morta** para garantir que a perda de dados não ocorra mesmo durante casos de borda raros.

>[!IMPORTANT]
>
>Você só pode criar um fluxo de dados de origem por [!DNL Google PubSub] assinatura. A reutilização de uma assinatura, mesmo em sandboxes, resulta em perda de dados.

## Conectar [!DNL Google PubSub] para Experience Platform

A documentação abaixo fornece informações sobre como se conectar [!DNL Google PubSub] para a Platform usando APIs ou a interface do usuário:

### Uso de APIs

* [Crie uma conexão de origem Google PubSub usando a API do Serviço de fluxo](../../tutorials/api/create/cloud-storage/google-pubsub.md)
* [Coletar dados de transmissão usando a API de Serviço de Fluxo](../../tutorials/api/collect/streaming.md)

### Uso da interface

* [Criar uma conexão de origem Google PubSub na interface](../../tutorials/ui/create/cloud-storage/google-pubsub.md)
* [Configurar um fluxo de dados para uma conexão de armazenamento em nuvem na interface](../../tutorials/ui/dataflow/streaming/cloud-storage-streaming.md)
