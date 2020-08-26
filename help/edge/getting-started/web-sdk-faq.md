---
title: Perguntas frequentes sobre o SDK da Web
seo-title: Perguntas frequentes sobre o Adobe Experience Platform Web SDK
description: Perguntas frequentes sobre o Adobe Experience Platform Web SDK
seo-description: Perguntas frequentes sobre o Adobe Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: f51513e66945c41d06f12f4ac8f05ddad0d32898
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 2%

---


# Perguntas frequentes

Estas Perguntas frequentes incluem perguntas frequentes sobre o SDK da Web do Adobe/

## O que é Adobe Experience Platform Web SDK?

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite que os clientes da Adobe Experience Cloud interajam com os vários serviços na Experience Cloud.

Ele envia dados de uma forma agnóstica à solução (XDM) para a Adobe Experience Platform Edge Network, que mapeia os dados para formatos e destinos específicos da solução e os envia em tempo real.

**Mais informações** sobre a apresentação do[Adobe Summit](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html)

## Qual é a diferença entre o Adobe Experience Platform Web SDK e as soluções anteriores?

### Antes do SDK do Adobe Experience Platform

Atualmente, é necessário implantar diferentes bibliotecas JavaScript com base em cada solução individual.

* Cada solução tem sua própria biblioteca, schema e domínio JavaScript.
* Nenhuma dessas bibliotecas foi construída para trabalhar uma com a outra.
* Casos de uso entre soluções e Adobe Experience Platform exigem que essas bibliotecas diferentes sejam interdependentes, causando atrito de implantação.

Embora a Adobe Experience Platform Launch facilite ao máximo a implantação e o gerenciamento dessas bibliotecas, ainda há problemas com:

* Tamanho da biblioteca (excesso de código de Adobe em uma página)
* Desempenho (os sites demoram muito para carregar)
* Várias chamadas para um único caso de uso
* Aguardando retorno de ECID antes das chamadas de personalização (causa atraso)
* Coleta de dados fragmentada (o que é uma evar?)
* Confusão de schemas entre soluções (A4T)
* Muitas outras coisas menos ótimas

Além disso, atualmente não há biblioteca JavaScript que envia dados diretamente para a Adobe Experience Platform.

### Com Adobe Experience Platform Web SDK

O novo SDK da Web envia dados para as seguintes soluções para um único destino (AEP Edge Network) e resolve os casos mais comuns de uso de solução mencionados.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID de visitante
* Adobe Experience Platform

Outras soluções serão seguidas ainda este ano.

O Adobe Experience Platform Web SDK também pode enviar dados diretamente para a Adobe Experience Platform. Esses dados estão no XDM e são mapeados para o schema de solução do lado do servidor.

## Qual é o valor deste novo SDK da Web?

**Desempenho:** O SDK da Web é menor do que o uso de todas as bibliotecas de Adobe atuais e fornece cargas de página significativamente mais rápidas.

**Simplicidade:** A combinação de XDM, Web SDK, Launch, Experience Edge, soluções Adobe Experience Cloud e Adobe Experience Platform cria uma história de coleta de dados fácil de entender e simples de seguir.

* **XDM:** O schema agente da solução que você usa para enviar dados para o Adobe. Não há mais marcação para evars ou mboxes.
* **SDK da Web:** Facilita o envio e a recepção de dados para a Adobe Experience Platform Edge Network.
* **Iniciar:** Simplifica a implantação e a configuração do SDK da Web (e de quaisquer outras tags JavaScript) em um site.
* **Experience Edge:** Direcione facilmente os dados para a Adobe Experience Platform e as soluções no formato necessário.
* **Soluções Adobe Experience Platform e Adobe:** Habilite sua proposta de valor.

**Controle:** Como todos os dados estão usando um fluxo único e conectado de dados, você pode logicamente acompanhar e controlar a aparência dos dados a cada milissegundo de sua jornada, de e para os aplicativos.

