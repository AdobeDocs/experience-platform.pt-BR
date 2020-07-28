---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Perguntas frequentes sobre o Privacy Service
topic: troubleshooting
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '856'
ht-degree: 0%

---


# [!DNL Privacy Service] guia de solução de problemas

O Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface de usuário para ajudar o empresa a gerenciar solicitações de privacidade de dados do cliente. Com [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados pessoais ou privados do cliente, facilitando a conformidade automatizada com as regulamentações organizacionais e legais de privacidade.

Este documento fornece respostas para perguntas frequentes sobre [!DNL Privacy Service]o , bem como informações sobre erros frequentemente encontrados na API.

## Ao fazer solicitações de privacidade na API, qual é a diferença entre uma ID de usuário e uma ID de usuário? {#user-ids}

Para fazer um novo trabalho de privacidade na API, a carga JSON da solicitação deve conter um `users` storage que lista informações específicas para cada usuário ao qual a solicitação de privacidade se aplica. Cada item na `users` matriz é um objeto que representa um usuário específico, identificado pelo seu `key` valor.

Por sua vez, cada objeto de usuário (ou `key`) contém sua própria `userIDs` matriz. Essa matriz lista valores de ID específicos **para esse usuário** específico.

Consider the following example `users` array:

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

O storage contém dois objetos, representando usuários individuais identificados por seus `key` valores (&quot;DavidSmith&quot; e &quot;user12345&quot;). &quot;DavidSmith&quot; tem apenas uma ID listada (seu endereço de email), enquanto &quot;user12345&quot; tem duas (seu endereço de email e ECID).

Para obter mais informações sobre como fornecer informações de identidade do usuário, consulte o guia sobre dados de [identidade para solicitações](identity-data.md)de privacidade.


## Posso usar [!DNL Privacy Service] para limpar dados que foram enviados acidentalmente para [!DNL Platform]?

O Adobe não suporta o uso [!DNL Privacy Service] para limpar dados que foram acidentalmente enviados a um produto. [!DNL Privacy Service] foi projetado para ajudá-lo a cumprir suas obrigações de acesso ou exclusão de solicitações da pessoa em causa (ou do consumidor). Essas solicitações são sensíveis ao tempo e são concluídas com relação à lei de privacidade aplicável. A apresentação de pedidos que não sejam de acesso a pessoas em causa/consumidores ou de pedidos de eliminação afeta todos os [!DNL Privacy Service] clientes e a capacidade de [!DNL Privacy Service] suportar os prazos legais adequados.

Entre em contato com seu gerente de conta (CDM) para coordenar e fornecer um nível de esforço para remover quaisquer PII ou problemas de dados.

## Como obtenho informações sobre o status da minha solicitação de privacidade ou trabalho?

Você pode recuperar detalhes sobre um determinado trabalho usando a [!DNL Privacy Service] API ou a interface do usuário.

### Uso da API

Para recuperar o status de um determinado trabalho usando a [!DNL Privacy Service] API, faça uma solicitação para o terminal raiz (`GET /`), usando a ID do trabalho no caminho da solicitação. Para obter mais detalhes, consulte a seção sobre como [verificar o status de uma tarefa](api/privacy-jobs.md#check-the-status-of-a-job) no guia do [!DNL Privacy Service] desenvolvedor.

### Uso da interface

Todas as solicitações de trabalho ativas estão listadas no widget Solicitações **[!UICONTROL de]** trabalho no painel da [!DNL Privacy Service] interface do usuário. O status de cada solicitação de cargo é exibido na coluna **[!UICONTROL Status]** . Para obter mais informações sobre como visualizar solicitações de trabalho na interface do usuário, consulte o guia [do usuário do](ui/user-guide.md)Privacy Service.

## Como baixar os resultados de meus trabalhos de privacidade concluídos?

A [!DNL Privacy Service] API e a interface do usuário fornecem métodos para baixar os resultados de trabalhos concluídos no formato ZIP.

### Uso da API

Faça uma solicitação para o terminal raiz (`GET /`) na [!DNL Privacy Service] API, usando a ID do trabalho cujos resultados você deseja baixar no caminho da solicitação. Se o status do trabalho for concluído, a API incluirá um `downloadURL` atributo no corpo da resposta. Este atributo contém um URL que você pode colar na barra de endereços do seu navegador para baixar o arquivo ZIP.

Para obter mais detalhes, consulte a seção sobre como [procurar um trabalho pela ID](api/privacy-jobs.md#check-the-status-of-a-job) no guia do [!DNL Privacy Service] desenvolvedor.

### Uso da interface

No painel da interface do usuário, localize o trabalho que deseja baixar do widget Solicitações [!DNL Privacy Service] de **** trabalho. Clique na ID do trabalho para abrir a página Detalhes _do_ trabalho. Aqui, clique em **Download** no canto superior direito para baixar o arquivo ZIP. Consulte o guia [do usuário do](ui/user-guide.md) Privacy Service para obter etapas mais detalhadas.

## Mensagens de erro comuns

A tabela a seguir descreve alguns erros comuns no [!DNL Privacy Service], com descrições para ajudar a resolver seus respectivos problemas.

| Mensagem de erro | Descrição |
| --- | --- |
| IDs de usuário não encontradas. | Algumas IDs de usuário fornecidas na solicitação não foram encontradas e foram ignoradas. Verifique se você está usando as namespaces e os valores de ID corretos na carga da solicitação. Consulte o documento sobre como [fornecer dados](./identity-data.md) de identidade para obter uma explicação mais detalhada. |
| Namespace inválida | Uma namespace de identidade fornecida para uma ID de usuário era inválida. Consulte a seção sobre namespaces [de identidade](./api/appendix.md#standard-namespaces) padrão no apêndice do guia do [!DNL Privacy Service] desenvolvedor para obter uma lista de namespaces aceitas. Se estiver usando uma namespace personalizada, certifique-se de que está configurando a propriedade da ID como &quot; `type` personalizada&quot;. |
| Parcialmente concluído | A tarefa foi concluída com êxito, mas alguns dados não eram aplicáveis à solicitação e foram ignorados. |
| Os dados não estão no formato necessário. | Um ou mais valores de dados para o aplicativo especificado foram formatados incorretamente. Verifique os detalhes do trabalho para obter mais informações. |
| A Organização IMS não foi provisionada. | Esta mensagem ocorre quando a sua Organização IMS não foi provisionada para [!DNL Privacy Service]. Entre em contato com o administrador para obter mais informações. |
| O acesso e as permissões são necessários. | O acesso e as permissões são necessários para o uso [!DNL Privacy Service]. Entre em contato com o administrador para obter acesso. |
| Ocorreu um problema ao carregar e arquivar os dados de acesso. | Quando esse erro ocorrer, carregue novamente os dados de acesso e tente novamente. |
| A carga de trabalho foi excedida para o limite de taxa de documento atual. | Quando este erro ocorrer, reduza a taxa de envio e tente novamente. |