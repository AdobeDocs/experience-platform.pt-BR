---
title: Consentimento de suporte
seo-title: Preferência de consentimento do SDK da Web para Adobe Experience Platform
description: Saiba como suportar preferências de consentimento com o SDK da Web do Experience Platform
seo-description: Saiba como suportar preferências de consentimento com o SDK da Web do Experience Platform
translation-type: tm+mt
source-git-commit: 7b07a974e29334cde2dee7027b9780a296db7b20
workflow-type: tm+mt
source-wordcount: '516'
ht-degree: 0%

---


# Consentimento de suporte

Para respeitar a privacidade do usuário, você pode solicitar o consentimento do usuário antes de permitir que o SDK use dados específicos do usuário para determinados fins. Atualmente, o SDK permite que os usuários opt in ou saiam de todas as finalidades, mas no futuro a Adobe espera fornecer um controle mais detalhado sobre finalidades específicas.

Se o usuário opt in para todos os fins, o SDK poderá executar as seguintes tarefas:

* Envie dados de e para os servidores da Adobe.
* Ler e gravar cookies ou itens de armazenamento da Web (exceto por persistir nas preferências de aceitação do usuário).

Se o usuário opt out de todas as finalidades, o SDK não executará nenhuma dessas tarefas.

## Configurando o consentimento

Por padrão, o usuário é opt in para todos os fins. Para impedir que o SDK execute as tarefas acima até que o usuário opt in, passe `"defaultConsent": { "general": "pending" }` durante a configuração do SDK da seguinte maneira:

```javascript
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

Quando o consentimento padrão para a finalidade geral está definido como pendente, tentar executar quaisquer comandos que dependam das preferências de aceitação do usuário (por exemplo, o `event` comando) resulta na fila do comando no SDK. Esses comandos não são processados até que você comunique as preferências de aceitação do usuário ao SDK.

Nesse ponto, talvez você prefira pedir ao usuário para opt in em algum lugar na interface do usuário. Após a coleta das preferências do usuário, comunique-as ao SDK.

## Comunicar preferências de consentimento

Se o usuário opt in, execute o `setConsent` comando com a `general` opção definida como `in` :

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

Como o usuário agora opt in, o SDK executa todos os comandos previamente enfileirados. Os comandos futuros que dependem da opt in do usuário _não_ serão colocados na fila e, em vez disso, serão executados prontamente.

Se o usuário optar por opt out, execute o `setConsent` comando com a `general` opção definida como `out` :

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
>Depois que um usuário opt out, o SDK não permitirá que você defina o consentimento dos usuários para `in`.

Como o usuário optou por opt out, as promessas que foram retornadas de comandos previamente enfileirados são rejeitadas. Comandos futuros que dependem da opt in do usuário retornarão promessas que são igualmente rejeitadas. Para obter mais informações sobre como manipular ou suprimir erros, consulte [Executando comandos](executing-commands.md).

>[!NOTE]
>
>Atualmente, o SDK suporta apenas a `general` finalidade. Embora planejemos criar um conjunto mais robusto de propósitos ou categorias que corresponderão aos diferentes recursos e ofertas de produtos da Adobe, a implementação atual é uma abordagem de aceitação total ou parcial.  Isso se aplica somente ao Adobe Experience Platform [!DNL Web SDK] e NÃO a outras bibliotecas do Adobe JavaScript.

## Persistência das preferências de consentimento

Depois de comunicar as preferências do usuário ao SDK usando o `setConsent` comando, o SDK persiste as preferências do usuário para um cookie. Na próxima vez que o usuário carregar seu site no navegador, o SDK recuperará e usará essas preferências persistentes. Não há necessidade de executar o `setConsent` comando novamente, exceto para comunicar uma alteração nas preferências do usuário, que pode ser feita a qualquer momento.