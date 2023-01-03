---
title: Suporte às preferências de consentimento do cliente usando o SDK da Web da Adobe Experience Platform
description: Saiba como oferecer suporte às preferências de consentimento com o SDK da Web da Adobe Experience Platform.
keywords: consentimento; defaultConsent; consentimento padrão; setConsent; grupo de campos Privacidade de perfil; grupo de campos Privacidade de eventos de experiência; grupo de campos Privacidade;
exl-id: 647e4a84-4a66-45d6-8b05-d78786bca63a
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '950'
ht-degree: 0%

---

# Suporte às preferências de consentimento do cliente

Para respeitar a privacidade do usuário, convém solicitar o consentimento do usuário antes de permitir que o SDK use dados específicos do usuário para determinados fins. Atualmente, o SDK permite que os usuários incluam ou excluam de todas as finalidades, mas no futuro a Adobe espera fornecer um controle mais granular sobre finalidades específicas.

Se o usuário optar por todos os fins, o SDK poderá executar as seguintes tarefas:

* Envie dados de e para servidores Adobe.
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

Quando o consentimento padrão para o propósito geral estiver definido como pendente, a tentativa de executar quaisquer comandos que dependam das preferências de aceitação do usuário (por exemplo, a variável `sendEvent` ) resulta no comando em fila no SDK. Esses comandos não são processados até que você comunique as preferências de aceitação do usuário ao SDK.

>[!NOTE]
>
>Os comandos são enfileirados apenas na memória. Eles não são salvos em carregamentos de página.

Se você não quiser coletar eventos que ocorreram antes de as preferências de aceitação do usuário serem definidas, é possível enviar `"defaultConsent": "out"` durante a configuração do SDK. A tentativa de executar qualquer comando que dependa das preferências de aceitação do usuário não terá efeito até que você tenha comunicado as preferências de aceitação do usuário ao SDK.

>[!NOTE]
>
>Atualmente, o SDK suporta apenas um único propósito, tudo ou nada. Embora planejemos criar um conjunto mais robusto de finalidades ou categorias que corresponderão aos diferentes recursos do Adobe e ofertas de produtos, a implementação atual é uma abordagem de aceitação de tudo ou nada.  Isso se aplica somente ao Adobe Experience Platform [!DNL Web SDK] e NÃO outras bibliotecas JavaScript do Adobe.

Nesse ponto, talvez você prefira solicitar que o usuário aceite participar de algum lugar na interface do usuário. Depois que as preferências do usuário forem coletadas, comunique essas preferências ao SDK.

## Comunicar preferências de consentimento por meio do padrão Adobe Experience Platform

O SDK oferece suporte às versões 1.0 e 2.0 do padrão de consentimento do Adobe Experience Platform. Atualmente, os padrões 1.0 e 2.0 suportam apenas a aplicação automática de uma preferência de consentimento total ou nulo. O padrão 1.0 está sendo eliminado gradualmente em favor do padrão 2.0. O padrão 2.0 permite adicionar preferências de consentimento adicionais que podem ser usadas para impor manualmente a preferência de consentimento.

### Uso da versão padrão do Adobe 2.0

Se estiver usando o Adobe Experience Platform, será necessário incluir um grupo de campos de esquema de privacidade ao esquema do perfil. Consulte [Governança, privacidade e segurança no Adobe Experience Platform](../../landing/governance-privacy-security/overview.md) para obter mais informações sobre o Adobe standard versão 2.0. Você pode adicionar dados dentro do objeto de valor abaixo que correspondem ao esquema do `consents` do [!UICONTROL Consentimentos e preferências] grupo de campos do perfil.

Se o usuário optar por participar, execute o `setConsent` com a preferência de coleta definida como `y` como se segue:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
      }
    }]
});
```

O campo de hora deve especificar quando o usuário atualizou pela última vez suas preferências de consentimento. Se o usuário optar por rejeitar, execute o `setConsent` com a preferência de coleta definida como `n` como se segue:

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "n"
        },
        metadata: {
          time: "2021-03-17T15:51:30-07:00"
        }
      }
    }]
});
```

### Uso da versão padrão do Adobe 1.0

Se o usuário optar por participar, execute o `setConsent` com o `general` opção definida como `in` como se segue:

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

Se o usuário optar por rejeitar, execute o `setConsent` com o `general` opção definida como `out` como se segue:

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

## Comunicar preferências de consentimento por meio do padrão TCF do IAB

O SDK suporta o registro das preferências de consentimento de um usuário fornecidas por meio do padrão da Estrutura de transparência e consentimento (TCF) do Interative Advertising Bureau Europe (IAB). A cadeia de consentimento pode ser definida por meio da mesma `setConsent` comando como acima, desta forma:

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

Quando o consentimento é definido dessa forma, o Perfil do cliente em tempo real é atualizado com as informações de consentimento. Para que isso funcione, o esquema XDM do perfil precisa conter a variável [Grupo de campos Privacidade do perfil](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/profile/profile-privacy.schema.md). Ao enviar eventos, as informações de consentimento do IAB precisam ser adicionadas manualmente ao objeto XDM do evento. O SDK não inclui automaticamente as informações de consentimento nos eventos. Para enviar as informações de consentimento nos eventos, a variável [Grupo de campos Privacidade do evento de experiência](https://github.com/adobe/xdm/blob/master/docs/reference/mixins/experience-event/experienceevent-privacy.schema.md) precisa ser adicionado ao schema do Evento de experiência.

## Enviar vários padrões em uma solicitação

O SDK também oferece suporte ao envio de mais de um objeto de consentimento em uma solicitação.

```javascript
alloy("setConsent", {
    consent: [{
      standard: "Adobe",
      version: "2.0",
      value: {
        collect: {
          val: "y"
        },
        metadata: {
          time: "2021-03-17T15:48:42-07:00"
        }
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

Depois de comunicar as preferências do usuário ao SDK usando o `setConsent` , o SDK mantém as preferências do usuário para um cookie. Na próxima vez que o usuário carregar seu site no navegador, o SDK recuperará e usará essas preferências persistentes para determinar se os eventos podem ou não ser enviados para o Adobe.

Você precisará armazenar as preferências do usuário de maneira independente para mostrar a caixa de diálogo de consentimento com as preferências atuais. Não há como recuperar as preferências do usuário do SDK. Para garantir que as preferências do usuário permaneçam sincronizadas com o SDK, você pode chamar a função `setConsent` em cada carregamento de página. O SDK só fará uma chamada de servidor se as preferências tiverem sido alteradas.

## Sincronização de identidades ao definir o consentimento

Quando o consentimento padrão estiver pendente ou suspenso, a variável `setConsent` pode ser o primeiro pedido que sai e estabelece identidade. Por causa disso, pode ser importante sincronizar identidades na primeira solicitação. O mapa de identidade pode ser adicionado a `setConsent` como no `sendEvent` comando. Consulte [Recuperar Experience Cloud ID](../identity/overview.md)
