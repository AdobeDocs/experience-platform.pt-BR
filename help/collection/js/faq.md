---
title: Perguntas frequentes sobre o Adobe Experience Platform Web SDK
description: Obtenha respostas para perguntas frequentes sobre o Adobe Experience Platform Web SDK.
exl-id: 6ddb4b4d-c9b8-471a-bd2e-135dc4202876
source-git-commit: 66105ca19ff1c75f1185b08b70634b7d4a6fd639
workflow-type: tm+mt
source-wordcount: '1665'
ht-degree: 1%

---

# Perguntas frequentes

Este guia fornece respostas a perguntas frequentes sobre o Adobe Experience Platform Web SDK.

## Em que a Adobe Experience Platform Web SDK difere das soluções anteriores?

### Antes do Experience Platform Web SDK

Atualmente, é necessário implantar diferentes bibliotecas JavaScript com base em cada solução individual.

* Cada solução tem sua própria biblioteca, esquema e domínio do JavaScript.
* Nenhuma dessas bibliotecas foi criada para funcionar entre si.
* Casos de uso entre soluções e Adobe Experience Platform exigem que essas bibliotecas diferentes sejam interdependentes, causando atrito na implantação.

Embora as tags na Experience Platform facilitem o máximo possível a implantação e o gerenciamento dessas bibliotecas, ainda há problemas com:

* Tamanho da biblioteca (excesso de código Adobe em uma página)
* Desempenho (os sites demoram muito para carregar)
* Várias chamadas para um único caso de uso
* Aguardar o retorno de ECID antes das chamadas de personalização (causa atraso)
* Coleta de dados fraturada (o que é uma evar?)
* Confusão de esquema entre soluções (A4T)
* Muitas outras coisas menos ótimas

Além disso, atualmente não há nenhuma biblioteca do JavaScript que envie dados diretamente para o Adobe Experience Platform.

### Com o Experience Platform Web SDK

O novo Web SDK envia dados das seguintes soluções para um único destino (Experience Platform Edge Network) e resolve os casos de uso mais comuns da solução mencionada acima.

* Adobe Analytics
* Adobe Audience Manager
* Adobe Target
* ID de visitante
* Adobe Experience Platform

Outras soluções serão seguidas.

O Adobe Experience Platform Web SDK também pode enviar dados diretamente para o Adobe Experience Platform. Esses dados estão no formato XDM e são mapeados para o esquema da solução do lado do servidor.

## Qual é o valor desse novo Web SDK?

**Desempenho:** o Web SDK é menor do que o uso de todas as bibliotecas Adobe atuais e fornece carregamentos de página significativamente mais rápidos.

**Simplicidade:** a combinação de XDM, Web SDK, tags, Edge Network, soluções da Adobe Experience Cloud e Adobe Experience Platform cria uma história de coleta de dados fácil de entender e simples de seguir.

* **XDM:** O esquema independente de solução usado para enviar dados para a Adobe. Não há mais tags para evars ou mboxes.
* **Web SDK:** facilita o envio e o recebimento de dados para o Adobe Experience Platform Edge Network.
* **Marcas:** simplifica a implantação e a configuração do Web SDK (e de qualquer outra marca da JavaScript) em um site.
* **Edge Network:** encaminhe facilmente os dados para a Adobe Experience Platform e soluções no formato necessário.
* **Soluções da Adobe Experience Platform e da Adobe:** Habilite a proposta de valor.

**Controle:** como todos os dados estão usando um único fluxo conectado de dados, você pode acompanhar e controlar logicamente como os dados são a cada milissegundo de sua jornada, de e para aplicativos.

**Moderno e pronto para o futuro:** O Web SDK e sua conexão com a Edge Network permitiram que o Adobe modernizasse significativamente a maneira como o Adobe lida com a coleta de dados, a personalização, o consentimento e o futuro dos cookies de terceiros. (Ele permite um domínio próprio, gerenciado pela Adobe.)

