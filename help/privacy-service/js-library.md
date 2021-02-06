---
keywords: Experience Platform;home;populares tópicos
solution: Experience Platform
title: Visão geral da biblioteca JavaScript de privacidade do Adobe
topic: overview
description: A Biblioteca JavaScript de privacidade do Adobe permite recuperar identidades de pessoa de dados para uso no Privacy Service.
translation-type: tm+mt
source-git-commit: f2238d35f3e2a279fbe8ef8b581282102039e932
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 6%

---


# Visão geral da Biblioteca JavaScript de privacidade do Adobe

Como processador de dados, o Adobe processa dados pessoais de acordo com as permissões e instruções da sua empresa. Como o controlador de dados, você determinará os dados pessoais que a Adobe processa e armazena em seu nome. Dependendo das informações que você escolher enviar pelas soluções Adobe Experience Cloud, o Adobe pode armazenar informações privadas aplicáveis às regulamentações de privacidade, como [!DNL General Data Protection Regulation] (GDPR) e [!DNL California Consumer Privacy Act] (CCPA). Consulte o documento sobre a privacidade [no Adobe Experience Cloud](https://www.adobe.com/br/privacy/marketing-cloud.html) para obter mais informações sobre como as soluções Experience Cloud coletam dados privados.

A **Biblioteca JavaScript de Privacidade do Adobe** permite que os controladores de dados automatizem a recuperação de todas as identidades de indivíduos de dados geradas pelas soluções [!DNL Experience Cloud] para um domínio específico. Usando a API fornecida pela [Adobe Experience Platform Privacy Service](home.md), essas identidades podem ser usadas para criar solicitações de acesso e exclusão de dados privados pertencentes a essas pessoas de dados.

>[!NOTE]
>
>O [!DNL Privacy JS Library] normalmente precisa apenas ser instalado em páginas relacionadas à privacidade e não precisa ser instalado em todas as páginas de um site ou domínio.

## Funções

O [!DNL Privacy JS Library] fornece várias funções para gerenciar identidades em [!DNL Privacy Service]. Essas funções só podem ser usadas para gerenciar as identidades armazenadas no navegador para um visitante específico. Eles não podem ser usados para enviar informações diretamente para [!DNL Experience Cloud Central Service].

A tabela a seguir descreve as diferentes funções fornecidas pela biblioteca:

| Função | Descrição |
| --- | --- |
| `retrieveIdentities` | Retorna uma matriz de identidades correspondentes (`validIds`) que foram recuperadas de [!DNL Privacy Service], bem como uma matriz de identidades que não foram encontradas (`failedIds`). |
| `removeIdentities` | Remove cada identidade correspondente (válida) do navegador. Retorna uma matriz de identidades correspondentes (`validIds`), com cada identidade contendo um booleano `isDeletedClientSide` que indica se essa ID foi excluída. |
| `retrieveThenRemoveIdentities` | Recupera uma matriz de identidades correspondentes (`validIds`) e remove essas identidades do navegador. Embora essa função seja semelhante a `removeIdentities`, é melhor usada quando a solução Adobe que você está usando requer uma solicitação de acesso antes da exclusão ser possível (como quando um identificador exclusivo deve ser recuperado antes de ser fornecido em uma solicitação de exclusão). |

>[!NOTE]
>
>`removeIdentities` e  `retrieveThenRemoveIdentities` só remova identidades do navegador para obter soluções de Adobe específicas que as suportem. Por exemplo, a Adobe Audience Manager não exclui as IDs demdex armazenadas em cookies de terceiros, enquanto a Adobe Target exclui todos os cookies que armazenam suas IDs.

Como as três funções representam processos assíncronos, qualquer identidade recuperada deve ser tratada com retornos de chamada ou promessas.


## Instalação

Para start usando o [!DNL Privacy JS Library], você deve instalá-lo no computador usando um dos seguintes métodos:

* Instale usando npm executando o seguinte comando: `npm install @adobe/adobe-privacy`
* Use a Extensão Adobe Launch sob o nome `AdobePrivacy`
* Baixar do repositório [Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instanciar [!DNL Privacy JS Library]

Todos os aplicativos que utilizam [!DNL Privacy JS Library] devem instanciar um novo objeto `AdobePrivacy`, que deve ser configurado para uma solução Adobe específica. Por exemplo, uma instanciação para o Adobe Analytics seria semelhante ao seguinte:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Para obter uma lista completa dos parâmetros suportados para diferentes soluções de Adobe, consulte a seção do apêndice sobre os [parâmetros de configuração da solução Adobe](#adobe-solution-configuration-parameters) suportados.

## Amostras de código

As amostras de código a seguir demonstram como usar o [!DNL Privacy JS Library] para vários cenários comuns, desde que você não esteja usando [!DNL Launch] ou o DTM.

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
| `failedIDs` | Um objeto JSON que contém todas as IDs que não foram recuperadas de [!DNL Privacy Service] ou que não foram encontradas de outra forma. |

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

O código a seguir define uma função, `handleRemovedIDs`, a ser usada como um retorno de chamada ou promessa para lidar com as identidades recuperadas por `removeIdentities` depois que elas forem removidas do navegador.

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
| `validIds` | Um objeto JSON que contém todas as IDs recuperadas com êxito. |
| `failedIDs` | Um objeto JSON que contém todas as IDs que não foram recuperadas de [!DNL Privacy Service] ou que não foram encontradas de outra forma. |

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

Ao ler este documento, você foi apresentado às funcionalidades principais do [!DNL Privacy JS Library]. Depois de usar a biblioteca para recuperar uma lista de identidades, você pode usar essas identidades para criar acesso aos dados e excluir solicitações para a API [!DNL Privacy Service]. Consulte o [guia do desenvolvedor do Privacy Service](api/getting-started.md) para obter mais informações.

## Apêndice

Esta seção contém informações adicionais para usar o [!DNL Privacy JS Library].

### Parâmetros de configuração da solução Adobe

A seguir está uma lista dos parâmetros de configuração aceitos para as soluções de Adobe compatíveis, usadas quando [instanciar um objeto AdobePrivacy](#instantiate-the-privacy-js-library).

**Adobe Analytics**

| Parâmetro | Descrição |
| --- | --- |
| `cookieDomainPeriods` | O número de períodos em um domínio para o rastreamento de cookies (o padrão é 2). |
| `dataCenter` | data center de coleta de dados do Adobe. Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. Os valores potenciais são: <ul><li>&quot;d1&quot;: Data center de San Jose.</li><li>&quot;d2&quot;: Data center de Dallas.</li></ul> |
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
| `aamUUIDCookieName` | Nome do cookie primário que contém a ID de usuário exclusiva retornada da Adobe Audience Manager. |

**Serviço Adobe ID (ECID)**

| Parâmetro | Descrição |
| --- | --- |
| `imsOrgID` | Sua IMS Organization ID. |