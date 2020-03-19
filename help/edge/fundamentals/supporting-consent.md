---
title: Consentimento de suporte
seo-title: Preferência de consentimento do SDK da Web do Adobe Experience Platform
description: Saiba como oferecer suporte às preferências de consentimento com o Experience Platform Web SDK
seo-description: Saiba como oferecer suporte às preferências de consentimento com o Experience Platform Web SDK
translation-type: tm+mt
source-git-commit: 0cc6e233646134be073d20e2acd1702d345ff35f

---


# (Beta) Consentimento de suporte

>[!IMPORTANT]
>
>O SDK da Web da plataforma Adobe Experience está atualmente em beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Para respeitar a privacidade do usuário, você pode solicitar o consentimento do usuário antes de permitir que o SDK use dados específicos do usuário para determinados fins. Atualmente, o SDK permite que os usuários aceitem ou recusem todos os fins, mas no futuro a Adobe espera fornecer um controle mais detalhado sobre fins específicos.

Se o usuário optar por todos os fins, o SDK poderá executar as seguintes tarefas:

* Envie dados de e para os servidores da Adobe.
* Ler e gravar cookies ou itens de armazenamento da Web (exceto por persistir nas preferências de aceitação do usuário).

Se o usuário optar por não participar de todas as finalidades, o SDK não executará nenhuma dessas tarefas.

## Configurando o consentimento

Por padrão, o usuário é aceito para todos os fins. Para impedir que o SDK execute as tarefas acima até que o usuário opte por participar, passe `"defaultConsent": { "general": "pending" }` durante a configuração do SDK da seguinte maneira:

```javascript
alloy("configure", {
  "configId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "imsOrgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": { "general": "pending" }
});
```

Quando o consentimento padrão para a finalidade geral está definido como pendente, tentar executar quaisquer comandos que dependam das preferências de aceitação do usuário (por exemplo, o `event` comando) resulta na fila do comando no SDK. Esses comandos não são processados até que você comunique as preferências de aceitação do usuário ao SDK.

Nesse ponto, talvez você prefira pedir ao usuário para aceitar em algum lugar na interface do usuário. Após a coleta das preferências do usuário, comunique-as ao SDK.

## Comunicar preferências de consentimento

Se o usuário optar por participar, execute o `setConsent` comando com a `general` opção definida como `in` :

```javascript
alloy("setConsent", {
  "general": "in"
});
```

Como o usuário agora aceitou, o SDK executa todos os comandos previamente na fila. Os comandos futuros que dependem do usuário optar por não __ serão colocados na fila e, em vez disso, serão executados prontamente.

Se o usuário optar por recusar, execute o `setConsent` comando com a `general` opção definida como `out` :

```javascript
alloy("setConsent", {
  "general": "out"
});
```

>[!NOTE]
>
>Depois que um usuário rejeitar, o SDK não permitirá que você defina o consentimento dos usuários para `in`.

Como o usuário optou por recusar, as promessas que foram retornadas de comandos previamente enfileirados são rejeitadas. Comandos futuros que dependem do usuário optar retornarão promessas que são rejeitadas da mesma forma. Para obter mais informações sobre como manipular ou suprimir erros, consulte [Executando comandos](executing-commands.md).

>[!NOTE]
>
>Atualmente, o SDK suporta apenas a `general` finalidade. Embora planejemos criar um conjunto mais robusto de objetivos ou categorias que corresponderão aos diferentes recursos e ofertas de produtos da Adobe, a implementação atual é uma abordagem de aceitação total ou parcial.  Isso se aplica somente ao SDK da Web da plataforma Adobe Experience e NÃO a outras bibliotecas do Adobe JavaScript.

## Persistência das preferências de consentimento

Depois de comunicar as preferências do usuário ao SDK usando o `setConsent` comando, o SDK persiste as preferências do usuário para um cookie. Na próxima vez que o usuário carregar seu site no navegador, o SDK recuperará e usará essas preferências persistentes. Não há necessidade de executar o `setConsent` comando novamente, exceto para comunicar uma alteração nas preferências do usuário, que pode ser feita a qualquer momento.