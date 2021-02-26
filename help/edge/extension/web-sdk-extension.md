---
title: Extensão SDK da Web da Adobe Experience Platform Visão geral
description: Saiba mais sobre o Adobe Experience Platform Web SDK Extension for Adobe Experience Platform Launch
translation-type: tm+mt
source-git-commit: 18e511337eaa8b6eb7785b1ee5f1ce2366ddd7c7
workflow-type: tm+mt
source-wordcount: '560'
ht-degree: 19%

---


# Visão geral da extensão do Adobe Experience Platform Web SDK

A extensão Adobe Experience Platform Web SDK envia dados para a Adobe Experience Cloud de propriedades da Web por meio da Adobe Experience Platform Edge Network. A extensão permite que você faça o stream de dados para a Plataforma, sincronize identidades, processe sinais de consentimento do cliente e colete dados de contexto automaticamente.

Este documento aborda como configurar a extensão na interface do usuário do Adobe Experience Platform Launch.

## Configurar a extensão

Se a extensão SDK da Web da plataforma já tiver sido instalada para uma propriedade, abra a propriedade na interface do usuário do Platform launch e selecione a guia **[!UICONTROL Extensões]**. Em Plataforma Web SDK, selecione **[!UICONTROL Configurar]**.

![](../images/extension/overview/configure.png)

Se ainda não tiver instalado a extensão, selecione a guia **[!UICONTROL Catálogo]**. Na lista de extensões disponíveis, localize a extensão SDK da Web da plataforma e selecione **[!UICONTROL Instalar]**.

![](../images/extension/overview/install.png)

Em ambos os casos, você chega à página de configuração do SDK da Web da plataforma. As seções abaixo explicam as opções de configuração da extensão.

![](../images/extension/overview/config-screen.png)

## Opções gerais de configuração

As opções de configuração na parte superior da página informam à Adobe Experience Platform onde rotear os dados e quais configurações devem ser usadas no servidor.

### [!UICONTROL Nome]

A extensão Adobe Experience Platform Web SDK suporta várias instâncias na página. Isso é usado para enviar dados para várias organizações com uma única configuração do Platform Launch.

O nome da extensão padroniza &quot;[!DNL alloy]&quot;. No entanto, é possível alterar o nome da instância para qualquer nome de objeto JavaScript válido.

### **[!UICONTROL ID da organização IMS]**

A [!UICONTROL ID de organização IMS] é a organização para a qual você gostaria que os dados fossem enviados no Adobe. Na maioria das vezes, você deve usar o valor padrão preenchido automaticamente. Quando você tiver várias instâncias na página, preencha esse campo com o valor da segunda organização para a qual deseja enviar dados.

### **[!UICONTROL Domínio de borda]**

O [!UICONTROL Domínio de Borda] é o domínio do qual a extensão Adobe Experience Platform envia e recebe dados. A extensão requer o uso de um CNAME próprio para o tráfego de produção. O domínio padrão de terceiros funciona em ambientes de desenvolvimento, mas não é adequado para ambientes de produção. As instruções sobre como configurar um CNAME primário estão listadas [aqui](https://docs.adobe.com/content/help/pt-BR/core-services/interface/ec-cookies/cookies-first-party.html).

## [!UICONTROL Configurações do Edge]

Quando uma solicitação é enviada para a Adobe Experience Platform Edge Network, uma ID de configuração de borda é usada para fazer referência à configuração do servidor. Isso permite que você atualize a configuração sem precisar fazer alterações de código em seu site.

Consulte o guia em [configurações de borda](../fundamentals/edge-configuration.md) para obter mais informações.

## [!UICONTROL Privacidade]

A seção [!UICONTROL Privacy] permite que você configure como o SDK lida com os sinais de consentimento do cliente em seu site. Especificamente, permite selecionar o nível padrão de consentimento que é assumido de um cliente se nenhuma outra preferência de consentimento explícita tiver sido fornecida. A tabela a seguir detalha o que cada opção implica:

| [!UICONTROL Nível de Consentimento Padrão] | Descrição |
| --- | --- |
| [!UICONTROL Em] | Aceitar. Use essa opção se você assumir o consentimento do cliente por padrão e apenas seguir os sinais de recusa. |
| [!UICONTROL Pending] | Pressupõe-se que os clientes com consentimento &quot;pendente&quot; sejam opt out até que um sinal de aceitação seja enviado. Use essa opção se você precisar de consentimento explícito do cliente para suas operações comerciais. |
| [!UICONTROL Fornecido pelo elemento de dados] | O nível de consentimento padrão é determinado por um elemento de dados separado que você define. Ao usar essa opção, você deve especificar o elemento de dados usando o menu suspenso fornecido. |