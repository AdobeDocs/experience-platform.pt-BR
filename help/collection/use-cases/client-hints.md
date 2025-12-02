---
title: Dicas do cliente do agente do usuário
description: Saiba como as dicas do cliente do agente do usuário funcionam no Web SDK. As dicas do cliente permitem que os proprietários de sites acessem muitas das mesmas informações disponíveis na sequência de agente do usuário, mas com mais privacidade.
keywords: user-agent;client hints; string; sequência user-agent; baixa entropia; alta entropia
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '1230'
ht-degree: 3%

---

# Dicas do cliente do agente do usuário

## Visão geral {#overview}

Toda vez que um navegador faz uma solicitação a um servidor Web, o cabeçalho da solicitação inclui informações sobre o navegador e o ambiente no qual o navegador está em execução. Todos esses dados são agregados em uma sequência, chamada de sequência de agente do usuário.

Este é um exemplo da aparência de uma sequência de agente do usuário em uma solicitação proveniente de um navegador Chrome em execução em um dispositivo [!DNL Mac OS].

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

>[!NOTE]
>
>Ao longo dos anos, a quantidade de informações de navegador e dispositivo incluída na sequência de agente do usuário cresceu e foi modificada várias vezes. O exemplo acima mostra uma seleção das informações mais comuns do agente do usuário.

| Campo | Valor |
|---|---|
| Nome do software | `Chrome` |
| Versão do software | `105` |
| Versão completa do software | `105.0.0.0` |
| Nome do mecanismo de layout | `AppleWebKit` |
| Versão do mecanismo de layout | `537.36` |
| Sistema operacional | `Mac OS X` |
| Versão do sistema operacional | `10.15.7` |
| Dispositivo | `Intel Mac OS X 10_15_7` |

## Casos de uso {#use-cases}

As sequências de agente do usuário vêm sendo usadas há muito tempo para fornecer às equipes de marketing e desenvolvimento insights importantes sobre como navegadores, sistemas operacionais e dispositivos exibem o conteúdo do site, bem como sobre como os usuários interagem com os sites.

As cadeias de caracteres do agente do usuário também são usadas para bloquear spam e filtrar bots que rastreiam sites para vários fins adicionais.

## Strings de agente do usuário no Adobe Experience Cloud {#user-agent-in-adobe}

As soluções da Adobe Experience Cloud utilizam as sequências de agente do usuário de várias maneiras.

* A Adobe Analytics utiliza a sequência de agente do usuário para aumentar e obter informações adicionais relacionadas a sistemas operacionais, navegadores e dispositivos usados para visitar um site.
* O Adobe Audience Manager e o Adobe Target qualificam os usuários finais para campanhas de segmentação e personalização, com base nas informações fornecidas pela sequência de agente do usuário.

## Apresentando dicas do cliente do agente do usuário {#ua-ch}

Nos últimos anos, os proprietários de sites e fornecedores de marketing têm usado strings de agente do usuário juntamente com outras informações incluídas nos cabeçalhos de solicitação para criar impressões digitais. Essas impressões digitais podem ser usadas como meio de identificar usuários sem o conhecimento deles.

Apesar do importante propósito das cadeias de caracteres do agente do usuário para os proprietários do site, os desenvolvedores de navegador decidiram alterar como as cadeias de caracteres do agente do usuário operam, a fim de limitar possíveis problemas de privacidade para os usuários finais.

A solução que eles desenvolveram é chamada de [user agent client hints](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). As dicas do cliente ainda permitem que os sites coletem as informações necessárias do navegador, do sistema operacional e do dispositivo, além de fornecer maior proteção contra métodos de rastreamento ocultos, como impressão digital.

As dicas do cliente permitem que os proprietários de sites acessem muitas das mesmas informações disponíveis na sequência de agente do usuário, mas com mais privacidade.

