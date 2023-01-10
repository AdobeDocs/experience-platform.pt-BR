---
title: Dicas do cliente do agente do usuário
description: Saiba como as Dicas do cliente do agente-usuário funcionam no SDK da Web
keywords: agente do usuário;dicas do cliente; string; sequência agente-utilizador; baixa entropia; alta entropia
exl-id: a909b1d1-be9d-43ba-bb4b-d28b0c609f65
source-git-commit: 4a2ae40fc64c4340ddb05db881c2176bb2aedc46
workflow-type: tm+mt
source-wordcount: '1065'
ht-degree: 5%

---

# Dicas do cliente do agente do usuário

## Visão geral {#overview}

Toda vez que um navegador da Web faz uma solicitação a um servidor da Web, o cabeçalho da solicitação inclui informações sobre o navegador e o ambiente no qual o navegador está sendo executado. Todos esses dados são agregados em uma sequência de caracteres, chamada de [!DNL User-Agent] string.

Este é um exemplo de como uma [!DNL User-Agent] string é semelhante a uma solicitação proveniente de um navegador Chrome em execução em um [!DNL Mac OS] dispositivo.

>[!NOTE]
>
>Ao longo dos anos, a quantidade de informações de navegador e dispositivo incluída no [!DNL User-Agent] a sequência de caracteres foi expandida e modificada várias vezes. O exemplo abaixo mostra uma seleção dos mais comuns [!DNL User-Agent] informações.

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
| Dispositivo | Mac OS X 10_15_7 da Intel |

## Casos de uso {#use-cases}

[!DNL User-Agent] As strings são usadas há muito para fornecer às equipes de marketing e desenvolvimento informações importantes sobre como os navegadores, sistemas operacionais e dispositivos exibem o conteúdo do site, bem como sobre como os usuários interagem com os sites.

[!DNL User-Agent] as cadeias de caracteres também são usadas para bloquear spam e filtrar bots que rastreiam sites para uma variedade de finalidades adicionais.

## [!DNL User-Agent] strings no Adobe Experience Cloud {#user-agent-in-adobe}

As soluções da Adobe Experience Cloud utilizam o [!DNL User-Agent] strings de várias maneiras.

* A Adobe Analytics utiliza o [!DNL User-Agent] aumentar e derivar informações adicionais relacionadas a sistemas operacionais, navegadores e dispositivos usados para visitar um site.
* O Adobe Audience Manager e a Adobe Target qualificam os usuários finais para campanhas de segmentação e personalização com base nas informações fornecidas pela [!DNL User-Agent] string.

## Apresentando dicas do cliente do agente do usuário {#ua-ch}

Nos últimos anos, proprietários de sites e fornecedores de marketing usaram [!DNL User-Agent] strings juntamente com outras informações incluídas nos cabeçalhos de solicitação para criar impressões digitais. Estas impressões digitais podem ser utilizadas como meio de identificação dos utilizadores sem o seu conhecimento.

Apesar do importante objetivo [!DNL User-Agent] servidores de strings para proprietários de sites, os desenvolvedores de navegadores decidiram mudar como [!DNL User-Agent] As cadeias de caracteres operam para limitar possíveis problemas de privacidade para os usuários finais.

