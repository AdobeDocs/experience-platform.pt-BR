---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral dos conjuntos de dados
topic: datasets
translation-type: tm+mt
source-git-commit: dcdd94a3a13a13b4104e57b74ecf613bc316b0af
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 2%

---


# Visão geral dos conjuntos de dados

Todos os dados ingeridos com êxito na Adobe Experience Platform são mantidos no Data Lake como conjuntos de dados. Um conjunto de dados é um armazenamento e uma construção de gerenciamento para uma coleção de dados, geralmente uma tabela, que contém um schema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados.

Este documento fornece uma visão geral de alto nível dos conjuntos de dados na plataforma da experiência.

## Criação de conjuntos de dados e rastreamento de metadados

O serviço de catálogo é o sistema de registro para localização e linhagem de dados na plataforma Experience e é usado para criar e gerenciar conjuntos de dados. O Catálogo rastreia os metadados de cada conjunto de dados, que inclui uma referência ao schema do Modelo de Dados de Experiência (XDM) ao qual o conjunto de dados está em conformidade (explicado na próxima seção) e o número de registros ingeridos nesse conjunto de dados.

Consulte a visão geral [do serviço de](../home.md) catálogo para obter mais informações.

## Impondo restrições nos dados do conjunto de dados

O Experience Data Model (XDM) é a estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente. Todos os dados ingeridos na Plataforma devem estar em conformidade com um schema XDM predefinido antes de serem persistentes no Data Lake como um conjunto de dados.

Todos os conjuntos de dados contêm uma referência ao schema XDM que restringe o formato e a estrutura dos dados que eles podem armazenar. Tentar carregar dados em um conjunto de dados que não esteja em conformidade com o schema XDM do conjunto de dados fará com que a ingestão falhe.

Para obter mais informações sobre o XDM, consulte a visão geral [do Sistema](../../xdm/home.md)XDM.

## Como inserir dados em conjuntos de dados

A ingestão de dados da plataforma Adobe Experience representa os vários métodos pelos quais a plataforma ingere dados de várias fontes. Independentemente do método de ingestão, todos os dados ingeridos com êxito são convertidos em arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Esses arquivos em lote são adicionados aos conjuntos de dados dedicados e persistem no Data Lake.

Consulte a visão geral [da ingestão de](../../ingestion/home.md) dados para obter mais informações.

## Aplicar rótulos de uso a conjuntos de dados

O Adobe Experience Platform Data Governance permite gerenciar dados do cliente para garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Usando a Rotulagem e Aplicação de Uso de Dados (DULE) como sua estrutura principal, o Data Governance permite aplicar rótulos de uso para classificar dados de acordo com as políticas de uso que se aplicam a esses dados.

Os rótulos de uso de dados podem ser aplicados a conjuntos de dados inteiros ou a campos de conjuntos de dados individuais. Os rótulos adicionados no nível do conjunto de dados são herdados por todos os campos dentro desse conjunto de dados.

Consulte a visão geral [do](../../data-governance/home.md) Data Governance para obter mais informações sobre o serviço. Para obter as etapas sobre como trabalhar com rótulos de uso em [!DNL Platform], consulte os seguintes guias:

* [Gerenciar rótulos na interface do usuário](../../data-governance/labels/user-guide.md)
* [Gerenciar rótulos na API](../../data-governance/labels/api.md)

## Conjuntos de dados em serviços de plataforma downstream

Depois que os conjuntos de dados tiverem sido usados para armazenar dados ingeridos, esses conjuntos de dados serão usados pelos serviços de plataforma downstream para atualizar os perfis do cliente, obter insights por meio do aprendizado da máquina e muito mais.

A seguir está uma lista de serviços downstream que usam conjuntos de dados para várias operações. Consulte a documentação de cada serviço para obter mais informações.

* [API](../../data-access/home.md)de acesso a dados: Permite acessar e baixar o conteúdo de arquivos armazenados em conjuntos de dados.
* [Serviço](../../identity-service/home.md)de identidade da plataforma Adobe Experience: Corresponde identidades entre dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos schemas XDM aos quais eles estão em conformidade.
* [Perfil](../../profile/home.md)do cliente em tempo real: Aproveita o Serviço de identidade para criar perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. O Cliente em tempo real extrai dados do Data Lake e persiste em perfis do cliente em seu próprio armazenamento de dados separado.
* [Serviço](../../segmentation/home.md)de segmentação da plataforma Adobe Experience: Permite que você crie segmentos e gere audiências a partir dos dados do Perfil do cliente em tempo real. Essas audiências podem ser exportadas para seus próprios conjuntos de dados no Data Lake.
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Usa aprendizado de máquina e inteligência artificial para descobrir insights em grandes conjuntos de dados.
* [Serviço](../../query-service/home.md)de Query da plataforma Adobe Experience: Permite usar SQL padrão para dados de query na plataforma Experience, unindo quaisquer conjuntos de dados no Data Lake e capturando os resultados do query como um novo conjunto de dados para uso no relatórios, na Data Science Workspace ou no Perfil do cliente em tempo real.
* [Serviço](../../decisioning-service/home.md)de decisão da plataforma Adobe Experience: Aproveita o Perfil do cliente em tempo real para determinar a escolha mais provável que um cliente fará a partir de um conjunto de opções, com base nos dados comportamentais que o Perfil extrai dos conjuntos de dados ativados.

## Próximas etapas

Ao ler esse documento, você foi apresentado aos principais usos dos conjuntos de dados na plataforma da experiência, bem como aos vários serviços da plataforma que utilizam conjuntos de dados. Para obter mais detalhes sobre as várias maneiras como os conjuntos de dados são usados na Plataforma, consulte a documentação de serviço vinculada em toda esta visão geral.

Para obter etapas sobre como interagir com conjuntos de dados na interface do usuário da plataforma de experiência, consulte o guia [do usuário dos](user-guide.md)conjuntos de dados.