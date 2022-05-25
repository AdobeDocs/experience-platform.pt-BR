---
keywords: Experience Platform; home; IAB; IAB 2.0; consentimento; Consentimento
solution: Experience Platform
title: Suporte ao IAB TCF 2.0 no Experience Platform
topic-legacy: privacy events
description: Saiba como configurar operações de dados e esquemas para transmitir opções de consentimento do cliente ao ativar segmentos para destinos no Adobe Experience Platform.
exl-id: af787adf-b46e-43cf-84ac-dfb0bc274025
source-git-commit: fb0d8aedbb88aad8ed65592e0b706bd17840406b
workflow-type: tm+mt
source-wordcount: '2563'
ht-degree: 1%

---

# Suporte ao IAB TCF 2.0 no Experience Platform

O [!DNL Transparency & Consent Framework] (TCF), conforme descrito pela [!DNL Interactive Advertising Bureau] (IAB), é um quadro técnico de padrão aberto destinado a permitir que as organizações obtenham, registrem e atualizem o consentimento do consumidor para o processamento dos seus dados pessoais, em conformidade com o [!DNL General Data Protection Regulation] (GDPR). A segunda iteração da estrutura, TCF 2.0, concede mais flexibilidade para como os consumidores podem fornecer ou reter consentimento, incluindo se e como os fornecedores podem usar determinados recursos de processamento de dados, como a geolocalização precisa.

