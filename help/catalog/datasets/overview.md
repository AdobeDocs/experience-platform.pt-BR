---
keywords: Experience Platform;página inicial;tópicos populares;local de dados;Local de dados;Gerenciamento de dados;gerenciamento de dados;Linhagem;linhagem;tipo de dados;tipos de dados;tipos de dados;Tipo de dados
solution: Experience Platform
title: Visão geral dos conjuntos de dados
description: Este documento fornece uma visão geral de alto nível dos conjuntos de dados na Experience Platform.
user-guide-description: Obtenha uma visão geral de alto nível dos conjuntos de dados no Experience Platform com este guia. Saiba como criá-los, aplicar restrições aos dados e assimilar dados nos conjuntos de dados aqui.
exl-id: 51ecefb0-a699-4b1a-80f1-26c6ba92fcbf
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '872'
ht-degree: 6%

---

# Visão geral dos conjuntos de dados

Todos os dados assimilados com êxito na Adobe Experience Platform são mantidos no [!DNL Data Lake] como conjuntos de dados. Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas). Os conjuntos de dados também contêm metadados que descrevem vários aspectos dos dados armazenados.

Este documento fornece uma visão geral de alto nível dos conjuntos de dados no [!DNL Experience Platform].

## Criação de conjuntos de dados e metadados de rastreamento

[!DNL Catalog Service] é o sistema de registro para localização e linhagem de dados em [!DNL Experience Platform], e é usado para criar e gerenciar conjuntos de dados. [!DNL Catalog] rastreia os metadados de cada conjunto de dados, o que inclui uma referência ao esquema [!DNL Experience Data Model] (XDM) com o qual o conjunto de dados está em conformidade (explicado na próxima seção) e o número de registros assimilados nesse conjunto de dados.

Consulte a [Visão geral do Serviço de Catálogo](../home.md) para obter mais informações.

## Imposição de restrições em dados do conjunto de dados

O [!DNL Experience Data Model] (XDM) é a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente. Todos os dados assimilados em [!DNL Experience Platform] devem estar em conformidade com um esquema XDM predefinido antes de serem mantidos em [!DNL Data Lake] como um conjunto de dados.

Todos os conjuntos de dados contêm uma referência ao esquema XDM que restringe o formato e a estrutura dos dados que eles podem armazenar. Tentar carregar dados para um conjunto de dados que não esteja em conformidade com o esquema XDM do conjunto de dados causará falha na assimilação.

Para obter mais informações sobre o XDM, consulte a [Visão geral do sistema XDM](../../xdm/home.md).

## Assimilar dados em conjuntos de dados

A Assimilação de dados do Adobe Experience Platform representa os vários métodos pelos quais o [!DNL Experience Platform] assimila dados de várias fontes. Independentemente do método de assimilação, todos os dados assimilados com êxito são convertidos em arquivos em lote. Lotes são unidades de dados que consistem em um ou mais arquivos que serão assimilados como uma única unidade. Esses arquivos em lote são adicionados a conjuntos de dados dedicados e mantidos no [!DNL Data Lake].

Consulte a [Visão geral da assimilação de dados](../../ingestion/home.md) para obter mais informações.

## Rótulos aplicados a conjuntos de dados de esquemas

O Adobe Experience Platform Data Governance permite gerenciar dados de clientes para garantir conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. A estrutura de governança de dados permite aplicar rótulos de uso para categorizar os dados de acordo com as políticas de uso que se aplicam a esses dados. Os rótulos podem ser aplicados a esquemas individuais, campos nesses esquemas e conjuntos de dados individuais inteiros. Quando os rótulos são aplicados diretamente a um esquema, eles são propagados para todos os conjuntos de dados existentes e futuros baseados nesse esquema.