Quando navegadores modernos enviam um usuário para um servidor Web, a sequência de agente do usuário é enviada em cada solicitação, independentemente da necessidade. As dicas do cliente, por outro lado, executam um modelo em que o servidor deve solicitar ao navegador as informações adicionais que ele deseja saber sobre o cliente. Ao receber essa solicitação, o navegador pode aplicar suas próprias políticas ou configurações do usuário para determinar quais dados são retornados. Em vez de expor toda a sequência do agente do usuário por padrão em todas as solicitações, o acesso agora é gerenciado de forma explícita e auditável.

## Suporte ao navegador {#browser-support}

[As dicas do cliente do agente do usuário](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) foram introduzidas com [!DNL Google Chrome] versão 89.

Outros navegadores baseados em Chromium são compatíveis com a API Client Hints, como:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Categorias {#categories}

Há duas categorias de dicas do cliente do agente do usuário:

* [Dicas do cliente de baixa entropia](#low-entropy)
* [Dicas do cliente de alta entropia](#high-entropy)

### Dicas do cliente de baixa entropia {#low-entropy}

As dicas de cliente de baixa entropia incluem informações básicas que não podem ser usadas para imprimir digitais nos usuários. Informações como marca do navegador, plataforma e se a solicitação vem de um dispositivo móvel.

As dicas de cliente de baixa entropia são ativadas por padrão no Web SDK e são transmitidas a cada solicitação.

| Cabeçalho HTTP | JavaScript | Incluído no usuário-agente por padrão | Incluído nas dicas do cliente por padrão |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Sim | Sim |
| `Sec-CH-UA-Platform` | `platform` | Sim | Sim |
| `Sec-CH-UA-Mobile` | `mobile` | Sim | Sim |

### Dicas do cliente de alta entropia {#high-entropy}

As dicas de alta entropia do cliente são informações mais detalhadas sobre o dispositivo cliente, como a versão da plataforma, arquitetura, modelo, bits (plataformas de 64 ou 32 bits) ou a versão completa do sistema operacional. Essas informações poderiam ser potencialmente usadas na impressão digital.

| Propriedade | Descrição | Cabeçalho HTTP | Caminho XDM | Exemplo | Incluído no agente do usuário por padrão | Incluído nas dicas do cliente por padrão |
| --- | --- | --- | --- | --- |---|---|
| Versão do sistema operacional | A versão do sistema operacional. | `Sec-CH-UA-Platform-Version` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.platformVersion` | `10.15.7` | Sim | Não |
| Arquitetura | A arquitetura subjacente do CPU. | `Sec-CH-UA-Arch` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.architecture` | `x86` | Sim | Não |
| Modelo do dispositivo | O nome do dispositivo usado. | `Sec-CH-UA-Model` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.model` | `Intel Mac OS X 10_15_7` | Sim | Não |
| Bitness | O número de bits que a arquitetura subjacente do CPU suporta. | `Sec-CH-UA-Bitness` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.bitness` | `64` | Sim | Não |
| Fornecedor do navegador | A empresa que criou o navegador. A dica de baixa entropia `Sec-CH-UA` também coleta esse elemento. | `Sec-CH-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.vendor` | `Google` | Sim | Não |
| Nome do navegador | O navegador usado. A dica de baixa entropia `Sec-CH-UA` também coleta esse elemento. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.brand` | `Chrome` | Sim | Não |
| Versão do navegador | A versão significativa do navegador. A dica de baixa entropia `Sec-CH-UA` também coleta esse elemento. A versão exata do navegador não é coletada automaticamente. | `Sec-UA-Full-Version-List` | `xdm.environment.browserDetails.`<br>`userAgentClientHints.version` | `105` | Sim | Não |


As dicas de cliente de alta entropia são desativadas por padrão no Web SDK. Para ativá-los, você deve configurar manualmente o Web SDK para solicitar dicas de cliente de alta entropia.

## Impacto das dicas de cliente de alta entropia nas soluções da Experience Cloud {#impact-in-experience-cloud-solutions}

Algumas soluções da Adobe Experience Cloud dependem das informações incluídas nas dicas de cliente de alta entropia ao gerar relatórios.

Se você não ativar dicas de cliente de alta entropia em seu ambiente, os relatórios e características do Adobe Analytics e do Audience Manager descritos abaixo não funcionarão.

### Relatórios do Adobe Analytics que dependem de dicas de cliente de alta entropia {#analytics}

A dimensão [Sistema operacional](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) inclui a versão do sistema operacional que é armazenada como uma dica de cliente de alta entropia. Se as dicas de clientes de alta entropia não estiverem ativadas, a versão do sistema operacional pode ser imprecisa para ocorrências coletadas dos navegadores Chromium.

### Características do Audience Manager que dependem de dicas de cliente de alta entropia {#aam}

[!DNL Google] atualizou a funcionalidade do navegador [!DNL Chrome] para minimizar as informações coletadas pelo cabeçalho `User-Agent`. Como resultado, os clientes do Audience Manager que usam o [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=pt-BR) não receberão mais informações confiáveis de características com base nas [chaves de nível de plataforma](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html).

Os clientes do Audience Manager que usam chaves de nível de plataforma para direcionamento devem alternar para [Coleção de Dados do Adobe Experience Platform](/help/collection/home.md) em vez de [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=pt-BR) e habilitar as [Dicas de Cliente de Alta Entropia](#enabling-high-entropy-client-hints) para continuar recebendo dados de características confiáveis.

## Ativação de dicas de cliente de alta entropia {#enabling-high-entropy-client-hints}

Para habilitar dicas de cliente de alta entropia na implantação do Web SDK, você deve incluir a opção de contexto `highEntropyUserAgentHints` adicional no campo [`context`](/help/collection/js/commands/configure/context.md).

Por exemplo, para recuperar dicas de cliente de alta entropia de propriedades da Web, sua configuração seria semelhante a:

`context: ["highEntropyUserAgentHints", "web"]`

## Exemplo {#example}

As dicas do cliente contidas nos cabeçalhos da primeira solicitação feita pelo navegador a um servidor da web conterão a marca do navegador, a versão principal do navegador e um indicador de se o cliente é um dispositivo móvel. Cada parte dos dados terá seu próprio valor de cabeçalho em vez de ser agrupada em uma única sequência de agente do usuário, conforme mostrado abaixo:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

O cabeçalho [!DNL User-Agent] equivalente para o mesmo navegador seria semelhante a:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Embora as informações sejam semelhantes, a primeira solicitação para o servidor contém dicas do cliente. Eles incluem apenas um subconjunto do que está disponível na sequência de agente do usuário. Faltam na solicitação a arquitetura do sistema operacional, a versão completa do sistema operacional, o nome do mecanismo de layout, a versão do mecanismo de layout e a versão completa do navegador.

No entanto, em solicitações subsequentes, o [!DNL Client Hints API] permite que os servidores da Web solicitem detalhes adicionais sobre o dispositivo. Quando esses valores são solicitados, dependendo da política do navegador ou das configurações do usuário, a resposta do navegador pode incluir essas informações.

Veja abaixo um exemplo do objeto JSON retornado por [!DNL Client Hints API] quando valores de alta entropia são solicitados:


```json
{
   "architecture":"x86",
   "bitness":"64",
   "brands":[
      {
         "brand":" Not A;Brand",
         "version":"99"
      },
      {
         "brand":"Chromium",
         "version":"100"
      },
      {
         "brand":"Google Chrome",
         "version":"100"
      }
   ],
   "fullVersionList":[
      {
         "brand":" Not A;Brand",
         "version":"99.0.0.0"
      },
      {
         "brand":"Chromium",
         "version":"100.0.4896.127"
      },
      {
         "brand":"Google Chrome",
         "version":"100.0.4896.127"
      }
   ],
   "mobile":false,
   "model":"",
   "platformVersion":"12.2.1"
}
```
