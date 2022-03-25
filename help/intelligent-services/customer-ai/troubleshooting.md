---
keywords: Experience Platform, introdução, atendimento ao cliente, tópicos populares, entrada de atendimento ao cliente, saída de atendimento ao cliente, solução de problemas de atendimento ao cliente, erros de atendimento ao cliente
solution: Intelligent Services, Real-time Customer Data Platform
feature: Customer AI
title: Solução de problemas de erro de AI do cliente
topic-legacy: Getting started
description: Encontre respostas para erros comuns no Customer AI.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: 16120a10f8a6e3fd7d2143e9f52a822c59a4c935
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Solução de problemas de erro de AI do cliente

O Customer AI exibe erros quando o treinamento, a pontuação e a configuração do modelo falham. No **[!UICONTROL Instâncias do serviço]** , uma coluna para **[!UICONTROL STATUS DA ÚLTIMA EXECUÇÃO]** exibe uma das seguintes mensagens: **[!UICONTROL Sucesso]**, **[!UICONTROL Problema de treinamento]** e **[!UICONTROL Falha]**.

![status da última execução](./images/errors/last-run-status.png)

No caso de **[!UICONTROL Falha]** ou **[!UICONTROL Problema de treinamento]** for exibido, você poderá selecionar o status de execução para abrir um painel lateral. O painel lateral contém o **[!UICONTROL Status da última execução]** e **[!UICONTROL Detalhes da última execução]**. **[!UICONTROL Detalhes da última execução]** contém informações sobre por que a execução falhou. Caso o Customer AI não possa fornecer detalhes sobre o erro, entre em contato com o suporte com o código de erro fornecido.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Não é possível acessar a AI do cliente no Chrome incógnito

Os erros de carregamento no modo incógnito do Google Chrome estão presentes devido às atualizações nas configurações de segurança do modo incógnito do Google Chrome. O problema está sendo trabalhado ativamente com o Chrome para tornar o experience.adobe.com um domínio confiável.

<img src="./images/errors/error.PNG" width="500" /><br />

### Correção recomendada

Para contornar esse problema, você precisa adicionar experience.adobe.com como um site que sempre pode usar cookies. Comece navegando até **chrome://settings/cookies**. Em seguida, role para baixo até o **Comportamentos personalizados** seção seguida por selecionar a variável **Adicionar** ao lado de &quot;sites que sempre podem usar cookies&quot;. No recipiente que aparece, copie e cole `[*.]experience.adobe.com` em seguida, selecione o **Inclusão de cookies de terceiros** nesta caixa de seleção de site. Depois de concluir, selecione **Adicionar** e recarregue a API do cliente em incógnito.

![correção recomendada](./images/errors/cookies2.gif)

## A qualidade do modelo é ruim

Se receber o erro &quot;[!UICONTROL A Qualidade do Modelo é ruim. Recomendamos criar um novo aplicativo com a configuração modificada]&quot;. Siga as etapas recomendadas abaixo para ajudar a solucionar o problema.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Correção recomendada

&quot;A qualidade do modelo é pobre&quot; significa que a precisão do modelo não se encontra dentro de um intervalo aceitável. O Customer AI não pôde criar um modelo confiável e o AUC (Área sob a curva ROC) &lt; 0,65 após o treinamento. Para corrigir o erro, é recomendável alterar um dos parâmetros de configuração e executar o treinamento novamente.

Comece verificando a precisão dos seus dados. É importante que seus dados contenham os campos necessários para seu resultado preditivo.

- Verifique se o conjunto de dados tem as datas mais recentes. O Customer AI sempre assume que os dados estão atualizados quando o modelo é acionado.
- Verifique se há dados ausentes em sua previsão e janela de qualificação definidas. Seus dados precisam ser completos sem lacunas. Além disso, verifique se o conjunto de dados atende ao [Requisitos de dados históricos do Customer AI](./input-output.md#data-requirements).
- Verifique se há dados ausentes no comércio, aplicativo, web e pesquisa, nas propriedades do campo de esquema.

Se os dados não parecerem ser o problema, tente alterar a condição de população de qualificação para restringir o modelo a determinados perfis (por exemplo, `_experience.analytics.customDimensions.eVars.eVar142` existe nos últimos 56 dias). Isso restringe a população e o tamanho dos dados usados na janela de treinamento.

Se a restrição da população de qualificação não funcionou ou não for possível, altere sua janela de previsão.

- Tente alterar a janela de previsão para 7 dias e veja se o erro continua ocorrendo. Se o erro não ocorrer mais, isso indica que talvez você não tenha dados suficientes para a janela de previsão definida.
