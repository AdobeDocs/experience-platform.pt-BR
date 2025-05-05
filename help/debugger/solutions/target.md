---
title: Testar uma implementação do Adobe Target com o Adobe Experience Platform Debugger
description: Saiba como usar o Adobe Experience Platform Debugger para testar e depurar um site habilitado com o Adobe Target.
exl-id: f99548ff-c6f2-4e99-920b-eb981679de2d
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 2%

---

# Testar uma implementação do Adobe Target com o Adobe Experience Platform Debugger

O Adobe Experience Platform Debugger fornece um conjunto de ferramentas úteis para testar e depurar um site que foi equipado com uma implementação do Adobe Target. Este guia aborda alguns fluxos de trabalho comuns e práticas recomendadas para usar o Experience Platform Debugger em um site habilitado para o Target.

## Pré-requisitos

Para usar o Experience Platform Debugger para Target, o site deve usar a [biblioteca at.js](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/) versão 1.x ou superior. As versões anteriores não são compatíveis.

## Inicializar o Experience Platform Debugger

Abra o site que deseja testar em um navegador e abra a extensão do Experience Platform Debugger.

Selecione **[!DNL Target]** na navegação à esquerda. Se o Experience Platform Debugger detectar que uma versão compatível da at.js está em execução no site, os detalhes de implementação do Adobe Target serão mostrados.

![O modo de exibição do Target selecionado no Experience Platform Debugger, indicando que o Adobe Target está ativo na página do navegador exibida no momento](../images/solutions/target/target-initialized.png)

## Informações de configuração global

As informações sobre a configuração global da implementação são exibidas na parte superior da exibição do Target no Experience Platform Debugger.

![Informações de configuração global do Target realçadas no Experience Platform Debugger](../images/solutions/target/global-config.png)

