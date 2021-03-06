---
description: O serviço de destinos no Adobe Experience Platform usa modelos de configuração para vários componentes que criam a funcionalidade de destinos. Combinados, esses componentes permitem que o Experience Platform se conecte aos parceiros de destino, envie mensagens personalizadas e ative dados de perfil no ecossistema digital.
title: Opções de configuração no Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: ad0d38cbd249642d582a807c5679065827f57717
workflow-type: tm+mt
source-wordcount: '345'
ht-degree: 2%

---

# Opções de configuração no Destination SDK

## Visão geral {#overview}

O serviço de destinos no Adobe Experience Platform usa modelos de configuração para vários componentes que criam a funcionalidade de destinos. Combinados, esses componentes permitem que o Experience Platform se conecte aos parceiros de destino, envie mensagens personalizadas e ative dados de perfil no ecossistema digital. Os modelos usados no Adobe Experience Platform são:

* **Configuração de destino**: Contém informações básicas sobre seu destino. Essa configuração inclui os tipos de identidade que seu destino pode suportar e vários atributos de interface do usuário para seu cartão de destino na interface do usuário do Adobe Experience Platform.
* **Especificações do servidor e do modelo**: Vincula informações sobre as especificações do servidor e o modelo usado pelo Adobe para fornecer cargas ao destino.
   * **Especificações do servidor**: Um template que armazena os detalhes do terminal.
   * **Especificações do modelo**: Nesse template, você pode definir como transformar campos de atributo de perfil entre o esquema XDM e o formato compatível com a plataforma. Para obter informações detalhadas sobre os idiomas de modelos suportados, os formatos de mensagem e as informações necessárias para o Adobe configurar a integração com sua plataforma, leia [Formato de mensagem](./message-format.md).
* **Configuração de autenticação**: Essas configurações definem como os usuários do Adobe Experience Platform se conectam ao seu destino.
* **Configuração de metadados de público-alvo**: Este modelo permite configurar como os públicos-alvo/segmentos são criados, atualizados ou excluídos de forma programática no seu destino.

![Modelos e configurações do Destination SDK](./assets/self-service-configuration.png)

## Links relacionados {#related-links}

As páginas abaixo fornecem mais detalhes sobre a funcionalidade e as opções de configuração disponíveis no Destination SDK e as operações de API correspondentes que você pode executar.

| Descrição da funcionalidade | Referência da API |
|--- |--- |
| [Configuração de destino](./destination-configuration.md) | [Operações de endpoint da API de destinos](./destination-configuration-api.md) |
| [Especificações do servidor e do modelo](./server-and-template-configuration.md) | [Operações de endpoint da API de servidores de destino](./destination-server-api.md) |
| [Configuração de autenticação](./authentication-configuration.md) | [Operações da API do endpoint de credenciais](./credentials-configuration-api.md) |
| [Gerenciamento de metadados do público-alvo](./audience-metadata-management.md) | [Operações da API de ponto de extremidade de metadados de público-alvo](./audience-metadata-api.md) |
| [Configuração do OAuth 2](./oauth2-authentication.md) | Configurar usando o `customerAuthenticationConfigurations` no [Ponto de extremidade da API de /destinos](./destination-configuration-api.md). |
| [Formato de mensagem](./message-format.md) | - |
| [Teste de destino](./test-destination.md) | [Operações da API de teste de destino](./destination-testing-api.md) |
| [Publicação de destino](./configure-destination-instructions.md#publish-destination) | [Operações da API de publicação de destino](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}
