---
title: Dicas do cliente do agente do usuário
description: Saiba como as dicas do cliente do agente do usuário funcionam no SDK da Web. As dicas do cliente permitem que os proprietários de sites acessem muitas das mesmas informações disponíveis na sequência de agente do usuário, mas com mais privacidade.
keywords: user-agent;client hints; string; sequência user-agent; baixa entropia; alta entropia
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: e300e57df998836a8c388511b446e90499185705
workflow-type: tm+mt
source-wordcount: '1192'
ht-degree: 7%

---

# Dicas do cliente do agente do usuário

## Visão geral {#overview}

Toda vez que um navegador faz uma solicitação a um servidor Web, o cabeçalho da solicitação inclui informações sobre o navegador e o ambiente no qual o navegador está em execução. Todos esses dados são agregados em uma sequência, chamada de sequência de agente do usuário.

Este é um exemplo da aparência de uma sequência de agente do usuário em uma solicitação proveniente de um navegador Chrome em execução em uma [!DNL Mac OS] dispositivo.

>[!NOTE]
>
>Ao longo dos anos, a quantidade de informações de navegador e dispositivo incluída na sequência de agente do usuário cresceu e foi modificada várias vezes. O exemplo abaixo mostra uma seleção das informações mais comuns do agente do usuário.

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/105.0.0.0 Safari/537.36`
```

| Campo | Valor |
|---|---|
| Nome do software | Google Chrome |
| Versão do software | 105 |
| Versão completa do software | 105.0.0.0 |
| Nome do mecanismo de layout | AppleWebKit |
| Versão do mecanismo de layout | 537.36 |
| Sistema operacional | Mac OS X |
| Versão do sistema operacional | 10.15.7 |
| Dispositivo | SO Mac X 10_15_7 |

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

A solução que eles desenvolveram é chamada de [dicas do cliente do agente do usuário](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). As dicas do cliente ainda permitem que os sites coletem as informações necessárias do navegador, do sistema operacional e do dispositivo, além de fornecer maior proteção contra métodos de rastreamento ocultos, como impressão digital.

As dicas do cliente permitem que os proprietários de sites acessem muitas das mesmas informações disponíveis na sequência de agente do usuário, mas com mais privacidade.

Quando navegadores modernos enviam um usuário para um servidor Web, a sequência de agente do usuário é enviada em cada solicitação, independentemente da necessidade. As dicas do cliente, por outro lado, executam um modelo em que o servidor deve solicitar ao navegador as informações adicionais que ele deseja saber sobre o cliente. Ao receber essa solicitação, o navegador pode aplicar suas próprias políticas ou configurações do usuário para determinar quais dados são retornados. Em vez de expor toda a sequência do agente do usuário por padrão em todas as solicitações, o acesso agora é gerenciado de forma explícita e auditável.

## Suporte ao navegador {#browser-support}

[Dicas do cliente do agente do usuário](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) foram introduzidos com [!DNL Google Chrome]versão 89.

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

As dicas de cliente de baixa entropia são ativadas por padrão no SDK da Web e são transmitidas a cada solicitação.

| Cabeçalho HTTP | JavaScript | Incluído no usuário-agente por padrão | Incluído nas dicas do cliente por padrão |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Sim | Sim |
| `Sec-CH-UA-Platform` | `platform` | Sim | Sim |
| `Sec-CH-UA-Mobile` | `mobile` | Sim | Sim |

### Dicas do cliente de alta entropia {#high-entropy}

As dicas de alta entropia do cliente são informações mais detalhadas sobre o dispositivo cliente, como a versão da plataforma, arquitetura, modelo, bits (plataformas de 64 ou 32 bits) ou a versão completa do sistema operacional. Essas informações poderiam ser potencialmente usadas na impressão digital.

| Cabeçalho HTTP | JavaScript | Incluído no agente do usuário por padrão | Incluído nas dicas do cliente por padrão |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | Sim | Não |
| `Sec-CH-UA-Arc` | `architecture` | Sim | Não |
| `Sec-CH-UA-Model` | `model` | Sim | Não |
| `Sec-CH-UA-Bitness` | `Bitness` | Sim | Não |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | Sim | Não |

