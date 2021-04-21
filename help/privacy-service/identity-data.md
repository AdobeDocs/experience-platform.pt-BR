---
keywords: Experience Platform, home, tópicos populares, ECID, ecid
solution: Experience Platform
title: Dados de identidade para solicitações de privacidade
topic-legacy: overview
description: Este documento fornece orientação geral sobre como configurar suas operações de dados e aproveitar as tecnologias do Adobe para recuperar efetivamente as informações de identidade apropriadas para solicitações de privacidade do cliente.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '650'
ht-degree: 3%

---

# Dados de identidade para solicitações de privacidade

Para que o Adobe Experience Platform [!DNL Privacy Service] processe solicitações de clientes para seus dados privados (incluindo solicitações de acesso, exclusão ou recusa de venda), ele deve ser fornecido com identificadores exclusivos que vinculam um cliente específico aos dados privados armazenados em seus aplicativos habilitados para Adobe Experience Cloud. [!DNL Privacy Service] em seguida, usa esses identificadores para coletar todos os dados armazenados sob a identidade do cliente no  [!DNL Experience Cloud] e processá-los de acordo com a solicitação do cliente.

Este documento fornece orientação geral sobre como configurar suas operações de dados e aproveitar as tecnologias do Adobe para recuperar efetivamente as informações de identidade apropriadas para solicitações de privacidade do cliente.

## Identidades e namespaces

Quando um cliente pode interagir com sua marca por meio de vários canais diferentes, pode ser desafiador reconciliar os identificadores diferentes que são registrados a partir dessas muitas interações. Isso, por sua vez, pode dificultar a determinação de quais dados pertencem a uma determinada pessoa em seus aplicativos [!DNL Experience Cloud].

Por exemplo, ao manipular solicitações de dados do cliente em [!DNL Privacy Service], uma identidade pode representar um valor de cookie definido em um domínio controlado por Adobe, um valor de cookie em um domínio de terceiros e compartilhado com o Adobe ou um identificador personalizado que você define explicitamente em sua Organização IMS.

Portanto, é necessário que cada identidade enviada para [!DNL Privacy Service] seja acompanhada de um namespace que forneça contexto relacionando o valor de identidade com seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Adobe Experience Platform Identity Service mantém um armazenamento de namespaces de identidade definidos globalmente e pelo usuário. Para obter informações mais detalhadas sobre namespaces, consulte a [visão geral do namespace de identidade](../identity-service/namespaces.md). Para obter uma lista de namespaces e qualificadores de namespace padrão que são usados em [!DNL Privacy Service], consulte a [seção do apêndice](api/appendix.md) no guia do desenvolvedor.

## ECID e serviço de Opt-in

O Adobe Experience Cloud [!DNL Identity Service] serve como uma estrutura de identificação comum para [!DNL Experience Cloud] e atribui uma ID exclusiva e persistente para cada visitante do site. A [!DNL Experience Cloud] ID (ECID) rastreia a atividade de um cliente por meio do uso de um cookie primário, pode identificar exclusivamente um dispositivo em vários aplicativos e permite identificar o mesmo visitante do site e seus dados em diferentes aplicativos [!DNL Experience Cloud]. Consulte a [Visão geral do serviço de identidade do Experience Cloud](https://docs.adobe.com/content/help/pt-BR/id-service/using/intro/overview.html) para obter mais informações.

O Serviço de Opt-in, uma extensão de [!DNL Experience Cloud Identity Service], permite configurar protocolos no aplicativo para permitir que os visitantes determinem se você pode definir um cookie no dispositivo ou no navegador do visitante. Para obter informações mais detalhadas sobre o Serviço de Opt-in, incluindo como configurar o serviço para seu aplicativo, consulte a [documentação do Serviço de Opt-in](https://docs.adobe.com/content/help/pt-BR/id-service/using/implementation/opt-in-service/optin-overview.html).

Depois que os visitantes do site receberem ECIDs, você poderá utilizar o Adobe [!DNL Privacy JavaScript Library] para recuperar essas IDs para uso em solicitações de privacidade, conforme descrito na próxima seção.

## [!DNL Privacy JS Library]

O [!DNL Adobe Privacy JavaScript Library] fornece várias funções que permitem recuperar e remover identidades de cliente armazenadas no navegador. A biblioteca pode ser configurada para recuperar informações de identidade de vários aplicativos Adobe, incluindo ECID. Por meio do uso de retornos de chamada ou promessas, é possível manipular programaticamente as IDs recuperadas com êxito e enviá-las para a API [!DNL Privacy Service].

Para obter mais informações sobre [!DNL Privacy JS Library], incluindo amostras de código para vários casos de uso comuns, consulte a [Visão geral da biblioteca JS de privacidade](js-library.md).

## Próximas etapas

Este documento forneceu uma breve visão geral dos conceitos centrais envolvidos na recuperação de dados de identidade do cliente para uso em solicitações de privacidade. É recomendável revisar os links de documentação fornecidos em cada seção para obter informações mais detalhadas sobre esses conceitos e serviços. Para obter etapas sobre como enviar IDs recuperadas para [!DNL Privacy Service] para criar solicitações de acesso, exclusão ou recusa de venda, consulte o [Guia do desenvolvedor do Privacy Service](api/getting-started.md).
