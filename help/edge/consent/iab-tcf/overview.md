---
title: Suporte à TCF 2.0 do IAB no SDK da Web da Adobe Experience Platform
description: Saiba como oferecer suporte às preferências de consentimento do TCF 2.0 do IAB usando o SDK da Web da Adobe Experience Platform
keywords: consentimento; setConsent; grupo de campo de privacidade do perfil; grupo de campo de privacidade do evento de experiência; grupo de campo de privacidade; IAB TCF 2.0; CDP em tempo real; Perfil de dados do cliente em tempo real
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: da7696d288543abd21ff8a1402e81dcea32efbc2
workflow-type: tm+mt
source-wordcount: '879'
ht-degree: 0%

---

# Suporte à TCF 2.0 do IAB no SDK da Web da Adobe Experience Platform

O SDK da Web da Adobe Experience Platform tem suporte para a Estrutura de transparência e consentimento do Interative Advertising Bureau, versão 2.0 (TCF do IAB 2.0). Este guia mostra os requisitos para oferecer suporte ao IAB TCF 2.0 por meio do Adobe Experience Platform Web SDK, integrando-o à Plataforma de dados do cliente em tempo real, ao Audience Manager, aos Eventos de experiência, ao Adobe Analytics e ao Experience Edge.

Além disso, os guias a seguir estão disponíveis para ajudar no aprendizado de como integrar a TCF do IAB 2.0 com e sem a Adobe Experience Platform Launch.

- [Com Adobe Experience Platform Launch](./with-launch.md)
- [Sem Adobe Experience Platform Launch](./without-launch.md)

## Introdução

Para implementar o SDK da Web com o IAB TCF 2.0, você deve ter uma compreensão funcional do Experience Data Model (XDM) e dos Experience Events. Antes de começar, reveja o seguinte documento:

- [Visão geral](../../../xdm/home.md) do sistema do Experience Data Model (XDM): A padronização e a interoperabilidade são conceitos-chave por trás do Adobe Experience Platform. [!DNL Experience Data Model (XDM)], impulsionada pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

## integração Experience Platform

Para enviar dados de consentimento ao Adobe Experience Platform usando o SDK, o seguinte é obrigatório:

- Um conjunto de dados cujo esquema se baseia na classe [!DNL XDM Individual Profile] e contém campos de consentimento TCF 2.0, habilitados para uso em [!DNL Real-time Customer Profile].
- Um conjunto de dados configurado com a Platform e o conjunto de dados habilitado para perfil mencionado acima.

Consulte o guia em [TCF 2.0 Compliance](../../../landing/governance-privacy-security/consent/iab/overview.md) para obter instruções sobre como criar os conjuntos de dados e o conjunto de dados necessários.

## integração Audience Manager

O Adobe Audience Manager (AAM) inclui suporte para IAB TCF 2.0, que permite avaliar, honrar e encaminhar as opções de privacidade do cliente para parceiros downstream. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Para integrar com o Audience Manager por meio do SDK da Web da Adobe Experience Platform, verifique se você tem um conjunto de dados configurado para encaminhar para o Adobe Audience Manager.

## Integração entre Experience Events e Adobe Analytics

Enquanto a CDP em tempo real e os públicos-alvo do Audience Manager monitoram as preferências de consentimento atuais de um cliente, os Eventos de experiência podem reter as preferências de consentimento do cliente que estavam ativas quando o evento foi coletado.

Para coletar informações de consentimento sobre eventos, é necessário o seguinte:

- Um conjunto de dados com base na classe [!DNL XDM Experience Event], com o grupo de campos de esquema de privacidade [!DNL Experience Event].
- Um conjunto de dados configurado com o conjunto de dados [!DNL XDM Experience Event] acima.

Para obter mais informações sobre como converter um evento de experiência XDM em uma ocorrência do Analytics, comece lendo a documentação de [Visão geral do Analytics](../../data-collection/adobe-analytics/analytics-overview.md).

## Integração do SDK da Web da Adobe Experience Platform

As seções abaixo descrevem os principais pontos de integração entre o IAB TCF 2.0 e o Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Mesmo sem a CDP em tempo real ou a configuração do Audience Manager, ainda é possível integrar a TCF do IAB 2.0 ao SDK da Web. As preferências de consentimento podem ser usadas para controlar a coleção de Eventos de experiência e definir um cookie de identidade.

### Consentimento padrão

O consentimento padrão é usado quando não há preferência de consentimento já salva para um cliente. Isso significa que as opções de consentimento padrão podem controlar o comportamento do SDK da Web da Adobe Experience Platform e alterar com base na região de um cliente.

Por exemplo, se você tem um cliente que não está sob a jurisdição do Regulamento Geral sobre a Proteção de Dados (GDPR), o consentimento padrão pode ser definido como `in`, mas dentro da jurisdição do GDPR, o consentimento padrão pode ser definido como `pending`. Sua Plataforma de gerenciamento de consentimento (CMP) pode detectar a região do cliente e fornecer o sinalizador `gdprApplies` para IAB TCF 2.0. Esse sinalizador pode ser usado para definir o consentimento padrão.

Para obter mais informações sobre o consentimento padrão, consulte a [seção de consentimento padrão](../../fundamentals/configuring-the-sdk.md#default-consent) na documentação de configuração do SDK.

### Definir o consentimento quando ele for alterado

O SDK da Web da Adobe Experience Platform tem um comando `setConsent`, que comunica as preferências de consentimento do cliente a todos os serviços do Adobe usando o IAB TCF 2.0. Se estiver integrando com o Real-time CDP, isso atualizará o perfil do cliente. Se estiver integrando com o Audience Manager, isso atualizará as informações do cliente. Chamar isso também define um cookie com uma preferência de consentimento tudo ou nada que controla se os Eventos de experiência futuros podem ser enviados. Essa ação é chamada sempre que o consentimento é alterado. Em carregamentos de página futuros, o cookie de consentimento da Experience Edge será lido para determinar se os Eventos de experiência podem ser enviados e se um cookie de identidade pode ser definido.

Semelhante à integração do IAB TCF 2.0, o Experience Edge dá consentimento quando um cliente tem o consentimento explícito para os seguintes objetivos:

- **Finalidade 1:** armazenar e/ou acessar informações em um dispositivo
- **Finalidade 10:** desenvolver e melhorar produtos
- **Propósito especial 1:** garanta a segurança, evite fraudes e depure. (De acordo com os regulamentos da TCF do IAB, isso é sempre consentido)
- **Permissão de fornecedor de Adobe:** Consentimento para Adobe (Fornecedor 565)

Para obter mais informações sobre o comando `setConsent`, leia a documentação em [Suporte ao consentimento](../../consent/supporting-consent.md).

### Adicionar consentimento aos eventos de experiência

O SDK da Web da Adobe Experience Platform tem um comando `sendEvent` que coleta um Evento de experiência. Se estiver integrando com Eventos de experiência ou Adobe Analytics e quiser as preferências de consentimento em cada Evento de experiência, adicione as informações de consentimento a cada comando `sendEvent`.

Para obter mais informações sobre o comando `sendEvent`, leia a documentação sobre [eventos de rastreamento](../../fundamentals/tracking-events.md).

## Próximas etapas

Agora que você tem uma compreensão básica da Estrutura de transparência e consentimento 2.0 do IAB, consulte qualquer um dos guias sobre como usar o IAB TCF 2.0 [com Adobe Experience Platform Launch](./with-launch.md) ou [sem Adobe Experience Platform Launch](./without-launch.md).
