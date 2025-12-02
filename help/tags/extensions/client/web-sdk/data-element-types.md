---
title: Tipos de elementos de dados na extensão do Adobe Experience Platform Web SDK
description: Saiba mais sobre os diferentes tipos de elementos de dados fornecidos pela extensão de tag do Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: 8cb8dcf7217440da98f6856293c530a66d4c3444
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 5%

---

# Tipos de elementos de dados

Depois de definir os [tipos de ação](actions/actions-overview.md) na extensão de tag, você deve configurar os tipos de elementos de dados. Esta página descreve os tipos de elementos de dados disponíveis.

## Mapa de identidade {#identity-map}

Um mapa de identidade permite estabelecer identidades para o visitante da página da Web. Um mapa de identidade consiste em namespaces, como `CRMID`, `Phone` ou `Email`, com cada namespace contendo um ou mais identificadores. Por exemplo, se o indivíduo em seu site tiver fornecido dois números de telefone, o namespace do telefone deverá conter dois identificadores.

No elemento de dados [!UICONTROL Identity map], você fornecerá as seguintes informações para cada identificador:

* **[!UICONTROL ID]**: o valor que identifica o visitante. Por exemplo, se o identificador pertence ao namespace _phone_, o [!UICONTROL ID] pode ser _555-555-5555_. Normalmente, esse valor é derivado de uma variável JavaScript ou de alguns outros dados na página. Portanto, é melhor criar um elemento de dados que faça referência aos dados da página e, em seguida, fazer referência ao elemento de dados no campo [!UICONTROL ID] dentro do elemento de dados [!UICONTROL Identity map]. Se, ao ser executado na página, o valor da ID for qualquer coisa menos uma string preenchida, o identificador será removido automaticamente do mapa de identidade.
* **[!UICONTROL Authenticated state]**: uma seleção que indica se o visitante está autenticado.
* **[!UICONTROL Primary]**: uma seleção que indica se o identificador deve ser usado como o identificador principal do indivíduo. Se nenhum identificador for marcado como principal, a ECID será usada como o identificador principal.

![Imagem da interface do usuário mostrando a tela Editar Elemento de Dados.](assets/identity-map-data-element.png)

>[!TIP]
>
>A Adobe recomenda enviar identidades que representam uma pessoa, como `Luma CRM Id` como a identidade principal.
>
>Se o mapa de identidade contiver o identificador de pessoa (por exemplo, `Luma CRM Id`), o identificador de pessoa se tornará o identificador principal. Caso contrário, `ECID` se tornará a identidade principal.

Você não deve fornecer um [!DNL ECID] ao criar um mapa de identidade. Ao usar a SDK, um [!DNL ECID] é gerado automaticamente no servidor e incluído no mapa de identidade.

O elemento de dados do mapa de identidade é frequentemente usado com o elemento de dados [[!UICONTROL Variable]](#variable) e a ação [[!UICONTROL Set consent]](actions/set-consent.md).

Leia mais sobre o [Adobe Experience Platform Identity Service](/help/identity-service/home.md).

## Objeto XDM {#xdm-object}

A formatação dos dados para o XDM é mais fácil com o elemento de dados do objeto XDM. Ao abrir esse elemento de dados pela primeira vez, selecione a sandbox e o esquema corretos da Adobe Experience Platform. Após selecionar o esquema, você verá a estrutura dele, que pode ser facilmente preenchida.

![Imagem da interface do usuário mostrando a estrutura do objeto XDM.](assets/XDM-object.png)

Observe que quando você abre determinados campos do esquema, como `web.webPageDetails.URL`, alguns itens são coletados automaticamente. Embora vários itens sejam coletados automaticamente, você pode substituir qualquer item, se necessário. Todos os valores podem ser preenchidos manualmente ou usando outros elementos de dados.

>[!NOTE]
>
>Preencha apenas as informações que você está interessado em coletar. Tudo o que não for preenchido será omitido quando os dados forem enviados para as soluções.

## Variable {#variable}

Você pode criar objetos de carga usando o elemento de dados **[!UICONTROL Variable]**. Há suporte para os objetos [!UICONTROL XDM] e [!UICONTROL Data].

* Ao selecionar [!UICONTROL XDM], selecione o [!UICONTROL Sandbox] e o [!UICONTROL Schema] desejados.
* Ao selecionar [!UICONTROL Data], selecione as soluções desejadas. As soluções disponíveis incluem [!UICONTROL Adobe Analytics] e [!UICONTROL Adobe Target].

![Imagem da interface do usuário de marcas mostrando as opções do elemento de dados.](assets/variable-data-element.png)

Depois de criar esse elemento de dados, você pode usar a ação [Atualizar variável](actions/update-variable.md) para modificá-lo. Quando estiver pronto, você poderá incluir este elemento de dados na ação [Enviar evento](actions/send-event.md) para enviar dados para uma sequência de dados.

## Media: Qualidade da experiência {#quality-experience}

Um elemento de dados **[!UICONTROL Quality of Experience]** é útil ao enviar eventos de streaming de mídia para o Adobe Experience Platform. Você pode adicionar esse elemento ao criar uma sessão de mídia e os seguintes eventos de mídia conterão dados atualizados de Qualidade da experiência.

![Imagem da interface do usuário mostrando a tela Criar Elemento de Dados de Qualidade de Experiência.](assets/qoe-data-element.png)

## Próximas etapas {#next-steps}

Saiba mais sobre casos de uso específicos, como [acessar a ECID](accessing-the-ecid.md).
