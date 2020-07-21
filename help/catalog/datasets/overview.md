---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral dos conjuntos de dados
topic: datasets
translation-type: tm+mt
source-git-commit: bfbf2074a9dcadd809de043d62f7d2ddaa7c7b31
workflow-type: tm+mt
source-wordcount: '711'
ht-degree: 2%

---


# Visão geral dos conjuntos de dados

Todos os dados ingeridos com êxito no Adobe Experience Platform são mantidos dentro dos conjuntos de dados [!DNL Data Lake] como. Um conjunto de dados é um armazenamento e uma construção de gerenciamento para uma coleção de dados, geralmente uma tabela, que contém um schema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados.

Este documento fornece uma visão geral de alto nível dos conjuntos de dados em [!DNL Experience Platform].

## Criação de conjuntos de dados e rastreamento de metadados

[!DNL Catalog Service] é o sistema de registro para localização de dados e linhagem dentro [!DNL Experience Platform]e é usado para criar e gerenciar conjuntos de dados. [!DNL Catalog] rastreia os metadados de cada conjunto de dados, que inclui uma referência ao schema [!DNL Experience Data Model] (XDM) ao qual o conjunto de dados está em conformidade (explicado na próxima seção) e o número de registros ingeridos nesse conjunto de dados.

Consulte a visão geral [do serviço de](../home.md) catálogo para obter mais informações.

## Impondo restrições nos dados do conjunto de dados

[!DNL Experience Data Model] (XDM) é a estrutura padronizada pela qual [!DNL Platform] organiza os dados de experiência do cliente. Todos os dados inseridos no [!DNL Platform] devem estar em conformidade com um schema XDM predefinido antes de serem persistentes no conjunto de dados [!DNL Data Lake] .

Todos os conjuntos de dados contêm uma referência ao schema XDM que restringe o formato e a estrutura dos dados que eles podem armazenar. Tentar carregar dados em um conjunto de dados que não esteja em conformidade com o schema XDM do conjunto de dados fará com que a ingestão falhe.

Para obter mais informações sobre o XDM, consulte a visão geral [do Sistema](../../xdm/home.md)XDM.

## Como inserir dados em conjuntos de dados

A ingestão de dados de Adobe Experience Platform representa os vários métodos pelos quais [!DNL Platform] os dados são ingeridos de várias fontes. Independentemente do método de ingestão, todos os dados ingeridos com êxito são convertidos em arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Esses arquivos em lote são então adicionados a conjuntos de dados dedicados e persistem no [!DNL Data Lake].

Consulte a visão geral [da ingestão de](../../ingestion/home.md) dados para obter mais informações.

## Aplicar rótulos de uso a conjuntos de dados

O Adobe Experience Platform [!DNL Data Governance] permite gerenciar dados do cliente para garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Usar a Rotulagem e a Imposição de Uso de Dados (DULE) como sua estrutura principal [!DNL Data Governance] permite aplicar rótulos de uso para classificar dados de acordo com as políticas de uso que se aplicam a esses dados.

Os rótulos de uso de dados podem ser aplicados a conjuntos de dados inteiros ou a campos de conjuntos de dados individuais. Os rótulos adicionados no nível do conjunto de dados são herdados por todos os campos dentro desse conjunto de dados.

Consulte a visão geral [do](../../data-governance/home.md) Data Governance para obter mais informações sobre o serviço. Para obter as etapas sobre como trabalhar com rótulos de uso em [!DNL Platform], consulte os seguintes guias:

* [Gerenciar rótulos na interface do usuário](../../data-governance/labels/user-guide.md)
* [Gerenciar rótulos na API](../../data-governance/labels/api.md)

## Conjuntos de dados em [!DNL Platform] serviços a jusante

Depois que os conjuntos de dados tiverem sido usados para armazenar dados ingeridos, esses conjuntos de dados serão usados pelos [!DNL Platform] serviços de downstream para atualizar os perfis do cliente, obter insights por meio do aprendizado da máquina e muito mais.

A seguir está uma lista de serviços downstream que usam conjuntos de dados para várias operações. Consulte a documentação de cada serviço para obter mais informações.

* [!DNL Data Access API](../../data-access/home.md): Permite acessar e baixar o conteúdo de arquivos armazenados em conjuntos de dados.
* [Serviço](../../identity-service/home.md)de identificação de Adobe Experience Platform: Corresponde identidades entre dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos schemas XDM aos quais eles estão em conformidade.
* [!DNL Real-time Customer Profile](../../profile/home.md): Aproveita [!DNL Identity Service] para criar perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. [!DNL Real-time Customer Profile] extrai dados dos perfis do cliente [!DNL Data Lake] e persiste em seu próprio armazenamento de dados separado.
* [Serviço](../../segmentation/home.md)de segmentação de Adobe Experience Platform: Permite que você crie segmentos e gere audiências a partir de seus [!DNL Real-time Customer Profile] dados. Essas audiências podem ser exportadas para seus próprios conjuntos de dados dentro da [!DNL Data Lake].
* [Espaço de trabalho](../../data-science-workspace/home.md)da ciência de dados do Adobe Experience Platform: Usa aprendizado de máquina e inteligência artificial para descobrir insights em grandes conjuntos de dados.
* [Serviço](../../query-service/home.md)de Query Adobe Experience Platform: Permite que você use SQL padrão para query de dados no, unindo quaisquer conjuntos de dados no [!DNL Experience Platform]e capturando resultados de query como um novo conjunto de dados para uso em relatórios, [!DNL Data Lake] ou [!DNL Data Science Workspace][!DNL Real-time Customer Profile].
* [Serviço](../../decisioning-service/home.md)de decisão de Adobe Experience Platform: Aproveita [!DNL Real-time Customer Profile] para determinar a escolha mais provável que um cliente fará de um conjunto de opções, com base nos dados comportamentais que [!DNL Profile] extraem de conjuntos de dados ativados.

## Próximas etapas

Ao ler esse documento, você foi apresentado aos principais usos dos conjuntos de dados no [!DNL Experience Platform], bem como aos vários [!DNL Platform] serviços que utilizam conjuntos de dados. Para obter mais detalhes sobre as várias maneiras em que os conjuntos de dados são usados, consulte a documentação do serviço vinculada em toda esta visão geral. [!DNL Platform]

Para obter etapas sobre como interagir com conjuntos de dados na [!DNL Experience Platform] interface do usuário, consulte o guia [do usuário dos](user-guide.md)conjuntos de dados.