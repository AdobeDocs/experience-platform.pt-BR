---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 14 de outubro de 2020
doc-type: release notes
last-update: October 13, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 8f646c26ce73671ef4e427d8cba51091a8884795
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 4%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 14 de outubro de 2020**

- [Preparação de dados](#data-prep)
- [Perfil do cliente em tempo real](#profile)
- [Serviço de segmentação](#segmentation)
- [Fontes](#sources)
- [Tempo para o valor](#time-to-value)

## Preparação de dados {#data-prep}

O Data Prep permite que os engenheiros de dados mapeiem, transformem e validem dados para e do Experience Data Model (XDM).

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Função `is_set`  | A `is_set` função permite verificar a presença de um atributo nos dados de origem. `is_set` pode ser usado em combinação com `is_empty` para verificar a presença do atributo e a presença do valor dentro do atributo. |
| Função `get_values`  | A `get_values` função permite obter os valores do mapa de entrada para qualquer tecla. |

Para obter mais informações, leia a visão geral [da Preparação de](../../data-prep/home.md)dados.

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com [!DNL Real-time Customer Profile]o, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] permite consolidar seus dados de clientes diferentes em uma visualização unificada, oferecendo uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

| Recurso | Descrição |
| ------- | ----------- |
| Adições à API de pré-visualização do perfil | A API de pré-visualização do Perfil (`/previewsamplestatus`) agora inclui a capacidade de visualização de um detalhamento do total de fragmentos do perfil na organização IMS, bem como de visualização da distribuição de fragmentos do perfil nas namespaces de identidade. |
| Atualizações da visualização do schema união | Na interface do usuário do Experience Platform, os usuários podem encontrar mais facilmente informações relacionadas a todos os schemas e conjuntos de dados que contribuem para o schema da união, bem como os principais atributos da superfície, como campos de identidade e relacionamento. Essas atualizações melhoram a capacidade de solucionar problemas e validar se os perfis estão configurados corretamente, se as identidades estão corretamente agrupadas e se os dados foram assimilados com êxito. |

Para obter mais informações sobre [!DNL Real-time Customer Profile], incluindo tutoriais e práticas recomendadas para trabalhar com [!DNL Profile] dados, leia a visão geral [do Perfil do cliente em tempo](../../profile/home.md)real.

## Serviço de segmentação {#segmentation}

O Adobe Experience Platform Segmentation Service fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar audiências a partir de seus [!DNL Real-time Customer Profile] dados. Esses segmentos são configurados e mantidos centralmente [!DNL Platform], tornando-os facilmente acessíveis por qualquer aplicativo Adobe.

[!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo comercializável de pessoas dentro da sua base de clientes. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Remoção do limite de segmentação de fluxo | O limite de sete dias para o período de pesquisa foi removido. |

Para obter mais informações sobre [!DNL Segmentation Service], consulte a visão geral da [segmentação](../../segmentation/home.md)

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Mapeamento hierárquico | Você pode pré-visualização um arquivo de origem hierárquico, como JSON ou Parquet, durante o processo de ingestão de dados. |
| Suporte de autenticação SSH para SFTP | Você pode conectar sua conta SFTP com [!DNL Platform] chaves SSH abertas RSA/DSA. See the [SFTP overview](../../sources/connectors/cloud-storage/ftp-sftp.md) for more information. |
| Melhorias no UX | Você pode ativar seu conjunto de dados para [!DNL Profile] durante o processo de ingestão de dados. Consulte o tutorial de fluxo de trabalho [de fluxo de dados do armazenamento](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) em nuvem para obter mais informações. |

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.

## Tempo para o valor {#time-to-value}

A Adobe Experience Platform permite que as equipes de Operações de marketing construam uma visualização de 360 graus de seus clientes sem exigir uma ampla experiência em engenharia de dados. O objetivo é acelerar as equipes e valorizar a velocidade dos dados.

&quot;Tempo para valorizar&quot; recorta entre personas. Os engenheiros de dados podem concluir as tarefas de forma eficiente e rápida, com transparência de atividade de dados, para que um perfil robusto e escalonável do cliente em tempo real esteja disponível mais cedo. Os profissionais de marketing podem usar o perfil completo e robusto do cliente para segmentação e ativação.

### Destaques dos recursos

#### Esquema

Atualiza a utilização e o fluxo de trabalho, além de fornecer insights prontos para uso, padronização e transparência dos campos principais nas composições do schema. Expõe a linha de dados para a combinação de modelos de dados individuais representados como o &quot;schema de união&quot;, fornecendo insight sobre a estrutura e os ingredientes para o Perfil do cliente em tempo real.

- Atualização do fluxo de trabalho do schema
   - Use atalhos para o tipo mais comum de schemas XDM, com configurações automatizadas no editor de schemas e recomendações de combinação baseadas em seus objetivos
   - Aumente a eficiência do fluxo de trabalho com vários recursos de seleção e pré-visualização de mixagem
   - Forneça transparência nos principais atributos da composição do schema, incluindo identidade, relacionamento e campos obrigatórios e obsoletos
- União Linha de dados do Schema e Principais atributos Transparência

#### Ingestão de dados e coleta

O mapeamento automático, a pré-visualização de mapeamento e a atualização de usabilidade trazem dados de qualquer plataforma ou fonte para uso em perfis, segmentação de downstream e ativação. O sistema tem a eficiência e inteligência para facilitar o uso desse processo, mesmo para pessoas fora da TI.

- Acesso mais fácil a fontes de dados com cartão de página de catálogo e atualização do padrão de ação em linha da tabela de dados
- Campo/expressão calculada para ingestão de dados
- As recomendações de mapeamento de dados agilizam o processo de ingestão
- Mapeamento de pré-visualizações e validações

#### Configuração do perfil

O visualizador de perfis amigável ao profissional de marketing com personalização ajuda você a entender a composição de um perfil para uso em casos de segmentação, planejamento e ativação. O fluxo de trabalho consolidado monta o perfil de forma controlada e eficiente, fornecendo um fluxo de trabalho passo a passo para a política de mesclagem.

- Visualização cada perfil individual em um visualizador de perfis aprimorado que exibe um painel com personalização total, permitindo dados agrupados entre canais com base nas metas comerciais do profissional de marketing.
- Edite atributos padrão e personalizados no widget Informações básicas, de acordo com as necessidades dos negócios.
- Personalize widgets com atributos do perfil do cliente em tempo real, usando o seletor de schemas de união. O schema de união é derivado dos modelos de dados subjacentes usados na ingestão dos dados do perfil.


#### Monitoramento

Garante a transparência do fluxo de dados e fornece insight sobre a integridade do tráfego de dados no sistema a partir dos conectores de origem, fornecendo mais autoatendimento e uma acionabilidade mais rápida para solucionar problemas.

- Monitore todas as execuções de fluxo e veja uma visualização detalhada de cada execução, incluindo status de conclusão, duração da execução, lista de arquivos processados, erros e diagnósticos acionáveis