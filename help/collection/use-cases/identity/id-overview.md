---
title: Dados de identidade no Web SDK
description: Saiba como recuperar e gerenciar Adobe Experience Cloud IDs (ECIDs) usando o Adobe Experience Platform Web SDK.
exl-id: 03060cdb-becc-430a-b527-60c055c2a906
source-git-commit: 66105ca19ff1c75f1185b08b70634b7d4a6fd639
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 0%

---

# Dados de identidade no Web SDK

O Adobe Experience Platform Web SDK usa [Adobe Experience Cloud IDs (ECIDs)](/help/identity-service/features/ecid.md) para rastrear o comportamento do visitante. Usando o [!DNL ECIDs], você pode garantir que cada dispositivo tenha um identificador exclusivo que possa persistir em várias sessões, vinculando todas as ocorrências que ocorrem durante e entre sessões da Web a um dispositivo específico.

Este documento fornece uma visão geral de como gerenciar [!DNL ECIDs] e [!DNL CORE IDs] usando o Web SDK.

## Rastreamento de ECIDs usando o Web SDK {#tracking-ecids-web-sdk}

O Web SDK atribui e rastreia [!DNL ECIDs] usando cookies, com vários métodos disponíveis para configurar como esses cookies são gerados.

Quando um novo usuário chega ao seu site, o [Adobe Experience Cloud Identity Service](/help/identity-service/home.md) tenta definir um cookie de identificação do dispositivo para esse usuário.