As dicas de cliente de alta entropia são desativadas por padrão no SDK da Web. Para habilitá-los, você deve configurar manualmente o SDK da Web para solicitar dicas de cliente de alta entropia.

## Impacto das dicas do cliente de alta entropia nas soluções Experience Cloud {#impact-in-experience-cloud-solutions}

Algumas soluções da Adobe Experience Cloud dependem das informações incluídas nas dicas de cliente de alta entropia ao gerar relatórios.

Se você não ativar dicas de cliente de alta entropia em seu ambiente, os relatórios e características do Adobe Analytics e do Audience Manager descritos abaixo não funcionarão.

### Relatórios do Adobe Analytics que dependem de dicas de cliente de alta entropia {#analytics}

A variável [Sistema operacional](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html?lang=pt-BR) dimensão inclui a versão do sistema operacional que é armazenada como uma dica de cliente de alta entropia. Se as dicas de clientes de alta entropia não estiverem ativadas, a versão do sistema operacional pode ser imprecisa para ocorrências coletadas dos navegadores Chromium.

### Características de Audience Manager que dependem de dicas de cliente de alta entropia {#aam}

[!DNL Google] atualizou o [!DNL Chrome] funcionalidade do navegador para minimizar as informações coletadas por meio do `User-Agent` cabeçalho. Como resultado, os clientes do Audience Manager que usam o [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=pt-BR) não receberão mais informações confiáveis para características com base em [chaves de nível de plataforma](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/traits/trait-device-targeting.html).

Os clientes do Audience Manager que usam chaves de nível de plataforma para direcionamento devem mudar para [Experience Platform Web SDK](https://experienceleague.adobe.com/docs/experience-platform/edge/home.html?lang=pt-BR) em vez de [DIL](https://experienceleague.adobe.com/docs/audience-manager/user-guide/dil-api/dil-overview.html?lang=pt-BR)e habilitar [Client Hints de alta entropia](#enabling-high-entropy-client-hints) para continuar recebendo dados de características confiáveis.

## Ativação de dicas de cliente de alta entropia {#enabling-high-entropy-client-hints}

Para habilitar dicas de cliente de alta entropia na implantação do SDK da Web, você deve incluir as dicas adicionais `highEntropyUserAgentHints` opção de contexto, conforme descrito na [documentação de configuração](configuring-the-sdk.md#context), juntamente com a configuração existente.

Por exemplo, para recuperar dicas de cliente de alta entropia de propriedades da Web, sua configuração seria semelhante a:

`context: ["highEntropyUserAgentHints", "web"]`

## Exemplo {#example}

As dicas do cliente contidas nos cabeçalhos da primeira solicitação feita pelo navegador a um servidor da web conterão a marca do navegador, a versão principal do navegador e um indicador de se o cliente é um dispositivo móvel. Cada parte dos dados terá seu próprio valor de cabeçalho em vez de ser agrupada em uma única sequência de agente do usuário, conforme mostrado abaixo:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

O equivalente [!DNL User-Agent] para o mesmo navegador seria semelhante a:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Embora as informações sejam semelhantes, a primeira solicitação para o servidor contém dicas do cliente. Eles incluem apenas um subconjunto do que está disponível na sequência de agente do usuário. Faltam na solicitação a arquitetura do sistema operacional, a versão completa do sistema operacional, o nome do mecanismo de layout, a versão do mecanismo de layout e a versão completa do navegador.

No entanto, em pedidos subsequentes, a [!DNL Client Hints API] permite que os servidores da web solicitem detalhes adicionais sobre o dispositivo. Quando esses valores são solicitados, dependendo da política do navegador ou das configurações do usuário, a resposta do navegador pode incluir essas informações.

Veja abaixo um exemplo do objeto JSON retornado pelo [!DNL Client Hints API] quando valores de alta entropia são solicitados:


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
