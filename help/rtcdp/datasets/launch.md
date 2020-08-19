---
keywords: website tags;web tags;launch tutorial
title: Tutorial Implementar tags de site com Adobe Launch
seo-title: Implementar tags de site com o Adobe Launch
description: Use o Adobe Launch para implementar tags de site no Adobe Experience Platform
seo-description: Use o Adobe Launch para implementar tags de site no Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 15323134f0c626cad2c4e90b3e1c0662cf7e57dd
workflow-type: tm+mt
source-wordcount: '475'
ht-degree: 9%

---


# Tutorial: Implementar tags de site com o Adobe Launch

Este tutorial explica como implementar as tags de seu site para enviar dados para a Adobe Experience Platform usando o Adobe Launch.

## Pré-requisitos

* O schema e o conjunto de dados necessários são criados em [!DNL Platform].
* A configuração necessária foi implantada em [!DNL Experience Edge] e tem a ID de configuração e o [!DNL Edge] domínio correspondentes.
* O CMS da empresa já foi configurado para fornecer um objeto JavaScript em cada página com os dados necessários para enviar [!DNL Platform].

## Etapas

Este tutorial contém as seguintes etapas:

1. Instale a [!DNL Web SDK] extensão Adobe Experience Platform.
1. Crie uma regra para informar [!DNL Launch] quais dados serão enviados.
1. Compacte a extensão e a regra em uma biblioteca.

## Instale a [!DNL Web SDK] extensão Adobe Experience Platform

Primeiro, instale a [!DNL Web SDK] extensão Adobe Experience Platform.

1. Em [!DNL Launch], abra a guia **[!UICONTROL Extensões]** .

   ![imagem](assets/launch-overview.png)

1. Selecione a extensão do Adobe Experience Platform Web SDK na [!DNL Launch] extensão [!DNL Catalog]A tela de configuração é aberta.

   ![imagem](assets/launch-extension-install.png)

   Para obter mais informações, consulte [Extensões](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) na [!DNL Launch] documentação.

1. Configurar a extensão.

   As únicas configurações necessárias no momento são:

   * **ID de configuração:** Especifique a ID de configuração obtida do seu representante de Adobe.
   * **Domínio de borda:** Especifique o domínio de borda obtido do seu representante de Adobe.

1. Clique em **[!UICONTROL Salvar]** e prossiga para a próxima etapa.

## Criar uma regra para informar [!DNL Launch] quais dados serão enviados

Em seguida, crie uma regra para [!DNL Launch] saber quais dados você deseja enviar à Adobe Experience Platform e quando deseja enviá-los.

1. Na guia **[!UICONTROL Regras]** , configure um evento que será acionado em cada nova página do site quando a [!DNL Launch] biblioteca for carregada.

   ![imagem](assets/launch-make-a-rule.png)

1. Adicionar uma ação.

   Para configurar a ação, diga [!DNL Launch] onde localizar sua camada de dados. A camada de dados é um objeto JavaScript que existe na página, que é entregue pelo mesmo CMS que renderiza a página da Web. Forneça o caminho do JavaScript para o objeto de dados.

   ![imagem](assets/launch-add-aep-action.png)

   O objeto de dados enviado precisa ser um XDM válido que passe a validação em relação ao schema usado pelo conjunto de dados conectado à sua ID de configuração.

1. Clique em **[!UICONTROL Manter alterações]**.

Para obter mais informações, consulte [Regras](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/manage-resources/rules.html) na [!DNL Launch] documentação.

## Compacte a extensão e a regra em uma biblioteca

Em seguida, [agrupe a extensão](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/publish/overview.html) e a nova regra em uma biblioteca e teste essas alterações em um ambiente de desenvolvimento.

![imagem](assets/launch-add-changes-to-library.png)

Depois de concluir o teste, promova a biblioteca por meio do fluxo de trabalho para que ela possa ser implantada no site de produção. Os dados agora fluem de cada usuário individual para o Adobe Experience Platform.

![imagem](assets/launch-promote-library.png)

Para obter mais informações, consulte [Bibliotecas](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/publish/libraries.html) na [!DNL Launch] documentação.