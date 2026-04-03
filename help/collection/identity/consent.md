---
title: Consentimento e identidade na coleção de dados
description: Entenda como as escolhas de consentimento afetam o comportamento de identidade em implementações do Web SDK, incluindo a geração de ECID, a persistência de cookies e a continuidade de visitantes.
source-git-commit: 696e5098ebf556bfc0fa4fc22ff637cb0835eee0
workflow-type: tm+mt
source-wordcount: '1149'
ht-degree: 2%

---

# Consentimento e identidade na coleção de dados

O consentimento e a identidade estão intimamente conectados em implementações do Web SDK. Como e quando você coleta o consentimento afeta diretamente quando e se o Web SDK gera uma ECID, define cookies de identidade e envia dados para a Edge Network. Quando o consentimento não é tratado com cuidado, o resultado geralmente é uma inflação inesperada de visitantes, lacunas na continuidade da identidade ou ambos.

Esta página explica como as opções de consentimento interagem com o comportamento da identidade e fornece orientação para configurar sua implementação a fim de evitar armadilhas comuns. Para obter informações sobre como o Web SDK lida com ECIDs, FPIDs e outros sinais de identidade, consulte [Identidade na Coleção de Dados](./overview.md).

## Como o consentimento afeta a identidade {#how-consent-affects-identity}

O Web SDK usa a variável de configuração [`defaultConsent`](/help/collection/js/commands/configure/defaultconsent.md) e o comando [`setConsent`](/help/collection/js/commands/setconsent.md) para controlar se envia dados para o Edge Network. O status de consentimento determina diretamente quando uma ECID é gerada e quando os cookies de identidade são definidos.

A tabela a seguir mostra o efeito combinado de `defaultConsent` e `setConsent` na coleta de dados, configuração de cookie e comportamento de identidade.

| `defaultConsent` | `setConsent` | Ocorre a coleta de dados | Cookies de navegador definidos | Comportamento de identidade |
| --- | --- | --- | --- | --- |
| `in` | Não definido | Sim | Sim | Uma ECID é gerada imediatamente na primeira solicitação. Os cookies de identidade são definidos no carregamento da página. |
| `in` | `in` | Sim | Sim | A ECID existente do visitante é preservada. O comportamento de identidade é inalterado. |
| `in` | `out` | Não | Sim | A coleta de dados é interrompida. Os cookies de identidade da ECID e do `kndctr_` existentes permanecem no navegador até que expirem. |
| `pending` | Não definido | Não | Não | Nenhuma ECID é gerada. Não há cookies definidos. Eventos são enfileirados localmente até que `setConsent` seja chamado. |
| `pending` | `in` | Sim | Sim | Os eventos em fila são enviados. Uma ECID é gerada na primeira solicitação e os cookies de identidade são definidos. |
| `pending` | `out` | Não | Sim | Os eventos em fila são descartados. Nenhuma ECID é gerada. O cookie de consentimento é definido para registrar a preferência do visitante. |
| `out` | Não definido | Não | Não | Nenhuma ECID é gerada. Não há cookies definidos. Nenhum evento é enviado. |
| `out` | `in` | Sim | Sim | Uma ECID é gerada na primeira solicitação e os cookies de identidade são definidos. |
| `out` | `out` | Não | Sim | Nenhuma ECID é gerada. O cookie de consentimento é definido para registrar a preferência do visitante. |

>[!NOTE]
>
>Os cookies de identidade e consentimento são definidos mesmo quando um visitante opta por não participar. Esses cookies são necessários para honrar as preferências de coleção de dados do visitante. Consulte [Cookies do Web SDK](https://experienceleague.adobe.com/pt-br/docs/core-services/interface/data-collection/cookies/web-sdk) para obter uma lista completa de cookies que o Web SDK define.

Quando um visitante consente novamente depois de revogá-lo anteriormente (chamando `setConsent` com `"general": "in"` após `"general": "out"`), o Web SDK retoma o envio de eventos e usa a ECID existente do cookie, se ela não tiver expirado. A identidade do visitante é preservada.

Depois que um visitante concede ou nega o consentimento, o Web SDK persiste sua preferência em um cookie de consentimento `kndctr_`. Em carregamentos de páginas subsequentes, o SDK lê esse cookie e aplica a preferência armazenada automaticamente. Você não precisa chamar `setConsent` novamente, a menos que a preferência do visitante seja alterada. Observe que o valor de configuração `defaultConsent` não persiste entre os carregamentos de página, mas o consentimento resolvido do visitante (definido por meio de `setConsent`) persiste.

>[!NOTE]
>
>Eventos enfileirados enquanto o consentimento é `pending` são mantidos na memória e não sobrevivem aos recarregamentos de página. Se um visitante navegar para uma nova página antes do consentimento ser resolvido, os eventos em fila da página anterior serão perdidos.

## Padrões de implementação {#implementation-patterns}

### Modelo de Opt-in (consentimento necessário antes da coleta) {#opt-in}

Use esse padrão quando as regulamentações (como o GDPR) exigirem consentimento explícito antes de coletar quaisquer dados.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "pending"
});

