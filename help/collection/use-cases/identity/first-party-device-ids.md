---
title: Usar IDs de dispositivo primário no Web SDK
description: Saiba como configurar IDs de dispositivo primário (FPIDs) no Adobe Experience Platform Web SDK.
exl-id: c3b17175-8a57-43c9-b8a0-b874fecca952
source-git-commit: bb90bbddf33bc4b0557026a0f34965ac37475c65
workflow-type: tm+mt
source-wordcount: '2173'
ht-degree: 0%

---

# Usar IDs de dispositivo primário no Web SDK

O Adobe Experience Platform Web SDK atribui [Adobe Experience Cloud IDs (ECIDs)](https://experienceleague.adobe.com/docs/experience-platform/identity/ecid.html?lang=pt-BR) aos visitantes do site usando cookies para rastrear o comportamento do usuário. Para resolver as restrições do navegador nas vidas do cookie, você pode definir e gerenciar seus próprios identificadores de dispositivo, conhecidos como IDs de dispositivo primário (FPIDs).

>[!NOTE]
>
>O suporte à ID de dispositivo próprio só está disponível ao enviar dados para o Experience Platform Edge Network por meio do Web SDK.

>[!IMPORTANT]
>
>As IDs de dispositivo próprio não são compatíveis com a funcionalidade de [cookies de terceiros](/help/tags/extensions/client/web-sdk/configure/identity.md) no Web SDK. Você pode usar IDs de dispositivo primário ou cookies de terceiros, mas não ambos simultaneamente.

## Pré-requisitos {#prerequisites}

Antes de começar, familiarize-se com o funcionamento dos dados de identidade no Web SDK, incluindo ECIDs e `identityMap`. Consulte a visão geral sobre [dados de identidade no Web SDK](id-overview.md) para obter mais informações.

## Requisitos de formatação de ID de dispositivo próprio {#formatting-requirements}

O Edge Network só aceita IDs que estejam em conformidade com o [formato UUIDv4](https://datatracker.ietf.org/doc/html/rfc4122). As IDs de dispositivo que não estão no formato UUIDv4 serão rejeitadas.

* [!DNL UUIDs] são únicos e aleatórios, com uma probabilidade negligenciável de colisão.
* [!DNL UUIDv4] não pode ser propagado usando endereços IP ou outras informações pessoais identificáveis (PII).
* Bibliotecas para gerar o [!DNL UUIDs] estão disponíveis para cada linguagem de programação.

## Definir o cookie [!DNL FPID] usando seu próprio servidor {#set-cookie-server}

Ao definir um cookie por meio do seu próprio servidor, você pode usar vários métodos para impedir que o cookie seja restrito devido a políticas do navegador:

* Gerar cookies usando linguagens de script do lado do servidor
* Definir cookies em resposta a uma solicitação de API feita a um subdomínio ou outro endpoint no site
* Gerar cookies usando um [!DNL CMS]
* Gerar cookies usando um [!DNL CDN]

Além disso, você sempre deve definir o cookie FPID no registro `A` do seu domínio.

>[!IMPORTANT]
>
>Os cookies definidos com o método `document.cookie` da JavaScript quase nunca serão protegidos das políticas de navegador que restringem a duração dos cookies.

### Quando definir o cookie {#when-to-set-cookie}

Idealmente, o cookie [!DNL FPID] deve ser definido antes de fazer qualquer solicitação para a Edge Network. No entanto, em cenários em que isso não é possível, um [!DNL ECID] ainda é gerado usando métodos existentes e atua como o identificador principal, desde que o cookie exista.

Supondo que [!DNL ECID] seja afetado por uma política de exclusão de navegador, mas [!DNL FPID] não, [!DNL FPID] se tornará o identificador principal na próxima visita e será usado para propagar [!DNL ECID] em cada visita subsequente.

### Definição da expiração do cookie {#set-expiration}

Definir a expiração de um cookie é algo que deve ser considerado cuidadosamente ao implementar a funcionalidade [!DNL FPID]. Ao decidir isso, você deve considerar os países ou regiões em que sua organização opera, juntamente com as leis e políticas em cada uma dessas regiões.

Como parte dessa decisão, você pode adotar uma política de configuração de cookies em toda a empresa ou uma que varie para os usuários em cada local onde você opera.

Independentemente da configuração escolhida para a expiração inicial de um cookie, você deve garantir que inclua uma lógica que estenda a expiração do cookie toda vez que ocorrer uma nova visita ao site.

## Impacto dos sinalizadores de cookies {#cookie-flag-impact}

Há vários sinalizadores de cookies que afetam como os cookies são tratados em navegadores diferentes:

* [&quot;HTTPOnly&quot;](#httponly)
* [&quot;Seguro&quot;](#secure)
* [&quot;SameSite&quot;](#samesite)

### `HTTPOnly`

Os cookies definidos com o sinalizador `HTTPOnly` não podem ser acessados com scripts do lado do cliente. Isso significa que, se você definir um sinalizador `HTTPOnly` ao definir o [!DNL FPID], deverá usar uma linguagem de script do lado do servidor para ler o valor do cookie para inclusão no `identityMap`.

Se você optar por fazer o Edge Network ler o valor do cookie [!DNL FPID], definir o sinalizador `HTTPOnly` garantirá que o valor não seja acessível por scripts do lado do cliente, mas não terá nenhum impacto negativo na capacidade do Edge Network de ler o cookie.

>[!NOTE]
>
>O uso do sinalizador `HTTPOnly` não afeta as políticas de cookies que podem restringir a duração do cookie. No entanto, ainda é algo que você deve considerar ao definir e ler o valor de [!DNL FPID].

### `Secure`

Os cookies definidos com o atributo `Secure` só são enviados ao servidor com uma solicitação criptografada através do protocolo [!DNL HTTPS]. O uso desse sinalizador pode ajudar a garantir que invasores intermediários não possam acessar facilmente o valor do cookie. Quando possível, é sempre uma boa ideia definir o sinalizador `Secure`.

### `SameSite`

O atributo `SameSite` permite que os servidores determinem se os cookies são enviados com solicitações entre sites. O atributo fornece alguma proteção contra ataques de falsificação entre sites. Existem três valores possíveis: `Strict`, `Lax` e `None`. Consulte sua equipe interna para determinar qual é a configuração certa para sua organização.

Se nenhum atributo `SameSite` for especificado, a configuração padrão para alguns navegadores agora será `SameSite=Lax`.

## Hierarquia de ID {#id-hierarchy}

Quando um [!DNL ECID] e [!DNL FPID] estão presentes, o [!DNL ECID] é priorizado na identificação do usuário. Isso garante que, quando um [!DNL ECID] existente estiver presente no armazenamento de cookies do navegador, ele permanecerá o identificador principal e as contagens de visitantes existentes não correm o risco de serem afetadas. Para usuários existentes, o [!DNL FPID] não se tornará a identidade principal até que o [!DNL ECID] expire ou seja excluído como resultado de uma política de navegador ou processo manual.

As identidades são priorizadas na seguinte ordem:

1. [!DNL ECID] incluído no `identityMap`
1. [!DNL ECID] armazenado em um cookie
1. [!DNL FPID] incluído no `identityMap`
1. [!DNL FPID] armazenado em um cookie

## Migração para IDs de dispositivos primários {#migrating-to-fpid}

Se você estiver migrando de uma implementação anterior para IDs de dispositivo primário, pode ser difícil visualizar como a transição pode parecer em um nível baixo.

Para ajudar a ilustrar esse processo, considere um cenário que envolva um cliente que visitou seu site anteriormente e o impacto que uma migração do [!DNL FPID] teria em como esse cliente é identificado nas soluções da Adobe.

![Diagrama que mostra como os valores de ID de um cliente são atualizados entre visitas após a migração para FPIDs](/help/collection/js/assets/identity/tracking/visits.png)

>[!IMPORTANT]
>
>O cookie `ECID` é sempre priorizado em relação ao `FPID`.

| Visita | Descrição |
| --- | --- |
| Primeira visita | Suponha que você ainda não começou a definir o cookie [!DNL FPID]. O [!DNL ECID] contido no [cookie AMCV](https://experienceleague.adobe.com/docs/id-service/using/intro/cookies.html?lang=pt-BR#section-c55af54828dc4cce89f6118655d694c8) será o identificador usado para identificar o visitante. |
| Segunda visita | A implantação da solução [!DNL FPID] foi iniciada. O [!DNL ECID] existente ainda está presente e permanece o identificador principal para identificação do visitante. |
| Terceira visita | Entre a segunda e a terceira visita, decorreu tempo suficiente para que [!DNL ECID] fosse excluído devido à política do navegador. No entanto, como o [!DNL FPID] foi definido usando um [!DNL DNS] [!DNL A] registro, o [!DNL FPID] persiste. O [!DNL FPID] agora é considerado a ID primária e usado para propagar o [!DNL ECID], que é gravado no dispositivo do usuário final. O usuário agora seria considerado um novo visitante nas soluções Adobe Experience Platform e Experience Cloud. |
| Quarta visita | Entre a terceira e a quarta visita, decorreu tempo suficiente para que [!DNL ECID] fosse excluído devido à política do navegador. Assim como na visita anterior, o [!DNL FPID] permanece devido à maneira como foi definido. Desta vez, o mesmo [!DNL ECID] é gerado como a visita anterior. O usuário é visto em todas as soluções da Experience Platform e da Experience Cloud como o mesmo usuário da visita anterior. |
| Quinta visita | Entre a quarta e a quinta visita, o usuário final limpou todos os cookies em seu navegador. Um novo [!DNL FPID] é gerado e usado para propagar a criação de um novo [!DNL ECID]. O usuário agora seria considerado um novo visitante nas soluções Adobe Experience Platform e Experience Cloud. |

{style="table-layout:auto"}

## Uso de IDs de dispositivo primário (FPIDs) {#using-fpid}

As IDs de dispositivo próprio ([!DNL FPIDs]) rastreiam visitantes usando cookies próprios. Os cookies próprios são mais eficazes quando definidos com um servidor que usa um [registro A](https://datatracker.ietf.org/doc/html/rfc1035) DNS (para IPv4) ou [registro AAAA](https://datatracker.ietf.org/doc/html/rfc3596) (para IPv6), em vez de um código [!DNL CNAME] ou [!DNL JavaScript] DNS.

>[!IMPORTANT]
>
>Há suporte para [!DNL A] ou [!DNL AAAA] registros somente para configuração e rastreamento de cookies. O método principal de coleta de dados é por meio de um [!DNL DNS CNAME]. [!DNL FPIDs] são definidos com um registro [!DNL A] ou [!DNL AAAA] e enviados ao Adobe com um [!DNL CNAME].
>
>O [Programa de Certificados Gerenciados pela Adobe](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=pt-BR#adobe-managed-certificate-program) também é compatível com a coleta de dados primária.

Depois que um cookie [!DNL FPID] é definido, seu valor pode ser buscado e enviado para a Adobe à medida que os dados do evento são coletados. Os [!DNL FPIDs] coletados são usados para gerar [!DNL ECIDs], que são os identificadores primários em aplicativos Adobe Experience Cloud.

Você pode usar [!DNL FPIDs] de duas maneiras:

* **[Método 1](#setting-cookie-datastreams)**: configure um [!DNL CNAME] para suas chamadas do Web SDK e inclua o nome do cookie [!DNL FPID] na configuração da sequência de dados.
* **[Método 2](#identityMap)**: incluir [!DNL FPID] no mapa de identidade. Consulte a seção mais abaixo neste documento sobre [uso de FPIDs em `identityMap`](#identityMap) para obter mais informações.

### Método 1: configurar um CNAME para suas chamadas do Web SDK e definir um cookie de ID primária na sua sequência de dados {#setting-cookie-datastreams}

Para definir um cookie [!DNL FPID] do seu próprio domínio, você precisa configurar seu próprio [!DNL CNAME] (Nome Canônico) para suas chamadas do Web SDK e habilitar a funcionalidade [!DNL First Party ID Cookie] na configuração da sequência de dados.

**Etapa 1. Configure um CNAME para seu domínio de implantação do Web SDK**

Um registro [!DNL CNAME] no DNS permite criar um alias de um nome de domínio para outro. Isso pode ajudar a fazer com que serviços de terceiros pareçam fazer parte do seu próprio domínio, fazendo com que seus cookies pareçam cookies primários.

**Exemplo**

Considere que você deseja implementar o Web SDK em seu site `example.com`. O Web SDK envia dados à Edge Network para o domínio `edge.adobedc.net`.

| Sem [!DNL CNAME] | Com [!DNL CNAME] |
|---------|----------|
| <ul><li>O site `example.com` usa o domínio `edge.adobedc.net` do Web SDK para enviar dados à Edge Network.</li><li>Os cookies definidos por `edge.adobedc.net` são considerados cookies de terceiros, pois não vêm do seu domínio `example.com`. Dependendo dos navegadores dos usuários, os cookies de terceiros podem estar bloqueados e seus dados não chegam à Edge Network.</li></ul> | <ul><li>Você cria um subdomínio onde implanta o Web SDK, como o `metrics.example.com`.</li><li>Você definiu um registro de [!DNL CNAME] em seu sistema DNS para que `metrics.example.com` aponte para `edge.adobedc.net`.</li><li>Quando seu site define cookies por meio do `metrics.example.com`, eles parecem vir do `example.com` (originais) em vez de `edge.adobedc.net` (de terceiros) para o navegador. Isso torna o cookie de ID primária menos provável de ser bloqueado, garantindo uma coleta de dados mais precisa.</li></ul> |

Quando a coleta de dados primários é habilitada usando um [!DNL CNAME], todos os cookies do seu domínio serão enviados em solicitações feitas ao ponto de extremidade da coleta de dados.

Para usar essa funcionalidade, você precisa definir o cookie [!DNL FPID] no nível superior do seu domínio, em vez de um subdomínio específico. Se você o definir em um subdomínio, o valor do cookie não será enviado para a Edge Network e a solução [!DNL FPID] não funcionará conforme o esperado.

>[!IMPORTANT]
>
>Este recurso exige que a [Coleção de dados próprios](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=pt-BR) esteja habilitada.

**Etapa 2. Habilitar a funcionalidade &#x200B;** [!UICONTROL First Party ID Cookie]&#x200B;**para sua sequência de dados**

Após configurar seu CNAME, você deve habilitar a opção **[!UICONTROL First Party ID Cookie]** para sua sequência de dados. Esta configuração informa ao Edge Network para fazer referência a um cookie especificado ao pesquisar uma ID de dispositivo primário, em vez de pesquisar esse valor no [mapa de identidade](#identityMap).

Consulte a [documentação de configuração da sequência de dados](/help/datastreams/configure.md#advanced-options) para saber como configurar a sequência de dados.

Consulte a documentação sobre [cookies próprios](https://experienceleague.adobe.com/docs/core-services/interface/administration/ec-cookies/cookies-first-party.html?lang=pt-BR) para obter mais detalhes sobre como eles funcionam com a Adobe Experience Cloud.

![Imagem da interface do usuário da plataforma mostrando a configuração da sequência de dados destacando a configuração do Cookie de ID de Primeira Parte](/help/collection/js/assets/first-party-id-datastreams.png)

Ao habilitar esta configuração, você deve fornecer o nome do cookie no qual se espera que o [!DNL FPID] seja armazenado.

>[!NOTE]
>
>Ao usar IDs primárias, não é possível executar sincronizações de ID de terceiros. As sincronizações de ID de terceiros dependem do serviço [!DNL Visitor ID] e do `UUID` gerado por esse serviço. Ao usar a funcionalidade de ID própria, o [!DNL ECID] é gerado sem o uso do serviço [!DNL Visitor ID], o que torna as sincronizações de ID de terceiros impossíveis.
><br> Quando você usa IDs primárias, os recursos do [Audience Manager](https://experienceleague.adobe.com/pt-br/docs/audience-manager) direcionados para ativação em plataformas de parceiros não são compatíveis, visto que as sincronizações de ID de parceiro da Audience Manager são baseadas principalmente no `UUIDs` ou `DIDs`. O [!DNL ECID] derivado de uma ID própria não está vinculado a um `UUID`, tornando-o inendereçável.

## Método 2: usar FPIDs em `identityMap` {#identityMap}

Como alternativa ao armazenamento de [!DNL FPID] em seu próprio cookie, você pode enviar o [!DNL FPID] para a Edge Network por meio do mapa de identidade.

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

Se [!DNL FPID] estiver contido em um cookie que está sendo lido pela Edge Network quando a coleta de dados próprios estiver habilitada, você deverá capturar apenas o [!DNL CRM ID] autenticado:

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

O seguinte `identityMap` resultaria em uma resposta de erro do Edge Network, pois o indicador `primary` para [!DNL FPID] está ausente. Pelo menos uma das IDs presentes em `identityMap` deve ser marcada como `primary`.

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

A resposta do erro retornada pela Edge Network nesse caso seria semelhante ao seguinte:

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

## Perguntas frequentes {#faq}

Esta é uma lista de respostas para perguntas frequentes sobre IDs de dispositivos primários.

### Qual a diferença entre o seed de uma ID e a simples geração de uma ID?

O conceito de propagação é exclusivo, na medida em que o [!DNL FPID] transmitido ao Adobe Experience Cloud é convertido em um [!DNL ECID] usando um algoritmo determinístico. Sempre que o mesmo [!DNL FPID] for enviado ao Edge Network, o mesmo [!DNL ECID] será propagado do [!DNL FPID].

### Quando a ID de dispositivo primário deve ser gerada?

Para reduzir a inflação potencial de visitantes, o [!DNL FPID] deve ser gerado antes de fazer sua primeira solicitação usando o Web SDK. No entanto, se você não conseguir fazer isso, um [!DNL ECID] ainda será gerado para esse usuário e será usado como o identificador principal. O [!DNL FPID] que foi gerado não se tornará o identificador principal até que o [!DNL ECID] não esteja mais presente.

### Quais métodos de coleta de dados oferecem suporte a IDs de dispositivos primários?

Atualmente, somente o Web SDK oferece suporte a IDs de dispositivos primários.

### As IDs de dispositivo primárias são armazenadas em qualquer plataforma ou solução da Experience Cloud?

Depois que o [!DNL FPID] tiver sido usado para propagar um [!DNL ECID], ele será descartado do `identityMap` e substituído pelo [!DNL ECID] que foi gerado. O [!DNL FPID] não está armazenado em nenhuma solução da Adobe Experience Platform ou da Experience Cloud.
