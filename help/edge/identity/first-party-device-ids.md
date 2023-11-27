---
title: IDs de dispositivo próprio no SDK da Web da plataforma
description: Saiba como configurar IDs de dispositivo primário (FPIDs) para o Adobe Experience Platform Web SDK.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: ffcd428f84a4dcbbc95560cb4da5fd1c6d858a28
workflow-type: tm+mt
source-wordcount: '1779'
ht-degree: 2%

---

# IDs de dispositivo próprio no SDK da Web da plataforma

O SDK da Web da Adobe Experience Platform atribui [Adobe Experience Cloud IDs (ECIDs)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=pt-BR) aos visitantes do site por meio do uso de cookies, para rastrear o comportamento do usuário. Para levar em conta as restrições do navegador nas vidas do cookie, você pode optar por definir e gerenciar seus próprios identificadores de dispositivo. Elas são chamadas de IDs de dispositivo próprios (FPIDs).

>[!NOTE]
>
>O suporte à ID de dispositivo próprio só está disponível ao enviar dados para a Rede de borda da Platform por meio do SDK da Web da Platform.

Este documento aborda como configurar IDs de dispositivo primário para a implementação do SDK da Web da Platform.

## Pré-requisitos

Este guia supõe que você esteja familiarizado com como os dados de identidade funcionam para o SDK da Web da plataforma, incluindo a função das ECIDs e `identityMap`. Consulte a visão geral em [dados de identidade no SDK da Web](./overview.md) para obter mais informações.

## Uso de FPIDs

