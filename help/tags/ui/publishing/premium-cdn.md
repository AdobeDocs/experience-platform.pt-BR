---
title: Tags do Experience Platform (China)
description: Saiba mais sobre o recurso Tags de Experience Platform (China) para tags e como ele pode ser usado para fornecer seu conteúdo em várias regiões geográficas.
exl-id: 33e36d3b-9e21-44a8-8498-32a5fc20b46b
source-git-commit: 9c39fd5d0353cc171230818d79ac213ce200dc1e
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Tags do Experience Platform (China)

Ao usar um [host gerenciado por Adobe](./hosts/managed-by-adobe-host.md) para entregar ativos de tags da Adobe Experience Platform em seu site, esses ativos são distribuídos entre várias redes de entrega de conteúdo (CDNs) no mundo inteiro para fornecer a velocidade de download mais rápida. No entanto, há determinadas regiões que exigem que todos os ativos do site sejam replicados e hospedados em um servidor nessa região.

Para levar em conta isso, as tags no Experience Platform fornecem um recurso Tags de Experience Platform (China) que permite fornecer conteúdo a essas regiões especiais.

O suporte a Tags de Experience Platform (China) é um recurso pago e deve ser adquirido por sua organização para permitir e usá-lo. Este guia aborda como configurar e usar esse recurso na interface do usuário do Experience Platform ou na interface da coleção de dados após a compra.

## Habilitar tags Experience Platform (China) para sua organização

Tags de Experience Platform (China) ativadas no nível da empresa. Depois que sua organização comprar o recurso Tags de Experience Platform (China), um administrador de Adobe habilitará o recurso na interface para sua empresa.

## Recriar e instalar bibliotecas de tags com códigos incorporados atualizados

Depois que as Tags do Experience Platform (China) são ativadas, isso não significa que os seus ativos de tags são imediatamente replicados e prontos para uso nas novas regiões. Isso significa apenas que agora é possível escolher quando aceitar essa funcionalidade.

>[!IMPORTANT]
>
>As bibliotecas criadas antes da ativação de tags na China continuarão a operar como estão exatamente como hoje. Isso também se aplica a bibliotecas não gerenciadas pelo Adobe, já que [ambientes arquivados](./environments.md#archive) usam URLs relativas somente para seus caminhos de ativos. Observe que, após ativar as Tags de Experience Platform (China), qualquer biblioteca criada que não seja gerenciada pelo Adobe se comportará como se o recurso Tags na China não estivesse ativado.

Depois de ativar as tags na China e recriar as bibliotecas que deseja usar nas novas regiões de hospedagem, você pode recuperar os códigos incorporados da nova região de hospedagem para adicionar aos seus sites.

>[!NOTE]
>
>O código de inserção da biblioteca listado na região de hospedagem [!UICONTROL Padrão] continuará a funcionar como está, bem como quaisquer códigos de inserção de Topo ou de Base da página que já estejam nos seus sites.

Visite a página **[!UICONTROL Ambientes]** ou exiba as instruções de instalação do ambiente na tela de edição da biblioteca para encontrar os novos códigos incorporados. Cada nova região de hospedagem com suporte aparece após a região de hospedagem [!UICONTROL Padrão] (usada para áreas no mundo que têm suporte sem Tags de Experience Platform (China)). A captura de tela abaixo mostra um código de inserção para a região da China, que usa `.cn` como seu domínio de nível superior (TLD).

![Incorporar código para a região da China](../../images/ui/publishing/premium-cdn/embed-codes.png)

Escolha o código de inserção apropriado para a página da Web e cole-o na marca `<head>` do seu documento. Para obter mais informações sobre como usar os códigos de inserção para instalar bibliotecas de tags, consulte o [guia da interface do usuário de ambientes](./environments.md#installation).

## Próximas etapas

Este guia abordou como ativar e instalar o recurso Tags do Experience Platform (China) para a implementação de tags. Para obter mais informações sobre como instalar e testar bibliotecas de marcas em suas propriedades da Web e móveis, consulte a [visão geral de publicação](./overview.md).
