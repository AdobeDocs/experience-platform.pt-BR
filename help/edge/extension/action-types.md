---
title: Tipos de ação na extensão SDK da Web da Adobe Experience Platform
description: Saiba mais sobre os diferentes tipos de ação fornecidos pela extensão de tag Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: 5218e6cf82b74efbbbcf30495395a4fe2ad9fe14
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 4%

---

# Tipos de ação

Depois de configurar a [extensão de tag do Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), configure os tipos de ação.

Esta página descreve os tipos de ação disponíveis.


## Enviar evento

Envia um evento para Adobe [!DNL Experience Platform] para que o Adobe Experience Platform possa coletar os dados enviados e agir de acordo com essas informações. Selecione uma instância (caso tenha mais de uma). Todos os dados que deseja enviar podem ser enviados no campo **[!UICONTROL Dados XDM]**. Use um objeto JSON que esteja em conformidade com a estrutura do esquema XDM. Esse objeto pode ser criado na página ou por meio de um **[!UICONTROL Custom Code]** **[!UICONTROL Data Element]**.

Há alguns outros campos no tipo de ação Enviar evento que também podem ser úteis dependendo de sua implementação. Observe que esses campos são todos opcionais.

- **Tipo:** este campo permite que você especifique um tipo de evento que será gravado no esquema XDM. Consulte a [documentação](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) para obter mais informações sobre os tipos de evento padrão.
- **Dados:** os dados que não correspondem a um esquema XDM podem ser enviados usando este campo. Este campo é útil se você estiver tentando atualizar um perfil do Adobe Target ou enviar atributos do Recommendations do Target. Para obter exemplos, visualize nossa [documentação](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en).
<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **ID do conjunto de dados:**  se precisar enviar dados para um conjunto de dados diferente daquele especificado no conjunto de dados, especifique essa ID do conjunto de dados aqui.
- **O documento será descarregado:** se você quiser garantir que os eventos alcancem o servidor mesmo que o usuário saia da página, marque a caixa de seleção  **[!UICONTROL Documento será]** descarregada. Isso permite que os eventos cheguem ao servidor, mas as respostas são ignoradas.
- **Renderizar decisões de personalização visual:** se você deseja renderizar o conteúdo personalizado na página, marque a caixa de seleção  **[!UICONTROL Renderizar personalização visual]** do . Você também pode especificar escopos de decisão, se necessário. Consulte a [documentação de personalização](https://experienceleague.adobe.com/docs/experience-platform/edge/personalization/rendering-personalization-content.html?lang=en#automatically-rendering-content) para obter mais informações sobre como renderizar conteúdo personalizado.

## Definir consentimento

Após receber o consentimento do usuário, ele deve ser comunicado ao SDK da Web da Adobe Experience Platform usando o tipo de ação &quot;Definir consentimento&quot;. Atualmente, há suporte para dois tipos de padrões: &quot;Adobe&quot; e &quot;IAB TCF&quot;. Consulte [Suporte a preferências de consentimento do cliente](../consent/supporting-consent.md). Ao usar o Adobe versão 2.0, somente um valor de elemento de dados é suportado. Será necessário criar um elemento de dados que resolva o objeto de consentimento.

Nesta ação, você também recebe um campo opcional para incluir um Mapa de identidade para que as identidades possam ser sincronizadas após o recebimento do consentimento. A sincronização é útil quando o consentimento é configurado como &quot;Pendente&quot; ou &quot;Fora&quot;, pois a chamada de consentimento é provavelmente a primeira chamada a ser acionada.

## Redefinir ID de mesclagem de eventos

Se você quiser redefinir a ID da mesclagem de eventos na página, é possível fazê-lo com esta ação. Para redefinir sua ID, selecione a ID de mesclagem que deseja redefinir e acione a ação conforme necessário.

## O que vem a seguir

Depois de definir suas ações, [configure seus tipos de elemento de dados](data-element-types.md).
