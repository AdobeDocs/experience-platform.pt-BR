---
keywords: Experience Platform, controle de dados, atendimento ao cliente, tópicos populares
solution: Experience Platform
feature: Customer AI
title: Governança de dados no Customer AI
description: A Adobe Experience Platform fornece vários serviços e ferramentas que permitem controlar com segurança seus dados de experiência coletados para cumprir suas práticas comerciais, obrigações legais e processo de desenvolvimento.
exl-id: de0836a4-7bc2-4f9c-95a9-c01dd9e2b03f
source-git-commit: f0bd35d8fb592900c61ed4a1a74d05901bc32810
workflow-type: tm+mt
source-wordcount: '295'
ht-degree: 6%

---

# AI e governança de dados do cliente

Todas as configurações relacionadas ao controle de dados no Customer AI são herdadas do Adobe Experience Platform.

## Governança de dados {#governance}

A integração entre a API do cliente e a Governança de dados da Adobe Experience Platform oferece a capacidade de controlar e compreender os dados em toda a jornada por meio da plataforma. Isso envolve a manutenção da qualidade dos dados, da linhagem dos dados, da catalogação de dados e muito mais.

Os rótulos e as políticas de uso de dados criados em conjuntos de dados consumidos pela Platform podem ser encontrados no fluxo de trabalho de configuração do Customer AI. Esses rótulos param ou avisam os usuários que usam campos rotulados.

Essa integração permite gerenciar a conformidade com mais eficiência. Os administradores de dados da sua organização podem definir políticas de restrição de uso. Como resultado, você pode usar dados que estão em conformidade com as políticas definidas pelos Data Stewards. Leia a documentação em [Rótulos e políticas](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-dataviews/data-governance.html?lang=pt-BR) para saber mais.

## Política de consentimento {#consent-policy}

O Customer AI respeita suas preferências de consentimento. Depois de configurar sua política de consentimento e ativá-la conforme documentado aqui, a Customer AI honrará os dados de consentimento coletados de você. Somente dados consentidos são usados para pontuar o modelo em execuções subsequentes do modelo. As novas pontuações substituirão as pontuações antigas e podem ser usadas na segmentação. Este recurso só está disponível para clientes do HealthCare e para clientes do Privacy and Security shield.

Saiba mais sobre esse recurso aqui:

[Introdução ao Customer AI](../../customer-ai/getting-started.md)
[Adobe Experience Platform e aplicativos](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html)
[Diagramas de arquitetura do Adobe Experience Cloud](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/experience-cloud.html)
