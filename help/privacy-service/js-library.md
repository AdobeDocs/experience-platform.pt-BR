---
keywords: Experience Platform;página inicial;tópicos populares
solution: Experience Platform
title: Visão geral da biblioteca JavaScript de privacidade do Adobe
description: A Biblioteca JavaScript de privacidade de Adobe permite recuperar identidades de titulares de dados para uso no Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: fcd44aef026c1049ccdfe5896e6199d32b4d1114
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 6%

---

# Visão geral da biblioteca JavaScript de privacidade do Adobe

Como processador de dados, a Adobe processa dados pessoais de acordo com a permissão e as instruções de sua empresa. Como o controlador de dados, você determinará os dados pessoais que a Adobe processa e armazena em seu nome. Dependendo das informações que você escolher enviar pelas soluções da Adobe Experience Cloud, o Adobe pode armazenar informações privadas aplicáveis a regulamentos de privacidade, como o [!DNL General Data Protection Regulation] (GDPR) e [!DNL California Consumer Privacy Act] (CCPA). Consulte o documento sobre [privacidade no Adobe Experience Cloud](https://www.adobe.com/br/privacy/marketing-cloud.html) para obter mais informações sobre como as soluções Experience Cloud coletam dados privados.

A variável **Biblioteca JavaScript de Privacidade Adobe** permite que os controladores de dados automatizem a recuperação de todas as identidades de titulares de dados geradas pelo [!DNL Experience Cloud] para um domínio específico. O uso da API fornecida por [Adobe Experience Platform Privacy Service](home.md), essas identidades podem ser usadas para criar, acessar e excluir solicitações de dados privados pertencentes a esses titulares de dados.

>[!NOTE]
>
>A variável [!DNL Privacy JS Library] normalmente, o só precisa ser instalado em páginas relacionadas à privacidade e o não precisa ser instalado em todas as páginas de um site ou domínio.

## Funções

A variável [!DNL Privacy JS Library] O fornece várias funções para gerenciar identidades no [!DNL Privacy Service]. Essas funções só podem ser usadas para gerenciar as identidades armazenadas no navegador para um visitante específico. Elas não podem ser usadas para enviar informações para o [!DNL Experience Cloud Central Service] diretamente.

A tabela a seguir descreve as diferentes funções fornecidas pela biblioteca:

| Função | Descrição |
| --- | --- |
| `retrieveIdentities` | Retorna uma matriz de identidades correspondentes (`validIds`) que foram recuperados de [!DNL Privacy Service], bem como uma série de identidades que não foram encontradas (`failedIds`). |
| `removeIdentities` | Remove cada identidade correspondente (válida) do navegador. Retorna uma matriz de identidades correspondentes (`validIds`), com cada identidade contendo um `isDeletedClientSide` booleano que indica se essa ID foi excluída. |
| `retrieveThenRemoveIdentities` | Recupera uma matriz de identidades correspondentes (`validIds`) e, em seguida, remove essas identidades do navegador. Embora essa função seja semelhante a `removeIdentities`, é melhor usá-lo quando a solução Adobe que você está usando exigir uma solicitação de acesso antes que a exclusão seja possível (como quando um identificador exclusivo deve ser recuperado antes de ser fornecido em uma solicitação de exclusão). |

>[!NOTE]
>
>`removeIdentities` e `retrieveThenRemoveIdentities` remova somente as identidades do navegador para soluções de Adobe específicas que as suportem. Por exemplo, o Adobe Audience Manager não exclui as IDs demdex armazenadas em cookies de terceiros, enquanto o Adobe Target exclui todos os cookies que armazenam suas IDs.

Como todas as três funções representam processos assíncronos, qualquer identidade recuperada deve ser tratada usando retornos de chamada ou promessas.


## Instalação

Para começar a usar o [!DNL Privacy JS Library], você deve instalá-lo em sua máquina usando um dos seguintes métodos:

* Instale usando o npm executando o seguinte comando: `npm install @adobe/adobe-privacy`
* Baixe do [Repositório GitHub do Experience Cloud](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

Também é possível instalar a biblioteca por meio de uma extensão de tag. Consulte a visão geral no [Extensão de tag de privacidade do Adobe](../tags/extensions/client/privacy/overview.md) para obter mais informações.

## Instanciar o [!DNL Privacy JS Library]

Todos os aplicativos que utilizam o [!DNL Privacy JS Library] deve instanciar um novo `AdobePrivacy` objeto, que deve ser configurado para uma solução de Adobe específica. Por exemplo, uma instanciação do Adobe Analytics seria semelhante ao seguinte:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{ORG_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Para obter uma lista completa dos parâmetros suportados para as diferentes soluções de Adobe, consulte a seção do apêndice sobre os parâmetros suportados [Parâmetros de configuração da solução Adobe](#adobe-solution-configuration-parameters).

## Amostras de código {#samples}

As amostras de código a seguir demonstram como usar o [!DNL Privacy JS Library] para vários cenários comuns, desde que você não esteja usando tags.

### Recuperar identidades

Este exemplo demonstra como recuperar uma lista de identidades de [!DNL Experience Cloud].

#### JavaScript

O código a seguir define uma função, `handleRetrievedIDs`, para ser usado como um retorno de chamada ou promessa para lidar com as identidades recuperadas pelo `retrieveIdentities`.

```javascript
function handleRetrievedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.retrieveIdentities(handleRetrievedIDs);

// If using promises:
adobePrivacy.retrieveIdentities().then(handleRetrievedIDs);
```

| Variable | Descrição |
| --- | --- |
| `validIds` | Um objeto JSON que contém todas as IDs recuperadas com sucesso. |
| `failedIDs` | Um objeto JSON que contém todas as IDs que não foram recuperadas do [!DNL Privacy Service], ou não pôde ser encontrado. |

#### Resultado

Se o código for executado com sucesso, `validIDs` é preenchida com uma lista de identidades recuperadas.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543"
},
{
    "company": "adobe",
    "namespace": "gsurfer_id",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao"
}
```

### Remover identidades

Este exemplo demonstra como remover uma lista de identidades do navegador.

#### JavaScript

O código a seguir define uma função, `handleRemovedIDs`, para ser usado como um retorno de chamada ou promessa para lidar com as identidades recuperadas pelo `removeIdentities` após serem removidos do navegador.

```javascript
function handleRemovedIDs(ids) {
    const validIDs = ids.validIDs;
    const failedIDs = ids.failedIDs;
}

// If using callbacks:
adobePrivacy.removeIdentities(handleRemovedIDs);

// If using promises:
adobePrivacy.removeIdentities().then(handleRemovedIDs)…
```

| Variable | Descrição |
| --- | --- |
| `validIds` | Um objeto JSON que contém todas as IDs recuperadas com sucesso. |
| `failedIDs` | Um objeto JSON que contém todas as IDs que não foram recuperadas do [!DNL Privacy Service], ou não pôde ser encontrado. |

#### Resultado

Se o código for executado com sucesso, `validIDs` é preenchida com uma lista de identidades recuperadas.

```json
{
    "company": "adobe",
    "namespace": "ECID",
    "namespaceId": 4,
    "type": "standard",
    "name": "Experience Cloud ID",
    "description": "This is the ID generated by the ID Service.",
    "value": "79352169365966186342525781172209986543",
    "isDeletedClientSide": false
},
{
    "company": "adobe",
    "namespace": "AMO",
    "namespaceId": 411,
    "type": "standard",
    "value": "WqmIJQAAB669Ciao",
    "isDeletedClientSide": true
}
```

## Próximas etapas

Ao ler este documento, você foi apresentado às funcionalidades principais do [!DNL Privacy JS Library]. Depois de usar a biblioteca para recuperar uma lista de identidades, você pode usar essas identidades para criar acesso aos dados e excluir solicitações para a [!DNL Privacy Service] API. Consulte a [Guia da API do Privacy Service](api/overview.md) para obter mais informações.

## Apêndice

Esta seção contém informações adicionais para usar o [!DNL Privacy JS Library].

### Parâmetros de configuração da solução Adobe {#config-params}

Veja a seguir uma lista dos parâmetros de configuração aceitos para as soluções de Adobe compatíveis, usadas quando [instanciar um objeto do Adobe Privacy](#instantiate-the-privacy-js-library).

**Todas as soluções**

| Parâmetro | Descrição |
| --- | --- |
| `key` | Uma ID exclusiva que identifica o usuário ou titular dos dados. Esta propriedade deve ser usada para fins de rastreamento interno e não é usada pelo Adobe. |

**Adobe Analytics**

| Parâmetro | Descrição |
| --- | --- |
| `cookieDomainPeriods` | O número de períodos em um domínio usado para rastreamento de cookies (o padrão é `2`, por exemplo, `.domain.com`). Não o defina aqui, a menos que especificado no seu Web beacon JavaScript. |
| `dataCenter` | O data center de coleta de dados do Adobe. Isso só deve ser incluído se estiver especificado no seu Web beacon do JavaScript. Os valores em potencial são: <ul><li>`d1`: data center de San Jose</li><li>`d2`: data center de Dallas</li></ul> |
| `reportSuite` | A ID do conjunto de relatórios conforme especificado no Web beacon do JavaScript (por exemplo, `s_code.js` ou `dtm`). |
| `trackingServer` | Um domínio de coleção de dados não SSL. Isso só deve ser incluído se estiver especificado no seu Web beacon do JavaScript. |
| `trackingServerSecure` | Um domínio de coleção de dados SSL. Isso só deve ser incluído se estiver especificado no seu Web beacon do JavaScript. |
| `visitorNamespace` | O namespace usado para agrupar visitantes. Isso só deve ser incluído se estiver especificado no seu Web beacon do JavaScript. |

**Adobe Audience Manager**

| Parâmetro | Descrição |
| --- | --- |
| `aamUUIDCookieName` | Nome do cookie primário que contém a ID de usuário exclusiva retornada do Adobe Audience Manager. |

**Serviço de identidade da Adobe Experience Cloud (ECID)**

| Parâmetro | Descrição |
| --- | --- |
| `imsOrgID` | Sua ID de organização. |

**Adobe Target**

| Parâmetro | Descrição |
| --- | --- |
| `clientCode` | Código do cliente que identifica um cliente no Adobe Target System. |
