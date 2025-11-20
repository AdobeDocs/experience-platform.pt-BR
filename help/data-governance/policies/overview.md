---
keywords: Experience Platform;página inicial;tópicos populares;dule;DULE
solution: Experience Platform
title: Visão geral das políticas de uso de dados
description: As políticas de uso de dados são regras que descrevem os tipos de ações de marketing que você tem permissão ou restrição para executar em dados dentro do Adobe Experience Platform.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 18%

---

# Visão geral das políticas de uso de dados {#policies-overview}

>[!CONTEXTUALHELP]
>id="platform_governance_policies_restrictusage"
>title="Restringir uso de dados"
>abstract="O tipo de política de uso de dados avalia ações de marketing específicas aplicadas a rótulos de governança de dados para restringir o uso de dados para atividades de marketing."

Para que os rótulos de uso de dados sigam efetivamente a conformidade de dados, as políticas de uso de dados devem ser implementadas. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing que você tem permissão ou restrição para executar em dados no [!DNL Experience Platform].

Há dois tipos de políticas disponíveis:

* **[!UICONTROL Data governance policy]**: Restrinja a ativação de dados com base na ação de marketing que está sendo executada e nos rótulos de uso de dados transportados pelos dados em questão.
* **[!UICONTROL Consent policy]**: filtre os perfis que podem ser ativados para [destinos](../../destinations/home.md) com base no consentimento ou nas preferências dos clientes

