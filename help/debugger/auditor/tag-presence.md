---
title: Referência do teste de presença de tag
description: Saiba como o recurso auditor testa a presença de tags no Adobe Experience Platform Debugger.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 34%

---

# Referência do teste de presença de tag

Esta referência fornece mais informações sobre como o recurso de auditor no Adobe Experience Platform Debugger testa a presença de tags.

>[!NOTE]
>
>Para obter mais informações sobre testes do auditor no Platform Debugger, consulte o [visão geral dos recursos do auditor](./overview.md).

Os testes de presença de tag avaliam se determinadas tags existem na página e se elas estão no lugar certo no código da página.

| Teste | Peso | Critérios | Recomendação |
| --- | --- | --- | --- |
| Advertising Cloud - Presença de código | 5 | A tag da Advertising Cloud não está disponível no DOM. | Implemente a tag do Advertising Cloud usando o [Extensão de tag do Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Pixel de segmento implementado | 5 | Atualize seus pixels de segmento da Advertising Cloud para as novas tags somente de imagem da Advertising Cloud. O uso de tags de segmento AMO obsoletas pode resultar em perda de dados. | Implemente o pixel do segmento do Advertising Cloud usando o [Extensão de tag do Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - Carregado no DOM | 5 | A tag do Adobe Analytics não foi detectada. | Instale a versão mais recente do Analytics. <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) |
| Launch - Biblioteca carregada | 5 | A `global _satellite` O objeto não foi encontrado no DOM, o que significa que a biblioteca de tags não está instalada ou não está sendo executada. | Verifique se a biblioteca de tags está implementada na página e se não está bloqueada por atividades de script subsequentes. |
| Launch - Não tem vários scripts incorporados | 5 | Os sites de produção devem carregar apenas um código incorporado por página. | Verifique se apenas a biblioteca de produção está sendo carregada na página. |
| Launch - `pageBottom` o retorno de chamada existe em `<body>` | 5 | O `_satellite.pageBottom()` o retorno de chamada não foi encontrado dentro do `<body>` da página. Esse teste falhará se a variável `pageBottom` A chamada do não foi encontrada na página ou se estiver no `<head>` (ou qualquer outro local inesperado). Ele só passará se `pageBottom` é encontrada em algum lugar dentro do `<body>` . | Adicione o script em linha imediatamente antes do fechamento `</body>` para garantir a funcionalidade correta das tags.<br><br>[Informações adicionais](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - `pageBottom` o retorno de chamada não deve existir quando implantado de forma assíncrona | 5 | O `_satellite.pageBottom()` o retorno de chamada foi encontrado na página, o que não deve ocorrer quando as tags são implantadas de forma assíncrona. | Remova o `_satellite.pageBottom()` para ativar a funcionalidade adequada de tags. <br><br>[Informações adicionais](../../tags/ui/client-side/asynchronous-deployment.md) |
| Serviço da Experience Cloud ID - Presença do código | 5 | O código do Serviço da Experience Cloud ID não foi encontrado. O uso de Experience Cloud IDs (ECIDs) é altamente recomendado para garantir que você obtenha o máximo de valor das soluções de Experience Cloud e seja essencial para o gerenciamento de ID nas soluções de Experience Cloud. | Instale a versão mais recente da ECID.<br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) |
| Cookie do serviço da Experience Cloud ID | 5 | O `AMCV_` cookie não encontrado. É necessário instanciar um objeto de visitante do código `VisitorAPI.js` . | Se essa for uma implementação de tags, verifique se a AdobeOrg ID foi inserida corretamente na ferramenta ECID. <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=pt-BR) |
| Serviço da Experience Cloud ID - valor da MID presente | 5 | O valor da MID não foi encontrado no `AMCV_` cookie. | Teste novamente para verificar se há latência de API ECID. Se a condição persistir, entre em contato com o Atendimento ao cliente da Adobe. <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target - Presença de código | 5 | O Adobe Target deve ser definido no DOM. | Instale a versão mais recente do Target (at.js). <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Target - Biblioteca carregada em `<head>` | 4 | A biblioteca do Target deve ser carregada no `<head>` . | Verifique se a biblioteca do Target está carregada no `<head>` . <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style=&quot;table-layout:auto&quot;}
