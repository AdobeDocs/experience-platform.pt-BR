---
solution: Experience Platform
title: Adobe Experience Platform Destination SDK glossary
description: Entenda a terminologia importante ao criar um destino usando Experience Platform Destination SDK.
source-git-commit: 3dae91fbe46dc3e23c6ac0cfb10c25ac8473876a
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 1%

---


# Adobe Experience Platform Destination SDK glossary

Consulte este glossário para obter as definições dos termos usados no Destination SDK. Para outros termos do Adobe Experience Platform, consulte [glossário Experience Platform](/help/landing/glossary.md).

## A

**Política de agregação**: ao configurar como os dados devem ser exportados para o destino de transmissão em tempo real, você pode definir como os dados do perfil são agregados antes de serem enviados para a plataforma de destino. Isso ajuda a otimizar a entrega de dados, agrupando registros de dados com base em critérios específicos, reduzindo a frequência de chamadas de API e melhorando a eficiência geral. Diferentes políticas podem ser configuradas para atender a vários requisitos de destino, garantindo que os dados sejam empacotados e entregues da maneira mais eficaz. [Leia mais](/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md).

**Configuração de metadados de público**: uma configuração de metadados de público refere-se à configuração estruturada e aos parâmetros definidos no Adobe Experience Platform que permitem a criação, atualização e exclusão programáticas de segmentos de público-alvo em um destino especificado. Essa configuração utiliza modelos de metadados de público-alvo para se alinhar às especificações da API de marketing da plataforma de destino. Leia mais sobre o [configuração de metadados de público](/help/destinations/destination-sdk/functionality/audience-metadata-management.md) e [macros disponíveis](/help/destinations/destination-sdk/functionality/audience-metadata-management.md#macros).

## D

**Endpoint de configuração de destino**: um endpoint de configuração de destino no Adobe Experience Platform, especificamente o `/authoring/destinations` O endpoint da API é usado para criar, recuperar, atualizar e excluir configurações para destinos. Essas configurações definem como os dados do Adobe Experience Platform são entregues a vários sistemas ou destinos externos, como plataformas de marketing, serviços de armazenamento em nuvem ou outros endpoints de processamento de dados. Leia mais sobre [opções de configuração disponíveis](/help/destinations/destination-sdk/functionality/configuration-options.md#destination-configuration) e visualize o [documentação de referência](/help/destinations/destination-sdk/authoring-api/destination-configuration/create-destination-configuration.md).

**Instância de destino**: uma configuração específica de uma configuração de destino no Adobe Experience Platform, criada e gerenciada por meio da interface do usuário do Experience Platform. Ele inclui todos os parâmetros e credenciais necessários para conectar e enviar dados ao destino. Depois de estabelecer a conexão com o destino, você pode obter a ID da instância de destino quando [procurar uma conexão com seu destino](/help/destinations/ui/destination-details-page.md).

![Imagem da interface do usuário sobre como obter a ID da instância de destino](/help/destinations/destination-sdk/assets/testing-api/get-destination-instance-id.png)

## P

**[!DNL Pebble]modelo**: A [!DNL Pebble] O template é usado para transformar dados exportados do Adobe Experience Platform no formato exigido pela plataforma de destino. Ele emprega o [!DNL Pebble] linguagem de modelo, que permite a transformação dinâmica de dados por meio de funções como `filter`, `for`, `if`, e `set`. O Adobe Experience Platform inclui funções personalizadas adicionais, como `addedSegments` e `removedSegments`. Esses modelos ajudam a formatar elementos de dados, como carimbos de data e hora e associações de público-alvo, para atender às especificações do destino. Saiba mais [aqui](/help/destinations/destination-sdk/functionality/destination-server/message-format.md) e [aqui](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**Destino privado**: integrações personalizadas criadas por clientes individuais da Adobe Experience Platform. Elas são personalizadas para atender a necessidades específicas dos negócios e só podem ser acessadas na organização do cliente, oferecendo flexibilidade nas configurações de exportação de dados. Os destinos privados estão disponíveis somente para clientes do Real-Time CDP Ultimate. [Leia mais](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

**Destino público**: uma integração disponível publicamente no catálogo do Adobe Experience Platform. Esses destinos são padronizados, de marca e simplificam a configuração do cliente, fornecendo parâmetros pré-configurados. Elas podem ser acessadas por todos os clientes que usam o Adobe Experience Platform. [Leia mais](/help/destinations/destination-sdk/overview.md#productized-custom-integrations).

## S

**Modelo de documentação de autoatendimento**: o modelo de documentação de autoatendimento fornece um formato estruturado que você pode usar para documentar seu destino. Ele inclui seções para obter uma visão geral, casos de uso, pré-requisitos, identidades, públicos-alvo, tipos de exportação e frequência compatíveis, bem como etapas para conectar ao destino, ativar públicos-alvo e mapear atributos. Use este modelo para garantir uma documentação abrangente e consistente, permitindo que os clientes comecem a usar seu destino rapidamente e entendam os casos de uso fornecidos. Leia mais sobre [como documentar seu destino](/help/destinations/destination-sdk/docs-framework/documentation-instructions.md), [baixar o modelo de documentação de autoatendimento mais recente](/help/destinations/destination-sdk/assets/docs-framework/yourdestination-template.zip), e [visualizar como ele é renderizado](/help/destinations/destination-sdk/docs-framework/self-service-template.md).

## T

**Especificações e estratégias de modelos**: as especificações do modelo são configurações usadas para formatar solicitações HTTP enviadas do Adobe Experience Platform para um destino. Eles transformam campos de atributo de perfil do esquema XDM em um formato compatível com a plataforma de destino. Usar uma linguagem de modelo semelhante a [!DNL Jinja], essas especificações permitem transformações de dados dinâmicos com base em regras específicas e dados de entrada. [Saiba mais](/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md).

**API de teste**: a API de teste permite validar as configurações de destino antes de enviar uma solicitação de publicação. Ele fornece ferramentas para gerar perfis de amostra e testar o fluxo de dados, garantindo que a configuração corresponda aos requisitos do destino. A API é compatível com destinos de transmissão e baseados em arquivo (em lote), oferecendo uma maneira de simular dados e solucionar possíveis problemas no processo de configuração. Leia mais sobre a API de teste para [transmissão](/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md) e [destinos baseados em arquivo](/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md).

**Modelo de transformação**: um modelo de transformação personaliza o formato dos dados do esquema XDM do Adobe para o formato esperado do destino. [Saiba mais](/help/destinations/destination-sdk/functionality/destination-server/message-format.md).