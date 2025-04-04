---
title: Suporte IAB TCF 2.0 no Adobe Experience Platform Web SDK
description: Saiba como oferecer suporte às preferências de consentimento da TCF 2.0 do IAB usando o Adobe Experience Platform Web SDK
keywords: consentimento;setConsent;Grupo de campos de privacidade de perfil;Grupo de campos de privacidade de evento de experiência;Grupo de campos de privacidade;IAB TCF 2.0;Real-Time CDP;
exl-id: 78e728f4-1604-40bf-9e21-a056024bbc98
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%

---

# Suporte ao IAB TCF 2.0 no Adobe Experience Platform Web SDK

O Adobe Experience Platform Web SDK tem suporte para o Interative Advertising Bureau Transparency &amp; Consent Framework, versão 2.0 (IAB TCF 2.0). Este guia mostra os requisitos para oferecer suporte ao IAB TCF 2.0 por meio da integração do Adobe Experience Platform Web SDK com o Adobe Real-Time Customer Data Platform, Audience Manager, Experience Events, Adobe Analytics e Edge Network.

Além disso, os guias a seguir estão disponíveis para ajudar a saber como integrar a TCF do IAB 2.0 com e sem tags.

- [Com tags](./with-tags.md)
- [Sem tags](./without-tags.md)

## Introdução

Para implementar o Web SDK com a TCF do IAB 2.0, é necessário ter uma compreensão funcional do Experience Data Model (XDM) e dos Eventos de experiência. Antes de começar, revise o seguinte documento:

- [Visão geral do sistema do Experience Data Model (XDM)](../../../xdm/home.md): a padronização e a interoperabilidade são os principais conceitos por trás do Adobe Experience Platform. O [!DNL Experience Data Model (XDM)], orientado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

## Integração do Experience Platform

Para enviar dados de consentimento ao Adobe Experience Platform usando a SDK, é necessário:

- Um conjunto de dados cujo esquema é baseado na classe [!DNL XDM Individual Profile] e contém campos de consentimento TCF 2.0, habilitados para uso em [!DNL Real-Time Customer Profile].
- Uma sequência de dados configurada com o Experience Platform e o conjunto de dados habilitado para perfil mencionado acima.

Consulte o guia sobre [Conformidade com a TCF 2.0](../../../landing/governance-privacy-security/consent/iab/overview.md) para obter instruções sobre como criar os conjuntos de dados e a sequência de dados necessários.

## Integração do Audience Manager

O Adobe Audience Manager (AAM) inclui suporte para IAB TCF 2.0, que permite avaliar, honrar e encaminhar as opções de privacidade do cliente para parceiros downstream. <!--For more information, read the documentation on [Sending Data to Audience Manager](../audience-manager/audience-manager-overview.md).-->

>[!TIP]
>
>Para integrar ao Audience Manager por meio do Adobe Experience Platform Web SDK, verifique se você tem um fluxo de dados configurado para encaminhar para o Adobe Audience Manager.

## Integração entre eventos de experiência e Adobe Analytics

Enquanto os públicos da Real-Time CDP e da Audience Manager acompanham as preferências de consentimento atuais de um cliente, os Eventos de experiência podem manter as preferências de consentimento de um cliente que estavam ativas quando o evento foi coletado.

Para coletar informações de consentimento sobre eventos, é necessário o seguinte:

- Um conjunto de dados com base na classe [!DNL XDM Experience Event], com o grupo de campos de esquema de privacidade [!DNL Experience Event].
- Uma sequência de dados configurada com o conjunto de dados [!DNL XDM Experience Event] acima.

Para obter mais informações sobre como converter um Evento de experiência XDM em uma ocorrência do Analytics, consulte [Envio de dados para o Adobe Analytics usando a Web SDK](/help/web-sdk/use-cases/adobe-analytics.md).

## Integração do Adobe Experience Platform Web SDK

As seções abaixo descrevem os principais pontos de integração entre o IAB TCF 2.0 e o Adobe Experience Platform Web SDK.

>[!NOTE]
>
>Mesmo sem a configuração do Real-Time CDP ou do Audience Manager, ainda é possível integrar a TCF do IAB 2.0 com o Web SDK. As preferências de consentimento podem ser usadas para controlar a coleção de eventos de experiência e definir um cookie de identidade.

### Consentimento padrão

O consentimento padrão é usado quando não há preferência de consentimento já salva para um cliente. Ou seja, as opções de consentimento padrão podem controlar o comportamento do Adobe Experience Platform Web SDK e alterar com base na região de um cliente.

Por exemplo, se você tiver um cliente que não esteja na jurisdição do Regulamento Geral sobre a Proteção de Dados (GDPR), o consentimento padrão poderá ser definido como `in`, mas dentro da jurisdição do GDPR, o consentimento padrão poderá ser definido como `pending`. Sua Plataforma de Gerenciamento de Consentimento (CMP) pode detectar a região do cliente e fornecer o sinalizador `gdprApplies` para a TCF do IAB 2.0. Esse sinalizador pode ser usado para definir o consentimento padrão. Consulte [`defaultConsent`](/help/web-sdk/commands/configure/defaultconsent.md) para obter mais informações.

### Definição do consentimento quando ele é alterado

O Adobe Experience Platform Web SDK tem um comando `setConsent`, que comunica as preferências de consentimento do cliente para todos os serviços da Adobe usando a TCF do IAB 2.0. Se você estiver integrando o com o Real-Time CDP, isso atualizará o perfil do cliente. Se você estiver integrando o com o Audience Manager, isso atualizará as informações do cliente. Chamar isso também define um cookie com uma preferência de consentimento &quot;tudo ou nada&quot; que controla se os eventos de experiência futuros podem ser enviados. Essa ação deve ser chamada sempre que o consentimento for alterado. Em carregamentos de página futuros, o cookie de consentimento da Edge Network será lido para determinar se os Eventos de experiência podem ser enviados e se um cookie de identidade pode ser definido.

Semelhante à integração do IAB TCF 2.0 da Audience Manager, a Edge Network consente quando um cliente consente explicitamente com as seguintes finalidades:

- **Finalidade 1:** Armazenar e/ou acessar informações em um dispositivo
- **Finalidade 10:** desenvolver e melhorar produtos
- **Propósito Especial 1:** garanta a segurança, evite fraudes e depure. (De acordo com os regulamentos da TCF do IAB, isso é sempre aceito)
- **Permissão de Fornecedor da Adobe:** Consentimento para Adobe (Fornecedor 565)

Para obter mais informações sobre o comando `setConsent`, leia a documentação dedicada do Web SDK em [setConsent](../../../web-sdk/commands/setconsent.md).

### Adicionar consentimento a eventos de experiência

O Adobe Experience Platform Web SDK tem um comando [`sendEvent`](/help/web-sdk/commands/sendevent/overview.md) que coleta um Evento de Experiência. Se estiver integrando com Eventos de Experiência ou Adobe Analytics e quiser as preferências de consentimento em cada Evento de Experiência, adicione informações de consentimento a cada comando `sendEvent`.

## Próximas etapas

Agora que você tem uma compreensão básica da Estrutura de transparência e consentimento 2.0 do IAB, consulte qualquer um dos guias sobre o uso do IAB TCF 2.0 [com tags](./with-tags.md) ou [sem tags](./without-tags.md).
