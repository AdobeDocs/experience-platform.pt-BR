---
keywords: iniciar tags da Web;tags da Web iniciar;tags do site;tags da Web;iniciar;Iniciar;Iniciar
title: Tutorial Implementar tags de site com Adobe Launch
seo-title: Implementar tags de site com o Adobe Launch
description: Use o Adobe Launch para implementar tags de site no Adobe Experience Platform
seo-description: Use o Adobe Launch para implementar tags de site no Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 00010d38a5d05800aeac9af8505093fee3593b45
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 8%

---


# Tutorial: Implementar tags de site com o Adobe Launch

Este tutorial explica como implementar as tags de seu site para enviar dados para a Adobe Experience Platform usando o Adobe Launch.

## Pré-requisitos

* O schema e o conjunto de dados necessários são criados em [!DNL Platform].
* A configuração necessária foi implantada no Experience Edge e possui a ID de configuração e o domínio de borda correspondentes.
* O CMS da empresa já foi configurado para fornecer um objeto JavaScript em cada página com os dados necessários para enviar à plataforma.

## Etapas

Este tutorial contém as seguintes etapas:

1. Instale a extensão Adobe Experience Platform [!DNL Web SDK].
1. Crie uma regra para dizer [!DNL Launch] quais dados enviar.
1. Compacte a extensão e a regra em uma biblioteca.

## Instale a extensão Adobe Experience Platform [!DNL Web SDK]

Primeiro, instale a extensão Adobe Experience Platform [!DNL Web SDK].

1. Em [!DNL Launch], abra a guia **[!UICONTROL Extensões]**.

   ![imagem](assets/launch-overview.png)

1. Selecione a extensão do Adobe Experience Platform Web SDK no Catálogo de extensão de inicialização
A tela de configuração é aberta.

   ![imagem](assets/launch-extension-install.png)

   Para obter mais informações, consulte [Extensões](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) na documentação [!DNL Launch].

1. Configurar a extensão.

   As únicas configurações necessárias no momento são:

   * **ID de configuração:** especifique a ID de configuração obtida do representante do Adobe.
   * **Domínio de borda:** especifique o domínio de borda obtido do seu representante de Adobe.

1. Selecione **[!UICONTROL Salvar]** e vá para a próxima etapa.

## Crie uma regra para dizer [!DNL Launch] quais dados serão enviados

Em seguida, crie uma regra para permitir que [!DNL Launch] saiba quais dados você deseja enviar à Adobe Experience Platform e quando deseja enviá-los.

1. Na guia **[!UICONTROL Regras]**, configure um evento que será acionado em cada nova página do site quando a biblioteca [!DNL Launch] for carregada.

   ![imagem](assets/launch-make-a-rule.png)

1. Adicionar uma ação.

   Para configurar a ação, diga [!DNL Launch] onde localizar a camada de dados. A camada de dados é um objeto JavaScript que existe na página, que é entregue pelo mesmo CMS que renderiza a página da Web. Forneça o caminho do JavaScript para o objeto de dados.

   ![imagem](assets/launch-add-aep-action.png)

   O objeto de dados enviado precisa ser um XDM válido que passe a validação em relação ao schema usado pelo conjunto de dados conectado à sua ID de configuração.

1. Selecione **[!UICONTROL Manter alterações]**.

Para obter mais informações, consulte [Regras](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html) na documentação [!DNL Launch].

## Compacte a extensão e a regra em uma biblioteca

Em seguida, [agrupe a extensão](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) e a nova regra em uma biblioteca e teste essas alterações em um ambiente de desenvolvimento.

![imagem](assets/launch-add-changes-to-library.png)

Depois de concluir o teste, promova a biblioteca por meio do fluxo de trabalho para que ela possa ser implantada no site de produção. Os dados agora fluem de cada usuário individual para o Adobe Experience Platform.

![imagem](assets/launch-promote-library.png)

Para obter mais informações, consulte [Bibliotecas](https://docs.adobe.com/content/help/pt-BR/launch/using/reference/publish/libraries.html) na documentação [!DNL Launch].