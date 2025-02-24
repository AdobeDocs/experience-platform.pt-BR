---
title: Visão geral da extensão do Adobe Content Analytics
description: Saiba mais sobre a extensão de tag do Adobe Content Analytics no Adobe Experience Platform.
hide: true
hidefromtoc: true
source-git-commit: d6288d9515d7efaf874cb056f06d04b2002fd369
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 0%

---

# Visão geral da extensão do Adobe Content Analytics

A extensão de tag [!DNL Adobe Content Analytics] permite o rastreamento de eventos relacionados a conteúdo em um site. A extensão envia dados de conteúdo (experiências e ativos) para uma sequência de dados no Adobe Experience Cloud a partir das propriedades da Web por meio do Experience Platform Edge Network.

A extensão permite transmitir dados de evento relacionados a conteúdo específico para a Platform, para que você possa usar esses dados em seus relatórios de análise de conteúdo no Customer Journey Analytics.

Este documento explica como configurar a extensão de tag na interface do usuário de tags.

## Instalar a extensão de tag do Adobe Content Analytics {#install}

>[!NOTE]
>
>A extensão de marca do Adobe Content Analytics é instalada automaticamente como parte da propriedade de marca criada automaticamente ao usar o [assistente de configuração guiado do Content Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided){target="_blank"}.


### Instalação manual

No caso de uma configuração manual, a extensão de tag do Adobe Content Analytics precisa de uma propriedade para ser instalada no. Se ainda não tiver feito isso, consulte a documentação sobre [criação de uma propriedade de marca](https://experienceleague.adobe.com/en/docs/platform-learn/implement-in-websites/configure-tags/create-a-property).

Após criar uma propriedade ou ao selecionar a propriedade criada usando o [assistente de configuração guiada do Content Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided), abra a propriedade e selecione a guia **[!UICONTROL Extensões]** na barra lateral esquerda.

Selecione a guia **[!UICONTROL Catálogo]**. Na lista de extensões disponíveis, localize a extensão **[!DNL Adobe Content Analytics]** e selecione **[!UICONTROL Instalar]**.

![Imagem mostrando a interface do usuário de Marcas com a extensão do Web SDK selecionada](assets/aca-tag-install.png)

Depois de selecionar **[!UICONTROL Instalar]**, você deve configurar a extensão de tag do Adobe Content Analytics e salvar a configuração.


<!--
## Configure schema

The [Content Analytics guided configuration wizard](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided) automatically populates the proper value for the **[!UICONTROL Tenant Schema Name]**. 

![Image that shows the Schema configuration of the Adobe Content Analytics tag extension in the Tags UI](assets/aca-tag-schema.png)

>[!WARNING]
>
>Do not modify the value for **[!UICONTROL Tenant Schema Name]**.

-->

## Configurar datastreams

O [assistente de configuração guiada do Content Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided) seleciona automaticamente o valor adequado da **[!UICONTROL Sandbox]** e da **[!UICONTROL Sequência de Dados de Produção]**. Opcionalmente, você pode configurar uma **[!UICONTROL Sequência de Dados de Preparo]** e uma **[!UICONTROL Sequência de Dados de Desenvolvimento]** adicionais.

![Imagem que mostra a configuração de Sequências de Dados da extensão de marca do Adobe Content Analytics na interface de Marcas](assets/aca-tag-datastreams.png)

Você pode substituir os valores selecionados automaticamente para **[!UICONTROL Sandbox]** e **[!UICONTROL Sequência de dados de produção]** caso queira usar o Content Analytics em uma sandbox diferente e com sequências de dados diferentes. Ao fazer isso, você pode selecionar uma sandbox e sequências de dados nos menus suspensos disponíveis ou selecionar **[!UICONTROL Inserir valores]** e inserir uma ID de sequência de dados personalizada para cada ambiente.

>[!IMPORTANT]
>
>Ao configurar outra sandbox e fluxos de dados, verifique se
>
>* a sandbox selecionada ainda não está associada a outra configuração do Content Analytics e
>* qualquer sequência de dados selecionada tem o serviço Experience Platform configurado com um conjunto de dados de evento de experiência do Content Analytics habilitado.

Consulte o guia em [datastreams](../../../../datastreams/overview.md) para saber como configurar um datastream.



## Configurar a filtragem de eventos

Na seção **[!UICONTROL Filtragem de Eventos]**, você pode modificar as expressões regulares para filtrar **[!UICONTROL URLs de Páginas]** e **[!UICONTROL URLs de Assets]** ao coletar dados para a Análise de Conteúdo. As expressões regulares definidas no [assistente de configuração guiada do Content Analytics](https://experienceleague.adobe.com/en/docs/analytics-platform/using/content-analytics/configuration/guided) são preenchidas automaticamente.

![Imagem mostrando as configurações de filtragem de eventos da extensão de marca do Adobe Content Analytics na interface de Marcas](assets/aca-tag-eventfiltering.png)


### Exemplos

* Você deseja excluir todas as páginas de documentação do Content Analytics.<br/>Usar a seguinte expressão regular: `^(?!.*documentation).*`
* Você deseja excluir todas as imagens de logotipo do JPEG e do SVG do Content Analytics.<br/>Usar a seguinte expressão regular: `^(?!.*(logo\.jpg|\.svg)).*$`

Você pode usar **[!UICONTROL Testar Regex]** para testar sua expressão regular no **[!UICONTROL Testador de Expressão Regular]**.

![Imagem mostrando o testador de expressão regular da extensão de marca do Adobe Content Analytics na interface do usuário de Marcas](assets/aca-tag-regextester.png)

