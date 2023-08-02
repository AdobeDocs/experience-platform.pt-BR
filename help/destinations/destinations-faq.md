---
keywords: destinos, perguntas, perguntas frequentes, faq, perguntas frequentes sobre destinos
title: Perguntas frequentes
description: Respostas às perguntas mais frequentes sobre destinos do Adobe Experience Platform
exl-id: 2c34ecd0-a6d0-48dd-86b0-a144a6acf61a
source-git-commit: 810bcd011fd6e172c79f4482e047aa6e715c3918
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 4%

---

# Perguntas frequentes {#faq}

## Visão geral {#overview}

Este documento fornece respostas a perguntas frequentes sobre destinos do Adobe Experience Platform. Para perguntas e solução de problemas relacionados a outros [!DNL Platform] serviços, incluindo os encontrados em todos os [!DNL Platform] APIs, consulte o [guia de solução de problemas do Experience Platform](../landing/troubleshooting.md).

## Perguntas gerais sobre destinos {#general}

### Por que estou vendo diferentes contagens de perfis na interface do usuário do Experience Platform e nos arquivos CSV exportados?

+++Resposta Esse é um comportamento normal devido à forma como o Experience Platform executa a segmentação.

A segmentação de transmissão atualiza a contagem de perfis para públicos-alvo de transmissão ao longo do dia, enquanto a segmentação em lote atualiza a contagem de perfis para públicos-alvo em lote uma vez a cada 24 horas.

Quando o agendamento de exportação de público-alvo é diferente do agendamento de segmentação, o perfil é contado entre a interface do usuário e o exportado [!DNL CSV] O arquivo será diferente, especialmente quando se trata de públicos de transmissão.

Consulte a [Documentação do Serviço de segmentação](../segmentation/home.md) para obter mais detalhes.
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


## [!DNL Facebook Custom Audiences] {#facebook-faq}

### O que preciso fazer antes de ativar públicos no [!DNL Facebook Custom Audiences]?

+++Resposta Antes de enviar os públicos-alvo para [!DNL Facebook], certifique-se de atender aos seguintes requisitos:

