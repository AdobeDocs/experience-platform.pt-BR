---
title: Tipos de ação na extensão SDK da Web da Adobe Experience Platform
description: Saiba mais sobre os diferentes tipos de ação fornecidos pela extensão de tag Adobe Experience Platform Web SDK.
solution: Experience Platform
exl-id: a4bf0bb9-59b4-4c43-97e6-387768176517
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '821'
ht-degree: 2%

---


# Tipos de ação

Depois de configurar o [Extensão de tag do Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), você deve configurar os tipos de ação.

Esta página descreve os tipos de ação compatíveis com o [Extensão de tag do Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md).

## Enviar evento {#send-event}

Envia um evento para o Adobe [!DNL Experience Platform] para que o Adobe Experience Platform possa coletar os dados enviados e agir de acordo com essas informações. Selecione uma instância (caso tenha mais de uma). Todos os dados que você deseja enviar podem ser enviados na variável **[!UICONTROL Dados XDM]** campo. Use um objeto JSON que esteja em conformidade com a estrutura do esquema XDM. Esse objeto pode ser criado na página ou por meio de um **[!UICONTROL Código personalizado]** **[!UICONTROL Elemento de dados]**.

Há alguns outros campos no tipo de ação Enviar evento que também podem ser úteis dependendo de sua implementação. Observe que esses campos são todos opcionais.

- **Tipo:** Este campo permite que você especifique um tipo de evento que será gravado no esquema XDM. Consulte a [documentação](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=en#using-the-sendbeacon-api) para obter mais informações sobre os tipos de evento padrão.
- **Dados:** Os dados que não correspondem a um esquema XDM podem ser enviados usando esse campo. Este campo é útil se você estiver tentando atualizar um perfil do Adobe Target ou enviar atributos do Recommendations do Target. Por exemplo, veja nossa [documentação](https://experienceleague.adobe.com/docs/experience-platform/edge/fundamentals/tracking-events.html?lang=pt-BR).<!--- **Merge ID:** If you would like to specify a merge ID for your event, you can do so in this field. Please note that the solutions downstream are not able to merge your event data at this time. -->
- **ID do conjunto de dados:** Se precisar enviar dados para um conjunto de dados diferente daquele especificado no conjunto de dados, especifique essa ID do conjunto de dados aqui.
- **O documento será descarregado:** Se você deseja garantir que os eventos alcancem o servidor mesmo que o usuário saia da página, verifique a variável **[!UICONTROL O documento será descarregado]** caixa de seleção. Isso permite que os eventos cheguem ao servidor, mas as respostas são ignoradas.
- **Renderizar decisões de personalização visual:** Se você deseja renderizar o conteúdo personalizado na página, marque a opção **[!UICONTROL Renderizar decisões de personalização visual]** caixa de seleção. Você também pode especificar escopos de decisão e/ou superfícies, se necessário. Consulte a [documentação de personalização](../personalization/rendering-personalization-content.md#automatically-rendering-content) para obter mais informações sobre renderização de conteúdo personalizado.

## Definir consentimento {#set-consent}

Após receber o consentimento do usuário, ele deve ser comunicado ao SDK da Web da Adobe Experience Platform usando o tipo de ação &quot;Definir consentimento&quot;. Atualmente, há suporte para dois tipos de padrões: &quot;Adobe&quot; e &quot;IAB TCF&quot;. Consulte [Suporte às preferências de consentimento do cliente](../consent/supporting-consent.md). Ao usar o Adobe versão 2.0, somente um valor de elemento de dados é suportado. Será necessário criar um elemento de dados que resolva o objeto de consentimento.

Nesta ação, você também recebe um campo opcional para incluir um Mapa de identidade para que as identidades possam ser sincronizadas após o recebimento do consentimento. A sincronização é útil quando o consentimento é configurado como &quot;Pendente&quot; ou &quot;Fora&quot;, pois a chamada de consentimento é provavelmente a primeira chamada a ser acionada.

## Redefinir ID de mesclagem de eventos {#reset-event-merge-id}

Se você quiser redefinir a ID da mesclagem de eventos na página, é possível fazê-lo com esta ação. Para redefinir sua ID, selecione a ID de mesclagem que deseja redefinir e acione a ação conforme necessário.

## (Beta) Atualizar variável {#update-variable}

>[!IMPORTANT]
>
>No momento, essa é uma funcionalidade beta e está sujeita a alterações. As versões futuras podem conter alterações de quebra.

Use esta ação para modificar um objeto XDM como resultado de um evento. Esta ação destina-se a criar um objeto que poderá ser referenciado posteriormente a partir de um **[!UICONTROL Enviar evento]** para gravar o objeto XDM do evento.

Para usar esse tipo de ação, você deve ter definido um [variável](data-element-types.md#variable) elemento de dados. Depois que você escolher um elemento de dados variável para modificar, um editor será exibido, de modo semelhante ao editor da [Objeto XDM](data-element-types.md#xdm-object) elemento de dados.

![](./assets/update-variable.png)

O esquema XDM usado para o editor é o esquema selecionado no [!UICONTROL variável] elemento de dados. Você pode definir uma ou mais propriedades do objeto clicando em uma das propriedades na árvore à esquerda e, em seguida, modificando o valor à direita.Por exemplo, na captura de tela abaixo, a propriedade generatedBy está sendo definida como o elemento de dados &quot;Produzido pelo elemento de dados&quot;.

![](./assets/update-variable-set-property.png)

Há algumas diferenças entre o editor na ação de variável de atualização e o editor no elemento de dados do objeto XDM. Primeiro, a ação da variável de atualização tem um item de nível raiz rotulado &quot;xdm&quot;. Se você clicar nesse item, poderá especificar um elemento de dados a ser usado para definir o objeto inteiro. Em segundo lugar, a ação da variável de atualização tem caixas de seleção para limpar os dados do objeto xdm. Clique em uma das propriedades à esquerda e marque a caixa de seleção à direita para limpar o valor. Isso eliminará o valor atual antes de definir quaisquer valores na variável.

## Próximas etapas {#next-steps}

Após ler este artigo, você deve ter uma melhor compreensão de como configurar suas ações. Em seguida, leia sobre como [configurar os tipos de elemento de dados](data-element-types.md).
