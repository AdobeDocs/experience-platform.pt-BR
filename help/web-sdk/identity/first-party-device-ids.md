---
title: IDs de dispositivo próprio no SDK da Web
description: Saiba como configurar IDs de dispositivo primário (FPIDs) no Adobe Experience Platform Web SDK.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: 1cb38e3eaa83f2ad0e7dffef185d5edaf5e6c38c
workflow-type: tm+mt
source-wordcount: '1904'
ht-degree: 0%

---


# IDs de dispositivo próprio no SDK da Web

O SDK da Web da Adobe Experience Platform atribui [Adobe Experience Cloud IDs (ECIDs)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=pt-BR) aos visitantes do site usando cookies para rastrear o comportamento do usuário. Para levar em conta as restrições do navegador nas vidas dos cookies, você pode optar por definir e gerenciar seus próprios identificadores de dispositivo. Elas são chamadas de IDs de dispositivos primários (`FPIDs`).

>[!NOTE]
>
>O suporte a ID de dispositivo próprio só está disponível ao enviar dados para o Edge Network do Experience Platform por meio do SDK da Web.

>[!IMPORTANT]
>
>As IDs de dispositivo próprio não são compatíveis com a funcionalidade de [cookies de terceiros](../../tags/extensions/client/web-sdk/web-sdk-extension-configuration.md#identity) no SDK da Web.
>Você pode usar IDs de dispositivo primário ou cookies de terceiros, mas não pode usar ambos os recursos simultaneamente.

Este documento explica como configurar IDs de dispositivo primário para a implementação do SDK da Web.

## Pré-requisitos

Este guia supõe que você esteja familiarizado com como os dados de identidade funcionam para o SDK da Web da Platform, incluindo a função das ECIDs e do `identityMap`. Consulte a visão geral sobre [dados de identidade no SDK da Web](./overview.md) para obter mais informações.

## Uso de IDs de dispositivo primário (FPIDs) {#using-fpid}

As IDs de dispositivo próprio ([!DNL FPIDs]) rastreiam visitantes usando cookies próprios. Os cookies próprios são mais eficazes quando definidos com um servidor que usa um [registro A](https://datatracker.ietf.org/doc/html/rfc1035) DNS (para IPv4) ou [registro AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (para IPv6), em vez de um código [!DNL CNAME] ou [!DNL JavaScript] DNS.

>[!IMPORTANT]
>
>Há suporte para [!DNL A] ou [!DNL AAAA] registros somente para configuração e rastreamento de cookies. O método principal para coleta de dados é por meio de um [!DNL DNS] [!DNL CNAME]. Em outras palavras, [!DNL FPIDs] são definidos usando um registro [!DNL A] ou [!DNL AAAA], e são enviados para o Adobe usando um [!DNL CNAME].
>
>O [Programa de Certificados Gerenciados por Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) ainda é suportado para a coleta de dados próprios.

Depois que um cookie [!DNL FPID] é definido, seu valor pode ser buscado e enviado para o Adobe conforme os dados do evento são coletados. Os [!DNL FPIDs] coletados são usados como seeds para gerar [!DNL ECIDs], que continuam a ser os identificadores primários nos aplicativos do Adobe Experience Cloud.

Para enviar um [!DNL FPID] para um visitante do site para o Edge Network, você deve incluir o [!DNL FPID] no `identityMap` para esse visitante. Consulte a seção mais abaixo neste documento sobre [uso de FPIDs em `identityMap`](#identityMap) para obter mais informações.

### Requisitos de formatação de ID de dispositivo próprio {#formatting-requirements}

O Edge Network só aceita [!DNL IDs] que estejam em conformidade com o [formato UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). As IDs de Dispositivo que não estão no formato [!DNL UUIDv4] serão rejeitadas.

A geração de um [!DNL UUID] quase sempre resultará em uma ID exclusiva e aleatória, com a probabilidade de ocorrer uma colisão sendo insignificante. [!DNL UUIDv4] não pode ser propagado usando endereços IP ou qualquer outra informação pessoal identificável ([!DNL PII]). [!DNL UUIDs] são universais e podem ser encontradas bibliotecas para praticamente todas as linguagens de programação para gerá-los.

## Configuração de um cookie de ID primário na interface dos fluxos de dados {#setting-cookie-datastreams}

Você pode especificar um nome de cookie na interface dos Datastreams, onde o [!DNL FPID] pode residir, em vez de ter que ler o valor do cookie e incluir o [!DNL FPID] no mapa de identidade.

>[!IMPORTANT]
>
>Este recurso exige que a [Coleção de dados próprios](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=en) esteja habilitada.

Consulte a [documentação de sequências de dados](../../datastreams/configure.md) para obter informações detalhadas sobre como configurar uma sequência de dados.

Ao configurar sua sequência de dados, habilite a opção **[!UICONTROL Cookie de ID primária]**. Esta configuração informa o Edge Network a fazer referência a um cookie especificado ao pesquisar uma ID de dispositivo primário, em vez de procurar esse valor no [mapa de identidade](#identityMap).

Consulte a documentação sobre [cookies próprios](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=pt-BR) para obter mais detalhes sobre como eles funcionam com a Adobe Experience Cloud.

![Imagem da interface do usuário da plataforma mostrando a configuração da sequência de dados destacando a configuração do Cookie de ID de Primeira Parte](../assets/first-party-id-datastreams.png)

Ao ativar essa configuração, você deve fornecer o nome do cookie no qual a ID deve ser armazenada.

Ao usar IDs primárias, não é possível executar sincronizações de ID de terceiros. As sincronizações de ID de terceiros dependem do serviço [!DNL Visitor ID] e do `UUID` gerado por esse serviço. Ao usar a funcionalidade de ID própria, o [!DNL ECID] é gerado sem o uso do serviço [!DNL Visitor ID], o que torna as sincronizações de ID de terceiros impossíveis.

Quando você usa IDs primárias, os recursos de [Audience Manager](https://experienceleague.adobe.com/en/docs/audience-manager) direcionados para ativação em plataformas de parceiros não são compatíveis, considerando que as sincronizações de ID de parceiro de Audience Manager se baseiam principalmente em `UUIDs` ou `DIDs`. O [!DNL ECID] derivado de uma ID própria não está vinculado a um `UUID`, tornando-o inendereçável.

## Configurar um cookie usando seu próprio servidor {#set-cookie-server}

Ao definir um cookie usando um servidor que você possui, é possível usar vários métodos para impedir que o cookie seja restrito devido a políticas do navegador:

* Gerar cookies usando linguagens de script do lado do servidor
* Definir cookies em resposta a uma solicitação de API feita a um subdomínio ou outro endpoint no site
* Gerar cookies usando um [!DNL CMS]
* Gerar cookies usando um [!DNL CDN]

>[!IMPORTANT]
>
>Os cookies definidos com o método `document.cookie` da JavaScript quase nunca serão protegidos das políticas de navegador que restringem a duração dos cookies.

### Quando definir o cookie {#when-to-set-cookie}

Idealmente, o cookie [!DNL FPID] deve ser definido antes de fazer qualquer solicitação para o Edge Network. No entanto, em cenários em que isso não é possível, um [!DNL ECID] ainda é gerado usando métodos existentes e atua como o identificador principal, desde que o cookie exista.

Supondo que [!DNL ECID] seja afetado por uma política de exclusão de navegador, mas [!DNL FPID] não, [!DNL FPID] se tornará o identificador principal na próxima visita e será usado para propagar [!DNL ECID] em cada visita subsequente.

### Definição da expiração do cookie {#set-expiration}

Definir a expiração de um cookie é algo que deve ser considerado cuidadosamente ao implementar a funcionalidade [!DNL FPID]. Ao decidir isso, você deve considerar os países ou regiões em que sua organização opera, juntamente com as leis e políticas em cada uma dessas regiões.

Como parte dessa decisão, você pode adotar uma política de configuração de cookies em toda a empresa ou uma que varie para os usuários em cada local onde você opera.

Independentemente da configuração escolhida para a expiração inicial de um cookie, você deve garantir que inclua uma lógica que estenda a expiração do cookie toda vez que ocorrer uma nova visita ao site.

## Impacto dos sinalizadores de cookies {#cookie-flag-impact}

Há vários sinalizadores de cookies que afetam como os cookies são tratados em navegadores diferentes:

* [&quot;HTTPOnly&quot;](#http-only)
* [&quot;Seguro&quot;](#secure)
* [&quot;SameSite&quot;](#same-site)

### `HTTPOnly` {#http-only}

Os cookies definidos com o sinalizador `HTTPOnly` não podem ser acessados com scripts do lado do cliente. Isso significa que, se você definir um sinalizador `HTTPOnly` ao definir o [!DNL FPID], deverá usar uma linguagem de script do lado do servidor para ler o valor do cookie para inclusão no `identityMap`.

Se você optar por fazer com que o Edge Network leia o valor do cookie [!DNL FPID], definir o sinalizador `HTTPOnly` garante que o valor não esteja acessível por nenhum script do lado do cliente, mas não terá nenhum impacto negativo na capacidade do Edge Network de ler o cookie.

>[!NOTE]
>
>O uso do sinalizador `HTTPOnly` não afeta as políticas de cookies que podem restringir a duração do cookie. No entanto, ainda é algo que você deve considerar ao definir e ler o valor de [!DNL FPID].

### `Secure` {#secure}

Os cookies definidos com o atributo `Secure` só são enviados ao servidor com uma solicitação criptografada através do protocolo [!DNL HTTPS]. O uso desse sinalizador pode ajudar a garantir que invasores intermediários não possam acessar facilmente o valor do cookie. Quando possível, é sempre uma boa ideia definir o sinalizador `Secure`.

### `SameSite` {#same-site}

O atributo `SameSite` permite que os servidores determinem se os cookies são enviados com solicitações entre sites. O atributo fornece alguma proteção contra ataques de falsificação entre sites. Existem três valores possíveis: `Strict`, `Lax` e `None`. Consulte sua equipe interna para determinar qual é a configuração certa para sua organização.

Se nenhum atributo `SameSite` for especificado, a configuração padrão para alguns navegadores agora será `SameSite=Lax`.

## Usando FPIDs em `identityMap` {#identityMap}

Veja abaixo um exemplo de como você definiria um [!DNL FPID] no `identityMap`:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
      }
    ]
  }
}
```

Assim como em outros tipos de identidade, você pode incluir [!DNL FPID] com outras identidades em `identityMap`. Este é um exemplo de [!DNL FPID] incluído com um [!DNL CRM ID] autenticado:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": false
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Se [!DNL FPID] estiver contido em um cookie que está sendo lido pelo Edge Network quando a coleta de dados próprios estiver habilitada, você deverá capturar apenas o [!DNL CRM ID] autenticado:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

O seguinte `identityMap` resultaria em uma resposta de erro do Edge Network, pois o indicador `primary` para o [!DNL FPID] está ausente. Pelo menos uma das IDs presentes em `identityMap` deve ser marcada como `primary`.

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-12d3-a456-426614174000",
        "authenticatedState": "ambiguous"
      }
    ],
    "EMAIL": [
      {
        "id": "email@mail.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

Nesse caso, a resposta do erro retornada pelo Edge Network seria semelhante ao seguinte:

```json
{
    "type": "https://ns.adobe.com/aep/errors/EXEG-0306-400",
    "status": 400,
    "title": "No primary identity set in request (event)",
    "detail": "No primary identity found in the input event. Update the request accordingly to your schema and try again.",
    "report": {
        "requestId": "{REQUEST_ID}",
        "configId": "{CONFIG_ID}",
        "orgId": "{ORG_ID}"
    }
}
```

## Hierarquia de ID {#id-hierarchy}

Quando um [!DNL ECID] e [!DNL FPID] estão presentes, o [!DNL ECID] é priorizado na identificação do usuário. Isso garante que, quando um [!DNL ECID] existente estiver presente no armazenamento de cookies do navegador, ele permanecerá o identificador principal e as contagens de visitantes existentes não correm o risco de serem afetadas. Para usuários existentes, o [!DNL FPID] não se tornará a identidade principal até que o [!DNL ECID] expire ou seja excluído como resultado de uma política de navegador ou processo manual.

As identidades são priorizadas na seguinte ordem:

1. [!DNL ECID] incluído no `identityMap`
1. [!DNL ECID] armazenado em um cookie
1. [!DNL FPID] incluído no `identityMap`
1. [!DNL FPID] armazenado em um cookie

## Migração para IDs de dispositivos primários {#migrating-to-fpid}

Se você estiver migrando de uma implementação anterior para IDs de dispositivo primário, pode ser difícil visualizar como a transição pode parecer em um nível baixo.

Para ajudar a ilustrar esse processo, considere um cenário que envolva um cliente que visitou seu site anteriormente e o impacto que uma migração do [!DNL FPID] teria em como esse cliente é identificado nas soluções Adobe.

![Diagrama que mostra como os valores de ID de um cliente são atualizados entre visitas após a migração para FPIDs](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>O cookie `ECID` é sempre priorizado em relação ao `FPID`.

| Visite a | Descrição |
| --- | --- |
| Primeira visita | Suponha que você ainda não começou a definir o cookie [!DNL FPID]. O [!DNL ECID] contido no [cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) será o identificador usado para identificar o visitante. |
| Segunda visita | A implantação da solução [!DNL FPID] foi iniciada. O [!DNL ECID] existente ainda está presente e permanece o identificador principal para identificação do visitante. |
| Terceira visita | Entre a segunda e a terceira visita, decorreu tempo suficiente para que [!DNL ECID] fosse excluído devido à política do navegador. No entanto, como o [!DNL FPID] foi definido usando um [!DNL DNS] [!DNL A] registro, o [!DNL FPID] persiste. O [!DNL FPID] agora é considerado a ID primária e usado para propagar o [!DNL ECID], que é gravado no dispositivo do usuário final. O usuário agora seria considerado um novo visitante nas soluções Adobe Experience Platform e Experience Cloud. |
| Quarta visita | Entre a terceira e a quarta visita, decorreu tempo suficiente para que [!DNL ECID] fosse excluído devido à política do navegador. Assim como na visita anterior, o [!DNL FPID] permanece devido à maneira como foi definido. Desta vez, o mesmo [!DNL ECID] é gerado como a visita anterior. O usuário é visto em todas as soluções de Experience Platform e Experience Cloud como o mesmo usuário da visita anterior. |
| Quinta visita | Entre a quarta e a quinta visita, o usuário final limpou todos os cookies em seu navegador. Um novo [!DNL FPID] é gerado e usado para propagar a criação de um novo [!DNL ECID]. O usuário agora seria considerado um novo visitante nas soluções Adobe Experience Platform e Experience Cloud. |

{style="table-layout:auto"}

## Perguntas frequentes {#faq}

Esta é uma lista de respostas para perguntas frequentes sobre IDs de dispositivos primários.

### Qual a diferença entre o seed de uma ID e a simples geração de uma ID?

O conceito de propagação é exclusivo, na medida em que o [!DNL FPID] transmitido ao Adobe Experience Cloud é convertido em um [!DNL ECID] usando um algoritmo determinístico. Sempre que o mesmo [!DNL FPID] for enviado para o Edge Network, o mesmo [!DNL ECID] será propagado do [!DNL FPID].

### Quando a ID de dispositivo primário deve ser gerada?

Para reduzir a inflação potencial de visitantes, o [!DNL FPID] deve ser gerado antes de fazer sua primeira solicitação usando o SDK da Web. No entanto, se você não conseguir fazer isso, um [!DNL ECID] ainda será gerado para esse usuário e será usado como o identificador principal. O [!DNL FPID] que foi gerado não se tornará o identificador principal até que o [!DNL ECID] não esteja mais presente.

### Quais métodos de coleta de dados oferecem suporte a IDs de dispositivos primários?

Atualmente, somente o SDK da Web oferece suporte a IDs de dispositivos primários.

### As IDs de dispositivo primárias são armazenadas em qualquer plataforma ou solução Experience Cloud?

Depois que o [!DNL FPID] tiver sido usado para propagar um [!DNL ECID], ele será descartado do `identityMap` e substituído pelo [!DNL ECID] que foi gerado. O [!DNL FPID] não está armazenado em nenhuma solução Adobe Experience Platform ou Experience Cloud.
