---
keywords: Experience Platform;página inicial;tópicos populares;segmentação;Segmentação;Correspondência de segmentos;correspondência de segmentos
solution: Experience Platform
title: Perguntas frequentes sobre correspondência de segmentos
description: A Correspondência de segmentos é um serviço de compartilhamento de segmentos no Adobe Experience Platform que permite que dois ou mais usuários da Platform troquem dados de segmento de maneira segura, controlada e compatível com a privacidade.
exl-id: cfa9db16-0bc3-4d25-914d-0d923eccb5a3
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '414'
ht-degree: 0%

---

# [!DNL Segment Match] perguntas frequentes

Este guia fornece respostas para perguntas legais e de privacidade frequentes sobre a correspondência de segmentos do Adobe Experience Platform.

## Quais dados são compartilhados durante as sobreposições da estimativa e como o Adobe pode garantir que essas métricas sejam obtidas com segurança?

![overlap-report.png](./images/overlap-report.png)

Nenhum dado de cliente ou segmento é movido entre sandboxes para obter essas métricas de estimativa de sobreposição. As identidades aplicáveis pré-hash selecionadas pelo cliente em qualquer sandbox são adicionadas a uma estrutura de dados probabilística em que as próprias IDs são representadas em um formato com hash.

Esse é um processo unidirecional, o que significa que os identificadores originais com pré-hash não são expostos e não podem ter engenharia reversa.

Essas estruturas de dados têm propriedades exclusivas que permitem que a engenharia execute operações de união e interseção entre elas, mesmo que as informações codificadas sejam severamente compactadas ou com hash. Essas operações permitem [!DNL Segment Match] para obter a interseção estimada de duas estruturas de dados compostas por IDs de duas sandboxes diferentes sem precisar comparar os valores reais. Desde [!DNL Segment Match] O usa apenas as estruturas de dados, as IDs nunca deixam os armazenamentos de Perfil da respectiva organização para fins de estimativa. Isso permite que o Adobe atenda aos requisitos de privacidade e segurança dos clientes e, ao mesmo tempo, ofereça ferramentas de estimativa altamente precisas para orientar os contratos de colaboração de dados.

## Qual é o processo por trás da designação de quais identidades recebem as IDs de segmento compartilhado?

[!DNL Segment Match] O fornece aos clientes uma opção para configurar quais namespaces usar no serviço. Essa seleção é aplicada ao processo de estimativa descrito na pergunta anterior e ao processo de transferência de dados, caso o cliente decida publicar o feed em uma sandbox do parceiro.

O processo de transferência de dados entre as identidades criptografadas de duas organizações diferentes é executado em um ambiente de computação neutro. O trabalho de transferência de dados pertence ao Adobe, e as organizações envolvidas na parceria não têm acesso a esse ambiente nem obtêm acesso a nenhum log que possa ser um resultado do trabalho de transferência de dados.

Somente a associação de segmento é assimilada nos fragmentos de perfil sobrepostos de uma organização recebedora e nenhuma identidade adicional é transferida da organização remetente para a organização recebedora. Nenhuma informação de texto simples identificável pessoalmente (PII) é lida pelo trabalho de transferência de dados porque [!DNL Segment Match] O permite sobreposições somente em namespaces criptografados SHA256 (email/telefone) sempre que os dados forem PII. Os resultados nunca são armazenados no ambiente de computação.
