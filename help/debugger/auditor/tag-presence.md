---
title: Referência do teste de presença de tag
description: Saiba como o recurso do auditor testa a presença de tags na Adobe Experience Platform Debugger.
exl-id: 8f01f89e-2a3b-41bc-b971-f3c60d0ae3fa
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 17%

---

# Referência do teste de presença de tag

Esta referência fornece mais informações sobre como o recurso de auditor no Adobe Experience Platform Debugger testa a presença de tags.

>[!NOTE]
>
>Para obter mais informações sobre testes do auditor no Experience Platform Debugger, consulte a [visão geral do recurso do auditor](./overview.md).

Os testes de presença de tags avaliam se determinadas tags existem na página e se estão no lugar certo no código da página.

| Teste | Peso | Critérios | Recomendação |
| --- | --- | --- | --- |
| Advertising Cloud - Presença de código | 5 | A tag da Advertising Cloud não está disponível no DOM. | Implemente a tag da Advertising Cloud usando a [extensão de tag da Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Pixel de segmento implementado | 5 | Atualize seus pixels de segmento da Advertising Cloud para as novas tags somente de imagem da Advertising Cloud. O uso de tags de segmento AMO obsoletas pode resultar em perda de dados. | Implemente o pixel do segmento da Advertising Cloud usando a [extensão de tag da Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Analytics - Carregado no DOM | 5 | A tag do Adobe Analytics não foi detectada. | Instale a versão mais recente do Analytics. <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Launch - Biblioteca carregada | 5 | Um objeto `global _satellite` não foi encontrado no DOM, o que significa que a biblioteca de tags não está instalada ou não está sendo executada. | Verifique se a biblioteca de tags está implementada na página e se não está bloqueada pelas atividades subsequentes de script. |
| Launch - Não tem vários scripts incorporados | 5 | Os sites de produção devem carregar apenas um código incorporado por página. | Verifique se apenas a biblioteca de produção está sendo carregada na página. |
| Inicialização - O retorno de chamada `pageBottom` existe em `<body>` | 5 | O retorno de chamada `_satellite.pageBottom()` necessário não foi encontrado dentro de `<body>` da página. Esse teste falhará se a chamada `pageBottom` não for encontrada na página, ou se estiver na tag `<head>` (ou em algum outro local inesperado). Ele só passará se `pageBottom` for encontrado em algum lugar dentro da tag `<body>`. | Adicione o script em linha imediatamente antes da marca de fechamento `</body>` para garantir a funcionalidade adequada das marcas.<br><br>[Informações adicionais](../../tags/ui/client-side/asynchronous-deployment.md) |
| Inicialização - O retorno de chamada `pageBottom` não deve existir quando implantado de forma assíncrona | 5 | O retorno de chamada `_satellite.pageBottom()` foi encontrado na página, o que não deve ocorrer quando as tags são implantadas de forma assíncrona. | Remova o script `_satellite.pageBottom()` para habilitar a funcionalidade de marcas adequada. <br><br>[Informações adicionais](../../tags/ui/client-side/asynchronous-deployment.md) |
| Serviço da Experience Cloud ID - Presença do código | 5 | O código do Serviço da Experience Cloud ID não foi encontrado. O uso de Experience Cloud IDs (ECIDs) é altamente recomendado para garantir que você obtenha o máximo de valor das soluções da Experience Cloud e seja essencial para o gerenciamento de ID nas soluções da Experience Cloud. | Instale a versão mais recente da ECID.<br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) |
| Serviço da Experience Cloud ID - Presença de cookies | 5 | O cookie `AMCV_` não foi encontrado. É necessário instanciar um objeto de visitante do código `VisitorAPI.js`. | Se esta for uma implementação de tags, verifique se a AdobeOrg ID foi inserida corretamente na ferramenta ECID. <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Serviço da Experience Cloud ID - valor da MID presente | 5 | O valor MID não foi encontrado no cookie `AMCV_`. | Teste novamente para verificar se há latência de API ECID. Se a condição persistir, entre em contato com o Atendimento ao cliente da Adobe. <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html) |
| Target - Presença de código | 5 | O Adobe Target deve ser definido no DOM. | Instale a versão mais recente do Target (at.js). <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |
| Destino - Biblioteca carregada em `<head>` | 4 | A biblioteca do Target deve ser carregada na marca `<head>`. | Verifique se a biblioteca do Target está carregada na tag `<head>`. <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style="table-layout:auto"}
