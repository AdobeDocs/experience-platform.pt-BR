---
title: Perfis de cliente potencial
description: Saiba como criar e usar perfis de prospecto para coletar informações sobre clientes desconhecidos usando informações de terceiros.
type: Documentation
exl-id: 194d25d6-88ae-4a7a-9b79-39120bced5c7
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 1%

---

# Perfis em potencial

O Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde e quando eles interagem com sua marca.

Os perfis de cliente potencial são usados para representar pessoas que ainda não se envolveram com a sua empresa, mas que você deseja contatar. Com perfis de prospecto, você pode complementar seus perfis de clientes com atributos de parceiros de terceiros confiáveis.

## Navegar {#browse}

Para acessar perfis de cliente potencial, selecione **[!UICONTROL Perfis]** na seção **[!UICONTROL Prospetos]**.

A página **[!UICONTROL Procurar]** é exibida. Uma lista de todos os perfis de cliente potencial da sua organização é exibida.

![O botão [!UICONTROL Perfis] está realçado, exibindo a página [!UICONTROL Procurar] para perfis de clientes potenciais.](../images/prospect-profile/browse-profiles.png)

>[!IMPORTANT]
>
>Embora a maioria da funcionalidade de navegação entre perfis de clientes e perfis de clientes potenciais seja a mesma, você **não pode** procurar perfis de clientes potenciais por política de mesclagem. Isso ocorre porque os perfis de clientes potenciais são regidos automaticamente por uma política de mesclagem baseada no tempo projetada pelo sistema. Mais informações sobre políticas de mesclagem podem ser encontradas na [visão geral da política de mesclagem](../merge-policies/overview.md).

Para obter mais informações sobre perfis de navegação, leia a [seção Procurar do guia do usuário Perfil](./user-guide.md#browse-identity).

## Detalhes do perfil de cliente potencial {#profile-details}

>[!IMPORTANT]
>
>Um perfil de cliente potencial expirará automaticamente após 25 dias de residência no Adobe Experience Platform.

Para exibir mais informações sobre um perfil de cliente potencial específico, selecione um perfil na página [!UICONTROL Procurar].

![Um perfil de cliente potencial está realçado na página de navegação.](../images/prospect-profile/select-specific-profile.png)

São exibidas informações sobre o perfil de cliente potencial, incluindo os atributos associados ao perfil e à associação de público-alvo.

![A página de detalhes do perfil do cliente potencial é exibida.](../images/prospect-profile/profile-details.png)

Para obter mais informações sobre essas guias, leia a [seção Exibir detalhes do perfil do Guia do usuário do perfil](./user-guide.md#profile-detail).

Você também pode ver todos os atributos no formato JSON selecionando **[!UICONTROL Exibir JSON]**.

![O botão [!UICONTROL Exibir JSON] está realçado na página de detalhes do perfil de cliente potencial.](../images/prospect-profile/profile-select-view-json.png)

A caixa de diálogo [!UICONTROL Exibir JSON] é exibida. Os atributos do perfil do cliente potencial agora são exibidos no formulário JSON.

![Os atributos do perfil do cliente potencial são exibidos no formato JSON.](../images/prospect-profile/profile-view-json.png)

## Casos de uso sugeridos {#use-cases}

Para saber como usar a funcionalidade de perfis de cliente potencial no Experience Platform em combinação com outra funcionalidade do Experience Platform, leia a seguinte documentação do caso de uso:

- [Envolver e adquirir novos clientes por meio da funcionalidade de prospecção](../../rtcdp/partner-data/prospecting.md)

## Próximas etapas

Depois de ler este guia, você entenderá como os perfis de cliente potencial podem ser usados no Adobe Experience Platform. Para saber como esses perfis de clientes potenciais podem ser usados em públicos-alvo, leia o [guia de públicos-alvo de clientes potenciais](../../segmentation/types/prospect-audiences.md).
