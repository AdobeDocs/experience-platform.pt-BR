---
title: Perguntas frequentes
description: Obtenha respostas para perguntas frequentes sobre tags no Adobe Experience Platform.
source-git-commit: 39d9468e5d512c75c9d540fa5d2bcba4967e2881
workflow-type: tm+mt
source-wordcount: '903'
ht-degree: 32%

---

# Guia de solução de problemas de tags

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](./term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Este documento fornece respostas a perguntas frequentes sobre tags no Adobe Experience Platform.

## O que são tags?

Tags são a próxima geração de recursos de gerenciamento de tags fornecidos pelo Adobe, e incorporados ao Adobe Experience Platform. Tags permitem que os clientes:

- Implantar produtos da Web do lado do cliente usando integrações chamadas de *extensões*
- Fornecer configuração dinamicamente para atualizar as implementações do cliente em aplicativos móveis nativos
- Capturar, definir, gerenciar e compartilhar dados de maneira consistente entre os produtos de marketing e publicidade de outros fornecedores e da Adobe

As tags são um sistema avançado de entrega de código e configuração que avalia condições e executa ações para implantar bibliotecas e produtos do lado do cliente de maneira eficiente e eficaz. Eles também fornecem uma abordagem altamente escalável para gerenciar e criar integrações e têm um conjunto robusto de APIs para interação programática.

## Quanto custam as tags?

Não há custo adicional para tags. Eles estão disponíveis para qualquer cliente [!DNL Adobe Experience Cloud].

## Ouvi dizer que existem plug-ins agora. De que isso se trata?

Tags são criadas na Adobe Experience Platform e são totalmente extensíveis. Clientes, parceiros de Adobe, agências e fornecedores de tecnologia de marketing ou publicidade podem criar uma extensão de tag que adiciona novas funcionalidades ou modifica as funcionalidades existentes. O sistema permite que os parceiros e clientes criem, gerenciem e atualizem suas próprias integrações. Esta é apenas uma forma como o Adobe está abrindo o Adobe Experience Platform para que os clientes e parceiros possam integrar produtos e negócios a ele. Isso ajuda todos a conectarem a tecnologia da Adobe às tecnologias de marketing e publicidade de outros fornecedores com mais facilidade.

## Todas as extensões de terceiros estarão disponíveis imediatamente?

As extensões já estão disponíveis para soluções Adobe e um grande e crescente número de fornecedores e tecnologias independentes de análise, marketing, publicidade e consentimento. Continuamos trabalhando com nossos parceiros para expandir o ecossistema. Como as extensões podem ser criadas, gerenciadas e atualizadas pelos proprietários da tecnologia, os clientes não precisam aguardar que a engenharia do Adobe as crie.

## Quando os clientes ou parceiros podem criar extensões?

As tags abriram seu portal de autoatendimento virtual, que os desenvolvedores de extensão podem usar para criar suas próprias integrações com a Adobe Cloud Platform.

Temos muitos clientes que também optam por criar suas próprias extensões privadas para usar somente em suas próprias empresas usando os mesmos métodos de desenvolvimento de extensão.

## As tags atendem aos padrões de segurança da minha empresa?

As tags estão prontas para SOC-2 e Gramm-Leach-Bliley Act. Tags também oferecem a capacidade de se auto-hospedar. As bibliotecas JavaScript e configurações móveis podem ser atendidas em seus próprios servidores ou no CDN de sua escolha. Para equipes de TI e segurança, isso permite executar testes automáticos, verificar os arquivos no próprio sistema de controle de versão e estar em total conformidade com os processos de migração de produção interna, relacionados à segurança ou outros.

## Quando posso migrar para tags?

Agora é o melhor momento para migrar para tags. O processo de migração facilita a cópia das propriedades do DTM em tags. Recomendamos testes abrangentes, mas automatizamos o máximo possível (sem alterações no código incorporado na página e migração automatizada de regras e elementos de dados).

## As tags são compatíveis com aplicativos de página única e com a minha estrutura favorita?

Sim. As tags têm os recursos para oferecer flexibilidade aos usuários e desenvolvedores de extensão na coleta, gerenciamento e distribuição de dados em experiências de aplicativo de página única ou em páginas ou sites com Ajax excessivo. Isso se aplica independentemente das preferências de estrutura de desenvolvimento, seja Angular, React.js, Ember, Meteor, etc.

## As tags são compatíveis com camadas de dados dinâmicos?

Sim. As tags incluem uma extensão especializada no acompanhamento de alterações nas camadas de dados dinâmicos.

## Quais tipos de evento as tags suportam?

Os tipos de evento estão disponíveis por meio das extensões. A quantidade de tipos de evento suportados varia de acordo com a extensão. Por exemplo, a extensão do YouTube inclui quatro tipos de evento de vídeo: play, pause, end e time played. Por meio das extensões, as tags podem suportar quaisquer outros tipos de evento do navegador ou tipos de evento sintético, como sequências específicas de atividades do visitante.

## As tags irão acelerar (ou desacelerar) meu site?

As tags foram projetadas para fornecer e executar tecnologias de marketing e publicidade em seu site da maneira mais eficiente possível, usando as práticas recomendadas atuais. Quando usadas corretamente, as tags comprovaram melhorar o desempenho dos sites em relação aos métodos alternativos que fornecem funcionalidade semelhante.

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

A maioria dos clientes do Adobe aproveita os recursos mais modernos da plataforma da Web nos navegadores atuais para criar experiências de usuário melhores, incluindo aplicativos de página única e páginas e sites interativos com Ajax excessivo. À medida que a maioria dos clientes mudam para abordagens mais modernas com seus sites, eles exigem uma solução como tags que viabilizam essas abordagens.

## As tags funcionam em aplicativos móveis nativos?

Sim! As tags agora oferecem suporte a propriedades e configuração móveis para o novo Adobe Experience Platform [Mobile SDKs](https://sdkdocs.com) para implementar a coleta e a entrega de dados em um ambiente de aplicativo móvel nativo. Visite a [documentação](https://sdkdocs.com) para saber mais.

## E se eu tiver outras dúvidas?

Se você tiver outras dúvidas, pergunte na Comunidade do Adobe na página de tags principais localizada em [https://adobe.com/go/launchme](https://adobe.com/go/launchme).

As tags são apenas um exemplo de onde a plataforma está se dirigindo: mais aberto, mais integrado e sempre dedicado ao sucesso do cliente.
