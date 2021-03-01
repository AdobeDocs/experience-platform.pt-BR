---
title: Suporte às preferências de consentimento do cliente usando o SDK da Web da Adobe Experience Platform
description: Saiba como oferecer suporte às preferências de consentimento com o SDK da Web da Adobe Experience Platform.
keywords: consentimento; defaultConsent; consentimento padrão; setConsent; Mistura de privacidade de perfil; Mistura de privacidade de eventos de experiência; Mixin de privacidade;
translation-type: tm+mt
source-git-commit: 308c10eb0d1f78dad2b8b6158f28d0384a65c78c
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---


# Suporte às preferências de consentimento do cliente

Para respeitar a privacidade do usuário, convém solicitar o consentimento do usuário antes de permitir que o SDK use dados específicos do usuário para determinados fins. Atualmente, o SDK permite que os usuários incluam ou excluam de todos os fins, mas, no futuro, a Adobe espera fornecer um controle mais granular sobre fins específicos.

Se o usuário optar por todos os fins, o SDK poderá executar as seguintes tarefas:

* Envie dados de e para os servidores da Adobe.
* Leia e grave cookies ou itens de armazenamento da Web.

Se o usuário optar por não participar de todos os fins, o SDK não executará nenhuma dessas tarefas.

## Configuração do consentimento

Por padrão, o usuário é aceito para todos os fins. Para impedir que o SDK execute as tarefas acima até que o usuário opte por participar, passe `"defaultConsent": "pending"` durante a configuração do SDK da seguinte maneira:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```

Quando o consentimento padrão para o propósito geral está definido como pendente, a tentativa de executar qualquer comando que dependa das preferências de aceitação do usuário (por exemplo, o comando `event`) resulta no enfileiramento do comando no SDK. Esses comandos não são processados até que você comunique as preferências de aceitação do usuário ao SDK.

Nesse ponto, talvez você prefira solicitar que o usuário aceite participar de algum lugar na interface do usuário. Depois que as preferências do usuário forem coletadas, comunique essas preferências ao SDK.

## Comunicar preferências de consentimento por meio do Adobe Standard

Se o usuário optar por participar, execute o comando `setConsent` com a opção `general` definida como `in` da seguinte maneira:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    }]
});
```

Como o usuário agora aceitou, o SDK executa todos os comandos enfileirados anteriormente. Os comandos futuros que dependem da opção do usuário no não serão enfileirados e, em vez disso, serão executados imediatamente.

Se o usuário optar por rejeitar, execute o comando `setConsent` com a opção `general` definida como `out` da seguinte maneira:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "out"
      }
    }]
});
```

>[!NOTE]
>
>Depois que um usuário optar por rejeitar, o SDK não permitirá que você defina o consentimento dos usuários para `in`.

Como o usuário optou por rejeitar, as promessas que foram retornadas de comandos enfileirados anteriormente são rejeitadas. Os comandos futuros que dependem da aceitação do usuário retornarão promessas que são igualmente rejeitadas. Para obter mais informações sobre como manipular ou suprimir erros, consulte [Executando Comandos](../fundamentals/executing-commands.md).

>[!NOTE]
>
>Atualmente, o SDK suporta apenas a finalidade `general`. Embora planejemos criar um conjunto mais robusto de finalidades ou categorias que corresponderão aos diferentes recursos e ofertas de produtos da Adobe, a implementação atual é uma abordagem de aceitação de tudo ou nada.  Isso se aplica somente à Adobe Experience Platform [!DNL Web SDK] e NÃO a outras bibliotecas JavaScript da Adobe.

## Comunicar preferências de consentimento por meio do padrão TCF do IAB

O SDK suporta o registro das preferências de consentimento de um usuário fornecidas por meio do padrão da Estrutura de transparência e consentimento (TCF) do Interative Advertising Bureau Europe (IAB). A cadeia de consentimento pode ser definida por meio do mesmo comando `setConsent` acima, assim:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

Quando o consentimento é definido dessa forma, o Perfil do cliente em tempo real é atualizado com as informações de consentimento. Para que isso funcione, o esquema XDM do perfil precisa conter a [Mixin da privacidade do perfil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Ao enviar eventos, as informações de consentimento do IAB precisam ser adicionadas manualmente ao objeto XDM do evento. O SDK não inclui automaticamente as informações de consentimento nos eventos. Para enviar as informações de consentimento nos eventos, o [Mixin da Privacidade de eventos de experiência](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) precisa ser adicionado ao schema de eventos de experiência.

## Enviar ambos os padrões em uma solicitação

O SDK também oferece suporte ao envio de mais de um objeto de consentimento em uma solicitação.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "1.0",
      value: {
        general: "in"
      }
    },{
      standard: "IAB TCF",
      version: "2.0",
      value: "CO1Z4yuO1Z4yuAcABBENArCsAP_AAH_AACiQGCNX_T5eb2vj-3Zdt_tkaYwf55y3o-wzhhaIse8NwIeH7BoGP2MwvBX4JiQCGBAkkiKBAQdtHGhcCQABgIhRiTKMYk2MjzNKJLJAilsbe0NYCD9mnsHT3ZCY70--u__7P3fAwQgkwVLwCRIWwgJJs0ohTABCOICpBwCUEIQEClhoACAnYFAR6gAAAIDAACAAAAEEEBAIABAAAkIgAAAEBAKACIBAACAEaAhAARIEAsAJEgCAAVA0JACKIIQBCDgwCjlACAoAAAAA.YAAAAAAAAAAA",
      gdprApplies: true
    }]
});
```

## Persistência das preferências de consentimento

Depois de comunicar as preferências do usuário ao SDK usando o comando `setConsent`, o SDK manterá as preferências do usuário para um cookie. Na próxima vez que o usuário carregar seu site no navegador, o SDK recuperará e usará essas preferências persistentes para determinar se os eventos podem ou não ser enviados para a Adobe. Não há necessidade de executar o comando `setConsent` novamente, exceto para comunicar uma alteração nas preferências do usuário, o que você pode fazer a qualquer momento.

## Sincronização de identidades ao definir o consentimento

Quando o consentimento padrão está pendente, `setConsent` pode ser a primeira solicitação que sai e estabelece a identidade. Por causa disso, pode ser importante sincronizar identidades na primeira solicitação. O mapa de identidade pode ser adicionado ao comando `setConsent`, como no comando `sendEvent`. Consulte [Recuperar Experience Cloud ID](../identity/overview.md)

