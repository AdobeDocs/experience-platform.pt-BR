---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Dados de identidade para solicitações de privacidade
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '616'
ht-degree: 3%

---


# Dados de identidade para solicitações de privacidade

Para que a Adobe Experience Platform [!DNL Privacy Service] processe solicitações de clientes de seus dados privados (incluindo solicitações de acesso, exclusão ou cancelamento de vendas), ela deve ser fornecida com identificadores exclusivos que vinculam um cliente específico aos dados privados armazenados em seus aplicativos habilitados pela Adobe Experience Cloud. [!DNL Privacy Service] em seguida, usa esses identificadores para coletar todos os dados armazenados sob a identidade do cliente dentro [!DNL Experience Cloud]e processá-los de acordo com a solicitação do cliente.

Este documento fornece orientações gerais sobre como configurar suas operações de dados e aproveitar as tecnologias da Adobe para recuperar efetivamente as informações de identidade apropriadas para as solicitações de privacidade do cliente.

## Identidades e namespaces

Quando um cliente pode interagir com sua marca através de vários canais diferentes, pode ser difícil reconciliar os identificadores diferentes que são registrados dessas muitas interações. Isso, por sua vez, pode tornar difícil determinar quais dados pertencem a uma pessoa específica em seus [!DNL Experience Cloud] aplicativos.

Por exemplo, ao lidar com solicitações de dados do cliente em [!DNL Privacy Service], uma identidade pode representar um valor de cookie definido em um domínio controlado pela Adobe, um valor de cookie em um domínio de terceiros e compartilhado com a Adobe ou um identificador personalizado que você define explicitamente na organização IMS.

Por conseguinte, é necessário que cada identidade enviada [!DNL Privacy Service] seja acompanhada de uma **namespace** que forneça o contexto, relacionando o valor de identificação com o seu sistema de origens. Uma namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma ID da Advertising Cloud da Adobe (&quot;AdCloud&quot;) ou uma ID da Adobe Target (&quot;TNTID&quot;).

O Adobe Experience Platform Identity Service mantém um armazenamento de namespaces de identidade definidas globalmente e definidas pelo usuário. Para obter informações mais detalhadas sobre namespaces, consulte a visão geral [da namespace de](../identity-service/namespaces.md)identidade. Para obter uma lista de qualificadores padrão de namespaces e namespaces comumente usados em [!DNL Privacy Service], consulte a seção [do](api/appendix.md) apêndice no guia do desenvolvedor.

## ECID e serviço de aceitação

A Adobe Experience Cloud [!DNL Identity Service] serve como uma estrutura de identificação comum para [!DNL Experience Cloud]e atribui uma ID exclusiva e persistente a cada visitante do site. A [!DNL Experience Cloud] ID (ECID) rastreia a atividade de um cliente por meio do uso de um cookie primário, pode identificar exclusivamente um dispositivo em vários aplicativos e permite identificar o mesmo visitante do site e seus dados em diferentes [!DNL Experience Cloud] aplicativos. See the [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/pt-BR/id-service/using/intro/overview.html) for more information.

O serviço de aceitação, uma extensão de [!DNL Experience Cloud Identity Service], permite que você configure protocolos em seu aplicativo para permitir que os visitantes determinem se você pode definir um cookie no dispositivo ou navegador do visitante. Para obter informações mais detalhadas sobre o serviço de aceitação, incluindo como configurar o serviço para seu aplicativo, consulte a documentação [do serviço de](https://docs.adobe.com/content/help/pt-BR/id-service/using/implementation/opt-in-service/optin-overview.html)aceitação.

Depois que os visitantes do site tiverem ECIDs atribuídas, você poderá utilizar a Adobe para recuperar essas IDs [!DNL Privacy JavaScript Library] para uso em solicitações de privacidade, conforme descrito na próxima seção.

## [!DNL Privacy JS Library]

O [!DNL Adobe Privacy JavaScript Library] fornece várias funções que permitem recuperar e remover identidades de clientes que estão armazenadas no navegador. A biblioteca pode ser configurada para recuperar informações de identidade de vários aplicativos da Adobe, incluindo ECID. Por meio do uso de retornos de chamada ou promessas, você pode manipular de forma programática as IDs recuperadas com êxito e enviá-las para a [!DNL Privacy Service] API.

Para obter mais informações sobre [!DNL Privacy JS Library], incluindo exemplos de código para vários casos de uso comuns, consulte a visão geral [da Biblioteca JS de](js-library.md)privacidade.

## Próximas etapas

Este documento forneceu uma breve visão geral dos conceitos centrais envolvidos na recuperação de dados de identidade do cliente para uso em solicitações de privacidade. É recomendável que você reveja os links de documentação fornecidos em cada seção para obter informações mais detalhadas sobre esses conceitos e serviços. Para obter etapas sobre como enviar IDs recuperadas [!DNL Privacy Service] para criação de solicitações de acesso, exclusão ou cancelamento de vendas, consulte o guia [do desenvolvedor do](api/getting-started.md)Privacy Service.