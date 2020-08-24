---
keywords: Experience Platform;home;popular topics;opt-out
solution: Experience Platform
title: Aceitar opções
topic: overview
description: 'O Experience Platform permite que seus clientes enviem solicitações de não participação relacionadas ao uso e armazenamento de seus dados no Perfil do cliente em tempo real]. Essas solicitações de cancelamento fazem parte da California Consumer Privacy Act (CCPA), que dá aos residentes da Califórnia o direito de acessar e excluir seus dados pessoais e saber se seus dados pessoais foram vendidos ou divulgados (e a quem). '
translation-type: tm+mt
source-git-commit: 0fc356b67af4d34e35cd9329385ec284d9336953
workflow-type: tm+mt
source-wordcount: '1006'
ht-degree: 0%

---


# Aceitar solicitações de não participação em segmentos

[!DNL Experience Platform] permite que seus clientes enviem solicitações de recusa relacionadas ao uso e armazenamento de seus dados no [!DNL Real-time Customer Profile]. Essas solicitações de cancelamento fazem parte da CCPA [!DNL California Consumer Privacy Act] (California), que concede aos residentes da Califórnia o direito de acessar e excluir seus dados pessoais e saber se seus dados pessoais foram vendidos ou divulgados (e a quem).

Depois que um cliente optar por não participar, é importante que sua organização cumpra essas opções ao gerar audiências para atividades de marketing. Este documento descreve detalhes importantes relacionados ao cumprimento de solicitações de não participação.

## Introdução

O cumprimento dos pedidos de opção de não participação exige uma compreensão dos vários [!DNL Adobe Experience Platform] serviços envolvidos. Antes de trabalhar com solicitações de recusa, consulte a documentação dos seguintes serviços:

