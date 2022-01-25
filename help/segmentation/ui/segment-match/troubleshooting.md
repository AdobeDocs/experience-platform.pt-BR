---
keywords: Experience Platform, página inicial, tópicos populares, segmentação, Segmentação, Correspondência de segmentos, correspondência de segmentos
solution: Experience Platform
title: Perguntas frequentes sobre a correspondência de segmentos (Beta)
description: Correspondência de segmentos é um serviço de compartilhamento de segmentos no Adobe Experience Platform que permite que dois ou mais usuários da plataforma troquem dados de segmento de maneira segura, regida e amigável à privacidade.
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: 50795be308649052037be62153109eadab02c9a1
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---

# [!DNL Segment Match] perguntas frequentes (Beta)

Este guia fornece respostas à privacidade e a perguntas legais frequentemente feitas sobre a Correspondência de segmentos do Adobe Experience Platform.

## Quais dados são compartilhados durante as sobreposições de estimativa e como o Adobe pode garantir que essas métricas sejam obtidas com segurança?

![overlap-report.png](./images/overlap-report.png)

Nenhum dado de cliente ou segmento é movido entre sandboxes para obter essas métricas de estimativa de sobreposição. As identidades aplicáveis pré-hash selecionadas pelo cliente em qualquer sandbox são adicionadas a uma estrutura de dados probabilística na qual as próprias IDs são representadas em um formato hash.

Esse é um processo unidirecional, o que significa que os identificadores pré-hash originais não são expostos e não podem ser modificados inversamente.

Essas estruturas de dados têm propriedades exclusivas que permitem que a engenharia execute operações de união e interseção entre elas, mesmo que as informações codificadas sejam severamente compactadas ou transformadas em hash. Essas operações permitem [!DNL Segment Match] para obter a interseção estimada de duas estruturas de dados compostas de IDs de duas sandboxes diferentes sem precisar comparar os valores reais. Since [!DNL Segment Match] somente usa as estruturas de dados, as IDs nunca deixam os respectivos armazenamentos de perfil das organizações IMS para fins de estimativa. Isso permite que o Adobe atenda aos requisitos de privacidade e segurança dos clientes e, ao mesmo tempo, ofereça ferramentas de estimativa altamente precisas para orientar os contratos de colaboração de dados.

## Qual é o processo por trás da designação de quais identidades recebem as IDs de segmento compartilhado?

[!DNL Segment Match] O fornece aos clientes uma opção para configurar quais namespaces usar no serviço. Essa seleção é aplicada ao processo de estimativa descrito na pergunta anterior e ao processo de transferência de dados, caso o cliente decida publicar o feed em uma sandbox de parceiro.

O processo de transferência de dados entre as identidades criptografadas de duas organizações diferentes é executado em um ambiente de computação neutro. O trabalho de transferência de dados é de propriedade da Adobe, e as organizações envolvidas na parceria não têm acesso a esse ambiente, nem têm acesso a quaisquer logs que possam ser um resultado do trabalho de transferência de dados.

Somente a associação de segmento é assimilada em fragmentos de Perfil sobrepostos da Organização IMS de um receptor e nenhuma identidade adicional é transferida da Organização IMS do remetente para a Organização IMS do destinatário. Nenhuma informação de identificação pessoal (PII) de texto simples é lida pelo trabalho de transferência de dados porque [!DNL Segment Match] O permite sobreposições somente em namespaces criptografados SHA256 (email/telefone) sempre que os dados forem PII. Os resultados nunca são armazenados no ambiente de computação.
