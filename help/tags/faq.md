---
title: Tags Troubleshooting Guide
description: Obtenha respostas a perguntas frequentes sobre tags na Adobe Experience Platform.
exl-id: c06b8e25-4d79-4a11-94da-94ac096b5e33
source-git-commit: 2181ec15f2d868d1821a5f9926729d2796f2f298
workflow-type: tm+mt
source-wordcount: '1042'
ht-degree: 80%

---

# Guia de solução de problemas de tags

>[!NOTE]
>
>Adobe Experience Platform Launch has been rebranded as a suite of data collection technologies in Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](./term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Este documento fornece respostas a perguntas frequentes sobre tags na Adobe Experience Platform.

## O que são tags?

As tags são a próxima geração de recursos de gerenciamento de tags fornecidos pela Adobe, incorporados à Adobe Experience Platform. As tags permitem que os clientes:

- Implantar produtos da Web do lado do cliente usando integrações chamadas de *extensões*
- Fornecer configuração dinamicamente para atualizar as implementações do cliente em aplicativos móveis nativos
- Capturar, definir, gerenciar e compartilhar dados de maneira consistente entre os produtos de marketing e publicidade de outros fornecedores e da Adobe

As tags são um sistema avançado de entrega de código e configuração que avalia condições e executa ações para implantar bibliotecas e produtos do lado do cliente de maneira eficiente. Também oferecem uma abordagem altamente escalável para gerenciar e criar integrações e têm um conjunto robusto de APIs para interação programática.

## Quanto custam as tags?

Não há custo adicional para tags. Elas estão disponíveis para qualquer cliente da [!DNL Adobe Experience Cloud].

## Ouvi dizer que existem plug-ins agora. De que isso se trata?

As tags são criadas na Adobe Experience Platform e são totalmente extensíveis. Clientes, parceiros da Adobe, agências e fornecedores de tecnologia de marketing ou publicidade podem criar uma extensão de tag que adiciona nova funcionalidade ou modifica a funcionalidade existente. O sistema permite que os parceiros e clientes criem, gerenciem e atualizem suas próprias integrações. Essa é apenas uma das formas como a Adobe está expandindo a Adobe Experience Platform para que os clientes e parceiros possam integrar produtos e negócios a ela. Isso ajuda todos a conectarem a tecnologia da Adobe às tecnologias de marketing e publicidade de outros fornecedores com mais facilidade.

## Todas as extensões de terceiros estarão disponíveis imediatamente?

As extensões já estão disponíveis para soluções da Adobe e um grande e crescente número de fornecedores e tecnologias independentes de análise, marketing, publicidade e consentimento. Continuamos trabalhando com nossos parceiros para expandir o ecossistema. Como as extensões podem ser criadas, gerenciadas e atualizadas pelos proprietários da tecnologia, os clientes não precisam aguardar até que a engenharia da Adobe as crie.

## Quando os clientes ou parceiros podem criar extensões?

As tags abriram um portal de autoatendimento virtual, que os desenvolvedores de extensões podem usar para criar suas próprias integrações com a Adobe Cloud Platform.

Temos muitos clientes que também optam por criar suas próprias extensões privadas para usar somente em suas próprias empresas usando os mesmos métodos de desenvolvimento de extensão.

## As tags atendem aos padrões de segurança de minha empresa?

As tags estão prontas para SOC-2 e Gramm-Leach-Bliley Act. As tags também podem ser auto-hospedadas. As bibliotecas JavaScript e as configurações móveis podem ser fornecidas por meio de seus próprios servidores ou da CDN de sua escolha. Para equipes de TI e segurança, isso permite executar testes automáticos, verificar os arquivos no próprio sistema de controle de versão e estar em total conformidade com os processos de migração de produção interna, relacionados à segurança ou outros.

## Quando posso migrar para tags?

Agora é o melhor momento para migrar para tags. O processo de migração facilita a cópia das propriedades do DTM para as tags. Recomendamos testes abrangentes, mas automatizamos o máximo possível (sem alterações no código incorporado na página e migração automatizada de regras e elementos de dados).

## As tags são compatíveis com aplicativos de página única e com minha estrutura favorita?

Sim. As tags têm recursos para oferecer flexibilidade aos usuários e desenvolvedores de extensão para coleta, gerenciamento e distribuição de dados em experiências de aplicativo de página única ou em páginas ou sites com grande uso de Ajax. Isso se aplica independentemente das preferências de estrutura de desenvolvimento, seja Angular, React.js, Ember, Meteor, etc.

## As tags são compatíveis com camadas de dados dinâmicos?

Sim. As tags incluem uma extensão especializada no acompanhamento de alterações nas camadas de dados dinâmicos.

## A quais tipos de evento as tags dão suporte?

Os tipos de evento estão disponíveis por meio das extensões. A quantidade de tipos de evento com suporte varia de acordo com a extensão. Por exemplo, a extensão do YouTube inclui quatro tipos de evento de vídeo: play, pause, end e time played. Por meio das extensões, as tags podem dar suporte a quaisquer outros tipos de eventos de navegador ou sintéticos, como sequências específicas de atividades de visitante.

## As tags tornarão meu site mais rápido (ou mais lento)?

As tags foram criadas para fornecer e executar tecnologias de marketing e publicidade em seu site da forma mais eficiente possível usando as práticas recomendadas atuais. Quando usadas corretamente, as tags comprovaram melhorar o desempenho dos sites em relação aos métodos alternativos que fornecem funcionalidade semelhante.

## Quais navegadores são compatíveis com as tags?

Suporte de navegador para tags:

- [!DNL Chrome] (mais recente)
- [!DNL Safari] (mais recente)
- [!DNL Firefox] (mais recente)
- [!DNL Microsoft Edge] (mais recente)
- [!DNL Internet Explorer] (10 e superior)
- [!DNL iOS Safari] (mais recente)
- [!DNL Android Chrome] (mais recente)

Suporte de navegador para a interface de aplicativo de tags:

- [!DNL Chrome] (mais recente)
- [!DNL Safari] (mais recente)
- [!DNL Firefox] (mais recente)
- [!DNL Microsoft Edge] (mais recente)

Agora a maioria dos clientes da Adobe aproveita os recursos mais modernos da plataforma da Web nos navegadores atuais para criar melhores experiências de usuário, incluindo aplicativos de página única, bem como páginas e sites interativos com grande uso de Ajax. À medida que a maioria dos clientes muda para abordagens mais modernas em seus sites, eles buscam uma solução como tags, para viabilizar essas abordagens.

## As tags funcionam em aplicativos móveis nativos?

Sim! Agora as tags oferecem suporte a propriedades e configuração para dispositivos móveis para os novos [SDKs móveis](https://sdkdocs.com) da Adobe Experience Platform a fim de implementar a coleta e a entrega de dados em um ambiente de aplicativo móvel nativo. Visite a [documentação](https://sdkdocs.com) para saber mais.

## Why is the UI saying there was an error loading my account?

If you receive a message saying that there was an error loading your account, it means that your account does not belong to any product profiles for tags. [](./ui/administration/manage-permissions.md)

## Why can&#39;t I add any properties in the UI?

If you cannot create any new properties when logged in to the Data Collection UI, it means that your account does not belong to a product profile that has the Manage Properties right.

[](./ui/administration/manage-permissions.md) [](./ui/administration/user-permissions.md)

## E se eu tiver outras dúvidas?

[](https://adobe.com/go/launchme)[](http://join.connectionsdevs.chat)
