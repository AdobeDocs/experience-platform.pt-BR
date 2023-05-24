---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Guia de solução de problemas do Privacy Service
description: Este documento fornece respostas a perguntas frequentes sobre o Privacy Service, bem como informações sobre erros encontrados com frequência na API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '916'
ht-degree: 0%

---

# [!DNL Privacy Service] guia de solução de problemas

Adobe Experience Platform [!DNL Privacy Service] O fornece uma API RESTful e uma interface para ajudar as empresas a gerenciar solicitações de privacidade de dados do cliente. Com [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados privados ou pessoais do cliente, facilitando a conformidade automatizada com as regulamentações organizacionais e legais de privacidade.

Este documento fornece respostas a perguntas frequentes sobre [!DNL Privacy Service], bem como informações sobre erros comuns na API.

## Ao fazer solicitações de privacidade na API, qual é a diferença entre um usuário e uma ID de usuário? {#user-ids}

Para fazer um novo trabalho de privacidade na API, a carga JSON da solicitação deve conter uma `users` matriz que lista informações específicas de cada usuário ao qual a solicitação de privacidade se aplica. Cada item no `users` matriz é um objeto que representa um usuário específico, identificado por sua `key` valor.

Por sua vez, cada objeto de usuário (ou `key`) contém sua própria `userIDs` matriz. Essa matriz lista valores de ID específicos **para esse usuário específico**.

Considere o exemplo a seguir `users` matriz:

```json
"users": [
  {
    "key": "DavidSmith",
    "action": ["access"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "dsmith@acme.com",
        "type": "standard"
      }
    ]
  },
  {
    "key": "user12345",
    "action": ["access", "delete"],
    "userIDs": [
      {
        "namespace": "email",
        "value": "ajones@acme.com",
        "type": "standard"
      },
      {
        "namespace": "ECID",
        "type": "standard",
        "value":  "443636576799758681021090721276",
        "isDeletedClientSide": false
      }
    ]
  }
]
```

A matriz contém dois objetos, representando usuários individuais identificados por seus `key` valores (&quot;DavidSmith&quot; e &quot;user12345&quot;). &quot;DavidSmith&quot; tem apenas uma ID listada (seu endereço de email), enquanto &quot;user12345&quot; tem duas (seu endereço de email e ECID).

Para obter mais informações sobre como fornecer informações de identidade do usuário, consulte o manual sobre [dados de identidade para solicitações de privacidade](identity-data.md).


## Posso usar [!DNL Privacy Service] para limpar dados enviados por acidente para o [!DNL Platform]?

O Adobe não suporta o uso de [!DNL Privacy Service] para limpar dados enviados por acidente a um produto. [!DNL Privacy Service] O foi projetado para ajudá-lo a cumprir suas obrigações de acesso ou exclusão de solicitações do titular dos dados (ou consumidor). Qualquer outro uso do Privacy Service para limpeza ou manutenção de dados não é suportado ou permitido.

As solicitações de privacidade são sensíveis ao tempo e são concluídas em relação à lei de privacidade aplicável. a submissão de solicitações que não são acesso do titular dos dados/consumidor ou solicitações de exclusão afeta todos [!DNL Privacy Service] clientes e a capacidade de [!DNL Privacy Service] para apoiar os prazos legais adequados. Um limite rígido de upload diário está em vigor para ajudar a evitar o abuso do serviço.

Entre em contato com a equipe de conta do Adobe para coordenar e realizar um nível de esforço para remover qualquer problema de PII ou dados.

## Como posso obter informações sobre o status da minha solicitação de privacidade ou do meu trabalho?

Você pode recuperar detalhes sobre um job específico usando o [!DNL Privacy Service] API ou interface do usuário.

### Uso da API

Para recuperar o status de um job específico usando o [!DNL Privacy Service] , faça uma solicitação à raiz (`GET /`), usando a ID da tarefa no caminho da solicitação. Para obter mais detalhes, consulte a seção sobre [verificação do status de um job](api/privacy-jobs.md#check-the-status-of-a-job) no [!DNL Privacy Service] Guia da API.

### Uso da interface

Todas as solicitações de trabalho ativas estão listadas no **[!UICONTROL Solicitações de tarefa]** widget na [!DNL Privacy Service] Painel da interface do usuário. O status de cada solicitação de trabalho é exibido abaixo de **[!UICONTROL Status]** coluna. Para obter mais informações sobre como exibir solicitações de trabalho na interface, consulte [guia do usuário do Privacy Service](ui/user-guide.md).

## Como baixar os resultados dos meus processos de privacidade concluídos?

A variável [!DNL Privacy Service] A API e a interface do usuário fornecem métodos para baixar os resultados de trabalhos concluídos no formato ZIP.

### Uso da API

Faça uma solicitação à raiz (`GET /`) no [!DNL Privacy Service] API, usando a ID do trabalho cujos resultados você deseja baixar no caminho da solicitação. Se o status da tarefa for concluído, a API incluirá uma `downloadURL` no corpo da resposta. Este atributo contém um URL que você pode colar na barra de endereços do navegador para baixar o arquivo ZIP.

Para obter mais detalhes, consulte a seção sobre [procurar um trabalho pela ID](api/privacy-jobs.md#check-the-status-of-a-job) no [!DNL Privacy Service] Guia da API.

### Uso da interface

No [!DNL Privacy Service] painel da interface do usuário, localize o trabalho que deseja baixar na **Solicitações de tarefa** widget. Selecione a ID do trabalho para abrir a página Detalhes do trabalho. Aqui, selecione **Baixar** no canto superior direito para baixar o arquivo ZIP. Consulte a [guia do usuário do Privacy Service](ui/user-guide.md) para obter etapas mais detalhadas.

## Mensagens de erro comuns

A tabela a seguir descreve alguns erros comuns no [!DNL Privacy Service], com descrições para ajudar a resolver seus respectivos problemas.

| Mensagem de erro | Descrição |
| --- | --- |
| IDs de usuário não encontradas. | Algumas IDs de usuário fornecidas na solicitação não foram encontradas e foram ignoradas. Verifique se você está usando os namespaces e valores de ID corretos na carga da solicitação. Consulte o documento sobre [fornecimento de dados de identidade](./identity-data.md) para obter uma explicação mais detalhada. |
| Namespace inválido | Um namespace de identidade fornecido para uma ID de usuário era inválido. Consulte a seção sobre [namespaces de identidade padrão](./api/appendix.md#standard-namespaces) no [!DNL Privacy Service] Apêndice do guia de API para obter uma lista de namespaces aceitos. Se estiver usando um namespace personalizado, verifique se está definindo as IDs do `type` para &quot;personalizado&quot;. |
| Concluído parcialmente | O trabalho foi concluído com êxito, mas alguns dados não eram aplicáveis à solicitação fornecida e foram ignorados. |
| Os dados não estão no formato exigido. | Um ou mais valores de dados para o aplicativo especificado foram formatados incorretamente. Verifique os detalhes do trabalho para obter mais informações. |
| A Organização IMS não foi provisionada. | Esta mensagem ocorre quando sua organização não foi provisionada para [!DNL Privacy Service]. Entre em contato com o administrador para obter mais informações. |
| O acesso e as permissões são necessários. | O acesso e as permissões são necessários para usar o [!DNL Privacy Service]. Entre em contato com o administrador para obter acesso. |
| Ocorreu um problema ao carregar e arquivar os dados de acesso. | Quando esse erro ocorrer, carregue novamente os dados de acesso e tente novamente. |
| A carga de trabalho foi excedida para o limite de taxa de documentos atual. | Quando esse erro ocorrer, reduza a taxa de envio e tente novamente. |
