---
keywords: Experience Platform, home, tópicos populares, ECID, ecid
solution: Experience Platform
title: Dados de identidade para solicitações de privacidade
topic-legacy: overview
description: Este documento fornece orientação geral sobre como configurar suas operações de dados e aproveitar as tecnologias do Adobe para recuperar efetivamente as informações de identidade apropriadas para solicitações de privacidade do cliente.
exl-id: 43b0292a-ea4d-4858-b584-ba71029724f6
source-git-commit: 82dea48c732b3ddea957511c22f90bbd032ed9b7
workflow-type: tm+mt
source-wordcount: '646'
ht-degree: 2%

---

# Dados de identidade para solicitações de privacidade

Para o Adobe Experience Platform [!DNL Privacy Service] para processar as solicitações do cliente para seus dados privados (incluindo solicitações de acesso, exclusão ou recusa de venda), ele deve ser fornecido com identificadores exclusivos que vinculam um cliente específico aos dados privados armazenados em seus aplicativos habilitados para a Adobe Experience Cloud. [!DNL Privacy Service] em seguida, usa esses identificadores para coletar todos os dados armazenados sob a identidade do cliente em [!DNL Experience Cloud]e processá-lo de acordo com a solicitação do cliente.

Este documento fornece orientação geral sobre como configurar suas operações de dados e aproveitar as tecnologias do Adobe para recuperar efetivamente as informações de identidade apropriadas para solicitações de privacidade do cliente.

## Identidades e namespaces

Quando um cliente pode interagir com sua marca por meio de vários canais diferentes, pode ser desafiador reconciliar os identificadores diferentes que são registrados a partir dessas muitas interações. Isso, por sua vez, pode dificultar a determinação de quais dados pertencem a uma determinada pessoa em seu [!DNL Experience Cloud] aplicativos.

Por exemplo, ao manipular solicitações de dados do cliente em [!DNL Privacy Service], uma identidade pode representar um valor de cookie definido em um domínio controlado por Adobe, um valor de cookie em um domínio de terceiros e compartilhado com o Adobe ou um identificador personalizado que você define explicitamente na organização IMS.

Por conseguinte, é necessário que cada identidade seja enviada para [!DNL Privacy Service] é acompanhada de um namespace que fornece contexto ao relacionar o valor de identidade com seu sistema de origem. Um namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma Adobe Advertising Cloud ID (&quot;AdCloud&quot;) ou Adobe Target ID (&quot;TNTID&quot;).

O Adobe Experience Platform Identity Service mantém um armazenamento de namespaces de identidade definidos globalmente e pelo usuário. Para obter informações mais detalhadas sobre namespaces, consulte o [visão geral do namespace de identidade](../identity-service/namespaces.md). Para obter uma lista de namespaces padrão e qualificadores de namespace que são comumente usados em [!DNL Privacy Service], consulte o [seção apêndice](api/appendix.md) no guia da API.

## ECID e serviço de Opt-in

Adobe Experience Cloud [!DNL Identity Service] constitui um quadro comum de identificação para [!DNL Experience Cloud]e atribui uma ID exclusiva e persistente para cada visitante do site. O [!DNL Experience Cloud] A ID (ECID) rastreia a atividade de um cliente por meio do uso de um cookie primário, pode identificar um dispositivo de maneira exclusiva em vários aplicativos e permite identificar o mesmo visitante do site e seus dados em diferentes [!DNL Experience Cloud] aplicativos. Consulte a [Visão geral do serviço de identidade do Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) para obter mais informações.

Serviço de Opt-in, uma extensão do [!DNL Experience Cloud Identity Service], permite que você configure protocolos em seu aplicativo para permitir que os visitantes determinem se você pode definir um cookie no dispositivo ou no navegador do visitante. Para obter informações mais detalhadas sobre o Serviço de Opt-in, incluindo como configurar o serviço para seu aplicativo, consulte [Documentação do serviço de Opt-in](https://experienceleague.adobe.com/docs/id-service/using/implementation/opt-in-service/optin-overview.html?lang=pt-BR).

Depois que os visitantes do site receberem ECIDs, você poderá utilizar o Adobe [!DNL Privacy JavaScript Library] para recuperar essas IDs para uso em solicitações de privacidade, conforme descrito na próxima seção.

## [!DNL Privacy JS Library]

O [!DNL Adobe Privacy JavaScript Library] O fornece várias funções que permitem recuperar e remover identidades de cliente armazenadas no navegador. A biblioteca pode ser configurada para recuperar informações de identidade de vários aplicativos Adobe, incluindo ECID. Por meio do uso de retornos de chamada ou promessas, é possível manipular programaticamente as IDs recuperadas com êxito e enviá-las para a [!DNL Privacy Service] API.

Para obter mais informações sobre [!DNL Privacy JS Library], incluindo amostras de código para vários casos de uso comuns, consulte [Visão geral da biblioteca JS de privacidade](js-library.md).

## Próximas etapas

Este documento forneceu uma breve visão geral dos conceitos centrais envolvidos na recuperação de dados de identidade do cliente para uso em solicitações de privacidade. É recomendável revisar os links de documentação fornecidos em cada seção para obter informações mais detalhadas sobre esses conceitos e serviços. Para obter etapas sobre como enviar IDs recuperadas para o [!DNL Privacy Service] para criar solicitações de acesso, exclusão ou recusa de venda, consulte o [Guia da API do Privacy Service](api/overview.md).