* Seu [!DNL Facebook] a conta de usuário deve ter o **[!DNL Manage campaigns]** permissão ativada para a conta de anúncio que você planeja usar.
* A variável **Adobe Experience Cloud** conta comercial deve ser adicionada como um parceiro de publicidade em sua [!DNL Facebook Ad Account]. Use `business ID=206617933627973`. Consulte [Adicionar parceiros ao seu gerente de negócios](https://www.facebook.com/business/help/1717412048538897) na documentação do Facebook para obter detalhes.
  >[!IMPORTANT]
  >
  > Ao configurar as permissões para o Adobe Experience Cloud, você deve ativar o **Gerenciar campanhas** permissão. Isso é necessário para a integração de [!DNL Adobe Experience Platform].
* Leia e assine o [!DNL Facebook Custom Audiences] Termos de serviço. Para fazer isso, acesse `https://business.facebook.com/ads/manage/customaudiences/tos/?act=[accountID]`, onde `accountID` é a sua [!DNL Facebook Ad Account ID].
+++

### Preciso adicionar aplicativos ou pixels às [!DNL Facebook] conta de anunciante?

+++Número de resposta Como essa não é uma integração baseada em pixels, não há necessidade de adicionar pixels à conta do anunciante.
+++

### Quanto tempo o Facebook leva para processar informações do Adobe Experience Platform?

+++Resposta Em março de 2021, [!DNL Facebook Custom Audiences] precisa de até uma hora para processar informações recebidas do [!DNL Platform].
+++

### Posso usar [!DNL Facebook Custom Audiences] para direcionamento de público em outros [!DNL Facebook] aplicativos, como [!DNL Instagram]?

+++Senha Você pode usar o [!DNL Facebook Custom Audiences] destino para direcionamento de público-alvo na família de aplicativos da Facebook compatíveis com [!DNL Facebook Custom Audiences], incluindo [!DNL Facebook], [!DNL Instagram], [!DNL Audience Network], e [!DNL Messenger]. A seleção do aplicativo no qual os anunciantes desejam executar campanhas é indicada no nível de posicionamento no [!DNL Facebook Ads Manager].
+++

### Qual é a diferença entre as variáveis [!DNL Facebook Custom Audiences] conexão e [!DNL Facebook Pixel] extensão?

+++Responder A [!DNL Facebook Custom Audiences] usos da conexão [!DNL Platform] identidades ao enviar públicos para o [!DNL Facebook], enquanto a variável [[!DNL Facebook Pixel] conexão](../destinations/catalog/advertising/facebook-pixel.md) usa o [!DNL Facebook] pixel integrado em um site.

Estas duas integrações são complementares; você pode usar ambas para garantir uma melhor cobertura do público-alvo. Como exemplo, você pode usar a variável [!DNL Facebook Pixel] extensão para visitantes de sites de prospecção que não criaram uma conta, enquanto [!DNL Facebook Custom Audiences] podem ajudar você a direcionar clientes existentes, com base em [!DNL Platform] identidades.
+++

### A integração do Adobe Experience Platform com o [!DNL Facebook Custom Audiences] oferecer suporte à desqualificação de usuários de um público-alvo quando eles não se qualificam mais para ele?**

+++Responda Sim, a integração permite remover usuários do [!DNL Facebook Custom Audiences] quando eles não se qualificarem mais.
+++

### Como devo aplicar hash aos dados do público-alvo antes de enviá-los para o [!DNL Facebook]?

+++Resposta
[!DNL Facebook] exige que nenhuma informação pessoal identificável (PII) seja enviada em claro. Portanto, os públicos-alvo foram ativados para [!DNL Facebook] pode ser desativado *com hash* identificadores, como endereços de email ou números de telefone.

Para obter explicações detalhadas sobre os requisitos de correspondência de ID, consulte [Requisitos de correspondência de ID](catalog/social/facebook.md#id-matching-requirements).
+++

### Em que tipo de identidades posso ativar [!DNL Facebook Custom Audiences]?

+++Resposta
[!DNL Facebook Custom Audiences] O é compatível com a ativação das seguintes identidades: emails com hash, números de telefone com hash, [!DNL GAID], [!DNL IDFA]e IDs externas personalizadas.
+++

### Posso criar vários destinos do Facebook na interface do usuário da Platform para contas separadas do Facebook?

+++Responda Sim. Um destino do Facebook no Experience Platform é 1:1 para uma conta de anúncio no Facebook. É possível criar um destino do Facebook separado para cada conta de anúncio do Facebook na empresa. Siga as [tutorial de conexão de destino](/help/destinations/ui/connect-destination.md) e conecte-se a uma conta do Facebook separada para cada novo destino do Facebook na interface do usuário da plataforma. Não há limite para o número de contas de anúncios do Facebook às quais você pode se conectar.
+++

## Correspondência de cliente do Google {#google-customer-match}

### Ao exportar públicos para o Google Customer Match, por que vejo números extras anexados ao final dos nomes de público na interface do Google?

+++O Answer Google exige que os nomes dos públicos-alvo sejam exclusivos. Os números que você está vendo são [Carimbos de data e hora UNIX](https://www.unixtimestamp.com/) além disso, elas são anexadas para manter os nomes de público-alvo exclusivos, caso você tenha mapeado o mesmo público-alvo para vários destinos do Google.
+++

## Públicos-alvo correspondentes do linkedIn {#linkedin}

### Preciso adicionar aplicativos ou pixels às [!DNL LinkedIn] conta de anunciante?

+++Número de resposta Como essa não é uma integração baseada em pixels, não há necessidade de adicionar pixels à conta do anunciante.
+++

### O que preciso fazer antes de ativar públicos no [!DNL LinkedIn Matched Audiences]?

+++Resposta Antes que você possa usar o [!UICONTROL Público-alvo correspondente do linkedIn] destino, verifique se [!DNL LinkedIn Campaign Manager] a conta tem o [!DNL Creative Manager] nível de permissão ou superior.

Para saber como editar suas [!DNL LinkedIn Campaign Manager] permissões do usuário, consulte [Adicionar, editar e remover permissões de usuário em contas publicitárias](https://www.linkedin.com/help/lms/answer/5753) na documentação do LinkedIn.
+++

### Como devo aplicar hash aos dados do público-alvo antes de enviá-los para o [!DNL LinkedIn]?

+++Resposta
[!DNL LinkedIn] exige que nenhuma informação pessoal identificável (PII) seja enviada em claro. Portanto, os públicos-alvo foram ativados para [!DNL LinkedIn] pode ser desativado *com hash* identificadores, como endereços de email ou números de telefone.

Para obter explicações detalhadas sobre os requisitos de correspondência de ID, consulte [Requisitos de correspondência de ID](catalog/social/linkedin.md#id-matching-requirements).
+++

### Em que tipo de identidades posso ativar [!DNL LinkedIn]?

+++Resposta
[!DNL LinkedIn Matched Audiences] O é compatível com a ativação das seguintes identidades: emails com hash, [!DNL GAID], e [!DNL IDFA].
+++

## Personalização de mesma página e próxima página por meio da Adobe Target e destinos de Personalização personalizada {#same-next-page-personalization}

### Preciso usar o SDK da Web do Experience Platform para enviar públicos-alvo e atributos para a Adobe Target?

+++Número de resposta, [SDK da Web](../edge/home.md) não é necessário ativar públicos para [Adobe Target](catalog/personalization/adobe-target-connection.md).

No entanto, se [[!DNL at.js]](https://experienceleague.adobe.com/docs/target-dev/developer/client-side/at-js-implementation/overview.html?lang=pt-BR) é usada em vez do SDK da Web, somente a personalização da próxima sessão é compatível.

Para [personalização de mesma página e próxima página](ui/activate-edge-personalization-destinations.md) casos de uso, você deve usar [SDK da Web](../edge/home.md) ou o [API do servidor de rede de borda](../server-api/overview.md). Consulte a documentação em [ativação de públicos-alvo para destinos de borda](ui/activate-edge-personalization-destinations.md) para obter mais detalhes sobre a implementação.
+++

### Há um limite no número de atributos que posso enviar do Real-time Customer Data Platform para o Adobe Target ou um destino de Personalização personalizada?

+++Responda Sim, casos de uso de personalização de mesma página e próxima página são compatíveis com no máximo 30 atributos por sandbox ao ativar públicos para destinos do Adobe Target ou de Personalização personalizada. Consulte mais informações sobre medidas de proteção de ativação na [documentação das medidas de proteção](guardrails.md#edge-destinations-activation).
+++

### Que tipos de atributos são aceitos para ativação (por exemplo, arrays, mapas etc.)?

+++Resposta Atualmente, somente atributos estáticos de valor único são suportados, como `person.name.firstName`. Atributos de matriz não são aceitos no momento.
+++

<!-- **Is there a limit on the number of audiences that can be activated to Adobe Target and Custom Personalization destinations?**

Yes, you can activate a maximum of 150 edge audiences per sandbox.  For more information on activation guardrails, see the [default guardrails for activation](guardrails.md#edge-destinations-activation). -->

### Depois de criar um público-alvo no Experience Platform, quanto tempo levará para que esse público-alvo fique disponível para casos de uso de segmentação de borda?

+++Resposta As definições de público-alvo são propagadas para a [Rede de borda](../edge/home.md) em até uma hora. No entanto, se um público-alvo for ativado dentro dessa primeira hora, alguns visitantes que se qualificariam para o público-alvo poderão ser perdidos.
+++

### Onde posso ver os atributos ativados no Adobe Target?

+++Os atributos de resposta estarão disponíveis para uso no Target no [JSON](https://experienceleague.adobe.com/docs/target/using/experiences/offers/create-json-offer.html) e [HTML](https://experienceleague.adobe.com/docs/target/using/experiences/offers/manage-content.html?lang=pt-BR) ofertas.
+++

### Posso criar um destino sem um fluxo de dados e, em seguida, adicionar um fluxo de dados ao mesmo destino em um ponto posterior?

+++Resposta No momento, não há suporte para isso na interface do usuário de Destinos. Se precisar de assistência neste caso, entre em contato com o representante da Adobe.
+++

### O que acontece se eu excluir um destino do Adobe Target?

+++Resposta Ao excluir um destino, todos os públicos-alvo e atributos mapeados no destino são excluídos da Adobe Target e também são removidos da Rede de borda.
+++

### A integração funciona usando a API do servidor de rede de borda?

+++Responda Sim, a API do servidor de rede de borda funciona com o destino de Personalização personalizada. Como os atributos de perfil podem conter dados confidenciais, para protegê-los, o destino da Personalização personalizada exige que você use a API do servidor de rede de borda para a coleta de dados. Além disso, todas as chamadas de API devem ser feitas em um [contexto autenticado](../server-api/authentication.md).
+++

### Só posso ter uma política de mesclagem que esteja ativa no edge. Posso criar públicos-alvo que usem uma política de mesclagem diferente e ainda enviá-los para a Adobe Target como públicos-alvo de transmissão?

+++Número de resposta Todos os públicos-alvo que você deseja ativar para o Adobe Target devem usar uma interface ativa na borda [política de mesclagem](../profile/merge-policies/ui-guide.md).
+++

### As DULE (Label Usage Labeling and Enforcement, Rotulagem e aplicação de uso de dados) e as políticas de consentimento são aplicadas?

+++Responda Sim. A variável [Políticas de consentimento e governança de dados](../data-governance/home.md) criado e associado às ações de marketing selecionadas controlará a ativação dos atributos selecionados.
+++
