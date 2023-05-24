---
title: Implementação da extensão Adobe Experience Platform Assurance
description: Este guia explica como implementar e instalar a extensão Adobe Experience Platform Assurance.
exl-id: b7bd1bb1-1606-4d00-97e0-c329c86d8ca4
source-git-commit: 05a7b73da610a30119b4719ae6b6d85f93cdc2ae
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 3%

---

# Implementação da extensão Adobe Experience Platform Assurance

Este tutorial explica como instalar e implementar a extensão do Platform Assurance no SDK móvel. Para obter instruções sobre como adicionar a extensão do Assurance ao seu aplicativo, leia o [Visão geral da extensão do Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Introdução

Para instalar e implementar a extensão Assurance, será necessário acessar os seguintes serviços:

- A variável [Interface da coleção de dados do Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Criar uma propriedade móvel

>[!NOTE]
>
>Se você já tiver uma propriedade móvel, poderá prosseguir para a próxima etapa.

Na interface da Coleção de dados, selecione **[!UICONTROL Tags]**. Uma lista de propriedades móveis e da Web é exibida, com informações sobre as propriedades que pertencem à sua organização. Selecionar **[!UICONTROL Nova propriedade]** para criar uma nova propriedade.

![O botão Nova propriedade é realçado, mostrando o que você seleciona para criar uma nova propriedade](./images/implement-assurance/create-new-property.png)

A variável **[!UICONTROL Criar propriedade]** é exibida. Insira o nome da nova propriedade e selecione **[!UICONTROL Dispositivo móvel]** como sua plataforma. Depois de inserir os detalhes, selecione **[!UICONTROL Salvar]** para criar a propriedade móvel.

>[!NOTE]
>
>A propriedade móvel do **[!UICONTROL Privacidade]** a configuração faz **não** de dados do Assurance.

![A página Criar Propriedade é exibida. Você pode inserir informações sobre sua propriedade móvel aqui.](./images/implement-assurance/create-property.png)

## Instalar a extensão Assurance

Selecione a propriedade móvel na qual você deseja instalar a extensão do Assurance.

![A página Propriedades da tag é exibida, com a propriedade móvel selecionada realçada.](./images/implement-assurance/select-mobile-property.png)

A variável **detalhes da propriedade móvel** é exibida. Selecionar **[!UICONTROL Extensões]** para exibir uma lista das extensões atualmente associadas à sua propriedade móvel.

![A página de detalhes da propriedade móvel é exibida. As informações sobre atividades recentes são exibidas. A guia Extensões é realçada.](./images/implement-assurance/tag-properties.png)

Selecionar **[!UICONTROL Catálogo]** para ver uma lista de extensões que você pode adicionar à propriedade móvel. Usando o filtro, localize o **[!UICONTROL AEP Assurance]** e selecione **[!UICONTROL Instalar]**.

![O catálogo de extensões é exibido. A extensão do Assurance é filtrada e exibida, com o botão de instalação realçado.](./images/implement-assurance/assurance-extension.png)

## Próximas etapas

Agora que você instalou a extensão Assurance na propriedade móvel, é possível começar a usar o Assurance nos aplicativos. Para saber como adicionar a extensão do Assurance ao seu aplicativo, leia o [Visão geral da extensão do Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Para saber como usar o Assurance, leia o [uso do guia do Assurance](./using-assurance.md).
