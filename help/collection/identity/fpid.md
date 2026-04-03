---
title: Usar IDs de dispositivo primário na coleção de dados
description: Configure IDs de dispositivo primário (FPIDs) para obter a identidade durável em implementações da Web que enviam dados para a Edge Network.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1905'
ht-degree: 0%

---

# Usar IDs de dispositivo primário na coleção de dados

O Experience Platform Edge Network usa Experience Cloud IDs (ECIDs) para identificar visitantes do site. Para melhorar a durabilidade da identidade em propriedades próprias, você pode definir e gerenciar seus próprios identificadores de dispositivo, conhecidos como IDs de dispositivo primário (FPIDs). O Edge Network usa o FPID para propagar a ECID que as soluções da Adobe usam.

Esta página supõe que você esteja familiarizado com ECIDs e `identityMap`. Consulte [Identidade na Coleção de Dados](./overview.md) para obter mais informações.

## Quando usar FPIDs {#when-to-use}

As restrições de navegador podem encurtar a vida útil dos cookies que o Adobe usa para reconhecer visitantes recorrentes. Se você precisar de identidade mais durável em sites que sua organização possui e controla, os FPIDs permitem gerenciar seu próprio identificador de dispositivo e usá-lo para propagar a ECID.

Os FPIDs são compatíveis com implementações da Web que usam o Web SDK, incluindo a extensão de tag da Web SDK. Eles são ideais quando o objetivo principal é uma persistência de identidade mais forte em domínios pertencentes a sua organização, ou quando você deseja uma continuidade melhor para relatórios e personalização em propriedades próprias da Web. Elas também permitem definir e gerenciar um cookie próprio da infraestrutura que você controla.

Os FPIDs não são a ferramenta correta quando seu objetivo principal é a entrega de aplicativo para Web ou a continuidade de identidade em vários domínios. Para estes cenários, consulte [compartilhamento de identidade móvel para Web](./mobile-to-web.md) e [compartilhamento entre domínios](./cross-domain-sharing.md).

Os benefícios do uso de FPIDs incluem:

* Maior persistência em propriedades próprias.
* Mais controle sobre como o identificador de dispositivo é gerado e gerenciado.
* Uma base durável para análise e personalização.

As compensações para o uso de FPIDs incluem:

* Mais responsabilidade de implementação do que depender do comportamento de identidade padrão.
* Coordenação entre a lógica de cookie do lado do servidor e a configuração da coleção de dados.
* A validação adicional para confirmar o identificador está sendo usada conforme esperado.

### Caminho de configuração de alto nível

