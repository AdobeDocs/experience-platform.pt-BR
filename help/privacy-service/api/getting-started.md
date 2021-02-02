---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Guia do desenvolvedor do Privacy Service
description: Use a RESTful API para gerenciar os dados pessoais de seus participantes de dados em aplicativos Adobe Experience Cloud
topic: developer guide
translation-type: tm+mt
source-git-commit: 5d1b22253f2b382bef83e30a4295218ba6b85331
workflow-type: tm+mt
source-wordcount: '771'
ht-degree: 0%

---


# [!DNL Privacy Service] guia do desenvolvedor

A Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface de usuário que permitem gerenciar (acessar e excluir) os dados pessoais de seus sujeitos de dados (clientes) em todos os aplicativos Adobe Experience Cloud. [!DNL Privacy Service] também fornece um mecanismo central de auditoria e registro que permite acessar o status e os resultados de trabalhos que envolvem  [!DNL Experience Cloud] aplicativos.

Este guia aborda como usar a API [!DNL Privacy Service]. Para obter detalhes sobre como usar a interface do usuário, consulte a [visão geral da interface do Privacy Service](../ui/overview.md). Para obter uma lista abrangente de todos os pontos de extremidade disponíveis na API [!DNL Privacy Service], consulte a [referência da API](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml).

## Introdução {#getting-started}

Este guia exige um entendimento prático dos seguintes recursos [!DNL Experience Platform]:

* [[!DNL Privacy Service]](../home.md): Fornece uma API RESTful e uma interface de usuário que permite gerenciar o acesso e a exclusão de solicitações de seus participantes de dados (clientes) em aplicativos Adobe Experience Cloud.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas bem-sucedidas para a API do Privacy Service.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção em [como ler chamadas de API de exemplo](../../landing/troubleshooting.md) no guia de solução de problemas [!DNL Experience Platform].

## Reunir valores para cabeçalhos necessários

Para fazer chamadas para a API [!DNL Privacy Service], primeiro você deve coletar suas credenciais de acesso para serem usadas nos cabeçalhos necessários:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Isso envolve obter permissões de desenvolvedor para [!DNL Experience Platform] no Adobe Admin Console e gerar as credenciais no Adobe Developer Console.

### Obtenha acesso de desenvolvedor a [!DNL Experience Platform]

Para obter acesso do desenvolvedor a [!DNL Platform], siga as etapas iniciais no [tutorial de autenticação do Experience Platform](https://www.adobe.com/go/platform-api-authentication-en). Quando você chegar à etapa &quot;Gerar credenciais de acesso no Console do desenvolvedor do Adobe&quot;, volte a este tutorial para gerar as credenciais específicas para [!DNL Privacy Service].

### Gerar credenciais de acesso

Usando o Console do desenvolvedor do Adobe, você deve gerar as três credenciais de acesso a seguir:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Seus `{IMS_ORG}` e `{API_KEY}` precisam ser gerados apenas uma vez e podem ser reutilizados em futuras chamadas de API. No entanto, seu `{ACCESS_TOKEN}` é temporário e deve ser regenerado a cada 24 horas.

As etapas para gerar esses valores são abordadas em detalhes abaixo.

#### Configuração única

Vá para [Console do desenvolvedor do Adobe](https://www.adobe.com/go/devs_console_ui) e faça logon com seu Adobe ID. Em seguida, siga as etapas descritas no tutorial em [criar um projeto vazio](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) na documentação do Console do desenvolvedor do Adobe.

Depois de criar um novo projeto, selecione **[!UICONTROL Adicionar API]** na tela **[!UICONTROL Visão geral do projeto]**.

![](../images/api/getting-started/add-api-button.png)

A tela **[!UICONTROL Adicionar uma API]** é exibida. Selecione **[!UICONTROL API Privacy Service]** na lista de APIs disponíveis antes de selecionar **[!UICONTROL Next]**.

![](../images/api/getting-started/add-privacy-service-api.png)

A tela **[!UICONTROL Configurar API]** é exibida. Selecione a opção para **[!UICONTROL Gerar um par de teclas]** e selecione **[!UICONTROL Gerar par de teclas]** no canto inferior direito.

![](../images/api/getting-started/generate-key-pair.png)

O par de chaves é gerado automaticamente e um arquivo ZIP contendo uma chave privada e um certificado público é baixado para o computador local (para ser usado em uma etapa posterior). Selecione **[!UICONTROL Salvar a API configurada]** para concluir a configuração.

![](../images/api/getting-started/key-pair-generated.png)

Depois que a API for adicionada ao projeto, a página do projeto será exibida novamente na página **Visão geral da API de Privacy Service**. Aqui, role para baixo até a seção **[!UICONTROL Conta de Serviço (JWT)]**, que fornece as seguintes credenciais de acesso necessárias em todas as chamadas para a API [!DNL Privacy Service]:

* **[!UICONTROL ID]** DO CLIENTE: A ID do cliente é a necessária  `{API_KEY}` para isso, que deve ser fornecida no cabeçalho x-api-key.
* **[!UICONTROL ID]** DA ORGANIZAÇÃO: A ID da organização é o  `{IMS_ORG}` valor que deve ser usado no cabeçalho x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autenticação para cada sessão

A credencial final necessária que você deve coletar é seu `{ACCESS_TOKEN}`, que é usado no cabeçalho de Autorização. Ao contrário dos valores para `{API_KEY}` e `{IMS_ORG}`, um novo token deve ser gerado a cada 24 horas para continuar usando [!DNL Platform] APIs.

Para gerar um novo `{ACCESS_TOKEN}`, abra a chave privada baixada anteriormente e cole seu conteúdo na caixa de texto ao lado de **[!UICONTROL Gerar token de acesso]** antes de selecionar **[!UICONTROL Gerar token]**.

![](../images/api/getting-started/paste-private-key.png)

Um novo token de acesso é gerado e um botão para copiar o token na área de transferência é fornecido. Esse valor é usado para o cabeçalho de Autorização necessário e deve ser fornecido no formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Próximas etapas

Agora que você entende quais cabeçalhos devem ser usados, você está pronto para começar a fazer chamadas para a API [!DNL Privacy Service]. O documento em [tarefas de privacidade](privacy-jobs.md) percorre as várias chamadas de API que você pode fazer usando a API [!DNL Privacy Service]. Cada chamada de exemplo inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.
