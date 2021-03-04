---
keywords: Experience Platform, home, tópicos populares, recusar, segmentação, serviço de segmentação, serviço de segmentação, opções de honra, recusas, rejeitar, excluir;
solution: Experience Platform
title: Respeito das solicitações de recusa em segmentos
topic: visão geral
description: 'A Adobe Experience Platform permite que seus clientes enviem solicitações de recusa relacionadas ao uso e armazenamento de seus dados no Perfil do cliente em tempo real]. Essas solicitações de recusa fazem parte da California Consumer Privacy Act (CCPA), que fornece aos residentes da Califórnia o direito de acessar e excluir seus dados pessoais e saber se seus dados pessoais são vendidos ou divulgados (e para quem). '
translation-type: tm+mt
source-git-commit: 126b3d1cf6d47da73c6ab045825424cf6f99e5ac
workflow-type: tm+mt
source-wordcount: '1033'
ht-degree: 0%

---


# Respeito às solicitações de recusa em segmentos

A Adobe Experience Platform permite que seus clientes enviem solicitações de recusa relacionadas ao uso e armazenamento de seus dados em [!DNL Real-time Customer Profile]. Essas solicitações de recusa fazem parte da [!DNL California Consumer Privacy Act] (CCPA), que fornece aos residentes da Califórnia o direito de acessar e excluir seus dados pessoais e saber se seus dados pessoais são vendidos ou divulgados (e para quem).

Depois que um cliente optar por não participar, é importante que sua organização honre essas opções ao gerar públicos-alvo para atividades de marketing. Este documento descreve detalhes importantes sobre o cumprimento de solicitações de recusa.

## Introdução