A solução que eles desenvolveram é chamada de [Dicas do cliente do agente do usuário](https://developer.chrome.com/docs/privacy-sandbox/user-agent/). As dicas do cliente ainda permitem que os sites coletem as informações necessárias do navegador, sistema operacional e dispositivo, além de fornecer maior proteção contra métodos de rastreamento ocultos, como impressão digital.

As dicas do cliente permitem que os proprietários do site acessem grande parte das mesmas informações disponíveis no [!DNL User-Agent] , mas de uma maneira mais preservada da privacidade.

Quando navegadores modernos enviam um usuário para um servidor da Web, o [!DNL User-Agent] é enviada em cada solicitação, independentemente de ser obrigatória. As dicas do cliente, por outro lado, impõem um modelo em que o servidor deve solicitar ao navegador as informações adicionais que ele deseja saber sobre o cliente. Ao receber essa solicitação, o navegador pode aplicar suas próprias políticas ou configurações do usuário para determinar quais dados são retornados. Em vez de expor o todo [!DNL User-Agent] por padrão, em todas as solicitações, o acesso agora é gerenciado de forma explícita e auditável.

## Suporte ao navegador {#browser-support}

[Dicas do cliente do agente do usuário](https://developer.chrome.com/docs/privacy-sandbox/user-agent/) foram introduzidas com [!DNL Google Chrome ]versão 89.

Navegadores adicionais baseados em Chromium oferecem suporte à API de dicas do cliente, como:

* [!DNL Microsoft Edge]
* [!DNL Opera]
* [!DNL Brave]
* [!DNL Chrome for Android]
* [!DNL Opera for Android]
* [!DNL Samsung Internet]

## Categorias {#categories}

Existem duas categorias de Dicas de Cliente do Agente de Usuário:

* [Dicas de cliente de baixa entropia](#low-entropy)
* [Dicas do cliente de alta entropia](#high-entropy)

### Dicas de cliente de baixa entropia {#low-entropy}

As dicas do cliente de baixa entropia incluem informações básicas que não podem ser usadas para usuários de impressão digital. Informações como marca do navegador, plataforma e se a solicitação vem de um dispositivo móvel.

Dicas de cliente de baixa entropia são ativadas por padrão no SDK da Web e são passadas em cada solicitação.

| Cabeçalho HTTP | JavaScript | Incluído no User-Agent por padrão | Incluído em dicas do cliente por padrão |
|---|---|---|---|
| `Sec-CH-UA` | `brands` | Sim | Sim |
| `Sec-CH-UA-Platform` | `platform` | Sim | Sim |
| `Sec-CH-UA-Mobile` | `mobile` | Sim | Sim |

### Dicas do cliente de alta entropia {#high-entropy}

Dicas de cliente de alta entropia são informações mais detalhadas sobre o dispositivo cliente, como versão da plataforma, arquitetura, modelo, bits (plataformas de 64 bits ou 32 bits) ou versão completa do sistema operacional. Essas informações poderiam ser usadas na impressão digital.

| Cabeçalho HTTP | JavaScript | Incluído no User-Agent por padrão | Incluído em Dicas do cliente por padrão |
|---|---|---|---|
| `Sec-CH-UA-Platform-Version` | `platformVersion` | Sim | Não |
| `Sec-CH-UA-Arc` | `architecture` | Sim | Não |
| `Sec-CH-UA-Model` | `model` | Sim | Não |
| `Sec-CH-UA-Bitness` | `Bitness` | Sim | Não |
| `Sec-CH-UA-Full-Version-List` | `fullVersionList` | Sim | Não |

Dicas de cliente de alta entropia são desativadas por padrão no SDK da Web. Para habilitá-los, você deve configurar manualmente o SDK da Web para solicitar dicas de cliente de alta entropia.

## Dicas de cliente de alta entropia afetam as soluções de Experience Cloud {#impact-in-experience-cloud-solutions}

Algumas soluções da Adobe Experience Cloud dependem das informações incluídas em dicas de cliente de alta entropia ao gerar relatórios.

Se você não ativar dicas de cliente de alta entropia em seu ambiente, os relatórios e características do Adobe Analytics e Audience Manager descritos abaixo não funcionarão.

### Relatórios do Adobe Analytics que dependem de dicas de cliente de alta entropia {#analytics}

O [Sistema operacional](https://experienceleague.adobe.com/docs/analytics/components/dimensions/operating-systems.html) A dimensão inclui a versão do sistema operacional que é armazenada como uma dica de cliente de alta entropia. Se as dicas de clientes de alta entropia não estiverem ativadas, a versão do sistema operacional pode ser imprecisa para ocorrências coletadas de navegadores Chromium.

### Audience Manager traços que dependem de dicas de cliente de alta entropia {#aam}

Se suas características do Audience Manager usarem qualquer uma das seguintes propriedades, você deverá ativar dicas de cliente de alta entropia. Caso contrário, as características deixarão de funcionar.

* Versão do sistema operacional
* Modelo do dispositivo
* Fabricante do dispositivo
* Fornecedor de dispositivo

## Ativar dicas de cliente de alta entropia {#enabling-high-entropy-client-hints}

Para ativar dicas de cliente de alta entropia na implantação do SDK da Web, você deve incluir o `highEntropyUserAgentHints` opção de contexto, conforme descrito na [documentação de configuração](configuring-the-sdk.md#context), juntamente com a configuração existente.

Por exemplo, para recuperar dicas de cliente de alta entropia das propriedades da Web, sua configuração seria semelhante a:

`context: ["highEntropyUserAgentHints", "web"]`

## Exemplo {#example}

As dicas do cliente contidas nos cabeçalhos da primeira solicitação feita pelo navegador para um servidor da Web conterão a marca do navegador, a versão principal do navegador e um indicador de se o cliente é um dispositivo móvel. Cada parte dos dados terá seu próprio valor de cabeçalho em vez de ser agrupada em um único [!DNL User-Agent] string, conforme mostrado abaixo:

```shell
Sec-CH-UA: "Chromium";v="101", "Google Chrome";v="101", " Not;A Brand";v="99"

Sec-CH-UA-Mobile: ?0

Sec-CH-UA-Platform: "macOS
```

O equivalente [!DNL User-Agent] para o mesmo navegador seria semelhante a:

```shell
Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/101.0.4951.54 Safari/537.36
```

Embora as informações sejam semelhantes, a primeira solicitação para o servidor contém dicas do cliente. Eles incluem apenas um subconjunto do que está disponível na variável [!DNL User-Agent] string. Falta a solicitação na arquitetura do sistema operacional, versão completa do sistema operacional, nome do mecanismo de layout, versão do mecanismo de layout e versão completa do navegador.

No entanto, em pedidos subsequentes, a variável [!DNL Client Hints API] O permite que servidores da web solicitem detalhes adicionais sobre o dispositivo. Quando esses valores são solicitados, dependendo da política do navegador ou das configurações do usuário, a resposta do navegador pode incluir essas informações.

Abaixo está um exemplo do objeto JSON retornado pela variável [!DNL Client Hints API] quando valores de alta entropia são solicitados:


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
