---
title: Tutorial Implementar tags de site com o Adobe Launch
seo-title: Implementar tags de site com o Adobe Launch
description: Usar o Adobe Launch para implementar tags de site na Adobe Experience Platform
seo-description: Usar o Adobe Launch para implementar tags de site na Adobe Experience Platform
translation-type: tm+mt
source-git-commit: 3083f6fb25a331eb6dd1d9a63b65aa206481dcb3

---


# Tutorial: Implementar tags de site com o Adobe Launch

Este tutorial explica como implementar as tags de seu site para enviar dados para a Adobe Experience Platform usando o Adobe Launch.

## Pré-requisitos

* O esquema e o conjunto de dados necessários são criados na Plataforma.
* A configuração necessária foi implantada no Experience Edge e possui a ID de configuração e o domínio de borda correspondentes.
* O CMS da empresa já foi configurado para fornecer um objeto JavaScript em cada página com os dados necessários para enviar à Plataforma.

## Etapas

Este tutorial contém as seguintes etapas:

1. Instale a extensão do SDK da Web do Adobe Experience Platform.
1. Crie uma regra para informar ao Launch quais dados serão enviados.
1. Compacte a extensão e a regra em uma biblioteca.

## Instalar a extensão do SDK da Web do Adobe Experience Platform

Primeiro, instale a extensão do SDK da Web do Adobe Experience Platform.

1. No Launch, abra a guia **[!UICONTROL Extensions]**.

   ![image](assets/launch-overview.png)

1. Selecione a extensão do SDK da Web do Adobe Experience Platform no Catálogo de extensões de inicializaçãoA tela de configuração é aberta.

   ![image](assets/launch-extension-install.png)

   Para obter mais informações, consulte [Extensões](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/extensions/overview.html) na documentação do Launch.

1. Configurar a extensão.

   As únicas configurações necessárias no momento são:

   * **ID de configuração:** Especifique a ID de configuração obtida de seu representante da Adobe.
   * **Domínio de borda:** Especifique o domínio de borda obtido do seu representante da Adobe.

1. Clique **[!UICONTROL Save]** e continue para a próxima etapa.

## Criar uma regra para informar ao Launch quais dados serão enviados

Em seguida, crie uma regra para permitir que o Launch saiba quais dados você deseja enviar para a Adobe Experience Platform e quando deseja enviá-los.

1. Na **[!UICONTROL Rules]** guia, configure um evento que será acionado em cada nova página do site quando a biblioteca Iniciar for carregada.

   ![image](assets/launch-make-a-rule.png)

1. Adicionar uma ação.

   Para configurar a ação, informe Iniciar onde localizar a camada de dados. A camada de dados é um objeto JavaScript que existe na página, que é entregue pelo mesmo CMS que renderiza a página da Web. Forneça o caminho do JavaScript para o objeto de dados.

   ![image](assets/launch-add-aep-action.png)

   O objeto de dados enviado precisa ser um XDM válido que passe a validação em relação ao esquema usado pelo conjunto de dados conectado à sua ID de configuração.

1. Clique em **[!UICONTROL Keep Changes]**.

Para obter mais informações, consulte [Regras](https://docs.adobe.com/content/help/en/launch/using/reference/manage-resources/rules.html) na documentação Iniciar.

## Compacte a extensão e a regra em uma biblioteca

Em seguida, [agrupe a extensão](https://docs.adobe.com/content/help/en/launch/using/reference/publish/overview.html) e a nova regra em uma biblioteca e teste essas alterações em um ambiente de desenvolvimento.

![image](assets/launch-add-changes-to-library.png)

Depois de concluir o teste, promova a biblioteca por meio do fluxo de trabalho para que ela possa ser implantada no site de produção. Os dados agora fluem de cada usuário individual para a Adobe Experience Platform.

![image](assets/launch-promote-library.png)

Para obter mais informações, consulte [Bibliotecas](https://docs.adobe.com/content/help/en/launch/using/reference/publish/libraries.html) na documentação do Launch.