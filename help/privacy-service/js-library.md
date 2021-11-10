---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Visão geral da biblioteca JavaScript de privacidade do Adobe
topic-legacy: overview
description: A Biblioteca JavaScript de Privacidade do Adobe permite recuperar identidades de titular de dados para uso no Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: 7f3a0594147a8cea292263f60aa45dc5ebb8484e
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 6%

---

# Visão geral da biblioteca JavaScript de privacidade do Adobe

Como processador de dados, o Adobe processa dados pessoais de acordo com a permissão e as instruções de sua empresa. Como o controlador de dados, você determinará os dados pessoais que a Adobe processa e armazena em seu nome. Dependendo das informações que você escolher enviar por meio das soluções da Adobe Experience Cloud, o Adobe pode armazenar informações privadas aplicáveis às regulamentações de privacidade, como a [!DNL General Data Protection Regulation] (GDPR) e [!DNL California Consumer Privacy Act] (CCPA). Consulte o documento em [privacidade na Adobe Experience Cloud](https://www.adobe.com/br/privacy/marketing-cloud.html) para obter mais informações sobre como as soluções do Experience Cloud coletam dados privados.

O **Biblioteca JavaScript de privacidade do Adobe** permite que os controladores de dados automatizem a recuperação de todas as identidades do titular de dados geradas por [!DNL Experience Cloud] para um domínio específico. Uso da API fornecida por [Adobe Experience Platform Privacy Service](home.md), essas identidades podem ser usadas para criar solicitações de acesso e exclusão de dados privados pertencentes a esses titulares de dados.

>[!NOTE]
>
>O [!DNL Privacy JS Library] O geralmente só precisa ser instalado em páginas relacionadas à privacidade e não precisa ser instalado em todas as páginas de um site ou domínio.

## Funções

O [!DNL Privacy JS Library] O fornece várias funções para gerenciar identidades no [!DNL Privacy Service]. Essas funções só podem ser usadas para gerenciar as identidades que são armazenadas no navegador para um visitante específico. Eles não podem ser usados para enviar informações para a [!DNL Experience Cloud Central Service] diretamente.

A tabela a seguir descreve as diferentes funções fornecidas pela biblioteca:

| Função | Descrição |
| --- | --- |
| `retrieveIdentities` | Retorna uma matriz de identidades correspondentes (`validIds`) que foram recuperados de [!DNL Privacy Service], bem como uma matriz de identidades que não foram encontradas (`failedIds`). |
| `removeIdentities` | Remove cada identidade (válida) correspondente do navegador. Retorna uma matriz de identidades correspondentes (`validIds`), com cada identidade contendo um `isDeletedClientSide` booleano que indica se essa ID foi excluída. |
| `retrieveThenRemoveIdentities` | Recupera uma matriz de identidades correspondentes (`validIds`) e remove essas identidades do navegador. Embora essa função seja semelhante a `removeIdentities`, ele é melhor usado quando a solução Adobe que você está usando requer uma solicitação de acesso antes da exclusão ser possível (como quando um identificador exclusivo deve ser recuperado antes de fornecê-lo em uma solicitação de exclusão). |

>[!NOTE]
>
>`removeIdentities` e `retrieveThenRemoveIdentities` remover somente identidades do navegador para soluções específicas do Adobe que as suportam. Por exemplo, o Adobe Audience Manager não exclui as IDs demdex armazenadas em cookies de terceiros, enquanto o Adobe Target exclui todos os cookies que armazenam suas IDs.

Como todas as três funções representam processos assíncronos, quaisquer identidades recuperadas devem ser tratadas usando retornos de chamada ou promessas.


## Instalação

Para começar a usar o [!DNL Privacy JS Library], você deve instalá-lo em sua máquina usando um dos seguintes métodos:

* Instale usando npm executando o seguinte comando: `npm install @adobe/adobe-privacy`
* Faça o download do [Repositório GitHub do Experience Cloud](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

Você também pode instalar a biblioteca por meio de uma extensão de tag na interface do usuário da coleta de dados. Consulte a visão geral no [Extensão de tag do Adobe Privacy](../tags/extensions/web/privacy/overview.md) para obter mais informações.

## Instancie o [!DNL Privacy JS Library]

Todos os aplicativos que utilizam a variável [!DNL Privacy JS Library] deve instanciar um novo `AdobePrivacy` , que deve ser configurado para uma solução Adobe específica. Por exemplo, uma instanciação do Adobe Analytics seria semelhante ao seguinte:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Para obter uma lista completa dos parâmetros suportados para diferentes soluções de Adobe, consulte a seção de apêndice sobre os [Parâmetros de configuração da solução Adobe](#adobe-solution-configuration-parameters).

## Amostras de código {#samples}

As amostras de código a seguir demonstram como usar o [!DNL Privacy JS Library] para vários cenários comuns, desde que você não esteja usando tags.

### Recuperar identidades

Este exemplo demonstra como recuperar uma lista de identidades de [!DNL Experience Cloud].

#### JavaScript

O código a seguir define uma função, `handleRetrievedIDs`, a utilizar como um retorno de chamada ou promessa para tratar as identidades recuperadas por `retrieveIdentities`.

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
| `validIds` | Um objeto JSON contendo todas as IDs que foram recuperadas com êxito. |
| `failedIDs` | Um objeto JSON contendo todas as IDs que não foram recuperadas de [!DNL Privacy Service], ou não foi possível encontrá-lo. |

#### Resultado

Se o código for executado com êxito, `validIDs` é preenchida com uma lista de identidades recuperadas.

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

O código a seguir define uma função, `handleRemovedIDs`, a utilizar como um retorno de chamada ou promessa para tratar as identidades recuperadas por `removeIdentities` após terem sido removidos do navegador.

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

| Variável | Descrição |
| --- | --- |
| `validIds` | Um objeto JSON contendo todas as IDs que foram recuperadas com êxito. |
| `failedIDs` | Um objeto JSON contendo todas as IDs que não foram recuperadas de [!DNL Privacy Service], ou não foi possível encontrá-lo. |

#### Resultado

Se o código for executado com êxito, `validIDs` é preenchida com uma lista de identidades recuperadas.

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

Ao ler este documento, você foi introduzido nas funcionalidades principais do [!DNL Privacy JS Library]. Depois de usar a biblioteca para recuperar uma lista de identidades, você pode usar essas identidades para criar acesso aos dados e excluir solicitações para a [!DNL Privacy Service] API. Consulte a [Guia da API do Privacy Service](api/overview.md) para obter mais informações.

## Apêndice

Esta seção contém informações complementares sobre o uso da variável [!DNL Privacy JS Library].

### Parâmetros de configuração da solução Adobe {#config-params}

Veja a seguir uma lista dos parâmetros de configuração aceitos para soluções de Adobe compatíveis, usados quando [instanciamento de um objeto do AdobePrivacy](#instantiate-the-privacy-js-library).

**Todas as soluções**

| Parâmetro | Descrição |
| --- | --- |
| `key` | Uma ID exclusiva que identifica o usuário ou o titular dos dados. Essa propriedade deve ser usada para fins de rastreamento interno e não é usada pelo Adobe. |

**Adobe Analytics**

| Parâmetro | Descrição |
| --- | --- |
| `cookieDomainPeriods` | O número de períodos em um domínio usado para rastreamento de cookies (o padrão é `2`, por exemplo `.domain.com`). Não o defina aqui, a menos que especificado no beacon da Web do JavaScript. |
| `dataCenter` | O data center de coleta de dados do Adobe. Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. Os valores potenciais são: <ul><li>`d1`: Data center de San Jose</li><li>`d2`: data center de Dallas</li></ul> |
| `reportSuite` | A ID do conjunto de relatórios conforme especificado no beacon da Web do JavaScript (por exemplo, `s_code.js` ou `dtm`). |
| `trackingServer` | Um domínio de coleta de dados não SSL. Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. |
| `trackingServerSecure` | Um domínio de coleta de dados SSL. Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. |
| `visitorNamespace` | O namespace usado para agrupar visitantes. Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. |

**Adobe Audience Manager**

| Parâmetro | Descrição |
| --- | --- |
| `aamUUIDCookieName` | Nome do cookie primário contendo a ID de usuário exclusiva retornada do Adobe Audience Manager. |

**Serviço de identidade da Adobe Experience Cloud (ECID)**

| Parâmetro | Descrição |
| --- | --- |
| `imsOrgID` | Sua IMS Organization ID. |

**Adobe Target**

| Parâmetro | Descrição |
| --- | --- |
| `clientCode` | Código do cliente que identifica um cliente no Sistema Adobe Target. |
