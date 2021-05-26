---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform de 26 de maio de 2021.
doc-type: release notes
last-update: May 26, 2021
author: ens72741
exl-id: 8f2c9bf8-1487-46e4-993b-bd9b63774cab
source-git-commit: 8508d213834bb21951df4fe118732b60465b6d73
workflow-type: tm+mt
source-wordcount: '831'
ht-degree: 4%

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