// When the visitor grants consent:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "in" }
  }]
});
```

Com este padrão:
* Nenhuma ECID é gerada até que o consentimento seja concedido.
* Eventos acionados antes do consentimento (como a exibição de página inicial) são enfileirados e enviados após o consentimento ser concedido.
* Os cookies de identidade são definidos somente após a primeira solicitação bem-sucedida do Edge Network.

### Modelo de recusa (coleção por padrão, parada na negação) {#opt-out}

Use esse padrão quando os regulamentos permitirem a coleta de dados por padrão com uma opção de recusa.

```js
alloy("configure", {
  orgId: "YOUR_ORG_ID@AdobeOrg",
  edgeDomain: "data.example.com",
  defaultConsent: "in"
});

// If the visitor opts out:
alloy("setConsent", {
  consent: [{
    standard: "Adobe",
    version: "1.0",
    value: { general: "out" }
  }]
});
```

Com este padrão:
* Uma ECID é gerada imediatamente no primeiro carregamento da página.
* Todos os eventos são enviados até que o visitante opte por não participar.
* Após a recusa, o Web SDK interrompe o envio de eventos, mas os cookies existentes permanecem.

## Consentimento com IDs de dispositivo primário {#consent-with-fpids}

Se sua implementação usa [IDs de dispositivo próprio (FPIDs)](./fpid.md), o cookie FPID é definido pelo seu servidor independentemente do estado de consentimento do Web SDK. O cookie FPID é um identificador que você gerencia em sua própria infraestrutura. No entanto, o FPID só é enviado para o Edge Network quando o Web SDK faz uma solicitação (que é fechada por consentimento):

* Com `defaultConsent: "pending"`, o FPID existe no navegador, mas não é usado para propagar uma ECID até que o consentimento seja concedido.
* Com `defaultConsent: "in"`, o FPID é usado na primeira solicitação e propaga a ECID imediatamente.

Se sua implementação de consentimento exigir que nenhum identificador seja definido antes do consentimento, atrase a definição do cookie FPID até que o consentimento seja comunicado. A marcação de consentimento do Web SDK sozinha não impede que o cookie FPID seja definido, pois ele é gerenciado pelo seu servidor.

## Armadilhas comuns {#common-pitfalls}

+++**O banner de consentimento apaga os cookies de identidade**

**Problema**: Algumas CMPs (plataformas de gerenciamento de consentimento) limpam todos os cookies, incluindo os `kndctr_` cookies de identidade, ao apresentar o banner de consentimento, antes que o visitante faça uma escolha. Quando o visitante consente, o Web SDK gera uma nova ECID porque a anterior foi excluída. O visitante aparece como uma nova pessoa nos relatórios.

**Sintomas**:
* Um pico na contagem de visitantes únicos após implantar um banner de consentimento.
* Os visitantes recorrentes são contados como novos visitantes sempre que o consentimento expira e interagem com o banner novamente.

**Solução**: configure seu CMP para preservar os cookies do `kndctr_`. Esses cookies são cookies de identidade, não cookies de rastreamento. Eles identificam o dispositivo e não contêm dados comportamentais. Se o CMP exigir a limpeza de cookies, adicione `kndctr_` cookies prefixados a uma lista de exclusão. Como alternativa, atrase a limpeza dos cookies até que o visitante negue explicitamente o consentimento, em vez de limpá-los antecipadamente.

+++

+++**O consentimento atrasado causa identidade duplicada**

**Problema**: quando `defaultConsent` está definido como `pending`, o Web SDK aguarda por consentimento antes de enviar quaisquer dados. Se o consentimento for concedido no final do ciclo de vida da página (por exemplo, após uma interação com banner que aciona um recarregamento de página), a seguinte sequência poderá causar problemas:

1. Carregamentos de página. `defaultConsent: "pending"`. O Web SDK não envia solicitações.
2. O visitante consente. O CMP aciona um recarregamento de página.
3. A página é carregada novamente. O Web SDK é inicializado com consentimento agora concedido e gera uma ECID.

Esse fluxo é normal e funciona corretamente. O problema ocorre quando o CMP ou sua implementação limpa inadvertidamente os cookies entre as etapas 2 e 3, ou quando o Web SDK é configurado de forma diferente na recarga.

**Solução**: verifique se a configuração do Web SDK (especialmente `orgId` e `defaultConsent`) é idêntica em todos os carregamentos de página. Se o CMP acionar um recarregamento após o consentimento, verifique se os cookies de identidade sobrevivem ao recarregamento.

+++

+++**Usando `defaultConsent: "in"` com um banner de consentimento**

**Problema**: Algumas implementações definem `defaultConsent: "in"` e chamam `setConsent` com `"general": "out"` se o visitante recusar. Essa abordagem gera uma ECID e envia pelo menos uma solicitação antes que o consentimento seja negado. Dependendo dos seus requisitos normativos, essa coleta de dados inicial pode não se alinhar à política de privacidade da sua organização.

**Solução**: se seu ambiente regulatório requer consentimento antes de qualquer coleta de dados ou geração de ECID, use `defaultConsent: "pending"`. Essa configuração garante que o Web SDK não se comunique com a Edge Network até que o consentimento seja explicitamente concedido.

+++
