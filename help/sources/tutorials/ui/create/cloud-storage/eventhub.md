---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Criar um conector de origem de Hubs de Evento do Azure na interface do usuário
topic: overview
translation-type: tm+mt
source-git-commit: 75581529ede3772606bc18fea683da5d396996c5
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 1%

---


# Criar um conector de origem de Hubs de Evento do Azure na interface do usuário

>[!NOTE]
> O conector do Hubs de Evento do Azure está em beta. Os recursos e a documentação estão sujeitos a alterações.

Os conectores de origem na Adobe Experience Platform fornecem a capacidade de assimilar dados de origem externa de forma programada. Este tutorial fornece etapas para autenticação de um conector de origem do Hubs de Evento do Azure (a seguir denominado &quot;Hubs de Evento&quot;) usando a interface de usuário da Plataforma.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

- [Sistema](../../../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   - [Noções básicas da composição](../../../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [Perfil](../../../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Se você já tiver uma conta Hubs de Evento, poderá ignorar o restante desse documento e prosseguir para o tutorial sobre como [configurar um dataflow](../../dataflow/streaming/cloud-storage.md).

### Reunir credenciais obrigatórias

Para autenticar seu conector de origem Hubs de Evento, é necessário fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| ---------- | ----------- |
| `sasKeyName` | O nome da regra de autorização, que também é conhecida como o nome da chave SAS. |
| `sasKey` | A assinatura de acesso compartilhado gerada. |
| `namespace` | A namespace dos Hubs de Evento que você está acessando. |

Para obter mais informações sobre esses valores, consulte [este documento](https://docs.microsoft.com/en-us/azure/event-hubs/authenticate-shared-access-signature)Hubs de Evento.

## Conecte sua conta de Hubs de Eventos

Depois de reunir as credenciais necessárias, siga as etapas abaixo para vincular sua conta Hubs de Evento à Plataforma.

Faça logon na [Adobe Experience Platform](https://platform.adobe.com) e selecione **Fontes** na barra de navegação esquerda para acessar a área de trabalho *Fontes* . A guia *Catálogo* exibe várias fontes que podem ser conectadas à Plataforma. Cada fonte mostra o número de contas existentes associadas a elas.

Na categoria do Armazenamento ** Cloud, selecione Hubs **do Evento** Azure e clique **no ícone + (+)** para criar um novo conector de Hubs do Evento.

![](../../../../images/tutorials/create/eventhub/catalog.png)

A caixa de diálogo *Conectar-se aos Hubs* de Eventos do Azure é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Nova conta

Se você estiver usando novas credenciais, selecione **Nova conta**. No formulário de entrada exibido, forneça um nome, uma descrição opcional e suas credenciais de Hubs de Evento. Quando terminar, selecione **Connect** e aguarde algum tempo para a nova conexão ser estabelecida.

![](../../../../images/tutorials/create/eventhub/new.png)

### Conta existente

Para conectar uma conta existente, selecione a conta de Hubs de Evento à qual deseja se conectar e, em seguida, selecione **Avançar** para continuar.

![](../../../../images/tutorials/create/eventhub/existing.png)

## Próximas etapas

Ao seguir este tutorial, você conectou sua conta Hubs de Eventos à Plataforma. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados do seu armazenamento em nuvem para a Plataforma](../../dataflow/streaming/cloud-storage.md).