- [!DNL Real-time Customer Profile](../profile/home.md): Fornece um perfil unificado e em tempo real para o cliente, com base em dados agregados de várias fontes.
- [!DNL Adobe Experience Platform Segmentation Service](./home.md): Permite que você crie segmentos de audiência a partir de [!DNL Real-time Customer Profile] dados.
- [!DNL Experience Data Model (XDM)](../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.
- [!DNL Adobe Experience Platform Privacy Service](../privacy-service/home.md): Ajuda as organizações a automatizar a conformidade com as regulamentações de privacidade de dados que envolvem dados de clientes dentro [!DNL Platform].

## Misturas de não participação

Para atender às solicitações de recusa do CCPA, um dos schemas que faz parte do schema da união deve conter os campos de opção [!DNL Experience Data Model] (XDM) necessários. Há duas combinações que podem ser usadas para adicionar campos de opção de não participação a um schema, cada uma é abordada com mais detalhes nas seções a seguir:

- [Privacidade](#profile-privacy)do perfil: Usado para capturar tipos diferentes de opção de não participação (geral ou vendas/compartilhamento).
- [Detalhes](#profile-preferences-details)das preferências do perfil: Usado para capturar solicitações de recusa para canais XDM específicos.

Para obter instruções passo a passo sobre como adicionar uma mistura a um schema, consulte a seção &quot;Adicionar uma mistura&quot; na seguinte documentação XDM:
- [Tutorial](../xdm/api/getting-started.md)da API do Registro do schema.: Criação de um schema usando a API de registro do Schema.
- [Tutorial](../xdm/tutorials/create-schema-ui.md)do Editor de schemas: Criação de um schema usando a interface do usuário da Plataforma.

Esta é uma imagem de exemplo mostrando as combinações de opção de não participação adicionadas a um schema na interface do usuário:

![](images/opt-outs/opt-out-mixins-user-interface.png)

A estrutura de cada mistura, bem como uma descrição dos campos que contribuem para o schema, são descritos com mais detalhes nas seções a seguir.

### [!DNL Profile Privacy] {#profile-privacy}

A [!DNL Profile Privacy] combinação permite capturar dois tipos de solicitações de cancelamento CCPA dos clientes:

1. Recusa geral
2. Opção de não participação de vendas/compartilhamento

![](images/opt-outs/profile-privacy.png)

The [!DNL Profile Privacy] mixin contains the following fields:

- Opções de privacidade (`privacyOptOuts`): Uma matriz que contém uma lista de objetos de opção de não participação.
- Tipo de opção de não participação (`optOutType`): O tipo de opção de não participação. Este campo é um enum com dois valores possíveis:
   - Recusa geral (`general_opt_out`)
   - Recusa de compartilhamento de vendas (`sales_sharing_opt_out`)
- Valor da opção de não participação (`optOutValue`): O estado ativo da opção de não participação, também conhecido como o valor do sinal de não participação, com base no tipo de opção de não participação especificado. Este campo é um enum com quatro valores possíveis:
   - Não fornecido (`not_provided`): Uma solicitação de opção de não participação não foi fornecida.
   - Verificação pendente (`pending`): A solicitação de não participação está aguardando verificação.
   - Recusar (`out`): O cliente optou por não participar.
   - Inclusão (`in`): O cliente aceitou.
- Carimbo de data e hora de recusa (`timestamp`): Carimbo de data e hora do sinal de não participação recebido.

Para visualização da estrutura completa da [!DNL Profile Privacy] mistura, consulte o repositório [público GitHub do](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) XDM ou pré-visualização a mistura usando a interface do usuário da plataforma.

### [!DNL Profile Preferences Details] {#profile-preferences-details}

A [!DNL Profile Preferences Details] combinação fornece vários campos que representam preferências para perfis do cliente (como formato do email, idioma preferencial e fuso horário). Um dos campos incluídos nessa combinação, OptInOut (`optInOut`), permite que valores de opção de não participação sejam definidos para canais individuais.

![](images/opt-outs/profile-preferences-details.png)

O [!DNL Profile Preferences Details] mixin contém os seguintes campos relacionados a opções de não participação:

- OptInOut (`optInOut`): Um objeto em que cada chave representa um URI válido e conhecido para um canal de comunicação e o estado ativo da opção de não participação para cada canal. Cada canal pode ter um de quatro valores possíveis:
   - Não fornecido (`not_provided`): Não foi fornecida uma solicitação de opção de não participação para este canal.
   - Verificação pendente (`pending`): A solicitação de não participação para este canal está pendente de verificação.
   - Recusar (`out`): O cliente optou por não participar deste canal.
   - Inclusão (`in`): O cliente optou por este canal.
- Recusa global (`globalOptout`): Um valor booliano que, quando definido como true, define uma substituição global de não participação para o perfil. O valor padrão para esse campo é falso.

O exemplo JSON abaixo destaca como o objeto OptInOut pode capturar vários sinais de recusa para diferentes canais de comunicação:

```json
{
  "xdm:optInOut": {
    "https://ns.adobe.com/xdm/channels/email": "pending",
    "https://ns.adobe.com/xdm/channels/phone": "out",
    "https://ns.adobe.com/xdm/channels/sms": "in",
    "https://ns.adobe.com/xdm/channels/fax": "not_provided",
    "https://ns.adobe.com/xdm/channels/direct-mail": "not_provided",
    "https://ns.adobe.com/xdm/channels/apns": "not_provided",
    "xdm:globalOptout": false
  }
}
```

Para visualização de toda a estrutura da combinação Detalhes das preferências do Perfil, visite o repositório [público do GitHub do](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) XDM ou pré-visualização a combinação usando a [!DNL Platform] interface do usuário.

## Tratamento de opções na segmentação

Para garantir que os perfis marcados com sinalizadores de recusa CCPA não sejam incluídos nos segmentos, os campos especiais devem ser adicionados aos segmentos existentes ou incluídos durante a criação do segmento.

As seções abaixo demonstram como adicionar os campos apropriados para os dois tipos de sinalizadores de opção de não participação:
1. Recusa geral
2. Opção de não participação de vendas/compartilhamento

### Recusa geral

[!DNL Segmentation] atende automaticamente a todos os perfis que contêm o sinalizador &quot;Recusageral&quot;, o que significa que esses perfis não serão incluídos no audiência ou nas exportações por padrão. No entanto, é prática recomendada adicionar os campos apropriados para garantir que os perfis que não foram incluídos nas audiências e atividades de marketing.

Isso pode ser feito usando a interface do usuário, adicionando atributos de opção de não participação de **[!UICONTROL privacidade]** . Nesse caso, o segmento é definido para incluir somente aqueles que opt in (o que significa que eles não têm um sinalizador de opção de não participação geral em seus perfis). Isso é feito declarando que o &quot;Tipo[!UICONTROL de]opção de não participação&quot; é igual a &quot;[!UICONTROL Opção de não participação]geral&quot; e o &quot;Valor[!UICONTROL de]opção de não participação&quot; é igual a &quot;[!UICONTROL Aceitação]&quot;.

![](images/opt-outs/segment-general-opt-out.png)

### Opção de não participação de vendas/compartilhamento

Se um usuário tiver um sinalizador de recusa de vendas/compartilhamento definido em seu perfil, esse perfil não deverá mais ser usado para nenhuma criação de segmento ou atividades de marketing. Para garantir que esse sinalizador seja respeitado, o &quot;Tipo[!UICONTROL de]opção de não participação&quot; deve ser igual a &quot;Opção de não participação[!UICONTROL no compartilhamento de]vendas&quot; e o &quot;Valor[!UICONTROL de]opção de não participação&quot; deve ser igual a &quot;[!UICONTROL Aceitação]&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Próximas etapas

Para obter mais informações sobre segmentação, inclusive trabalhar com definições de segmentos e audiências por meio da API e da interface do usuário, comece lendo a visão geral [da](./home.md)segmentação.

Para saber mais sobre a privacidade de dados no [!DNL Platform], incluindo como [!DNL Privacy Service] facilitar a conformidade automatizada com as regulamentações legais e organizacionais de privacidade, consulte a documentação sobre [!DNL Privacy Service](../privacy-service/home.md).