O cumprimento de solicitações de recusa requer uma compreensão dos vários serviços [!DNL Adobe Experience Platform] envolvidos. Antes de trabalhar com solicitações de recusa, revise a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../profile/home.md): Fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
- [[!DNL Adobe Experience Platform Segmentation Service]](./home.md): Permite criar segmentos de público-alvo a partir de  [!DNL Real-time Customer Profile] dados.
- [[!DNL Experience Data Model (XDM)]](../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.
- [[!DNL Adobe Experience Platform Privacy Service]](../privacy-service/home.md): Ajuda as organizações a automatizar a conformidade com as regulamentações de privacidade de dados que envolvem dados de clientes no  [!DNL Platform].

## Misturas de rejeição

Para honrar as solicitações de recusa do CCPA, um dos esquemas que fazem parte do schema da união deve conter os campos de recusa [!DNL Experience Data Model] (XDM) necessários. Há duas combinações que podem ser usadas para adicionar campos de opção de não participação a um schema, cada uma é abordada com mais detalhes nas seções a seguir:

- [Privacidade](#profile-privacy) do perfil: Usado para capturar diferentes tipos de recusa (geral ou vendas/compartilhamento).
- [Detalhes](#profile-preferences-details) das preferências de perfil: Usado para capturar solicitações de recusa para canais XDM específicos.

Para obter instruções passo a passo sobre como adicionar uma mixin a um schema, consulte a seção &quot;Adicionar uma mixin&quot; na seguinte documentação XDM:
- [Tutorial da API do Registro de Esquema](../xdm/api/getting-started.md).: Criação de um esquema usando a API do Registro de esquema.
- [Tutorial](../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Criar um schema usando a interface do usuário da plataforma .

Esta é uma imagem de exemplo mostrando as combinações de opt out adicionadas a um schema na interface do usuário:

![](images/opt-outs/opt-out-mixins-user-interface.png)

A estrutura de cada mixin, bem como uma descrição dos campos que contribuem para o schema, são descritos mais detalhadamente nas seções a seguir.

### [!DNL Profile Privacy] {#profile-privacy}

A combinação [!DNL Profile Privacy] permite capturar dois tipos de solicitações de recusa do CCPA dos clientes:

1. Opt out geral
2. Opção de rejeição de vendas/compartilhamento

![](images/opt-outs/profile-privacy.png)

O mixin [!DNL Profile Privacy] contém os seguintes campos:

- Opções de não participação de privacidade (`privacyOptOuts`): Uma matriz contendo uma lista de objetos de opção de não participação.
- Tipo de rejeição (`optOutType`): O tipo de recusa. Este campo é um enum com dois valores possíveis:
   - Opção de rejeição geral (`general_opt_out`)
   - Rejeição de compartilhamento de vendas (`sales_sharing_opt_out`)
- Valor de rejeição (`optOutValue`): O estado ativo da recusa, também conhecido como o valor do sinal de recusa, com base no tipo de rejeição especificado. Este campo é um enum com quatro valores possíveis:
   - Não fornecido (`not_provided`): Não foi fornecida uma solicitação de recusa.
   - Verificação pendente (`pending`): A solicitação de recusa está pendente da verificação.
   - Opção de rejeição (`out`): O cliente recusou a participação.
   - Opt-In (`in`): O cliente aceitou.
- Carimbo de data e hora de rejeição (`timestamp`): Carimbo de data e hora do sinal de recusa recebido.

Para visualizar a estrutura completa da mixin [!DNL Profile Privacy], consulte o [repositório GitHub público XDM](https://github.com/adobe/xdm/blob/master/schemas/context/profile-privacy.schema.json) ou visualize o mixin usando a interface do usuário da plataforma.

### [!DNL Profile Preferences Details] {#profile-preferences-details}

O mixin [!DNL Profile Preferences Details] fornece vários campos que representam preferências para perfis do cliente (como formato do email, idioma preferencial e fuso horário). Um dos campos incluídos nesse mixin, OptInOut (`optInOut`), permite que valores de opt out sejam definidos para canais individuais.

![](images/opt-outs/profile-preferences-details.png)

O mixin [!DNL Profile Preferences Details] contém os seguintes campos relacionados às opções de não participação:

- OptInOut (`optInOut`): Um objeto em que cada chave representa um URI válido e conhecido para um canal de comunicação e o estado ativo da recusa para cada canal. Cada canal pode ter um dos quatro valores possíveis:
   - Não fornecido (`not_provided`): Não foi fornecida uma solicitação de recusa para este canal.
   - Verificação pendente (`pending`): A solicitação de recusa para este canal está pendente de verificação.
   - Opção de rejeição (`out`): O cliente optou por não participar deste canal.
   - Opt-In (`in`): O cliente optou por participar deste canal.
- Opção de rejeição global (`globalOptout`): Um valor booleano que, quando definido como true, define uma substituição de recusa global para o perfil. O valor padrão para esse campo é false.

O exemplo JSON abaixo destaca como o objeto OptInOut pode capturar vários sinais de opt out para diferentes canais de comunicação:

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

Para visualizar a estrutura completa da mesclagem Detalhes das preferências de perfil , visite o [repositório GitHub público XDM](https://github.com/adobe/xdm/blob/master/schemas/context/profile-preferences-details.schema.json) ou visualize a mesclagem usando a interface [!DNL Platform].

## Tratamento de recusas na segmentação

Para garantir que os perfis marcados com sinalizadores de recusa do CCPA não sejam incluídos em segmentos, campos especiais devem ser adicionados a segmentos existentes ou incluídos durante a criação do segmento.

As seções abaixo demonstram como adicionar os campos apropriados para os dois tipos de sinalizadores de opt out:
1. Opt out geral
2. Opção de rejeição de vendas/compartilhamento

### Opt out geral

[!DNL Segmentation] O atende automaticamente a todos os perfis que contêm o sinalizador de &quot;[!UICONTROL recusa geral]&quot;, o que significa que esses perfis não serão incluídos em públicos-alvo ou exportações por padrão. No entanto, é uma prática recomendada adicionar os campos apropriados para garantir que os perfis de não participação não sejam incluídos em públicos-alvo e atividades de marketing.

Isso pode ser feito usando a interface do usuário adicionando atributos **[!UICONTROL Privacy Opt-Outs]**. Nesse caso, o segmento é definido para incluir apenas aqueles que optaram por participar (o que significa que não têm um sinalizador de opt out geral em seu perfil). Isso é feito declarando que o &quot;[!UICONTROL Opt-Out Type]&quot; é igual a &quot;[!UICONTROL General Opt-Out]&quot; e o &quot;[!UICONTROL Opt-Out Value]&quot; é igual a &quot;[!UICONTROL Opt-in]&quot;.

![](images/opt-outs/segment-general-opt-out.png)

### Opção de rejeição de vendas/compartilhamento

Se um usuário tiver um sinalizador de recusa de vendas/compartilhamento definido em seu perfil, esse perfil não deverá mais ser usado para nenhuma criação de segmento ou atividade de marketing. Para garantir que esse sinalizador seja cumprido, o &quot;[!UICONTROL Opt-Out Type]&quot; deve ser igual a &quot;[!UICONTROL Sales Sharing Opt-Out]&quot; e o &quot;[!UICONTROL Opt-Out Value]&quot; deve ser igual a &quot;[!UICONTROL Opt-in]&quot;.

![](images/opt-outs/segment-sales-sharing-opt-out.png)

<!-- ### Overriding default exclusions

In some instances, such as building a segment of people who have opted out, it may be necessary to override the default exclusion of opted-out profiles. This override can be done via the API or in the Segment Builder user interface. -->

## Próximas etapas

Para obter mais informações sobre segmentação, incluindo o trabalho com definições de segmento e públicos-alvo por meio da API e interface do usuário, comece lendo a [visão geral da segmentação](./home.md).

Para saber mais sobre a privacidade de dados dentro de [!DNL Platform], incluindo como [!DNL Privacy Service] ajuda a facilitar a conformidade automatizada com as regulamentações legais e organizacionais de privacidade, consulte a documentação em [[!DNL Privacy Service]](../privacy-service/home.md).
