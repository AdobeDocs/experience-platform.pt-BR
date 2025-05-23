---
title: Notas de versão de abril de 2021 da Adobe Experience Platform
description: As notas de versão de abril de 2021 da Adobe Experience Platform.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '890'
ht-degree: 33%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 21 de abril de 2021**

Atualizações dos recursos já existentes na Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

O [!DNL Data Prep] permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para edição de mapeamento para fluxos de dados existentes | Agora é possível atualizar os conjuntos de mapeamento de um fluxo de dados existente. Não é possível atualizar conjuntos de mapeamento para fluxos de dados que foram agendados para uma assimilação única. Este recurso não tem suporte para API HTTP, Adobe Analytics, Adobe Audience Manager e [!DNL Marketo Engage]. Para obter mais informações, consulte o tutorial sobre [atualização de fluxos de dados de fontes na interface](../../sources/tutorials/ui/update-dataflows.md). |
| Suporte para assimilação por transmissão | Agora é possível usar as funções de preparação de dados ao criar uma conexão de origem de streaming. Para obter mais informações, consulte o tutorial sobre [criação de uma conexão de origem de streaming na interface](../../sources/tutorials/ui/create/streaming/http.md). |

Para obter mais informações, consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

O Experience Data Model (XDM) é uma especificação de código aberto projetada para melhorar o poder das experiências digitais. Ele fornece estruturas e definições comuns para que qualquer aplicativo se comunique com os serviços na Adobe Experience Platform. Ao aderir aos padrões do XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

| Recurso | Descrição |
| --- | --- |
| Recomendações de esquema por setor | Ao selecionar classes e grupos de campos de esquema na interface do Editor de esquemas, você pode usar um novo filtro para exibir componentes padrão recomendados com base em seu setor específico. Consulte a documentação sobre [modelos de dados do setor](https://www.adobe.com/go/xdm-industry-erds-en) para obter mais informações sobre como esses componentes se relacionam entre si em casos de uso diferentes do setor. |

## [!DNL Intelligent Services] {#intelligent-services}

Os Serviços inteligentes capacitam analistas e profissionais de marketing a aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing definam previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de uma especialização em ciência de dados.

### IA do cliente

A IA do cliente, disponível no Real-Time Customer Data Platform, é usada para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado de máquina, escolher um algoritmo, treinar ou implantar.

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para dados do Adobe Analytics | Atualização da funcionalidade para oferecer suporte a conjuntos de dados do Adobe Analytics por meio do conector de origem do Analytics sem a necessidade de ETL para seus dados em conformidade com o esquema Consumer Experience Event (CEE). |
| Suporte para dados do Adobe Audience Manager | Atualização da funcionalidade para oferecer suporte a conjuntos de dados do Adobe Audience Manager por meio do conector de origem do Audience Manager sem a necessidade de ETL para que seus dados estejam em conformidade com o esquema Consumer Experience Event (CEE). |
| Resumo de desempenho do modelo | A IA do cliente agora tem uma [guia de resumo de desempenho do modelo](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) na página de insights da instância do serviço. A guia de desempenho do modelo mostra todas as taxas de conversão e churn reais. Isso permite que você decifre e entenda o que está acontecendo em cada um de seus compartimentos de propensão. |

Para obter mais informações sobre conjuntos de dados compatíveis, consulte a [[!DNL Intelligent Services] documentação de preparação de dados](../../intelligent-services/data-preparation.md).

### IA de atribuição

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ela pode ser usada por comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para dados do Adobe Analytics | Atualização da funcionalidade para oferecer suporte a conjuntos de dados do Adobe Analytics por meio do conector de origem do Analytics sem a necessidade de ETL para seus dados em conformidade com o esquema Consumer Experience Event (CEE). |

Para obter mais informações sobre conjuntos de dados compatíveis, consulte a [[!DNL Intelligent Services] documentação de preparação de dados](../../intelligent-services/data-preparation.md).

## Serviço de segmentação {#segmentation}

O Serviço de Segmentação da Adobe Experience Platform fornece uma interface de usuário e uma API RESTful que permite criar segmentos e gerar públicos a partir dos dados do [!DNL Real-Time Customer Profile]. Esses segmentos são configurados e mantidos centralmente no Experience Platform, tornando-os prontamente acessíveis por qualquer aplicativo do Adobe.

O [!DNL Segmentation Service] define um subconjunto específico de perfis descrevendo os critérios que distinguem um grupo de pessoas na sua base de clientes que pode ser direcionado por campanhas de marketing. Os segmentos podem ser baseados em dados de registro (como informações demográficas) ou em eventos de séries temporais que representam interações de clientes com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Funções de agregação adicionais | As funções de contagem foram adicionadas no Construtor de segmentos. As funções de contagem permitem contar o número de vezes que o evento especificado foi realizado. Mais informações sobre as funções de contagem podem ser encontradas na seção funções de contagem do [guia do Construtor de segmentos](../../segmentation/ui/segment-builder.md#count-functions) |

Para obter mais informações sobre o [!DNL Segmentation Service], consulte a [Visão geral de segmentação](../../segmentation/home.md).

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da Experience Platform. É possível assimilar dados de várias origens, como aplicativos da Adobe, do armazenamento na nuvem, um software de terceiros e do seu sistema de CRM.

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Agora você pode criar uma conexão de origem [!DNL Marketo Engage] usando a interface do usuário para trazer dados B2B para a Experience Platform e manter esses dados atualizados usando aplicativos conectados à Experience Platform. Para obter mais informações, consulte a [[!DNL Marketo Engage] documentação do conector de origem](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Origens do Beta migrando para o GA | As seguintes fontes foram promovidas de beta para GA: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
