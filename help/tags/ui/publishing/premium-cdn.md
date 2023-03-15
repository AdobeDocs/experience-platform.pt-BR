---
title: Suporte Premium à CDN para tags
description: Saiba mais sobre o recurso CDN premium para tags e como ele pode ser usado para fornecer seu conteúdo em várias regiões geográficas.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 8ded2aed32dffa4f0923fedac7baf798e68a9ec9
workflow-type: tm+mt
source-wordcount: '540'
ht-degree: 0%

---

# Suporte Premium à CDN para tags (Beta)

>[!IMPORTANT]
>
>O recurso CDN premium para tags está atualmente na versão beta e sua organização pode ainda não ter acesso a ele. Esta documentação está sujeita a alterações.

Quando você usa um [Host gerenciado por Adobe](./hosts/managed-by-adobe-host.md) para fornecer os ativos de tags da Adobe Experience Platform em seu site, esses ativos são distribuídos entre várias redes de entrega de conteúdo (CDNs) em todo o mundo para fornecer a velocidade de download mais rápida. No entanto, há determinadas regiões que exigem que todos os ativos do site sejam replicados e hospedados em um servidor nessa região.

Para levar em conta isso, as tags no Experience Platform fornecem um recurso CDN premium que permite fornecer conteúdo a essas regiões especiais.

O suporte CDN Premium é um recurso pago e deve ser adquirido pela sua organização para ser habilitado e usado. Este guia aborda como configurar e usar esse recurso na interface do usuário do Experience Platform ou na interface da coleção de dados após a compra.

## Habilitar a CDN premium para sua organização

O CDN Premium é ativado no nível da empresa. Depois que sua organização comprar o recurso CDN premium, um administrador de Adobe habilitará o recurso na interface do usuário para sua empresa.

## Recriar e instalar bibliotecas de tags com códigos incorporados atualizados

Depois que o CDN premium é ativado, isso não significa que os ativos de tag são replicados imediatamente e estão prontos para uso nas novas regiões. Isso significa apenas que agora é possível escolher quando aceitar essa funcionalidade.

>[!IMPORTANT]
>
>As bibliotecas criadas antes da ativação da CDN premium continuarão a operar como estão exatamente como fazem hoje. Isso também se aplica a bibliotecas não gerenciadas pelo Adobe, pois [ambientes arquivados](./environments.md#archive) usar URLs relativos somente para seus caminhos de ativos. Observe que após ter ativado o CDN premium, qualquer biblioteca criada que não seja gerenciada pelo Adobe se comportará como se o recurso CDN premium não estivesse ativado.

Depois de habilitar o CDN premium e recriar as bibliotecas que deseja usar nas novas regiões de hospedagem, você pode recuperar os novos códigos incorporados da região de hospedagem para adicionar aos sites.

>[!NOTE]
>
>O código incorporado da biblioteca que está listado no [!UICONTROL Padrão] A região de hospedagem continuará a funcionar como está, bem como quaisquer códigos incorporados de Topo ou de Base da página que já estejam em seus sites.

Visite o **[!UICONTROL Ambientes]** ou visualize as instruções de instalação do ambiente na tela editar biblioteca para localizar os novos códigos incorporados. Cada nova região de hospedagem compatível é exibida após a variável [!UICONTROL Padrão] região de hospedagem (usada para áreas no mundo compatíveis sem CDN premium). A captura de tela abaixo mostra um código integrado para a região da China, que usa `.cn` como seu domínio de nível superior (TLD).

![Código de inserção para a região da China](../../images/ui/publishing/premium-cdn/embed-codes.png)

Escolha o código incorporado apropriado para a página da Web e cole-o na `<head>` do seu documento. Para obter mais informações sobre como usar os códigos incorporados para instalar bibliotecas de tags, consulte o [guia da interface do usuário de ambientes](./environments.md#installation).

## Próximas etapas

Este guia abordou como ativar e instalar o recurso CDN premium para a implementação de tags. Para obter mais informações sobre como instalar e testar bibliotecas de tags na Web e em propriedades móveis, consulte o [visão geral da publicação](./overview.md).
