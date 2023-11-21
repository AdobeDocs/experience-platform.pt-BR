---
keywords: Experience Platform;página inicial;tópicos populares;controle de acesso;adobe admin console
solution: Experience Platform
feature: Attribution AI
title: Controle de acesso para o Attribution AI
description: Este documento fornece informações sobre o controle de acesso baseado em atributos para o Attribution AI.
exl-id: 3ed672bf-1fa6-4893-99e0-afc2b2179543
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 1%

---

# Controle de acesso no Attribution AI

O controle de acesso do Attribution AI é fornecido por meio do Adobe Experience Platform na [Adobe Admin Console](https://adminconsole.adobe.com/). Essa funcionalidade aproveita perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes.

Para obter mais informações sobre controle de acesso, consulte a [visão geral do controle de acesso](../../../access-control/home.md).

## Controle de acesso baseado em atributos

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível somente em uma versão limitada.

[Controle de acesso baseado em atributos](../../../access-control/abac/overview.md) O é um recurso do Adobe Experience Platform que permite aos administradores controlar o acesso a objetos e/ou recursos específicos com base em atributos. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário.

Essa funcionalidade permite rotular campos de esquema do Experience Data Model (XDM) com rótulos que definem escopos organizacionais ou de uso de dados. Em paralelo, os administradores podem usar a interface de administração de usuários e funções para definir políticas de acesso em torno de campos de esquema XDM e gerenciar melhor o acesso fornecido aos usuários ou grupos de usuários (usuários internos, externos ou de terceiros). Além disso, o controle de acesso baseado em atributos permite que os administradores gerenciem o acesso a segmentos específicos.

Por meio do controle de acesso baseado em atributos, os administradores podem controlar o acesso dos usuários a dados pessoais confidenciais (SPD) e a informações de identificação pessoal (PII) em todos os fluxos de trabalho e recursos da plataforma. Os administradores podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.

Devido ao controle de acesso baseado em atributos, alguns campos e funcionalidades podem ter acesso restrito e estar indisponíveis para determinados modelos de serviço do Attribution AI. Os exemplos incluem &quot;Identidade&quot;, &quot;Definição de pontuação&quot; e &quot;Clone&quot;.

Na parte superior do espaço de trabalho Attribution AI **página de insights**, os detalhes exibidos na barra lateral têm acesso restrito.

![O espaço de trabalho do Attribution AI com os campos de esquema restritos realçados.](../images/user-guide/access-restricted.png)

Se você selecionar conjuntos de dados com esquemas restritos na **[!UICONTROL Criar fluxo de trabalho de modelo]** , um sinal de aviso será exibido ao lado do nome do conjunto de dados com a mensagem: [!UICONTROL As informações restritas são excluídas].

![O espaço de trabalho do Attribution AI com os campos restritos do conjunto de dados destacados.](../images/user-guide/restricted-info-excluded.png)

Ao visualizar conjuntos de dados com esquema restrito no **[!UICONTROL Criar fluxo de trabalho de modelo]** página, um aviso será exibido para informar que [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na pré-visualização do conjunto de dados.]

![O espaço de trabalho do Attribution AI com os resultados dos campos de esquema visualizados restritos destacados.](../images/user-guide/restricted-dataset-preview.png)

Depois de criar um modelo com informações restritas e prosseguir para a **[!UICONTROL Definir meta]** etapa, um aviso é exibido na parte superior: [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na configuração.]

![O espaço de trabalho do Attribution AI com os campos restritos dos resultados do modelo foi realçado.](../images/user-guide/information-not-displayed-save-and-exit.png)

## Próximas etapas

Ao ler este guia, você foi apresentado aos principais princípios de controle de acesso no [!DNL Experience Platform]. Agora você pode continuar com a [guia do usuário de controle de acesso](../overview.md) para obter etapas detalhadas sobre como usar o [!DNL Admin Console] para criar perfis de produtos e atribuir permissões para [!DNL Platform].
