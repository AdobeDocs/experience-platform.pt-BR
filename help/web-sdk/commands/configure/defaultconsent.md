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

A variável `defaultConsent` determina como você lida com o consentimento da coleta de dados antes de chamar a [`setConsent`](../setconsent.md) comando. Essa propriedade é importante quando você não deseja coletar dados acidentalmente de indivíduos que residem em áreas onde o consentimento é necessário antes de coletar dados.

Por padrão, os usuários optam por todas as finalidades e o SDK da Web pode executar as seguintes tarefas:

* Enviar dados para e de servidores do Adobe.
* Ler e gravar cookies ou itens de armazenamento na Web.

Se os usuários recusarem todas as finalidades, o SDK da Web não executará nenhuma dessas tarefas.

A variável `defaultConsent` A propriedade suporta três valores:

* **`in`**: a coleta de dados continua normalmente, até que o usuário opte por não participar.
* **`out`**: os dados são descartados permanentemente até que o usuário opte por entrar.
* **`pending`**: os dados são armazenados localmente até que o usuário opte por usar o [`setConsent`](../setconsent.md) comando. Quando o consentimento padrão para a finalidade geral é definido como `pending`, tentando executar qualquer comando que dependa das preferências de aceitação do usuário (por exemplo, o [`sendEvent`](../sendevent/overview.md) comando) faz com que o comando seja enfileirado no SDK da Web. Os comandos em fila não são processados até que você comunique as preferências de aceitação do usuário ao SDK da Web.

>[!NOTE]
>
> Os dados de consentimento não persistem entre os carregamentos de página.

Se você tiver um visitante que não esteja na jurisdição do Regulamento Geral sobre a Proteção de Dados (GDPR), o consentimento padrão poderá ser definido como `in`. Os visitantes dentro da jurisdição do GDPR podem ter seu consentimento padrão definido como `pending`. Sua Plataforma de gerenciamento de consentimento (CMP) pode detectar a região do cliente e fornecer o sinalizador `gdprApplies` para o IAB TCF 2.0. Esse sinalizador pode ser usado para definir o consentimento padrão.

Se não quiser coletar eventos que ocorreram antes da definição das preferências de aceitação do usuário, você pode enviar `"defaultConsent": "out"` durante a configuração do SDK da Web. Tentar executar qualquer comando que dependa das preferências de aceitação do usuário não terá efeito até que você comunique as preferências de aceitação do usuário ao SDK da Web.

>[!NOTE]
>
>Atualmente, o SDK da Web oferece suporte apenas a um único recurso do tipo &quot;tudo ou nada&quot;. Embora planejemos criar um conjunto mais robusto de finalidades ou categorias que corresponderão aos diferentes recursos de Adobe e ofertas de produtos, a implementação atual é uma abordagem do tipo &quot;tudo ou nada&quot; para a aceitação.  Isso só se aplica a [!DNL Web SDK] e NÃO outras bibliotecas JavaScript do Adobe.

## Usar `defaultConsent` juntamente com `setConsent` {#using-consent}

O SDK da Web oferece dois comandos complementares de configuração de consentimento:

* [`defaultConsent`](defaultconsent.md): este comando destina-se a capturar as preferências de consentimento dos clientes do Adobe que usam o SDK da Web.
* [`setConsent`](../setconsent.md): este comando destina-se a capturar as preferências de consentimento dos visitantes do site.

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
| **AMCV_###@AdobeOrg** | 34128000 (395 dias) | Apresentar quando [`idMigrationEnabled`](../configure/idmigrationenabled.md) está ativado. Ajuda na transição para o SDK da Web enquanto algumas partes do site ainda usam `visitor.js`. |
| **Cookie demdex** | 15552000 (180 dias) | Apresentar se a sincronização de ID estiver habilitada. O Audience Manager define este cookie para atribuir um identificador exclusivo a um visitante do site. O cookie demdex ajuda o Audience Manager a executar funções básicas, como a identificação do visitante, a sincronização de ID, a segmentação, a modelagem, a geração de relatórios etc. |
| **kndctr_orgid_cluster** | 1800 (30 minutos) | Armazena a região do Edge Network que atende às solicitações do usuário atual. A região é usada no caminho do URL para que o Edge Network possa rotear a solicitação para a região correta. Se um usuário se conectar com um endereço IP diferente ou em uma sessão diferente, a solicitação será roteada novamente para a região mais próxima. |
| **kndct_orgid_identity** | 34128000 (395 dias) | Armazena a ECID, bem como outras informações relacionadas à ECID. |
| **kndctr_orgid_consent** | 15552000 (180 dias) | Armazena a preferência de consentimento dos usuários para o site. |
| **s_ecid** | 63115200 (2 anos) | Contém uma cópia da ID do Experience Cloud ([!DNL ECID]) ou MID. A MID é armazenada em um par de valores chave que segue a sintaxe `s_ecid=MCMID\|<ECID>`. |

## Definir o consentimento padrão usando a extensão de tag do SDK da Web

Selecione o botão de opção desejado em **[!UICONTROL Consentimento padrão]** quando [configuração da extensão de tag](/help/tags/extensions/client/web-sdk/web-sdk-extension-configuration.md).

1. Efetue logon no [experience.adobe.com](https://experience.adobe.com) usando suas credenciais do Adobe ID.
1. Navegue até **[!UICONTROL Coleta de dados]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Extensões]** e, em seguida, clique em **[!UICONTROL Configurar]** no [!UICONTROL Adobe Experience Platform Web SDK] cartão.
1. Role para baixo até [!UICONTROL Privacidade] e selecione a opção desejada **[!UICONTROL Consentimento padrão]**.
1. Clique em **[!UICONTROL Salvar]** e, em seguida, publique as alterações.

## Definir o consentimento padrão usando a biblioteca JavaScript do SDK da Web

Defina o `defaultConsent` para o nível de consentimento desejado ao executar a variável `configure` comando. Essa propriedade diferencia maiúsculas e minúsculas e oferece suporte apenas aos três valores a seguir: `"in"`, `"out"`, e `"pending"`. Se você tentar usar qualquer outro valor, a biblioteca emitirá um erro.

```js
alloy("configure", {
  "edgeConfigId": "ebebf826-a01f-4458-8cec-ef61de241c93",
  "orgId": "ADB3LETTERSANDNUMBERS@AdobeOrg",
  "defaultConsent": "pending"
});
```
