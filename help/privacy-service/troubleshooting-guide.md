---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Guia de solução de problemas de Privacy Service
topic-legacy: troubleshooting
description: Este documento fornece respostas a perguntas frequentes sobre o Privacy Service, bem como informações sobre erros comumente encontrados na API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '884'
ht-degree: 0%

---

# [!DNL Privacy Service] guia de solução de problemas

Adobe Experience Platform [!DNL Privacy Service] O fornece uma RESTful API e interface do usuário para ajudar as empresas a gerenciar solicitações de privacidade de dados do cliente. Com [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados pessoais de clientes, facilitando a conformidade automatizada com as regulamentações organizacionais e legais de privacidade.

Este documento fornece respostas para perguntas frequentes sobre [!DNL Privacy Service], bem como informações sobre erros comumente encontrados na API.

## Ao fazer solicitações de privacidade na API, qual é a diferença entre um usuário e uma ID de usuário? {#user-ids}

Para fazer um novo trabalho de privacidade na API, a carga JSON da solicitação deve conter uma `users` que lista informações específicas para cada usuário ao qual a solicitação de privacidade se aplica. Cada item na variável `users` matriz é um objeto que representa um usuário específico, identificado por seu `key` valor.

Por sua vez, cada objeto do usuário (ou `key`) contém o seu próprio `userIDs` matriz. Essa matriz lista valores de ID específicos **para esse usuário específico**.

Considere o exemplo a seguir `users` array:

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

Para obter mais informações sobre como fornecer informações de identidade do usuário, consulte o guia em [dados de identidade para solicitações de privacidade](identity-data.md).


## Posso usar [!DNL Privacy Service] para limpar dados enviados acidentalmente para o [!DNL Platform]?

O Adobe não suporta o uso de [!DNL Privacy Service] para limpar dados que foram acidentalmente submetidos a um produto. [!DNL Privacy Service] O foi projetado para ajudar você a cumprir suas obrigações em relação às solicitações de acesso ou exclusão do titular dos dados (ou do consumidor). Essas solicitações são sensíveis ao tempo e são concluídas com relação à legislação de privacidade aplicável. A apresentação de pedidos que não sejam do titular dos dados/do consumidor ou de pedidos de supressão afeta todos os [!DNL Privacy Service] clientes e a capacidade de [!DNL Privacy Service] apoiar os prazos legais adequados.

Entre em contato com o gerente da conta (CDM) para coordenar e fornecer um nível de esforço para remover qualquer problema de PII ou dados.

## Como obtenho informações sobre o status da minha solicitação de privacidade ou trabalho?

Você pode recuperar detalhes sobre um determinado trabalho usando o [!DNL Privacy Service] API ou interface do usuário.

### Uso da API

Para recuperar o status de um determinado trabalho usando o [!DNL Privacy Service] API, faça uma solicitação para a raiz (`GET /`), usando a ID do trabalho no caminho da solicitação. Para obter mais detalhes, consulte a seção em [verificando o status de um trabalho](api/privacy-jobs.md#check-the-status-of-a-job) no [!DNL Privacy Service] Guia da API.

### Uso da interface do usuário

Todas as solicitações de trabalho ativas estão listadas na **[!UICONTROL Solicitações de trabalho]** no widget [!DNL Privacy Service] Painel da interface do usuário. O status de cada solicitação de trabalho é exibido sob a variável **[!UICONTROL Status]** coluna. Para obter mais informações sobre como visualizar solicitações de trabalho na interface do usuário, consulte o [Guia do usuário do Privacy Service](ui/user-guide.md).

## Como faço o download dos resultados dos meus trabalhos de privacidade concluídos?

O [!DNL Privacy Service] A API e a interface do usuário fornecem métodos para baixar os resultados de trabalhos concluídos no formato ZIP.

### Uso da API

Faça uma solicitação para a raiz (`GET /`) na seção [!DNL Privacy Service] API, usando a ID da tarefa cujos resultados você deseja baixar no caminho da solicitação. Se o status da tarefa for concluído, a API incluirá uma `downloadURL` no corpo da resposta. Esse atributo contém um URL que você pode colar na barra de endereços do navegador para baixar o arquivo ZIP.

Para obter mais detalhes, consulte a seção em [pesquisar uma tarefa pela ID](api/privacy-jobs.md#check-the-status-of-a-job) no [!DNL Privacy Service] Guia da API.

### Uso da interface do usuário

No [!DNL Privacy Service] No painel da interface do usuário, encontre o trabalho que deseja baixar na **Solicitações de trabalho** widget. Selecione a ID do trabalho para abrir a página Detalhes do trabalho . Aqui, selecione **Baixar** no canto superior direito para baixar o arquivo ZIP. Consulte a [Guia do usuário do Privacy Service](ui/user-guide.md) para obter etapas mais detalhadas.

## Mensagens de erro comuns

A tabela a seguir descreve alguns erros comuns em [!DNL Privacy Service], com descrições para ajudar a resolver seus respectivos problemas.

| Mensagem de erro | Descrição |
| --- | --- |
| IDs de usuário não encontradas. | Algumas das IDs de usuário fornecidas na solicitação não foram encontradas e foram ignoradas. Verifique se você está usando os namespace e os valores de ID corretos na carga da solicitação. Consulte o documento em [fornecimento de dados de identidade](./identity-data.md) para obter uma explicação mais detalhada. |
| Namespace Inválido | Um namespace de identidade fornecido para uma ID de usuário era inválido. Consulte a seção sobre [namespaces de identidade padrão](./api/appendix.md#standard-namespaces) no [!DNL Privacy Service] Apêndice do guia de API para obter uma lista de namespaces aceitos. Se estiver usando um namespace personalizado, certifique-se de configurar as IDs `type` para &quot;personalizado&quot;. |
| Parcialmente Concluído | O trabalho foi concluído com êxito, mas alguns dados não eram aplicáveis à solicitação e foram ignorados. |
| Os dados não estão no formato necessário. | Um ou mais valores de dados para o aplicativo especificado foram formatados incorretamente. Verifique os detalhes do trabalho para obter mais informações. |
| A Organização IMS não foi provisionada. | Essa mensagem ocorre quando a sua Organização IMS não foi provisionada para [!DNL Privacy Service]. Entre em contato com o administrador para obter mais informações. |
| O acesso e as permissões são necessários. | O acesso e as permissões são necessários para usar [!DNL Privacy Service]. Entre em contato com o administrador para obter acesso. |
| Ocorreu um problema ao carregar e arquivar os dados de acesso. | Quando este erro ocorrer, faça novamente o upload dos dados de acesso e tente novamente. |
| A carga de trabalho foi excedida para o limite de taxa de documentos atual. | Quando este erro ocorrer, reduza a taxa de envio e tente novamente. |
