---
title: Notas de versão da Adobe Experience Platform, abril de 2021
description: As notas de versão de abril de 2021 para o Adobe Experience Platform.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
exl-id: cc78e48a-3578-4c55-ae86-1946d62bddb9
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 9%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 21 de abril de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Experience Data Model (XDM)]](#xdm)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Segmentation Service]](#segmentation)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para edição de mapeamento para fluxos de dados existentes | Agora você pode atualizar os conjuntos de mapeamento de um fluxo de dados existente. Não é possível atualizar conjuntos de mapeamento para fluxos de dados que foram agendados para uma ingestão única. Esse recurso não é compatível com a API HTTP, Adobe Analytics, Adobe Audience Manager e [!DNL Marketo Engage]. Para obter mais informações, consulte o tutorial em [atualização de fluxos de dados de fontes na interface do usuário](../../sources/tutorials/ui/update-dataflows.md). |
| Suporte para assimilação de streaming | Agora é possível usar funções de preparação de dados ao criar uma conexão de origem de fluxo. Para obter mais informações, consulte o tutorial em [criação de uma conexão de origem de transmissão na interface do usuário](../../sources/tutorials/ui/create/streaming/http.md). |

Para obter mais informações, consulte o [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## [!DNL Experience Data Model (XDM)] {#xdm}

O Experience Data Model (XDM) é uma especificação de código aberto criada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo se comunicar com serviços no Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados em uma representação comum para fornecer insights de uma maneira mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

| Recurso | Descrição |
| --- | --- |
| Recomendações de schema por setor | Ao selecionar classes e grupos de campos de esquema na interface do Editor de esquemas, você pode usar um novo filtro para exibir componentes padrão recomendados com base em seu setor específico. Consulte a documentação em [modelos de dados do setor](https://www.adobe.com/go/xdm-industry-erds-en) para obter mais informações sobre como esses componentes se relacionam entre si para diferentes casos de uso do setor. |

## [!DNL Intelligent Services] {#intelligent-services}

Os Serviços inteligentes capacitam analistas e profissionais de marketing a aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso da experiência do cliente. Isso permite que os analistas de marketing configurem previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de experiência em ciência de dados.

### Customer AI

O Customer AI disponível no Real-time Customer Data Platform é usado para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado de máquina, escolher um algoritmo, treinar ou implantar.

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para dados do Adobe Analytics | Atualização da funcionalidade para oferecer suporte aos conjuntos de dados do Adobe Analytics por meio do conector de origem do Analytics, sem a necessidade de ETL aos dados para estar em conformidade com o esquema Evento de experiência do consumidor (CEE). |
| Suporte para dados do Adobe Audience Manager | Atualização da funcionalidade para oferecer suporte aos conjuntos de dados da Adobe Audience Manager por meio do conector de origem do Audience Manager sem a necessidade de ETL aos dados para estar em conformidade com o esquema Evento de experiência do consumidor (CEE). |
| Resumo do desempenho do modelo | O Customer AI agora tem um [guia resumo do desempenho do modelo](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) na página insights da instância de serviço. A guia de desempenho do modelo mostra todas as taxas de conversão e de churn reais. Isso permite decifrar e entender o que está acontecendo em cada um dos compartimentos de propensão. |

Para obter mais informações sobre conjuntos de dados compatíveis, consulte o [[!DNL Intelligent Services] documentação de preparação de dados](../../intelligent-services/data-preparation.md).

### Attribution AI

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ele pode ser usado pelos comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para dados do Adobe Analytics | Atualização da funcionalidade para oferecer suporte aos conjuntos de dados do Adobe Analytics por meio do conector de origem do Analytics, sem a necessidade de ETL aos dados para estar em conformidade com o esquema Evento de experiência do consumidor (CEE). |

Para obter mais informações sobre conjuntos de dados compatíveis, consulte o [[!DNL Intelligent Services] documentação de preparação de dados](../../intelligent-services/data-preparation.md).

## Serviço de segmentação {#segmentation}

O Serviço de segmentação da Adobe Experience Platform fornece uma interface de usuário e uma RESTful API que permite criar segmentos e gerar públicos a partir de sua [!DNL Real-time Customer Profile] dados. Esses segmentos são configurados e mantidos centralmente na Platform, tornando-os acessíveis a qualquer aplicativo do Adobe.

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Funções adicionais de agregação | Funções de contagem foram adicionadas no Construtor de segmentos. As funções de contagem permitem contar o número de vezes que o evento especificado foi concluído. Mais informações sobre as funções de contagem podem ser encontradas na seção funções de contagem do [Guia do Construtor de segmentos](../../segmentation/ui/segment-builder.md#count-functions) |

Para obter mais informações sobre [!DNL Segmentation Service]consulte o [Visão geral da segmentação](../../segmentation/home.md).

## [!DNL Sources] {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Agora você pode criar um [!DNL Marketo Engage] conexão de origem usando a interface do usuário para trazer dados B2B para a plataforma e manter esses dados atualizados usando aplicativos conectados à plataforma. Para obter mais informações, consulte o [[!DNL Marketo Engage] documentação do conector de origem](../../sources/connectors/adobe-applications/marketo/marketo.md). |
| Fontes beta movendo-se para GA | As seguintes fontes foram promovidas de beta para GA: <ul><li>[[!DNL Amazon Kinesis]](../../sources/connectors/cloud-storage/kinesis.md)</li><li>[[!DNL Azure EventHubs]](../../sources/connectors/cloud-storage/eventhub.md)</li><li>[[!DNL HTTP API]](../../sources/connectors/streaming/http.md)</li><li>[[!DNL MariaDB]](../../sources/connectors/databases/mariadb.md)</li><li>[[!DNL Microsoft SQL Server]](../../sources/connectors/databases/sql-server.md)</li><li>[[!DNL Oracle]](../../sources/connectors/databases/oracle.md)</li></ul> |

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
