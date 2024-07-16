---
title: defaultConsent
description: Defina o método de coleta de consentimento padrão para a propriedade da Web.
exl-id: 2a22fa8b-a234-4d3e-9b55-c7482a928fe6
source-git-commit: d3591053939147589dae24e1e4c20d53b1f87dd3
workflow-type: tm+mt
source-wordcount: '799'
ht-degree: 5%

---


# `defaultConsent`

A propriedade `defaultConsent` determina como você lida com o consentimento da coleta de dados antes de chamar o comando [`setConsent`](../setconsent.md). Essa propriedade é importante quando você não deseja coletar dados acidentalmente de indivíduos que residem em áreas onde o consentimento é necessário antes de coletar dados.

Por padrão, os usuários optam por todas as finalidades e o SDK da Web pode executar as seguintes tarefas:

* Enviar dados para e de servidores do Adobe.
* Ler e gravar cookies ou itens de armazenamento na Web.

Se os usuários recusarem todas as finalidades, o SDK da Web não executará nenhuma dessas tarefas.

A propriedade `defaultConsent` dá suporte a três valores:

* **`in`**: a coleta de dados continua normalmente, até que o usuário opte por não participar.
* **`out`**: os dados são descartados permanentemente até que o usuário opte por entrar.
* **`pending`**: os dados são armazenados localmente até que o usuário opte por usar o comando [`setConsent`](../setconsent.md). Quando o consentimento padrão para fins gerais é definido como `pending`, tentar executar qualquer comando que dependa das preferências de aceitação do usuário (por exemplo, o comando [`sendEvent`](../sendevent/overview.md)) resultará no comando sendo enfileirado no SDK da Web. Os comandos em fila não são processados até que você comunique as preferências de aceitação do usuário ao SDK da Web.

>[!NOTE]
>
> Os dados de consentimento não persistem entre os carregamentos de página.

Se você tiver um visitante que não esteja na jurisdição do Regulamento Geral sobre a Proteção de Dados (GDPR), o consentimento padrão poderá ser definido como `in`. Os visitantes dentro da jurisdição do GDPR podem ter seu consentimento padrão definido como `pending`. Sua Plataforma de Gerenciamento de Consentimento (CMP) pode detectar a região do cliente e fornecer o sinalizador `gdprApplies` para a TCF 2.0 do IAB. Esse sinalizador pode ser usado para definir o consentimento padrão.

Se você não quiser coletar eventos que ocorreram antes das preferências de aceitação do usuário serem definidas, passe `"defaultConsent": "out"` durante a configuração do SDK da Web. Tentar executar qualquer comando que dependa das preferências de aceitação do usuário não terá efeito até que você comunique as preferências de aceitação do usuário ao SDK da Web.

>[!NOTE]
>
>Atualmente, o SDK da Web oferece suporte apenas a um único recurso do tipo &quot;tudo ou nada&quot;. Embora planejemos criar um conjunto mais robusto de finalidades ou categorias que corresponderão aos diferentes recursos de Adobe e ofertas de produtos, a implementação atual é uma abordagem do tipo &quot;tudo ou nada&quot; para a aceitação.  Isso se aplica somente a [!DNL Web SDK] e NÃO a outras bibliotecas JavaScript do Adobe.

## Usando `defaultConsent` junto com `setConsent` {#using-consent}

O SDK da Web oferece dois comandos complementares de configuração de consentimento:

* [`defaultConsent`](defaultconsent.md): este comando destina-se a capturar as preferências de consentimento dos clientes do Adobe que usam o SDK da Web.
* [`setConsent`](../setconsent.md): este comando tem como objetivo capturar as preferências de consentimento dos visitantes do site.

Quando usadas juntas, essas configurações podem levar a diferentes resultados de coleta de dados e configuração de cookie, dependendo de seus valores configurados.

Consulte a tabela abaixo para entender quando ocorre a coleta de dados e quando os cookies são definidos, com base nas configurações de consentimento.

| defaultConsent | setConsent | Ocorre a coleta de dados | O SDK da Web define cookies do navegador |
|---------|----------|---------|---------|
| `in` | `in` | Sim | Sim |
| `in` | `out` | Não | Sim |
| `in` | Não definido | Sim | Sim |
| `pending` | `in` | Sim | Sim |
| `pending` | `out` | Não | Sim |
| `pending` | Não definido | Não | Não |
| `out` | `in` | Sim | Sim |
| `out` | `out` | Não | Sim |
| `out` | Não definido | Não | Não |

Os seguintes cookies são definidos quando a configuração de consentimento permite:

| Nome | Idade máxima | Descrição |
|---|---|---|
| **AMCV_###@AdobeOrg** | 34128000 (395 dias) | Presente quando [`idMigrationEnabled`](../configure/idmigrationenabled.md) estiver habilitado. Ajuda na transição para o SDK da Web enquanto algumas partes do site ainda usam o `visitor.js`. |
| **Cookie Demdex** | 15552000 (180 dias) | Apresentar se a sincronização de ID estiver habilitada. O Audience Manager define este cookie para atribuir um identificador exclusivo a um visitante do site. O cookie demdex ajuda o Audience Manager a executar funções básicas, como a identificação do visitante, a sincronização de ID, a segmentação, a modelagem, a geração de relatórios etc. |
| **kndctr_orgid_cluster** | 1800 (30 minutos) | Armazena a região do Edge Network que atende às solicitações do usuário atual. A região é usada no caminho do URL para que o Edge Network possa rotear a solicitação para a região correta. Se um usuário se conectar com um endereço IP diferente ou em uma sessão diferente, a solicitação será roteada novamente para a região mais próxima. |
| **kndct_orgid_identity** | 34128000 (395 dias) | Armazena a ECID, bem como outras informações relacionadas à ECID. |
| **kndctr_orgid_consent** | 15552000 (180 dias) | Armazena a preferência de consentimento dos usuários para o site. |
| **s_ecid** | 63115200 (2 anos) | Contém uma cópia da ID de Experience Cloud ([!DNL ECID]) ou MID. A MID é armazenada em um par de valores chave que segue a sintaxe `s_ecid=MCMID\|<ECID>`. |

## Definir o consentimento padrão usando a extensão de tag do SDK da Web

Selecione o botão de opção desejado em **[!UICONTROL Consentimento padrão]** ao [configurar a extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Coleção de dados]** > **[!UICONTROL Marcas]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e clique em **[!UICONTROL Configurar]** no cartão [!UICONTROL Adobe Experience Platform Web SDK].
1. Role para baixo até a seção [!UICONTROL Privacidade] e selecione o **[!UICONTROL Consentimento padrão]** desejado.
1. Clique em **[!UICONTROL Salvar]** e publique suas alterações.

## Definir o consentimento padrão usando a biblioteca JavaScript do SDK da Web

Defina a propriedade da cadeia de caracteres `defaultConsent` com o nível de consentimento desejado ao executar o comando `configure`. Esta propriedade diferencia maiúsculas e minúsculas e oferece suporte apenas aos três valores a seguir: `"in"`, `"out"` e `"pending"`. Se você tentar usar qualquer outro valor, a biblioteca emitirá um erro.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
