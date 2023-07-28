---
title: Tipos de elementos de dados na extensão SDK da Web do Adobe Experience Platform
description: Saiba mais sobre os diferentes tipos de elementos de dados fornecidos pela extensão de tag do Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 44fac57a30295b476910c0b37314eaebba175157
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 5%

---


# Tipos de elementos de dados

Depois de definir o [tipos de ação](action-types.md) no [Extensão de tag do SDK da Web da Adobe Experience Platform](web-sdk-extension-configuration.md), você deve configurar os tipos de elementos de dados. Esta página descreve os tipos de elementos de dados disponíveis.

## Mapa de identidade {#identity-map}

Um mapa de identidade permite estabelecer identidades para o visitante da página da Web. Um mapa de identidade consiste em namespaces, como `CRMID`, `Phone` ou `Email`, com cada namespace contendo um ou mais identificadores. Por exemplo, se o indivíduo em seu site tiver fornecido dois números de telefone, o namespace do telefone deverá conter dois identificadores.

No [!UICONTROL Mapa de identidade] elemento de dados, você fornecerá as seguintes informações para cada identificador:

* **[!UICONTROL ID]**: o valor que identifica o visitante. Por exemplo, se o identificador pertencer à variável _telefone_ namespace, o [!UICONTROL ID] pode ser _555-555-5555_. Normalmente, esse valor é derivado de uma variável JavaScript ou de algum outro dado na página, portanto, é melhor criar um elemento de dados que faça referência aos dados da página e, em seguida, fazer referência ao elemento de dados na [!UICONTROL ID] campo dentro do [!UICONTROL Mapa de identidade] elemento de dados. Se, ao ser executado na página, o valor da ID for qualquer coisa menos uma string preenchida, o identificador será removido automaticamente do mapa de identidade.
* **[!UICONTROL Estado autenticado]**: uma seleção que indica se o visitante está autenticado.
* **[!UICONTROL Principal]**: uma seleção que indica se o identificador deve ser usado como o identificador principal do indivíduo. Se nenhum identificador for marcado como principal, a ECID será usada como o identificador principal.

![Imagem da interface mostrando a tela Editar elemento de dados.](assets/identity-map-data-element.png)

>[!TIP]
>
>Adobe recomenda enviar identidades que representam uma pessoa, como `Luma CRM Id` como a identidade principal.
>
>Se o mapa de identidade contiver o identificador de pessoa (por exemplo, `Luma CRM Id`), então o identificador de pessoa se tornará o identificador principal. Caso contrário, `ECID` torna-se a identidade principal.

Você não deve fornecer um [!DNL ECID] ao criar um mapa de identidade. Ao usar o SDK, uma variável [!DNL ECID] é gerado automaticamente no servidor e incluído no mapa de identidade.

O elemento de dados do mapa de identidade é frequentemente usado em conjunto com a variável [[!UICONTROL Objeto XDM] tipo de elemento de dados](#xdm-object) e a variável [[!UICONTROL Definir consentimento] tipo de ação](action-types.md#set-consent).

Leia mais sobre [Serviço de identidade da Adobe Experience Platform](../../../../identity-service/home.md).

## Objeto XDM {#xdm-object}

A formatação dos dados para o XDM é mais fácil com o elemento de dados do objeto XDM. Ao abrir esse elemento de dados pela primeira vez, selecione a sandbox e o esquema corretos da Adobe Experience Platform. Após selecionar o esquema, você verá a estrutura dele, que pode ser facilmente preenchida.

![Imagem da interface mostrando a estrutura do objeto XDM.](assets/XDM-object.png)

Observe que quando você abre determinados campos do esquema, como `web.webPageDetails.URL`, alguns itens são coletados automaticamente. Embora vários itens sejam coletados automaticamente, você pode substituir qualquer item, se necessário. Todos os valores podem ser preenchidos manualmente ou usando outros elementos de dados.

>[!NOTE]
>
>Preencha apenas as informações que você está interessado em coletar. Tudo o que não for preenchido será omitido quando os dados forem enviados para as soluções.

## Variable {#variable}

Outra maneira de criar objetos XDM é usar o **[!UICONTROL Variável]** elemento de dados. Embora o elemento de dados do objeto XDM seja criado quando referenciado, como dentro de um `sendEvent` , o **[!UICONTROL Variável]** o elemento de dados pode ser atualizado via [!UICONTROL Atualizar variável] ações. Para usar o elemento de dados, selecione a sandbox e o esquema corretos do Adobe Experience Platform.

![Imagem da interface mostrando a tela Criar elemento de dados.](assets/variable-data-element.png)

Depois de criar esse elemento de dados, você pode usar [Atualizar variável](./action-types.md#update-variable) ações para modificar o elemento de dados. Em seguida, nas ações enviar evento, use o elemento de dados variável para a opção XDM.

## Próximas etapas {#next-steps}

Saiba mais sobre casos de uso específicos, como [acesso à ECID](accessing-the-ecid.md).