**Tempo de implantação:** o Adobe trabalhou duro (e continuará) para facilitar ao máximo a implantação da Web SDK através de marcas e mapear dados do lado do cliente para XDM. Depois que esse trabalho for concluído, todas as outras soluções da Adobe e os serviços da Adobe Experience Platform poderão ser ativados ou desativados no lado do servidor. Por exemplo, se estiver usando isso para o Adobe Analytics e quiser ativar o Target ou o Experience Platform, basta girar um botão na configuração do Fluxo de dados e ativar esses casos de uso.

## O que é o `alloy.js`?

`alloy.js` é o nome da biblioteca JavaScript do Web SDK. Ele é referenciado no código-fonte e no nome do arquivo do SDK.

## Os clientes precisam comprar o Adobe Experience Platform para usar o [!DNL Web SDK]?

Não. Qualquer cliente da Adobe Digital Experience pode usar o Adobe Experience Platform Web SDK gratuitamente.

* Os clientes que *não* têm acesso ao Experience Platform ou à Real-time CDP e desejam usar o [!DNL Web SDK] precisarão configurar as permissões corretas para criar esquemas e fluxos de dados na interface da Coleção de dados ou na interface do Experience Platform.
* Os clientes que têm acesso ao Experience Platform ou à Real-time CDP e desejam usar o [!DNL Web SDK] precisarão configurar as permissões certas para criar esquemas, conjuntos de dados, namespaces de identidade e fluxos de dados na interface da Coleção de dados ou na interface da Experience Platform.

