---
title: Perguntas frequentes sobre o Adobe Experience Platform Web SDK
description: Obtenha respostas para perguntas frequentes sobre o Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 002a57d1d5cfb2e7bdbd9b587e77ca4487a28f65
workflow-type: tm+mt
source-wordcount: '2268'
ht-degree: 2%

---


# Perguntas frequentes

Este guia fornece respostas a perguntas frequentes sobre o Adobe Experience Platform Web SDK.

## O que é o Adobe Experience Platform Web SDK?

O Adobe Experience Platform Web SDK é uma biblioteca JavaScript do lado do cliente que permite interagir com os vários serviços na Adobe Experience Cloud.

O SDK da Web envia dados de maneira independente de solução (XDM) para o Edge Network do Experience Platform, que mapeia os dados para formatos e destinos específicos da solução e os envia em tempo real.

Assista ao vídeo a seguir para obter mais informações sobre o SDK da Web: [Conheça o Alloy.js e Nunca marque para um eVar ou Mbox novamente](https://www.adobe.com/summit/2020/with-alloy-js-never-tag-for-an-evar-or-mbox-again.html).

## Em que o Adobe Experience Platform Web SDK difere das soluções anteriores?

### Antes do SDK da Web do Experience Platform

Atualmente, é necessário implantar diferentes bibliotecas JavaScript com base em cada solução individual.

* Cada solução tem sua própria biblioteca, esquema e domínio do JavaScript.
* Nenhuma dessas bibliotecas foi criada para funcionar entre si.
* Casos de uso entre soluções e Adobe Experience Platform exigem que essas bibliotecas diferentes sejam interdependentes, causando atrito na implantação.

Embora as tags na Platform facilitem o máximo possível a implantação e o gerenciamento dessas bibliotecas, ainda há problemas com:

* Tamanho da biblioteca (excesso de código de Adobe em uma página)
* Desempenho (os sites demoram muito para carregar)
* Várias chamadas para um único caso de uso
* Aguardar o retorno de ECID antes das chamadas de personalização (causa atraso)
* Coleta de dados fraturada (o que é uma evar?)
* Confusão de esquema entre soluções (A4T)
* Muitas outras coisas menos ótimas

Além disso, atualmente não há nenhuma biblioteca do JavaScript que envie dados diretamente para o Adobe Experience Platform.

### Com o SDK da Web do Experience Platform

O novo SDK da Web envia dados das seguintes soluções para um único destino (Experience Platform Edge Network) e resolve os casos de uso mais comuns da solução mencionada acima.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID de visitante
* Adobe Experience Platform

Outras soluções serão seguidas.

O SDK da Web da Adobe Experience Platform também pode enviar dados diretamente para a Adobe Experience Platform. Esses dados estão no formato XDM e são mapeados para o esquema da solução do lado do servidor.

## Qual é o valor desse novo SDK da Web?

**Desempenho:** o SDK da Web é menor do que o uso de todas as bibliotecas de Adobe atuais e fornece carregamentos de página significativamente mais rápidos.

**Simplicidade:** a combinação de XDM, SDK da Web, tags, Edge Network, soluções da Adobe Experience Cloud e Adobe Experience Platform cria uma história de coleta de dados fácil de entender e simples de seguir.

* **XDM:** O esquema independente de solução usado para enviar dados para o Adobe. Não há mais tags para evars ou mboxes.
* **SDK da Web:** facilita o envio e o recebimento de dados para o Adobe Experience Platform Edge Network.
* **Marcas:** simplifica a implantação e a configuração do SDK da Web (e de qualquer outra marca da JavaScript) em um site.
* **Edge Network:** encaminhe facilmente os dados para a Adobe Experience Platform e soluções no formato necessário.
* **Soluções Adobe Experience Platform e Adobe:** Habilitem sua proposta de valor.

**Controle:** como todos os dados estão usando um único fluxo conectado de dados, você pode acompanhar e controlar logicamente como os dados são a cada milissegundo de sua jornada, de e para aplicativos.

**Moderno e pronto para o futuro:** O SDK da Web e sua conexão com o Edge Network permitiram que o Adobe modernizasse significativamente a maneira como o Adobe lida com a coleta de dados, a personalização, o consentimento e o futuro dos cookies de terceiros. (Ele permite um domínio próprio, gerenciado pelo Adobe.)

**Tempo de implantação:** o Adobe trabalhou muito (e continuará) para facilitar ao máximo a implantação do SDK da Web por meio de marcas e o mapeamento dos dados do lado do cliente para o XDM. Depois que esse trabalho for concluído, todas as outras soluções Adobe e serviços da Adobe Experience Platform poderão ser ativados ou desativados no lado do servidor. Por exemplo, se estiver usando isso para Adobe Analytics e quiser ativar o Target ou Experience Platform, basta virar um botão de alternância na configuração do Datastream e ativar esses casos de uso.

## O que é o [!DNL alloy.js]?

[!DNL alloy.js] é o nome da biblioteca JavaScript do SDK da Web. Ele é referenciado no código-fonte e no nome do arquivo do SDK.

## Os clientes precisam comprar o Adobe Experience Platform para usar o [!DNL Web SDK]?

Não. Qualquer cliente da Adobe Digital Experience pode usar o SDK da Web da Adobe Experience Platform gratuitamente. Os clientes que desejam usar o [!DNL Web SDK] precisarão configurar as permissões certas para criar esquemas, conjuntos de dados, namespaces de identidade e fluxos de dados na interface da Coleção de dados ou na interface do Experience Platform.

Para obter mais informações sobre como configurar essas permissões, consulte nossa documentação em [gerenciamento de permissões de coleta de dados](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html).

## Quem deve usar o SDK da Web?

O Adobe Experience Platform Web SDK foi desenvolvido para os seguintes clientes:

* Usuários do Adobe Experience Platform
   * Se você precisar enviar dados diretamente de um dispositivo para o Adobe Experience Platform, essa é a maneira oficialmente recomendada.
   * A Adobe está ciente de que o uso do conector Adobe Analytics é mais rápido se você já tiver o Adobe Analytics, mas essa não é a estratégia de longo prazo para a coleta de dados.

* Clientes de soluções da Adobe Experience Cloud
   * Os novos clientes do Adobe Analytics, Adobe Audience Manager e Adobe Target devem começar com o novo SDK da Web e não usar bibliotecas herdadas.
   * Os clientes existentes que desejam obter a implementação mais otimizada possível devem usar o novo SDK da Web.

## Como faço para obter acesso ao SDK da Web?

O SDK da Web está disponível no momento para o público em geral e pode ser usado para enviar dados para produtos da Adobe Experience Cloud. A capacidade de enviar dados para soluções de terceiros será disponibilizada em breve.

O SDK não é cobrado e é hospedado pelo Adobe gratuitamente. Se necessário, você pode baixá-lo e hospedá-lo em seus próprios servidores sem custo algum.

O SDK da Web requer acesso a [configurações de sequência de dados](../datastreams/overview.md) e ao [construtor de esquema XDM](../xdm/tutorials/create-schema-ui.md) do Experience Platform para que os servidores Adobe manipulem corretamente os dados de entrada provenientes do SDK. Se quiser obter acesso, entre em contato com a equipe de conta do Adobe para iniciar o processo de solicitação.

## Quais casos de uso são aceitos atualmente pelo SDK da Web?

O SDK da Web está evoluindo rapidamente. Mais casos de uso estão sendo trabalhados. Você pode encontrar a [lista de casos de uso atualmente suportados aqui.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## Os clientes atuais precisam remarcar seus sites?

Depende. O Adobe Experience Platform Web SDK pode ser implantado em dois estilos diferentes. Um futuro documento de migração fornecerá detalhes adicionais.

* **Apenas outra marca:** Se o site já estiver marcado para soluções e você não puder remarcar, mas quiser enviar dados para o Adobe Experience Platform Edge Network para casos de uso de Experience Platform ou para os recursos de encaminhamento de eventos futuros (veja abaixo), você poderá adicionar a marca `alloy.js` ao site, onde ela funciona como &quot;apenas outra marca&quot;.

* **A única tag:** Se você quiser usar o SDK da Web para uma solução Experience Cloud, deverá usá-lo para _todas_ as soluções dessa página. Por exemplo, se seu site já estiver marcado para o Adobe Analytics e você quiser usá-lo para o Target, será necessário usá-lo para ambos, bem como para qualquer outro no futuro.

Em outras palavras, se você decidir usar o SDK da Web da Adobe Experience Platform para casos de uso que não sejam de solução, poderá marcar o site com `alloy.js` e seguir em frente como se fosse uma nova solução. Se quiser usá-lo para Adobe Analytics, Target ou Audience Manager ou para casos de uso de aplicativos, talvez seja necessário remover qualquer um dos códigos herdados na página.

## Posso migrar as ECIDs quando começar a usar o SDK da Web para que os visitantes do meu site não comecem a aparecer como novos visitantes?

Sim, o SDK da Web da Adobe Experience Platform fornece um recurso de migração de identidade. Siga as instruções para migração de ID na [documentação de identidade do SDK da Web da Platform](/help/web-sdk/identity/overview.md#id-migration) para obter mais detalhes.

## Qual é a diferença entre o SDK da Web e as tags?

* **As marcas no Experience Platform** gerenciam o código do dispositivo. Use-os para implantar o código com mais facilidade. Eles são livres e poderosos.

* **Adobe Experience Platform Web SDK** é o nome oficial do novo código que seria implantado por marcas para casos de uso de Adobe. É também livre e poderosa.

* **`alloy.js`** é o nome de arquivo do código do SDK da Web da Adobe Experience Platform.

## Preciso usar tags para implantar o SDK da Web?

Não. Você mesmo pode baixar o arquivo `alloy.js`.

No entanto:

* O SDK da Web do Adobe Experience Platform requer algo chamado ID de sequência de dados para que a rede de borda possa identificar o fluxo e determinar o que fazer com os dados. Essa ID é criada no Experience Platform. Isso não significa que você precisa usar a interface do para criar propriedades ou implantar o código JavaScript, mas sim usar tags para criar uma ID de configuração.

* As tags não são apenas a melhor tag disponível e o gerenciador do SDK, facilita muito a implantação do `alloy.js` e o mapeamento de dados para esquemas XDM. Se decidir não usar marcas, será necessário gerenciar a implantação do `alloy.js`, a geração de eventos e o mapeamento de dados no XDM antes de enviá-los. Este é um processo _muito_ mais difícil do que o uso de tags.

* É recomendável usar marcas para implantar `alloy.js`, mesmo que seja a única marca para a qual você o usa.

## O que é encaminhamento de eventos?

Se você usar nossos SDKs e enviar XDM para o Edge Network, esses novos recursos do encaminhamento de eventos permitirão instalar novas extensões do lado do servidor e mapear esses dados para qualquer coisa—e enviá-la para qualquer lugar—de nossa rede de borda. Pense nisso como &quot;coleta de dados como um serviço&quot;. Ele estará disponível por um custo e será fornecido como parte do Adobe Experience Platform.

## O que é um CNAME ou domínio próprio e por que ele é importante?

Mais informações sobre um CNAME estão disponíveis na [documentação sobre o Adobe](https://experienceleague.adobe.com/docs/id-service/using/reference/analytics-reference/cname.html?lang=pt-BR)

## O SDK da Web da Adobe Experience Platform usa cookies? Em caso afirmativo, quais cookies ele usa?

Sim, atualmente o SDK da Web usa entre um e sete cookies, dependendo da implementação. Abaixo está uma lista dos cookies que você pode ver com o SDK da Web e a maneira como eles são usados:

| **Nome** | **maxAge** | **Idade amigável** | **Descrição** |
|---|---|---|---|
| **kndct_orgid_identity** | 34128000 | 395 dias | O cookie de identidade armazena a ECID, bem como outras informações relacionadas à ECID. |
| **kndctr_orgid_consent_check** | 7200 | 2 horas | Este cookie baseado em sessão sinaliza ao servidor para procurar as preferências de consentimento no lado do servidor. |
| **kndctr_orgid_consent** | 15552000 | 180 dias | Este cookie armazena a preferência de consentimento do usuário para o site. |
| **kndctr_orgid_cluster** | 1800 | 30 minutos | Este cookie armazena a região do Edge Network que está atendendo as solicitações do usuário atual. A região é usada no caminho do URL para que o Edge Network possa rotear a solicitação para a região correta. Esse cookie tem uma duração de 30 minutos, para que, se um usuário se conectar com um endereço IP diferente, a solicitação possa ser roteada para a região mais próxima. |
| **mbox** | 63072000 | 2 anos | Este cookie é exibido quando a configuração de migração do Target é definida como verdadeira. Isso permitirá que o [cookie da mbox](https://developer.adobe.com/target/implement/client-side/atjs/atjs-cookies/) do Target seja definido pelo SDK da Web. |
| **mboxEdgeCluster** | 1800 | 30 minutos | Este cookie é exibido quando a configuração de migração do Target é definida como verdadeira. Esse cookie permite que o SDK da Web comunique o cluster de borda correto com a at.js para que os perfis do Target possam permanecer em sincronia enquanto os usuários navegam em um site. |
| **AMCV_###@AdobeOrg** | 34128000 | 395 dias | Esse cookie só aparece quando a migração de ID no SDK da Web da Adobe Experience Platform está ativada. Este cookie ajuda na transição para o SDK da Web enquanto algumas partes do site ainda usam visitor.js. Consulte [`idMigrationEnabled`](/help/web-sdk/commands/configure/idmigrationenabled.md) para obter mais informações. |

Ao usar o SDK da Web, o Edge Network define um ou mais dos cookies acima. O Edge Network define todos os cookies com os atributos `secure` e `sameSite="none"`.

Se você tiver seções seguras e não seguras em seu site, isso pode interferir na identificação do usuário. Quando um usuário navega de uma seção segura do site para uma seção não segura, o Edge Network gera um novo `ECID` com a solicitação.

## Quais navegadores são compatíveis com o SDK da Web da Adobe Experience Platform?

O Adobe Experience Platform Web SDK foi projetado para funcionar de maneira ideal nas versões mais recentes do Google Chrome, Safari, Firefox, Internet Explorer 11 e Microsoft Edge Chromium. Você pode ter problemas ao usar determinados recursos em versões mais antigas dos navegadores.

## Onde posso obter mais informações sobre o Adobe Experience Platform Web SDK?

* [Documentação](/help/web-sdk/home.md)
* [Código Source](https://github.com/adobe/alloy)

### Suporte ao Internet Explorer {#support-internet-explore}

Esse SDK usa promessas, que são um método de comunicar a conclusão de tarefas assíncronas. A implementação [Promise](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) usada pelo SDK tem suporte nativo em todos os navegadores de destino, exceto [!DNL Internet Explorer]. Para usar o SDK em [!DNL Internet Explorer], você deve ter `window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Para determinar se você já tem `window.Promise` polyfilled:

1. Abra seu site no [!DNL Internet Explorer].
1. Abra o console de depuração do navegador.
1. Digite `window.Promise` no console e pressione Enter.

Se algo diferente de `undefined` aparecer, você provavelmente já preencheu `window.Promise` em polinização. Outra maneira de determinar se o `window.Promise` está popularizado é carregar seu site depois de concluir as instruções de instalação acima. Se o SDK emitir um erro mencionando algo sobre uma promessa, provavelmente você não preencheu `window.Promise` com polyfill.

Se você determinou que deve preencher `window.Promise` em excesso, inclua a seguinte marca de script acima do código base fornecido anteriormente:

```html
<script src="https://cdn.jsdelivr.net/npm/promise-polyfill@8/dist/polyfill.min.js"></script>
```

Esta marca carrega um script que garante que `window.Promise` seja uma implementação Promise válida.

>[!NOTE]
>
>Se você optar por carregar uma implementação Promise diferente, verifique se ela aceita `Promise.prototype.finally`.

### Suporte ao Internet Explorer

O SDK do Adobe Experience Platform usa promessas, que são um método de comunicar a conclusão de tarefas assíncronas. A implementação [Promise](https://developer.mozilla.org/pt-BR/docs/Web/JavaScript/Reference/Global_Objects/Promise) usada pelo SDK tem suporte nativo em todos os navegadores de destino, exceto [!DNL Internet Explorer]. Para usar o SDK em [!DNL Internet Explorer], você deve ter `window.Promise` [polyfilled](https://remysharp.com/2010/10/08/what-is-a-polyfill).

Uma biblioteca que você poderia usar para polyfill promessa é promessa-polyfill. Consulte a [documentação de promessa-polyfill](https://www.npmjs.com/package/promise-polyfill) para obter mais informações sobre como instalar com o NPM.

>[!NOTE]
>
>Se você optar por carregar uma implementação Promise diferente, verifique se ela aceita `Promise.prototype.finally`.
