---
description: O serviço de destinos no Adobe Experience Platform usa endpoints de configuração para vários componentes que criam a funcionalidade de destinos. Saiba como esses componentes combinados permitem que o Experience Platform se conecte a parceiros de destino, envie mensagens personalizadas e ative dados de perfil no ecossistema digital.
title: Opções de configuração no Destination SDK
source-git-commit: 3f31a54c0cf329d374808dacce3fac597a72aa11
workflow-type: tm+mt
source-wordcount: '828'
ht-degree: 0%

---


# Opções de configuração no Destination SDK

O serviço de destinos no Adobe Experience Platform usa endpoints de configuração para vários componentes que criam a funcionalidade de destinos.

Combinados, esses componentes permitem que o Experience Platform se conecte às plataformas de destino, envie mensagens personalizadas, exporte arquivos personalizados e ative dados de perfil no ecossistema digital.

O diagrama abaixo mostra uma visão geral de alto nível dos componentes que você pode configurar por meio do Destination SDK para criar seu próprio destino. Esses componentes são descritos mais abaixo.

![Diagrama mostrando os componentes do Destination SDK, endpoints de configuração e as operações suportadas por eles.](../assets/functionality/destination-sdk-components-diagram.png)

## Configuração de servidor {#server-configuration}

A configuração do servidor de destino vincula as informações sobre as especificações do servidor e o modelo usado pelo Adobe para entregar payloads ao seu destino.

Por exemplo, é aqui que você especifica os endpoints de API do seu lado aos quais o Experience Platform precisa se conectar, bem como os cabeçalhos e o formato das chamadas de API que o Platform fará.

Para destinos baseados em arquivo, essa configuração também inclui a formatação de arquivo e os formatos de compactação compatíveis com seu destino. Você pode configurar as funcionalidades descritas abaixo por meio da [endpoint de servidores de destino](../authoring-api/destination-server/create-destination-server.md).

* [Especificações do servidor](destination-server/server-specs.md): um modelo de configuração que contém informações sobre o local de armazenamento ou endpoint HTTP para o qual os dados são enviados.
* [Especificações do modelo](destination-server/templating-specs.md): neste modelo, você pode definir como estruturar a solicitação de API HTTP para o endpoint, incluindo como transformar campos de atributo de perfil entre o esquema XDM e o formato compatível com sua plataforma. Use essas informações junto com o [formato da mensagem](destination-server/message-format.md) documentação.
* [Formato da mensagem](destination-server/message-format.md): esta seção aborda informações detalhadas sobre idiomas de modelos compatíveis, formatos de mensagem e as informações necessárias para o Adobe configurar a integração com sua plataforma. Use essas informações junto com o [especificações do modelo](destination-server/templating-specs.md) documentação.
* [Especificações do arquivo](destination-server/file-formatting.md): um modelo de configuração que inclui as opções de compactação e formatação de arquivo para o destino do lote.

## Configuração de destino {#destination-configuration}

Esse endpoint de configuração contém informações básicas e avançadas sobre o destino. Por exemplo, é aqui que você especifica os tipos de identidade que seu destino pode suportar, o formato desejado de arquivos exportados (para destinos baseados em arquivos) e vários atributos de interface do usuário para seu cartão de destino na interface do usuário do Adobe Experience Platform.

Consulte a documentação abaixo para obter detalhes sobre cada um dos componentes da configuração de destino. Você pode configurar as funcionalidades descritas abaixo por meio da [endpoint de destinos](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Configuração de autenticação do cliente](destination-configuration/customer-authentication.md): selecione o mecanismo de autenticação que o Experience Platform deve usar para se conectar ao seu destino. Essa configuração gera a variável [Configurar novo destino](../../ui/connect-destination.md) página na interface do usuário do Experience Platform, onde os usuários conectam o Experience Platform às contas que têm com seu destino.
* [Autenticação OAuth2](destination-configuration/oauth2-authentication.md): saiba mais sobre todas as [!DNL OAuth2] fluxos de autenticação compatíveis com o Destination SDK e obtenha instruções para configurar [!DNL OAuth2] autenticação para o seu destino.
* [Campos de dados do cliente](destination-configuration/customer-data-fields.md): saiba como criar campos de entrada na interface do Experience Platform que permitem que os usuários especifiquem várias informações relevantes para conexão e exportação de dados para o seu destino.
* [Atributos da interface](destination-configuration/ui-attributes.md): saiba como configurar os atributos da interface do usuário, como o link de documentação, a categoria da placa de destino, o tipo de conexão e a frequência de destino, para destinos criados com o Destination SDK.
* [Configuração de esquema](destination-configuration/schema-configuration.md): saiba como definir o esquema de destino do seu destino para o qual os usuários podem mapear atributos de perfil e identidades.
* [Configuração do namespace de identidade](destination-configuration/identity-namespace-configuration.md): saiba como configurar as identidades compatíveis com seu destino. Essa configuração preenche as identidades do público-alvo no [etapa de mapeamento](../../ui/activate-segment-streaming-destinations.md#mapping) da interface do usuário do Experience Platform, em que os usuários mapeiam identidades e atributos de seus esquemas XDM para o esquema em seu destino.
* [Entrega de destino](destination-configuration/destination-delivery.md): saiba como configurar exatamente para onde os dados exportados vão e qual regra de autenticação é usada no local onde os dados serão direcionados.
* [Configuração de metadados de público](destination-configuration/audience-metadata-configuration.md): saiba como os metadados de público, como nomes de público-alvo ou IDs, devem ser compartilhados entre o Experience Platform e o seu destino.
* [Política de agregação](destination-configuration/aggregation-policy.md): saiba como configurar uma política de agregação para determinar como as solicitações HTTP para o seu destino devem ser agrupadas e armazenadas em lote.
* [Configuração em lote](destination-configuration/batch-configuration.md): Defina várias configurações de nomenclatura de arquivos e agendamento de exportação disponíveis para os usuários ao se conectarem ao seu destino na interface de usuário do Experience Platform.
* [Qualificações do perfil histórico](destination-configuration/historical-profile-qualifications.md): saiba mais sobre as qualificações de perfil históricas compatíveis com destinos criados com o Destination SDK.

## Configuração de metadados de público {#audience-metadata-configuration}

Esse componente permite configurar como os públicos-alvo são criados, atualizados ou excluídos de forma programática no destino. Para destinos baseados em arquivo, permite configurar uma notificação sempre que os arquivos forem entregues com êxito ao destino. Você pode configurar essa funcionalidade por meio da [endpoint de templates de público](../metadata-api/create-audience-template.md).

## Próximas etapas {#next-steps}

Após a leitura deste artigo, você tem uma visão geral da funcionalidade fornecida pelo Destination SDK e quais páginas devem ser lidas para obter mais informações sobre configurações específicas. Em seguida, você pode ler os guias que incluem todas as etapas para [configurar um streaming](../guides/configure-destination-instructions.md) ou um [destino baseado em arquivo](../guides/configure-file-based-destination-instructions.md) usando o Destination SDK.
