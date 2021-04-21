---
keywords: Experience Platform, página inicial, tópicos populares, local dos dados, Localização dos dados, Gerenciamento de dados, Gerenciamento de dados, Linhagem, linhagem, tipo de dados, tipos de dados, Tipos de dados, Tipo de dados
solution: Experience Platform
title: Visão geral dos conjuntos de dados
topic-legacy: datasets
description: Este documento fornece uma visão geral de alto nível dos conjuntos de dados no Experience Platform.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '707'
ht-degree: 2%

---

# Visão geral dos conjuntos de dados

Todos os dados assimilados com êxito no Adobe Experience Platform são mantidos no [!DNL Data Lake] como conjuntos de dados. Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados.

Este documento fornece uma visão geral de alto nível dos conjuntos de dados em [!DNL Experience Platform].

## Criar conjuntos de dados e rastrear metadados

[!DNL Catalog Service] é o sistema de registro para localização e linhagem de dados no  [!DNL Experience Platform], e é usado para criar e gerenciar conjuntos de dados. [!DNL Catalog] rastreia os metadados de cada conjunto de dados, o que inclui uma referência ao esquema  [!DNL Experience Data Model] (XDM) ao qual o conjunto de dados está em conformidade (explicado na próxima seção) e o número de registros assimilados nesse conjunto de dados.

Consulte a [Visão geral do serviço de catálogo](../home.md) para obter mais informações.

## Como impor restrições aos dados do conjunto de dados

[!DNL Experience Data Model] (XDM) é a estrutura padronizada pela qual  [!DNL Platform] organiza os dados de experiência do cliente. Todos os dados assimilados em [!DNL Platform] devem estar em conformidade com um esquema XDM predefinido antes de serem mantidos em [!DNL Data Lake] como um conjunto de dados.

Todos os conjuntos de dados contêm uma referência ao esquema XDM que restringe o formato e a estrutura dos dados que podem armazenar. Tentar fazer upload de dados para um conjunto de dados que não esteja em conformidade com o esquema XDM do conjunto de dados causará falha na assimilação.

Para obter mais informações sobre XDM, consulte a [Visão geral do sistema XDM](../../xdm/home.md).

## Inserção de dados em conjuntos de dados

A Assimilação de dados do Adobe Experience Platform representa os vários métodos pelos quais [!DNL Platform] assimila dados de várias fontes. Independentemente do método de assimilação, todos os dados assimilados com êxito são convertidos em arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Esses arquivos em lote são adicionados aos conjuntos de dados dedicados e mantidos dentro do [!DNL Data Lake].

Consulte a [Visão geral da assimilação de dados](../../ingestion/home.md) para obter mais informações.

## Aplicar rótulos de uso a conjuntos de dados

O Adobe Experience Platform [!DNL Data Governance] permite gerenciar os dados do cliente para garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. A estrutura [!DNL Data Governance] permite aplicar rótulos de uso para categorizar dados de acordo com as políticas de uso que se aplicam a esses dados.

Os rótulos de uso de dados podem ser aplicados a conjuntos de dados inteiros ou a campos individuais do conjunto de dados. Os rótulos adicionados no nível do conjunto de dados são herdados por todos os campos nesse conjunto de dados.

Consulte a [Visão geral da governança de dados](../../data-governance/home.md) para obter mais informações sobre o serviço. Para obter etapas sobre como trabalhar com rótulos de uso em [!DNL Platform], consulte os seguintes guias:

* [Gerenciar rótulos na interface do usuário](../../data-governance/labels/user-guide.md)
* [Gerenciar rótulos do conjunto de dados na API](../../data-governance/labels/dataset-api.md)

## Conjuntos de dados em serviços downstream [!DNL Platform]

Depois que os conjuntos de dados tiverem sido usados para armazenar dados assimilados, esses conjuntos de dados serão usados pelos serviços downstream [!DNL Platform] para atualizar perfis do cliente, obter insights por meio do aprendizado de máquina e muito mais.

Veja a seguir uma lista de serviços downstream que usam conjuntos de dados para várias operações. Consulte a documentação de cada serviço para obter mais informações.

* [[!DNL Data Access API]](../../data-access/home.md): Permite acessar e baixar o conteúdo dos arquivos armazenados em conjuntos de dados.
* [Serviço](../../identity-service/home.md) de identidade da Adobe Experience Platform: Corresponde identidades entre dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos esquemas XDM aos quais eles estão em conformidade.
* [[!DNL Real-time Customer Profile]](../../profile/home.md): Aproveitamento  [!DNL Identity Service] para criar perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. [!DNL Real-time Customer Profile] extrai dados do  [!DNL Data Lake] e mantém os perfis do cliente em seu próprio armazenamento de dados separado.
* [Serviço](../../segmentation/home.md) de segmentação do Adobe Experience Platform: Permite criar segmentos e gerar públicos-alvo a partir de seus  [!DNL Real-time Customer Profile] dados. Esses públicos podem ser exportados para seus próprios conjuntos de dados no [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): Usa aprendizado de máquina e inteligência artificial para descobrir insights em grandes conjuntos de dados.
* [Serviço](../../query-service/home.md) de query do Adobe Experience Platform: Permite usar o SQL padrão para consultar dados no  [!DNL Experience Platform], unindo quaisquer conjuntos de dados no  [!DNL Data Lake] e capturando resultados de query como um novo conjunto de dados para uso em relatórios,  [!DNL Data Science Workspace]ou  [!DNL Real-time Customer Profile].

## Próximas etapas

Ao ler este documento, você foi introduzido nos principais usos dos conjuntos de dados em [!DNL Experience Platform], bem como nos vários serviços [!DNL Platform] que utilizam conjuntos de dados. Para obter mais detalhes sobre as várias maneiras como os conjuntos de dados são usados em [!DNL Platform], consulte a documentação do serviço vinculada em toda esta visão geral.

Para obter etapas sobre como interagir com conjuntos de dados na interface do usuário [!DNL Experience Platform], consulte o [guia do usuário dos conjuntos de dados](user-guide.md).
