---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Guia do desenvolvedor do Privacy Service
description: Use a RESTful API para gerenciar os dados pessoais de seus participantes de dados em aplicativos Adobe Experience Cloud
topic: developer guide
translation-type: tm+mt
source-git-commit: 1b398e479137a12bcfc3208d37472aae3d6721e1
workflow-type: tm+mt
source-wordcount: '762'
ht-degree: 0%

---


# [!DNL Privacy Service] guia do desenvolvedor

A Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface de usuário que permite gerenciar (acessar e excluir) os dados pessoais de seus sujeitos de dados (clientes) nos aplicativos Adobe Experience Cloud. [!DNL Privacy Service] também fornece um mecanismo central de auditoria e registro que permite acessar o status e os resultados de trabalhos que envolvem [!DNL Experience Cloud] aplicativos.

Este guia aborda como usar a [!DNL Privacy Service] API. Para obter detalhes sobre como usar a interface do usuário, consulte a visão geral [da interface do](../ui/overview.md)Privacy Service. Para obter uma lista abrangente de todos os pontos de extremidade disponíveis na [!DNL Privacy Service] API, consulte a referência [da](https://www.adobe.io/apis/experiencecloud/gdpr/api-reference.html)API.

## Introdução {#getting-started}

Este guia exige um entendimento prático dos seguintes [!DNL Experience Platform] recursos:

* [[!DNL Privacy Service]](../home.md): Fornece uma API RESTful e uma interface de usuário que permite gerenciar o acesso e a exclusão de solicitações de seus participantes de dados (clientes) em aplicativos Adobe Experience Cloud.

As seções a seguir fornecem informações adicionais que você precisará saber para fazer chamadas bem-sucedidas para a API do Privacy Service.

### Lendo chamadas de exemplo da API

Este tutorial fornece exemplos de chamadas de API para demonstrar como formatar suas solicitações. Isso inclui caminhos, cabeçalhos necessários e cargas de solicitação formatadas corretamente. O JSON de amostra retornado em respostas de API também é fornecido. Para obter informações sobre as convenções usadas na documentação para chamadas de API de amostra, consulte a seção sobre [como ler chamadas](../../landing/troubleshooting.md) de API de exemplo no guia de [!DNL Experience Platform] solução de problemas.

## Reunir valores para cabeçalhos necessários

Para fazer chamadas para a [!DNL Privacy Service] API, primeiro você deve coletar suas credenciais de acesso para serem usadas nos cabeçalhos necessários:

* Autorização: Portador `{ACCESS_TOKEN}`
* x-api-key: `{API_KEY}`
* x-gw-ims-org-id: `{IMS_ORG}`

Isso envolve obter permissões de desenvolvedor para [!DNL Experience Platform] no Adobe Admin Console e gerar as credenciais no Adobe Developer Console.

### Obtenha acesso de desenvolvedor a [!DNL Experience Platform]

Para obter acesso do desenvolvedor ao [!DNL Platform], siga as etapas iniciais no tutorial [de autenticação do](../../tutorials/authentication.md)Experience Platform. Quando você chegar à etapa &quot;Gerar credenciais de acesso no Console do desenvolvedor do Adobe&quot;, retorne a este tutorial para gerar as credenciais específicas para [!DNL Privacy Service].

### Gerar credenciais de acesso

Usando o Console do desenvolvedor do Adobe, você deve gerar as três credenciais de acesso a seguir:

* `{IMS_ORG}`
* `{API_KEY}`
* `{ACCESS_TOKEN}`

Sua `{IMS_ORG}` e `{API_KEY}` só precisam ser geradas uma vez e podem ser reutilizadas em futuras chamadas de API. No entanto, o seu `{ACCESS_TOKEN}` é temporário e precisa ser regenerado a cada 24 horas.

As etapas para gerar esses valores são abordadas em detalhes abaixo.

#### Configuração única

Vá para o [Adobe Developer Console](https://www.adobe.com/go/devs_console_ui) e faça logon com seu Adobe ID. Em seguida, siga as etapas descritas no tutorial sobre como [criar um projeto](https://www.adobe.io/apis/experienceplatform/console/docs.html#!AdobeDocs/adobeio-console/master/projects-empty.md) vazio na documentação do Console do desenvolvedor do Adobe.

Depois de criar um novo projeto, clique em **[!UICONTROL Adicionar API]** na tela Visão geral _[!UICONTROL do]_ projeto.

![](../images/api/getting-started/add-api-button.png)

A tela _[!UICONTROL Adicionar uma API]_ é exibida. Selecione **[!UICONTROL Privacy Service API]** na lista de APIs disponíveis antes de clicar em **[!UICONTROL Avançar]**.

![](../images/api/getting-started/add-privacy-service-api.png)

A tela _[!UICONTROL Configure API (Configurar API]_ ) é exibida. Selecione a opção para **[!UICONTROL Gerar um par]** de teclas e clique em **[!UICONTROL Gerar um par]** de teclas no canto inferior direito.

![](../images/api/getting-started/generate-key-pair.png)

O par de chaves é gerado automaticamente e um arquivo ZIP contendo uma chave privada e um certificado público é baixado para o computador local (para ser usado em uma etapa posterior). Selecione **[!UICONTROL Salvar API]** configurada para concluir a configuração.

![](../images/api/getting-started/key-pair-generated.png)

Depois que a API for adicionada ao projeto, a página do projeto será exibida novamente na página de visão geral _da API do_ Privacy Service. Aqui, role para baixo até a seção _[!UICONTROL Service Account (JWT)]_ , que fornece as seguintes credenciais de acesso que são necessárias em todas as chamadas para a [!DNL Privacy Service] API:

* **[!UICONTROL ID]** DO CLIENTE: A ID do cliente é a necessária `{API_KEY}` para isso, que deve ser fornecida no cabeçalho x-api-key.
* **[!UICONTROL ID]** DA ORGANIZAÇÃO: A ID da organização é o `{IMS_ORG}` valor que deve ser usado no cabeçalho x-gw-ims-org-id.

![](../images/api/getting-started/jwt-credentials.png)

#### Autenticação para cada sessão

A credencial final necessária que você deve coletar é sua, `{ACCESS_TOKEN}`usada no cabeçalho Autorização. Diferentemente dos valores para `{API_KEY}` e `{IMS_ORG}`, um novo token deve ser gerado a cada 24 horas para continuar usando [!DNL Platform] APIs.

Para gerar uma nova `{ACCESS_TOKEN}`, abra a chave privada baixada anteriormente e cole seu conteúdo na caixa de texto ao lado de _[!UICONTROL Gerar token de acesso]_ antes de clicar em **[!UICONTROL Gerar token]**.

![](../images/api/getting-started/paste-private-key.png)

Um novo token de acesso é gerado e um botão para copiar o token na área de transferência é fornecido. Esse valor é usado para o cabeçalho de Autorização necessário e deve ser fornecido no formato `Bearer {ACCESS_TOKEN}`.

![](../images/api/getting-started/generated-access-token.png)

## Próximas etapas

Agora que você entende quais cabeçalhos devem ser usados, você está pronto para começar a fazer chamadas para a [!DNL Privacy Service] API. O documento em trabalhos [de](privacy-jobs.md) privacidade percorre as várias chamadas de API que você pode fazer usando a [!DNL Privacy Service] API. Cada chamada de exemplo inclui o formato de API geral, uma solicitação de amostra mostrando os cabeçalhos necessários e uma resposta de amostra.
