---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Visão geral da Biblioteca JavaScript de privacidade da Adobe
topic: overview
translation-type: tm+mt
source-git-commit: 5b32c1955fac4f137ba44e8189376c81cdbbfc40
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 5%

---


# Visão geral da Biblioteca JavaScript de privacidade da Adobe

Como um processador de dados, a Adobe processa dados pessoais de acordo com suas permissões e instruções de empresa. Como o controlador de dados, você determinará os dados pessoais que a Adobe processa e armazena em seu nome. Dependendo das informações que você escolher enviar pelas soluções da Adobe Experience Cloud, a Adobe pode armazenar informações privadas aplicáveis a regulamentos de privacidade, como o [!DNL General Data Protection Regulation] (RGPD) e [!DNL California Consumer Privacy Act] (CCPA). Consulte o documento sobre [privacidade na Adobe Experience Cloud](https://www.adobe.com/br/privacy/marketing-cloud.html) para obter mais informações sobre como as soluções do Experience Cloud coletam dados privados.

A Biblioteca **JavaScript de privacidade da** Adobe permite que os controladores de dados automatizem a recuperação de todas as identidades de pessoa de dados geradas pelas [!DNL Experience Cloud] soluções para um domínio específico. Usando a API fornecida pelo [Adobe Experience Platform Privacy Service](home.md), essas identidades podem ser usadas para criar solicitações de acesso e exclusão de dados privados pertencentes a essas pessoas de dados.

>[!NOTE]
>
>Normalmente, o [!DNL Privacy JS Library] precisa apenas ser instalado em páginas relacionadas à privacidade e não precisa ser instalado em todas as páginas de um site ou domínio.

## Funções

O [!DNL Privacy JS Library] fornece várias funções para gerenciar identidades em [!DNL Privacy Service]. Essas funções só podem ser usadas para gerenciar as identidades armazenadas no navegador para um visitante específico. Eles não podem ser usados para enviar informações [!DNL Experience Cloud Central Service] diretamente ao público.

A tabela a seguir descreve as diferentes funções fornecidas pela biblioteca:

| Função | Descrição |
| --- | --- |
| `retrieveIdentities` | Retorna uma matriz de identidades correspondentes (`validIds`) que foram recuperadas [!DNL Privacy Service], bem como uma matriz de identidades que não foram encontradas (`failedIds`). |
| `removeIdentities` | Remove cada identidade correspondente (válida) do navegador. Retorna uma matriz de identidades correspondentes (`validIds`), com cada identidade contendo um `isDeleteClientSide` booleano que indica se essa ID foi excluída. |
| `retrieveThenRemoveIdentities` | Recupera uma matriz de identidades correspondentes (`validIds`) e remove essas identidades do navegador. Embora essa função seja semelhante a `removeIdentities`, é melhor usada quando a solução Adobe que você está usando requer uma solicitação de acesso antes que a exclusão seja possível (como quando um identificador exclusivo deve ser recuperado antes de ser fornecido em uma solicitação de exclusão). |

>[!NOTE]
>
>`removeIdentities` e `retrieveThenRemoveIdentities` remover identidades somente do navegador para soluções específicas da Adobe que as suportam. Por exemplo, o Adobe Audience Manager não exclui as IDs demdex armazenadas em cookies de terceiros, enquanto o Adobe Target exclui todos os cookies que armazenam suas IDs.

Como as três funções representam processos assíncronos, qualquer identidade recuperada deve ser tratada com retornos de chamada ou promessas.


## Instalação

Para start usando o [!DNL Privacy JS Library], você deve instalá-lo em sua máquina usando um dos seguintes métodos:

* Instale usando npm executando o seguinte comando: `npm install @adobe/adobe-privacy`
* Use a extensão do Adobe Launch com o nome `AdobePrivacy`
* Download de [https://github.com/Adobe-Marketing-Cloud/adobe-privacy](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instancie o [!DNL Privacy JS Library]

Todos os aplicativos que utilizam o [!DNL Privacy JS Library] devem instanciar um novo `AdobePrivacy` objeto, que deve ser configurado para uma solução específica da Adobe. Por exemplo, uma instância do Adobe Analytics seria semelhante ao seguinte:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    key: "{DATA_SUBJECT_ID}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Para obter uma lista completa dos parâmetros compatíveis com diferentes soluções da Adobe, consulte a seção de apêndice sobre os parâmetros [de configuração da solução](#adobe-solution-configuration-parameters)Adobe suportados.

## Amostras de código

As amostras de código a seguir demonstram como usar o [!DNL Privacy JS Library] para vários cenários comuns, desde que você não esteja usando [!DNL Launch] ou DTM.

### Recuperar identidades

Este exemplo demonstra como recuperar uma lista de identidades de [!DNL Experience Cloud].

#### JavaScript

O código a seguir define uma função, `handleRetrievedIDs`, a ser usada como um retorno de chamada ou promessa para lidar com as identidades recuperadas por `retrieveIdentities`.

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
| `validIds` | Um objeto JSON que contém todas as IDs recuperadas com êxito. |
| `failedIDs` | Um objeto JSON que contém todas as IDs que não foram recuperadas [!DNL Privacy Service]ou que não foram encontradas. |

#### Resultado

Se o código for executado com êxito, `validIDs` será preenchido com uma lista de identidades recuperadas.

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

O código a seguir define uma função, `handleRemovedIDs`, a ser usada como um retorno de chamada ou promessa para lidar com as identidades recuperadas `removeIdentities` após elas terem sido removidas do navegador.

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
| `validIds` | Um objeto JSON que contém todas as IDs recuperadas com êxito. |
| `failedIDs` | Um objeto JSON que contém todas as IDs que não foram recuperadas [!DNL Privacy Service]ou que não foram encontradas. |

#### Resultado

Se o código for executado com êxito, `validIDs` será preenchido com uma lista de identidades recuperadas.

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

Ao ler este documento, o senhor foi apresentado às principais funcionalidades do [!DNL Privacy JS Library]. Depois de usar a biblioteca para recuperar uma lista de identidades, você pode usar essas identidades para criar acesso aos dados e excluir solicitações à [!DNL Privacy Service] API. Consulte o guia [do desenvolvedor do](api/getting-started.md) Privacy Service para obter mais informações.

## Apêndice

Esta seção contém informações adicionais para o uso do [!DNL Privacy JS Library].

### Parâmetros de configuração da solução Adobe

A seguir está uma lista dos parâmetros de configuração aceitos para as soluções da Adobe suportadas, usados ao [instanciar um objeto](#instantiate-the-privacy-js-library)Adobe Privacy.

**Adobe Analytics**

| Parâmetro | Descrição |
| --- | --- |
| `cookieDomainPeriods` | O número de períodos em um domínio para o rastreamento de cookies (o padrão é 2). |
| `dataCenter` | Centro de dados de coleta de dados da Adobe. Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. Os valores potenciais são: <ul><li>&quot;d1&quot;: Data center de San Jose.</li><li>&quot;d2&quot;: Data center de Dallas.</li></ul> |
| `reportSuite` | ID do conjunto de relatórios conforme especificado no beacon da Web JavaScript (por exemplo, &quot;s_code.js&quot; ou &quot;dtm&quot;). |
| `trackingServer` | Domínio de coleta de dados (não SSL). Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. |
| `trackingServerSecure` | Domínio de coleta de dados (SSL). Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. |
| `visitorNamespace` | Namespace usada para agrupar visitantes. Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. |

**Adobe Target**

| Parâmetro | Descrição |
| --- | --- |
| `clientCode` | Código do cliente que identifica um cliente no Adobe Target System. |

**Adobe Audience Manager**

| Parâmetro | Descrição |
| --- | --- |
| `aamUUIDCookieName` | Nome do cookie primário que contém a ID de usuário exclusiva retornada do Adobe Audience Manager. |

**Serviço de Adobe ID (ECID)**

| Parâmetro | Descrição |
| --- | --- |
| `imsOrgID` | Sua ID de empresa IMS. |