1. Gerar e gerenciar uma ID de dispositivo primário na infraestrutura sob seu controle.
1. Configure sua implementação para ler essa ID em um [cookie próprio](#setting-cookie-datastreams) ou na [carga de identidade](#identityMap).
1. Valide se os visitantes recorrentes mantêm uma identidade consistente ao longo do tempo em suas propriedades.

## Como os FPIDs funcionam {#how-fpids-work}

O FPID transmitido ao Adobe Experience Cloud é convertido em uma ECID usando um algoritmo determinístico. Sempre que o mesmo FPID for enviado para o Edge Network, a mesma ECID será propagada do FPID. Depois que o FPID for usado para propagar uma ECID, ele será descartado de `identityMap` e substituído pela ECID gerada. O FPID não é armazenado nas soluções da Adobe Experience Platform ou da Experience Cloud.

Quando uma ECID e um FPID existem, a ECID é sempre usada para identificar o usuário primeiro. Essa priorização garante que, quando uma ECID existente estiver presente no armazenamento de cookies do navegador, ela permanecerá o identificador principal e as contagens de visitantes existentes não arriscarão a inflação. Para usuários existentes, o FPID não se torna a identidade principal até que o ECID expire ou seja excluído como resultado da política do navegador ou da ação manual.

As identidades são priorizadas na seguinte ordem:

1. ECID incluída no `identityMap`
1. ECID armazenada em um cookie
1. FPID incluído no `identityMap`
1. FPID armazenado em um cookie

## Gerar e definir o cookie FPID {#set-fpid-cookie}

O Edge Network só aceita IDs que estejam em conformidade com o [formato UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). As IDs de dispositivo que não estão no formato UUIDv4 foram rejeitadas.

* Os UUIDs são únicos e aleatórios, com uma probabilidade negligenciável de colisão.
* UUIDv4 não pode ser propagado usando endereços IP ou qualquer outra informação de identificação pessoal (PII).
* As bibliotecas para gerar UUIDs estão disponíveis para cada linguagem de programação.

### Configuração de cookie do lado do servidor {#set-cookie-server}

Ao definir um cookie por meio do seu próprio servidor, você pode usar vários métodos para ajudar a impedir que o cookie seja restrito pelas políticas do navegador:

* Gerar cookies usando linguagens de script do lado do servidor
* Definir cookies em resposta a uma solicitação de API feita a um subdomínio ou outro endpoint no site
* Gerar cookies usando um sistema de gerenciamento de conteúdo (CMS)
* Gerar cookies usando uma rede de entrega de conteúdo (CDN)

Os cookies próprios são mais eficazes quando definidos com um servidor que usa um [registro A](https://datatracker.ietf.org/doc/html/rfc1035) DNS (para IPv4) ou [registro AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (para IPv6), em vez de um código DNS `CNAME` ou JavaScript.

>[!IMPORTANT]
>
>Os cookies definidos com o método `document.cookie` da JavaScript (incluindo o método de tag [`cookie.set()`](../tags/cookie.md)) quase nunca são protegidos das políticas de navegador que restringem a duração do cookie.

Observe que os registros `A` ou `AAAA` só têm suporte para configuração e rastreamento de cookies. O método principal de coleta de dados é por meio de um DNS `CNAME`. Os FPIDs são definidos com um registro `A` ou `AAAA` e enviados para a Adobe com um `CNAME`. O [Programa de Certificados Gerenciados pela Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=pt-BR#adobe-managed-certificate-program) permite configurar um `CNAME` para coleta de dados.

### Quando definir o cookie {#when-to-set-cookie}

Idealmente, o cookie FPID é definido antes de enviar dados para a Edge Network. Se sua implementação exigir consentimento antes de coletar dados, consulte [Consentimento com IDs de dispositivo primário](./consent.md#consent-with-fpids) para obter orientação sobre como coordenar o cookie FPID com seu fluxo de consentimento. A inflação de visitante é reduzida quando você garante que o FPID esteja disponível para propagar a ECID a partir da primeira solicitação. Em cenários nos quais isso não é possível, uma ECID ainda é gerada usando métodos existentes e atua como o identificador principal, desde que o cookie exista. O FPID gerado não se torna o identificador principal até que a ECID não esteja mais presente. Supondo que a ECID seja afetada por uma política de exclusão do navegador, mas o FPID não, o FPID se torna o identificador principal na próxima visita e é usado para propagar a ECID em cada visita subsequente.

### Definir a expiração {#set-expiration}

A Adobe recomenda considerar cuidadosamente a duração do cookie FPID. Considere a política de privacidade de sua organização juntamente com as leis e políticas dos países ou regiões em que sua organização opera. Dependendo da configuração de sua organização, você pode adotar uma política de configuração de cookies em toda a empresa ou uma que varia para os usuários em cada local onde você opera. Independentemente da expiração inicial do cookie, inclua uma lógica que estenda a expiração sempre que ocorrer uma nova visita ao site.

### Sinalizadores de cookie {#cookie-flags}

Há vários sinalizadores de cookies que afetam como os cookies são tratados em navegadores diferentes:

* **`HTTPOnly`**: os cookies definidos com o sinalizador `HTTPOnly` não podem ser acessados com scripts do lado do cliente. Isso significa que, se você definir um sinalizador `HTTPOnly` ao definir o FPID, deverá usar uma linguagem de script do lado do servidor para ler o valor do cookie para inclusão no `identityMap`. Se você optar por fazer com que o Edge Network leia o valor do cookie FPID, definir o sinalizador `HTTPOnly` garante que o valor não seja acessível por scripts do lado do cliente, mas não afete negativamente a capacidade do Edge Network de ler o cookie. O uso do sinalizador `HTTPOnly` não afeta as políticas de cookies que podem restringir a duração do cookie. No entanto, ainda é algo a ser considerado ao definir e ler o valor do FPID.
* **`Secure`**: os cookies definidos com o atributo `Secure` só são enviados ao servidor com uma solicitação criptografada através do protocolo HTTPS. O uso desse sinalizador pode ajudar a garantir que invasores intermediários não possam acessar facilmente o valor do cookie. Quando possível, é sempre uma boa ideia definir o sinalizador `Secure`.
* **`SameSite`**: o atributo `SameSite` permite que os servidores determinem se os cookies são enviados com solicitações entre sites. O atributo fornece alguma proteção contra ataques de falsificação entre sites. Existem três valores possíveis: `Strict`, `Lax` e `None`. Consulte sua equipe interna para determinar qual é a configuração certa para sua organização. Se nenhum atributo `SameSite` for especificado, a configuração padrão para alguns navegadores será `SameSite=Lax`.

## Enviar o FPID para o Edge Network {#send-fpid}

Você pode enviar FPIDs para a Edge Network de duas maneiras:

* **[Método 1](#setting-cookie-datastreams)**: configure um `CNAME` para suas chamadas do Web SDK e inclua o nome do cookie FPID na configuração da sequência de dados.
* **[Método 2](#identityMap)**: incluir o FPID no mapa de identidade.

### Método 1: configurar um `CNAME` e definir um cookie de ID próprio na sua sequência de dados {#setting-cookie-datastreams}

Para definir um cookie FPID de seu próprio domínio, você deve configurar seu próprio `CNAME` para suas chamadas do Web SDK e, em seguida, habilitar a funcionalidade de cookie de ID primária na configuração da sequência de dados. Um registro `CNAME` no DNS permite criar um alias de um nome de domínio para outro. Este alias pode ajudar a fazer com que serviços de terceiros apareçam como se fossem parte de seu próprio domínio, fazendo com que seus cookies pareçam cookies primários. Quando a coleta de dados próprios é habilitada usando um `CNAME`, todos os cookies do seu domínio são enviados em solicitações feitas ao ponto de extremidade de coleta de dados.

1. Trabalhe com a Adobe para criar um registro `CNAME` para uso da coleção de dados em sua organização. Consulte o [programa de certificados gerenciados pela Adobe](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/data-collection/adobe-managed-cert) para ver o processo completo.
1. Habilite a opção **[!UICONTROL First Party ID Cookie]** na sequência de dados. Essa configuração informa o Edge Network a consultar o cookie especificado ao pesquisar uma ID de dispositivo primário em vez de pesquisar o valor no mapa de identidade. Ao ativar essa configuração, você deve fornecer o nome do cookie no qual o FPID deve ser armazenado. Consulte [Criar e configurar datastreams](/help/datastreams/configure.md#advanced-options) para obter mais informações.

   ![Imagem da interface do usuário da plataforma mostrando a configuração da sequência de dados destacando a configuração do Cookie de ID de Primeira Parte](/help/collection/js/assets/first-party-id-datastreams.png)

### Método 2: usar FPIDs em `identityMap` {#identityMap}

Como alternativa ao armazenamento do FPID no seu próprio cookie, você pode enviar o FPID para a Edge Network por meio do mapa de identidade.

Veja abaixo um exemplo de como definir um FPID no `identityMap`:

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

Assim como em outros tipos de identidade, você pode incluir o FPID com outras identidades em `identityMap`. O exemplo a seguir inclui o FPID com uma ID do CRM autenticada:

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
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

Se o FPID estiver contido em um cookie que está sendo lido pela Edge Network quando a coleta de dados primários estiver ativada, capture somente a ID do CRM autenticada:

```json
{
  "identityMap": {
    "EMAIL": [
      {
        "id": "user@example.com",
        "authenticatedState": "authenticated",
        "primary": true
      }
    ]
  }
}
```

O seguinte `identityMap` resulta em uma resposta de erro do Edge Network porque o indicador `primary` para o FPID está ausente. Pelo menos uma das IDs presentes em `identityMap` deve ser marcada como `primary`.

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
        "id": "user@example.com",
        "authenticatedState": "authenticated"
      }
    ]
  }
}
```

## Migração para FPIDs {#migrating-to-fpid}

Se você estiver migrando de uma implementação anterior para IDs de dispositivo primário, pode ser difícil visualizar como a transição pode parecer em um nível baixo. Para ajudar a ilustrar esse processo, considere um cenário que envolva um cliente que visitou seu site anteriormente e qual impacto uma migração FPID teria em como esse cliente é identificado nas soluções da Adobe.

![Diagrama que mostra como os valores de ID de um cliente são atualizados entre visitas após a migração para FPIDs](/help/collection/js/assets/identity/tracking/visits.png)

| Visita | Descrição |
| --- | --- |
| Primeira visita | Suponha que você ainda não tenha começado a definir o cookie FPID. A ECID contida no [cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=pt-BR#section-c55af54828dc4cce89f6118655d694c8) é o identificador usado para identificar o visitante. |
| Segunda visita | A implantação da solução FPID foi iniciada. A ECID existente ainda está presente e permanece o identificador principal para a identificação do visitante. |
| Terceira visita | Entre a segunda e a terceira visita, decorreu tempo suficiente para que a ECID fosse excluída devido à política do navegador. No entanto, como o FPID foi definido usando um registro DNS `A`, o FPID persiste. O FPID agora é considerado a ID primária e é usado para propagar a ECID, que é gravada no dispositivo do usuário final. O usuário agora é considerado um novo visitante nas soluções Adobe Experience Platform e Experience Cloud. |
| Quarta visita | Entre a terceira e a quarta visita, decorreu tempo suficiente para que a ECID fosse excluída devido à política do navegador. Assim como na visita anterior, o FPID permanece devido à maneira como foi definido. Desta vez, a mesma ECID é gerada como a visita anterior. O usuário é visto em todas as soluções da Adobe Experience Platform e da Experience Cloud como o mesmo usuário da visita anterior. |
| Quinta visita | Entre a quarta e a quinta visita, o usuário final limpou todos os cookies do navegador. Um novo FPID é gerado e usado para propagar a criação de uma nova ECID. O usuário agora é considerado um novo visitante nas soluções Adobe Experience Platform e Experience Cloud. |
