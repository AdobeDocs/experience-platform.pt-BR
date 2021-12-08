---
keywords: Experience Platform, página inicial, tópicos populares, segmentação, Segmentação, Correspondência de segmentos, correspondência de segmentos
solution: Experience Platform
title: Perguntas frequentes sobre a correspondência de segmentos (Beta)
description: Correspondência de segmentos é um serviço de compartilhamento de segmentos no Adobe Experience Platform que permite que dois ou mais usuários da plataforma troquem dados de segmento de maneira segura, regida e amigável à privacidade.
source-git-commit: 81ef2030ff26d2aee146316fcdab41d9311e84c7
workflow-type: tm+mt
source-wordcount: '446'
ht-degree: 0%

---

# [!DNL Segment Match] perguntas frequentes (Beta)

>[!IMPORTANT]
>
>Segment Match is currently in beta and your organization may not have access to it yet. The functionality described in this documentation is subject to change.

This guide provides answers to privacy and legal questions often asked about Adobe Experience Platform Segment Match.

## Quais dados são compartilhados durante as sobreposições de estimativa e como o Adobe pode garantir que essas métricas sejam obtidas com segurança?

![overlap-report.png](./images/overlap-report.png)

Nenhum dado de cliente ou segmento é movido entre sandboxes para obter essas métricas de estimativa de sobreposição. As identidades aplicáveis pré-hash selecionadas pelo cliente em qualquer sandbox são adicionadas a uma estrutura de dados probabilística na qual as próprias IDs são representadas em um formato hash.

This is a one-way process, meaning the original pre-hashed identifiers are not exposed and cannot be reverse-engineered.

These data structures have unique properties that allow engineering to perform union and intersection operations between them, even if the information encoded is severely compressed or hashed. Essas operações permitem [!DNL Segment Match] para obter a interseção estimada de duas estruturas de dados compostas de IDs de duas sandboxes diferentes sem precisar comparar os valores reais. Since [!DNL Segment Match] somente usa as estruturas de dados, as IDs nunca deixam os respectivos armazenamentos de perfil das organizações IMS para fins de estimativa. Isso permite que o Adobe atenda aos requisitos de privacidade e segurança dos clientes e, ao mesmo tempo, ofereça ferramentas de estimativa altamente precisas para orientar os contratos de colaboração de dados.

## What is the process behind designating which identities receive the shared segment IDs?

[!DNL Segment Match] O fornece aos clientes uma opção para configurar quais namespaces usar no serviço. Essa seleção é aplicada ao processo de estimativa descrito na pergunta anterior e ao processo de transferência de dados, caso o cliente decida publicar o feed em uma sandbox de parceiro.

O processo de transferência de dados entre as identidades criptografadas de duas organizações diferentes é executado em um ambiente de computação neutro. O trabalho de transferência de dados é de propriedade da Adobe, e as organizações envolvidas na parceria não têm acesso a esse ambiente, nem têm acesso a quaisquer logs que possam ser um resultado do trabalho de transferência de dados.

Somente a associação de segmento é assimilada em fragmentos de Perfil sobrepostos da Organização IMS de um receptor e nenhuma identidade adicional é transferida da Organização IMS do remetente para a Organização IMS do destinatário. No plain text personally identifiable information (PII) is read by the data transfer job because [!DNL Segment Match] allows overlaps only on SHA256 encrypted namespaces (email/phone) whenever data is PII. Os resultados nunca são armazenados no ambiente de computação.