Os FPIDs rastreiam visitantes com o uso de cookies primários. Os cookies primários são mais eficazes quando definidos com um servidor que utiliza um DNS [Registro A](https://datatracker.ietf.org/doc/html/rfc1035) (para IPv4) ou [Registro AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (para IPv6), ao contrário de um CNAME DNS ou código JavaScript.

>[!IMPORTANT]
>
>Os registros A ou AAAA só têm suporte para a configuração e o rastreamento de cookies. O método principal de coleta de dados é por meio de um CNAME DNS. Em outras palavras, os FPIDs são definidos usando um registro A ou AAAA e são enviados para o Adobe usando um CNAME.
>
>A variável [Programa de certificado gerenciado pelo Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html#adobe-managed-certificate-program) O também é compatível com a coleta de dados primários.

Depois que um cookie FPID é definido, seu valor pode ser buscado e enviado para o Adobe conforme os dados do evento são coletados. Os FPIDs coletados são usados como seeds para gerar ECIDs, que continuam a ser os identificadores principais nos aplicativos do Adobe Experience Cloud.

Para enviar um FPID para um visitante do site para a Rede de borda da Platform, você deve incluir o FPID no `identityMap` para esse visitante. Consulte a seção mais adiante neste documento em [uso de FPIDs no `identityMap`](#identityMap) para obter mais informações.

### Requisitos de formatação de ID

A Platform Edge Network aceita somente IDs que estejam em conformidade com a [Formato UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). As IDs de dispositivo que não estão no formato UUIDv4 serão rejeitadas.

A geração de uma UUID quase sempre resultará em uma ID exclusiva e aleatória, com a probabilidade de ocorrência de uma colisão sendo negligenciável. UUIDv4 não pode ser propagado usando endereços IP ou quaisquer outras informações pessoais identificáveis (PII). Os UUIDs são universais e as bibliotecas podem ser encontradas para praticamente todas as linguagens de programação gerá-los.

## Configurar um cookie usando seu próprio servidor

Ao definir um cookie usando um servidor que você possui, vários métodos podem ser usados para impedir que o cookie seja restrito devido a políticas do navegador:

* Gerar cookies usando linguagens de script do lado do servidor
* Definir cookies em resposta a uma solicitação de API feita a um subdomínio ou outro endpoint no site
* Gerar cookies usando um CMS
* Gerar cookies usando um CDN

>[!IMPORTANT]
>
>Cookies definidos usando JavaScript `document.cookie` O método quase nunca será protegido de políticas do navegador que restrinjam a duração de cookies.

### Quando definir o cookie

Idealmente, o cookie FPID deve ser definido antes de fazer qualquer solicitação para a Rede de borda. No entanto, em cenários em que isso não é possível, uma ECID ainda é gerada usando métodos existentes e atua como o identificador principal, desde que o cookie exista.

Supondo que a ECID seja afetada por uma política de exclusão do navegador, mas o FPID não, o FPID se tornará o identificador principal na próxima visita e será usado para propagar a ECID em cada visita subsequente.

### Definição da expiração do cookie

Definir a expiração de um cookie é algo que deve ser cuidadosamente considerado ao implementar a funcionalidade FPID. Ao tomar essa decisão, você deve levar em conta os países ou regiões em que sua organização opera, juntamente com as leis e políticas em cada uma dessas regiões.

Como parte dessa decisão, você pode adotar uma política de configuração de cookie em toda a empresa ou uma que varie para os usuários em cada local onde você opera.

Independentemente da configuração escolhida para a expiração inicial de um cookie, você deve garantir que inclua uma lógica que estenda a expiração do cookie toda vez que ocorrer uma nova visita ao site.

## Impacto dos sinalizadores de cookies

Há uma variedade de sinalizadores de cookies que afetam como os cookies são tratados em navegadores diferentes:

* [&quot;HTTPOnly&quot;](#http-only)
* [`Seguro`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Cookies definidos usando o `HTTPOnly` o sinalizador não pode ser acessado usando scripts do lado do cliente. Isso significa que se você definir um `HTTPOnly` ao definir o FPID, você deve utilizar uma linguagem de script do lado do servidor para ler o valor do cookie para inclusão no `identityMap`.

Se você optar que a Platform Edge Network leia o valor do cookie FPID, definindo o `HTTPOnly` O sinalizador garantirá que o valor não esteja acessível por nenhum script do lado do cliente, mas não terá nenhum impacto negativo na capacidade da Rede de borda da plataforma de ler o cookie.

>[!NOTE]
>
>Utilização do `HTTPOnly` O sinalizador não afeta as políticas de cookies que podem restringir a duração do cookie. No entanto, ainda é algo que você deve considerar ao definir e ler o valor do FPID.

### `Secure` {#secure}

Cookies definidos com o `Secure` Os atributos são enviados somente ao servidor com uma solicitação criptografada pelo protocolo HTTPS. O uso desse sinalizador pode ajudar a garantir que invasores intermediários não possam acessar facilmente o valor do cookie. Quando possível, é sempre uma boa ideia definir a `Secure` sinalizador.

### `SameSite` {#same-site}

A variável `SameSite` O atributo permite que os servidores determinem se os cookies são enviados com solicitações entre sites. O atributo fornece alguma proteção contra ataques de falsificação entre sites. Existem três valores possíveis: `Strict`, `Lax` e `None`. Consulte sua equipe interna para determinar qual é a configuração certa para sua organização.

Se não `SameSite` for especificado, a configuração padrão para alguns navegadores será `SameSite=Lax`.

## Uso de FPIDs no `identityMap` {#identityMap}

Veja abaixo um exemplo de como você definiria um FPID por conta própria na variável `identityMap`:

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

Assim como em outros tipos de identidade, você pode incluir o FPID com outras identidades no `identityMap`. Este é um exemplo do FPID incluído com uma ID de CRM autenticada:

```json
{
  "identityMap": {
    "FPID": [
      {
        "id": "123e4567-e89b-42d3-9456-426614174000",
        "authenticatedState": "ambiguous",
        "primary": true
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

Se o FPID estiver contido em um cookie que está sendo lido pela Rede de borda quando a coleta de dados primários estiver ativada, você deverá capturar somente a ID do CRM autenticada:

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

As seguintes `identityMap` resultaria em uma resposta de erro da Rede de borda, pois a variável `primary` indicador do FPID. Pelo menos uma das IDs presentes no `identityMap` deve ser marcado como `primary`.

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

A resposta de erro retornada pela Rede de borda nesse caso seria semelhante ao seguinte:

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

## Hierarquia de ID

Quando uma ECID e um FPID estiverem presentes, a ECID será priorizada na identificação do usuário. Isso garantirá que, quando uma ECID existente estiver presente no armazenamento de cookies do navegador, ela continuará sendo o identificador principal e as contagens de visitantes existentes não correm o risco de ser afetadas. Para usuários existentes, o FPID não se tornará a identidade principal até que a ECID expire ou seja excluída como resultado de uma política de navegador ou processo manual.

As identidades são priorizadas na seguinte ordem:

1. ECID incluída na `identityMap`
1. ECID armazenada em um cookie
1. FPID incluído no `identityMap`
1. FPID armazenado em um cookie

## Migração para IDs de dispositivos primários

Se você estiver migrando para o uso de FPIDs de uma implementação anterior, pode ser difícil visualizar como a transição pode ser em um nível baixo.

Para ajudar a ilustrar esse processo, considere um cenário que envolva um cliente que visitou seu site anteriormente e qual impacto uma migração de FPID teria em como esse cliente é identificado nas soluções Adobe.

![Diagrama que mostra como os valores de ID de um cliente são atualizados entre visitas após a migração para FPIDs](../assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>A variável `ECID` o cookie é sempre priorizado em relação ao `FPID`.

| Visita | Descrição |
| --- | --- |
| Primeira visita | Suponha que você ainda não tenha começado a definir o cookie FPID. A ECID contida no [cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) será o identificador usado para identificar o visitante. |
| Segunda visita | A implantação da solução de ID de dispositivo próprio foi iniciada. A ECID existente ainda está presente e continua sendo o identificador principal para identificação de visitantes. |
| Terceira visita | Entre a segunda e a terceira visita, decorreu um período de tempo suficiente para que a ECID fosse excluída devido à política do navegador. No entanto, como o FPID foi definido usando um registro DNS A, o FPID persiste. O FPID agora é considerado a ID primária e usado para propagar a ECID, que é gravada no dispositivo do usuário final. O usuário agora seria considerado um novo visitante nas soluções Adobe Experience Platform e Experience Cloud. |
| Quarta visita | Entre a terceira e a quarta visitas, decorreu um período de tempo suficiente para que a ECID fosse excluída devido à política do navegador. Assim como na visita anterior, o FPID permanece devido à maneira como foi definido. Desta vez, a mesma ECID é gerada como a visita anterior. O usuário é visto em todas as soluções de Experience Platform e Experience Cloud como o mesmo usuário da visita anterior. |
| Quinta visita | Entre a quarta e a quinta visitas, o usuário final limpou todos os cookies em seu navegador. Um novo FPID é gerado e usado para propagar a criação de uma nova ECID. O usuário agora seria considerado um novo visitante nas soluções Adobe Experience Platform e Experience Cloud. |

{style="table-layout:auto"}

## Perguntas frequentes

Esta é uma lista de respostas para perguntas frequentes sobre IDs de dispositivos primários.

### Qual a diferença entre o seed de uma ID e a simples geração de uma ID?

O conceito de seed é exclusivo, pois o FPID transmitido ao Adobe Experience Cloud é convertido em uma ECID usando um algoritmo determinístico. Sempre que o mesmo FPID for enviado para a Rede de borda da Adobe Experience Platform, a mesma ECID será propagada do FPID.

### Quando a ID de dispositivo primário deve ser gerada?

Para reduzir a inflação potencial de visitantes, o FPID deve ser gerado antes de fazer sua primeira solicitação usando o SDK da Web da plataforma. No entanto, se você não conseguir fazer isso, uma ECID ainda será gerada para esse usuário e usada como o identificador principal. O FPID gerado não se tornará o identificador principal até que a ECID não esteja mais presente.

### Quais métodos de coleta de dados oferecem suporte a IDs de dispositivos primários?

Atualmente, somente o SDK da Web da Platform é compatível com FPIDs.

### Os FPIDs são armazenados em alguma plataforma ou solução de Experience Cloud?

Depois que o FPID for usado para propagar uma ECID, ele será descartado do `identityMap` e substituído pela ECID que foi gerada. O FPID não está armazenado em nenhuma solução Adobe Experience Platform ou Experience Cloud.
