---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Guia de solução de problemas do Privacy Service
description: Este documento fornece respostas a perguntas frequentes sobre o Privacy Service, bem como informações sobre erros encontrados com frequência na API.
exl-id: 8afbb065-0f41-4048-9003-a22c0c839717
source-git-commit: b48c24ac032cbf785a26a86b50a669d7fcae5d97
workflow-type: tm+mt
source-wordcount: '1028'
ht-degree: 4%

---

# Guia de solução de problemas do [!DNL Privacy Service]

O Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface para ajudar as empresas a gerenciar solicitações de privacidade de dados do cliente. Com o [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados pessoais ou privados do cliente, facilitando a conformidade automatizada com as regulamentações organizacionais e legais de privacidade.

Este documento fornece respostas a perguntas frequentes sobre o [!DNL Privacy Service], bem como informações sobre erros encontrados com frequência na API.

## Ao fazer solicitações de privacidade na API, qual é a diferença entre um usuário e uma ID de usuário? {#user-ids}

Para fazer um novo trabalho de privacidade na API, a carga JSON da solicitação deve conter uma matriz `users` que lista informações específicas de cada usuário ao qual a solicitação de privacidade se aplica. Cada item na matriz `users` é um objeto que representa um usuário específico, identificado por seu valor `key`.

Por sua vez, cada objeto de usuário (ou `key`) contém sua própria matriz `userIDs`. Esta matriz lista valores de ID específicos **para esse usuário específico**.

Considere o exemplo de matriz `users` a seguir:

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

A matriz contém dois objetos, representando usuários individuais identificados por seus valores `key` (&quot;DavidSmith&quot; e &quot;user12345&quot;). &quot;DavidSmith&quot; tem apenas uma ID listada (seu endereço de email), enquanto &quot;user12345&quot; tem duas (seu endereço de email e ECID).

Para obter mais informações sobre como fornecer informações de identidade do usuário, consulte o manual em [dados de identidade para solicitações de privacidade](identity-data.md).


## Posso usar o [!DNL Privacy Service] para limpar dados que foram enviados por acidente para [!DNL Experience Platform]?

A Adobe não oferece suporte ao uso de [!DNL Privacy Service] para limpeza de dados enviados por acidente a um produto. O [!DNL Privacy Service] foi projetado para ajudá-lo a cumprir suas obrigações de acesso ao titular dos dados (ou consumidor) ou de exclusão de solicitações. Qualquer outro uso do Privacy Service para limpeza ou manutenção de dados não é suportado ou permitido.

As solicitações de privacidade são sensíveis ao tempo e são concluídas em relação à lei de privacidade aplicável. o envio de solicitações que não são acesso ao titular dos dados/consumidor ou solicitações de exclusão afeta todos os clientes do [!DNL Privacy Service] e a capacidade do [!DNL Privacy Service] de oferecer suporte às linhas do tempo legais apropriadas. Um limite rígido de upload diário está em vigor para ajudar a evitar o abuso do serviço.

Entre em contato com a equipe de conta da Adobe para coordenar e fornecer um nível de esforço para remover qualquer problema de PII ou dados.

## Como posso obter informações sobre o status da minha solicitação de privacidade ou do meu trabalho?

Você pode recuperar detalhes sobre um trabalho específico usando a API [!DNL Privacy Service] ou a interface do usuário.

### Uso da API

Para recuperar o status de um trabalho específico usando a API [!DNL Privacy Service], faça uma solicitação para o ponto de extremidade raiz (`GET /`) usando a ID do trabalho no caminho da solicitação. Para obter mais detalhes, consulte a seção sobre [verificação do status de um trabalho](api/privacy-jobs.md#check-the-status-of-a-job) no guia de API [!DNL Privacy Service].

### Uso da interface

Todas as solicitações de trabalho ativas estão listadas no widget **[!UICONTROL Solicitações de trabalho]**, no painel da interface do usuário [!DNL Privacy Service]. O status de cada solicitação de trabalho é exibido abaixo da coluna **[!UICONTROL Status]**. Para obter mais informações sobre como exibir solicitações de trabalho na interface do usuário, consulte o [guia do usuário do Privacy Service](ui/user-guide.md).

## Como baixar os resultados dos meus processos de privacidade concluídos?

A API [!DNL Privacy Service] e a interface do usuário fornecem métodos para baixar os resultados de trabalhos concluídos no formato ZIP.

### Uso da API

Faça uma solicitação para o ponto de extremidade raiz (`GET /`) na API [!DNL Privacy Service], usando a ID do trabalho cujos resultados você deseja baixar no caminho da solicitação. Se o status do trabalho for concluído, a API incluirá um atributo `downloadURL` no corpo da resposta. Este atributo contém um URL que você pode colar na barra de endereços do navegador para baixar o arquivo ZIP.

Para obter mais detalhes, consulte a seção sobre [procurando um trabalho pela sua ID](api/privacy-jobs.md#check-the-status-of-a-job) no guia de API [!DNL Privacy Service].

### Uso da interface

No painel da interface do usuário do [!DNL Privacy Service], encontre o trabalho que deseja baixar no widget **Solicitações de trabalho**. Selecione a ID do trabalho para abrir a página Detalhes do trabalho. Aqui, selecione **Baixar** no canto superior direito para baixar o arquivo ZIP. Consulte o [guia do usuário do Privacy Service](ui/user-guide.md) para obter etapas mais detalhadas.

## Mensagens de erro comuns {#common-error-messages}

A tabela a seguir descreve alguns erros comuns em [!DNL Privacy Service], com descrições para ajudar a resolver seus respectivos problemas.

| Mensagem de erro | Descrição |
| --- | --- |
| IDs de usuário não encontradas. | Algumas IDs de usuário fornecidas na solicitação não foram encontradas e foram ignoradas. Verifique se você está usando os namespaces e valores de ID corretos na carga da solicitação. Consulte o documento em [fornecendo dados de identidade](./identity-data.md) para obter uma explicação mais detalhada. |
| Namespace inválido | Um namespace de identidade fornecido para uma ID de usuário era inválido. Consulte a seção sobre [namespaces de identidade padrão](./api/appendix.md#standard-namespaces) no apêndice do guia de API [!DNL Privacy Service] para obter uma lista de namespaces aceitos. Se estiver usando um namespace personalizado, verifique se está definindo a propriedade `type` da ID como &quot;personalizada&quot;. |
| Concluído parcialmente | O trabalho foi concluído com êxito, mas alguns dados não eram aplicáveis à solicitação fornecida e foram ignorados. |
| Os dados não estão no formato necessário. | Um ou mais valores de dados para o aplicativo especificado foram formatados incorretamente. Verifique os detalhes do trabalho para obter mais informações. |
| A Organização IMS não foi provisionada. | Esta mensagem ocorre quando sua organização não foi provisionada para [!DNL Privacy Service]. Entre em contato com o administrador para obter mais informações. |
| O acesso e as permissões são necessários. | O acesso e as permissões são necessários para usar o [!DNL Privacy Service]. Entre em contato com o administrador para obter acesso. |
| Houve um problema ao carregar e arquivar os dados de acesso. | Quando esse erro ocorrer, carregue novamente os dados de acesso e tente novamente. |
| A carga de trabalho foi excedida para o limite de taxa de documentos atual. | Quando esse erro ocorrer, reduza a taxa de envio e tente novamente. |
| Muitas solicitações<br> (erros HTTP 429) | Se os padrões de envio excederem o limite monitorado de trabalhos de titulares de dados permitidos, você receberá um erro HTTP 429 em resposta ao tráfego contínuo da sua organização. O Privacy Service se destina ao processamento de solicitações de privacidade do titular dos dados. Não deve ser usado para limpeza de dados. Se você receber erros HTTP 429, os limites de limitação e solicitação serão implementados para proteger o Adobe contra abusos que podem colocar em risco a conformidade legítima.<br>Métodos alternativos para minimizar seus dados são fornecidos por [definindo agendamentos de expiração do conjunto de dados](../hygiene/ui/dataset-expiration.md) e usando o [recurso de exclusão de registro](../hygiene/ui/record-delete.md). Consulte a respectiva documentação para obter mais informações sobre como aplicar esses recursos. |
