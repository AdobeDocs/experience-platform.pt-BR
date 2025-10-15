---
keywords: destinos, perguntas, perguntas frequentes, faq, perguntas frequentes sobre destinos
title: Perguntas frequentes
description: Respostas às perguntas mais frequentes sobre destinos do Adobe Experience Platform
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 7f3459f678c74ead1d733304702309522dd0018b
workflow-type: tm+mt
source-wordcount: '1673'
ht-degree: 0%

---

# Perguntas frequentes {#faq}

## Visão geral {#overview}

Este documento fornece respostas a perguntas frequentes sobre destinos do Adobe Experience Platform. Para perguntas e soluções de problemas relacionadas a outros serviços do [!DNL Experience Platform], incluindo aquelas encontradas em todas as APIs do [!DNL Experience Platform], consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

## Perguntas gerais sobre destinos {#general}

### Por que estou vendo diferentes contagens de perfis na interface do usuário do Experience Platform e nos arquivos CSV exportados?

+++Resposta
Esse é um comportamento normal devido à forma como o Experience Platform executa a segmentação.

A segmentação de transmissão atualiza a contagem de perfis para públicos-alvo de transmissão ao longo do dia, enquanto a segmentação em lote atualiza a contagem de perfis para públicos-alvo em lote uma vez a cada 24 horas.

Quando a programação de exportação de público-alvo for diferente da programação de segmentação, a contagem de perfis entre a interface do usuário e o arquivo [!DNL CSV] exportado será diferente, especialmente quando se trata de públicos de transmissão.

Consulte a [documentação do Serviço de segmentação](../segmentation/home.md) para obter mais detalhes.
+++

### Por que vejo taxas de correspondência baixas ao desativar e reativar um público atualizado para o mesmo destino?

+++Resposta

A desativação e a remoção de um público-alvo de um destino de transmissão não acionam um preenchimento retroativo na reativação do público-alvo para o mesmo destino de transmissão.

**Exemplo**

Você ativou um público-alvo que consiste em 10 perfis para um destino de transmissão.

Depois de ativar o público-alvo, você percebe que deseja alterar a configuração do público-alvo e, portanto, desativa-o e altera seus critérios de população, resultando em uma população de público-alvo de 100 perfis.

Você reativa o público-alvo atualizado para o mesmo destino, mas como não há preenchimento retroativo acionado, seu destino não recebe os 90 perfis adicionais.

**Solução**

Para garantir que todos os perfis sejam enviados para o seu destino, você deve criar um novo público-alvo com a nova configuração e ativá-lo para o seu destino.

+++

### Quando um público-alvo é removido de um destino, há algum sinal enviado para o destino indicando que o público-alvo foi removido?

+++Resposta

Não, não há dependência entre o destino do Experience Platform e a instância do cliente do sistema de destino. Do lado da recepção, a única indicação que o sistema de direcionamento veria é que pararia de receber esses dados do público-alvo.

+++

<!--
## [!DNL Experience Cloud Audiences] {#eca-faq}

### What are the differences between the Experience Cloud Audiences and Adobe Target destinations?

+++Answer

See the table below for a feature comparison between the Experience Cloud Audiences and Adobe Target destinations.

||Experience Cloud Audiences|Adobe Target|
|---|---|---|
| **Supported Experience Cloud apps** | Supports audience activation to Audience Manager, Adobe Target, Adobe Analytics, Advertising Cloud, Marketo, Adobe Campaign | Supports audience activation only to Adobe Target |
| **Supports audience activation** | ✓ | ✓ |
| **Supports attribute activation** | X | ✓ |
| **Latency** | Profiles begin activating in 6 hours. Full population is visible in 48 hours​. |Depends on implementation​ type. <ul><li>Web SDK enables same-page/next-page​ personalization.</li><li>AT.js enables next-session personalization.</li></ul> |
| **DULE support** | ✓ | ✓ |
| **Marketing actions support** | ✓ | ✓ |
| **Supported IDs** | [!DNL ECID], [!DNL GAID], [!DNL IDFA], [!DNL email_lc_sha256] | Any ID type |
| **Sandbox support** | One sandbox | Multiple sandboxes |
| **Consent support** | X | Yes. Requires Privacy & Security Shield. |
| **Edge segmentation support** | Supports activation of edge audiences. Does not support edge segmentation. | Supports edge segmentation and activation of edge audiences. |
| **Supported audiences** | All types of audiences  | Edge merge policy required for activation.|

