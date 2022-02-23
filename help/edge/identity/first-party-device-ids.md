---
title: IDs de dispositivo próprio no SDK da Web da plataforma
description: Saiba como configurar IDs de dispositivos primários (FPIDs) para o SDK da Web da Adobe Experience Platform.
source-git-commit: 7a3a89fe92d965a5f5796f7722d3bc2daf6ef178
workflow-type: tm+mt
source-wordcount: '1680'
ht-degree: 0%

---

# IDs de dispositivo próprio no SDK da Web da plataforma

O SDK da Web da Adobe Experience Platform atribui [Adobe Experience Cloud IDs (ECIDs)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=en) para visitantes do site por meio de cookies, para rastrear o comportamento do usuário. Para levar em conta as restrições do navegador sobre o tempo de vida do cookie, você pode optar por definir e gerenciar seus próprios identificadores de dispositivo. Elas são chamadas de IDs de dispositivo originais (FPIDs).

>[!NOTE]
>
>O suporte à ID de dispositivo próprio só está disponível ao enviar dados para a Rede de borda da plataforma por meio do SDK da Web da plataforma.

Este documento aborda como configurar IDs de dispositivos primários para a implementação do SDK da Web da plataforma.

## Pré-requisitos

Este guia pressupõe que você esteja familiarizado com o funcionamento dos dados de identidade para o SDK da Web da plataforma, incluindo a função das ECIDs e `identityMap`. Consulte a visão geral em [dados de identidade no SDK da Web](./overview.md) para obter mais informações.

## Uso de FPIDs

Os cookies próprios são mais eficazes quando são definidos usando um servidor de propriedade do cliente que aproveita um registro A de DNS em vez de um CNAME de DNS. Usando IDs de dispositivo primários, você pode definir suas próprias IDs de dispositivo em cookies usando registros A de DNS. Essas IDs podem ser enviadas para o Adobe e usadas como sementes para gerar ECIDs que continuarão a ser os identificadores primários em aplicativos Adobe Experience Cloud.

