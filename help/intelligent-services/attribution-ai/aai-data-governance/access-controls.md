---
keywords: Experience Platform, home, tópicos populares, controle de acesso, console de administração da adobe
solution: Experience Platform
feature: Attribution AI
title: Controle de acesso para Attribution AI
description: Este documento fornece informações sobre o controle de acesso baseado em atributos para o Attribution AI.
source-git-commit: d82fd8dd5efbe314c09d32905f8ab964640cc11a
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 1%

---


# Controle de acesso

O controle de acesso do Attribution AI é fornecido pela Adobe Experience Platform no [Adobe Admin Console](https://adminconsole.adobe.com/). Essa funcionalidade utiliza perfis de produto no Admin Console, que vinculam usuários com permissões e sandboxes.

Para obter mais informações sobre o controle de acesso, consulte [visão geral do controle de acesso](../../../access-control/home.md).

## Controle de acesso baseado em atributos

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível apenas em uma versão limitada.

[Controle de acesso baseado em atributos](../../../access-control/abac/overview.md) é um recurso do Adobe Experience Platform que permite aos administradores controlar o acesso a objetos e/ou recursos específicos com base em atributos. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário.

Essa funcionalidade permite rotular campos de esquema do Experience Data Model (XDM) com rótulos que definem escopos organizacionais ou de uso de dados. Em paralelo, os administradores podem usar a interface de administração de usuário e função para definir políticas de acesso em torno dos campos do esquema XDM e gerenciar melhor o acesso dado aos usuários ou grupos de usuários (usuários internos, externos ou de terceiros). Além disso, o controle de acesso baseado em atributos permite que os administradores gerenciem o acesso a segmentos específicos.

Por meio do controle de acesso baseado em atributos, os administradores podem controlar o acesso dos usuários aos dados pessoais confidenciais (SPD) e às informações de identificação pessoal (PII) em todos os fluxos de trabalho e recursos da plataforma. Os administradores podem definir funções de usuário que têm acesso apenas a campos e dados específicos que correspondem a esses campos.

Devido ao controle de acesso baseado em atributos, alguns campos e funcionalidades podem ter acesso restrito e estar indisponíveis para determinados modelos de serviço do Attribution AI. Os exemplos incluem, &quot;Identidade&quot;, &quot;Definição de pontuação&quot; e &quot;Clonar&quot;.

Na parte superior do espaço de trabalho do Attribution AI **página de insights**, os detalhes exibidos na barra lateral têm acesso restrito.

![O espaço de trabalho Attribution AI com os campos de esquema restritos realçados.](../images/user-guide/access-restricted.png)

Se você selecionar conjuntos de dados com esquemas restritos na **[!UICONTROL Criar fluxo de trabalho modelo]** , um sinal de aviso é exibido ao lado do nome do conjunto de dados com a mensagem : [!UICONTROL As informações restritas são excluídas].

![O espaço de trabalho do Attribution AI com os campos de conjunto de dados restritos destacados.](../images/user-guide/restricted-info-excluded.png)

Ao visualizar conjuntos de dados com esquema restrito na **[!UICONTROL Criar fluxo de trabalho modelo]** , um aviso será exibido para informá-lo que [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na visualização do conjunto de dados.]

![O espaço de trabalho do Attribution AI com os resultados de campos de esquema visualizados restritos é realçado.](../images/user-guide/restricted-dataset-preview.png)

Depois de criar um modelo com informações restritas e prosseguir para a **[!UICONTROL Definir meta]** , um aviso é exibido na parte superior: [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na configuração.]

![A área de trabalho do Attribution AI com os campos restritos dos resultados do modelo é realçada.](../images/user-guide/information-not-displayed-save-and-exit.png)

## Próximas etapas

Ao ler este guia, você foi apresentado aos principais princípios do controle de acesso no [!DNL Experience Platform]. Agora você pode continuar com o [guia do usuário de controle de acesso](../overview.md) para obter etapas detalhadas sobre como usar o [!DNL Admin Console] para criar perfis de produto e atribuir permissões para [!DNL Platform].
