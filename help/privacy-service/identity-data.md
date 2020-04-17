---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Dados de identidade para solicitações de privacidade
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Dados de identidade para solicitações de privacidade

Para que o Adobe Experience Platform Privacy Service processe solicitações de clientes de seus dados privados (incluindo solicitações de acesso, exclusão ou cancelamento de vendas), ele deve ser fornecido com identificadores exclusivos que vinculam um cliente específico aos dados privados armazenados em seus aplicativos habilitados para a Adobe Experience Cloud. O Privacy Service usa esses identificadores para coletar todos os dados armazenados sob a identidade do cliente na Experience Cloud e processá-los de acordo com a solicitação do cliente.

Este documento fornece orientações gerais sobre como configurar suas operações de dados e aproveitar as tecnologias da Adobe para recuperar efetivamente as informações de identidade apropriadas para as solicitações de privacidade do cliente.

## Identidades e namespaces

Quando um cliente pode interagir com sua marca através de vários canais diferentes, pode ser difícil reconciliar os identificadores diferentes que são registrados dessas muitas interações. Isso, por sua vez, pode tornar difícil determinar quais dados pertencem a uma pessoa específica nos aplicativos da Experience Cloud.

Por exemplo, ao lidar com solicitações de dados do cliente no Privacy Service, uma identidade pode representar um valor de cookie definido em um domínio controlado pela Adobe, um valor de cookie em um domínio de terceiros e compartilhado com a Adobe ou um identificador personalizado que você define explicitamente em sua Organização IMS.

Por conseguinte, é necessário que cada identidade enviada ao Privacy Service seja acompanhada de uma **namespace** que forneça o contexto relacionando o valor de identidade ao seu sistema de origens. Uma namespace pode representar um conceito genérico, como um endereço de email (&quot;Email&quot;) ou associar a identidade a um aplicativo específico, como uma ID da Adobe Advertising Cloud (&quot;AdCloud&quot;) ou uma ID de Público alvo da Adobe (&quot;TNTID&quot;).

O Adobe Experience Platform Identity Service mantém um armazenamento de namespaces de identidade definidas globalmente e pelo usuário. Para obter informações mais detalhadas sobre namespaces, consulte a visão geral [da namespace de](../identity-service/namespaces.md)identidade. Para obter uma lista de qualificadores padrão de namespaces e namespaces que são comumente usados no Privacy Service, consulte a seção [de](api/appendix.md) apêndice no guia do desenvolvedor.

## ECID e serviço de aceitação

O Adobe Experience Cloud Identity Service serve como uma estrutura de identificação comum para a Experience Cloud e atribui uma ID exclusiva e persistente a cada visitante do site. A Experience Cloud ID (ECID) rastreia a atividade de um cliente por meio do uso de um cookie primário, pode identificar exclusivamente um dispositivo em vários aplicativos e permite identificar o mesmo visitante do site e seus dados em diferentes aplicativos da Experience Cloud. See the [Experience Cloud Identity Service overview](https://docs.adobe.com/content/help/pt-BR/id-service/using/intro/overview.html) for more information.

O Serviço de aceitação, uma extensão do Serviço de identidade da Experience Cloud, permite que você configure protocolos em seu aplicativo para permitir que os visitantes determinem se você pode definir um cookie no dispositivo ou no navegador do visitante. Para obter informações mais detalhadas sobre o serviço de aceitação, incluindo como configurar o serviço para seu aplicativo, consulte a documentação [do serviço de](https://docs.adobe.com/content/help/pt-BR/id-service/using/implementation/opt-in-service/optin-overview.html)aceitação.

Depois que os visitantes do site tiverem ECIDs atribuídas, você poderá utilizar a Biblioteca JavaScript de privacidade da Adobe para recuperar essas IDs para uso em solicitações de privacidade, conforme descrito na próxima seção.

## Biblioteca JS de privacidade

A Biblioteca JavaScript de privacidade da Adobe fornece várias funções que permitem recuperar e remover identidades de clientes armazenadas no navegador. A biblioteca pode ser configurada para recuperar informações de identidade de vários aplicativos da Adobe, incluindo ECID. Por meio do uso de retornos de chamada ou promessas, é possível manipular programaticamente as IDs recuperadas com êxito e enviá-las para a API do Privacy Service.

Para obter mais informações sobre a Biblioteca JS de privacidade, incluindo exemplos de código para vários casos de uso comuns, consulte a visão geral [da Biblioteca JS de](js-library.md)privacidade.

## Próximas etapas

Este documento forneceu uma breve visão geral dos conceitos centrais envolvidos na recuperação de dados de identidade do cliente para uso em solicitações de privacidade. É recomendável que você reveja os links de documentação fornecidos em cada seção para obter informações mais detalhadas sobre esses conceitos e serviços. Para obter etapas sobre como enviar IDs recuperadas para o Privacy Service para criar solicitações de acesso, exclusão ou cancelamento de venda, consulte o guia [](api/getting-started.md)do desenvolvedor do Privacy Service.