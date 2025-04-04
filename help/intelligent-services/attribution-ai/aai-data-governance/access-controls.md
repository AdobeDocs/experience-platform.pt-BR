---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Controle de acesso para o Attribution AI
description: Este documento fornece informações sobre o controle de acesso baseado em atributos para a IA de atribuição.
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# Controle de acesso na IA de atribuição

O controle de acesso da IA de atribuição é fornecido por meio do Adobe Experience Platform na [Adobe Admin Console](https://adminconsole.adobe.com/). Essa funcionalidade aproveita perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes.

Para obter mais informações sobre controle de acesso, consulte a [visão geral do controle de acesso](../../../access-control/home.md).

## Controle de acesso baseado em atributos

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível somente em uma versão limitada.

[O controle de acesso baseado em atributos](../../../access-control/abac/overview.md) é um recurso do Adobe Experience Platform que permite aos administradores controlar o acesso a objetos e/ou recursos específicos com base em atributos. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário.

Essa funcionalidade permite rotular campos de esquema do Experience Data Model (XDM) com rótulos que definem escopos organizacionais ou de uso de dados. Em paralelo, os administradores podem usar a interface de administração de usuários e funções para definir políticas de acesso em torno de campos de esquema XDM e gerenciar melhor o acesso fornecido aos usuários ou grupos de usuários (usuários internos, externos ou de terceiros). Além disso, o controle de acesso baseado em atributos permite que os administradores gerenciem o acesso a segmentos específicos.

Por meio do controle de acesso baseado em atributos, os administradores podem controlar o acesso dos usuários a dados pessoais confidenciais (SPD) e a informações de identificação pessoal (PII) em todos os fluxos de trabalho e recursos da Experience Platform. Os administradores podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.

Devido ao controle de acesso baseado em atributos, alguns campos e funcionalidades podem ter acesso restrito e estar indisponíveis para determinados modelos de serviço da IA de atribuição. Os exemplos incluem &quot;Identidade&quot;, &quot;Definição de pontuação&quot; e &quot;Clone&quot;.

Na parte superior da **página de insights** do espaço de trabalho da IA de atribuição, os detalhes exibidos na barra lateral restringiram o acesso.

![O espaço de trabalho da IA de atribuição com os campos de esquema restritos realçados.](../images/user-guide/access-restricted.png)

Se você selecionar conjuntos de dados com esquemas restritos na página **[!UICONTROL Criar fluxo de trabalho de modelo]**, um sinal de aviso será exibido ao lado do nome do conjunto de dados com a mensagem: [!UICONTROL As informações restritas são excluídas].

![O espaço de trabalho da IA de atribuição com os campos de conjunto de dados restritos foi realçado.](../images/user-guide/restricted-info-excluded.png)

Ao visualizar conjuntos de dados com esquema restrito na página **[!UICONTROL Criar fluxo de trabalho de modelo]**, um aviso será exibido para informar que [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na visualização do conjunto de dados.]

![O espaço de trabalho da IA de atribuição com os resultados dos campos de esquema visualizados restritos foi realçado.](../images/user-guide/restricted-dataset-preview.png)

Depois de criar um modelo com informações restritas e prosseguir para a etapa **[!UICONTROL Definir meta]**, um aviso é exibido na parte superior: [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na configuração.]

![O espaço de trabalho da IA de atribuição com os campos restritos dos resultados do modelo foi realçado.](../images/user-guide/information-not-displayed-save-and-exit.png)

## Próximas etapas

Ao ler este guia, você foi apresentado aos princípios mais importantes do controle de acesso no [!DNL Experience Platform]. Agora você pode continuar com o [guia do usuário de controle de acesso](../overview.md) para obter etapas detalhadas sobre como usar o [!DNL Admin Console] para criar perfis de produtos e atribuir permissões para [!DNL Experience Platform].
