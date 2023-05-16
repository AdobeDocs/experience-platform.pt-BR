---
description: O serviço de destinos no Adobe Experience Platform usa endpoints de configuração para vários componentes que criam a funcionalidade de destinos . Saiba como esses componentes combinados permitem que o Experience Platform se conecte a parceiros de destino, envie mensagens personalizadas e ative dados de perfil no ecossistema digital.
title: Opções de configuração no Destination SDK
source-git-commit: 65a658208b48a50184e55a6d64cdf7ad6de0f04f
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# Opções de configuração no Destination SDK

O serviço de destinos no Adobe Experience Platform usa endpoints de configuração para vários componentes que criam a funcionalidade de destinos .

Combinados, esses componentes permitem que o Experience Platform se conecte às plataformas de destino, envie mensagens personalizadas, exporte arquivos personalizados e ative os dados do perfil no ecossistema digital.

O diagrama abaixo mostra uma visão geral de alto nível dos componentes que você pode configurar por meio do Destination SDK para criar seu próprio destino. Esses componentes são descritos mais adiante.

![Diagrama mostrando os componentes do Destination SDK, os pontos de extremidade de configuração e as operações suportadas por eles.](../assets/functionality/destination-sdk-components-diagram.png)

## Configuração de servidor {#server-configuration}

A configuração do servidor de destino vincula informações sobre suas especificações do servidor e o modelo usado pelo Adobe para fornecer cargas ao destino.

Por exemplo, é aqui que você especifica os pontos de extremidade da API de seu lado que o Experience Platform precisa se conectar, bem como os cabeçalhos e o formato das chamadas de API que a Platform fará.

Para destinos com base em arquivo, essa configuração também inclui a formatação de arquivo e os formatos de compactação compatíveis com seu destino. Você pode configurar as funcionalidades descritas abaixo por meio do [ponto de extremidade de servidores de destino](../authoring-api/destination-server/create-destination-server.md).

* [Especificações do servidor](destination-server/server-specs.md): Um template de configuração que contém informações sobre o local de armazenamento ou o terminal HTTP para o qual os dados são enviados.
* [Especificações do modelo](destination-server/templating-specs.md): Nesse modelo, você pode definir como estruturar a solicitação da API HTTP para o terminal, incluindo como transformar campos de atributo de perfil entre o esquema XDM e o formato compatível com a plataforma. Use essas informações junto com a [formato de mensagem](destination-server/message-format.md) documentação.
* [Formato de mensagem](destination-server/message-format.md): Esta seção aborda informações detalhadas sobre idiomas de modelos suportados, formatos de mensagem e as informações necessárias para o Adobe configurar a integração com sua plataforma. Use essas informações junto com a [especificações do modelo](destination-server/templating-specs.md) documentação.
* [Especificações do arquivo](destination-server/file-formatting.md): Um template de configuração que inclui as opções de formatação e compactação de arquivo para o destino do lote.

## Configuração de destino {#destination-configuration}

Esse endpoint de configuração contém informações básicas e avançadas sobre o destino. Por exemplo, é aqui que você especifica os tipos de identidade que seu destino pode suportar, o formato desejado de arquivos exportados (para destinos com base em arquivo) e vários atributos de interface do usuário para seu cartão de destino na interface do usuário do Adobe Experience Platform.

Consulte a documentação abaixo para obter detalhes sobre cada um dos componentes de configuração de destino. Você pode configurar as funcionalidades descritas abaixo por meio do [endpoint de destinos](../authoring-api/destination-configuration/create-destination-configuration.md).

* [Configuração de autenticação do cliente](destination-configuration/customer-authentication.md): Selecione o mecanismo de autenticação que o Experience Platform deve usar para se conectar ao seu destino. Essa configuração gera a variável [Configurar novo destino](../../ui/connect-destination.md) na interface do usuário do Experience Platform, onde os usuários conectam o Experience Platform às contas que têm com seu destino.
* [Autenticação OAuth2](destination-configuration/oauth2-authentication.md): Saiba mais sobre todas as [!DNL OAuth2] fluxos de autenticação suportados pelo Destination SDK e obter instruções para configurar [!DNL OAuth2] autenticação para o seu destino.
* [Campos de dados do cliente](destination-configuration/customer-data-fields.md): Saiba como criar campos de entrada na interface do usuário do Experience Platform que permitem que os usuários especifiquem várias informações relevantes para como se conectar e exportar dados para seu destino.
* [Atributos da interface do usuário](destination-configuration/ui-attributes.md): Saiba como configurar os atributos da interface do usuário, como o link da documentação, a categoria da placa de destino e o tipo e a frequência da conexão de destino, para destinos criados com o Destination SDK.
* [Configuração do esquema](destination-configuration/schema-configuration.md): Saiba como definir o esquema de destino do seu destino para o qual os usuários podem mapear atributos e identidades de perfil.
* [Configuração do namespace de identidade](destination-configuration/identity-namespace-configuration.md): Saiba como configurar as identidades suportadas pelo seu destino. Essa configuração preenche as identidades de destino na variável [etapa de mapeamento](../../ui/activate-segment-streaming-destinations.md#mapping) da interface do usuário do Experience Platform, onde os usuários mapeiam identidades e atributos de seus esquemas XDM para o esquema no seu destino.
* [Delivery de destino](destination-configuration/destination-delivery.md): Saiba como configurar para onde exatamente os dados exportados vão e qual regra de autenticação é usada no local onde os dados serão enviados.
* [Configuração de metadados de público-alvo](destination-configuration/audience-metadata-configuration.md): Saiba como os metadados de segmento, como nomes de segmentos ou IDs, devem ser compartilhados entre o Experience Platform e seu destino.
* [Política de agregação](destination-configuration/aggregation-policy.md): Saiba como configurar uma política de agregação para determinar como as solicitações HTTP para seu destino devem ser agrupadas e armazenadas em lote.
* [Configuração em lote](destination-configuration/batch-configuration.md): Configure várias configurações de programação de nomeação e exportação de arquivos disponíveis para os usuários ao se conectar ao seu destino na interface do usuário do Experience Platform.
* [Qualificações de perfil histórico](destination-configuration/historical-profile-qualifications.md): Saiba mais sobre as qualificações de perfil histórico suportadas por destinos criados com o Destination SDK.

## Configuração de metadados de público-alvo {#audience-metadata-configuration}

Esse componente permite configurar como os públicos-alvo/segmentos são criados, atualizados ou excluídos de forma programática no seu destino. Para destinos com base em arquivos, isso permite configurar uma notificação sempre que os arquivos forem entregues com êxito ao seu destino. É possível configurar essa funcionalidade por meio do [endpoint de modelos de público-alvo](../metadata-api/create-audience-template.md).

## Próximas etapas {#next-steps}

Ao ler este artigo, agora você tem uma visão geral da funcionalidade fornecida pelo Destination SDK e quais páginas devem ser lidas para obter mais informações sobre configurações específicas. Em seguida, você pode ler os guias que incluem todas as etapas para [configurar um streaming](../guides/configure-destination-instructions.md) ou [destino baseado em arquivo](../guides/configure-file-based-destination-instructions.md) usando o Destination SDK.
