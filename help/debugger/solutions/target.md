---
title: Testar uma implementação do Adobe Target com o Adobe Experience Platform Debugger
description: Saiba como usar o Adobe Experience Platform Debugger para testar e depurar um site habilitado com o Adobe Target.
source-git-commit: 1ce7ac78936040d76faa3a58b92333a737fbeb66
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 5%

---

# Testar uma implementação do Adobe Target com o Adobe Experience Platform Debugger

O Adobe Experience Platform Debugger fornece um conjunto de ferramentas úteis para testar e depurar um site que foi criado com uma implementação do Adobe Target. Este guia aborda alguns fluxos de trabalho comuns e práticas recomendadas para usar o Platform Debugger em um site habilitado para o Target.

## Pré-requisitos

Para usar o Platform Debugger para Target, o site deve usar o [Biblioteca da at.js](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) versão 1.x ou superior. As versões anteriores não são compatíveis.

## Inicializando o Platform Debugger

Abra o site que deseja testar em um navegador e abra a extensão do Platform Debugger.

Selecionar **[!DNL Target]** no painel de navegação esquerdo. Se o Platform Debugger detectar que uma versão compatível da at.js está em execução no site, os detalhes de implementação do Adobe Target serão mostrados.

![A exibição do Target selecionada no Platform Debugger, indicando que o Adobe Target está ativo na página do navegador exibida no momento](../images/solutions/target/target-initialized.png)

## Informações de configuração global

As informações sobre a configuração global da implementação são exibidas na parte superior da exibição do Target no Platform Debugger.

![Informações de configuração global do Target destacadas no Platform Debugger](../images/solutions/target/global-config.png)

| Nome | Descrição |
| --- | --- |
| Código do cliente | Uma ID exclusiva que identifica a organização. |
| Versão | A versão da biblioteca do Adobe Target instalada no site. |
| Nome da solicitação global | O nome do [mbox global](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) para a implementação do Target, o nome padrão é `target-global-mbox`. |
| Evento de carregamento de página | Um valor booleano indicando se uma [evento de carregamento de página](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) ocorreu. Os eventos de carregamento de página são compatíveis apenas com a at.js 2.x. Para versões não compatíveis, esse valor assume como padrão `None`. |

{style=&quot;table-layout:auto&quot;}

## [!DNL Network Requests] {#network}

Selecionar **[!DNL Network Requests]** para exibir informações de resumo em cada solicitação de rede feita na página.

![O [!DNL Network Requests] seção para Target selecionado no Platform Debugger](../images/solutions/target/network-requests.png)

À medida que você executa ações na página (incluindo o recarregamento da página), novas colunas são adicionadas automaticamente à tabela, permitindo que você visualize a sequência de ações e como os valores são alterados entre cada solicitação.

![O [!DNL Network Requests] seção para Target selecionado no Platform Debugger](../images/solutions/target/new-request.png)

Os seguintes valores são capturados:

