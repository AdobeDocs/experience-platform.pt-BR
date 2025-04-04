---
title: Notas de versão de agosto de 2024 da Adobe Experience Platform
description: As notas de versão de agosto de 2024 da Adobe Experience Platform.
exl-id: 153891e9-fd82-4894-a047-c8d82f214fef
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1565'
ht-degree: 95%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 20 de agosto de 2024**

>[!TIP]
>
>Consulte a [visão geral da documentação de casos de uso de exemplo](https://experienceleague.adobe.com/pt-br/docs/experience-platform/rtcdp/use-cases/overview) para saber mais sobre vários casos de uso, como prospecção, aquisição, entre outros que sua organização pode alcançar com a Real-Time CDP.

Atualizações dos recursos existentes e da documentação na Experience Platform:

- [Controle de acesso baseado em atributos](#abac)
- [Assimilação de dados](#data-ingestion)
- [Destinos](#destinations)
- [Experience Data Model (XDM)](#xdm)
- [Serviço de identidade](#identity-service)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Controle de acesso baseado em atributos {#abac}

O controle de acesso baseado em atributos é um recurso da Adobe Experience Platform que oferece maior flexibilidade para gerenciar o acesso de usuários para marcas que valorizam a privacidade. É possível atribuir objetos individuais, como campos de esquema e segmentos, a funções de usuário. Esse recurso permite conceder ou revogar o acesso a objetos individuais para usuários específicos da Experience Platform em sua organização.

Por meio do controle de acesso baseado em atributos, os administradores da sua organização podem controlar o acesso dos usuários a dados pessoais confidenciais (SPD), informações de identificação pessoal (PII) e outros tipos personalizados de dados em todos os fluxos de trabalho e recursos da Experience Platform. Admins podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.

**Novo recurso**

| Atualização de recursos | Descrição |
| --- | --- |
| Novo recurso do Gerenciador de permissões | Agora é possível usar o [Gerenciador de permissões](../../access-control/abac/permission-manager/overview.md) para gerar relatórios usando consultas simples, o que ajuda a entender o gerenciamento de acesso, reduzindo o tempo gasto com a verificação de permissões de acesso em vários fluxos de trabalho e níveis de granularidade. Para obter mais informações sobre como criar relatórios para usuários e funções, consulte o [Guia do usuário do gerenciador de permissões](../../access-control/abac/permission-manager/permissions.md). ![Imagem da interface da Experience Platform com destaque para o Gerenciador de permissões no menu de navegação esquerdo.](assets/august/permission-manager-rn.png "Gerenciador de permissões na interface."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Para obter mais informações sobre o controle de acesso baseado em atributos, consulte a [visão geral do controle de acesso baseado em atributos](../../access-control/abac/overview.md). Para obter um guia abrangente sobre o fluxo de trabalho do controle de acesso baseado em atributos, leia o [guia completo do controle de acesso baseado em atributos](../../access-control/abac/end-to-end-guide.md).

## Ingestão de dados (atualizado em 23 de agosto) {#data-ingestion}

A Adobe Experience Platform fornece um conjunto avançado de recursos para assimilar qualquer tipo e qualquer latência de dados. Você pode assimilar usando APIs de lote ou transmissão, origens construídas pela Adobe, parceiros de integração de dados ou a interface da Adobe Experience Platform.

**Atualização do tratamento do formato de data na ingestão de dados em lote**

Esta versão aborda um problema com o *tratamento do formato de data* na ingestão de dados em lote. Anteriormente, o sistema transformava campos de data inseridos por clientes como `Date` no formato `DateTime`. Devido a isso, o fuso horário era adicionado automaticamente nos campos, causando dificuldades para usuários que preferiam ou exigiam o formato `Date`. A partir de agora, o fuso horário não será adicionado automaticamente a campos do tipo `Date`. Essa atualização garante que o formato exportado dos dados corresponda ao formato representado no perfil desse campo, conforme solicitado por clientes.

Campos `Date` antes dessa versão: `"birthDate": "2018-01-12T00:00:00Z"`
Campos `Date` após essa versão: `"birthDate": "2018-01-12"`

Leia mais sobre [ingestão em lote](/help/ingestion/batch-ingestion/overview.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados** {#new-updated-destinations}

| Destino | Descrição |
| ----------- | ----------- |
| [Braze](/help/destinations/catalog/mobile-engagement/braze.md) | O [!UICONTROL Braze] gerencia várias instâncias diferentes de seus painéis e pontos de acesso REST. Clientes do [!UICONTROL Braze] devem usar o ponto de acesso REST correto com base na instância para a qual foram provisionados(as). Esta versão adiciona um novo ponto de acesso US-07 que é possível selecionar ao se conectar ao [!UICONTROL Braze]. |

{style="table-layout:auto"}

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Recurso | Descrição |
| ----------- | ----------- |
| Disponibilidade geral da exportação de arquivos sob demanda para destinos em lote. | A opção de exportar arquivos sob demanda para destinos em lote agora está disponível para todos(as) os(as) clientes. Consulte a [documentação dedicada](../../destinations/ui/export-file-now.md) para obter mais detalhes. |
| Edição dos agendamentos de exportação para vários públicos-alvo exportados na [etapa de agendamento](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | Agora a opção de editar os agendamentos de exportação para vários públicos-alvo exportados diretamente da etapa de agendamento do fluxo de trabalho de ativação de público-alvo está disponível para todos(as) os(as) clientes. ![Imagem da interface da Experience Platform com destaque para a opção Editar agendamento na etapa de agendamento.](assets/august/edit-schedule.png "Opção Editar agendamento na etapa de agendamento."){width="250" align="center" zoomable="yes"} |
| Edição de nomes de arquivos para vários públicos-alvo exportados na [etapa de agendamento](../../destinations/ui/activate-batch-profile-destinations.md#scheduling). | Agora a opção de editar os nomes de vários arquivos exportados diretamente da etapa de agendamento do fluxo de trabalho de ativação de público-alvo está disponível para todos(as) os(as) clientes. ![Imagem da interface da Experience Platform com destaque para a opção Editar nome do arquivo na etapa de agendamento.](assets/august/edit-file-name.png "Opção Editar nome do arquivo na etapa de agendamento."){width="250" align="center" zoomable="yes"} |
| Remoção de vários públicos-alvo de um fluxo de dados a partir da página [Detalhes do destino](../../destinations/ui/destination-details-page.md#bulk-remove). | Agora a opção de remover vários públicos-alvo de fluxos de dados existentes a partir da página **[!UICONTROL Detalhes do destino]** está disponível para todos(as) os(as) clientes. ![Imagem da interface da Experience Platform com destaque para a opção Remover públicos-alvo na página Detalhes do destino.](assets/august/bulk-remove-audiences.png "Opção Remover públicos-alvo na página Detalhes do destino."){width="250" align="center" zoomable="yes"} |
| Exportação de vários arquivos sob demanda para destinos em lote a partir da página [Detalhes do destino](../../destinations/ui/destination-details-page.md#bulk-export). | Agora a opção de exportar vários arquivos sob demanda para destinos em lote a partir da página **[!UICONTROL Detalhes do destino]** está disponível para todos(as) os(as) clientes. ![Imagem da interface da Experience Platform com destaque para a opção Exportar arquivo agora na página Detalhes do destino.](assets/august/bulk-export-file-now.png "Opção Exportar arquivo agora na página Detalhes do destino."){width="250" align="center" zoomable="yes"} |
| Edição de nomes de arquivos para vários públicos-alvo exportados na página [Detalhes do destino](../../destinations/ui/destination-details-page.md#bulk-edit-file-names). | Agora é possível editar os nomes de vários arquivos exportados diretamente da página **[!UICONTROL Detalhes do destino]**. ![Imagem da interface da Experience Platform com destaque para a opção Editar nome do arquivo na página Detalhes do destino.](assets/august/edit-file-name-destination-details.png "Opção Editar nome do arquivo na página Detalhes do destino."){width="250" align="center" zoomable="yes"} |
| Remoção de vários conjuntos de dados de um fluxo de dados a partir da página [Detalhes do destino](../../destinations/ui/export-datasets.md#remove-dataset). | Agora a opção para remover vários conjuntos de dados de um fluxo de dados está disponível para todos(as) os(as) clientes. ![Imagem da interface da Experience Platform com destaque para a opção Remover conjuntos de dados na página Detalhes do destino.](assets/august/bulk-remove-datasets.png "Opção Remover conjuntos de dados na página Detalhes do destino."){width="250" align="center" zoomable="yes"} |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de destinos](../../destinations/home.md).

## Experience Data Model (XDM) {#xdm}

O XDM é uma especificação de código aberto que fornece estruturas e definições comuns (esquemas) para dados inseridos na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Fluxo de criação de esquema assistido por aprendizado de máquina | Use algoritmos avançados de aprendizado de máquina para analisar seus arquivos de dados de amostra e criar automaticamente esquemas otimizados usando campos padrão e personalizados.<br>Recursos principais:<br><ul><li>Criação de esquema mais rápida: gere esquemas diretamente de arquivos de dados de amostra usando campos XDM recomendados e gerados por aprendizado de máquina.</li><li>Evolução de esquema flexível: adicione ou atualize campos facilmente no esquema gerado.</li><li>Integração perfeita: totalmente integrado ao fluxo de criação de esquema principal na interface de esquemas, garantindo uma experiência fluida e coesa.</li><li>Revisão e edição eficientes: visualize e atualize rapidamente o esquema usando o editor de exibição simples, tornando o processo de criação mais eficiente e fácil de usar.</li></ul><br>Para saber mais, leia o [Guia do fluxo de trabalho de criação de esquemas assistido por aprendizado de máquina](../../xdm/ui/ml-assisted-schema-creation.md). |

{style="table-layout:auto"}

Para obter mais informações sobre o XDM no Experience Platform, consulte a [visão geral do sistema XDM](../../xdm/home.md).

## Serviço de identidade {#identity-service}

Use o Serviço de identidade da Adobe Experience Platform para criar uma visão abrangente dos clientes e seus comportamentos pela união de identidades entre dispositivos e sistemas, permitindo fornecer experiências digitais pessoais e impactantes em tempo real.

**Documentação atualizada**

| Recurso | Descrição |
| --- | --- |
| Guia de configurações de gráficos | Leia o [Guia de configurações de gráficos](../../identity-service/identity-graph-linking-rules/example-configurations.md) para obter informações sobre cenários de gráficos comuns que você pode encontrar ao trabalhar com regras de vinculação de gráficos e dados de identidade. O guia de configurações de gráficos fornece exemplos que variam de cenários de gráficos simples para uma única pessoa a cenários de gráficos complexos e hierárquicos para várias pessoas. Também é possível usar o guia para obter exemplos de eventos e configurações de algoritmo que podem ser inseridas na [interface de simulação de gráfico](../../identity-service/identity-graph-linking-rules/graph-simulation.md), bem como detalhamentos de como as identidades principais são selecionadas em determinados cenários de gráficos. |

{style="table-layout:auto"}

Para obter mais informações sobre o Serviço de identidade, leia a [Visão geral do serviço de identidade](../../identity-service/home.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] permite segmentar dados relacionados a indivíduos (como clientes, prospectos, usuários ou organizações) que estão armazenados na [!DNL Experience Platform] em públicos-alvo. Você pode criar públicos-alvo por meio de definições de segmento ou outras fontes a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos-alvo são configurados e mantidos de forma centralizada na [!DNL Experience Platform] e podem ser acessados a qualquer momento usando as soluções da Adobe.

**Recursos atualizados**

| Recurso | Descrição |
| ------- | ----------- |
| Detalhes de ingestão | Para públicos-alvo originados de um upload personalizado, é possível visualizar de forma mais abrangente os detalhes de sua ingestão na página de detalhes do público-alvo. Além disso, é possível aplicar rótulos aos atributos de conteúdo selecionando o esquema e os atributos desejados para rotulagem. Mais informações sobre a seção de detalhes da ingestão podem ser encontradas no [Guia do portal de público-alvo](../../segmentation/ui/audience-portal.md#ingestion-details). |

{style="table-layout:auto"}

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## Origens

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

Use fontes na Experience Platform para assimilar dados de um aplicativo da Adobe ou de uma fonte de dados de terceiros.

**Recurso atualizado**

| Recurso | Descrição |
| --- | --- |
| Atualizações no conector de origem do Adobe Analytics | A página de atividade do conjunto de dados não exibe informações sobre lotes, pois o conector de origem do Analytics é totalmente gerenciado pela Adobe. É possível monitorar o fluxo dos dados por meio de métricas sobre a ingestão de registros. Leia o guia sobre como criar uma [conexão de origem de dados do Analytics](../../sources/tutorials/ui/create/adobe-applications/analytics.md) para obter mais informações. |

**Documentação atualizada**

| Documentação atualizada | Descrição |
| --- | --- |
| Documentação ampliada com respeito à atualização de fluxos de dados | O guia sobre [atualização de fluxos de dados de fontes existentes na interface](../../sources/tutorials/ui/update-dataflows.md) foi atualizado para fornecer mais informações sobre a variedade de configurações que você pode realizar em um fluxo de dados existente. O guia também foi atualizado para esclarecer o comportamento esperado ao reabilitar um fluxo de dados desabilitado. |

{style="table-layout:auto"}

Para obter mais informações, leia a [visão geral de fontes](../../sources/home.md).
