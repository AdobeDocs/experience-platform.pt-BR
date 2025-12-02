---
title: Configurações da instância do SDK
description: Defina as configurações gerais para a instância do Web SDK.
source-git-commit: 09799847c61d82ed5b7cd372d92aa436697d54f3
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 2%

---

# Configurações da instância do SDK

Essa seção de configuração controla o nome da instância do Web SDK, a organização IMS à qual ela se aplica e o local para o qual você deseja enviar dados. Por padrão, uma instância é nomeada `alloy`.

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensions]** e selecione **[!UICONTROL Configure]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Localize o nome da instância logo abaixo da opção [!UICONTROL SDK instances] expandida.

![Imagem mostrando as configurações gerais da extensão de marca do Web SDK na interface do usuário de Marcas](../assets/web-sdk-ext-general.png)

As opções disponíveis são as seguintes:

## [!UICONTROL Name]

A extensão de tag do Adobe Experience Platform Web SDK é compatível com várias instâncias na página. O nome é usado para enviar dados para várias organizações sem exigir bibliotecas de tags duplicadas da Web SDK. Você pode alterar o nome da instância para qualquer nome de objeto JavaScript válido.

## [!UICONTROL IMS organization ID]

A ID da organização para a qual você deseja que os dados da Adobe sejam enviados. Na maioria das vezes, use o valor padrão preenchido automaticamente. Quando houver várias instâncias na página, preencha esse campo com o valor da segunda organização para a qual deseja enviar dados.

## [!UICONTROL Edge domain]

O domínio do qual a extensão envia e recebe dados. Embora o valor padrão de `edge.adobedc.net` funcione, a Adobe recomenda usar um domínio próprio na maioria dos casos. Consulte o [programa de certificados gerenciados pela Adobe](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/data-collection/adobe-managed-cert) para obter instruções sobre como configurar um domínio próprio adequado para a coleta de dados. Consulte também [`edgeDomain`](/help/collection/js/commands/configure/edgedomain.md) na documentação da biblioteca de JavaScript para obter orientação sobre como configurar esse valor.
