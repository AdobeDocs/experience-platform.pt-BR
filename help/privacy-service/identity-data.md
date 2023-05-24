---
keywords: Experience Platform;página inicial;tópicos populares;ECID;ecid
solution: Experience Platform
title: Dados de identidade para solicitações de privacidade
description: Este documento fornece orientação geral sobre como configurar as operações de dados e aproveitar as tecnologias Adobe para recuperar efetivamente as informações de identidade apropriadas para as solicitações de privacidade do cliente.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '645'
ht-degree: 2%

---

# Dados de identidade para solicitações de privacidade

Para o Adobe Experience Platform [!DNL Privacy Service] para processar as solicitações do cliente para seus dados privados (incluindo solicitações de acesso, exclusão ou recusa de venda), eles devem receber identificadores exclusivos que vinculam um cliente específico aos seus dados privados armazenados em seus aplicativos habilitados para Adobe Experience Cloud. [!DNL Privacy Service] O usa esses identificadores para coletar todos os dados armazenados na identidade do cliente no [!DNL Experience Cloud]e processá-lo de acordo com a solicitação do cliente.

Este documento fornece orientação geral sobre como configurar as operações de dados e aproveitar as tecnologias Adobe para recuperar efetivamente as informações de identidade apropriadas para as solicitações de privacidade do cliente.

## Identidades e namespaces

Quando um cliente pode interagir com sua marca por vários canais diferentes, pode ser desafiador reconciliar os identificadores diferentes que são registrados a partir dessas muitas interações. Isso, por sua vez, pode dificultar a determinação de quais dados pertencem a uma pessoa específica em seu [!DNL Experience Cloud] aplicativos.

Por exemplo, ao manipular solicitações de dados do cliente no [!DNL Privacy Service], uma identidade pode representar um valor de cookie definido em um domínio controlado por Adobe, um valor de cookie em um domínio de terceiros e compartilhado com o Adobe ou um identificador personalizado definido explicitamente na organização.

Por conseguinte, exige-se que cada identidade enviada [!DNL Privacy Service] é acompanhado de um namespace que fornece contexto ao relacionar o valor de identidade ao seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Adobe Experience Platform Identity Service mantém um armazenamento de namespaces de identidade definidos globalmente e pelo usuário. Para obter informações mais detalhadas sobre namespaces, consulte o [visão geral do namespace de identidade](../identity-service/namespaces.md). Para obter uma lista de namespaces padrão e qualificadores de namespace que são comumente usados em [!DNL Privacy Service], consulte o [seção apêndice](api/appendix.md) no guia da API.

## ECID e serviço de Opt-in

Adobe Experience Cloud [!DNL Identity Service] constitui um quadro de identificação comum para os [!DNL Experience Cloud]e atribui uma ID exclusiva e contínua a cada visitante do site. A variável [!DNL Experience Cloud] A ID (ECID) rastreia a atividade de um cliente por meio do uso de um cookie próprio, pode identificar exclusivamente um dispositivo em vários aplicativos e permite identificar o mesmo visitante do site e seus dados em diferentes [!DNL Experience Cloud] aplicativos. Consulte a [Visão geral do serviço de identidade do Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) para obter mais informações.

Serviço de Opt-in, uma extensão do [!DNL Experience Cloud Identity Service], permite que você configure protocolos em seu aplicativo para que os visitantes determinem se você pode adicionar um cookie no dispositivo ou no navegador do visitante. Para obter informações mais detalhadas sobre o serviço de Opt-in, incluindo como configurar o serviço para seu aplicativo, consulte [Documentação do serviço de Opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=pt-BR).

Depois que os visitantes do site tiverem recebido ECIDs, você poderá utilizar o Adobe [!DNL Privacy JavaScript Library] para recuperar essas IDs para uso em solicitações de privacidade, conforme descrito na próxima seção.

## [!DNL Privacy JS Library]

A variável [!DNL Adobe Privacy JavaScript Library] O fornece várias funções que permitem recuperar e remover as identidades do cliente armazenadas no navegador. A biblioteca pode ser configurada para recuperar informações de identidade de vários aplicativos Adobe, incluindo ECID. Com o uso de retornos de chamada ou promessas, é possível manipular programaticamente as IDs recuperadas com êxito e enviá-las para a [!DNL Privacy Service] API.

Para obter mais informações sobre [!DNL Privacy JS Library], incluindo amostras de código para vários casos de uso comuns, consulte o [Visão geral da biblioteca JS de privacidade](js-library.md).

## Próximas etapas

Este documento forneceu uma breve visão geral dos conceitos centrais envolvidos na recuperação de dados de identidade do cliente para uso em solicitações de privacidade. É recomendável revisar os links de documentação fornecidos em cada seção para obter informações mais detalhadas sobre esses conceitos e serviços. Para obter etapas sobre como enviar IDs recuperadas para o [!DNL Privacy Service] para criar solicitações de acesso, exclusão ou cancelamento de venda, consulte o [Guia da API do Privacy Service](api/overview.md).
