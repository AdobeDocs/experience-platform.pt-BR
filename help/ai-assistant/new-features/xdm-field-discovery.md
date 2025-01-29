---
title: Descoberta de campo XDM com o assistente de IA
description: Leia este documento para saber como usar o Assistente de IA para descoberta de campos do modelo de dados de experiência (XDM).
badge: Alfa
hide: true
hidefromtoc: true
exl-id: 041034c6-da45-437f-ad46-f9c2ded9f82c
source-git-commit: 58cf5d90d70239a4b47c600bd3a7a37129b07dc3
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# Descoberta de campo XDM com o Assistente de IA

>[!AVAILABILITY]
>
>Esse recurso está na Alpha e pode não estar disponível para sua organização. Para participar do programa Alpha e acessar esse recurso, entre em contato com a equipe de conta do Adobe.

Você pode usar o Assistente de IA para pesquisar e descobrir campos do Modelo de dados de experiência (XDM) que podem ser usados para criar públicos-alvo direcionados no Experience Platform.

Leia a tabela a seguir para obter os padrões de consulta e prompt compatíveis para a descoberta de campos XDM no Assistente do AI.

>[!TIP]
>
>Embora os padrões de consulta e prompt possam ser os mesmos em diferentes casos de uso, a formulação exata de uma pergunta varia dependendo dos campos e esquemas XDM usados para uma determinada sandbox.

| Tipo de consulta | Padrão de consulta/prompt | Exemplos |
| --- | --- | --- |
| Detecção de campo XDM por domínio ou área de dados | Mostre os campos XDM usados para representar {DATA_DOMAIN/AREA}. | <ul><li>Mostre-me os campos XDM usados para representar dados de consentimento.</li><li>Mostre-me os campos XDM usados para representar informações sobre assinaturas de email.</li></ul> |
| Descoberta de campo XDM por nome de campo geral | <ul><li>Mostre-me os campos XDM relacionados a {DATA_DOMAIN/AREA}.</li><li>Quais campos XDM contêm {GENERAL_FIELD_NAME}.</li></ul> | <ul><li>Mostre-me os campos XDM relacionados aos pedidos.</li><li>Mostre-me os campos XDM relacionados aos detalhes de interação.</li><li>Qual campo XDM contém IDs de visitante?</li><li>Qual campo XDM contém categorias de produto?</li></ul> |
| Detecção de campo XDM por linhagem de modelo de dados | <ul><li>Mostre todos os campos do {FIELD_GROUP/CLASS_NAME} que contêm {GENERAL_FIELD_NAME}.</li><li>O que é o {FIELD_GROUP/CLASS_NAME} do campo XDM {GENERAL_FIELD_NAME}?</li></ul> | <ul><li>Mostre-me todos os campos do grupo de campos que contêm dados do produto.</li><li>Mostre-me todos os campos do grupo de campos que contém dados de análise.</li><li>Qual é a classe do nome do campo XDM?</li><li>Qual é a classe das assinaturas de email de campo XDM?</li></ul> |
| Solicitação para obter descrições aprimoradas, juntamente com nomes de campo | {FIELD_DISCOVERY_QUERY}. Também inclui descrições aprimoradas. | <ul><li>Mostre-me os campos XDM usados para representar dados de consentimento. Também inclua a descrição aprimorada do campo.</li><li>Mostre-me os campos XDM relacionados aos detalhes de interação. Também inclua a descrição aprimorada do campo.</li></ul> |

{style="table-layout:auto"}
