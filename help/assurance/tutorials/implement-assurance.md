---
title: Implementação da extensão Adobe Experience Platform Assurance
description: Este guia explica como implementar e instalar a extensão Adobe Experience Platform Assurance.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '387'
ht-degree: 95%

---

# Implementação da extensão Adobe Experience Platform Assurance

Este tutorial explica como instalar e implementar a extensão do Experience Platform Assurance no Mobile SDK. Para obter instruções sobre como adicionar a extensão do Assurance ao seu aplicativo, leia a [Visão geral da extensão do Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Introdução

Para instalar e implementar a extensão do Assurance, será necessário o acesso aos seguintes serviços:

- A [interface da coleção de dados da Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Criar uma propriedade móvel

>[!NOTE]
>
>Se você já tiver uma propriedade móvel, poderá prosseguir para a próxima etapa.

Na interface da coleção de dados, selecione **[!UICONTROL Tags]**. Uma lista de propriedades móveis e da Web é exibida, com informações sobre as propriedades que pertencem à sua organização. Selecione **[!UICONTROL Nova propriedade]** para criar uma nova propriedade.

![O botão Nova propriedade é realçado, mostrando o que você deve selecionar para criar uma nova propriedade](./images/implement-assurance/create-new-property.png)

A página **[!UICONTROL Criar propriedade]** é exibida. Insira o nome da nova propriedade e selecione **[!UICONTROL Dispositivo móvel]** como sua plataforma. Depois de inserir os detalhes, selecione **[!UICONTROL Salvar]** para criar a propriedade móvel.

>[!NOTE]
>
>A configuração de **[!UICONTROL privacidade]** da propriedade móvel **não** afeta a coleção de dados do Assurance.

![A página Criar propriedade é exibida. Você pode inserir informações sobre sua propriedade móvel aqui.](./images/implement-assurance/create-property.png)

## Instalar a extensão do Assurance

Selecione a propriedade móvel na qual você deseja instalar a extensão do Assurance.

![A página Propriedades da tag é exibida, com a propriedade móvel selecionada realçada.](./images/implement-assurance/select-mobile-property.png)

A página **Detalhes da propriedade móvel** é exibida. Selecione **[!UICONTROL Extensões]** para exibir uma lista das extensões que estão atualmente associadas à sua propriedade móvel.

![A página de detalhes da propriedade móvel é exibida. As informações sobre atividades recentes são exibidas. A guia Extensões é realçada.](./images/implement-assurance/tag-properties.png)

Selecione **[!UICONTROL Catálogo]** para ver uma lista de extensões que você pode adicionar à propriedade móvel. Usando o filtro, localize a extensão **[!UICONTROL AEP Assurance]** e selecione **[!UICONTROL Instalar]**.

![O catálogo de extensões é exibido. A extensão do Assurance é filtrada e exibida, e o botão de instalação é realçado.](./images/implement-assurance/assurance-extension.png)

## Próximas etapas

Agora que instalou a extensão do Assurance na sua propriedade móvel, você pode começar a usar o Assurance em aplicativos. Para saber como adicionar a extensão do Assurance ao seu aplicativo, leia a [Visão geral da extensão do Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Para saber como usar o Assurance, leia o [Guia de uso do Assurance](./using-assurance.md).
