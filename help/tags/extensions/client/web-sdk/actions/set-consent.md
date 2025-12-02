---
title: Definir consentimento
description: Define o consentimento desejado para o visitante.
source-git-commit: 8dd658c46fc92ae6d450213ab79f2766f4211c53
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 0%

---

# Definir consentimento

A ação **[!UICONTROL Set consent]** determina se a extensão de tag deve enviar dados (aceitação), descartar dados (recusa) ou usar [consentimento padrão](../configure/consent.md) (consentimento desconhecido). Quando um usuário permite ou nega o consentimento em seu site, você pode usar essa ação para sincronizar suas preferências com a extensão de tag. O equivalente dessa ação na biblioteca JavaScript é o comando [`setConsent`](/help/collection/js/commands/setconsent.md).

1. Faça logon em [experience.adobe.com](https://experience.adobe.com) usando suas credenciais da Adobe ID.
1. Navegue até **[!UICONTROL Data Collection]** > **[!UICONTROL Tags]**.
1. Selecione a propriedade de tag desejada.
1. Navegue até **[!UICONTROL Rules]** e selecione a regra desejada.
1. Em [!UICONTROL Actions], selecione uma ação existente ou crie uma ação.
1. Defina o campo suspenso [!UICONTROL Extension] como **[!UICONTROL Adobe Experience Platform Web SDK]** e defina [!UICONTROL Action type] como **[!UICONTROL Set consent]**.

A extensão de tag é compatível com os seguintes padrões:

* **[Padrão do Adobe](/help/landing/governance-privacy-security/consent/adobe/overview.md)**: os padrões 1.0 e 2.0 são compatíveis.
* **[Estrutura de transparência e consentimento do IAB](/help/landing/governance-privacy-security/consent/iab/overview.md)**: se você usar esse padrão, o Perfil de cliente em tempo real do visitante será atualizado com as informações de consentimento se a implementação estiver configurada corretamente:
   1. O esquema de perfil individual XDM contém o [Grupo de campos de Consentimento do TCF 2.0 do IAB](/help/xdm/field-groups/profile/iab.md).
   1. O esquema do Evento de experiência contém o [Grupo de campos de Consentimento da TCF 2.0 do IAB](/help/xdm/field-groups/event/iab.md).

A Adobe recomenda armazenar qualquer preferência de caixa de diálogo de consentimento separadamente, como em um elemento de dados. A extensão de tag não oferece uma maneira de recuperar o consentimento. Para garantir que as preferências do usuário permaneçam sincronizadas com a extensão de tag, é possível executar essa ação em cada carregamento de página.

## Campos disponíveis

Esse tipo de ação oferece suporte às seguintes opções de configuração:

* **[!UICONTROL Instance]**: a instância do SDK à qual a ação se aplica. Esse menu suspenso estará desativado se sua implementação usar uma única instância do SDK.
* **[!UICONTROL Identity map]**: um elemento de dados que controla como uma ECID é gerada e a quais IDs as informações de consentimento estão vinculadas.
* **[!UICONTROL Consent information]**: determina se você deseja preencher um formulário ou fornecer um elemento de dados contendo informações de consentimento.
* **[!UICONTROL Standard]**: o padrão de consentimento que você deseja usar. As opções disponíveis incluem &#39;[!UICONTROL Adobe]&#39; e &#39;[!UICONTROL IAB TCF]&#39;.
* **[!UICONTROL Version]**: a versão do padrão de consentimento que você deseja usar.
* **[!UICONTROL Datastream configuration overrides]**: Esse comando oferece suporte a substituições de configuração de sequência de dados, fornecendo controle sobre quais aplicativos e serviços recebem esses dados. Ao definir uma substituição da configuração do fluxo de dados em um comando individual e nas configurações da extensão de tag, o comando individual tem prioridade. Consulte [Substituições da configuração da sequência de dados](../configure/configuration-overrides.md) para obter mais informações.

## Criação de uma regra que atualize as informações de consentimento

O momento ideal para usar essa ação é quando as preferências de consentimento de um cliente foram alteradas. É possível criar uma regra de tag para acompanhar essa alteração.

1. Em uma propriedade de marca, navegue até **[!UICONTROL Rules]** e selecione **[!UICONTROL Add rule]**.
1. Dê um nome desejado à regra e selecione o ícone &#39;`+`&#39; ao lado de **[!UICONTROL Events]**.
1. Defina as seguintes propriedades à esquerda:
   * **[!UICONTROL Extension]**: [!UICONTROL Core]
   * **[!UICONTROL EVent type]**: [!UICONTROL Custom code]
1. Abra o editor à direita e use o seguinte código como modelo:

```javascript
// Wait for window.__tcfapi to be defined, then trigger when the customer has completed their consent and preferences.
function addEventListener() {
  if (window.__tcfapi) {
    window.__tcfapi("addEventListener", 2, function (tcData, success) {
      if (success && tcData.eventStatus === "useractioncomplete") {
        // save the tcData.tcString in a data element
        _satellite.setVar("IAB TCF Consent String", tcData.tcString);
        _satellite.setVar("IAB TCF Consent GDPR", tcData.gdprApplies);
        trigger();
      }
    });
  } else {
    // window.__tcfapi wasn't defined. Check again in 100 milliseconds
    setTimeout(addEventListener, 100);
  }
}
addEventListener();
```

1. Selecione **[!UICONTROL Keep changes]**.

O bloco de código personalizado acima faz duas coisas:

* Aciona a regra quando as preferências de consentimento foram alteradas.
* Define dois elementos de dados: **Cadeia de Consentimento da TCF do IAB** e **GDPR de Consentimento da TCF do IAB**.

Estes elementos de dados são úteis ao definir a ação &#39;[!UICONTROL Set Consent]&#39;:

1. Selecione o ícone &#39;`+`&#39; ao lado de **[!UICONTROL Actions]**.
1. Defina as seguintes propriedades à esquerda:
   * **[!UICONTROL Extension]**: [!UICONTROL Adobe Experience Platform Web SDK]
   * **[!UICONTROL Action type]**: [!UICONTROL Set consent]
1. Defina as seguintes propriedades à direita:
   * **[!UICONTROL Standard]**: [!UICONTROL IAB TCF]
   * **[!UICONTROL Version]**: [!UICONTROL 2.0]
   * **[!UICONTROL Value]**: `%IAB TCF Consent String%`
   * **[!UICONTROL Does GDPR apply to this consent value]**: [!UICONTROL Provide a data element], com o valor `%IAB TCF Consent GDPR%`

![Ação de consentimento de definição de IAB](../assets/iab-action.png)

>[!NOTE]
>
>Não é possível escolher esses elementos de dados usando o seletor de elementos de dados porque eles foram criados por meio de código personalizado. Você deve digitar o nome do elemento de dados com os sinais de porcentagem.