>[!NOTE]
>
>Mais informações sobre o TCF 2.0 podem ser encontradas no [Site da IAB Europe](https://iabeurope.eu/tcf-2-0/), incluindo os materiais de apoio e as especificações técnicas.

O Adobe Experience Platform faz parte do [Lista de fornecedores do IAB TCF 2.0](https://iabeurope.eu/vendor-list-tcf-v2-0/), sob a ID **565**. Em conformidade com os requisitos do TCF 2.0, o Platform permite coletar dados de consentimento do cliente e integrá-los aos perfis de clientes armazenados. Esses dados de consentimento podem ser fatorado para determinar se os perfis estão incluídos em segmentos de público-alvo exportados, dependendo do caso de uso.

>[!IMPORTANT]
>
>A Platform só pode estar em conformidade com a versão 2.0 do TCF (ou posterior). As versões anteriores da TCF não são compatíveis.

Este documento fornece uma visão geral de como configurar as operações de dados e os esquemas de perfil para aceitar os dados de consentimento do cliente gerados pelo CMP e como a Platform transmite as opções de consentimento do usuário ao exportar segmentos.

## Pré-requisitos

Para seguir este guia, você deve usar uma Plataforma de gerenciamento de consentimento (CMP), comercial ou própria, integrada e compatível com a TCF do IAB. Consulte a [lista de CMPs compatíveis](https://iabeurope.eu/cmp-list/) para obter mais informações.

>[!IMPORTANT]
>
>Se a ID do CMP for inválida, a Platform continuará processando os dados como estão. Para aplicar o TCF 2.0, você deve confirmar que o CMP tem uma ID válida que foi registrada no IAB TCF 2.0 antes de enviar dados ao Platform.

Este guia também requer uma compreensão funcional dos seguintes serviços da plataforma:

* [Experience Data Model (XDM)](../../../../xdm/home.md): A estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
* [Serviço de identidade da Adobe Experience Platform](../../../../identity-service/home.md): Resolve o desafio fundamental colocado pela fragmentação dos dados de experiência do cliente ao unir identidades entre dispositivos e sistemas.
* [Perfil do cliente em tempo real](../../../../profile/home.md): Aproveitamento [!DNL Identity Service] para criar perfis detalhados do cliente a partir de seus conjuntos de dados em tempo real. [!DNL Real-time Customer Profile] extrai dados do Data Lake e mantém perfis de clientes em seu próprio armazenamento de dados separado.
* [Adobe Experience Platform Web SDK](../../../../edge/home.md): Uma biblioteca JavaScript do lado do cliente que permite integrar vários serviços da plataforma ao seu site voltado para o cliente.
   * [Comandos de consentimento do SDK](../../../../edge/consent/supporting-consent.md): Uma visão geral do caso de uso dos comandos SDK relacionados ao consentimento mostrados neste guia.
* [Serviço de segmentação do Adobe Experience Platform](../../../../segmentation/home.md): Permite dividir [!DNL Real-time Customer Profile] dados em grupos de indivíduos que compartilham características semelhantes e responderão de forma semelhante às estratégias de marketing.

Além dos serviços da plataforma listados acima, você também deve estar familiarizado com [destinos](../../../../data-governance/home.md) e seu papel no ecossistema da plataforma.

## Resumo do fluxo de consentimento do cliente {#summary}

As seções a seguir descrevem como os dados de consentimento são coletados e aplicados depois que o sistema é configurado corretamente.

### Coleta de dados de consentimento

A Platform permite coletar dados de consentimento do cliente por meio do seguinte processo:

1. Um cliente fornece suas preferências de consentimento para a coleta de dados por meio de uma caixa de diálogo no site.
1. O CMP detecta a alteração da preferência de consentimento e gera os dados de consentimento do TCF de acordo.
1. Usando o SDK da Web da plataforma, os dados de consentimento gerados (retornados pela CMP) são enviados para a Adobe Experience Platform.
1. Os dados de consentimento coletados são assimilados em um [!DNL Profile]Conjunto de dados habilitado para TCF cujo esquema contenha campos de consentimento da TCF.

Além dos comandos do SDK acionados por ganchos de alteração de consentimento da CMP, os dados de consentimento também podem fluir para o Experience Platform por meio de quaisquer dados XDM gerados pelo cliente que sejam carregados diretamente para um [!DNL Profile]Conjunto de dados habilitado para .

Qualquer segmento compartilhado com a plataforma pela Adobe Audience Manager (por meio da variável [!DNL Audience Manager] (conector de origem ou de outra forma) também pode conter dados de consentimento, desde que os campos apropriados tenham sido aplicados a esses segmentos por meio de [!DNL Experience Cloud Identity Service]. Para obter mais informações sobre como coletar dados de consentimento em [!DNL Audience Manager], consulte o documento no [Plug-in do Adobe Audience Manager para a TCF do IAB](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html?lang=pt-BR).

### Execução de consentimento a jusante

Depois que os dados de consentimento da TCF forem assimilados com êxito, os seguintes processos ocorrerão nos serviços downstream da plataforma:

1. [!DNL Real-time Customer Profile] atualiza os dados de consentimento armazenados para o perfil do cliente.
1. A Platform processa as IDs do cliente somente se a permissão do fornecedor para a Plataforma (565) for fornecida para cada ID em um cluster.
1. Ao exportar segmentos para destinos pertencentes aos membros da lista de fornecedores TCF 2.0, a Platform inclui apenas perfis se o fornecedor permitir ambas as plataformas (565) *e* o destino individual é fornecido para cada ID em um cluster.

O restante das seções neste documento fornecem orientação sobre como configurar a Platform e suas operações de dados para atender aos requisitos de coleta e aplicação descritos acima.

## Determine como gerar dados de consentimento do cliente em sua CMP {#consent-data}

Como cada sistema CMP é exclusivo, você deve determinar a melhor maneira de permitir que seus clientes forneçam consentimento à medida que interagirem com seu serviço. Uma maneira comum de fazer isso é usando uma caixa de diálogo de consentimento de cookie, semelhante ao seguinte exemplo:

![](../../../images/governance-privacy-security/consent/iab/overview/cmp-dialog.png)

Essa caixa de diálogo deve permitir que o cliente aceite ou saia do seguinte:

| Opção de consentimento | Descrição |
| --- | --- |
| **Finalidades** | Finalidades definem para quais finalidades de tecnologia de anúncios uma marca pode usar os dados de um cliente. As seguintes finalidades devem ser aceitas para que a Platform processe as IDs do cliente: <ul><li>**Finalidade 1**: Armazenar e/ou acessar informações em um dispositivo</li><li>**Finalidade 10**: Desenvolver e melhorar produtos</li></ul> |
| **Permissões do fornecedor** | Além de fins de tecnologia de anúncios, a caixa de diálogo também deve permitir que o cliente opte por aceitar ou não a utilização de seus dados por fornecedores específicos, incluindo a Adobe Experience Platform (565). |

### Sequências de consentimento {#consent-strings}

Independentemente do método usado para coletar os dados, o objetivo é gerar um valor de string com base nas opções de consentimento escolhidas pelo cliente, chamadas de string de consentimento.

Na especificação da TCF, as cadeias de consentimento são usadas para codificar detalhes relevantes sobre as configurações de consentimento de um cliente, em termos de finalidades de marketing específicas, conforme definido por políticas e fornecedores. A Platform usa essas cadeias de caracteres para armazenar as configurações de consentimento para cada cliente e, portanto, uma nova cadeia de consentimento deve ser gerada sempre que essas configurações forem alteradas.

As cadeias de caracteres de consentimento só podem ser criadas por uma CMP registrada junto à TCF do IAB. Para obter mais informações sobre como gerar cadeias de consentimento usando seu CMP específico, consulte o [guia de formatação da cadeia de consentimento](https://github.com/InteractiveAdvertisingBureau/GDPR-Transparency-and-Consent-Framework/blob/master/TCFv2/IAB%20Tech%20Lab%20-%20Consent%20string%20and%20vendor%20list%20formats%20v2.md) no repositório GitHub da TCF do IAB.

## Criar conjuntos de dados com campos de consentimento da TCF {#datasets}

Os dados de consentimento do cliente devem ser enviados para conjuntos de dados cujos esquemas contêm campos de consentimento da TCF. Consulte o tutorial em [criação de conjuntos de dados para capturar o consentimento do TCF 2.0](./dataset.md) para saber como criar o conjunto de dados de perfil necessário (e um conjunto de dados opcional do evento de experiência) antes de continuar com este guia.

## Atualizar [!DNL Profile] mesclar políticas para incluir dados de consentimento {#merge-policies}

Depois de criar uma [!DNL Profile]Conjunto de dados habilitado para coletar dados de consentimento, você deve garantir que suas políticas de mesclagem tenham sido configuradas para sempre incluir campos de consentimento TCF nos perfis do cliente. Isso envolve definir a precedência do conjunto de dados para que seu conjunto de dados de consentimento seja priorizado em relação a outros conjuntos de dados potencialmente conflitantes.

Para obter mais informações sobre como trabalhar com políticas de mesclagem, consulte [visão geral das políticas de mesclagem](../../../../profile/merge-policies/overview.md). Ao configurar suas políticas de mesclagem, você deve garantir que seus segmentos incluam todos os atributos de consentimento necessários fornecidos pela variável [Grupo de campos do esquema de privacidade XDM](./dataset.md#privacy-field-group), conforme descrito no guia sobre a preparação do conjunto de dados.

## Integre o SDK da Web do Experience Platform para coletar dados de consentimento do cliente {#sdk}

>[!NOTE]
>
>O uso do SDK da Web do Experience Platform é necessário para processar dados de consentimento diretamente no Adobe Experience Platform. [!DNL Experience Cloud Identity Service] no momento não é compatível.
>
>[!DNL Experience Cloud Identity Service] no entanto, o ainda é compatível com o processamento de consentimento no Adobe Audience Manager, e a conformidade com o TCF 2.0 requer apenas que a biblioteca seja atualizada para [versão 5.0](https://github.com/Adobe-Marketing-Cloud/id-service/releases).

Depois de configurar o CMP para gerar cadeias de consentimento, você deve integrar o SDK da Web do Experience Platform para coletar essas cadeias de caracteres e enviá-las para a Platform. O SDK da plataforma fornece dois comandos que podem ser usados para enviar dados de consentimento da TCF para a Plataforma (explicados nas subseções abaixo) e devem ser usados quando um cliente fornecer informações de consentimento pela primeira vez e a qualquer momento em que o consentimento for alterado posteriormente.

**O SDK não faz interface com nenhum CMP pronto para uso**. Cabe a você determinar como integrar o SDK ao seu site, acompanhar as alterações de consentimento no CMP e chamar o comando apropriado.

### Criar um novo armazenamento de dados

Para que o SDK envie dados para o Experience Platform, primeiro você deve criar um novo datastream para Platform na interface do usuário da coleta de dados. Etapas específicas para criar um novo conjunto de dados são fornecidas na seção [Documentação do SDK](../../../../edge/datastreams/overview.md).

Depois de fornecer um nome exclusivo para o armazenamento de dados, selecione o botão de alternância ao lado de **[!UICONTROL Adobe Experience Platform]**. Em seguida, use os seguintes valores para preencher o restante do formulário:

| Campo de fluxo de dados | Valor |
| --- | --- |
| [!UICONTROL Sandbox] | O nome da plataforma [sandbox](../../../../sandboxes/home.md) que contém a conexão de transmissão e os conjuntos de dados necessários para configurar o conjunto de dados. |
| [!UICONTROL Entrada de transmissão] | Uma conexão de transmissão válida para Experience Platform. Veja o tutorial em [criação de uma conexão de transmissão](../../../../ingestion/tutorials/create-streaming-connection-ui.md) se você não tiver uma entrada de transmissão existente. |
| [!UICONTROL Conjunto de dados do evento] | Selecione o [!DNL XDM ExperienceEvent] conjunto de dados criado na [etapa anterior](#datasets). Se você incluiu a variável [[!UICONTROL Consentimento do IAB TCF 2.0] grupo de campos](../../../../xdm/field-groups/event/iab.md) no esquema desse conjunto de dados, você pode rastrear eventos de alteração de consentimento ao longo do tempo usando o [`sendEvent`](#sendEvent) , armazenando esses dados nesse conjunto de dados. Lembre-se de que os valores de consentimento armazenados neste conjunto de dados são **not** usado em workflows de imposição automática. |
| [!UICONTROL Conjunto de dados de perfil] | Selecione o [!DNL XDM Individual Profile] conjunto de dados criado na [etapa anterior](#datasets). Ao responder aos ganchos de alteração de consentimento da CMP usando o [`setConsent`](#setConsent) , os dados coletados serão armazenados nesse conjunto de dados. Como esse conjunto de dados está habilitado para Perfil, os valores de consentimento armazenados nesse conjunto de dados são honrados durante os workflows de imposição automática. |

![](../../../images/governance-privacy-security/consent/iab/overview/edge-config.png)

Quando terminar, selecione **[!UICONTROL Salvar]** na parte inferior da tela e continue seguindo os prompts adicionais para concluir a configuração.

### Comandos de alteração de consentimento

Depois de criar o conjunto de dados descrito na seção anterior, você pode começar a usar comandos do SDK para enviar dados de consentimento para a Platform. As seções abaixo fornecem exemplos de como cada comando do SDK pode ser usado em diferentes cenários.

>[!NOTE]
>
>Para obter uma introdução à sintaxe comum para todos os comandos do SDK da plataforma, consulte o documento em [execução de comandos](../../../../edge/fundamentals/executing-commands.md).

#### Uso de ganchos de alteração de consentimento da CMP {#setConsent}

Muitas CMPs fornecem ganchos prontos para uso que ouvem eventos de alteração de consentimento. Quando esses eventos ocorrem, você pode usar a variável `setConsent` para atualizar os dados de consentimento desse cliente.

O `setConsent` O comando espera dois argumentos: (1) uma string que indica o tipo de comando (neste caso, &quot;setConsent&quot;) e (2) uma carga que contém uma `consent` , que deve conter pelo menos um objeto que forneça os campos de consentimento necessários, conforme mostrado abaixo:

```js
alloy("setConsent", {
  consent: [{
    standard: "IAB TCF",
    version: "2.0",
    value: "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
    gdprApplies: "true"
  }]
});
```

| Propriedade da carga útil | Descrição |
| --- | --- |
| `standard` | O padrão de consentimento que está sendo usado. Esse valor deve ser definido como `IAB` para processamento de consentimento do TCF 2.0. |
| `version` | O número da versão da norma de consentimento indicada em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento do TCF 2.0. |
| `value` | A cadeia de consentimento codificado em base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booleano que indica se o GDPR se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a este cliente, o valor deve ser definido como `true`. O padrão é `true` se não estiver definido. |

O `setConsent` deve ser usado como parte de um gancho do CMP que detecta alterações nas configurações de consentimento. O JavaScript a seguir fornece um exemplo de como a variável `setConsent` pode ser usado para `OnConsentChanged` gancho:

```js
OneTrust.OnConsentChanged(function () {
  // Retrieve the TCF 2.0 consent data generated by the CMP, and pass it to Alloy. 
  __tcfapi("getTCData", 2, function (data, success) {
    if (success) {
      var tcString = data.tcString;
      var gdpr = data.gdprApplies;

      alloy("setConsent", {
        consent: [{
          standard: "IAB TCF",
          version: "2.0",
          value: tcString,
          gdprApplies: gdpr
        }]
      });
    }
  });
});
```

#### Uso de eventos {#sendEvent}

Você também pode coletar dados de consentimento do TCF 2.0 em cada evento acionado na Platform usando a variável `sendEvent` comando.

>[!NOTE]
>
>Para usar esse método, você deve ter adicionado o grupo de campos Privacidade de eventos de experiência ao seu [!DNL Profile]-ativado [!DNL XDM ExperienceEvent] esquema. Consulte a seção sobre [atualização do schema ExperienceEvent](./dataset.md#event-schema) no guia de preparação do conjunto de dados para obter as etapas sobre como configurar isso.

O `sendEvent` deve ser usado como um retorno de chamada em ouvintes de eventos apropriados em seu site. O comando espera dois argumentos: (1) uma string que indica o tipo de comando (nesse caso, `sendEvent`) e (2) uma carga contendo um `xdm` objeto que fornece os campos de consentimento necessários como JSON:

```js
alloy("sendEvent", {
  xdm: {
    "consentStrings": [{
      "consentStandard": "IAB TCF",
      "consentStandardVersion": "2.0",
      "consentStringValue": "CLcVDxRMWfGmWAVAHCENAXCkAKDAADnAABRgA5mdfCKZuYJez-NQm0TBMYA4oCAAGQYIAAAAAAEAIAEgAA.argAC0gAAAAAAAAAAAA",
      "gdprApplies": true
    }]
  }
});
```

| Propriedade da carga útil | Descrição |
| --- | --- |
| `xdm.consentStrings` | Uma matriz que deve conter pelo menos um objeto que forneça os campos de consentimento necessários. |
| `consentStandard` | O padrão de consentimento que está sendo usado. Esse valor deve ser definido como `IAB` para processamento de consentimento do TCF 2.0. |
| `consentStandardVersion` | O número da versão da norma de consentimento indicada em `standard`. Esse valor deve ser definido como `2.0` para processamento de consentimento do TCF 2.0. |
| `consentStringValue` | A cadeia de consentimento codificado em base 64 gerada pelo CMP. |
| `gdprApplies` | Um valor booleano que indica se o GDPR se aplica ao cliente conectado no momento. Para que o TCF 2.0 seja aplicado a este cliente, o valor deve ser definido como `true`. O padrão é `true` se não estiver definido. |

### Tratamento de respostas do SDK

Todos [!DNL Platform SDK] comandos retornam promessas que indicam se a chamada foi bem-sucedida ou falhou. Em seguida, você pode usar essas respostas para obter uma lógica adicional, como exibir mensagens de confirmação para o cliente. Consulte a seção sobre [como lidar com sucesso ou falha](../../../../edge/fundamentals/executing-commands.md#handling-success-or-failure) no guia sobre como executar comandos do SDK para obter exemplos específicos.

## Exportar segmentos {#export}

>[!NOTE]
>
>Antes de começar a exportar segmentos, você deve garantir que seus segmentos incluam todos os campos de consentimento necessários. Consulte a seção sobre [configuração de políticas de mesclagem](#merge-policies) para obter mais informações.

Depois de coletar os dados de consentimento do cliente e criar segmentos de público-alvo contendo os atributos de consentimento necessários, você pode impor a conformidade com o TCF 2.0 ao exportar esses segmentos para destinos downstream.

Desde que a configuração de consentimento `gdprApplies` está definida como `true` para um conjunto de perfis de clientes, todos os dados desses perfis exportados para destinos downstream são filtrados com base nas preferências de consentimento da TCF para cada perfil. Qualquer perfil que não atende às preferências de consentimento necessárias é ignorado durante o processo de exportação.

Os clientes devem consentir com os seguintes objetivos (conforme descrito por [Políticas do TCF 2.0](https://iabeurope.eu/iab-europe-transparency-consent-framework-policies/#Appendix_A_Purposes_and_Features_Definitions)) para que seus perfis sejam incluídos em segmentos que são exportados para destinos:

* **Finalidade 1**: Armazenar e/ou acessar informações em um dispositivo
* **Finalidade 10**: Desenvolver e melhorar produtos

O TCF 2.0 também exige que a fonte de dados verifique a permissão de fornecedor do destino antes de enviar dados para esse destino. Dessa forma, a Platform verifica se a permissão do fornecedor do destino foi aceita para todas as IDs no cluster antes de incluir dados vinculados a esse destino.

>[!NOTE]
>
>Qualquer segmento compartilhado com a Adobe Audience Manager conterá os mesmos valores de consentimento da TCF 2.0 que seus equivalentes da plataforma. Since [!DNL Audience Manager] compartilha a mesma ID de fornecedor que a Plataforma (565), as mesmas finalidades e permissões de fornecedor são necessárias. Consulte o documento na [Plug-in do Adobe Audience Manager para a TCF do IAB](https://experienceleague.adobe.com/docs/audience-manager/user-guide/overview/data-privacy/consent-management/aam-iab-plugin.html) para obter mais informações.

## Testar sua implementação {#test-implementation}

Depois de configurar a implementação do TCF 2.0 e exportar segmentos para destinos, os dados que não atenderem aos requisitos de consentimento não serão exportados. No entanto, para ver se os perfis do cliente certos foram filtrados durante a exportação, você deve verificar manualmente os armazenamentos de dados em seus destinos para ver se o consentimento foi empregado corretamente.

É importante observar que, se várias IDs formarem um cluster e o TCF 2.0 se aplicar, todo o cluster será excluído se mesmo uma única ID não contiver os objetivos corretos e as permissões do fornecedor.

## Próximas etapas

Este documento cobriu o processo de configuração das operações de dados da plataforma para atender às suas obrigações comerciais, conforme descrito pelo TCF 2.0. Consulte a visão geral em [governança, privacidade e segurança](../../overview.md) para obter mais informações sobre os recursos relacionados à privacidade da Platform.