>[!IMPORTANT]
>
>Os rótulos não podem mais ser aplicados a campos no nível do conjunto de dados. Esse workflow foi substituído em favor da aplicação de rótulos no nível do schema. Quaisquer rótulos aplicados anteriormente no nível do objeto do conjunto de dados ainda serão compatíveis por meio da interface do usuário do Experience Platform até 31 de maio de 2024. Para garantir que seus rótulos sejam consistentes em todos os esquemas, todos os rótulos anteriormente anexados a campos no nível do conjunto de dados devem ser migrados para o nível do esquema por você no ano seguinte. Consulte a seção sobre [migrando rótulos aplicados anteriormente](../../data-governance/e2e.md#migrate-labels) para obter instruções sobre como fazer isso.

Consulte a [Visão geral da Governança de dados](../../data-governance/home.md) para obter mais informações sobre o serviço. Para as etapas sobre como trabalhar com rótulos de uso no [!DNL Experience Platform], consulte os guias a seguir:

* [Gerenciar rótulos na interface](../../data-governance/labels/user-guide.md)
* [Gerenciar rótulos de conjunto de dados na API](../../data-governance/labels/dataset-api.md)

## Conjuntos de dados nos serviços downstream [!DNL Experience Platform]

Depois que os conjuntos de dados forem usados para armazenar dados assimilados, eles serão usados pelos serviços downstream do [!DNL Experience Platform] para atualizar perfis de clientes, obter insights por meio do aprendizado de máquina e muito mais.

Veja a seguir uma lista de serviços downstream que usam conjuntos de dados para várias operações. Consulte a documentação de cada serviço para obter mais informações.

* [[!DNL Data Access API]](../../data-access/home.md): permite que você acesse e baixe o conteúdo dos arquivos armazenados em conjuntos de dados.
* [Adobe Experience Platform Identity Service](../../identity-service/home.md): une identidades em dispositivos e sistemas, vinculando conjuntos de dados com base nos campos de identidade definidos pelos esquemas XDM aos quais estão em conformidade.
* [[!DNL Real-Time Customer Profile]](../../profile/home.md): aproveita o [!DNL Identity Service] para criar perfis detalhados de clientes a partir de seus conjuntos de dados em tempo real. [!DNL Real-Time Customer Profile] extrai dados de [!DNL Data Lake] e mantém perfis de clientes em seu próprio armazenamento de dados separado.
* [Serviço de Segmentação do Adobe Experience Platform](../../segmentation/home.md): permite criar segmentos e gerar públicos a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos podem ser exportados para seus próprios conjuntos de dados no [!DNL Data Lake].
* [Adobe Experience Platform Data Science Workspace](../../data-science-workspace/home.md): usa aprendizado de máquina e inteligência artificial para descobrir insights em grandes conjuntos de dados.
* [Serviço de consulta Adobe Experience Platform](../../query-service/home.md): permite usar SQL padrão para consultar dados em [!DNL Experience Platform], ingressar em qualquer conjunto de dados dentro de [!DNL Data Lake] e capturar os resultados da consulta como um novo conjunto de dados para usar nos relatórios, [!DNL Data Science Workspace] ou [!DNL Real-Time Customer Profile].
* [Serviço Adobe Experience Platform Destinations](../../destinations/home.md): permite [exportar conjuntos de dados](/help/destinations/ui/export-datasets.md) para os destinos desejados de marketing por email ou armazenamento na nuvem, para atividades de relatório ou ciência de dados.

## Próximas etapas

Ao ler este documento, você foi apresentado aos usos principais dos conjuntos de dados no [!DNL Experience Platform], bem como aos vários serviços do [!DNL Experience Platform] que utilizam conjuntos de dados. Para obter mais detalhes sobre as várias formas de uso dos conjuntos de dados no [!DNL Experience Platform], consulte a documentação do serviço vinculada a esta visão geral.

Para obter etapas sobre como interagir com conjuntos de dados na interface do [!DNL Experience Platform], consulte o [guia do usuário de conjuntos de dados](user-guide.md).
