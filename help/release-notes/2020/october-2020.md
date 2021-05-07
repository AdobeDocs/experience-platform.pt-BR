---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform de outubro de 2020
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
translation-type: tm+mt
source-git-commit: ab0798851e5f2b174d9f4241ad64ac8afa20a938
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 4%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 14 de outubro de 2020**

- [Preparação de dados](#data-prep)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)
- [Tempo para Valor](#time-to-value)

## Preparação de dados {#data-prep}

A Preparação de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Função `is_set`  | A função `is_set` permite verificar a presença de um atributo nos dados de origem. `is_set` pode ser usado em combinação com  `is_empty` para verificar a presença do atributo e a presença do valor no atributo. |
| Função `get_values`  | A função `get_values` permite obter os valores do mapa de entrada para qualquer chave específica. |

Para obter mais informações, leia a [Visão geral da preparação de dados](../../data-prep/home.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com [!DNL Real-time Customer Profile], você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] O permite consolidar seus dados de clientes diferentes em uma visualização unificada que oferece uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Adições à API de visualização do perfil | A API de visualização de perfil (`/previewsamplestatus`) agora inclui a capacidade de exibir um detalhamento do total de fragmentos de perfil na organização IMS, bem como exibir a distribuição de fragmentos de perfil nos namespaces de identidade. |
| Atualizações da exibição de esquema de união | Na interface do usuário do Experience Platform, os usuários podem encontrar mais facilmente informações sobre todos os esquemas e conjuntos de dados que contribuem para o esquema de união, bem como atributos principais de superfície, como campos de identidade e relação. Essas atualizações melhoram a capacidade de solucionar problemas e validar se os perfis estão configurados corretamente, as identidades são compiladas corretamente e os dados foram assimilados com êxito. |

Para obter mais informações sobre [!DNL Real-time Customer Profile], incluindo tutoriais e práticas recomendadas para trabalhar com dados [!DNL Profile], leia a [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

## Serviço de segmentação {#segmentation}

O Serviço de segmentação do Adobe Experience Platform fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar públicos a partir dos dados [!DNL Real-time Customer Profile]. Esses segmentos são configurados e mantidos centralmente em [!DNL Platform], tornando-os acessíveis a qualquer aplicativo do Adobe.

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Remoção do limite de segmentação de fluxo | O limite de sete dias para o período de pesquisa foi removido. |

Para obter mais informações sobre [!DNL Segmentation Service], consulte a [Visão geral da segmentação](../../segmentation/home.md)

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permite estruturar, rotular e aprimorar esses dados usando serviços [!DNL Platform]. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte à autenticação SSH para SFTP | Você pode conectar sua conta SFTP a [!DNL Platform] usando chaves SSH RSA/DSA Open. Consulte a [Visão geral do SFTP](../../sources/connectors/cloud-storage/sftp.md) para obter mais informações. |
| Melhorias no UX | Você pode ativar seu conjunto de dados para [!DNL Profile] durante o processo de assimilação de dados. Consulte o tutorial [cloud storage data aflow workflow](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obter mais informações. |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).

## Tempo para Valor {#time-to-value}

A Adobe Experience Platform permite que as equipes de operações de marketing criem uma visão de 360 graus de seus clientes sem exigir uma ampla experiência em engenharia de dados. O objetivo é acelerar equipes e valorizar a velocidade dos dados.

O &quot;Tempo para valor&quot; divide as personas. Os engenheiros de dados podem realizar tarefas de maneira eficiente e acelerada com transparência da atividade dos dados, para que um perfil robusto e dimensionável do cliente em tempo real esteja disponível mais cedo. Os profissionais de marketing podem usar o perfil completo e robusto do cliente para segmentação e ativação.

### Destaques dos recursos

#### Esquema

Atualiza a usabilidade e o fluxo de trabalho e fornece insights prontos para uso, padronização e transparência de campos principais em composições de esquema. Expõe a linhagem de dados para a combinação de modelos de dados individuais representados como o &quot;schema de união&quot;, fornecendo informações sobre a estrutura e os ingredientes para o Perfil do cliente em tempo real.

- Atualização do workflow do schema
   - Use atalhos para o tipo mais comum de esquemas XDM, com configurações automatizadas nas recomendações do editor de esquema e do grupo de campos do esquema, com base em seus objetivos
   - Aumente a eficiência do fluxo de trabalho com seleção de vários grupos de campos e recurso de visualização
   - Forneça transparência nos atributos principais da composição do schema, incluindo identidade, relacionamento e campos obrigatórios e obsoletos
- Linear de dados do esquema Union e transparência de atributos-chave

#### Assimilação e coleta de dados

O mapeamento automático, a visualização de mapeamento e a atualização de usabilidade trazem dados de qualquer plataforma ou fonte para uso no perfil, na segmentação de downstream e na ativação. O sistema tem eficiência e inteligência para facilitar o uso desse processo, mesmo para pessoas fora da TI.

- Acesso mais fácil a fontes de dados com o cartão de página de catálogo e a atualização do padrão de ação em linha da tabela de dados
- Campo/expressão calculado para assimilação de dados
- As recomendações de mapeamento de dados agilizam o processo de assimilação
- Visualização de mapeamento e validações

#### Configuração do perfil

O visualizador de perfil compatível com o profissional de marketing com personalização ajuda você a entender a composição de um perfil para uso na segmentação, no planejamento e nos casos de ativação. O fluxo de trabalho consolidado hidrata o perfil de forma controlada e eficiente, fornecendo um fluxo de trabalho passo a passo para a política de mesclagem.

- Visualize cada perfil individual em um visualizador de perfil aprimorado que exibe um painel com personalização total, permitindo dados agrupados entre canais com base nas metas de negócios do profissional de marketing.
- Edite atributos padrão e personalizados no widget Informações básicas, de acordo com as necessidades dos negócios.
- Personalize widgets com atributos do perfil do cliente em tempo real, usando o seletor de esquema de união. O schema de união é derivado dos modelos de dados subjacentes usados na assimilação de dados de perfil.


#### Monitoramento

Garante a transparência do fluxo de dados e fornece informações sobre a integridade do tráfego de dados no sistema a partir de conectores de origem, fornecendo mais autoatendimento e agilidade mais rápida para solucionar problemas de situações.

- Monitore todas as execuções de fluxo e veja uma exibição detalhada de cada execução, incluindo status de conclusão, duração da execução, lista de arquivos processados, erros e diagnósticos acionáveis