| Nome | Descrição |
| --- | --- |
| Código do cliente | Uma ID exclusiva que identifica a organização. |
| Versão | A versão da biblioteca Adobe Target instalada atualmente no site. |
| Nome da solicitação global | O nome da [mbox global](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/?) para a implementação do Target, sendo o nome padrão `target-global-mbox`. |
| Evento de carregamento de página | Um valor booliano que indica se um [evento de carregamento de página](https://developer.adobe.com/target/implement/client-side/atjs/how-atjs-works/how-atjs-works/#atjs-2x-diagrams) ocorreu. Os eventos de carregamento de página são compatíveis somente com a at.js 2.x. Para versões não compatíveis, esse valor é padronizado como `None`. |

{style="table-layout:auto"}

## [!DNL Network Requests] {#network}

Selecione **[!DNL Network Requests]** para exibir informações resumidas sobre cada solicitação de rede feita na página.

![A seção [!DNL Network Requests] do Destino selecionada no Experience Platform Debugger](../images/solutions/target/network-requests.png)

À medida que você executa ações na página (incluindo o recarregamento da página), novas colunas são adicionadas automaticamente à tabela, permitindo visualizar a sequência de ações e como os valores são alterados entre cada solicitação.

![A seção [!DNL Network Requests] do Destino selecionada no Experience Platform Debugger](../images/solutions/target/new-request.png)

Os seguintes valores são capturados:

| Nome | Descrição |
| --- | --- |
| [!DNL Page Title] | O título da página que iniciou esta solicitação. |
| [!DNL Page URL] | O URL da página que iniciou a solicitação. |
| [!DNL URL] | O URL bruto da solicitação. |
| [!DNL Method] | O método HTTP para a solicitação. |
| [!DNL Query String] | A string de consulta da solicitação, retirada do URL. |
| [!DNL POST Body] | O corpo da solicitação (definido somente para solicitações POST). |
| [!DNL Pathname] | O nome do caminho do URL da solicitação. |
| [!DNL Hostname] | O nome do host do URL da solicitação. |
| [!DNL Domain] | O domínio do URL da solicitação. |
| [!DNL Timestamp] | Um carimbo de data e hora de quando a solicitação (ou evento) ocorreu no fuso horário do navegador. |
| [!DNL Time Since Page Load] | O tempo decorrido desde o carregamento inicial da página no momento da solicitação. |
| [!DNL Initiator] | O iniciador da solicitação. Em outras palavras, quem fez o pedido? |
| [!DNL clientCode] | O identificador da conta da sua organização conforme reconhecido pelo Target. |
| [!DNL requestType] | A API usada para a solicitação. Se estiver usando a at.js 1.x, o valor será `/json`. Se estiver usando a at.js 2.x, o valor será `delivery`. |
| [!DNL Audience Manager Blob] | Fornece informações sobre metadados Audience Manager criptografados, conhecidos como &quot;blob&quot;. |
| [!DNL Audience Location Hint] | A ID da região de coleta de dados. Este é um identificador numérico para a localização geográfica de um data center de serviço de ID específico. Para obter mais informações, consulte a documentação do Audience Manager em [IDs de região, locais e nomes de host do DCS](https://experienceleague.adobe.com/docs/audience-manager/user-guide/api-and-sdk-code/dcs/dcs-api-reference/dcs-regions.html?lang=pt-BR) e o guia do Serviço de identidade da Experience Cloud em [`getLocationHint`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/getlocationhint.html?lang=pt-BR#reference-a761030ff06c4439946bb56febf42d4c). |
| [!DNL Browser Height] | A altura do navegador em pixels. |
| [!DNL Browser Time Offset] | O deslocamento de tempo do navegador associado ao seu fuso horário. |
| [!DNL Browser Width] | A largura do navegador em pixels. |
| [!DNL Color Depth] | A intensidade de cor da tela. |
| [!DNL context] | Um objeto que contém informações contextuais sobre o navegador usado para fazer a solicitação, incluindo dimensões de tela e plataforma do cliente. |
| [!DNL prefetch] | Os parâmetros usados em durante o processamento de `prefetch`. |
| [!DNL execute] | Os parâmetros usados durante o processamento de `execute`. |
| [!DNL Experience Cloud Visitor ID] | Se algum for detectado, fornecerá informações sobre a [Experience Cloud ID (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR) atribuída ao visitante do site atual. |
| [!DNL experienceCloud] | Contém as Experience Cloud IDs para esta sessão de usuário específica: uma [ID de dados complementares](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/before-implement.html?lang=pt-BR&#section_2C1F745A2B7D41FE9E30915539226E3A) do A4T e uma [ID de visitante (ECID)](https://experienceleague.adobe.com/docs/id-service/using/intro/overview.html?lang=pt-BR). |
| [!DNL id] | A [ID de Destino](https://developers.adobetarget.com/api/delivery-api/#section/Identifying-Visitors/Target-ID) do visitante. |
| [!DNL Mbox Host] | O [host](https://experienceleague.adobe.com/docs/target/using/administer/hosts.html?lang=pt-BR) ao qual a solicitação do Target foi feita. |
| [!DNL Mbox PC] | Uma cadeia de caracteres que encapsula a ID de sessão [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) e a dica de local [Adobe Target Edge](https://experienceleague.adobe.com/docs/target/using/introduction/how-target-works.html?lang=pt-BR#concept_0AE2ED8E9DE64288A8B30FCBF1040934). Esse valor é usado pela at.js para garantir que a sessão e o local do Edge permaneçam fixos. |
| [!DNL Mbox Referrer] | O referenciador de URL para a solicitação [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) específica. |
| [!DNL Mbox URL] | A URL do servidor [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/). |
| [!DNL Mbox Version] | A versão de [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/) que está sendo usada. |
| [!DNL mbox3rdPartyId] | O [`mbox3rdPartyId`](https://experienceleague.adobe.com/docs/target/using/audiences/visitor-profiles/3rd-party-id.html?lang=pt-BR) atribuído ao visitante atual. |
| [!DNL mboxRid] | A ID da solicitação [`mbox`](https://developer.adobe.com/target/implement/client-side/atjs/global-mbox/global-mbox-overview/). |
| [!DNL requestId] | Um identificador exclusivo para a solicitação. |
| [!DNL Screen Height] | A altura da tela em pixels. |
| [!DNL Screen Width] | A largura da tela em pixels. |
| [!DNL Supplemental Data ID] | Uma ID gerada pelo sistema usada para corresponder visitantes com chamadas correspondentes do Adobe Target e do Adobe Analytics. Consulte o [guia de solução de problemas do A4T](https://experienceleague.adobe.com/docs/target/using/integrate/a4t/troubleshoot-a4t/a4t-troubleshooting.html?lang=pt-BR&#section_75002584FA63456D8D9086172925DD8D) para obter mais informações. |
| [!DNL vst] | A [configuração da API do Experience Cloud Identity Service](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/configurations/function-vars.html?lang=pt-BR). |
| [!DNL webGLRenderer] | Fornece informações sobre o renderizador WebGL usado na página, se aplicável. |

{style="table-layout:auto"}

Para exibir os detalhes de um parâmetro em um evento de rede específico, selecione a célula da tabela em questão. Um popover é exibido fornecendo mais informações sobre o parâmetro, incluindo uma descrição e seu valor. Se o valor for um objeto JSON, a caixa de diálogo incluirá uma visualização totalmente navegável da estrutura do objeto.

![A seção [!DNL Network Requests] do Destino selecionada no Experience Platform Debugger](../images/solutions/target/request-param-details.png)

## [!DNL Configuration]

Selecione **[!DNL Configuration]** para habilitar ou desabilitar uma seleção de ferramentas de depuração adicionais para o Target.

![A seção [!DNL Configuration Requests] do Destino selecionada no Experience Platform Debugger](../images/solutions/target/configuration.png)

| Ferramenta de depuração | Descrição |
| --- | --- |
| [!DNL Target Console Logging] | Quando ativado, permite acessar os logs do at.js na guia do console do navegador. Este recurso também pode ser habilitado ao adicionar um parâmetro de consulta `mboxDebug` (com qualquer valor) à URL do navegador. |
| [!DNL Target Disable] | Quando ativadas, todas as funcionalidades do Target são desativadas na página. Isso pode ser usado para determinar se uma oferta específica do Target está causando o problema na página. |
| [!DNL Target Trace] | **Observação**: você deve estar conectado para habilitar este recurso.<br><br>Quando habilitados, os tokens de rastreamento são enviados com cada busca e um objeto de rastreamento é retornado em cada resposta. `at.js` analisa a resposta `window.__targetTraces`. Cada objeto de rastreamento contém as mesmas informações que a guia [[!DNL Network Requests]], com as seguintes adições:<ul><li>Um instantâneo de perfil, que permite ver atributos antes e depois das solicitações.</li><li>[atividades](https://experienceleague.adobe.com/docs/target/using/activities/target-activities-guide.html?lang=pt-BR) correspondentes e não correspondentes, mostrando por que o perfil atual se qualificou ou não para atividades específicas.<ul><li>Isso pode ajudar a identificar para quais públicos um perfil está se qualificando em um determinado momento e por quê.</li><li>Os documentos do Target contêm mais informações sobre diferentes tipos de atividades</li></ul></li></ul> |

{style="table-layout:auto"}
