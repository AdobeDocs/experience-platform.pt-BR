---
title: Tipos de elementos de dados na extensão SDK da Web do Adobe Experience Platform
description: Saiba mais sobre os diferentes tipos de elementos de dados fornecidos pela extensão de tag do Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 4caab19e1f58fc5cec5a3c56c43e47786d49c3dc
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 19%

---

# Tipos de elementos de dados

Depois de definir o [tipos de ação](action-types.md) no [Extensão de tag do SDK da Web da Adobe Experience Platform](web-sdk-extension-configuration.md), configure os tipos de elementos de dados.

Esta página descreve os tipos de elementos de dados disponíveis.


## ID de mesclagem de eventos

Quando usado, esse elemento de dados fornece uma ID de mesclagem de eventos. Nenhuma configuração é necessária para esse elemento de dados. O elemento de dados fornecido permanece o mesmo até que o visitante saia da página ou até que o tipo de ação &quot;Redefinir ID de mesclagem de eventos&quot; seja usado.

## Mapa de identidade

Um mapa de identidade permite estabelecer identidades para o visitante da página da Web. Um mapa de identidade consiste em namespaces, como _telefone_ ou _email_, com cada namespace contendo um ou mais identificadores. Por exemplo, se o indivíduo em seu site tiver fornecido dois números de telefone, o namespace do telefone deverá conter dois identificadores.

No [!UICONTROL Mapa de identidade] elemento de dados, você fornecerá as seguintes informações para cada identificador:

* **[!UICONTROL ID]**: o valor que identifica o visitante. Por exemplo, se o identificador pertencer à variável _telefone_ namespace, o [!UICONTROL ID] pode ser _555-555-5555_. Normalmente, esse valor é derivado de uma variável JavaScript ou de algum outro dado na página, portanto, é melhor criar um elemento de dados que faça referência aos dados da página e, em seguida, fazer referência ao elemento de dados na [!UICONTROL ID] campo dentro do [!UICONTROL Mapa de identidade] elemento de dados. Se, ao ser executado na página, o valor da ID for qualquer coisa menos uma string preenchida, o identificador será removido automaticamente do mapa de identidade.
* **[!UICONTROL Estado autenticado]**: uma seleção que indica se o visitante está autenticado.
* **[!UICONTROL Principal]**: uma seleção que indica se o identificador deve ser usado como o identificador principal do indivíduo. Se nenhum identificador for marcado como principal, a ECID será usada como o identificador principal.

Você não deve fornecer uma ECID ao criar um mapa de identidade. Ao usar o SDK, uma ECID é gerada automaticamente no servidor e incluída no mapa de identidade.

O elemento de dados do mapa de identidade é frequentemente usado em conjunto com a variável [[!UICONTROL Objeto XDM] tipo de elemento de dados](#xdm-object) e a variável [[!UICONTROL Definir consentimento] tipo de ação](action-types.md#set-consent).

Leia mais sobre [Serviço de identidade da Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/identity/home.html?lang=pt-BR).

![](./assets/identity-map-data-element.png)

## Objeto XDM {#xdm-object}

Use o formato XDM para enviar dados ao Adobe Experience Platform Web SDK. A formatação dos dados é mais fácil com o elemento de dados do objeto XDM. Ao abrir esse elemento de dados pela primeira vez, selecione a sandbox e o esquema corretos da Adobe Experience Platform. Após selecionar o esquema, você verá a estrutura dele, que pode ser facilmente preenchida.

![](./assets/XDM-object.png)

Observe que quando você abre determinados campos do esquema, como `web.webPageDetails.URL`, alguns itens são coletados automaticamente. Embora vários itens sejam coletados automaticamente, você pode substituir qualquer item, se necessário. Todos os valores podem ser preenchidos manualmente ou usando outros elementos de dados.

>[!NOTE]
>
>Preencha apenas as informações que você está interessado em coletar. Tudo o que não for preenchido será omitido quando os dados forem enviados para as soluções.
