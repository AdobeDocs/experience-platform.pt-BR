---
title: Implementação da extensão Adobe Experience Platform Assurance
description: Este guia explica como implementar e instalar a extensão Adobe Experience Platform Assurance.
source-git-commit: 24f452bdb923179eefe53fdb28d3a92d43e533cd
workflow-type: tm+mt
source-wordcount: '400'
ht-degree: 2%

---


# Implementação da extensão Adobe Experience Platform Assurance

Este tutorial explica como instalar e implementar a extensão do Platform Assurance no SDK móvel. Para obter instruções sobre como adicionar a extensão Assurance à sua aplicação, leia o [Visão geral da extensão do Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app).

## Introdução

Para instalar e implementar a extensão Assurance, você precisará acessar os seguintes serviços:

- O [Interface do usuário da coleta de dados do Adobe Experience Platform](https://experience.adobe.com/#/data-collection/)
- [Adobe Experience Platform Assurance](https://experience.adobe.com/assurance)

## Criar uma propriedade móvel

>[!NOTE]
>
>Se você já tiver uma propriedade móvel, poderá prosseguir para a próxima etapa.

Na interface do usuário da coleta de dados, selecione **[!UICONTROL Tags]**. Uma lista de propriedades móveis e da Web é exibida, com informações sobre as propriedades que pertencem à sua organização. Selecionar **[!UICONTROL Nova propriedade]** para criar uma nova propriedade.

![O botão Nova propriedade é realçado, mostrando o que você selecionou para criar uma nova propriedade](./images/implement-assurance/create-new-property.png)

O **[!UICONTROL Criar propriedade]** será exibida. Insira o nome da nova propriedade e selecione **[!UICONTROL Celular]** como sua plataforma. Depois de inserir seus detalhes, selecione **[!UICONTROL Salvar]** para criar a propriedade móvel.

>[!NOTE]
>
>O **[!UICONTROL Privacidade]** definir faz **not** afetam a coleta de dados do Assurance.

![A página Criar propriedade é exibida. Você pode inserir informações sobre sua propriedade móvel aqui.](./images/implement-assurance/create-property.png)

## Instalar a extensão Assurance

Selecione a propriedade móvel na qual deseja instalar a extensão Assurance.

![A página Propriedades da tag é exibida, com a propriedade móvel selecionada realçada.](./images/implement-assurance/select-mobile-property.png)

O **detalhes da propriedade móvel** será exibida. Selecionar **[!UICONTROL Extensões]** para exibir uma lista das extensões associadas à propriedade móvel no momento.

![A página de detalhes da propriedade móvel é exibida. As informações sobre atividades recentes são exibidas. A guia Extensões é realçada.](./images/implement-assurance/tag-properties.png)

Selecionar **[!UICONTROL Catálogo]** para ver uma lista de extensões que podem ser adicionadas à propriedade móvel. Com o filtro , localize a variável **[!UICONTROL Garantia da AEP]** e selecione **[!UICONTROL Instalar]**.

![O catálogo de extensões é exibido. A extensão Assurance é filtrada por e exibida, com o botão de instalação realçado.](./images/implement-assurance/assurance-extension.png)

## Próximas etapas

Agora que você instalou a extensão Assurance em sua propriedade móvel, pode começar a usar o Assurance em seus aplicativos. Para saber como adicionar a extensão Assurance ao seu aplicativo, leia o [Visão geral da extensão do Adobe Experience Platform Assurance](https://developer.adobe.com/client-sdks/documentation/platform-assurance-sdk/#add-the-aep-assurance-extension-to-your-app). Para saber como usar o Controle de qualidade, leia o [usando o guia de Controle](./using-assurance.md).
