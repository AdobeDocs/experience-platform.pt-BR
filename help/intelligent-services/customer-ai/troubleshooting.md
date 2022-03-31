---
keywords: Experience Platform, introdução, atendimento ao cliente, tópicos populares, entrada de atendimento ao cliente, saída de atendimento ao cliente, solução de problemas de atendimento ao cliente, erros de atendimento ao cliente
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Customer AI error troubleshooting
topic-legacy: Getting started
description: Encontre respostas para erros comuns no Customer AI.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: eae43834d1cd5931dd752b95023da7ac77668e56
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Solução de problemas de erro de AI do cliente

O Customer AI exibe erros quando o treinamento, a pontuação e a configuração do modelo falham. In the **[!UICONTROL Service instances]** section, a column for **[!UICONTROL LAST RUN STATUS]** displays one of the following messages: **[!UICONTROL Success]**, **[!UICONTROL Training issue]**, and **[!UICONTROL Failed]**.

![last run status](./images/errors/last-run-status.png)

No caso de **[!UICONTROL Falha]** ou **[!UICONTROL Problema de treinamento]** for exibido, você poderá selecionar o status de execução para abrir um painel lateral. The side panel  contains your **[!UICONTROL Last run status]** and **[!UICONTROL Last run details]**. **[!UICONTROL Detalhes da última execução]** contém informações sobre por que a execução falhou. Caso o Customer AI não possa fornecer detalhes sobre o erro, entre em contato com o suporte com o código de erro fornecido.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Unable to access Customer AI in Chrome incognito

Os erros de carregamento no modo incógnito do Google Chrome estão presentes devido às atualizações nas configurações de segurança do modo incógnito do Google Chrome. O problema está sendo trabalhado ativamente com o Chrome para tornar o experience.adobe.com um domínio confiável.

<img src="./images/errors/error.PNG" width="500" /><br />

### Recommended fix

Para contornar esse problema, você precisa adicionar experience.adobe.com como um site que sempre pode usar cookies. Start by navigating to **chrome://settings/cookies**. Next, scroll down to the **Customized behaviors** section followed by selecting the **Add** button next to &quot;sites that can always use cookies&quot;. In the popover that appears, copy and paste `[*.]experience.adobe.com` then select the **Including third-party cookies** on this site checkbox. Once complete, select **Add** and reload Customer AI in incognito.

![recommended fix](./images/errors/cookies2.gif)

## A qualidade do modelo é ruim

Se receber o erro &quot;[!UICONTROL A Qualidade do Modelo é ruim. Recomendamos criar um novo aplicativo com a configuração modificada]&quot;. Follow the recommended steps below to help troubleshoot.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Correção recomendada

&quot;A qualidade do modelo é pobre&quot; significa que a precisão do modelo não se encontra dentro de um intervalo aceitável. Customer AI was unable to build a reliable model and AUC (Area under the ROC curve) &lt; 0.65 after training. Para corrigir o erro, é recomendável alterar um dos parâmetros de configuração e executar o treinamento novamente.

Comece verificando a precisão dos seus dados. It is important that your data contains the necessary fields needed for your predictive outcome.

- Check whether your dataset has the latest dates. Customer AI always assumes that the data is up-to-date when the model is triggered.
- Verifique se há dados ausentes em sua previsão e janela de qualificação definidas. Seus dados precisam ser completos sem lacunas. Além disso, verifique se o conjunto de dados atende ao [Requisitos de dados históricos do Customer AI](./input-output.md#data-requirements).
- Verifique se há dados ausentes no comércio, aplicativo, web e pesquisa, nas propriedades do campo de esquema.

Se os dados não parecerem ser o problema, tente alterar a condição de população de qualificação para restringir o modelo a determinados perfis (por exemplo, `_experience.analytics.customDimensions.eVars.eVar142` existe nos últimos 56 dias). Isso restringe a população e o tamanho dos dados usados na janela de treinamento.

If restricting the eligibility population did not work or is not possible, change your prediction window.

- Try changing your prediction window to 7 days and see if the error continues to occur. Se o erro não ocorrer mais, isso indica que talvez você não tenha dados suficientes para a janela de previsão definida.