**Moderno e pronto para o futuro:** O SDK da Web e sua conexão com a Experience Edge Network permitiram que o Adobe modernizasse significativamente o modo como o Adobe lida com a coleta de dados, a personalização, o consentimento e o futuro de cookies de terceiros. (Ela ativa um domínio próprio, gerenciado pelo Adobe.)

**Tempo até o valor:** A Adobe trabalhou arduamente (e continuará) para facilitar ao máximo a implantação do SDK da Web via Launch e mapear dados do cliente para XDM.  Depois que esse trabalho for feito, todas as outras soluções de Adobe e os serviços da Adobe Experience Platform poderão ser ativados ou desativados no servidor. Por exemplo, se você estiver usando essa opção para Adobe Analytics e quiser ativar o Público alvo ou o Experience Platform, basta alternar a configuração do Experience Edge e acender esses casos de uso.

## O que é `alloy.js`?

`Alloy.js` é o nome do arquivo para o SDK da Web do Adobe Experience Platform. O Adobe Experience Platform Web SDK é o nome oficial, mas muitos desenvolvedores o chamam de &quot;liga&quot;.

## Os clientes precisam comprar a Adobe Experience Platform para usar o SDK da Web?

Não. Qualquer cliente da Adobe Digital Experience pode usá-la. Totalmente livre. Qualquer cliente que deseje usar o SDK da Web receberá acesso para criar schemas e conjuntos de dados na interface do usuário do Adobe Experience Platform.

## Quem deve usar o SDK da Web?

O Adobe Experience Platform Web SDK foi desenvolvido para as seguintes pessoas:

* Usuários do Adobe Experience Platform

   Se você precisar enviar dados diretamente de um dispositivo para a Adobe Experience Platform, essa é a maneira oficialmente recomendada.

   A Adobe está ciente de que o uso do conector Adobe Analytics é mais rápido se o cliente já tiver a Adobe Analytics, mas não é a estratégia de longo prazo para a coleta de dados.

* Clientes de soluções Adobe Experience Cloud

   Os novos clientes Adobe Analytics, Adobe Audience Manager e Adobe Target devem se start ao novo SDK da Web e não usar bibliotecas herdadas.

   Os clientes atuais que desejam obter a implementação mais otimizada possível devem usar o novo SDK da Web.


## Como obtenho acesso ao start usando o SDK da Adobe Experience Platform Web?

O SDK da Web está disponível atualmente para o público em geral e pode ser usado para enviar dados para produtos da Adobe Experience Cloud. A capacidade de enviar dados para soluções de terceiros está chegando em breve. Se você deseja obter acesso ao SDK da Web, entre em contato com seu CSM para start do processo de solicitação.

## Quais casos de uso são suportados atualmente pelo SDK da Web?

