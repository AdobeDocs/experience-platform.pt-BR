---
keywords: Experience Platform;home;popular tópicos;local de dados;Localização de dados;Gestão de dados;gestão de dados;linhagem;linhagem;tipo de dados;tipos de dados;Tipo de dados;Tipo de dados;;home;popular topics;data location;data location;Data Location;;lineage;data type;data type;data types;Data types;Data type
solution: Experience Platform
title: Visão geral dos conjuntos de dados
topic: datasets
description: Este documento fornece uma visão geral de alto nível dos conjuntos de dados no Experience Platform.
translation-type: tm+mt
source-git-commit: a1103bfbf79f9c87bac5b113c01386a6fb8950e7
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 2%

---


# Visão geral dos conjuntos de dados

Todos os dados ingeridos com êxito no Adobe Experience Platform são mantidos em [!DNL Data Lake] como conjuntos de dados. Um conjunto de dados é um armazenamento e uma construção de gerenciamento para uma coleção de dados, geralmente uma tabela, que contém um schema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados.

Este documento fornece uma visão geral de alto nível dos conjuntos de dados em [!DNL Experience Platform].

## Criação de conjuntos de dados e rastreamento de metadados

[!DNL Catalog Service] é o sistema de registro para localização de dados e linhagem dentro  [!DNL Experience Platform]e é usado para criar e gerenciar conjuntos de dados. [!DNL Catalog] rastreia os metadados de cada conjunto de dados, que inclui uma referência ao schema  [!DNL Experience Data Model] (XDM) ao qual o conjunto de dados está em conformidade (explicado na próxima seção) e o número de registros ingeridos nesse conjunto de dados.

Consulte [Visão geral do serviço de catálogo](../home.md) para obter mais informações.

## Impondo restrições nos dados do conjunto de dados

[!DNL Experience Data Model] (XDM) é a estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente. Todos os dados ingeridos em [!DNL Platform] devem estar em conformidade com um schema XDM predefinido antes que possam ser mantidos em [!DNL Data Lake] como um conjunto de dados.

Todos os conjuntos de dados contêm uma referência ao schema XDM que restringe o formato e a estrutura dos dados que eles podem armazenar. Tentar carregar dados em um conjunto de dados que não esteja em conformidade com o schema XDM do conjunto de dados fará com que a ingestão falhe.

Para obter mais informações sobre o XDM, consulte a [visão geral do sistema XDM](../../xdm/home.md).

## Como inserir dados em conjuntos de dados

A ingestão de dados da Adobe Experience Platform representa os vários métodos pelos quais [!DNL Platform] ingere dados de várias fontes. Independentemente do método de ingestão, todos os dados ingeridos com êxito são convertidos em arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Esses arquivos em lote são adicionados aos conjuntos de dados dedicados e persistem em [!DNL Data Lake].

Consulte [Visão geral da ingestão de dados](../../ingestion/home.md) para obter mais informações.

## Aplicar rótulos de uso a conjuntos de dados

A Adobe Experience Platform [!DNL Data Governance] permite que você gerencie dados do cliente para garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. A estrutura [!DNL Data Governance] permite que você aplique rótulos de uso para categorizar dados de acordo com as políticas de uso que se aplicam a esses dados.

Os rótulos de uso de dados podem ser aplicados a conjuntos de dados inteiros ou a campos de conjuntos de dados individuais. Os rótulos adicionados no nível do conjunto de dados são herdados por todos os campos dentro desse conjunto de dados.

Consulte [Visão geral do Data Governance](../../data-governance/home.md) para obter mais informações sobre o serviço. Para obter etapas sobre como trabalhar com rótulos de uso em [!DNL Platform], consulte os seguintes guias:

* [Gerenciar rótulos na interface do usuário](../../data-governance/labels/user-guide.md)
* [Gerenciar rótulos de conjunto de dados na API](../../data-governance/labels/dataset-api.md)

## Conjuntos de dados em serviços downstream [!DNL Platform]

Depois que os conjuntos de dados tiverem sido usados para armazenar dados ingeridos, esses conjuntos de dados serão usados pelos serviços downstream [!DNL Platform] para atualizar os perfis do cliente, obter insights por meio do aprendizado da máquina e muito mais.

A seguir está uma lista de serviços downstream que usam conjuntos de dados para várias operações. Consulte a documentação de cada serviço para obter mais informações.

* [[!DNL Data Access API]](../../data-access/home.md): Permite acessar e baixar o conteúdo de arquivos armazenados em conjuntos de dados.
* [Serviço](../../identity-service/home.md) de identidade Adobe Experience Platform: Corresponde identidades entre dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos schemas XDM aos quais eles estão em conformidade.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Aproveita  [!DNL Identity Service] para criar perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. [!DNL Real-time Customer Profile] extrai dados do  [!DNL Data Lake] e persiste os perfis do cliente em seu próprio armazenamento de dados separado.
* [Serviço](../../segmentation/home.md) de segmentação do Adobe Experience Platform: Permite que você crie segmentos e gere audiências a partir de seus  [!DNL Real-time Customer Profile] dados. Essas audiências podem ser exportadas para seus próprios conjuntos de dados dentro de [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Usa aprendizado de máquina e inteligência artificial para descobrir insights em grandes conjuntos de dados.
* [Serviço](../../query-service/home.md) de Query Adobe Experience Platform: Permite que você use SQL padrão para query de dados em  [!DNL Experience Platform], unindo quaisquer conjuntos de dados dentro dos resultados do query  [!DNL Data Lake] e capturando como um novo conjunto de dados para uso no relatórios,  [!DNL Data Science Workspace]ou  [!DNL Real-time Customer Profile].

## Próximas etapas

Ao ler esse documento, você foi apresentado aos principais usos dos conjuntos de dados em [!DNL Experience Platform], bem como aos vários serviços [!DNL Platform] que utilizam conjuntos de dados. Para obter mais detalhes sobre as várias maneiras como os conjuntos de dados são usados em [!DNL Platform], consulte a documentação do serviço vinculada em toda esta visão geral.

Para obter etapas sobre como interagir com conjuntos de dados na interface do usuário [!DNL Experience Platform], consulte o [guia do usuário dos conjuntos de dados](user-guide.md).