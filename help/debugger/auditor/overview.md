---
title: Guia Auditor
description: Saiba como usar a guia Auditor no Adobe Experience Platform Debugger para testar as implementações do Adobe Experience Cloud.
keywords: depurador;extensão do experience platform debugger;chrome;extensão;auditor;dtm;target
exl-id: 409094f8-a7d9-45f7-ba12-b5e6250abc0f
source-git-commit: df1a67e4b6f3d2eaeaba2b8d3c9b1588ee0b1461
workflow-type: tm+mt
source-wordcount: '368'
ht-degree: 32%

---

# Guia Auditor

No Adobe Experience Platform Debugger, você pode usar a guia **[!UICONTROL Auditor]** para executar uma série de testes de auditoria na sua página.

Para usar este recurso:

1. Selecione **[!UICONTROL Auditor]** na navegação à esquerda.
1. Selecione **[!UICONTROL Executar Testes do Auditor]**. Quando os testes estiverem concluídos, seus resultados aparecerão abaixo.

![Captura de tela dos resultados de teste na guia Auditor](../images/auditor-results.png)

A lista de resultados mostra o teste e seus resultados, e fornece sugestões para resolver qualquer problema.

## Interpretação dos resultados dos testes

Cada teste é ponderado e sua pontuação de teste é igual ao peso atribuído. Se você passar em um teste com um peso de 5, você receberá cinco pontos.

| Pontuação | Descrição |
| --- | --- |
| 0 | Alerta sobre problemas que você deve estar ciente, mas não afeta sua pontuação. |
| 1 | Recomenda uma otimização. Nenhum impacto na precisão dos dados. |
| 2 | Se esse teste falhar, você não terá acesso aos recursos e correções mais recentes no Adobe Experience Cloud. |
| 3 | Testes de eficiência e se a implementação segue as práticas recomendadas. |
| 4 | Falha significa que você pode estar coletando dados não confiáveis. |
| 5 | Falha significa que você pode ver perda de dados. |

Todos os testes foram bem-sucedidos ou não. Eles testam a conformidade ou não conformidade com as condições de teste, de modo que não há pontuações parciais para a conformidade parcial. Por exemplo, se o teste verificar a versão mais recente de uma solução da Adobe e você estiver somente atrasado em uma versão, você obterá a mesma pontuação se estiver com cinco versões de volta. As versões mais recentes incluem melhorias de desempenho e correções de erros, portanto, é recomendável que esteja na versão mais recente.

É **altamente recomendável** que você corrija quaisquer resultados de nível 4 ou 5.

É **recomendável** que você corrija quaisquer resultados de nível 1 a 3.

## Tecnologias de Adobe suportadas

O recurso de auditor é capaz de classificar as seguintes tecnologias de Adobe:

* Adobe Advertising Cloud DSP
* Adobe Advertising Cloud Search
* Adobe Analytics
* Serviço de identidade da Adobe Experience Cloud
* Adobe Target
* Tags (antigo Adobe Experience Platform Launch)

## Testar rubrica

Para obter mais informações sobre as estruturas de teste fornecidas por esse recurso, consulte os seguintes documentos:

* [Consistência de tags](./tag-consistency.md)
* [Presença de tag](./tag-presence.md)
* [Configuração](./configuration.md)
* [Alertas](./alerts.md)
