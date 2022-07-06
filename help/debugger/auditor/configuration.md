---
title: Referência do teste de configuração
description: Saiba como o recurso auditor testa configurações no Adobe Experience Platform Debugger.
exl-id: 92b07224-57f1-4891-9923-aa079945e6bc
source-git-commit: 797d4f305b4a6884ada4e0619beadff6a45ab42d
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 66%

---

# Referência do teste de configuração

Esta referência fornece mais informações sobre como o recurso auditor no Adobe Experience Platform Debugger executa testes de configuração.

>[!NOTE]
>
>Para obter mais informações sobre testes do auditor no Platform Debugger, consulte o [visão geral dos recursos do auditor](./overview.md).

Os testes de configuração verificam configurações, valores ou possíveis conflitos na implementação. O Platform Auditor avalia as tags em relação a outras regras e práticas recomendadas.

| Teste | Peso | Critérios | Recomendação |
| --- | --- | --- | --- |
| Advertising Cloud - Os nomes de conversão usam somente caracteres alfanuméricos | 3 | O `ev_conversion_property_name` deve conter apenas valores numéricos e decimais, EXCETO para a variável `ev_transid` , que pode conter valores de texto ou numéricos. Procure por pixels `everesttech.net`   que contenham um parâmetro de URL que comece com  `ev_`. | Certifique-se de que seus parâmetros de propriedade de transação contenham apenas valores numéricos e decimais.<br><br>Aviso:  Qualquer outro tipo de valor pode causar perda de dados. |
| Advertising Cloud - Os nomes de conversão usam caracteres com segurança de URL | 3 | Os nomes de propriedades de conversão não devem conter um E comercial (&amp;) ou um ponto de interrogação. | Verifique se os parâmetros de propriedade de transação não contêm um E comercial (&amp;) não codificado ou um ponto de interrogação. Elas quebram o formato do URL.<br><br>Aviso: Parâmetros de propriedade que contêm um E comercial (&amp;) não codificado ou um ponto de interrogação (por exemplo:  `ev_formComplete?=1` ou  `ev_formComplete&Submit=1`), pode resultar em perda de dados. |
| Advertising Cloud - ID de transação implementada corretamente | 1 | O nome da propriedade  `ev_transid=` não deve estar em branco. | O nome da propriedade  `ev_transid=` não deve ser deixado sem um valor. Se isso for deixado sem um valor, pode haver perda de dados de transação. Atribuir um valor a `ev_transid=` ou remover o parâmetro do pixel. |
| Analytics - Instanciado no DOM | 5 | O código do Adobe Analytics não está instalado ou não está sendo executado. Retorna 0 quando nenhum código do Analytics é encontrado na página da Web. | Verifique se a tag do Analytics está implementada na página e se não está bloqueada por atividades de script subsequentes.<br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/analytics/implementation/home.html?lang=pt-BR) |
| Analytics - Instanciado uma vez | 5 | O código do Adobe Analytics foi detectado mais de uma vez na página. . Retorna 0 quando nenhum código do A-Analytics é encontrado na página da Web. | Verifique se há apenas uma tag do Analytics na página.<br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/analytics/implementation/home.html) |
| Analytics - Versão mais recente | 3 | Suas páginas não estão executando a versão mais recente da biblioteca de códigos do Analytics. As bibliotecas de código que alimentam as tecnologias da Experience Cloud estão sendo constantemente atualizadas e aprimoradas para aproveitar as melhorias de desempenho e fornecer os recursos mais recentes. Retorna 0 quando nenhum código do Analytics é encontrado na página da Web. | Instale a última versão da biblioteca Analytics.<br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=pt-BR) |
| Launch - tags de terceiros são carregadas de forma assíncrona após DOM pronto | 3 | Para obter um equilíbrio entre uma boa experiência do usuário e a coleta de dados precisos, as tags de terceiros devem ser acionadas no DOM pronto. Isso garantirá que esses scripts de rastreamento sejam executados sem afetar a funcionalidade do site. | Resolva esse problema ajustando todas as regras que executam pixels de terceiros para serem acionados no DOM Ready.<br><br>[Informações adicionais](../../tags/ui/managing-resources/rules.md) |
| Serviço da Experience Cloud ID - Versão mais recente | 2 | Suas páginas não estão executando a versão mais recente da biblioteca de códigos do Serviço de ID de visitante,  visitorAPI.js. As bibliotecas de código que alimentam as tecnologias da Experience Cloud estão sendo constantemente atualizadas e aprimoradas para aproveitar as melhorias de desempenho e fornecer os recursos mais recentes. | Instale a versão mais recente da biblioteca do serviço de ID de visitante.<br><br>[Informações adicionais](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/library.html) |
| Launch - Versão mais recente | 2 | Essas páginas não estão executando a versão mais recente da biblioteca de códigos de tags (Turbine). As bibliotecas de código que alimentam as tecnologias da Experience Cloud estão sendo constantemente atualizadas e aprimoradas para aproveitar as melhorias de desempenho e fornecer os recursos mais recentes. | Recrie e publique a biblioteca de tags.<br><br>[Informações adicionais](../../tags/quick-start/quick-start.md) |
| Target - Versão mais recente | 2 | Suas páginas não estão executando a versão mais recente da biblioteca de códigos do Target. As bibliotecas de código que alimentam as tecnologias da Experience Cloud estão sendo constantemente atualizadas e aprimoradas para aproveitar as melhorias de desempenho e fornecer os recursos mais recentes. | Instale a última versão da biblioteca Target.<br><br>[Informações adicionais](https://developer.adobe.com/target/implement/client-side/) |
| Target - mboxDefault precede mboxCreate | 5 | O uso correto de  mboxCreate é semelhante a:<br><br> `<div class="mboxDefault"><!-Customer content--></div><script>mboxCreate('myMboxName')</script>` | Certifique-se de incluir uma  `<div class="mboxDefault"></div>` antes de chamar mboxCreate(). O at.js não adicionará um para você.<br><br>[Informações adicionais](https://developer.adobe.com/target/implement/client-side/) |
| Target - DOCTYPE válido | 5 | Um DOCTYPE inválido foi detectado. Nenhuma mbox será acionada neste cenário.  Para at.js, DOCTYPE deve estar no modo Padrões ou o Target não funcionará. | Atualize o DOCTYPE na página.<br><br>[Informações adicionais](https://developer.adobe.com/target/implement/client-side/atjs/target-atjs-faq/) |

{style=&quot;table-layout:auto&quot;}
