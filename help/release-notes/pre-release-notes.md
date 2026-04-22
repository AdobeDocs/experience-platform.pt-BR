---
title: Notas de pré-lançamento do Experience Platform
description: Uma visualização das notas de versão mais recentes do Adobe Experience Platform.
exl-id: f2c41dc8-9255-4570-b459-4f9fc28ee58b
source-git-commit: d052230ec5ddc4a28495f4928ab32957bf9038ac
workflow-type: tm+mt
source-wordcount: '1136'
ht-degree: 13%

---

# Notas de pré-lançamento do Adobe Experience Platform

>[!IMPORTANT]
>
>Este documento é uma **visualização** das notas de versão do mês atual. Os itens da versão estão sujeitos a alterações e podem ser adicionados ou removidos na versão final.

>[!TIP]
>
>Consulte a documentação a seguir para obter as notas de versão de outros aplicativos da Adobe Experience Platform:
>
>- [Adobe Journey Optimizer](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer/using/whats-new/release-notes)
>- [Adobe Journey Optimizer B2B](https://experienceleague.adobe.com/pt-br/docs/journey-optimizer-b2b/user/release-notes)
>- [Customer Journey Analytics](https://experienceleague.adobe.com/pt-br/docs/analytics-platform/using/releases/latest)
>- [Composição de público-alvo federado](https://experienceleague.adobe.com/en/docs/federated-audience-composition/using/release-notes)
>- [Real-Time CDP Collaboration](https://experienceleague.adobe.com/en/docs/real-time-cdp-collaboration/using/latest)

**Data de lançamento: abril de 2026**

Novos recursos e atualizações dos recursos existentes no Adobe Experience Platform:

- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de consultas](#query-service)
- [Real-Time CDP](#rtcdp)
- [Sandboxes](#sandboxes)
- [Serviço de segmentação](#segmentation-service)
- [Fontes](#sources)

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados**

| Destino | Descrição |
| --- | --- |
| [!BADGE Beta]{type=Informative} [Correspondência de Cliente de Anúncios da Microsoft](../destinations/catalog/advertising/microsoft-ads-customer-match.md) | Combinar clientes por endereço de email e reengajar com eles em todo o [!DNL Microsoft Advertising Network], incluindo anúncios de Pesquisa e Público-alvo. Vincule sua conta do [!DNL Microsoft Advertising] à Real-Time CDP para automatizar a criação e o gerenciamento de listas de correspondência de clientes diretamente da Experience Platform. |
| [!BADGE Beta]{type=Informative} [Reddit Custom Audience](../destinations/catalog/advertising/reddit-custom-audience.md) | Enviar audiências do Experience Platform para [!DNL Reddit Ads]. Conecte sua conta do [!DNL Reddit], mapeie identidades e ative públicos para alcançar as pessoas que exploram ativamente seus interesses no [!DNL Reddit]. |
| [Amazon Ads v2](../destinations/catalog/advertising/amazon-ads-v2.md) | [!DNL Amazon Ads v2] é o destino atual de todas as novas conexões de [!DNL Amazon Ads]. Se você tiver uma conexão [(Legacy) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md) existente, ela continuará a funcionar sem as alterações necessárias. O [!DNL Amazon Ads v2] se conecta ao [!DNL Ads Data Manager], que fornece suporte para tipos de identidade expandidos, campos relacionados a endereços e compartilhamento de dados entre produtos [!DNL Amazon Ads], melhorando o direcionamento e as taxas de correspondência de público-alvo em comparação ao [(Herdado) [!DNL Amazon Ads]](../destinations/catalog/advertising/amazon-ads.md). |
| [!DNL Rokt] | Use o [!DNL Rokt] para conectar os públicos da Experience Platform à tomada de decisões em tempo real orientada por IA, melhorando o desempenho da campanha por meio de direcionamento, supressão e personalização mais precisos. |

{style="table-layout:auto"}

**Correções e melhorias**

| Correção | Descrição |
| --- | --- |
| Suporte personalizado de monitoramento do Personalization | O painel de monitoramento para destinos agora oferece suporte a [!DNL Custom Personalization] destinos. A observação de limitação que excluiu [!DNL Custom Personalization] do monitoramento foi removida. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos Destinos](../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados trazidos para o Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum para fornecer insights de maneira mais rápida e integrada.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Visibilidade de uso do esquema do grupo de campos | Visualize quais esquemas usam um grupo de campos na página de detalhes e os explore em uma caixa de diálogo classificável com metadados de esquema. Isso ajuda a avaliar rapidamente as dependências e o impacto sem sair. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral do sistema XDM](../xdm/home.md).

## Serviço de consultas {#query-service}

Use o Serviço de Consulta para consultar dados no Adobe Experience Platform [!DNL Data Lake] com SQL padrão. Associe-se a qualquer conjunto de dados do [!DNL Data Lake] e capture os resultados da consulta como um novo conjunto de dados para usar em relatórios, no Data Science Workspace ou na assimilação no Perfil do Cliente em Tempo Real.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Data Distiller Accelerators | Execute e programe modelos SQL gerenciados pela Adobe e com parâmetros na interface do usuário do Serviço de consulta para executar análises comuns sem gravar SQL. Isso ajuda a padronizar os workflows de análise e reutilizar a lógica de consulta confiável em sua organização. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral do Serviço de consulta](../query-service/home.md).

## Real-Time CDP {#rtcdp}

O [!DNL Real-Time CDP] fornece perfis de clientes unificados e acionáveis assimilando, processando e ativando dados em vários canais em tempo real. Com o Real-Time CDP, as organizações podem conectar fontes de dados existentes, criar e ativar públicos-alvo avançados e garantir a ativação em conformidade com a privacidade nos destinos, tudo isso no Experience Platform. Isso permite que profissionais de marketing, analistas e equipes de TI ofereçam experiências oportunas e altamente personalizadas para seus clientes por meio de campanhas de marketing ininterruptas em vários canais.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Real-Time CDP MCP (Beta) | Use o MCP do Real-Time CDP para trazer o Real-Time CDP para agentes de IA e clientes compatíveis com MCP, permitindo que você interaja com as ferramentas do Real-Time CDP diretamente por meio de sua experiência LLM nativa. Conectando um cliente compatível com MCP (como Claude, ChatGPT, Claude Code, Codex, Cursor ou VS Code) ao `https://rtcdp-mcp.adobe.io/mcp`, você pode usar a linguagem natural para inspecionar públicos, configuração de destino e histórico de execução de ativação, sem gravar chamadas de API REST do Experience Platform ou navegar em vários fluxos de trabalho de interface do usuário. Depois de concluir um logon no Adobe com base em navegador, você terá acesso somente leitura a ferramentas que incluem: <ul><li>Pesquisar públicos existentes</li><li>Visualizar associação de público-alvo</li><li>Listar Tipos de Destino</li><li>Listar Contas Configuradas</li><li>Listar destinos configurados</li><li>Listar Conexões Do Source</li><li>Listar Conexões de Destino</li><li>Inspecionar execuções de ativação</li></ul>. Cada solicitação requer parâmetros `imsOrgId` e `sandboxName` para garantir que as ações tenham escopo para sua organização e sandbox. Observe que não há suporte para operações de gravação nesta versão do Beta. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral do Real-Time CDP](../rtcdp/home.md).

## Sandboxes {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Cópia Expressa | Use a Cópia Expressa para copiar objetos para uma sandbox de destino em uma única ação da [Interface do Usuário de Ferramentas da Sandbox](/help/sandboxes/ui/sandbox-tooling.md#express-copy). Os objetos dependentes são detectados automaticamente e criados na sandbox de destino ou reutilizados quando já existem. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral das sandboxes](../sandboxes/home.md).

## Serviço de segmentação {#segmentation-service}

Use o Serviço de segmentação para criar públicos-alvo a partir dos dados de clientes e gerenciar todo o ciclo de vida deles no Experience Platform.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Monitoramento da segmentação de transmissão | Monitore a segmentação por transmissão com visibilidade em tempo real da taxa de avaliação, da latência de assimilação e das métricas de qualidade de dados no nível da sandbox, do conjunto de dados e do segmento. Visualize métricas, incluindo taxa de avaliação, latência de assimilação P95, registros recebidos, registros avaliados, registros com falha e registros ignorados. Além disso, visualize novos perfis qualificados e desqualificados por segmento. Use esses insights para identificar violações de capacidade e problemas de assimilação antes que afetem seus dados. |

{style="table-layout:auto"}

Para obter mais informações, leia a [Visão geral dos públicos-alvo](../segmentation/home.md).

## Fontes {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Fontes novas ou atualizadas**

| Fonte | Descrição |
| --- | --- |
| Desabilitação automática de fluxo de dados | Os fluxos de dados de assimilação de origens que falham continuamente por 30 dias são desativados automaticamente, ajudando a exibir fluxos de dados não íntegros e a reduzir execuções com falha repetidas. |
| [!DNL Delta Sharing] | Você pode usar a origem [!DNL Delta Sharing] para trazer tabelas Delta para a Experience Platform por meio de um protocolo de compartilhamento de dados aberto e seguro. Depois de configurar uma conexão [!DNL Delta Sharing] e selecionar os compartilhamentos e tabelas que deseja assimilar, o Platform traz automaticamente esses dados para seus conjuntos de dados para que você possa usá-los para análise, segmentação e ativação. |
| [!DNL Meta Ads] (Beta) | Você pode usar o Beta (conector de origem) do [!DNL Meta Ads] no espaço de trabalho Fontes para autenticar em [!DNL Meta], selecionar suas contas de anúncio e agendar a assimilação de dados de campanha e desempenho do [!DNL Meta Ads] nos conjuntos de dados do Experience Platform. |
| [!DNL Talon.One] | Agora você pode conectar o Experience Platform ao [!DNL Talon.One] usando as novas fontes de lote e streaming do [!DNL Talon.One]. Use as novas fontes para assimilar dados do perfil de fidelidade, bem como eventos de transação e atividade de fidelidade para a Experience Platform. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../sources/home.md).
