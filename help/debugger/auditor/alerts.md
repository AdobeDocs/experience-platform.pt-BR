---
title: Referência de teste de alerta
description: Saiba como o recurso auditor testa alertas no Adobe Experience Platform Debugger.
exl-id: ac6f8675-6c34-48b4-b5dd-48e92af217fd
source-git-commit: 10a5605c40143b58f6ba0108cc087956aa929866
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 37%

---

# Referência do teste de alerta

Esta referência fornece mais informações sobre como o recurso auditor no Adobe Experience Platform Debugger executa testes de alerta.

>[!NOTE]
>
>Para obter mais informações sobre testes do auditor no Platform Debugger, consulte o [visão geral dos recursos do auditor](./overview.md).

Os alertas mostram problemas que você deve estar ciente, mas que não afetam sua pontuação. Essas são recomendações de práticas recomendadas que, em alguns casos, podem não se aplicar à sua implementação.

| Teste | Peso | Critérios | Recomendação |
| --- | --- | --- | --- |
| Advertising Cloud - Tag de conversão correta implementada | 0 | Verifique se a tag de conversão correta é usada.<br><br>**Aviso**: O uso das tags de conversão TubeMogul obsoletas pode resultar em perda de dados. | Atualize seus pixels de conversão para as novas tags de conversão somente de imagem da Advertising Cloud. Isso pode ser feito com mais facilidade com a variável [Extensão de tag do Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Tag JS correta usada | 0 | A Advertising Cloud deve usar as tags mais recentes do JavaScript. | Atualize seu JavaScript da Advertising Cloud para a versão mais recente. Usar as versões obsoletas do JavaScript pode resultar em perda de funcionalidade. Isso pode ser feito mais facilmente usando o [Extensão de tag do Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - tag somente imagem | 0 | O formato de pixel de imagem da Advertising Cloud deve corresponder a um dos seguintes formatos recomendados: <ul><li>`http(s)://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul> | Atualize seus pixels da Advertising Cloud para as novas tags somente de imagem da Advertising Cloud, que garantem que você esteja aproveitando toda a funcionalidade da Advertising Cloud. Isso pode ser feito com mais facilidade com a variável [Extensão de tag do Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Advertising Cloud - Sincronização DSP de pixels de segmento ativada | 0 | Verifique se o pixel do segmento TubeMogul contém uma configuração de sincronização DSP e recomende que a configuração seja adicionada ao pixel. A configuração de Sincronização de DSP é determinada pelo uso de um parâmetro da string de consulta. Para resumir: <ul><li>Se a tag estiver sendo acionada para um dos seguintes:<ul><li>`https://rtd.tubemogul.com/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://rtd-tm.everesttech.net/upi/?sid=<HASH_VALUE>`</li><li>`http(s)://pixel.everesttech.net/px2/<NUMERIC_ID>?`</li></ul></li><li>E a tag contém o parâmetro de URL `sid=`</li><li>EM SEGUIDA, verifique se o parâmetro de URL `cs=0` ou `cs=1` existe e, se não for recomendado, `cs=1` ser adicionado a esses pixels para que as taxas de correspondência do público-alvo possam melhorar.</li></ul> | Adicionar o parâmetro de URL `cs=1` aos pixels da Advertising Cloud para que a sincronização de DSP possa ocorrer, o que aumenta as taxas de correspondência do público-alvo. Isso pode ser feito com mais facilidade com a variável [Extensão de tag do Advertising Cloud](../../destinations/catalog/advertising/adobe-advertising-cloud.md). |
| Serviço da Experience Cloud ID - Use apenas uma AdobeOrg | 0 | Em uma implementação ECID normal, uma única AdobeOrg deve ser usada. | Valide se existem várias AdobeOrg IDs para essa implementação. <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/id-service/using/intro/id-request.html) |
| Launch - `pageBottom` inserção de callback | 0 | O `_satellite.pageBottom()` deve estar presente para que as tags funcionem. Adicione o script em linha imediatamente antes do fechamento `</body>` para garantir a funcionalidade adequada do DTM. Observação: É prática recomendada que a tag seja a última tag no `<body>`. Se for encontrado dentro do `<body>` , ela tem uma chance de funcionar, mas como não é a prática recomendada, ela pode funcionar incorretamente ou com resultados inesperados ou indesejados. | Adicione o script em linha imediatamente antes do fechamento `</body>` para garantir a funcionalidade adequada do DTM. <br><br>[Informações adicionais](../../tags/ui/client-side/asynchronous-deployment.md) |
| Launch - Auto-Hospedado | 0 | A biblioteca de tags está sendo hospedada na instância Akamai do Adobe em `assets.adobedtm.com`. A hospedagem própria é a abordagem recomendada para o carregamento de tags, pois oferece maior controle do desempenho do site por meio do controle de cache, reduzindo as dependências de scripts de terceiros e maior controle do processo de publicação. As bibliotecas de tags podem ser hospedadas e gerenciadas por meio de sua própria hospedagem na Web ou CDN. | Alternar para uma hospedagem própria é uma abordagem para carregar tags em uma página. Embora a hospedagem do por meio do Akamai CDN funcione na maioria dos casos, a hospedagem própria melhora o desempenho da página. <br><br>Informações adicionais:<ul><li>[Guia de início rápido de tags](../../tags/ui/client-side/asynchronous-deployment.md)</li><li>[Implantação assíncrona](../../tags/ui/client-side/asynchronous-deployment.md)</li></ul> |
| Launch - deve ser implantado de forma assíncrona | 0 | As tags devem ser implantadas de forma assíncrona para obter o melhor desempenho. | Inclua a `async` no script em linha para garantir a funcionalidade adequada de tags <br><br>[Informações adicionais](../../tags/ui/client-side/asynchronous-deployment.md) |
| Target - Conteúdo em `mboxDefault` | 0 | O conteúdo deve existir em `mboxDefault` ao usar `at.js`. | Verifique se o conteúdo está disponível. <br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/target/using/implement-target/implementing-target.html) |

{style=&quot;table-layout:auto&quot;}
