---
title: Notas de versão da Adobe Experience Platform de agosto de 2022
description: As notas de versão de agosto de 2022 para o Adobe Experience Platform.
source-git-commit: 2a507b4fe5b7c9dc523ceb5b2f39becf9e574ed9
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 10%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 24 de agosto de 2022**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Preparação de dados](#data-prep)
- [Fontes](#sources)

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para assimilar registros com avisos | A Preparação de dados agora localiza avisos (erros não críticos) nos campos e permitirá que o restante da linha seja assimilado. Todos os erros de transformação do mapeador agora são relatados como avisos e linhas que são parcialmente assimiladas são consideradas bem-sucedidas, com um aviso.  Também há suporte para monitoramento em registros com avisos e detalhes de diagnóstico. A assimilação parcial de registros com avisos está atualmente disponível apenas para dados de transmissão. Revise a documentação em [assimilação de registros com avisos](../../sources/tutorials/ui/monitor-streaming.md) para obter mais informações. |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre [!DNL Data Prep], consulte o [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
| --- | --- |
| Suporte entre regiões para origem do Adobe Analytics | Agora é possível assimilar conjuntos de relatórios de qualquer região (Estados Unidos, Reino Unido ou Cingapura). Os conjuntos de relatórios devem ser mapeados para a mesma organização da instância Sandbox do Experience Platform na qual a conexão de origem está sendo criada. Para obter mais informações, consulte o guia sobre [criação de uma conexão de origem do Adobe Analytics na interface do usuário](../../sources/tutorials/ui/create/adobe-applications/analytics.md). |

{style=&quot;table-layout:auto&quot;}

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
