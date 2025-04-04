---
keywords: Experience Platform;guia do usuário;ia do cliente;tópicos populares;controles de acesso;criar modelo;
solution: Experience Platform
feature: Customer AI
title: Controle de acesso para o Customer AI
description: Este documento fornece informações sobre o controle de acesso baseado em atributos para a IA do cliente.
exl-id: 02e3b6a4-304a-4ac4-b07c-010531101feb
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '520'
ht-degree: 4%

---

# Controle de acesso baseado em atributos na IA do cliente

>[!IMPORTANT]
>
>O controle de acesso baseado em atributos está disponível somente em uma versão limitada.

[O controle de acesso baseado em atributos](../../../access-control/abac/overview.md) é um recurso do Adobe Experience Platform que permite aos administradores controlar o acesso a objetos e/ou recursos específicos com base em atributos. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo ou segmento de esquema. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário.

Essa funcionalidade permite rotular campos de esquema do Experience Data Model (XDM) com rótulos que definem escopos organizacionais ou de uso de dados. Em paralelo, os administradores podem usar a interface de administração de usuários e funções para definir políticas de acesso em torno de campos de esquema XDM e gerenciar melhor o acesso fornecido aos usuários ou grupos de usuários (usuários internos, externos ou de terceiros). Além disso, o controle de acesso baseado em atributos permite que os administradores gerenciem o acesso a segmentos específicos.

Por meio do controle de acesso baseado em atributos, os administradores da sua organização podem controlar o acesso dos usuários a dados pessoais confidenciais (SPD) e a informações de identificação pessoal (PII) em todos os fluxos de trabalho e recursos da Experience Platform. Admins podem definir funções de usuário que tenham acesso somente a campos e dados específicos que correspondam a esses campos.

Devido ao controle de acesso baseado em atributos, alguns campos e funcionalidades teriam acesso restrito e não estariam disponíveis para determinados modelos de serviço da IA do cliente. Os exemplos incluem &quot;Identidade&quot;, &quot;Definição de pontuação&quot; e &quot;Clone&quot;.

![O espaço de trabalho da IA do cliente com os campos restritos dos resultados do modelo de serviço foi realçado.](../images/user-guide/unavailable-functionalities.png)

Na parte superior da **página de insights** da IA do cliente, observe que os detalhes na barra lateral, definição de pontuação, identidade e atributos de perfil mostram &quot;Acesso restrito&quot;.

![O espaço de trabalho da IA do cliente com os campos restritos do esquema realçados.](../images/user-guide/access-restricted.png)

Ao visualizar conjuntos de dados com esquema restrito na página **[!UICONTROL Criar fluxo de trabalho de modelo]**, um aviso será exibido para informar que [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na visualização do conjunto de dados.]

![O espaço de trabalho da IA do cliente com os campos restritos dos conjuntos de dados de visualização com resultados de esquema restritos foi realçado.](../images/user-guide/restricted-dataset-preview-save-and-exit-cai.png)

Depois de criar um modelo com informações restritas e prosseguir para a etapa **[!UICONTROL Definir meta]**, um aviso é exibido na parte superior: [!UICONTROL Devido a restrições de acesso, determinadas informações não são exibidas na configuração.]

![O espaço de trabalho da IA do cliente com os campos restritos dos resultados do modelo de serviço foi realçado.](../images/user-guide/information-not-displayed-save-and-exit.png)

Ao usar o controle de acesso, os privilégios **Exibir IA do cliente** e **Gerenciar IA do cliente** concedem acesso a diferentes funcionalidades da IA do cliente. A permissão **Gerenciar IA do cliente** permite **criar**,**atualizar**, **excluir**, **habilitar** ou **desabilitar** um modelo, enquanto a **Exibir IA do cliente** permite que você leia ou exiba-o. As ações **criar**, **atualizar** e **excluir** são registradas por logs de auditoria.

Consulte a documentação para saber [atribuir permissões para controle de acesso](../../../access-control/home.md) ou como [usar logs de auditoria para monitorar acesso e atividade](../../../landing/governance-privacy-security/audit-logs/overview.md).

## Próximas etapas

Ao ler este guia, você foi apresentado aos princípios mais importantes do controle de acesso no [!DNL Experience Platform]. Agora você pode continuar com o [guia do usuário de controle de acesso](../overview.md) para obter etapas detalhadas sobre como usar o [!DNL Admin Console] para criar perfis de produtos e atribuir permissões para [!DNL Experience Platform].
