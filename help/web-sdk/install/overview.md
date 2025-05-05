---
title: Visão geral de instalação do SDK da Web
description: Saiba como instalar o SDK da Web do Experience Platform.
keywords: instalação do sdk da web;instalando o sdk da web;internet explorer;promessa;pacote npm
exl-id: b1de7ca1-d0d2-4661-a273-a1acf29afcd5
source-git-commit: f75dcfc945be2f45c1638bdd4d670288aef6e1e6
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 0%

---

# Visão geral de instalação do SDK da Web

Há três maneiras compatíveis de usar o SDK da Web da Adobe Experience Platform:

1. **[Extensão de tag do SDK da Web](extension.md)**: o Adobe recomenda o uso desse método. Instale um carregador de tags no site e use a interface da Coleção de dados da Adobe Experience Platform para configurar a implementação.
1. **[Biblioteca JavaScript do SDK da Web](library.md)**: faça referência a um arquivo de biblioteca hospedado em CDN ou hospede o arquivo de biblioteca usando sua própria infraestrutura. Faça chamadas para a biblioteca dentro do código do site.
1. **[NPM](npm.md)**: instale o SDK da Web no site usando o gerenciador de pacotes NPM.

## Pré-requisitos

Antes de usar ou instalar o SDK da Web, você deve atender aos seguintes requisitos:

* A arquitetura no Adobe Experience Platform deve ser configurada primeiro. Essas configurações incluem esquemas, identidades e fluxos de dados necessários.
* Você deve ter as permissões certas configuradas para acessar as ferramentas apropriadas. Por exemplo, se sua organização decidir usar a extensão de tag, você deverá ter as permissões corretas para acessar a interface da Coleção de dados. Consulte [gerenciamento de permissões de coleta de dados](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=pt-BR) para obter mais informações.
* É recomendado ter um domínio próprio (CNAME). Se você já tiver um CNAME do Adobe Analytics, poderá usá-lo. Os testes no desenvolvimento funcionam sem um CNAME, mas o Adobe recomenda ter um antes de publicar na produção. Consulte [IDs de dispositivo próprio](../identity/first-party-device-ids.md) para obter mais informações.
