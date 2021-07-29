---
keywords: Experience Platform, home, tópicos populares
solution: Experience Platform
title: Visão geral da biblioteca JavaScript de privacidade do Adobe
topic-legacy: overview
description: A Biblioteca JavaScript de Privacidade do Adobe permite recuperar identidades de titular de dados para uso no Privacy Service.
exl-id: 757bf69e-25bf-4ef9-9787-3e74b213908a
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '944'
ht-degree: 6%

---

# Visão geral da biblioteca JavaScript de privacidade do Adobe

Como processador de dados, o Adobe processa dados pessoais de acordo com a permissão e as instruções de sua empresa. Como o controlador de dados, você determinará os dados pessoais que a Adobe processa e armazena em seu nome. Dependendo das informações que você escolher enviar por meio das soluções da Adobe Experience Cloud, o Adobe pode armazenar informações privadas aplicáveis às regulamentações de privacidade, como [!DNL General Data Protection Regulation] (GDPR) e [!DNL California Consumer Privacy Act] (CCPA). Consulte o documento sobre [privacidade no Adobe Experience Cloud](https://www.adobe.com/br/privacy/marketing-cloud.html) para obter mais informações sobre como as soluções do Experience Cloud coletam dados privados.

A **Biblioteca JavaScript de Privacidade do Adobe** permite que os controladores de dados automatizem a recuperação de todas as identidades de titular de dados geradas pelas soluções [!DNL Experience Cloud] de um domínio específico. Usando a API fornecida pelo [Adobe Experience Platform Privacy Service](home.md), essas identidades podem ser usadas para criar solicitações de acesso e exclusão de dados privados pertencentes a esses titulares de dados.

>[!NOTE]
>
>O [!DNL Privacy JS Library] normalmente só precisa ser instalado em páginas relacionadas à privacidade e não precisa ser instalado em todas as páginas de um site ou domínio.

## Funções

O [!DNL Privacy JS Library] fornece várias funções para gerenciar identidades em [!DNL Privacy Service]. Essas funções só podem ser usadas para gerenciar as identidades que são armazenadas no navegador para um visitante específico. Eles não podem ser usados para enviar informações diretamente para o [!DNL Experience Cloud Central Service].

A tabela a seguir descreve as diferentes funções fornecidas pela biblioteca:

| Função | Descrição |
| --- | --- |
| `retrieveIdentities` | Retorna uma matriz de identidades correspondentes (`validIds`) que foram recuperadas de [!DNL Privacy Service], bem como uma matriz de identidades que não foram encontradas (`failedIds`). |
| `removeIdentities` | Remove cada identidade (válida) correspondente do navegador. Retorna uma matriz de identidades correspondentes (`validIds`), com cada identidade contendo um booleano `isDeletedClientSide` que indica se essa ID foi excluída. |
| `retrieveThenRemoveIdentities` | Recupera uma matriz de identidades correspondentes (`validIds`) e remove essas identidades do navegador. Embora essa função seja semelhante a `removeIdentities`, ela é melhor usada quando a solução Adobe que você está usando requer uma solicitação de acesso antes da exclusão ser possível (como quando um identificador exclusivo deve ser recuperado antes de fornecê-lo em uma solicitação de exclusão). |

>[!NOTE]
>
>`removeIdentities` e remover  `retrieveThenRemoveIdentities` somente identidades do navegador para soluções específicas do Adobe que as suportam. Por exemplo, o Adobe Audience Manager não exclui as IDs demdex armazenadas em cookies de terceiros, enquanto o Adobe Target exclui todos os cookies que armazenam suas IDs.

Como todas as três funções representam processos assíncronos, quaisquer identidades recuperadas devem ser tratadas usando retornos de chamada ou promessas.


## Instalação

Para começar a usar o [!DNL Privacy JS Library], você deve instalá-lo em sua máquina usando um dos seguintes métodos:

* Instale usando npm executando o seguinte comando: `npm install @adobe/adobe-privacy`
* Instale a [extensão de tag do Adobe Privacy](../tags/extensions/web/privacy/overview.md) sob o nome `AdobePrivacy`
* Baixe do repositório [Experience Cloud GitHub](https://github.com/Adobe-Marketing-Cloud/adobe-privacy)

## Instancie o [!DNL Privacy JS Library]

Todos os aplicativos que utilizam o [!DNL Privacy JS Library] devem instanciar um novo objeto `AdobePrivacy`, que deve ser configurado para uma solução Adobe específica. Por exemplo, uma instanciação do Adobe Analytics seria semelhante ao seguinte:

```js
var adobePrivacy = new AdobePrivacy({
    imsOrgID: "{IMS_ORG}",
    reportSuite: "{REPORT_SUITE_ID}",
    trackingServer: "{SERVER_URL}",
    clientCode: "{TARGET_CLIENT_CODE}"
});
```

Para obter uma lista completa dos parâmetros suportados para diferentes soluções Adobe, consulte a seção Apêndice sobre os [parâmetros de configuração da solução Adobe](#adobe-solution-configuration-parameters) suportados.

## Amostras de código

As amostras de código a seguir demonstram como usar o [!DNL Privacy JS Library] para vários cenários comuns, desde que você não esteja usando tags.

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
| `validIds` | Um objeto JSON contendo todas as IDs que foram recuperadas com êxito. |
| `failedIDs` | Um objeto JSON contendo todas as IDs que não foram recuperadas de [!DNL Privacy Service] ou que não foi encontrado. |

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

O código a seguir define uma função, `handleRemovedIDs`, a ser usada como um retorno de chamada ou promessa para lidar com as identidades recuperadas por `removeIdentities` após terem sido removidas do navegador.

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
| `failedIDs` | Um objeto JSON contendo todas as IDs que não foram recuperadas de [!DNL Privacy Service] ou que não foi encontrado. |

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

Ao ler este documento, você foi introduzido nas funcionalidades principais do [!DNL Privacy JS Library]. Depois de usar a biblioteca para recuperar uma lista de identidades, você pode usar essas identidades para criar acesso aos dados e excluir solicitações para a API [!DNL Privacy Service]. Consulte o [Guia do desenvolvedor do Privacy Service](api/getting-started.md) para obter mais informações.

## Apêndice

Esta seção contém informações complementares para usar o [!DNL Privacy JS Library].

### Parâmetros de configuração da solução Adobe

Veja a seguir uma lista dos parâmetros de configuração aceitos para soluções de Adobe compatíveis, usadas ao [instanciar um objeto do AdobePrivacy](#instantiate-the-privacy-js-library).

**Adobe Analytics**

| Parâmetro | Descrição |
| --- | --- |
| `cookieDomainPeriods` | O número de períodos em um domínio para rastreamento de cookie (o padrão é 2). |
| `dataCenter` | data center de coleta de Adobe. Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. Os valores potenciais são: <ul><li>&quot;d1&quot;: Data center de San Jose.</li><li>&quot;d2&quot;: Data center de Dallas.</li></ul> |
| `reportSuite` | A ID do conjunto de relatórios conforme especificado no beacon da Web do JavaScript (por exemplo, &quot;s_code.js&quot; ou &quot;dtm&quot;). |
| `trackingServer` | Domínio de coleta de dados (não SSL). Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. |
| `trackingServerSecure` | Domínio de coleta de dados (SSL). Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. |
| `visitorNamespace` | Namespace usado para agrupar visitantes. Isso só deve ser incluído se for especificado no beacon da Web do JavaScript. |

**Adobe Target**

| Parâmetro | Descrição |
| --- | --- |
| `clientCode` | Código do cliente que identifica um cliente no Sistema Adobe Target. |

**Adobe Audience Manager**

| Parâmetro | Descrição |
| --- | --- |
| `aamUUIDCookieName` | Nome do cookie primário contendo a ID de usuário exclusiva retornada do Adobe Audience Manager. |

**Serviço Adobe ID (ECID)**

| Parâmetro | Descrição |
| --- | --- |
| `imsOrgID` | Sua IMS Organization ID. |
