---
title: Notas de versão da Adobe Experience Platform de setembro de 2022
description: As notas de versão de setembro de 2022 para o Adobe Experience Platform.
source-git-commit: 1890bd9dbce6a217951c28fc2fb3fec2634e714d
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 7%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 28 de setembro de 2022**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Identity Service](#identity-service)
- [Fontes](#sources)

## Serviço de identidade {#identity-service}

Fornecer experiências digitais relevantes requer ter uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em diferentes sistemas, fazendo com que cada cliente pareça ter várias &quot;identidades&quot;.

O serviço de identidade da Adobe Experience Platform ajuda você a obter uma melhor visão de seu cliente e de seu comportamento ao unir identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Suporte para exclusão de conjunto de dados | O Serviço de identidade agora oferece suporte à exclusão do conjunto de dados ao solicitar por meio do [API do Serviço de catálogo](https://developer.adobe.com/experience-platform-apis/references/catalog/), da interface do usuário ou da higiene de dados. Leia o guia em [exclusão de conjuntos de dados na interface do usuário](../../catalog/datasets/user-guide.md#delete-a-dataset) para obter mais informações. |

Para saber mais sobre o Serviço de identidade, leia a [Visão geral do Serviço de identidade](../../identity-service/home.md).

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Impacto da população do segmento Audience Manager no Perfil do cliente em tempo real | A assimilação de populações de segmentos de Audience Manager consideráveis afeta diretamente a contagem total de perfis ao enviar um segmento de Audience Manager para a Platform pela primeira vez usando a fonte de Audience Manager. Isso significa que a seleção de todos os segmentos pode levar a uma contagem de Perfis além do seu direito de uso de licença. Para obter mais informações, leia a [Visão geral da fonte de Audience Manager](../../sources/connectors/adobe-applications/audience-manager.md). Para obter informações sobre o uso da licença, leia a documentação em [uso do painel de uso da licença](../../dashboards/guides/license-usage.md). |

Para saber mais sobre fontes, leia a [visão geral das fontes](../../sources/home.md).