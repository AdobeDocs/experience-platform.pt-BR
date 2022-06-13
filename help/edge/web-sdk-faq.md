---
title: Perguntas frequentes sobre o Adobe Experience Platform Web SDK
description: Obtenha respostas para perguntas frequentes sobre o SDK da Web da Adobe Experience Platform.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 219f0f66026e8eb6729370916be3490309937f2a
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 2%

---

# Perguntas frequentes

Este guia fornece respostas para perguntas frequentes sobre o SDK da Web da Adobe Experience Platform.

## O que é o SDK da Web da Adobe Experience Platform?

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que os clientes do Adobe Experience Cloud interajam com os vários serviços no Experience Cloud.

Ele envia dados de uma maneira independente da solução (XDM) para a Adobe Experience Platform Edge Network, que mapeia os dados para a solução de formatos e destinos específicos e os envia em tempo real.

**Mais informações**
[Apresentação Adobe Summit](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Como o SDK da Web da Adobe Experience Platform difere das soluções anteriores?

### Antes do SDK do Adobe Experience Platform

Atualmente, é necessário implantar diferentes bibliotecas JavaScript com base em cada solução individual.

* Cada solução tem sua própria biblioteca, esquema e domínio do JavaScript.
* Nenhuma dessas bibliotecas foi criada para trabalhar entre si.
* Casos de uso entre soluções e Adobe Experience Platform exigem que essas bibliotecas diferentes sejam interdependentes, causando atrito de implantação.

Embora as tags na Platform facilitem ao máximo a implantação e o gerenciamento dessas bibliotecas, ainda há problemas com:

* Tamanho da biblioteca (excesso de código de Adobe em uma página)
* Desempenho (os sites demoram muito para carregar)
* Várias chamadas para um único caso de uso
* Aguardar o retorno da ECID antes das chamadas de personalização (causa atraso)
* Coleta de dados fragmentada (o que é uma evar?)
* Confusão de esquema entre soluções (A4T)
* Muitas outras coisas menos ótimas

Além disso, atualmente não há biblioteca de JavaScript que envie dados diretamente para a Adobe Experience Platform.

### Com o Adobe Experience Platform Web SDK

O novo SDK da Web envia dados das seguintes soluções para um único destino (Adobe Experience Platform Edge Network) e resolve os casos de uso mais comuns da solução mencionada.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID de visitante
* Adobe Experience Platform

Outras soluções serão seguidas ainda este ano.

O SDK da Web da Adobe Experience Platform também pode enviar dados diretamente para a Adobe Experience Platform. Esses dados estão no XDM e são mapeados para o schema de soluções do lado do servidor.

## Qual é o valor desse novo SDK da Web?

**Desempenho:** O SDK da Web é menor do que o uso de todas as bibliotecas Adobe atuais e fornece carregamentos de página significativamente mais rápidos.

**Simplicidade:** A combinação de XDM, SDK da Web, tags, Experience Edge, soluções da Adobe Experience Cloud e Adobe Experience Platform cria uma história de coleta de dados fácil de entender e simples de seguir.

* **XDM:** O schema independente da solução usado para enviar dados ao Adobe. Não há mais marcação para evars ou mboxes.
* **Adobe Experience Platform Web SDK:** Facilita o envio e o recebimento de dados para a Adobe Experience Platform Edge Network.
* **Tags:** Simplifica a implantação e a configuração do SDK da Web (e de quaisquer outras tags do JavaScript) em um site.
* **Experience Edge:** Direcione facilmente os dados para a Adobe Experience Platform e as soluções no formato necessário.
* **Soluções Adobe Experience Platform e Adobe:** Habilite sua proposta de valor.

**Controle:** Como todos os dados estão usando um fluxo único e conectado de dados, você pode, logicamente, seguir e controlar a aparência dos dados em cada milissegundo de sua jornada, de e para aplicativos.

**Moderno e pronto para o futuro:** O SDK da Web e sua conexão com a Rede de borda da Experience Cloud permitiram que o Adobe modernizasse significativamente o modo como o Adobe lida com a coleta de dados, a personalização, o consentimento e o futuro de cookies de terceiros. (Ela ativa um domínio próprio, gerenciado pelo Adobe.)

**Valor do tempo:** O Adobe trabalhou bastante (e continuará) para facilitar ao máximo a implantação do SDK da Web por meio de tags e mapear dados do lado do cliente para XDM. Depois que esse trabalho for feito, todas as outras soluções Adobe e serviços Adobe Experience Platform poderão ser ativados ou desativados no lado do servidor. Por exemplo, se estiver usando essa opção para o Adobe Analytics e quiser ativar o Target ou o Experience Platform, você pode simplesmente virar um botão na configuração do Datastream e acender esses casos de uso.

## O que é o Alloy?

Alloy é o nome do código do SDK da Web da Adobe Experience Platform. Ele é usado no código-fonte e no nome do arquivo do SDK, embora o SDK da Web da Adobe Experience Platform seja o nome oficial.

## Os clientes precisam comprar o Adobe Experience Platform para usar o [!DNL Web SDK]?

Não. Qualquer cliente da Adobe Digital Experience pode usar o SDK da Web da Adobe Experience Platform gratuitamente. Para usar o SDK da Web, você deve ter sua organização provisionada para esse recurso. Se você deseja obter acesso, preencha o seguinte [formulário](https://adobe.ly/websdkaccess) e o Adobe fornecerá acesso ao [Interface do usuário de datastreams](datastreams/overview.md) e a interface do usuário do Adobe Experience Platform (se necessário).

Clientes que desejam usar o [!DNL Web SDK] receberá acesso para criar esquemas, conjuntos de dados e namespaces de identidade na interface do usuário do Adobe Experience Platform.

## Quem deve usar o SDK da Web?

O SDK da Web da Adobe Experience Platform foi desenvolvido para as seguintes pessoas:

* Usuários do Adobe Experience Platform
   * Se você precisar enviar dados diretamente de um dispositivo para o Adobe Experience Platform, essa é a maneira oficialmente recomendada.
   * O Adobe está ciente de que usar o conector do Adobe Analytics é mais rápido se o cliente já tiver o Adobe Analytics, mas não é a estratégia de longo prazo para a coleta de dados.

* Clientes de solução Adobe Experience Cloud
   * Os novos clientes do Adobe Analytics, Adobe Audience Manager e Adobe Target devem começar com o novo SDK da Web e não usar bibliotecas herdadas.
   * Os clientes existentes que desejam obter a implementação mais otimizada possível devem usar o novo SDK da Web.


## Como obtenho acesso para começar a usar o SDK da Web da Adobe Experience Platform?

O SDK da Web está disponível no momento para o público em geral e pode ser usado para enviar dados para produtos da Adobe Experience Cloud. A capacidade de enviar dados para soluções de terceiros está chegando em breve. O SDK é gratuito, é hospedado gratuitamente pelo Adobe e pode ser baixado para que você possa hospedá-lo em seus próprios servidores, se desejar, gratuitamente. O SDK da Web da plataforma requer configurações de conjunto de dados e o construtor de esquema Adobe Experience Platform XDM, para que os servidores Adobe lidem corretamente com os dados de entrada provenientes do SDK. Se você quiser obter acesso, entre em contato com o Gerente de sucesso do cliente (CSM) para iniciar o processo de solicitação.

## Quais casos de uso são suportados atualmente pelo SDK da Web?

O SDK da Web está evoluindo rapidamente. Mais casos de uso estão sendo trabalhados. Você pode encontrar a variável [lista de casos de uso atualmente suportados aqui.](https://github.com/adobe/alloy/projects/5)

## Os clientes atuais precisam remarcar seus sites?

Depende. O SDK da Web da Adobe Experience Platform pode ser implantado em dois estilos diferentes. Um documento de migração futuro fornecerá detalhes adicionais.

* **Apenas outra tag:** Se o site já tiver tags de soluções e você não puder remarcar, mas desejar enviar dados para a Rede de borda da Adobe Experience Platform para casos de uso do Experience Platform ou os recursos de encaminhamento de eventos futuros (veja abaixo), é possível adicionar a variável `alloy.js` para o site, onde funciona como &quot;apenas outra tag&quot;.

* **A única tag :** Se quiser usar o SDK da Web para uma solução do Experience Cloud, use-o para _all_ das soluções da página. Por exemplo, se o seu site já estiver marcado para o Adobe Analytics e você quiser usá-lo para o Target, será necessário usá-lo para ambos, bem como para qualquer outro no futuro.

Em outras palavras, se você decidir usar o SDK da Web da Adobe Experience Platform para casos de uso que não sejam da solução, poderá adicionar tags ao site com `alloy.js` e continuar como se fosse uma nova solução. Se quiser usá-lo para Adobe Analytics, Target ou Audience Manager, ou para casos de uso de aplicativos, talvez seja necessário remover qualquer código herdado na página.

## Posso migrar as ECIDs quando começar a usar o Alloy para que os visitantes do meu site não comecem a aparecer como novos visitantes?

Sim, o SDK da Web da Adobe Experience Platform fornece um recurso de Migração de identidade. Siga as instruções para Migração de ID no [Documentação de identidade do SDK da Web da plataforma](https://experienceleague.adobe.com/docs/experience-platform/edge/identity/overview.html?lang=en#id-migration) para obter mais detalhes.

## Como o SDK da Web é diferente das tags?

* **Tags no Experience Platform** gerencie o código do dispositivo. Use-os para implantar o código com mais facilidade. Elas são livres e poderosas.

* **Adobe Experience Platform Web SDK** é o nome oficial do novo código que seria implantado por tags para casos de uso de Adobe. Também é livre e poderoso.

* **`alloy.js`** é o nome do arquivo do código Adobe Experience Platform Web SDK.

## Preciso usar tags para implantar o SDK da Web?

Não. Você pode baixar o `alloy.js` arquivo você mesmo.

No entanto:

* O SDK da Web da Adobe Experience Platform requer algo chamado de ID do conjunto de dados, para que a rede de borda possa identificar o fluxo e determinar o que fazer com os dados. Essa ID é criada no Experience Platform. Isso não significa que você precisa usar a interface do usuário da coleta de dados para criar propriedades ou implantar o código do JavaScript, mas sim usar tags para criar uma ID de configuração.

* As tags não são apenas o melhor gerenciador de tags e SDK disponível, mas também facilitam a implantação `alloy.js` e mapear dados para esquemas XDM. Se decidir não usar tags, será necessário gerenciar a implantação `alloy.js`, eventos e mapeamento de dados no XDM antes de enviá-los. Isso é uma _many_ processo mais difícil do que usar tags.

* É recomendável usar tags para implantar `alloy.js`, mesmo que seja a única tag para a qual você o usa.

## O que é o encaminhamento de eventos?

Se você usar nossos SDKs e enviar o XDM para o Experience Edge, esses novos recursos de encaminhamento de eventos permitirão instalar novas extensões do lado do servidor e mapear esses dados para qualquer coisa — e enviá-los para qualquer lugar — de nossa rede de borda. Pense nisso como &quot;coleta de dados como um serviço&quot;. Isso estará disponível por um custo, além de ser incluído como parte do Adobe Experience Platform.

## O que é um CNAME ou domínio próprio e por que ele é importante?

Mais informações sobre um CNAME estão disponíveis na seção [Documentação do Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html?lang=pt-BR)

## O SDK da Web da Adobe Experience Platform usa cookies? Em caso afirmativo, que cookies utiliza?

Sim, no momento, o SDK da Web usa entre 1 e 4 cookies, dependendo da implementação. Abaixo está uma lista dos 4 cookies que você pode ver com o SDK da Web e a maneira como eles são usados:

**kndct_orgid_identity:** O cookie de identidade é usado para armazenar a ECID, bem como algumas outras informações relacionadas à ECID.

**kdctr_orgid_consent:** Esse cookie armazena a preferência de consentimento do usuário para o site.

**kdctr_orgid_personalization:** Esse cookie inclui informações de sessão que o Adobe Target usa para personalizar páginas da Web.

**kdctr_orgid_consent:** Este cookie baseado em sessão sinaliza o servidor para procurar o lado do servidor das preferências de consentimento.

Ao usar o SDK da Web, a Edge Network define um ou mais dos cookies acima. A Edge Network define todos os cookies com a variável `secure` e `sameSite="none"` atributos.

Se você tiver seções seguras e não seguras no seu site, isso pode interferir na identificação do usuário. Quando um usuário navega de uma seção segura do site para uma seção não segura, a Edge Network gera um novo `ECID` com a solicitação.

## Quais navegadores são compatíveis com o SDK da Web da Adobe Experience Platform?

O SDK da Web da Adobe Experience Platform foi projetado para funcionar de maneira ideal nas versões mais recentes do Google Chrome, Safari, Firefox, Internet Explorer 11 e Microsoft Edge Chromium. Você pode ter problemas ao usar determinados recursos em versões mais antigas de navegadores.

## Onde posso obter mais informações sobre o SDK da Web da Adobe Experience Platform?

* [Documentação](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR)
* [Código fonte](https://github.com/adobe/alloy)
