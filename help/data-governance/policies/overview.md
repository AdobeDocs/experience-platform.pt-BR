---
keywords: Experience Platform;home;popular topics;dule;DULE
solution: Experience Platform
title: Visão geral das políticas de uso de dados
topic: policies
description: Para que os rótulos de uso de dados suportem de forma eficaz a conformidade dos dados, as políticas de uso de dados devem ser implementadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados no Experience Platform.
translation-type: tm+mt
source-git-commit: c081a7521be9715ca32d35504922a70767924fd7
workflow-type: tm+mt
source-wordcount: '1007'
ht-degree: 0%

---


# Visão geral das políticas de uso de dados

Para que os rótulos de uso de dados suportem de forma eficaz a conformidade dos dados, as políticas de uso de dados devem ser implementadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing às quais você tem permissão ou é restrito para executar em dados dentro de [!DNL Experience Platform].

Este documento fornece uma visão geral de alto nível das políticas de uso de dados e fornece links para documentação adicional para trabalhar com políticas na interface do usuário ou na API.

## Ações de marketing {#marketing-actions}

**As ações** de marketing (também chamadas de casos **de uso de** marketing) no contexto da estrutura de controle de dados são ações que um consumidor de [!DNL Experience Platform] dados pode realizar, para as quais sua organização deseja restringir o uso de dados. Dessa forma, uma política de uso de dados é definida pelo seguinte:

1. Uma ação de marketing específica
2. Os rótulos de uso de dados com os quais a ação está restrita não são executados

Um exemplo de uma ação de marketing pode ser o desejo de exportar um conjunto de dados para um serviço de terceiros. Se houver uma política em vigor dizendo que tipos específicos de dados (como Informações pessoais identificáveis (PII)) não podem ser exportados e você tentar exportar um conjunto de dados que contenha um rótulo &quot;I&quot; (Dados de identidade), você receberá uma resposta da [!DNL Policy Service] informando que uma política de uso de dados foi violada.

>[!NOTE]
>
>As ações de marketing por si só não restringem o uso de dados. Eles devem ser incluídos nas políticas de uso de dados habilitadas para que essas ações sejam avaliadas em caso de violação de política.

Quando o uso de dados ocorre no serviço de sua organização, as ações de marketing relevantes devem ser indicadas para que qualquer violação de política possa ser identificada. Em seguida, você pode usar a API [do serviço de política](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/dule-policy-service.yaml) DULE para verificar violações de política na sua integração.

>[!NOTE]
>
>Se estiver usando [!DNL Real-time Customer Data Platform], você pode configurar casos de uso de marketing em destinos para automatizar a aplicação de políticas. Consulte o documento sobre o controle de [dados na CDP](../../rtcdp/privacy/data-governance-overview.md) em tempo real para obter mais informações.

Consulte o apêndice deste documento para obter uma lista de ações [](#core-actions)de marketing definidas por Adobe. Você também pode definir suas próprias ações de marketing personalizadas usando a DULE [!DNL Policy Service] API ou a interface [!DNL Experience Platform ]do usuário. Mais informações sobre como trabalhar com ações e políticas de marketing são fornecidas na próxima seção.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://docs.adobe.com/content/help/en/audience-manager/user-guide/features/data-export-controls.html).
-->

## Gerenciamento de políticas de uso de dados {#manage}

Depois que os rótulos de uso de dados forem aplicados, os administradores de dados poderão usar a API DULE [!DNL Policy Service] ou a [!DNL Experience Platform] interface do usuário para gerenciar e avaliar as políticas relacionadas às ações de marketing que estão sendo executadas nos dados que contêm os rótulos de uso de dados. Você pode criar e atualizar políticas, determinar o status de uma política e trabalhar com ações de marketing para avaliar se uma ação específica viola uma política de uso de dados.

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, é necessário ativar essa política manualmente por meio da API ou da interface do usuário.

Para obter instruções passo a passo sobre como trabalhar com ações de marketing e políticas de uso de dados na API, consulte o tutorial sobre como [criar e avaliar políticas](create.md)de uso de dados. Para obter mais informações sobre as principais operações fornecidas pela [!DNL Policy Service] API, consulte o guia [do desenvolvedor do Serviço de](../api/getting-started.md)Políticas.

Para obter informações sobre como trabalhar com ações e políticas de marketing na [!DNL Platform] interface do usuário, consulte o guia [do usuário da política de uso de](./user-guide.md)dados.

## Próximas etapas

Este documento forneceu uma introdução às políticas de uso de dados na estrutura DULE. Agora você pode continuar a ler a documentação do processo vinculada ao longo deste guia para saber mais sobre como trabalhar com políticas na API e na interface do usuário.

## Apêndice

A seção a seguir fornece informações adicionais sobre as políticas de uso de dados.

### Ações de marketing definidas pelo Adobe {#core-actions}

A tabela abaixo descreve as principais ações de marketing fornecidas prontamente por Adobe.

>[!NOTE]
>
>As ações principais de marketing devem ser vistas como um ponto de partida para ajudá-lo a identificar quais políticas de uso criar e verificar violações. As definições e a forma como são interpretadas dependem das necessidades e políticas de sua organização.

| Ação de marketing | Descrição |
| --- | --- |
| Analytics | Uma ação que usa dados para fins de análise, como medição, análise e relatórios do uso pelos clientes dos sites ou aplicativos de sua organização. |
| Combinar com PII | Uma ação que combina informações pessoais identificáveis (PII) com dados anônimos. Os contratos para dados provenientes de redes de anúncios, servidores de anúncios e provedores de dados de terceiros geralmente incluem proibições contratuais específicas sobre o uso desses dados com dados diretamente identificáveis. |
| Definição de metas entre sites | Uma ação que usa dados para direcionamento de anúncios entre sites. A combinação de dados de vários sites, incluindo uma combinação de dados no local e dados fora do local ou uma combinação de dados de várias fontes fora do local, é chamada de dados entre sites. Os dados entre sites normalmente são coletados e processados para fazer inferências sobre os interesses dos usuários. |
| Ciência de dados | Uma ação que usa dados para workflows de ciência de dados. Alguns contratos incluem proibições explícitas sobre a utilização de dados para a ciência de dados. Às vezes, são redigidos em termos que proíbem o uso de dados para Inteligência Artificial (AI), aprendizado de máquina (ML) ou modelagem. |
| Direcionamento de email | Uma ação que usa dados em campanhas de direcionamento de email. |
| Exportar para terceiros | Uma ação que exporta dados para processadores e entidades que não têm relações diretas com os clientes. Muitos fornecedores de dados têm termos nos contratos que proíbem a exportação de dados de onde foram originalmente recolhidos. Por exemplo, os contratos de rede social muitas vezes restringem a transferência de dados que você recebe deles. |
| Anúncios no site | Uma ação que usa dados para anúncios no site, incluindo a seleção e o delivery de anúncios nos sites ou aplicativos de sua organização, ou para medir o delivery e a eficácia desses anúncios. |
| Personalização no site | Uma ação que usa dados para personalização de conteúdo no site. A personalização no site é qualquer dado usado para fazer inferências sobre os interesses dos usuários e é usado para selecionar qual conteúdo ou anúncios são fornecidos com base nessas inferências. |
| Personalização de identidade única | Uma ação que exige que uma única identidade seja usada para fins de personalização, em vez de unir identidades de várias fontes. |
