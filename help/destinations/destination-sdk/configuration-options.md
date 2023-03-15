---
description: O serviço de destinos no Adobe Experience Platform usa endpoints de configuração para vários componentes que criam a funcionalidade de destinos. Combinados, esses componentes permitem que o Experience Platform se conecte a parceiros de destino, envie mensagens personalizadas e ative dados de perfil no ecossistema digital.
title: Opções de configuração no Destination SDK
exl-id: 8890c70a-cdb9-4b9d-aa81-affe72b1fdc5
source-git-commit: 9b4c7da5aa02ae27608c2841b1d825445ac3015e
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 1%

---

# Opções de configuração no Destination SDK

## Visão geral {#overview}

O serviço de destinos no Adobe Experience Platform usa endpoints de configuração para vários componentes que criam a funcionalidade de destinos. Combinados, esses componentes permitem que o Experience Platform se conecte às plataformas de destino, envie mensagens personalizadas, exporte arquivos personalizados e ative dados de perfil no ecossistema digital. As configurações usadas no Adobe Experience Platform Destination SDK são:

* **Configuração de destino**: contém informações básicas sobre o destino. Essa configuração inclui os tipos de identidade que seu destino pode suportar, o formato desejado de arquivos exportados (para destinos baseados em arquivos) e vários atributos de interface do usuário para seu cartão de destino na interface do usuário do Adobe Experience Platform.
* **Especificações de servidor, arquivo e modelo**: une as informações sobre as especificações do servidor e o modelo usado pelo Adobe para entregar cargas úteis ao seu destino. Para destinos baseados em arquivo, essa configuração também inclui a formatação de arquivo e os formatos de compactação compatíveis com seu destino.
   * **Especificações do servidor**: um modelo de configuração que contém informações sobre o local de armazenamento ou endpoint HTTP para o qual os dados são enviados.&quot;
   * **Especificações do arquivo**: um modelo de configuração que inclui as opções de compactação e formatação de arquivo para o destino do lote.
   * **Especificações do modelo**: neste modelo, você pode definir como transformar campos de atributo de perfil entre o esquema XDM e o formato compatível com sua plataforma. Para obter informações detalhadas sobre idiomas de modelos compatíveis, formatos de mensagem e as informações necessárias para o Adobe configurar a integração com sua plataforma, leia [Formato da mensagem](./message-format.md).
* **Configuração de autenticação**: essas configurações definem como os usuários do Adobe Experience Platform se conectam ao seu destino.
* **Configuração de metadados de público**: esse endpoint de configuração permite definir como públicos-alvo/segmentos são criados, atualizados ou excluídos de forma programática no destino. Para destinos em lote, ele permite configurar uma notificação sempre que os arquivos forem entregues com êxito ao destino.

![Diagrama mostrando os pontos finais de configuração do Destination SDK e como eles são usados juntos.](./assets/self-service-configuration.png)

## Links relacionados {#related-links}

As páginas abaixo fornecem mais detalhes sobre as opções de funcionalidade e configuração disponíveis no Destination SDK e as operações de API correspondentes que você pode executar.

| Descrição da funcionalidade (destinos de transmissão) | Descrição da funcionalidade (destinos em lote) | Referência da API |
|--- |--- |--- |
| [Opções de configuração de destino](./destination-configuration.md) | [Opções de configuração de destino baseadas em arquivo](/help/destinations/destination-sdk/file-based-destination-configuration.md) | [Operações de endpoint da API de destinos](./destination-configuration-api.md) |
| [Especificações do servidor e do modelo](./server-and-template-configuration.md) | [Especificações de configuração de servidor e arquivo](/help/destinations/destination-sdk/server-and-file-configuration.md) | [Operações de ponto de extremidade da API dos servidores de destino](./destination-server-api.md) |
| [Configuração de autenticação](./authentication-configuration.md) | Igual aos destinos de transmissão. | Você pode configurar as informações de autenticação para seu destino por meio da `customerAuthenticationConfigurations` parâmetros do `/destinations` terminal. Mais informações para [transmissão](/help/destinations/destination-sdk/destination-configuration.md#customer-authentication-configurations) e [lote](/help/destinations/destination-sdk/file-based-destination-configuration.md#customer-authentication-configurations) destinos. |
| [Gerenciamento de metadados de público](./audience-metadata-management.md) | O mesmo para streaming. Consulte [exemplo baseado em arquivo](/help/destinations/destination-sdk/audience-metadata-management.md#example-file-based) para entender como os metadados de público-alvo podem ser usados em um contexto de destino em lote. | [Operações da API do ponto de extremidade de metadados de público](./audience-metadata-api.md) |
| [Configuração do OAuth 2](./oauth2-authentication.md) | Igual aos destinos de transmissão | Configurar o usando o `customerAuthenticationConfigurations` parâmetro no [Endpoint da API /destinations](./destination-configuration-api.md). |
| [Formato de mensagem](./message-format.md) | - | - |
| [Ferramentas de teste para destinos de transmissão](./test-destination.md) | [Ferramentas de teste para destinos baseados em arquivo](/help/destinations/destination-sdk/file-based-destination-testing-overview.md) | [Operações da API de teste de destino](./destination-testing-api.md) |
| [Publicação de destino](./configure-destination-instructions.md#publish-destination) | Igual aos destinos de transmissão | [Operações da API de publicação de destino](./destination-publish-api.md) |

{style="table-layout:auto"}

## Próximas etapas {#next-steps}

Após a leitura deste artigo, você tem uma visão geral da funcionalidade fornecida pelo Destination SDK e quais páginas devem ser lidas para obter mais informações sobre configurações específicas. Em seguida, você pode ler os guias que incluem todas as etapas para [configurar um streaming](/help/destinations/destination-sdk/configure-destination-instructions.md) ou um [destino baseado em arquivo](/help/destinations/destination-sdk/configure-file-based-destination-instructions.md) usando o Destination SDK.
