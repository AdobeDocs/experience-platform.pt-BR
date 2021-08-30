---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Guia da API do Privacy Service
description: A API do Privacy Service permite que os desenvolvedores criem e gerenciem solicitações de clientes para acessar ou excluir seus dados pessoais em aplicativos do Experience Cloud, em conformidade com as regulamentações legais de privacidade. Siga este manual para saber como executar operações importantes usando a API.
topic-legacy: developer guide
exl-id: c1d05e30-ef8f-4adf-87e0-1d6e3e9e9f9e
source-git-commit: 8133804076b1c0adf2eae5b748e86a35f3186d14
workflow-type: tm+mt
source-wordcount: '787'
ht-degree: 16%

---

# [!DNL Privacy Service] Manual da API

O Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e a interface do usuário que permitem gerenciar (acessar e excluir) os dados pessoais dos titulares de dados (clientes) nos aplicativos Adobe Experience Cloud. [!DNL Privacy Service] O também fornece um mecanismo central de auditoria e registro que permite acessar o status e os resultados de tarefas envolvendo  [!DNL Experience Cloud] aplicativos.

Este guia aborda como usar a API [!DNL Privacy Service]. Para obter detalhes sobre como usar a interface do usuário, consulte a [Visão geral da interface do usuário do Privacy Service](../ui/overview.md). Para obter uma lista abrangente de todos os endpoints disponíveis na API [!DNL Privacy Service], consulte a [Referência da API](https://www.adobe.io/experience-platform-apis/references/privacy-service/).

## Introdução {#getting-started}

Este guia requer um entendimento prático dos seguintes recursos [!DNL Experience Platform]:

* [[!DNL Privacy Service]](../home.md): Fornece uma RESTful API e interface do usuário que permitem gerenciar solicitações de acesso e exclusão de titulares de dados (clientes) em aplicativos Adobe Experience Cloud.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas com êxito para a API do Privacy Service.

### Lendo exemplos de chamadas de API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações do . Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de exemplo retornado nas respostas da API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de exemplo, consulte a seção sobre [como ler chamadas de API de exemplo](../../landing/troubleshooting.md) no [!DNL Experience Platform] guia de solução de problemas.

## Coletar valores para cabeçalhos necessários

Para fazer chamadas para a API [!DNL Privacy Service], primeiro você deve coletar suas credenciais de acesso para serem usadas nos cabeçalhos necessários:

* `Authorization: Bearer {ACCESS_TOKEN}`
* `x-api-key: {API_KEY}`
* `x-gw-ims-org-id: {IMS_ORG}`

Isso envolve obter permissões de desenvolvedor para [!DNL Experience Platform] no Adobe Admin Console e gerar as credenciais no Console do Desenvolvedor do Adobe.

### Obter acesso de desenvolvedor a [!DNL Experience Platform]

Para obter acesso de desenvolvedor a [!DNL Platform], siga as etapas iniciais no [tutorial de autenticação do Experience Platform](https://www.adobe.com/go/platform-api-authentication-en). Depois de chegar à etapa &quot;Gerar credenciais de acesso no Console do Desenvolvedor do Adobe&quot;, retorne a este tutorial para gerar as credenciais específicas para [!DNL Privacy Service].

### Gerar credenciais de acesso

Usando o Adobe Developer Console, você deve gerar as três credenciais de acesso descritas a seguir:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Seu `{IMS_ORG}` e `{API_KEY}` precisam ser gerados apenas uma vez e podem ser reutilizados em futuras chamadas de API. No entanto, seu `{ACCESS_TOKEN}` é temporário e deve ser gerado novamente a cada 24 horas.

As etapas de geração desses valores são descritas em detalhes abaixo.

#### Configuração única

Acesse o [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e faça logon com seu Adobe ID. Em seguida, siga as etapas descritas no tutorial em [criar um projeto vazio](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) na documentação do Console do desenvolvedor do Adobe.

Depois de criar um novo projeto, selecione **[!UICONTROL Adicionar API]** na tela **[!UICONTROL Visão geral do projeto]**.

![](../images/api/getting-started/add-api-button.png)

A tela **[!UICONTROL Adicionar uma API]** é exibida. Selecione **[!UICONTROL Privacy Service API]** na lista de APIs disponíveis antes de selecionar **[!UICONTROL Next]**.

![](../images/api/getting-started/add-privacy-service-api.png)

A tela **[!UICONTROL Configurar API]** é exibida. Selecione a opção **[!UICONTROL Generate a key pair]** e selecione **[!UICONTROL Generate keypair]** no canto inferior direito.

![](../images/api/getting-started/generate-key-pair.png)

O par de chaves é gerado automaticamente e um arquivo ZIP contendo uma chave privada e um certificado público é baixado no computador local (para ser usado em uma etapa posterior). Selecione **[!UICONTROL Salvar API configurada]** para concluir a configuração.

![](../images/api/getting-started/key-pair-generated.png)

Depois que a API for adicionada ao projeto, a página do projeto será exibida novamente na página **Visão geral da API do Privacy Service**. Daqui, role para baixo até a seção **[!UICONTROL Conta de Serviço (JWT)]**, que fornece as seguintes credenciais de acesso necessárias em todas as chamadas à API do [!DNL Privacy Service]

* **[!UICONTROL ID]** DO CLIENTE: A ID do cliente é o necessário  `{API_KEY}` para que o possa ser fornecido no cabeçalho x-api-key.
* **[!UICONTROL ID]** DA ORGANIZAÇÃO: A ID da organização é o  `{IMS_ORG}` valor que deve ser usado no cabeçalho x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autenticação para cada sessão

A credencial final necessária que você deve coletar é seu `{ACCESS_TOKEN}`, que é usado no cabeçalho da Autorização. Ao contrário dos valores para `{API_KEY}` e `{IMS_ORG}`, um novo token deve ser gerado a cada 24 horas para continuar usando [!DNL Platform] APIs.

Para gerar um novo `{ACCESS_TOKEN}`, abra a chave privada baixada anteriormente e cole seu conteúdo na caixa de texto ao lado de **[!UICONTROL Generate access token]** antes de selecionar **[!UICONTROL Generate Token]**.

![](../images/api/getting-started/paste-private-key.png)

É gerado um novo token de acesso, e é fornecido um botão para copiá-lo para a área de transferência. Esse valor é usado para o cabeçalho de Autorização necessário e deve ser fornecido no formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Próximas etapas

Agora que você sabe quais cabeçalhos usar, está pronto para começar a fazer chamadas para a API [!DNL Privacy Service]. O documento em [tarefas de privacidade](privacy-jobs.md) aborda as várias chamadas de API que você pode fazer usando a API [!DNL Privacy Service]. Cada chamada de exemplo inclui o formato da API geral, uma solicitação de amostra que mostra os cabeçalhos necessários e uma resposta de amostra.