Para enviar um FPID para um visitante do site para a Rede de borda da plataforma, você deve incluir o FPID no `identityMap` para esse visitante. Consulte a seção mais adiante neste documento em [usando FPIDs em `identityMap`](#identityMap) para obter mais informações.

## Requisitos de formatação de ID

A Rede de borda da plataforma aceita somente IDs que estejam em conformidade com a [Formato UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). As IDs de dispositivo que não estão no formato UUIDv4 serão rejeitadas.

A geração de um UUID quase sempre resultará em uma ID exclusiva e aleatória, com a probabilidade de uma colisão ocorrer sendo negligenciável. O UUIDv4 não pode ser pré-implantado usando endereços IP ou qualquer outra informação pessoal identificável (PII). As UUIDs são ubíquas e as bibliotecas podem ser encontradas para praticamente todas as linguagens de programação para gerá-las.

## Configuração de um cookie usando um registro A de DNS

Vários métodos podem ser usados para definir um cookie de uma forma que evite sua restrição devido às políticas do navegador:

* Gerar cookies usando linguagens de script do lado do servidor
* Definir cookies em resposta a uma solicitação de API feita para um subdomínio ou outro terminal no site
* Gerar cookies usando um CMS
* Gerar cookies usando um CDN

>[!NOTE]
>
>Cookies definidos usando o `document.cookie` quase nunca será protegido de políticas de navegador que restrinjam a duração do cookie.

## Quando definir o cookie

O cookie FPID deve ser definido preferencialmente antes de fazer qualquer solicitação à Edge Network. No entanto, em cenários em que isso não é possível, uma ECID ainda é gerada usando métodos existentes e atua como o identificador principal, desde que o cookie exista.

Supondo que a ECID seja eventualmente afetada por uma política de exclusão do navegador, mas o FPID não é, o FPID se tornará o identificador principal na próxima visita e será usado para propagação da ECID em cada visita subsequente.

## Definir a expiração do cookie

Definir a expiração de um cookie é algo que deve ser cuidadosamente considerado ao implementar a funcionalidade FPID. Ao tomar essa decisão, você deve levar em conta os países ou regiões em que sua organização opera, juntamente com as leis e políticas em cada uma dessas regiões.

Como parte dessa decisão, você pode adotar uma política de configuração de cookies em toda a empresa ou uma que varia para os usuários em cada local em que você opera.

Independentemente da configuração escolhida para a expiração inicial de um cookie, você deve incluir uma lógica que estende a expiração do cookie sempre que uma nova visita ao site ocorrer.

## Impacto dos sinalizadores de cookies

Há vários sinalizadores de cookies que afetam como os cookies são tratados em navegadores diferentes:

* [`HTTPOnly`](#http-only)
* [`Seguro`](#secure)
* [`SameSite`](#same-site)

### `HTTPOnly` {#http-only}

Cookies definidos com o `HTTPOnly` o sinalizador não pode ser acessado usando scripts do lado do cliente. Isso significa que se você definir uma `HTTPOnly` sinalizador ao definir o FPID, você deve aproveitar uma linguagem de script do lado do servidor para ler o valor do cookie para inclusão no `identityMap`.

Se você optar por fazer com que a Rede de borda da plataforma leia o valor do cookie FPID, defina a variável `HTTPOnly` O sinalizador garantirá que o valor não seja acessível por nenhum script do lado do cliente, mas não terá impacto negativo na capacidade da Rede de borda da plataforma de ler o cookie.

>[!NOTE]
>
>Utilização do `HTTPOnly` O sinalizador não tem impacto nas políticas do cookie que podem restringir a duração do cookie. No entanto, ainda é algo que você deve considerar ao definir e ler o valor do FPID.

### `Secure` {#secure}

Os cookies definidos com a variável `Secure` só são enviados para o servidor com uma solicitação criptografada pelo protocolo HTTPS. Usar esse sinalizador pode ajudar a garantir que os atacantes intermediários não possam acessar facilmente o valor do cookie. Sempre que possível, é uma boa ideia definir a variável `Secure` sinalizador.

### `SameSite` {#same-site}

O `SameSite` permite que os servidores determinem se os cookies são enviados com solicitações entre sites. O atributo fornece alguma proteção contra ataques de falsificação entre sites. Existem três valores possíveis: `Strict`, `Lax` e `None`. Consulte sua equipe interna para determinar qual configuração é a correta para sua organização.

Se não `SameSite` for especificado, a configuração padrão para alguns navegadores agora será `SameSite=Lax`.

## Uso de FPIDs em `identityMap` {#identityMap}

Abaixo está um exemplo de como você definiria um FPID por conta própria na variável `identityMap`:

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

Se o FPID estiver contido em um cookie que está sendo lido pela Rede de Borda quando a coleta de dados primários estiver ativada, você deve capturar somente a ID de CRM autenticada:

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

O seguinte `identityMap` resultaria em uma resposta de erro da rede de borda, pois falta a variável `primary` para o FPID. Pelo menos uma das IDs presentes em `identityMap` deve ser marcada como `primary`.

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

A resposta do erro retornada pelo Experience Edge nesse caso seria semelhante ao seguinte:

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

Quando uma ECID e FPID estiverem presentes, a ECID será priorizada na identificação do usuário. Isso garantirá que, quando uma ECID existente estiver presente no armazenamento de cookies do navegador, ela continuará sendo o identificador principal e as contagens de visitantes existentes não arriscam ser afetadas. Para usuários existentes, o FPID não se tornará a identidade primária até que o ECID expire ou seja excluído como resultado de uma política de navegador ou de um processo manual.

As identidades são priorizadas na seguinte ordem:

1. ECID incluída no `identityMap`
1. ECID armazenada em um cookie
1. FPID incluído no `identityMap`
1. FPID armazenado em um cookie

## Migração para IDs de dispositivos primários

Se você estiver migrando para FPIDs de uma implementação anterior, pode ser difícil visualizar como a transição pode ser em um nível baixo.

Para ajudar a ilustrar esse processo, considere um cenário que envolva um cliente que já visitou seu site anteriormente e o impacto que uma migração de FPID teria na forma como esse cliente é identificado nas soluções do Adobe.

![Diagrama que mostra como os valores de ID de um cliente são atualizados entre visitas após migrar para FPIDs](../images/identity/tracking/visits.png)

| Visita | Descrição |
| --- | --- |
| Primeira visita | Suponha que você ainda não tenha iniciado a configuração do cookie FPID. A ECID contida no [cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html#section-c55af54828dc4cce89f6118655d694c8) será o identificador usado para identificar o visitante. |
| Segunda visita | A implantação da solução ID de dispositivo próprio foi iniciada. A ECID existente ainda está presente e continua a ser o identificador principal para a identificação do visitante. |
| Terceira visita | Entre a segunda e a terceira visita, decorreu um tempo suficiente para a ECID ter sido excluída devido à política do navegador. No entanto, como o FPID foi definido usando um registro A de DNS, o FPID persiste. O FPID agora é considerado a ID primária e é usado para propagação da ECID, que é gravada no dispositivo do usuário final. O usuário agora seria considerado um novo visitante nas soluções Adobe Experience Platform e Experience Cloud. |
| Quarta visita | Entre a terceira e a quarta visitas, um tempo suficiente decorrido para a ECID ser excluída devido à política do navegador. Como a visita anterior, o FPID permanece devido à maneira como foi definido. Desta vez, o mesmo ECID é gerado como a visita anterior. O usuário é visto em todas as soluções Experience Platform e Experience Cloud como o mesmo usuário da visita anterior. |
| Quinta visita | Entre a quarta e a quinta visita, o usuário final limpou todos os cookies em seu navegador. Um novo FPID é gerado e usado para propagar a criação de um novo ECID. O usuário agora seria considerado um novo visitante nas soluções Adobe Experience Platform e Experience Cloud. |

{style=&quot;table-layout:auto&quot;}

## Perguntas frequentes

Veja a seguir uma lista de respostas para perguntas frequentes sobre IDs de dispositivos primários.

### Como a propagação de uma ID é diferente da simples geração de uma ID?

O conceito de propagação é exclusivo, na medida em que o FPID passado para a Adobe Experience Cloud é convertido em um ECID usando um algoritmo determinístico. Cada vez que o mesmo FPID é enviado para a Rede de borda da Adobe Experience Platform, o mesmo ECID é pré-implantado no FPID.

### Quando a ID de dispositivo primária deve ser gerada?

Para reduzir a inflação potencial de visitante, o FPID deve ser gerado antes de fazer sua primeira solicitação usando o SDK da Web da plataforma. No entanto, se você não conseguir fazer isso, uma ECID ainda será gerada para esse usuário e será usada como o identificador principal. O FPID gerado não se tornará o identificador principal até que o ECID não esteja mais presente.

### Quais métodos de coleta de dados oferecem suporte às IDs de dispositivo originais?

Atualmente, somente o SDK da Web da plataforma é compatível com FPIDs.

### Os FPIDs são armazenados em qualquer plataforma ou solução Experience Cloud?

Depois que o FPID for usado para propagação de uma ECID, ela será removida do `identityMap` e substituída pela ECID gerada. O FPID não é armazenado em nenhuma solução Adobe Experience Platform ou Experience Cloud.