>[!NOTE]
>
>As políticas de uso de dados não devem ser confundidas com as [políticas de controle de acesso](../../access-control/abac/end-to-end-guide.md#policy), que determinam se determinados usuários do Experience Platform em sua organização podem acessar determinados campos de dados, e são configuradas por meio da guia [!UICONTROL Permissions].

Este documento fornece uma visão geral de alto nível das políticas de uso de dados e fornece links para documentação adicional para trabalhar com políticas na interface ou na API.

## Ações de marketing {#marketing-actions}

As ações de marketing (também chamadas de casos de uso de marketing) no contexto da estrutura de governança de dados são ações que um consumidor de dados [!DNL Experience Platform] pode realizar e para as quais sua organização deseja restringir o uso de dados. Dessa forma, uma política de uso de dados é definida pelo seguinte:

1. Uma ação de marketing específica
2. As condições em que essa ação está impedida de ser executada

Um exemplo de ação de marketing pode ser o desejo de exportar um conjunto de dados para um serviço de terceiros. Se houver uma política em vigor informando que tipos específicos de dados (como Informações de identificação pessoal (PII)) não podem ser exportados e você tentar exportar um conjunto de dados que contenha um rótulo &quot;I&quot; (Dados de identidade), você receberá uma resposta do [!DNL Policy Service] informando que uma política de uso de dados foi violada.

>[!NOTE]
>
>As ações de marketing por si só não restringem o uso de dados. Eles devem ser incluídos em políticas ativadas de uso de dados para que essas ações sejam avaliadas quanto a violações de política.

Quando o uso de dados ocorrer no serviço de sua organização, ações de marketing relevantes devem ser indicadas para que qualquer violação de política possa ser identificada. Você pode usar a [API de Serviço de Política](https://www.adobe.io/experience-platform-apis/references/policy-service/) para verificar se há violações de política na sua integração.

>[!NOTE]
>
>Você pode configurar casos de uso de marketing em destinos para automatizar a aplicação de políticas. Consulte a [documentação de destinos](../../destinations/home.md) para obter mais informações sobre as opções de configuração para seu destino específico.

Consulte o apêndice deste documento para obter uma lista de [ações de marketing definidas pela Adobe disponíveis](#core-actions). Você também pode definir suas próprias ações de marketing personalizadas usando a API [!DNL Policy Service] ou a interface do usuário [!DNL Experience Platform]. Mais informações sobre como trabalhar com ações e políticas de marketing são fornecidas na próxima seção.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share audiences with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager audiences are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Experience Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Gerenciamento de políticas de uso de dados {#manage}

Depois que os rótulos de uso de dados forem aplicados, os administradores de dados poderão usar a API [!DNL Policy Service] ou a interface do usuário [!DNL Experience Platform] para gerenciar e avaliar as políticas relacionadas às ações de marketing que estão sendo executadas nos dados que contêm rótulos de uso de dados. Você pode criar e atualizar políticas, determinar o status de uma política e trabalhar com ações de marketing para avaliar se uma ação específica viola uma política de uso de dados.

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para aplicação, é necessário habilitar manualmente essa política por meio da API ou da interface.

Para obter instruções passo a passo sobre como trabalhar com ações de marketing e políticas de uso de dados na API, consulte o tutorial em [criação e avaliação de políticas de uso de dados](create.md). Para obter mais informações sobre as principais operações fornecidas pela API [!DNL Policy Service], consulte o [Guia do desenvolvedor do Serviço de Política](../api/getting-started.md).

Para obter informações sobre como trabalhar com ações e políticas de marketing na interface do usuário do [!DNL Experience Platform], consulte o [guia do usuário da política de uso de dados](./user-guide.md).

## Próximas etapas

Este documento forneceu uma introdução às políticas de uso de dados na estrutura de governança de dados. Agora você pode continuar lendo a documentação do processo vinculada a este guia para saber mais sobre como trabalhar com políticas na API e na interface do usuário.

## Apêndice

A seção a seguir fornece informações adicionais sobre as políticas de uso de dados.

### Ações de marketing definidas pela Adobe {#core-actions}

A tabela abaixo descreve as principais ações de marketing fornecidas prontas para uso pelo Adobe.

>[!NOTE]
>
>As principais ações de marketing devem ser vistas como um ponto de partida para ajudar a identificar quais políticas de uso criar e verificar violações. As definições e a forma como são interpretadas dependem das necessidades e políticas da organização.

| Ação de marketing | Descrição |
| --- | --- |
| Analytics | Uma ação que usa dados para fins de análise, como medir, analisar e gerar relatórios sobre o uso que os clientes fazem dos sites ou aplicativos de sua organização. |
| Combinar com dados diretamente identificáveis | Uma ação que combina Informações de identificação pessoal (PII) com dados anônimos. Os contratos para dados obtidos de redes de publicidade, servidores de publicidade e provedores de dados de terceiros geralmente incluem proibições contratuais específicas sobre o uso desses dados com dados diretamente identificáveis. |
| Direcionamento entre sites | Uma ação que usa dados para o direcionamento de anúncios entre sites. A combinação de dados de vários sites, incluindo uma combinação de dados internos e externos ou uma combinação de dados de várias fontes externas, é chamada de dados entre sites. Normalmente, os dados entre sites são coletados e processados para deduzir os interesses dos usuários. |
| Ciência de dados | Uma ação que usa dados de fluxos de trabalho de ciência de dados. Alguns contratos incluem proibições explícitas sobre o uso de dados para ciência de dados. Às vezes, essas proibições são realizadas em forma de cláusulas que proíbem o uso de dados para Inteligência artificial (IA), aprendizado de máquina (ML) ou modelagem. |
| Exportação de dados | Uma ação que exporta dados para qualquer local ou destino fora dos produtos e serviços da Adobe. Por exemplo, baixar dados para o computador local, copiar dados da tela, agendar a entrega de dados para um local fora do Adobe, Customer Journey Analytics Scheduled Projects, Baixar relatórios, API de relatórios e assim por diante. |
| Direcionamento de email | Uma ação que usa dados em campanhas de direcionamento por email. |
| Exportar para terceiros | Uma ação que exporta dados para processadores e entidades que não têm um relacionamento direto com os clientes. Muitos provedores de dados têm cláusulas nos contratos que proíbem a exportação de dados de onde foram originalmente coletados. Por exemplo, os contratos de redes sociais geralmente restringem a transferência de dados recebidos delas. |
| Advertising no local | Uma ação que usa dados para a adição de anúncios no site, incluindo a seleção e a entrega de anúncios nos sites ou aplicativos da organização, ou para medir a entrega e a eficácia desses anúncios. |
| Personalization no local | Uma ação que usa dados para a personalização de conteúdo no site. A personalização no local são quaisquer dados usados para deduzir os interesses dos usuários e são usados para selecionar qual conteúdo ou quais anúncios são veiculados com base nessas deduções. |
| Correspondência de segmentos | Uma ação que usa dados para a Correspondência de segmentos do Adobe Experience Platform, o que permite que dois ou mais usuários do Experience Platform troquem dados de público-alvo. Ao ativar políticas que fazem referência a essa ação, é possível restringir quais dados são usados para a Correspondência de segmentos. Por exemplo, se a política principal &quot;Restringir compartilhamento de dados&quot; estiver habilitada, os dados com um rótulo [C11](../labels/reference.md#c11) não poderão ser usados para a Correspondência de Segmentos. |
| Personalization de identidade única | Uma ação que requer que uma única identidade seja usada para fins de personalização, em vez de compilar identidades de várias fontes. |
