---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform de 21 de abril de 2021.
doc-type: release notes
last-update: April 21, 2021
author: ens72741
translation-type: tm+mt
source-git-commit: 73ecf6e6f9796088e2d14f9dc3d9667104b22a8e
workflow-type: tm+mt
source-wordcount: '586'
ht-degree: 14%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 21 de abril de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Sources]](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para edição de mapeamento para fluxos de dados existentes | Agora você pode atualizar os conjuntos de mapeamento de um fluxo de dados existente. Não é possível atualizar conjuntos de mapeamento para fluxos de dados que foram agendados para uma ingestão única. Esse recurso não é compatível com a API HTTP, Adobe Analytics, Adobe Audience Manager e [!DNL Marketo Engage]. Para obter mais informações, consulte o tutorial em [atualizar fluxos de dados de fontes na interface do usuário](../../sources/tutorials/ui/update-dataflows.md). |
| Suporte para assimilação de streaming | Agora é possível usar funções de preparação de dados ao criar uma conexão de origem de fluxo. Para obter mais informações, consulte o tutorial em [criar uma conexão de origem de transmissão na interface do usuário](../../sources/tutorials/ui/create/streaming/http.md). |

Para obter mais informações, consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## [!DNL Intelligent Services] {#intelligent-services}

Os Serviços inteligentes capacitam analistas e profissionais de marketing a aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso da experiência do cliente. Isso permite que os analistas de marketing configurem previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de experiência em ciência de dados.

### Customer AI

O Customer AI, disponível na Real-time Customer Data Platform, é usado para gerar pontuações de propensão personalizadas, como churn e conversão para perfis individuais em escala. Isso é feito sem precisar transformar as necessidades de negócios em um problema de aprendizado de máquina, escolher um algoritmo, treinar ou implantar.

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para dados do Adobe Analytics | Atualização da funcionalidade para oferecer suporte aos conjuntos de dados do Adobe Analytics por meio do conector de origem do Analytics, sem a necessidade de ETL aos dados para estar em conformidade com o esquema Evento de experiência do consumidor (CEE). |
| Suporte para dados do Adobe Audience Manager | Atualização da funcionalidade para oferecer suporte aos conjuntos de dados da Adobe Audience Manager por meio do conector de origem do Audience Manager sem a necessidade de ETL aos dados para estar em conformidade com o esquema Evento de experiência do consumidor (CEE). |
| Resumo do desempenho do modelo | O Customer AI agora tem uma [guia de resumo do desempenho do modelo](../../intelligent-services/customer-ai/user-guide/discover-insights.md#performance-metrics) na página de insights da instância de serviço. A guia de desempenho do modelo mostra todas as taxas de conversão e de churn reais. Isso permite decifrar e entender o que está acontecendo em cada um dos compartimentos de propensão. |

Para obter mais informações sobre conjuntos de dados compatíveis, consulte a [[!DNL Intelligent Services] documentação sobre preparação de dados](../../intelligent-services/data-preparation.md).

### Attribution AI

O Attribution AI é usado para atribuir créditos a pontos de contato que levam a eventos de conversão. Ele pode ser usado pelos comerciantes para ajudar a quantificar o impacto de marketing de cada ponto de contato de marketing individual em várias jornadas de clientes.

| Recurso | Descrição |
| ------- | ----------- |
| Suporte para dados do Adobe Analytics | Atualização da funcionalidade para oferecer suporte aos conjuntos de dados do Adobe Analytics por meio do conector de origem do Analytics, sem a necessidade de ETL aos dados para estar em conformidade com o esquema Evento de experiência do consumidor (CEE). |

Para obter mais informações sobre conjuntos de dados compatíveis, consulte a [[!DNL Intelligent Services] documentação sobre preparação de dados](../../intelligent-services/data-preparation.md).

## [!DNL Sources] {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| ------- | ----------- |
| [!DNL Marketo Engage] (Beta) | Agora você pode criar uma conexão de origem [!DNL Marketo Engage] usando a interface do usuário para trazer dados B2B para a plataforma e manter esses dados atualizados usando aplicativos conectados à plataforma. Para obter mais informações, consulte a [[!DNL Marketo Engage] documentação do conector de origem](../../sources/connectors/adobe-applications/marketo/marketo.md). |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
