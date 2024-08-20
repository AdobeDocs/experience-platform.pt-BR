---
title: Notas de versão da Adobe Experience Platform de agosto de 2024
description: As notas de versão de agosto de 2024 para Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 6d8c785a1e876ed6a729efbe01ad8fb4507bda0d
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 26%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quarta-feira, 20 de agosto de 2024**

>[!TIP]
>
>Veja uma [visão geral da documentação de casos de uso de exemplo](https://experienceleague.adobe.com/en/docs/experience-platform/rtcdp/use-cases/overview) para saber mais sobre vários casos de uso, como prospecção, aquisição e muito mais, que sua organização pode obter com a Real-Time CDP.

Atualizações dos recursos e da documentação existentes no Experience Platform:

- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de identidade](#identity-service)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Recurso | Descrição |
| ----------- | ----------- |
| A exportação de arquivos sob demanda para destinos em lote agora está disponível de modo geral. | A opção de exportar arquivos por demanda para destinos em lote agora está disponível para todos os clientes. Consulte a [documentação dedicada](../../destinations/ui/export-file-now.md) para obter mais detalhes. |
| Edite os agendamentos de exportação para vários públicos exportados na [etapa de agendamento](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | A opção para editar os agendamentos de exportação para vários públicos-alvo exportados diretamente da etapa de agendamento do fluxo de trabalho de ativação de público-alvo agora está disponível para todos os clientes. ![Imagem da interface de usuário do Experience Platform destacando a opção Editar agendamento na etapa de agendamento.](../2024/assets/august/edit-schedule.png) {width="250" align="center" zoomable="yes"} |
| Edite nomes de arquivos para vários públicos exportados na [etapa de agendamento](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | A opção para editar os nomes de vários arquivos exportados diretamente da etapa de agendamento do fluxo de trabalho de ativação de público agora está disponível para todos os clientes. ![Imagem da interface de usuário do Experience Platform destacando a opção Editar nome do arquivo na etapa de agendamento.](../2024/assets/august/edit-file-name.png) {width="250" align="center" zoomable="yes"} |
| Remova vários públicos-alvo de um fluxo de dados da página [Detalhes do destino](../../destinations/ui/destination-details-page.md#bulk-remove). | A opção de remover vários públicos-alvo de fluxos de dados existentes da página **[!UICONTROL Detalhes do destino]** agora está disponível para todos os clientes. ![Imagem da interface de usuário do Experience Platform destacando a opção Remover públicos-alvo na página Detalhes do Destino.](../2024/assets/august/bulk-remove-audiences.png) {width="250" align="center" zoomable="yes"} |
| Exporte vários arquivos por demanda para destinos em lote a partir da página [Detalhes do destino](../../destinations/ui/destination-details-page.md#bulk-export). | A opção de exportar vários arquivos por demanda para destinos em lote a partir da página **[!UICONTROL Detalhes do destino]** agora está disponível para todos os clientes. ![Imagem da interface de usuário do Experience Platform destacando a opção Exportar arquivo agora na página Detalhes do Destino.](../2024/assets/august/bulk-export-file-now.png) {width="250" align="center" zoomable="yes"} |
| Edite nomes de arquivos para vários públicos exportados da página [Detalhes do destino](../../destinations/ui/destination-details-page.md#bulk-edit-file-names). | Agora é possível editar os nomes de vários arquivos exportados diretamente da página **[!UICONTROL Detalhes do destino]**. ![Imagem da interface de usuário do Experience Platform destacando a opção de edição de nome de arquivo na página de detalhes do destino.](../2024/assets/august/edit-file-name-destination-details.png) {width="250" align="center" zoomable="yes"} |
| Remova vários conjuntos de dados de um fluxo de dados da página [Detalhes do destino](../../destinations/ui/export-datasets.md#remove-dataset). | A opção para remover vários conjuntos de dados de um fluxo de dados agora está disponível para todos os clientes. ![Imagem da interface de usuário do Experience Platform destacando a opção Remover conjuntos de dados na página de detalhes do destino.](../2024/assets/august/bulk-remove-datasets.png) {width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral dos destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Fluxo de criação de esquema assistido por ML | Use algoritmos avançados de aprendizado de máquina do para analisar arquivos de dados CSV de amostra e criar automaticamente esquemas otimizados usando campos padrão e personalizados.<br>Principais Recursos:<br><ul><li>Criação de esquema mais rápida: gere esquemas diretamente de arquivos de dados de amostra usando campos XDM recomendados e gerados pelo ML.</li><li>Evolução flexível do esquema: adicione ou atualize facilmente campos no esquema gerado.</li><li>Integração contínua: totalmente integrado ao fluxo de criação do esquema principal no URL do esquema, garantindo uma experiência do usuário perfeita e coesa.</li><li>Revisão e edição eficientes: visualize e atualize rapidamente seu esquema usando o editor de Exibição plana, tornando o processo de criação mais eficiente e fácil de usar.</li></ul> |

{style="table-layout:auto"}

<!-- To learn more, read the [ML-assisted schema creation overview](../../xdm/ui/ml-assisted-schema-creation.md)  -->

Para obter mais informações sobre o XDM na Platform, consulte a [Visão geral do sistema de XDM](../../xdm/home.md).

## Serviço de identidade {#identity-service}

Use o Serviço de identidade da Adobe Experience Platform para criar uma visualização abrangente dos clientes e seus comportamentos, unindo identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real.

**Documentação atualizada**

| Recurso | Descrição |
| --- | --- |
| Guia de configurações de gráfico | Leia o [guia de configurações de gráfico](../../identity-service/identity-graph-linking-rules/example-configurations.md) para obter informações sobre cenários de gráficos comuns que você pode encontrar ao trabalhar com regras de vinculação de gráficos de identidade e dados de identidade. O guia de configurações de gráfico fornece exemplos que variam de cenários de gráficos simples para uma única pessoa a cenários de gráficos complexos e hierárquicos para várias pessoas. Você também pode usar o guia para obter exemplos de eventos e configurações de algoritmo que você pode inserir na [interface de simulação de gráfico](../../identity-service/identity-graph-linking-rules/graph-simulation.md), bem como detalhamentos de como as identidades primárias são selecionadas tendo em conta determinados cenários gráficos. |

{style="table-layout:auto"}

Para obter mais informações sobre o Serviço de identidade, leia a [Visão geral do Serviço de identidade](../../identity-service/home.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] permite segmentar dados relacionados a indivíduos (como clientes, prospectos, usuários ou organizações) que estão armazenados na [!DNL Experience Platform] em públicos-alvo. Você pode criar públicos-alvo por meio de definições de segmento ou outras fontes a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos-alvo são configurados e mantidos de forma centralizada na [!DNL Platform] e podem ser acessados a qualquer momento usando as soluções da Adobe.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Detalhes de assimilação | Para públicos-alvo com a origem de upload personalizada, você pode visualizar os detalhes da assimilação do público-alvo na página de detalhes do público-alvo. Além disso, você pode aplicar rótulos aos atributos de carga selecionando o esquema e os atributos desejados para rotulagem. Mais informações sobre a seção de detalhes da assimilação podem ser encontradas no [Guia do Portal de Público](../../segmentation/ui/audience-portal.md#ingestion-details). |

{style="table-layout:auto"}

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Use fontes no Experience Platform para assimilar dados de um aplicativo Adobe ou de uma fonte de dados de terceiros.

**Documentação atualizada**

| Atualização da documentação | Descrição |
| --- | --- |
| Documentação ampliada sobre atualização de fluxos de dados | O guia sobre [atualização de fluxos de dados de fontes existentes na interface](../../sources/tutorials/ui/update-dataflows.md) foi atualizado para fornecer mais informações sobre a variedade de configurações que você pode fazer em um fluxo de dados existente. O guia também foi atualizado para esclarecer o comportamento esperado quando um fluxo de dados desativado é reativado. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral das fontes](../../sources/home.md).