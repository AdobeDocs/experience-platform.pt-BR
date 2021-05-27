---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform de 26 de maio de 2021.
doc-type: release notes
last-update: May 26, 2021
author: ens72741
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: c608ee8360fd07d6f98b31eed3b4691dc7124e12
workflow-type: tm+mt
source-wordcount: '1340'
ht-degree: 3%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 26 de maio de 2021**

Novos recursos no Adobe Experience Platform:

- [Painéis](#dashboards)

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Destinations]](#destinations)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [Perfil do cliente em tempo real](#profile)
- [Sandboxes](#sandboxes)
- [Fontes](#sources)

## Painéis {#dashboards}

O Adobe Experience Platform fornece vários painéis através dos quais você pode visualizar insights importantes sobre os dados de sua organização, conforme capturados durante os instantâneos diários.

| Recurso | Descrição |
| --- | --- |
| Insights do perfil | O painel de perfis fornece uma visão geral diária das métricas de Perfil do cliente em tempo real para cada política de mesclagem organizacional no Experience Platform. Esses insights de perfil estão disponíveis a todos os usuários com a capacidade de acessar e exibir dados de Perfil no Platform. |
| Insights do público | O painel de segmentos fornece insights relacionados ao público-alvo para todos os usuários com acesso para visualizar segmentos na Platform. O painel fornece uma visão geral diária das métricas de público-alvo para públicos-alvo criados com a interface do usuário do Construtor de segmentos ou importados da Adobe Audience Manager. |
| Insights de ativação | O painel de destinos está disponível para todos os usuários com a capacidade de acessar e visualizar destinos. O painel fornece uma visão geral diária das métricas de ativação para ativações em todos os destinos. |
| Insights específicos do usuário | A aparência dos painéis pode ser personalizada por cada usuário, incluindo a capacidade de modificar o layout do painel adicionando, removendo, redimensionando e reorganizando widgets. |
| Criação e gerenciamento de widgets | Todos os widgets padrão e personalizados são acessíveis aos profissionais de marketing em um repositório centralizado para democratizar a criação e o compartilhamento de insights:<br/><ul><li>A guia padrão contém widgets fornecidos pelo Adobe acessíveis no contexto do painel. </li><li>A guia personalizada contém widgets personalizados criados pela organização, incluindo uma opção para ocultar widgets da exibição.</li><li>O fluxo de trabalho de criação de widget dentro de Perfis e insights de público permite a edição, seleção, visualização e publicação de widgets personalizados.</li></ul> |
| Insights personalizados | Permissões de acesso permitem que engenheiros de dados e especialistas de marketing personalizem atributos de perfil disponíveis para a criação de widgets. |

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo a [visão geral dos painéis](../../dashboards/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

| Recurso | Descrição |
| ------- | ----------- |
| Avisos de erro menos rigorosos | As mensagens de erro do Mapeador de preparação de dados agora serão mais lenientes, fornecendo avisos em vez de erros, juntamente com linhas parcialmente transformadas. |
| Novas funções | Adição de funções para obter chaves, anexar elementos a uma matriz existente, anexar elementos de várias matrizes a uma matriz existente, usar objetos para criar matrizes e usar o nome do objeto JSON como um literal de string. |

Para obter mais informações, consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## [!DNL Destinations] {#destinations}

[!DNL Destinations] são integrações pré-criadas com plataformas de destino que permitem a ativação contínua de dados do Adobe Experience Platform. Você pode usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas por email, anúncios direcionados e muitos outros casos de uso.

| Recurso | Descrição |
| ------- | ----------- |
| Monitoramento aprimorado (beta) | Aumento dos recursos de monitoramento para destinos, incluindo informações para destinos em lote e streaming |
| [Exportação de arquivo incremental mais rápida (beta)](../../destinations/ui/activate-destinations.md#export-incremental-files) | Adição da capacidade de exportar arquivos incrementais para destinos a cada 3, 6, 8 ou 12 horas. <br> <br>No momento, esse recurso está na versão beta e só está disponível para alguns clientes. Os clientes não beta podem exportar arquivos incrementais uma vez por dia. |
| [Suporte à chave de desduplicação (beta)](../../destinations/ui/activate-destinations.md#deduplication-keys) | Adição da capacidade de definir namespaces de identidade ou atributos de perfil como chaves de desduplicação. Chaves de desduplicação eliminam a possibilidade de ter vários registros do mesmo perfil em um arquivo de exportação. <br> <br>No momento, esse recurso está em beta e só está disponível para um número selecionado de clientes. |

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

O Experience Data Model (XDM) é uma especificação de código aberto criada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo se comunicar com serviços no Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

| Recurso | Descrição |
| --- | --- |
| Grupos de campos de esquema | O termo &quot;mixin&quot; foi atualizado para &quot;field group&quot;. Essa alteração é refletida na interface do usuário do Adobe Experience Platform. Além disso, a API do Registro de Schema tem um novo ponto de extremidade [field groups](../../xdm/api/field-groups.md), enquanto o ponto de extremidade mixins foi substituído como um ponto de extremidade herdado. Consulte a [documentação XDM](../../xdm/home.md) para obter mais informações. |

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] O permite consolidar os dados do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Mesclar atualizações do fluxo de trabalho da política | Ao criar e atualizar políticas de mesclagem na interface do usuário, os usuários agora podem visualizar 20 perfis de amostra com base no esquema de união. Isso permite que os usuários visualizem a aparência dos perfis do cliente antes de salvar as configurações da política de mesclagem. Para obter mais informações, consulte o [guia da interface do usuário de políticas de mesclagem](../../profile/merge-policies/ui-guide.md). |
| Relatório de sobreposição de conjunto de dados | O relatório de sobreposição de conjunto de dados fornece visibilidade sobre a composição do armazenamento de Perfil, expondo os conjuntos de dados que mais contribuem para o público-alvo endereçável. Além de fornecer insights dos dados do Perfil, este relatório ajuda os usuários a tomar ações para otimizar o uso da licença, como definir um limite para a duração de determinados dados. Para saber mais, siga o tutorial em [gerar o relatório de sobreposição de conjunto de dados](../../profile/tutorials/dataset-overlap-report.md). |

Para obter mais informações sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados [!DNL Profile], comece lendo a [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Sandboxes] {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer os aplicativos de experiência digital em escala global. Geralmente, as empresas executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, teste e implantação desses aplicativos, além de garantir a conformidade operacional. Para atender a essa necessidade, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

| Recurso | Descrição |
| ------- | ----------- |
| Várias sandboxes de produção | Agora é possível criar e gerenciar várias sandboxes de produção na sua Organização IMS e dedicar sandboxes de produção específicas a linhas distintas de negócios, marcas, projetos ou regiões. Consulte os tutoriais sobre como criar uma sandbox de produção [na interface do usuário](../../sandboxes/ui/user-guide.md) ou [usando a API](../../sandboxes/api/overview.md) para obter mais informações. |

### Limitações conhecidas

- Cada Experience Cloud Organization vem com uma sandbox de produção padrão pré-criada. Essa sandbox atua como destino padrão para cada solicitação enviada para a plataforma a partir de outro aplicativo do Adobe ou de não-Adobe que não esteja (ainda) em conformidade com a sandbox. A sandbox de produção padrão não poderá ser redefinida se o gráfico de identidade hospedado nela também estiver sendo usado pelo Adobe Analytics para o recurso [Análise entre dispositivos (CDA)](https://experienceleague.adobe.com/docs/analytics/components/cda/overview.html) ou se o gráfico de identidade hospedado nele também estiver sendo usado pelo Adobe Audience Manager para o recurso [Destinos baseados em pessoas (PBD)](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/destinations/people-based/people-based-destinations-overview.html).
- As sandboxes de produção usadas para o compartilhamento bidirecional de segmentos com o Adobe Audience Manager ou o serviço principal de público-alvo não podem ser redefinidas nem excluídas.
- Todas as sandboxes de produção e desenvolvimento criadas pelo usuário podem ser excluídas, exceto a sandbox de produção padrão.

Para obter mais informações sobre sandboxes, consulte a [visão geral das sandboxes](../../sandboxes/home.md).

## [!DNL Sources] {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| ------- | ----------- |
| Suporte à interface do usuário para assimilação de arquivo compactado | Agora é possível visualizar e assimilar arquivos compactados JSON ou delimitados usando fontes de armazenamento em nuvem na interface do usuário do . Para obter mais informações, consulte o tutorial em [configurar um fluxo de dados para uma conexão de origem de armazenamento em nuvem na interface do usuário](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md). |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