* Para novos visitantes, um [!DNL ECID] é gerado e retornado na primeira resposta do Edge Network do Experience Platform.
* Para visitantes recorrentes, o [!DNL ECID] é recuperado do cookie [`kndctr_<orgId>_identity`](https://experienceleague.adobe.com/en/docs/core-services/interface/data-collection/cookies/web-sdk) e adicionado à carga da solicitação pela Edge Network.

Depois que o cookie contendo o [!DNL ECID] for definido, cada solicitação subsequente gerada pelo Web SDK incluirá um [!DNL ECID] codificado no cookie `kndctr_<orgId>_identity`.

Ao usar cookies para identificação de dispositivos, você tem duas maneiras de interagir com a Edge Network:

1. Crie um CNAME em seu próprio domínio que aponte para `adobedc.net`. Este método é conhecido como [coleção de dados próprios](#first-party).
1. Enviar dados diretamente para o domínio do Edge Network `adobedc.net`. Este método é conhecido como [coleção de dados de terceiros](#third-party).

Conforme explicado nas seções abaixo, o método de coleta de dados que você escolhe usar tem um impacto direto na vida útil do cookie nos navegadores.

## Rastreamento de IDs principais usando o Web SDK {#tracking-coreid-web-sdk}

Ao usar o Google Chrome com cookies de terceiros habilitados e não houver nenhum cookie `kndctr_<orgId>_identity` definido, a primeira solicitação do Edge Network passa por um domínio `demdex.net`, que define um cookie demdex. Este cookie contém um [!DNL CORE ID]. Este é um identificador de usuário único, diferente do [!DNL ECID].

Dependendo da sua implementação, talvez você queira [acessar o [!DNL CORE ID]](#retrieve-coreid).

### Coleta de dados primários {#first-party}

A coleta de dados primários envolve a configuração de cookies por meio de um `CNAME` em seu próprio domínio que aponta para `adobedc.net`.

Embora os navegadores tenham durante muito tempo tratado cookies definidos por `CNAME` pontos de extremidade de maneira semelhante aos definidos por pontos de extremidade de propriedade do site, as alterações recentes implementadas pelos navegadores criaram uma distinção em como os cookies `CNAME` são tratados. Embora não haja navegadores que atualmente bloqueiam cookies próprios `CNAME` por padrão, alguns navegadores restringem o tempo de vida dos cookies definidos com um `CNAME` para apenas sete dias.

### Coleta de dados de terceiros {#third-party}

A coleta de dados de terceiros envolve o envio de dados diretamente para o domínio do Edge Network `adobedc.net`.

Nos últimos anos, os navegadores da Web têm se tornado cada vez mais restritivos no manuseio de cookies definidos por terceiros. Alguns navegadores bloqueiam cookies de terceiros por padrão. Se você usar cookies de terceiros para identificar visitantes do site, a vida útil desses cookies é quase sempre mais curta do que o que estaria disponível usando cookies primários. Às vezes, um cookie de terceiros expira em apenas sete dias.

Além disso, ao usar a coleta de dados de terceiros, alguns bloqueadores de anúncios restringem o tráfego aos endpoints de coleta de dados do Adobe.

### Efeitos da duração do cookie em aplicativos Adobe Experience Cloud {#lifespans}

Independentemente de você escolher a coleção de dados próprios ou de terceiros, o período de tempo em que um cookie pode persistir afeta diretamente a contagem de visitantes no [Adobe Analytics](https://experienceleague.adobe.com/en/docs/analytics?lang=pt-BR) e no [Customer Journey Analytics](https://experienceleague.adobe.com/pt-br/docs/customer-journey-analytics). Além disso, os usuários finais podem experimentar experiências de personalização inconsistentes quando o [Adobe Target](https://experienceleague.adobe.com/en/docs/target) ou o [Offer Decisioning](https://experienceleague.adobe.com/en/docs/target/using/integrate/ajo/offer-decision) são usados no site.

Por exemplo, considere uma situação em que você criou uma experiência de personalização que promove qualquer item para a página inicial se um usuário o visualizou três vezes nos últimos sete dias.

Se um usuário final visitar três vezes por semana e não retornar ao site por sete dias, ele poderá ser considerado um novo usuário quando retornar ao site, pois seus cookies podem ter sido excluídos por uma política do navegador (dependendo do navegador usado quando visitou o site). Se isso acontecer, a ferramenta do Analytics tratará o visitante como um novo usuário, embora ele tenha visitado o site há pouco mais de sete dias. Além disso, qualquer esforço para personalizar a experiência do usuário começa novamente.

### IDs de dispositivo próprio (FPIDs) {#fpid}

Para levar em conta os efeitos da duração do cookie conforme descrito acima, você pode optar por definir e gerenciar seus próprios identificadores de dispositivo. Consulte o manual sobre [IDs de dispositivo próprio](./first-party-device-ids.md) para obter mais informações.

## Recuperar a ECID e a região do usuário atual {#retrieve-ecid}

Dependendo do seu caso de uso, há duas maneiras de acessar o [!DNL ECID]:

* [Recuperar o [!DNL ECID] por meio do Preparo de Dados para a Coleta de Dados](#retrieve-ecid-data-prep): este é o método recomendado que você deve usar.
* [Recuperar  [!DNL ECID] por meio do comando `getIdentity()`](#retrieve-ecid-getidentity): use este método somente quando precisar das informações [!DNL ECID] no lado do cliente.

### Recuperar o [!DNL ECID] por meio do Preparo de Dados para a Coleção de Dados {#retrieve-ecid-data-prep}

Use o [Preparo de Dados para a Coleção de Dados](/help/datastreams/data-prep.md) para mapear o [!DNL ECID] para um campo [!DNL XDM]. Esta é a maneira recomendada de acessar o [!DNL ECID].

Para fazer isso, defina o campo de origem para o seguinte caminho:

```js
xdm.identityMap.ECID[0].id
```

Em seguida, defina o campo de destino como um caminho XDM, onde o campo é do tipo `string`.

![Captura de tela de mapeamento de sequência de dados](/help/tags/extensions/client/web-sdk/assets/access-ecid-data-prep.png)


### Recuperar o [!DNL ECID] através do comando `getIdentity()` {#retrieve-ecid-getidentity}

>[!IMPORTANT]
>
>Você só deve recuperar a ECID por meio do comando `getIdentity()` se precisar de [!DNL ECID] no lado do cliente. Se você quiser mapear a ECID apenas para um campo XDM, use o [Preparo de dados para a coleção de dados](#retrieve-ecid-data-prep).

Para recuperar a ECID exclusiva do visitante atual, use o comando `getIdentity`. Para visitantes novos que ainda não têm um [!DNL ECID], esse comando gera um novo [!DNL ECID]. `getIdentity` também retorna a ID da região do visitante.

>[!NOTE]
>
>Normalmente, esse método é usado com soluções personalizadas que exigem a leitura da ID do [!DNL Experience Cloud] ou uma dica de localização do Adobe Audience Manager. Ela não é usada em uma implementação padrão.

```javascript
alloy("getIdentity")
  .then(function(result) {
    // The command succeeded.
    console.log("ECID:", result.identity.ECID);
    console.log("RegionId:", result.edge.regionId);
  })
  .catch(function(error) {
    // The command failed.
    // "error" will be an error object with additional information.
  });
```

## Recuperar a ID PRINCIPAL do usuário atual {#retrieve-coreid}

Para recuperar a ID CORE de um usuário, você pode usar o comando [`getIdentity()`](/help/collection/js/commands/getidentity.md), conforme mostrado abaixo.

```js
alloy("getIdentity",{
  "namespaces": ["CORE"]
});
```

## Usando o `identityMap` {#using-identitymap}

Usando um campo XDM [`identityMap` &#x200B;](/help/xdm/schema/composition.md#identityMap), você pode identificar um dispositivo/usuário usando várias identidades, definir seu estado de autenticação e decidir qual identificador é considerado o principal. Se nenhum identificador tiver sido definido como `primary`, o padrão principal será `ECID`.

`identityMap` campos são atualizados usando o comando `sentEvent`.

```javascript
alloy("sendEvent", {
  xdm: {
    "identityMap": {
      "ID_NAMESPACE": [ // Notice how each namespace can contain multiple identifiers.
        {
          "id": "1234",
          "authenticatedState": "authenticated",
          "primary": true
        }
      ]
    }
  }
});
```

>[!NOTE]
>
>A Adobe recomenda enviar namespaces que representam uma pessoa, como `CRMID`, como a identidade principal.

Cada propriedade em `identityMap` representa identidades pertencentes a um [namespace de identidade](/help/identity-service/features/namespaces.md) específico. O nome da propriedade deve ser o símbolo de namespace de identidade, que pode ser encontrado listado na interface do usuário do Adobe Experience Platform em &quot;[!UICONTROL Identities]&quot;. O valor da propriedade deve ser uma matriz de identidades pertencentes a esse namespace de identidade.

>[!IMPORTANT]
>
>A ID do namespace transmitida em `identityMap` diferencia maiúsculas de minúsculas. Use a ID de namespace correta para evitar uma coleta de dados incompleta.

Cada objeto de identidade na matriz de identidades contém as seguintes propriedades:

| Propriedade | Tipo de dados | Descrição |
| --- | --- | --- |
| `id` | String | **(Obrigatório)** A ID que você deseja definir para o namespace fornecido. |
| `authenticatedState` | String | **(Obrigatório)** O estado de autenticação da ID. Os valores possíveis são `ambiguous`, `authenticated` e `loggedOut`. |
| `primary` | Booleano | Determina se essa identidade deve ser usada como um fragmento primário no perfil. Por padrão, a ECID é definida como o identificador principal do usuário. Se omitido, esse valor assumirá `false` como padrão. |

O uso do campo `identityMap` para identificar dispositivos ou usuários leva ao mesmo resultado que o uso do método [`setCustomerIDs`](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/setcustomerids.html) de [!DNL ID Service API]. Consulte a [documentação da API do serviço de ID](https://experienceleague.adobe.com/docs/id-service/using/id-service-api/methods/get-set.html) para obter mais detalhes.

## Migração da API do visitante para ECID {#migrating-visitor-api-ecid}

Ao migrar do usando a API do visitante, também é possível migrar os cookies AMCV existentes. Para habilitar a migração da ECID, defina o parâmetro `idMigrationEnabled` na configuração. A migração de ID habilita os seguintes casos de uso:

* Quando algumas páginas de um domínio estão usando a API de visitante e outras páginas estão usando essa SDK. Para dar suporte a esse caso, o SDK lê os cookies AMCV existentes e grava um novo cookie com a ECID existente. Além disso, o SDK grava cookies AMCV para que, se a ECID for obtida primeiro em uma página instrumentada com a SDK, as páginas subsequentes instrumentadas com a API do visitante terão a mesma ECID.
* Quando o Adobe Experience Platform Web SDK é configurado em uma página que também tem a API do visitante. Para dar suporte a esse caso, se o cookie AMCV não foi definido, o SDK procura a API do visitante na página e a chama para obter a ECID.
* Quando todo o site estiver usando o Adobe Experience Platform Web SDK e não tiver uma API de visitante, é útil migrar as ECIDs para que as informações retornadas do visitante sejam retidas. Depois que a SDK for implantada com `idMigrationEnabled` por um momento para que a maioria dos cookies do visitante seja migrada, a configuração poderá ser desativada.

### Atualização de características para migração

Quando dados formatados em XDM são enviados para o Audience Manager, esses dados devem ser convertidos em sinais ao migrar. Suas características devem ser atualizadas para refletir as novas chaves que o XDM fornece. Este processo fica mais fácil com a [ferramenta BAAAM](https://experienceleague.adobe.com/docs/audience-manager/user-guide/reference/bulk-management-tools/bulk-management-intro.html#getting-started-with-bulk-management) criada pela Audience Manager.

## Usar no encaminhamento de eventos

Se você tiver o [encaminhamento de eventos](/help/tags/ui/event-forwarding/overview.md) habilitado e estiver usando o `appmeasurement.js` e o `visitor.js`, poderá manter o recurso de encaminhamento de eventos habilitado e isso não causará problemas. No back-end, o Adobe busca qualquer segmento do AAM e os adiciona à chamada do Analytics. Se a chamada para o Analytics contiver esses segmentos, o Analytics não chamará a Audience Manager para encaminhar dados, portanto, não há nenhuma coleta de dados dupla. Também não há necessidade de Dica de localização ao usar o Web SDK, pois os mesmos pontos de extremidade de segmentação são chamados no back-end.
