---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Perguntas frequentes sobre o Privacy Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 7e2e36e13cffdb625b7960ff060f8158773c0fe3

---


# Perguntas frequentes sobre o Privacy Service

Este documento fornece respostas para perguntas frequentes sobre o Adobe Experience Platform Privacy Service.

O Privacy Service fornece uma API RESTful e uma interface de usuário para ajudar o empresa a gerenciar solicitações de privacidade de dados do cliente. Com o Privacy Service, você pode enviar solicitações para acessar e excluir dados de clientes particulares ou pessoais, facilitando a conformidade automatizada com as regulamentações organizacionais e legais de privacidade.

## Posso usar o Privacy Service para limpar dados que foram enviados acidentalmente para a Plataforma?

A Adobe não oferece suporte ao uso do Privacy Service para limpar dados que foram acidentalmente enviados a um produto. O Privacy Service foi criado para ajudá-lo a cumprir suas obrigações de acesso ou exclusão de solicitações da pessoa de dados (ou do consumidor). Essas solicitações são sensíveis ao tempo e são concluídas com relação à lei de privacidade aplicável. A submissão de solicitações que não são de acesso de pessoa/consumidor ou solicitações de exclusão afeta todos os clientes do Privacy Service e a capacidade do Privacy Service de suportar os prazos legais apropriados.

Entre em contato com seu gerente de conta (CDM) para coordenar e fornecer um nível de esforço para remover quaisquer PII ou problemas de dados.

## Como obtenho informações sobre o status da minha solicitação de privacidade ou trabalho?

Você pode recuperar detalhes sobre um determinado trabalho usando a API do Privacy Service ou a interface do usuário.

### Uso da API

Para recuperar o status de um determinado trabalho usando a API do Privacy Service, faça uma solicitação para o terminal raiz (`GET /`), usando a ID do trabalho no caminho da solicitação. Para obter mais detalhes, consulte a seção sobre como [verificar o status de uma tarefa](api/privacy-jobs.md#check-the-status-of-a-job) no guia do desenvolvedor do Privacy Service.

### Uso da interface

Todas as solicitações de trabalho ativas estão listadas no widget Solicitações **de** trabalho no painel da interface do usuário do Privacy Service. O status de cada solicitação de cargo é exibido na coluna **Status** . Para obter mais informações sobre como visualizar solicitações de trabalho na interface do usuário, consulte o guia [do usuário do](ui/user-guide.md)Privacy Service.

## Como baixar os resultados de meus trabalhos de privacidade concluídos?

A API do Privacy Service e a interface do usuário fornecem métodos para baixar os resultados de trabalhos concluídos no formato ZIP.

### Uso da API

Faça uma solicitação para o terminal raiz (`GET /`) na API do Privacy Service, usando a ID do trabalho cujos resultados você deseja baixar no caminho da solicitação. Se o status do trabalho for concluído, a API incluirá um `downloadURL` atributo no corpo da resposta. Este atributo contém um URL que você pode colar na barra de endereços do seu navegador para baixar o arquivo ZIP.

Para obter mais detalhes, consulte a seção sobre como [pesquisar uma tarefa pela ID](api/privacy-jobs.md#check-the-status-of-a-job) no guia do desenvolvedor do Privacy Service.

### Uso da interface

No painel da interface do usuário do Privacy Service, localize o trabalho que deseja baixar no widget Solicitações **de** trabalho. Clique na ID do trabalho para abrir a página Detalhes _do_ trabalho. Aqui, clique em **Download** no canto superior direito para baixar o arquivo ZIP. Consulte o guia [do usuário do](ui/user-guide.md) Privacy Service para obter etapas mais detalhadas.