| Nome | Descrição |
| --- | --- |
| [!DNL Page Title] | O título da página que iniciou esta solicitação. |
| [!DNL Page URL] | O URL da página que iniciou a solicitação. |
| [!DNL URL] | O URL bruto da solicitação. |
| [!DNL Method] | O método HTTP para a solicitação. |
| [!DNL Query String] | A string de consulta da solicitação, retirada do URL. |
| [!DNL POST Body] | O corpo da solicitação (definido somente para solicitações de POST). |
| [!DNL Pathname] | O nome do caminho da URL da solicitação. |
| [!DNL Hostname] | O nome do host do URL da solicitação. |
| [!DNL Domain] | O domínio do URL da solicitação. |
| [!DNL Timestamp] | Um carimbo de data e hora de quando a solicitação (ou evento) ocorreu, dentro do fuso horário do navegador. |
| [!DNL Time Since Page Load] | O tempo decorrido desde o carregamento inicial da página no momento da solicitação. |
| [!DNL Initiator] | O iniciador da solicitação. Por outras palavras, quem apresentou o pedido? |
| [!DNL clientCode] | O identificador da conta de sua organização, conforme reconhecido pelo Target. |
| [!DNL requestType] | A API usada para a solicitação. Se estiver usando a at.js 1.x, o valor será `/json`. Se estiver usando a at.js 2.x, o valor será `delivery`. |
| [!DNL Audience Manager Blob] | Fornece informações sobre metadados de Audience Manager criptografados, chamados de &quot;blob&quot;. |
| [!DNL Audience Location Hint] | A ID da região de coleta de dados. Este é um identificador numérico para a localização geográfica de um data center de serviço de ID específico. Para obter mais informações, consulte a documentação do Audience Manager em [IDs da região do DCS, locais e nomes de host](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=pt-BR) e o guia do serviço de identidade do Experience Cloud em [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=en#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | A altura do navegador em pixels. |
| [!DNL Browser Time Offset] | O deslocamento de tempo do navegador associado ao seu fuso horário. |
| [!DNL Browser Width] | A largura do navegador em pixels. |
| [!DNL Color Depth] | A intensidade de cor da tela. |
| [!DNL context] | Um objeto que contém informações contextuais sobre o navegador usado para fazer a solicitação, incluindo dimensões de tela e plataforma do cliente. |
| [!DNL prefetch] | Os parâmetros usados durante `prefetch` processamento. |
| [!DNL execute] | Os parâmetros usados durante `execute` processamento. |
| [!DNL Experience Cloud Visitor ID] | Se um for detectado, o fornece informações sobre o [Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) que é atribuído ao visitante atual do site. |
| [!DNL experienceCloud] | Retém as IDs de Experience Cloud para esta sessão de usuário específica: a4T [ID de dados complementares](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?#section_2C1F745A2B7D41FE9E30915539226E3A)e um [ID de visitante (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html). |
| [!DNL id] | O [ID de destino](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) para o visitante. |
| [!DNL Mbox Host] | O [host](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html) que a solicitação do Target foi feita. |
| [!DNL Mbox PC] | Uma string que encapsula o [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) a ID da sessão e o [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html#concept_0AE2ED8E9DE64288A8B30FCBF1040934) dica de localização. Esse valor é usado pela at.js para garantir que a sessão e o local da borda permaneçam fixos. |
| [!DNL Mbox Referrer] | O referenciador de URL para o [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) solicitação. |
| [!DNL Mbox URL] | O URL da variável [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) servidor. |
| [!DNL Mbox Version] | A versão de [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) em uso. |
| [!DNL mbox3rdPartyId] | O [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html) atribuído ao visitante atual. |
| [!DNL mboxRid] | O [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) ID da solicitação. |
| [!DNL requestId] | Uma ID exclusiva para a solicitação. |
| [!DNL Screen Height] | A altura da tela em pixels. |
| [!DNL Screen Width] | A largura da tela em pixels. |
| [!DNL Supplemental Data ID] | Uma ID gerada pelo sistema usada para corresponder os visitantes com chamadas Adobe Target e Adobe Analytics correspondentes. Consulte a [Guia de solução de problemas do A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?#section_75002584FA63456D8D9086172925DD8D) para obter mais informações. |
| [!DNL vst] | O [Configuração da API do serviço de identidade do Experience Cloud](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html). |
| [!DNL webGLRenderer] | Fornece informações sobre o renderizador WebGL usado na página, se aplicável. |

{style=&quot;table-layout:auto&quot;}

Para exibir os detalhes de um parâmetro em um evento de rede específico, selecione a célula da tabela em questão. Um provedor é exibido fornecendo mais informações sobre o parâmetro, incluindo uma descrição e seu valor. Se o valor for um objeto JSON, a caixa de diálogo incluirá uma exibição totalmente navegável da estrutura do objeto.

![O [!DNL Network Requests] seção para Target selecionado no Platform Debugger](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

Selecionar **[!DNL Configuration]** para ativar ou desativar uma seleção de ferramentas de depuração adicionais para o Target.

![O [!DNL Configuration Requests] seção para Target selecionado no Platform Debugger](../images/solutions/target/configuration.png)

| Ferramenta de depuração | Descrição |
| --- | --- |
| [!DNL Target Console Logging] | Quando ativado, o permite acessar os logs do at.js na guia do console do navegador. Esse recurso também pode ser ativado ao adicionar um `mboxDebug` parâmetro de consulta (com qualquer valor) para o URL do navegador. |
| [!DNL Target Diable] | Quando ativadas, todas as funcionalidades do Target são desativadas na página. Isso pode ser usado para determinar se uma oferta específica do Target está causando o problema na página. |
| [!DNL Target Trace] | **Observação**: Você deve estar conectado para ativar esse recurso.<br><br>Quando ativados, os tokens de rastreamento são enviados com cada busca e um objeto de rastreamento é retornado em cada resposta. `at.js` analisa a resposta `window.__targetTraces`. Cada objeto de rastreamento contém as mesmas informações que o [[!DNL Network Requests] guia], com as seguintes adições:<ul><li>Um instantâneo do perfil, que permite visualizar atributos antes e depois de solicitações.</li><li>Correspondente e sem correspondência [atividades](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html), mostrando por que o perfil atual se qualificou ou não para atividades específicas.<ul><li>Isso pode ajudar a identificar para quais públicos-alvo um perfil está se qualificando em um determinado ponto e por quê.</li><li>Os documentos do Target contêm mais informações sobre tipos diferentes de atividades</li></ul></li></ul> |

{style=&quot;table-layout:auto&quot;}