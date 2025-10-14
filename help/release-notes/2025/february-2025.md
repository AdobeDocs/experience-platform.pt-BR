---
title: Notas da versão de fevereiro de 2025 da Adobe Experience Platform
description: Notas da versão de fevereiro de 2025 da Adobe Experience Platform.
exl-id: 734a9484-516e-4dd7-9503-8fcdc50cbaac
source-git-commit: c8fe5f05b7dcef7db2ae44d5b6575e123cbd014d
workflow-type: tm+mt
source-wordcount: '1677'
ht-degree: 16%

---

# Notas de versão da Adobe Experience Platform

>[!TIP]
>
>Esta versão inclui melhorias no complemento Federated Audience Composition. Para obter mais informações, leia as [notas de versão da Federated Audience Composition](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/release-notes).

**Data de lançamento: quarta-feira, 18 de fevereiro de 2025**

Atualizações dos recursos e da documentação existentes no Adobe Experience Platform:

- [Assistente de IA](#ai-assistant)
- [Serviço de catálogo](#catalog-service)
- [Preparação de dados](#data-prep)
- [Destinos](#destinations)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)
- [Atualizações na documentação](#documentation-updates)
   - [Comparação entre a rede e o hub Edge](#edge)
   - [API do Serviço de fluxo expandida para origens](#flow-service)
   - [Fazer backup de configurações de objeto usando ferramentas de sandbox](#back-up-object-configurations)
   - [Possibilite um centro de excelência usando ferramentas de sandbox](#center-of-excellence)
   - [Retenção de conjunto de dados de evento de experiência no data lake](#experience-event-dataset-retention)

## Assistente de IA {#ai-assistant}

O Assistente de IA no Adobe Experience Platform é uma experiência de conversação que você pode usar para acelerar seus fluxos de trabalho em aplicativos do Adobe. Você pode usar o AI Assistant para entender melhor o conhecimento do produto, solucionar problemas ou pesquisar informações e encontrar insights operacionais. O Assistente de IA é compatível com Experience Platform, Real-Time Customer Data Platform, Adobe Journey Optimizer e Customer Journey Analytics.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Disponibilidade geral de insights operacionais | Os insights operacionais no Assistente de IA agora estão em disponibilidade geral. Os insights operacionais se referem às respostas que o AI Assistant gera sobre os objetos de metadados (atributos, públicos, fluxos de dados, conjuntos de dados, destinos, jornadas, esquemas e fontes), incluindo contagens, pesquisas e impacto de linhagem. Os insights operacionais não observam dados na sandbox. Para obter mais informações, leia o [Guia da interface do usuário do Assistente de IA](../../ai-assistant/ui-guide.md). |
| Suporte para preenchimento automático de perguntas | Ao inserir uma pergunta no Assistente de IA, agora é possível selecionar em uma lista de perguntas recomendadas que o Assistente de IA fornece. Use esse recurso para acelerar ainda mais seus fluxos de trabalho com o Assistente de IA. Para obter mais informações, leia o manual sobre [usando o preenchimento automático de perguntas com o Assistente de IA](../../ai-assistant/ui-guide.md#use-question-autocomplete). |
| Suporte para observabilidade do conjunto de dados | Agora você pode usar o Assistente de IA para responder perguntas sobre métricas específicas do conjunto de dados, como tamanhos de armazenamento e contagens de linhas. As perguntas de observabilidade de dados aceitam qualificadores que podem ser usados para filtrar suas consultas por um determinado período de tempo. Para obter mais informações, leia o [guia de perguntas do Assistente de IA](../../ai-assistant/questions.md). |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral do Assistente de IA](../../ai-assistant/home.md).

## Serviço de catálogo {#catalog-service}

O Serviço de catálogo é o sistema de registro para localização e linhagem de dados na Adobe Experience Platform. Embora todos os dados assimilados na Experience Platform sejam armazenados no data lake como arquivos e diretórios, o Catálogo retém os metadados e a descrição desses arquivos e diretórios para fins de pesquisa e monitoramento.

| Recurso | Descrição |
| --- | --- |
| Novo ponto de acesso de API | Gerencie seus metadados de conjunto de dados do Adobe Experience Platform com mais eficiência com o novo ponto de extremidade [API de Serviço de Catálogo /v2/dataSets/{DATASET_ID}](../../catalog/api/update-object.md#patch-v2-notation). Atualize facilmente atributos complexos e profundamente aninhados do conjunto de dados à medida que o sistema cria automaticamente níveis de caminho ausentes para economizar tempo, reduzir etapas manuais e minimizar erros. |

{style="table-layout:auto"}

Para obter mais informações sobre o Serviço de Catálogo, leia a [Visão geral do Serviço de Catálogo](../../catalog/home.md).

## Preparação de dados {#data-prep}

Use o preparo de dados para mapear, transformar e validar dados de e para o Experience Data Model (XDM).

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte aprimorado para importar e exportar mapeamentos | Agora você pode exportar mapeamentos para um arquivo CSV e configurá-los localmente em uma planilha. É possível importar os mapeamentos atualizados para o Experience Platform usando a interface de mapeamento na interface do. Você pode usar esse recurso para configurar grandes números de mapeamentos sem precisar criá-los manualmente na interface do usuário. Além disso, ao criar um novo fluxo de dados, você pode fazer upload de uma cópia dos mapeamentos diretamente no Experience Platform para acelerar o fluxo de trabalho. Para obter mais informações, leia o manual sobre [importação e exportação de mapeamentos](../../data-prep/ui/mapping.md#import-mapping). |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral do Preparo de Dados](../../data-prep/home.md).

## Destinos (atualizado em 20 de fevereiro) {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados** {#new-updated-destinations}

| Destino | Descrição |
| --- | --- |
| [(Beta) Sincronização de Pessoa do Marketo Engage](/help/destinations/catalog/adobe/marketo-engage-person-sync.md) | Use o conector [!DNL Marketo Engage Person Sync] para transmitir atualizações dos públicos-alvo para os registros correspondentes na sua instância [!DNL Marketo Engage]. Este conector de destino está na versão beta e só está disponível para clientes selecionados. Para solicitar acesso, entre em contato com o representante da Adobe. |
| [A conexão CRM da Trade Desk](/help/destinations/catalog/advertising/tradedesk-emails.md) está disponível ao público | A conexão [!DNL The Trade Desk CRM] agora está disponível. Use o destino do CRM do [!DNL The Trade Desk] para ativar perfis para sua conta do [!DNL Trade Desk] para direcionamento de público e supressão com base nos dados do CRM. |
| [Conexão de Perfis de Participante do RainFocus](/help/destinations/catalog/marketing-automation/rainfocus.md) | Use o destino [!DNL RainFocus Attendee Profiles] para transmitir perfis de clientes do Adobe Experience Platform para a plataforma [!DNL RainFocus] para criar e atualizar perfis de participantes. |
| [Disponibilidade geral da conexão de critério](/help/destinations/catalog/advertising/criteo.md) | A conexão [!DNL Criteo] agora está disponível. O Criteo capacita a publicidade confiável e impactante para trazer experiências mais ricas para cada consumidor através da internet aberta. Com o maior conjunto de dados de comércio do mundo e a melhor IA do setor, o Criteo garante que cada ponto de contato na jornada de compras seja personalizado para alcançar os clientes com o anúncio certo, na hora certa. |
| Conexão com o [[!DNL Amazon Ads] &#x200B;](../../destinations/catalog/advertising/amazon-ads.md) | O conector [!DNL Amazon Ads], anteriormente na versão beta, agora está disponível para o público geral. O conector também foi atualizado para enviar um sinal de consentimento concedido para todos os perfis que consentiram em usar seus dados pessoais para publicidade. Leia mais sobre o novo controle [Sinal de consentimento](../../destinations/catalog/advertising/amazon-ads.md#destination-details) do Amazon Ads. |

{style="table-layout:auto"}

**Funcionalidade nova ou atualizada** {#destinations-new-updated-functionality}

| Recurso | Descrição |
| --- | --- |
| Usar rótulos de acesso para gerenciar o acesso do usuário aos fluxos de dados de destino | Como parte da funcionalidade do [[!UICONTROL controle de acesso baseado em atributos]](/help/access-control/abac/overview.md) no Real-Time CDP, agora é possível aplicar rótulos de acesso aos [fluxos de dados de destino](/help/dataflows/ui/monitor-destinations.md). Dessa forma, você pode garantir que apenas um subconjunto de usuários em sua organização tenha acesso a fluxos de dados de destino específicos. <br> **Importante**: ao pesquisar fluxos de dados de destino usando a caixa de pesquisa na parte superior da interface do usuário do Experience Platform, os resultados podem incluir fluxos de dados de destino que os rótulos de acesso do usuário impedem que você veja. Esse comportamento será corrigido em uma atualização futura. |
| [Relatórios no nível do público-alvo](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) da [conexão com o Marketo Engage](/help/destinations/catalog/adobe/marketo-engage.md) | Agora você pode [exibir informações](/help/dataflows/ui/monitor-destinations.md#audience-level-dataflow-runs-for-streaming-destinations) sobre as identidades ativadas, excluídas ou com falha detalhadas em um nível de público-alvo, para cada público que faz parte dos fluxos de dados deste destino. |
| Suporte a públicos externos para as conexões [TikTok](/help/destinations/catalog/social/tiktok.md) e [Snap Inc](/help/destinations/catalog/advertising/snap-inc.md) | Você pode ativar públicos externos para esses destinos em [uploads personalizados](../../segmentation/ui/audience-portal.md#import-audience) e [Composição de Público Federado](https://experienceleague.adobe.com/pt-br/docs/federated-audience-composition/using/start/audiences). |
| Exportar arrays, mapas e objetos para destinos de armazenamento na nuvem | Ao usar o botão de alternância **[!UICONTROL Exportar matrizes, mapas, objetos]** ao se conectar a um destino de armazenamento na nuvem, você pode exportar novos objetos complexos para destinos selecionados. [Leia mais](/help/destinations/ui/export-arrays-maps-objects.md) sobre a funcionalidade. |

{style="table-layout:auto"}

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

- Um problema nas ferramentas de teste do Destination SDK foi corrigido. Alguns clientes ou parceiros encontraram problemas com a [ferramenta de geração de perfil de exemplo](/help/destinations/destination-sdk/testing-api/streaming-destinations/sample-profile-generation-api.md) devido a um formato sem suporte quando o esquema usado para gerar perfis incluía tipos de dados com um seletor `No format`.
- Correção de um problema ao atualizar a especificação de destinos `targetConnection` usando a API de Serviço de Fluxo. Em alguns casos, a operação do PATCH se comportaria de forma semelhante a uma operação POST, corrompendo os fluxos de dados existentes. Esse problema foi corrigido e todos os clientes podem usar a API de Serviço de Fluxo para atualizar suas especificações do `targetConnection`. [Leia mais](/help/destinations/api/edit-destination.md#patch-target-connection).
- Ao exportar perfis para destinos baseados em arquivo, a desduplicação garante que apenas um perfil seja exportado quando vários perfis compartilharem a mesma chave de desduplicação e o mesmo carimbo de data e hora de referência. Essa versão inclui uma atualização do processo de desduplicação, garantindo que execuções sucessivas com as mesmas coordenadas sempre produzam os mesmos resultados, melhorando a consistência. [Leia mais](/help/destinations/ui/activate-batch-profile-destinations.md#deduplication-same-timestamp).

Para obter mais informações, leia a [visão geral de destinos](../../destinations/home.md).

## Serviço de segmentação {#segmentation-service}

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Divisão persistente | A Composição de público-alvo agora é compatível com divisões persistentes. É possível fazer com que os públicos-alvo divididos permaneçam constantes ao dividir por perfil ao adicionar um namespace de identidade ao bloco Split. Mais informações sobre este recurso podem ser encontradas na [documentação de Composição do Público-alvo](../../segmentation/ui/audience-composition.md). |

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

Use fontes na Experience Platform para assimilar dados de um aplicativo da Adobe ou de uma fonte de dados de terceiros.

**Recurso atualizado**

| Recurso | Descrição |
| --- | --- |
| Suporte para Exibições em [!DNL Microsoft Dynamics] | Agora você pode assimilar `"entityType": "view"` ao usar a origem [!DNL Microsoft Dynamics]. Para obter mais informações, leia o guia em [conectando uma [!DNL Microsoft Dynamics] origem à Experience Platform](../../sources/tutorials/api/create/crm/ms-dynamics.md). |
| Novos endereços IP para incluir na lista de permissões | Você deve adicionar os seguintes endereços IP ao arquivo de inclui na lista de permissões para usar as fontes da Experience Platform com êxito.<br></br>**VA7**<ul><li>`48.211.4.136/29`</li><li>`48.211.4.144/28`</li><li>`48.211.4.160/29`</li><li>`40.84.85.144/28`</li><li>`40.84.85.192/28`</li></ul>**AUS5**<ul><li>`20.213.194.144/29`</li><li>`20.227.120.32/27`</li></ul> <br></br>Para obter mais informações, leia o [guia de inclui na lista de permissões de endereço IP de origens](../../sources/ip-address-allow-list.md). |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).

## Atualizações na documentação {#documentation-updates}

### Comparação entre Edge Network e hub {#edge}

A [comparação entre o Edge Network e o hub](../../landing/edge-and-hub-comparison.md) fornece uma visão geral detalhando as diferenças entre os dois tipos de servidor para o Adobe Experience Platform (hub e Edge Network), incluindo quais serviços estão disponíveis em cada tipo de servidor, locais dos servidores, bem como cenários recomendados para o uso de cada tipo de servidor.

### Referência da API do Serviço de Fluxo expandido para origens {#flow-service}

A [[!DNL Flow Service] referência de API](https://developer.adobe.com/experience-platform-apis/references/flow-service/#tag/Source-connections) para fontes foi atualizada com novos exemplos de solicitação e resposta de API. Use a referência de API expandida para criar e atualizar especificações de conexão ao integrar sua própria origem ao Experience Platform. Você também pode usar a referência de API expandida para executar transições de estado em suas entidades de origem, atualizar conexões de origem e de destino existentes e recuperar fluxos e especificações de fluxo de acordo com um critério de filtragem específico.

### Fazer backup de configurações de objeto usando ferramentas de sandbox {#back-up-object-configurations}

Leia o [guia de configuração do objeto de backup](../../sandboxes/use-cases/backup-object-configuration.md) para obter instruções passo a passo sobre como criar um pacote de backup usando ferramentas de sandbox para garantir que suas configurações de objeto estejam armazenadas e seguras.

### Possibilite um centro de excelência usando ferramentas de sandbox {#center-of-excellence}

Leia o [guia do centro de excelência](../../sandboxes/use-cases/center-of-excellence.md) para obter instruções passo a passo sobre como criar um pacote de &quot;sandbox dourada&quot; que funcione como um centro de excelência para compartilhar configurações importantes com eficiência.

### Retenção de conjunto de dados de evento de experiência no data lake {#experience-event-dataset-retention}

Assuma o controle da Retenção do conjunto de dados do evento de experiência no Adobe Experience Platform usando o TTL (Time-To-Live). [Este guia](../../catalog/datasets/experience-event-dataset-retention-ttl-guide.md) orientará você na avaliação, configuração e gerenciamento das configurações de TTL para remover automaticamente registros desatualizados, otimizar o armazenamento e manter seus dados relevantes. Descubra as práticas recomendadas, os casos de uso reais e as principais considerações para aprimorar o gerenciamento do ciclo de vida dos dados.
