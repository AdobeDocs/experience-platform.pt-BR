---
keywords: Experience Platform;guia do usuário;ia do cliente;tópicos populares;controles de acesso;criar modelo;
solution: Experience Platform
feature: Customer AI
title: Controle de acesso para o Customer AI
description: Este documento fornece informações sobre o controle de acesso baseado em atributos para a IA do cliente.
exl-id: 02e3b6a4-304a-4ac4-b07c-010531101feb
source-git-commit: f28558d5939607cabf449cbc03b7e0f5406f6326
workflow-type: tm+mt
source-wordcount: '519'
ht-degree: 0%

---

# Controle de acesso baseado em atributos na IA do cliente

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível somente em uma versão limitada.

[Controle de acesso baseado em atributos](../../../access-control/abac/overview.md) O é um recurso do Adobe Experience Platform que permite aos administradores controlar o acesso a objetos e/ou recursos específicos com base em atributos. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário.

Essa funcionalidade permite rotular campos de esquema do Experience Data Model (XDM) com rótulos que definem escopos organizacionais ou de uso de dados. Em paralelo, os administradores podem usar a interface de administração de usuários e funções para definir políticas de acesso em torno de campos de esquema XDM e gerenciar melhor o acesso fornecido aos usuários ou grupos de usuários (usuários internos, externos ou de terceiros). Além disso, o controle de acesso baseado em atributos permite que os administradores gerenciem o acesso a segmentos específicos.

Por meio do controle de acesso baseado em atributos, os administradores da sua organização podem controlar o acesso dos usuários a dados pessoais confidenciais (SPD) e a informações de identificação pessoal (PII) em todos os fluxos de trabalho e recursos da plataforma. Os administradores podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.

Devido ao controle de acesso baseado em atributos, alguns campos e funcionalidades teriam acesso restrito e não estariam disponíveis para determinados modelos de serviço da IA do cliente. Os exemplos incluem &quot;Identidade&quot;, &quot;Definição de pontuação&quot; e &quot;Clone&quot;.

![O espaço de trabalho da IA do cliente com os campos restritos dos resultados do modelo de serviço é realçado.](../images/user-guide/unavailable-functionalities.png)

Na parte superior do espaço de trabalho da IA do cliente **página de insights**, observe que os detalhes na barra lateral, definição de pontuação, identidade e atributos de perfil mostram &quot;Acesso Restrito&quot;.

![O espaço de trabalho da IA do cliente com os campos restritos do esquema realçados.](../images/user-guide/access-restricted.png)

Ao visualizar conjuntos de dados com esquema restrito no **[!UICONTROL Criar fluxo de trabalho de modelo]** página, um aviso será exibido para informar que [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na pré-visualização do conjunto de dados.]

![O espaço de trabalho da IA do cliente com os campos restritos dos conjuntos de dados de visualização com resultados restritos de esquema é realçado.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Depois de criar um modelo com informações restritas e prosseguir para a **[!UICONTROL Definir meta]** etapa, um aviso é exibido na parte superior: [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na configuração.]

![O espaço de trabalho da IA do cliente com os campos restritos dos resultados do modelo de serviço é realçado.](../images/user-guide/information-not-displayed-save-and-exit.png)

Ao usar o controle de acesso, a variável **Exibir IA do cliente** e **Gerenciar o Customer AI** Os privilégios concedem acesso a diferentes funcionalidades da IA do cliente. A variável **Gerenciar o Customer AI** permissão permite **criar**,**atualizar**, **excluir**, **habilitar** ou **disable** um modelo enquanto **Exibir IA do cliente** permite ler ou visualizar. A variável **criar**, **atualizar** e **excluir** as ações são registradas por logs de auditoria.

Consulte a documentação para saber mais [atribuição de permissões para controle de acesso](../../../access-control/home.md) ou como [usar logs de auditoria para monitorar o acesso e a atividade](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Próximas etapas

Ao ler este guia, você foi apresentado aos principais princípios de controle de acesso no [!DNL Experience Platform]. Agora você pode continuar com a [guia do usuário de controle de acesso](../overview.md) para obter etapas detalhadas sobre como usar o [!DNL Admin Console] para criar perfis de produtos e atribuir permissões para [!DNL Platform].
