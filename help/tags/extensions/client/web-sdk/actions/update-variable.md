---
title: Atualizar variável
description: Modifica o conteúdo de um elemento de dados variável.
source-git-commit: f87e6a0e969aa0924656cdb2ea56aa79d2d7c841
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 0%

---

# Atualizar variável

A ação **[!UICONTROL Update variable]** permite fazer alterações parciais ou incrementais em um [elemento de dados de variável](../data-element-types.md#variable). Você pode usar esta ação para compilar um objeto que pode ser referenciado posteriormente em uma ação [[!UICONTROL Send event]](send-event.md). Preencher elementos de dados e atribuí-los a propriedades em um objeto XDM se encaixa na maioria dos casos de uso; essa ação oferece mais flexibilidade para permitir que você defina propriedades condicionalmente para diferentes elementos de dados com base nas condições da regra.

Antes de usar essa ação, você já deve ter um elemento de dados variável criado. Depois de selecionar um elemento de dados variável para modificar, um editor é exibido, permitindo que você defina os campos desejados para essa ação.

![Captura de tela da ação de atualização de variável na interface de configuração de ação](../assets/update-variable.png)

O esquema XDM usado no editor corresponde ao esquema selecionado no elemento de dados da variável. Você pode definir uma ou mais propriedades do objeto expandindo objetos e selecionando as propriedades desejadas. Por exemplo, na captura de tela abaixo, a propriedade `producedBy` está definida como o elemento de dados `%Produced by data element%`.

![Captura de tela da interface de configuração de ação mostrando uma propriedade atualizada](../assets/update-variable-set-property.png)

Se você selecionar um elemento de dados variável que use um objeto de dados em vez de um objeto XDM, os campos disponíveis dependerão dos produtos selecionados ao configurar o elemento de dados. Por exemplo, se você criar um objeto de dados que inclua Adobe Analytics, os campos, selecionar o elemento de dados variável nessa interface forneceria campos que você pode preencher específicos para o Adobe Analytics.

![Captura de tela da interface de configuração de ação mostrando um elemento de dados variável com base em um objeto de dados](../assets/variable-data-element-data.png)
