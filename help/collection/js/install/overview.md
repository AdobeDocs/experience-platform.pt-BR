---
title: Visão geral da instalação do Web SDK
description: Saiba como instalar o Experience Platform Web SDK.
keywords: instalação do sdk da web;instalando o sdk da web;internet explorer;promessa;pacote npm
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: a490c429047f5e5997d69f30a51e6b78debe2d5d
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 0%

---

# Visão geral da instalação do Web SDK

Há três maneiras compatíveis de usar o Adobe Experience Platform Web SDK:

1. **[Extensão de marca do Web SDK](/help/tags/extensions/client/web-sdk/overview.md)**: a Adobe recomenda usar esse método. Instale um carregador de tags no site e use a interface da Coleção de dados da Adobe Experience Platform para configurar a implementação.
1. **[Biblioteca JavaScript do Web SDK](library.md)**: faça referência a um arquivo de biblioteca hospedado em CDN ou hospede o arquivo de biblioteca usando sua própria infraestrutura. Faça chamadas para a biblioteca dentro do código do site.
1. **[NPM](npm.md)**: instale o Web SDK no site usando o gerenciador de pacotes NPM.

## Pré-requisitos

Antes de usar ou instalar o Web SDK, você deve atender aos seguintes requisitos:

* A arquitetura no Adobe Experience Platform deve ser configurada primeiro. Essas configurações incluem esquemas, identidades e fluxos de dados necessários.
* Você deve ter as permissões certas configuradas para acessar as ferramentas apropriadas. Por exemplo, se sua organização decidir usar a extensão de tag, você deverá ter as permissões corretas para acessar a interface da Coleção de dados. Consulte [Permissões de coleção de dados](../../permissions.md) para obter mais informações.
* É recomendado ter um domínio próprio (CNAME). Se você já tiver um CNAME do Adobe Analytics, poderá usá-lo. Os testes no desenvolvimento funcionam sem um CNAME, mas a Adobe recomenda ter um antes de publicar na produção. Consulte [IDs de dispositivo próprio](../../use-cases/identity/first-party-device-ids.md) para obter mais informações.
