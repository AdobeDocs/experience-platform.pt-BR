---
description: O serviço de destinos no Adobe Experience Platform usa endpoints de configuração para vários componentes que criam a funcionalidade de destinos . Combinados, esses componentes permitem que o Experience Platform se conecte aos parceiros de destino, envie mensagens personalizadas e ative dados de perfil no ecossistema digital.
title: Opções de configuração no Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '563'
ht-degree: 1%

---

# Opções de configuração no Destination SDK

## Visão geral {#overview}

O serviço de destinos no Adobe Experience Platform usa endpoints de configuração para vários componentes que criam a funcionalidade de destinos . Combinados, esses componentes permitem que o Experience Platform se conecte às plataformas de destino, envie mensagens personalizadas, exporte arquivos personalizados e ative os dados do perfil no ecossistema digital. As configurações usadas no Adobe Experience Platform Destination SDK são:

* **Configuração de destino**: Contém informações básicas sobre seu destino. Essa configuração inclui os tipos de identidade que seu destino pode suportar, o formato desejado de arquivos exportados (para destinos com base em arquivo) e vários atributos de interface do usuário para seu cartão de destino na interface do usuário do Adobe Experience Platform.
* **Especificações de servidor, arquivo e modelo**: Vincula informações sobre as especificações do servidor e o modelo usado pelo Adobe para fornecer cargas ao destino. Para destinos com base em arquivo, essa configuração também inclui a formatação de arquivo e os formatos de compactação compatíveis com seu destino.
   * **Especificações do servidor**: Um template de configuração que contém informações sobre o local de armazenamento ou o terminal HTTP para o qual os dados são enviados.&quot;
   * **Especificações do arquivo**: Um template de configuração que inclui as opções de formatação e compactação de arquivo para o destino do lote.
   * **Especificações do modelo**: Nesse template, você pode definir como transformar campos de atributo de perfil entre o esquema XDM e o formato compatível com a plataforma. Para obter informações detalhadas sobre os idiomas de modelos suportados, os formatos de mensagem e as informações necessárias para o Adobe configurar a integração com sua plataforma, leia [Formato de mensagem](./message-format.md).
* **Configuração de autenticação**: Essas configurações definem como os usuários do Adobe Experience Platform se conectam ao seu destino.
* **Configuração de metadados de público-alvo**: Esse ponto de extremidade de configuração permite configurar como os públicos-alvo/segmentos são criados, atualizados ou excluídos de forma programática no seu destino. Para destinos em lote, é possível configurar uma notificação sempre que os arquivos forem entregues com êxito ao destino.

![Diagrama que mostra os pontos de extremidade de configuração do Destination SDK e como eles são usados juntos.](./assets/self-service-configuration.png)

## Links relacionados {#related-links}

As páginas abaixo fornecem mais detalhes sobre a funcionalidade e as opções de configuração disponíveis no Destination SDK e as operações de API correspondentes que você pode executar.

| Descrição da funcionalidade (destinos de transmissão) | Descrição da funcionalidade (destinos em lote) | Referência da API |
|--- |--- |--- |
| [Opções de configuração de destino](./destination-configuration.md) | [Opções de configuração de destino baseadas em arquivo](/help/destinations/destination-sdk/file-based-destination-configuration.md) | [Operações de endpoint da API de destinos](./destination-configuration-api.md) |
| [Especificações do servidor e do modelo](./server-and-template-configuration.md) | [Especificações de configuração de servidor e arquivo](/help/destinations/destination-sdk/server-and-file-configuration.md) | [Operações de endpoint da API de servidores de destino](./destination-server-api.md) |
| [Configuração de autenticação](./authentication-configuration.md) | Igual a destinos de transmissão. | Você pode configurar as informações de autenticação para o seu destino por meio da variável `customerAuthenticationConfigurations` parâmetros da `/destinations` endpoint . Mais informações para [transmissão](/help/destinations/destination-sdk/destination-configuration.md#customer-authentication-configurations) e [lote](/help/destinations/destination-sdk/file-based-destination-configuration.md#customer-authentication-configurations) destinos. |
| [Gerenciamento de metadados do público-alvo](./audience-metadata-management.md) | Igual ao fluxo contínuo. Consulte [exemplo baseado em arquivo](/help/destinations/destination-sdk/audience-metadata-management.md#example-file-based) para entender como os metadados do público-alvo podem ser usados em um contexto de destino de lote. | [Operações da API de ponto de extremidade de metadados de público-alvo](./audience-metadata-api.md) |
| [Configuração do OAuth 2](./oauth2-authentication.md) | Igual a destinos de fluxo | Configurar usando o `customerAuthenticationConfigurations` no [Ponto de extremidade da API de /destinos](./destination-configuration-api.md). |
| [Formato de mensagem](./message-format.md) | - | - |
| [Ferramentas de teste para destinos de transmissão](./test-destination.md) | [Ferramentas de teste para destinos com base em arquivos](/help/destinations/destination-sdk/file-based-destination-testing-overview.md) | [Operações da API de teste de destino](./destination-testing-api.md) |
| [Publicação de destino](./configure-destination-instructions.md#publish-destination) | Igual a destinos de fluxo | [Operações da API de publicação de destino](./destination-publish-api.md) |

{style=&quot;table-layout:auto&quot;}

## Próximas etapas {#next-steps}

Ao ler este artigo, agora você tem uma visão geral da funcionalidade fornecida pelo Destination SDK e quais páginas devem ser lidas para obter mais informações sobre configurações específicas. Em seguida, você pode ler os guias que incluem todas as etapas para [configurar um streaming](/help/destinations/destination-sdk/configure-destination-instructions.md) ou [destino baseado em arquivo](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) usando o Destination SDK.
