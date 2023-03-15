---
title: Notas de versão da Adobe Experience Platform de outubro de 2020
description: As notas de versão de outubro de 2020 para o Adobe Experience Platform.
doc-type: release notes
last-update: October, 2020
author: crhoades, ens28527
exl-id: 89f5e2bd-8892-4d3f-a3fe-5433bb5ece7a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1016'
ht-degree: 4%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 14 de outubro de 2020**

- [Preparação de dados](#data-prep)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)
- [Tempo de implantação](#time-to-value)

## Preparação de dados {#data-prep}

O Preparo de dados permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Função `is_set`  | A variável `is_set` permite verificar a presença de um atributo nos dados de origem. `is_set` pode ser utilizado em combinação com `is_empty` para verificar a presença do atributo e a presença do valor dentro do atributo. |
| Função `get_values`  | A variável `get_values` permite obter os valores do mapa de entrada para qualquer chave fornecida. |

Para obter mais informações, leia a [Visão geral do Preparo de dados](../../data-prep/home.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde e quando eles interagem com sua marca. Com [!DNL Real-Time Customer Profile], você pode ter uma visão holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, de CRM e de terceiros. [!DNL Profile] O permite consolidar dados diferentes do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Adições da API de visualização de perfil | A API de visualização de perfil (`/previewsamplestatus`) agora inclui a capacidade de visualizar uma análise do total de fragmentos de perfil na organização do IMS, bem como visualizar a distribuição de fragmentos de perfil nos namespaces de identidade. |
| Atualizações de exibição de esquema de união | Na interface do usuário do Experience Platform, os usuários podem encontrar mais facilmente informações sobre todos os esquemas e conjuntos de dados que contribuem para o esquema de união, bem como destacar atributos-chave, como campos de identidade e relacionamento. Essas atualizações melhoram a capacidade de solucionar problemas e validar se os perfis estão configurados corretamente, se as identidades estão compiladas corretamente e se os dados foram assimilados com êxito. |

Para obter mais informações sobre [!DNL Real-Time Customer Profile], incluindo tutoriais e práticas recomendadas para trabalhar com a [!DNL Profile] dados, leia os [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## Serviço de segmentação {#segmentation}

O Serviço de segmentação da Adobe Experience Platform fornece uma interface de usuário e uma API RESTful que permite criar segmentos e gerar públicos-alvo a partir de seus [!DNL Real-Time Customer Profile] dados. Esses segmentos são configurados e mantidos de forma centralizada [!DNL Platform], tornando-os prontamente acessíveis por qualquer aplicativo Adobe.

[!DNL Segmentation Service] O define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas na sua base de clientes. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou eventos de séries temporais que representam interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Remoção do limite de segmentação de streaming | O limite de sete dias para o período de pesquisa foi removido. |

Para obter mais informações sobre [!DNL Segmentation Service], consulte o [Visão geral da segmentação](../../segmentation/home.md)

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte à autenticação SSH para SFTP | Você pode conectar sua conta SFTP ao [!DNL Platform] uso de chaves RSA/DSA Open SSH. Consulte a [Visão geral do SFTP](../../sources/connectors/cloud-storage/sftp.md) para obter mais informações. |
| Melhorias de UX | Você pode ativar seu conjunto de dados para [!DNL Profile] durante o processo de assimilação de dados. Consulte a [fluxo de trabalho de fluxo de dados do armazenamento na nuvem](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) tutorial para obter mais informações. |

Para saber mais sobre fontes, consulte a [visão geral das origens](../../sources/home.md).

## Tempo de implantação {#time-to-value}

A Adobe Experience Platform permite que as equipes de operações de marketing criem uma visualização de 360 graus de seus clientes sem exigir uma ampla experiência em engenharia de dados. O objetivo é acelerar as equipes e valorizar por meio da velocidade dos dados.

&quot;Tempo de implantação&quot; abrange personas. Os engenheiros de dados podem concluir as tarefas de maneira eficiente e acelerada com transparência da atividade de dados, para que um perfil do cliente em tempo real robusto e escalável esteja disponível antes. Os profissionais de marketing podem usar o perfil completo e robusto do cliente para segmentação e ativação.

### Destaques do recurso

#### Esquema

Atualiza a usabilidade e o fluxo de trabalho, além de fornecer insights, padronização e transparência imediatos dos principais campos nas composições do esquema. Expõe a linhagem de dados para a combinação de modelos de dados individuais representados como o &quot;esquema de união&quot;, fornecendo insights sobre a estrutura e os ingredientes para o Perfil do cliente em tempo real.

- Atualização do fluxo de trabalho de esquema
   - Use atalhos para o tipo mais comum de esquemas XDM, com configurações automatizadas no editor de esquemas e recomendações do grupo de campos de esquema com base em seus objetivos
   - Aumente a eficiência do fluxo de trabalho com a seleção de vários grupos de campos e o recurso de visualização
   - Forneça transparência sobre os principais atributos da composição do esquema, incluindo identidade, relacionamento e campos obrigatórios e obsoletos
- Linhagem de dados do esquema da união e transparência de atributos-chave

#### Assimilação e coleta de dados

O mapeamento automático, a pré-visualização de mapeamento e a atualização da usabilidade trazem dados de qualquer plataforma ou origem para uso em perfil, segmentação downstream e ativação. O sistema tem a eficiência e a inteligência para tornar esse processo mais fácil de usar, mesmo para pessoas fora da TI.

- Acesso mais fácil às fontes de dados com cartão de página de catálogo e atualização do padrão de ação em linha da tabela de dados
- Campo/expressão calculado para assimilação de dados
- As recomendações de mapeamento de dados aceleram o processo de assimilação
- Pré-visualização e validações de mapeamento

#### Configuração do perfil

Um visualizador de perfil compatível com o profissional de marketing com personalização ajuda você a entender a composição de um perfil para uso em casos de segmentação, planejamento e ativação. O fluxo de trabalho consolidado hidrata o perfil de maneira controlada e eficiente, fornecendo um fluxo de trabalho passo a passo para a política de mesclagem.

- Visualize cada perfil individual em um visualizador de perfil aprimorado que exibe um painel com personalização completa, permitindo dados agrupados entre canais com base nas metas de negócios do profissional de marketing.
- Edite atributos padrão e personalizados no widget de Informações básicas, de acordo com as necessidades dos negócios.
- Personalize widgets com atributos do perfil do cliente em tempo real, usando o seletor de esquema de união. O esquema de união é derivado dos modelos de dados subjacentes usados na assimilação de dados do perfil.


#### Monitoramento

Garante a transparência do fluxo de dados e fornece informações sobre a integridade do tráfego de dados no sistema a partir de conectores de origem, fornecendo mais autoatendimento e capacidade de ação mais rápida para solucionar problemas em situações.

- Monitore todas as execuções de fluxo e veja uma exibição detalhada de cada execução, incluindo status de conclusão, duração da execução, lista de arquivos processados, erros e diagnósticos acionáveis
