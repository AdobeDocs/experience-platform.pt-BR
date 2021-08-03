---
title: Visão geral da extensão do Adobe Experience Manager Forms
description: Saiba mais sobre a extensão de tag do Adobe Experience Manager Forms no Adobe Experience Platform.
source-git-commit: f31a1d2e84dee262e04f1db0415ffd76248ecb6c
workflow-type: tm+mt
source-wordcount: '316'
ht-degree: 6%

---

# Visão geral da extensão do Adobe Experience Manager Forms

Este documento fornece uma visão geral da extensão de tag do Adobe Experience Manager Forms no Adobe Experience Platform.

## Eventos

Os seguintes tipos de evento são fornecidos pela extensão :

1. **Renderizar**: Aciona quando o usuário renderiza (abre) um formulário.
1. **Erro**: Aciona quando o usuário comete um erro de validação em um formulário.
1. **Ajuda**: Aciona quando o usuário clica no ícone de ajuda de um campo.
1. **Enviar**: Acionadores no envio do formulário.
1. **Visita** ao campo: Aciona quando um campo é visitado.
1. **Abandono**: Aciona quando o usuário fecha a guia ou navega para um URL diferente.
1. **Salvar**: Aciona quando um formulário é salvo no portal.

>[!IMPORTANT]
>
>O evento Salvar não está disponível no momento para formulários como um serviço em nuvem. Os eventos personalizados despachados pelo editor de regras no Adaptive Forms podem ser capturados usando o evento principal &quot;Capturar evento personalizado&quot;.

## Elementos de dados

A extensão fornece vários elementos de dados que podem ser usados para enviar propriedades em chamadas do Analytics.

## Introdução

Siga as etapas abaixo para começar a usar a extensão .

1. Instale a extensão Adobe Experience Manager Forms no catálogo de extensões. Nenhuma configuração adicional é necessária após a instalação.
2. Instale e configure a extensão [Adobe Analytics](../analytics/overview.md#Configure-the-Adobe-Analytics-extension).

## Criação de uma regra

Uma regra que utiliza a extensão Experience Manager Forms seria semelhante ao seguinte:

![Configuração de ação](./images/rule.png)

Siga as etapas descritas abaixo para criar uma regra semelhante para sua implementação.

### Adicionar um evento

1. Selecione **Adobe Experience Manager Forms** na lista suspensa de extensão.
2. Selecione o evento a ser capturado.

![Configuração de ação](./images/AEM-forms-event.png)

### Adicionar uma ação

1. Selecione &quot;Adobe Analytics&quot; na lista suspensa de extensões.
2. Selecione &quot;definir variável&quot; na lista suspensa Tipo de ação.
3. Na visualização de configuração, escolha as propriedades e os eventos a serem enviados.
4. Adicione uma ação &quot;enviar beacon&quot; para enviar a chamada do Analytics com eventos e propriedades definidos na etapa 3
   ![Configuração de ação](./images/AEM-forms-sendBeacon.png)
5. Adicione uma ação &quot;limpar variável&quot;.

![Configuração de ação](./images/AEM-forms-action.png)