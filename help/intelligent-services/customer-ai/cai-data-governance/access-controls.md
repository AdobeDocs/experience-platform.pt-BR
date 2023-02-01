---
keywords: Experience Platform, guia do usuário, atendimento ao cliente, tópicos populares, controles de acesso, criar modelo;
solution: Experience Platform
feature: Customer AI
title: Controle de acesso para Customer AI
description: Este documento fornece informações sobre o controle de acesso baseado em atributos para o Customer AI.
source-git-commit: 6f386d859b8553050ead266fad0e473c7cf7095e
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Controle de acesso baseado em atributos

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível apenas em uma versão limitada.

[Controle de acesso baseado em atributos](../../../access-control/abac/overview.md) é um recurso do Adobe Experience Platform que permite aos administradores controlar o acesso a objetos e/ou recursos específicos com base em atributos. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário.

Essa funcionalidade permite rotular campos de esquema do Experience Data Model (XDM) com rótulos que definem escopos organizacionais ou de uso de dados. Em paralelo, os administradores podem usar a interface de administração de usuário e função para definir políticas de acesso em torno dos campos do esquema XDM e gerenciar melhor o acesso dado aos usuários ou grupos de usuários (usuários internos, externos ou de terceiros). Além disso, o controle de acesso baseado em atributos permite que os administradores gerenciem o acesso a segmentos específicos.

Por meio do controle de acesso baseado em atributos, os administradores da sua organização podem controlar o acesso dos usuários aos dados pessoais confidenciais (SPD) e às informações de identificação pessoal (PII) em todos os fluxos de trabalho e recursos da plataforma. Os administradores podem definir funções de usuário que têm acesso apenas a campos e dados específicos que correspondem a esses campos.

Devido ao controle de acesso baseado em atributos, alguns campos e funcionalidades teriam acesso restrito e não estariam disponíveis para determinados modelos de serviço do Customer AI. Os exemplos incluem, &quot;Identidade&quot;, &quot;Definição de pontuação&quot; e &quot;Clonar&quot;.

![A área de trabalho do Customer AI com os campos restritos do modelo de serviço é realçada.](../images/user-guide/unavailable-functionalities.png)

Na parte superior da área de trabalho do Customer AI **página de insights**, observe que os detalhes na barra lateral, definição de pontuação, identidade e atributos de perfil mostram &quot;Acesso restrito&quot;.

![A área de trabalho do Customer AI com os campos restritos do schema realçado.](../images/user-guide/access-restricted.png)

Ao visualizar conjuntos de dados com esquema restrito na **[!UICONTROL Criar fluxo de trabalho modelo]** , um aviso será exibido para informá-lo que [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na visualização do conjunto de dados.]

![A área de trabalho do Customer AI com os campos restritos dos conjuntos de dados de visualização com resultados restritos do schema são realçados.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Depois de criar um modelo com informações restritas e prosseguir para a **[!UICONTROL Definir meta]** , um aviso é exibido na parte superior: [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na configuração.]

![A área de trabalho do Customer AI com os campos restritos do modelo de serviço é realçada.](../images/user-guide/information-not-displayed-save-and-exit.png)

Ao usar o controle de acesso, a variável **Exibir AI do cliente** e **Gerenciar o Customer AI** concede acesso a diferentes funcionalidades da API do cliente. O **Gerenciar o Customer AI** permissão permite **criar**,**atualizar**, **excluir**, **habilitar** ou **disable** um modelo ao **Exibir AI do cliente** permite que você leia ou visualize. O **criar**, **atualizar** e **excluir** ações são registradas por logs de auditoria.

Consulte a documentação para saber mais [atribuição de permissões para controle de acesso](../../../access-control/home.md) ou como [usar logs de auditoria para monitorar o acesso e a atividade](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Próximas etapas

Ao ler este guia, você foi apresentado aos principais princípios do controle de acesso no [!DNL Experience Platform]. Agora você pode continuar com o [guia do usuário de controle de acesso](../overview.md) para obter etapas detalhadas sobre como usar o [!DNL Admin Console] para criar perfis de produto e atribuir permissões para [!DNL Platform].