+++

-->

## [!DNL Facebook Custom Audiences] {#facebook-faq}

### O que preciso fazer antes de ativar públicos no [!DNL Facebook Custom Audiences]?

+++Resposta
Antes de enviar seus públicos-alvo para o [!DNL Facebook], verifique se você atende aos seguintes requisitos:

* A permissão **[!DNL Manage campaigns]** da conta de usuário [!DNL Facebook] deve estar habilitada para a conta de Anúncio que você pretende usar.
* A conta comercial **Adobe Experience Cloud** deve ser adicionada como um parceiro de publicidade em seu [!DNL Facebook Ad Account]. Usar `business ID=206617933627973`. Consulte [Adicionar parceiros ao seu gerente de negócios](https://www.facebook.com/business/help/1717412048538897) na documentação do Facebook para obter detalhes.

  >[!IMPORTANT]
  >
  > Ao configurar as permissões para o Adobe Experience Cloud, você deve habilitar a permissão **Gerenciar campanhas**. Isso é necessário para a integração de [!DNL Adobe Experience Platform].
* Leia e assine os Termos de Serviço do [!DNL Facebook Custom Audiences]. Para fazer isso, vá para `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, onde `accountID` é seu [!DNL Facebook Ad Account ID].
+++

### Preciso adicionar aplicativos ou pixels à minha conta de anunciante [!DNL Facebook]?

+++Resposta
Não. Como essa não é uma integração baseada em pixels, não há necessidade de adicionar pixels à conta do anunciante.
+++

### Quanto tempo leva o Facebook para processar informações do Adobe Experience Platform?

+++Resposta
A partir de março de 2021, o [!DNL Facebook Custom Audiences] precisa de até uma hora para processar informações recebidas do [!DNL Experience Platform].
+++

### Posso usar o [!DNL Facebook Custom Audiences] para direcionamento de público em outros aplicativos do [!DNL Facebook], como o [!DNL Instagram]?

+++Atendimento
Você pode usar o destino [!DNL Facebook Custom Audiences] para direcionamento de público-alvo na família de aplicativos do Facebook com suporte no [!DNL Facebook Custom Audiences], incluindo [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network] e [!DNL Messenger]. A seleção do aplicativo no qual os anunciantes desejam executar campanhas é indicada no nível de posicionamento em [!DNL Facebook Ads Manager].
+++

### Qual é a diferença entre a conexão [!DNL Facebook Custom Audiences] e a extensão [!DNL Facebook Pixel]?

+++Resposta
A conexão [!DNL Facebook Custom Audiences] usa identidades [!DNL Experience Platform] ao enviar públicos-alvo para [!DNL Facebook], enquanto a [[!DNL Facebook Pixel] conexão](../destinations/catalog/advertising/facebook-pixel.md) usa o pixel [!DNL Facebook] integrado em um site.

Essas duas integrações são complementares; você pode usar ambas para garantir uma melhor cobertura do público-alvo. Como exemplo, você pode usar a extensão [!DNL Facebook Pixel] para visitantes de sites de prospecção que não criaram uma conta, enquanto o [!DNL Facebook Custom Audiences] pode ajudá-lo a direcionar clientes existentes, com base nas identidades [!DNL Experience Platform].
+++

### A integração do Adobe Experience Platform com o [!DNL Facebook Custom Audiences] oferece suporte à desqualificação de usuários de um público-alvo quando eles não se qualificam mais para ele?**

+++Resposta
Sim, a integração oferece suporte à remoção de usuários do [!DNL Facebook Custom Audiences] quando eles não estão mais qualificados.
+++

### Como devo aplicar um hash nos dados do público-alvo antes de enviá-los para o [!DNL Facebook]?

+++Resposta
[!DNL Facebook] exige que nenhuma informação pessoal identificável (PII) seja enviada em branco. Portanto, os públicos ativados para [!DNL Facebook] podem ser digitados de *identificadores com hash*, como endereços de email ou números de telefone.

Para obter explicações detalhadas sobre os requisitos de correspondência de ID, consulte [requisitos de correspondência de ID](catalog/social/facebook.md#id-matching-requirements).
+++

### Que tipo de identidades posso ativar no [!DNL Facebook Custom Audiences]?

+++Resposta
O [!DNL Facebook Custom Audiences] oferece suporte à ativação das seguintes identidades: emails com hash, números de telefone com hash, [!DNL GAID], [!DNL IDFA] e IDs externas personalizadas.
+++

### Posso criar vários destinos do Facebook na interface do usuário do Experience Platform para contas do Facebook separadas?

+++Resposta
Sim. Um destino do Facebook no Experience Platform é de 1:1 para uma conta publicitária no Facebook. É possível criar um destino do Facebook separado para cada conta de anúncio do Facebook em sua empresa. Siga o [tutorial de conexão de destino](/help/destinations/ui/connect-destination.md) e conecte-se a uma conta separada do Facebook para cada novo destino do Facebook na interface do usuário do Experience Platform. Não há limite para o número de contas de anúncios do Facebook às quais você pode se conectar.
+++

## Google Customer Match {#google-customer-match}

### Ao exportar públicos para o Google Customer Match, por que vejo números extras anexados ao final dos nomes de público na interface do Google?

+++Resposta
O Google exige que os nomes dos públicos-alvo sejam exclusivos. Os números que você está vendo são [carimbos de data e hora UNIX](https://www.unixtimestamp.com/) e são anexados para manter os nomes de público-alvo exclusivos, se você mapeou o mesmo público-alvo para vários destinos Google.
+++

## Públicos correspondentes do LinkedIn {#linkedin}

### Preciso adicionar aplicativos ou pixels à minha conta de anunciante [!DNL LinkedIn]?

+++Resposta
Não. Como essa não é uma integração baseada em pixels, não há necessidade de adicionar pixels à conta do anunciante.
+++

### O que preciso fazer antes de ativar públicos no [!DNL LinkedIn Matched Audiences]?

+++Resposta
Antes de poder usar o destino [!UICONTROL Público-alvo correspondente do LinkedIn], verifique se a sua conta [!DNL LinkedIn Campaign Manager] tem o nível de permissão [!DNL Creative Manager] ou superior.

Para saber como editar suas permissões de usuário do [!DNL LinkedIn Campaign Manager], consulte [Adicionar, Editar, e Remover Permissões de Usuário em Contas do Advertising](https://www.linkedin.com/help/lms/answer/5753) na documentação do LinkedIn.
+++

### Como devo aplicar um hash nos dados do público-alvo antes de enviá-los para o [!DNL LinkedIn]?

+++Resposta
[!DNL LinkedIn] exige que nenhuma informação pessoal identificável (PII) seja enviada em branco. Portanto, os públicos ativados para [!DNL LinkedIn] podem ser digitados de *identificadores com hash*, como endereços de email ou números de telefone.

Para obter explicações detalhadas sobre os requisitos de correspondência de ID, consulte [requisitos de correspondência de ID](catalog/social/linkedin.md#id-matching-requirements).
+++

### Que tipo de identidades posso ativar no [!DNL LinkedIn]?

+++Resposta
O [!DNL LinkedIn Matched Audiences] oferece suporte à ativação das seguintes identidades: emails com hash, [!DNL GAID] e [!DNL IDFA].

+++

## Personalização de mesma página e próxima página por meio dos destinos do Adobe Target e do Personalization personalizado {#same-next-page-personalization}

### Preciso usar o Experience Platform Web SDK para enviar públicos-alvo e atributos para a Adobe Target?

+++Resposta
Não, o [Web SDK](../web-sdk/home.md) não é necessário para ativar públicos para o [Adobe Target](catalog/personalization/adobe-target-connection.md).

No entanto, se [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=pt-BR) for usado em vez do Web SDK, somente a personalização da próxima sessão será suportada.

Para casos de uso de [personalização de mesma página e próxima página](ui/activate-edge-personalization-destinations.md), você deve usar o [Web SDK](../web-sdk/home.md) ou a [API Edge Network](https://developer.adobe.com/data-collection-apis/docs/api/). Consulte a documentação sobre [ativação de públicos-alvo para destinos de borda](ui/activate-edge-personalization-destinations.md) para obter mais detalhes de implementação.
+++

### Há um limite no número de atributos que posso enviar da Plataforma de dados do cliente em tempo real para a Adobe Target ou um destino de Personalization personalizado?

+++Resposta
Sim, casos de uso de personalização de mesma página e próxima página aceitam no máximo 30 atributos por sandbox ao ativar públicos-alvo para destinos do Adobe Target ou do Personalization personalizado. Consulte mais informações sobre medidas de proteção de ativação na [documentação de medidas de proteção](guardrails.md#edge-destinations-activation).
+++

### Que tipos de atributos são aceitos para ativação (por exemplo, arrays, mapas etc.)?

+++Resposta
Atualmente, somente atributos estáticos de valor único são suportados, como `person.name.firstName`. Atributos de matriz não são aceitos no momento.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Depois de criar um público-alvo no Experience Platform, quanto tempo levará para que esse público-alvo fique disponível para casos de uso de segmentação de borda?

+++Resposta
As definições de público-alvo são propagadas para o [Edge Network](../web-sdk/home.md) em até uma hora. No entanto, se um público-alvo for ativado dentro dessa primeira hora, alguns visitantes que se qualificariam para o público-alvo poderão ser perdidos.
+++

### Onde posso ver os atributos ativados no Adobe Target?

+++Resposta
Os atributos estarão disponíveis para uso no Target nas ofertas [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html?lang=pt-BR) e [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=pt-BR).
+++

### Posso criar um destino sem um fluxo de dados e, em seguida, adicionar um fluxo de dados ao mesmo destino em um ponto posterior?

+++Resposta
No momento, isso não é compatível com a interface de Destinos. Se precisar de assistência neste caso, entre em contato com o representante da Adobe.
+++

### O que acontece se eu excluir um destino do Adobe Target?

+++Resposta
Quando você exclui um destino, todos os públicos-alvo e atributos mapeados no destino são excluídos da Adobe Target e também são removidos da Edge Network.
+++

### A integração funciona usando a API do Edge Network?

+++Resposta
Sim, a API do Edge Network funciona com o destino do Personalization personalizado. Como os atributos de perfil podem conter dados confidenciais, para protegê-los, o destino Personalization personalizado exige que você use a API do Edge Network para coleta de dados. Além disso, todas as chamadas de API devem ser feitas em um [contexto autenticado](https://developer.adobe.com/data-collection-apis/docs/getting-started/authentication/).
+++

### Só posso ter uma política de mesclagem que esteja ativa no edge. Posso criar públicos-alvo que usem uma política de mesclagem diferente e ainda enviá-los para a Adobe Target como públicos-alvo de transmissão?

+++Resposta
Não. Todos os públicos que você deseja ativar para o Adobe Target devem usar uma [política de mesclagem](../profile/merge-policies/ui-guide.md) ativa na borda.
+++

### As DULE (Label Usage Labeling and Enforcement, Rotulagem e aplicação de uso de dados) e as políticas de consentimento são aplicadas?

+++Resposta
Sim. As [Políticas de Consentimento e Governança de Dados](../data-governance/home.md) criadas e associadas às ações de marketing selecionadas controlarão a ativação dos atributos selecionados.
+++

### Os destinos [!DNL Adobe Target] e [!DNL Custom Personalization] [!DNL HIPAA] são compatíveis?

+++Resposta
[!DNL Adobe Target] não é compatível com [!DNL HIPPA] com [[!DNL Adobe Healthcare Shield]](https://business.adobe.com/br/solutions/industries/healthcare.html). Os clientes devem consultar suas próprias equipes jurídicas em relação à preparação de [!DNL HIPPA] para canais de otimização personalizados antes de usar a personalização de borda por meio de [!DNL Adobe Target] ou dos destinos [!DNL Custom Personalization].

Para casos de uso em que o gerenciamento da política de consentimento precisa ser aplicado em escala, os clientes devem comprar o [!DNL Adobe Privacy & Security Shield]. Os recursos do [!DNL Adobe Privacy & Security Shield] são vendidos como um conjunto avançado de funcionalidades e não podem ser comprados separadamente.

Este serviço inclui chaves gerenciadas pelo cliente e limites elevados para gerenciar o ciclo de vida dos dados do cliente.

Os destinos [!DNL Adobe Target] e [!DNL Custom Personalization] estão integrados aos [Rótulos de Uso de Dados da Experience Platform](../data-governance/labels/overview.md) e ao [Serviço de Imposição de Política de Consentimento](../data-governance/enforcement/overview.md). Esses recursos estão disponíveis para todos os clientes.




+++