O SDK da Web está evoluindo rapidamente. Estão a ser trabalhados mais casos de utilização. Você pode encontrar a [lista de casos de uso atualmente suportados aqui.](https://github.com/adobe/alloy/projects/5)

## Os clientes atuais precisam remarcar seus sites?

Depende. O Adobe Experience Platform Web SDK pode ser implantado em dois estilos diferentes. Um documento de migração futuro fornecerá detalhes adicionais.

* **Apenas outra tag:** Se o site já estiver marcado para obter soluções e você não puder remarcar, mas quiser enviar dados para a Adobe Experience Platform Edge Network para casos de uso do Experience Platform ou para os recursos do lado do servidor do Launch futuros (veja abaixo), adicione a `alloy.js` tag ao site, onde ela funciona como &quot;apenas outra tag&quot;.

* **A única tag:** Se quiser usar o SDK da Web para uma solução de Experience Cloud, você deve usá-lo para _todas_ as soluções nessa página. Por exemplo, se o site já estiver marcado para o Analytics e você quiser usá-lo para o Público alvo, será necessário usá-lo tanto para o Analytics quanto para outros no futuro.

Em outras palavras, se você decidir usar o Adobe Experience Platform Web SDK para casos de uso que não sejam de solução, poderá marcar o site com `alloy.js` e continuar como se fosse uma nova solução. Se você quiser usá-lo para Adobe Analytics, Público alvo ou Audience Manager ou para casos de uso de aplicativos, talvez seja necessário remover qualquer código herdado na sua página.

## Posso migrar os ECIDs quando start usando o Alloy para que os visitantes do meu site não apareçam como novos visitantes?

Sim, o Adobe Experience Platform Web SDK fornece um recurso de Migração de identidade. Siga as instruções [deste documento](https://docs.adobe.com/content/help/en/experience-platform/edge/fundamentals/identity.html#id-migration) para obter mais detalhes.

## Como o SDK da Web é diferente do Adobe Experience Platform Launch?

* **O Launch** é o gerenciador de código do dispositivo. Use-o para implantar o código com mais facilidade. É livre e poderoso.

* **O Adobe Experience Platform Web SDK** é o nome oficial do novo código que seria implantado pelo Launch para casos de uso com Adobe. Também é livre e poderosa.

* **`alloy.js`** é o nome do arquivo do código SDK da Web do Adobe Experience Platform.

## Preciso usar o Adobe Experience Platform Launch para implantar o SDK da Web?

Não. Você mesmo pode baixar o `alloy.js` arquivo.

No entanto:

* O Adobe Experience Platform Web SDK requer algo chamado de ID de configuração do Experience Edge para que a rede de borda possa identificar o fluxo e determinar o que fazer com os dados. Essa ID é criada no Launch. Isso não significa que você precisa usar o Launch para criar propriedades ou implantar o código JavaScript, mas precisa usar o Launch para criar uma ID de configuração.

* A Adobe Experience Platform Launch não é apenas a melhor tag disponível e gerenciador de SDK, mas facilita a implantação `alloy.js` e o mapeamento de dados para schemas XDM. Se você decidir não usar o Launch, será necessário gerenciar a implantação `alloy.js`, o evento e o mapeamento dos dados para o XDM antes de enviá-los. Este é um processo _muito_ mais difícil do que usar o Launch.

* É recomendável usar o Launch para implantar `alloy.js`, mesmo se for a única tag usada.

## O que é o XDM e o que eu tenho que usar para o SDK da Web?

XDM é o formato de dados usado para enviar dados para a Adobe Experience Platform e o SDK da Web. A documentação [do SDK da](https://docs.adobe.com/content/help/en/experience-platform/edge/get-started/quick-start-with-launch.html#prepare-a-schema) Web o orienta a configurar facilmente um schema que você pode personalizar para suas necessidades específicas.

## O que é &quot;Adobe Experience Platform Launch Server Side&quot;?

Mais tarde em 2020, o Launch lançará os recursos de encaminhamento pelo lado do servidor. Se você usar nossos SDKs e enviar o XDM para o Experience Edge, esses novos recursos permitirão instalar novas extensões do lado do servidor e mapear esses dados em qualquer lugar da nossa rede de borda. Pense nisso como &quot;coleta de dados como um serviço&quot;.  Isso estará disponível por um custo, além de ser fornecido como parte da Adobe Experience Platform.

**Mais informações** sobre a apresentação do[Adobe Summit](https://adobe.bluejeans.com/playback/s/9LhauPOnRSUTYg6RMHAw4oJekhYfOQgdBLlNekVJdWevYktpxqX2IYyl5fz2Wxh9)

## O que é um domínio CNAME ou primário e por que isso importa?

Mais informações sobre um CNAME estão disponíveis na documentação do [Adobe](https://docs.adobe.com/content/help/pt-BR/id-service/using/reference/analytics-reference/cname.html)

## Onde posso obter mais informações sobre o Adobe Experience Platform Web SDK?

* [Documentação](https://docs.adobe.com/content/help/pt-BR/experience-platform/edge/home.html)
* [Código fonte](https://github.com/adobe/alloy)
