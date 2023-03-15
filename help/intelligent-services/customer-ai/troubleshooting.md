---
keywords: Experience Platform;introdução;ia do cliente;tópicos populares;entrada da ia do cliente;saída da ia do cliente;solução de problemas da ia do cliente;erros da ia do cliente
solution: Experience Platform, Real-time Customer Data Platform
feature: Customer AI
title: Solução de problemas de erro do Customer AI
description: Encontre respostas para erros comuns na IA do cliente.
type: Documentation
exl-id: 37ff4e85-da92-41ca-afd4-b7f3555ebd43
source-git-commit: e4e30fb80be43d811921214094cf94331cbc0d38
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---

# Solução de problemas de erro do Customer AI

A IA do cliente exibe erros quando o treinamento do modelo, a pontuação e a configuração falham. No **[!UICONTROL Instâncias de serviço]** seção, uma coluna para **[!UICONTROL STATUS DA ÚLTIMA EXECUÇÃO]** O exibe uma das seguintes mensagens: **[!UICONTROL Sucesso]**, **[!UICONTROL Problema de treinamento]**, e **[!UICONTROL Failed]**.

![status da última execução](./images/errors/last-run-status.png)

No caso de **[!UICONTROL Failed]** ou **[!UICONTROL Problema de treinamento]** for exibida, você poderá selecionar o status de execução para abrir um painel lateral. O painel lateral contém as **[!UICONTROL Status da última execução]** e **[!UICONTROL Detalhes da última execução]**. **[!UICONTROL Detalhes da última execução]** contém informações sobre por que a execução falhou. Caso a IA do cliente não possa fornecer detalhes sobre o erro, entre em contato com o suporte com o código de erro fornecido.

<img src="./images/errors/last-run-details.png" width="300" /><br />

## Não é possível acessar a IA do cliente no Chrome incógnito

Erros de carregamento no modo incógnito do Google Chrome estão presentes devido a atualizações nas configurações de segurança do modo incógnito do Google Chrome. O problema está sendo ativamente trabalhada com o Chrome para tornar o experience.adobe.com um domínio confiável.

<img src="./images/errors/error.PNG" width="500" /><br />

### Correção recomendada

Para contornar esse problema, é necessário adicionar experience.adobe.com como um site que sempre pode usar cookies. Comece navegando até **chrome://settings/cookies**. Em seguida, role para baixo até o **Comportamentos personalizados** seção seguida pela seleção do **Adicionar** botão ao lado de &quot;sites que sempre podem usar cookies&quot;. No popover exibido, copie e cole `[*.]experience.adobe.com` em seguida, selecione o **Inclusão de cookies de terceiros** nesta caixa de seleção do site. Após a conclusão, selecione **Adicionar** e recarregar a IA do cliente em incógnito.

![correção recomendada](./images/errors/cookies2.gif)

## A qualidade do modelo é ruim

Se você receber o erro &quot;[!UICONTROL A qualidade do modelo é ruim. Recomendamos criar um novo aplicativo com a configuração modificada]&quot;. Siga as etapas recomendadas abaixo para ajudar a solucionar problemas.

<img src="./images/errors/model-quality.png" width="300" /><br />

### Correção recomendada

&quot;A qualidade do modelo é ruim&quot; significa que a precisão do modelo não está dentro de uma faixa aceitável. A IA do cliente não conseguiu criar um modelo confiável e a AUC (Área sob a curva ROC) &lt; 0,65 após o treinamento. Para corrigir o erro, é recomendável alterar um dos parâmetros de configuração e executar novamente o treinamento.

Comece verificando a precisão dos seus dados. É importante que seus dados contenham os campos necessários para o resultado preditivo.

- Verifique se o conjunto de dados tem as datas mais recentes. A IA do cliente sempre presume que os dados estão atualizados quando o modelo é acionado.
- Verifique se há dados ausentes na janela de previsão e qualificação definida. Seus dados precisam ser completos sem lacunas. Além disso, verifique se seu conjunto de dados atende aos [Requisitos de dados históricos da IA do cliente](./input-output.md#data-requirements).
- Verifique se há dados ausentes no comércio, no aplicativo, na web e na pesquisa, nas propriedades do campo de esquema.

Se os dados não parecerem ser o problema, tente alterar a condição de população de qualificação para restringir o modelo a determinados perfis (por exemplo, `_experience.analytics.customDimensions.eVars.eVar142` existe nos últimos 56 dias). Isso restringe o público e o tamanho dos dados usados na janela de treinamento.

Se a restrição da população de qualificação não funcionar ou não for possível, altere a janela de previsão.

- Tente alterar a janela de previsão para 7 dias e veja se o erro continua ocorrendo. Se o erro não ocorrer mais, isso indica que talvez você não tenha dados suficientes para a janela de previsão definida.
