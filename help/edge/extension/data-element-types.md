---
title: Tipos de elementos de dados na extensão do SDK da Web da Adobe Experience Platform
description: Saiba mais sobre os diferentes tipos de elementos de dados fornecidos pela extensão de tag Adobe Experience Platform Web SDK.
exl-id: 3c2c257f-1fbc-4722-8040-61ad19aa533f
source-git-commit: db7700d5c504e484f9571bbb82ff096497d0c96e
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 8%

---


# Tipos de elementos de dados

Depois de definir o [tipos de ação](action-types.md) no [Extensão de tag do Adobe Experience Platform Web SDK](web-sdk-extension-configuration.md), você deve configurar os tipos de elemento de dados. Esta página descreve os tipos de elementos de dados disponíveis.

## ID da mesclagem de eventos {#event-merge-id}

Quando usado, esse elemento de dados fornece uma ID de mesclagem de eventos. Nenhuma configuração é necessária para esse elemento de dados. O elemento de dados fornecido permanece o mesmo até que o visitante saia da página ou até que a variável **[!UICONTROL Redefinir ID de mesclagem de eventos]** é usada.

## Mapa de identidade {#identity-map}

Um mapa de identidade permite estabelecer identidades para o visitante da sua página da Web. Um mapa de identidade consiste em namespaces, como _Telefone_ ou _email_, com cada namespace contendo um ou mais identificadores. Por exemplo, se o indivíduo em seu site tiver fornecido dois números de telefone, seu namespace de telefone deverá conter dois identificadores.

No [!UICONTROL Mapa de identidade] elemento de dados, você fornecerá as seguintes informações para cada identificador:

* **[!UICONTROL ID]**: O valor que identifica o visitante. Por exemplo, se o identificador pertencer à variável _Telefone_ namespace, o [!UICONTROL ID] pode ser _555-555-5555_. Normalmente, esse valor é derivado de uma variável JavaScript ou de algum outro dado na página, portanto, é melhor criar um elemento de dados que faça referência aos dados da página e, em seguida, faça referência ao elemento de dados no [!UICONTROL ID] no campo [!UICONTROL Mapa de identidade] elemento de dados. Se, ao executar em sua página, o valor da ID for qualquer coisa além de uma string preenchida, o identificador será removido automaticamente do mapa de identidade.
* **[!UICONTROL Estado autenticado]**: Uma seleção que indica se o visitante está autenticado.
* **[!UICONTROL Primário]**: Uma seleção que indica se o identificador deve ser usado como o identificador principal do indivíduo. Se nenhum identificador estiver marcado como primário, a ECID será usada como o identificador principal.

![Imagem da interface do usuário que mostra a tela Editar elemento de dados .](./assets/identity-map-data-element.png)

Você não deve fornecer um [!DNL ECID] ao criar um mapa de identidade. Ao usar o SDK, um [!DNL ECID] é gerado automaticamente no servidor e incluído no mapa de identidade.

O elemento de dados do mapa de identidade geralmente é usado em conjunto com a variável [[!UICONTROL Objeto XDM] tipo de elemento de dados](#xdm-object) e [[!UICONTROL Definir consentimento] tipo de ação](action-types.md#set-consent).

Leia mais sobre [Serviço de identidade da Adobe Experience Platform](../../identity-service/home.md).

## Objeto XDM {#xdm-object}

Formatar seus dados para XDM é mais fácil com o elemento de dados do objeto XDM. Ao abrir esse elemento de dados pela primeira vez, selecione a sandbox e o esquema corretos da Adobe Experience Platform. Após selecionar o esquema, é possível ver a estrutura do esquema, que pode ser facilmente preenchida.

![Imagem da interface do usuário que mostra a estrutura do objeto XDM.](assets/XDM-object.png)

Observe que, ao abrir determinados campos do esquema, como `web.webPageDetails.URL`, alguns itens são coletados automaticamente. Mesmo que vários itens sejam coletados automaticamente, você pode substituir qualquer item, se necessário. Todos os valores podem ser preenchidos manualmente ou usando outros elementos de dados.

>[!NOTE]
>
>Preencha apenas as informações que você está interessado em coletar. Qualquer coisa que não for preenchida é omitida quando os dados forem enviados para as soluções.

## Variável (Beta) {#variable}

>[!IMPORTANT]
>
>No momento, essa é uma funcionalidade beta e está sujeita a alterações. As versões futuras podem conter alterações de quebra.

Outra maneira de criar objetos XDM é usar o **[!UICONTROL Variável]** elemento de dados. Enquanto o elemento de dados do objeto XDM é criado quando referenciado, como dentro de um `sendEvent` , o **[!UICONTROL Variável]** o elemento de dados pode ser atualizado por meio de [!UICONTROL Atualizar variável] ações. Para usar o elemento de dados, selecione a sandbox e o schema corretos do Adobe Experience Platform.

![Imagem da interface do usuário que mostra a tela Criar elemento de dados .](assets/variable-data-element.png)

Depois de criar esse elemento de dados, você pode usar [Atualizar variável](./action-types.md#update-variable) ações para modificar o elemento de dados. Em seguida, nas ações de evento de envio, use o elemento de dados variável para a opção XDM .

## Próximas etapas {#next-steps}

Saiba mais sobre casos de uso específicos, como [acesso à ECID](accessing-the-ecid.md).
