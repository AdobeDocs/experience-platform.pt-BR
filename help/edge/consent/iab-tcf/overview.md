---
title: Suporte ao IAB TCF 2.0 no SDK da Web da Adobe Experience Platform
description: Saiba como oferecer suporte às preferências de consentimento da TCF 2.0 do IAB usando o SDK da Web da Adobe Experience Platform
keywords: consentimento;setConsent;Grupo de campos de privacidade de perfil;Grupo de campos de privacidade de evento de experiência;Grupo de campos de privacidade;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: 3272db15283d427eb4741708dffeb8141f61d5ff
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 0%

---

# Suporte ao IAB TCF 2.0 no SDK da Web do Adobe Experience Platform

O SDK da Web da Adobe Experience Platform tem suporte para a Estrutura de transparência e consentimento do Interative Advertising Bureau, versão 2.0 (IAB TCF 2.0). Este guia mostra os requisitos para oferecer suporte ao IAB TCF 2.0 por meio da integração do SDK da Web da Adobe Experience Platform com o Adobe Real-time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics e Edge Network.

Além disso, os guias a seguir estão disponíveis para ajudar a saber como integrar a TCF do IAB 2.0 com e sem tags.

- [Com tags](./with-launch.md)
- [Sem tags](./without-launch.md)

## Introdução

Para implementar o SDK da Web com o TCF do IAB 2.0, é necessário ter uma compreensão funcional do Experience Data Model (XDM) e dos Eventos de experiência. Antes de começar, revise o seguinte documento:

- [Visão geral do sistema do Experience Data Model (XDM)](../../../xdm/home.md): padronização e interoperabilidade são conceitos fundamentais por trás do Adobe Experience Platform. [!DNL Experience Data Model (XDM)]O, impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

## integração de Experience Platform

Para enviar dados de consentimento à Adobe Experience Platform usando o SDK, é necessário o seguinte:

- Um conjunto de dados cujo esquema é baseado na variável [!DNL XDM Individual Profile] e contém campos de consentimento TCF 2.0, habilitados para uso no [!DNL Real-Time Customer Profile].
- Uma sequência de dados configurada com a Platform e o conjunto de dados habilitado para perfil mencionado acima.

Consulte o guia em [Conformidade com TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) para obter instruções sobre como criar os conjuntos de dados e a sequência de dados necessários.

## integração de Audience Manager

O Adobe Audience Manager (AAM) inclui suporte para IAB TCF 2.0, que permite avaliar, honrar e encaminhar as opções de privacidade do cliente para parceiros downstream. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Para integrar com o Audience Manager por meio do SDK da Web da Adobe Experience Platform, verifique se você tem uma sequência de dados configurada para encaminhar para o Adobe Audience Manager.

## Integração entre eventos de experiência e Adobe Analytics

Enquanto os públicos-alvo da Real-Time CDP e do Audience Manager acompanham as preferências de consentimento atuais de um cliente, os Eventos de experiência podem manter as preferências de consentimento de um cliente que estavam ativas quando o evento foi coletado.

Para coletar informações de consentimento sobre eventos, é necessário o seguinte:

- Um conjunto de dados com base na variável [!DNL XDM Experience Event] classe, com o [!DNL Experience Event] grupo de campos de esquema de privacidade.
- Um fluxo de dados configurado com o [!DNL XDM Experience Event] acima.

Para obter mais informações sobre como converter um evento de experiência XDM em uma ocorrência do Analytics, comece lendo o [Visão geral do Analytics](../../data-collection/adobe-analytics/analytics-overview.md) documentação.

## Integração do SDK da Web do Adobe Experience Platform

As seções abaixo descrevem os principais pontos de integração entre o IAB TCF 2.0 e o Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Mesmo sem o Real-Time CDP ou o Audience Manager configurado, ainda é possível integrar a TCF do IAB 2.0 com o SDK da Web. As preferências de consentimento podem ser usadas para controlar a coleção de eventos de experiência e definir um cookie de identidade.

### Consentimento padrão

O consentimento padrão é usado quando não há preferência de consentimento já salva para um cliente. Ou seja, as opções de consentimento padrão podem controlar o comportamento do Adobe Experience Platform Web SDK e alterar com base na região de um cliente.

Por exemplo, se você tiver um cliente que não esteja na jurisdição do Regulamento Geral sobre a Proteção de Dados (GDPR), o consentimento padrão poderá ser definido como `in`, mas dentro da jurisdição do GDPR, o consentimento padrão pode ser definido como `pending`. Sua Plataforma de gerenciamento de consentimento (CMP) pode detectar a região do cliente e fornecer o sinalizador `gdprApplies` para o IAB TCF 2.0. Esse sinalizador pode ser usado para definir o consentimento padrão.

Para obter mais informações sobre consentimento padrão, consulte o [seção de consentimento padrão](../../fundamentals/configuring-the-sdk.md#default-consent) na documentação de configuração do SDK.

### Definição do consentimento quando ele é alterado

O Adobe Experience Platform Web SDK tem um `setConsent` , que comunica as preferências de consentimento do cliente para todos os serviços da Adobe usando a TCF do IAB 2.0. Se você estiver integrando o com o Real-Time CDP, isso atualizará o perfil do cliente. Se você estiver integrando o com o Audience Manager, isso atualizará as informações de seu cliente. Chamar isso também define um cookie com uma preferência de consentimento &quot;tudo ou nada&quot; que controla se os eventos de experiência futuros podem ser enviados. Essa ação deve ser chamada sempre que o consentimento for alterado. Em carregamentos de página futuros, o cookie de consentimento da Rede de borda será lido para determinar se os Eventos de experiência podem ser enviados e se um cookie de identidade pode ser definido.

Semelhante à integração do Audience Manager IAB TCF 2.0, a Rede de borda consente quando um cliente consente explicitamente com as seguintes finalidades:

- **Finalidade 1:** Armazenar e/ou acessar informações em um dispositivo
- **Finalidade 10:** Desenvolver e aprimorar produtos
- **Finalidade especial 1:** Garanta a segurança, evite fraudes e depure. (De acordo com os regulamentos da TCF do IAB, isso é sempre aceito)
- **Permissão de fornecedor Adobe:** Consentimento para Adobe (Fornecedor 565)

Para obter mais informações sobre o `setConsent` , leia a documentação em [Suporte ao consentimento](../../consent/supporting-consent.md).

### Adicionar consentimento a eventos de experiência

O Adobe Experience Platform Web SDK tem um `sendEvent` que coleta um Evento de experiência. Se estiver integrando com Eventos de experiência ou Adobe Analytics e quiser as preferências de consentimento em cada Evento de experiência, você deve adicionar as informações de consentimento a cada `sendEvent` comando.

Para obter mais informações sobre o `sendEvent` , leia a documentação em [rastreamento de eventos](../../fundamentals/tracking-events.md).

## Próximas etapas

Agora que você tem uma compreensão básica da Estrutura de transparência e consentimento 2.0 do IAB, consulte qualquer um dos guias sobre o uso da TCF do IAB 2.0 [com tags](./with-launch.md) ou [sem tags](./without-launch.md).