Para obter mais informações sobre como configurar essas permissões, consulte nossa documentação em [gerenciamento de permissões de coleta de dados](https://experienceleague.adobe.com/docs/experience-platform/collection/permissions.html?lang=pt-BR).

## Quem deve usar o Web SDK?

O Adobe Experience Platform Web SDK foi desenvolvido para os seguintes clientes:

* Usuários do Adobe Experience Platform
   * Se você precisar enviar dados diretamente de um dispositivo para o Adobe Experience Platform, essa é a maneira oficialmente recomendada.
   * A Adobe está ciente de que o uso do conector do Adobe Analytics é mais rápido se você já tiver o Adobe Analytics, mas essa não é a estratégia de longo prazo para a coleta de dados.

* Clientes de soluções da Adobe Experience Cloud
   * Os novos clientes do Adobe Analytics, Adobe Audience Manager e Adobe Target devem começar com o novo Web SDK e não usar bibliotecas herdadas.
   * Os clientes existentes que desejam obter a implementação mais otimizada possível devem usar o novo Web SDK.

## Como faço para obter acesso ao Web SDK?

O Web SDK está atualmente disponível para o público em geral e pode ser usado para enviar dados para produtos da Adobe Experience Cloud. A capacidade de enviar dados para soluções de terceiros será disponibilizada em breve.

O SDK é oferecido gratuitamente e é hospedado pela Adobe. Se necessário, você pode baixá-lo e hospedá-lo em seus próprios servidores sem custo algum.

O Web SDK requer acesso às [configurações de sequência de dados](/help/datastreams/overview.md) e ao [construtor de esquema XDM](/help/xdm/tutorials/create-schema-ui.md) do Experience Platform para que os servidores da Adobe manipulem corretamente os dados de entrada provenientes da SDK. Se quiser obter acesso, entre em contato com a equipe de conta da Adobe para iniciar o processo de solicitação.

## Quais casos de uso são aceitos atualmente pelo Web SDK?

O Web SDK está evoluindo rapidamente. Mais casos de uso estão sendo trabalhados. Você pode encontrar a [lista de casos de uso atualmente suportados aqui.](https://github.com/orgs/adobe/projects/18/views/1?filterQuery=)

## Os clientes atuais precisam remarcar seus sites?

Depende. O Adobe Experience Platform Web SDK pode ser implantado em dois estilos diferentes. Um futuro documento de migração fornecerá detalhes adicionais.

* **Apenas outra marca:** Se o site já estiver marcado para soluções e você não puder remarcar, mas quiser enviar dados para o Adobe Experience Platform Edge Network para casos de uso do Experience Platform ou para os recursos de encaminhamento de eventos futuros (veja abaixo), você poderá adicionar a marca `alloy.js` ao site, onde ela funciona como &quot;apenas outra marca&quot;.

* **A única marca:** Se quiser usar o Web SDK para uma solução da Experience Cloud, você deverá usá-la para _todas_ as soluções nessa página. Por exemplo, se seu site já estiver marcado para o Adobe Analytics e você quiser usá-lo para o Target, será necessário usá-lo para ambos, bem como para qualquer outro no futuro.

Em outras palavras, se você decidir usar o Adobe Experience Platform Web SDK para casos de uso que não sejam de solução, poderá marcar o site com `alloy.js` e seguir em frente como se fosse uma nova solução. Se quiser usá-lo para o Adobe Analytics, Target ou Audience Manager, ou para casos de uso de aplicativos, talvez seja necessário remover qualquer um dos códigos herdados na página.

## Posso migrar as ECIDs quando começar a usar o Web SDK para que os visitantes do meu site não comecem a aparecer como novos visitantes?

Sim, o Adobe Experience Platform Web SDK fornece um recurso de Migração de identidade. Siga as instruções para migração de ID na [documentação de identidade do Experience Platform Web SDK](/help/collection/use-cases/identity/id-overview.md#migrating-visitor-api-ecid) para obter mais detalhes.

## Qual é a diferença entre o Web SDK e as tags?

* **As marcas no Experience Platform** gerenciam o código do dispositivo. Use-os para implantar o código com mais facilidade. Eles são livres e poderosos.

* **Adobe Experience Platform Web SDK** é o nome oficial do novo código que seria implantado por marcas para casos de uso do Adobe. É também livre e poderosa.

* **`alloy.js`** é o nome de arquivo do código Adobe Experience Platform Web SDK.

## Preciso usar tags para implantar a Web SDK?

Não. Você mesmo pode baixar o arquivo `alloy.js`.

No entanto:

* O Adobe Experience Platform Web SDK requer algo chamado ID de sequência de dados para que a rede de borda possa identificar o fluxo e determinar o que fazer com os dados. Essa ID é criada no Experience Platform. Isso não significa que você precisa usar a interface do para criar propriedades ou implantar o código JavaScript, mas sim usar tags para criar uma ID de configuração.

* As tags não são apenas a melhor tag disponível e o gerenciador do SDK, facilitam a implantação do `alloy.js` e o mapeamento de dados para esquemas XDM. Se decidir não usar marcas, será necessário gerenciar a implantação do `alloy.js`, a geração de eventos e o mapeamento de dados no XDM antes de enviá-los. Este é um processo _muito_ mais difícil do que o uso de tags.

* É recomendável usar marcas para implantar `alloy.js`, mesmo que seja a única marca para a qual você o usa.

## O que é encaminhamento de eventos?

Se você usa nossos SDKs e envia XDM para a Edge Network, esses novos recursos do encaminhamento de eventos permitem instalar novas extensões do lado do servidor e mapear esses dados para qualquer coisa — e enviá-la para qualquer lugar — em nossa rede de borda. Pense nisso como &quot;coleta de dados como um serviço&quot;. Ele estará disponível por um custo e será fornecido como parte do Adobe Experience Platform.

## O que é um CNAME ou domínio próprio e por que ele é importante?

Consulte o [programa de certificado gerenciado pela Adobe](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/data-collection/adobe-managed-cert) no guia dos Serviços principais.

## O Adobe Experience Platform Web SDK usa cookies? Em caso afirmativo, quais cookies ele usa?

Consulte [Cookies do Adobe Experience Platform Web SDK](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/data-collection/cookies/web-sdk) no guia dos Serviços principais.

## Quais navegadores são compatíveis com o Adobe Experience Platform Web SDK?

O Adobe Experience Platform Web SDK foi projetado para funcionar de maneira ideal nas versões mais recentes do Google Chrome, Safari, Firefox e Microsoft Edge Chromium. Você pode ter problemas ao usar determinados recursos em versões mais antigas de navegadores ou navegadores obsoletos, como o Internet Explorer.

## Onde posso obter o código-fonte para o Web SDK?

Consulte o repositório [Alloy](https://github.com/adobe/alloy) no GitHub.
