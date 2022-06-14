---
keywords: Experience Platform, home, tópicos populares, dule, DULE
solution: Experience Platform
title: Visão geral das políticas de uso de dados
topic-legacy: policies
description: Para que os rótulos de uso de dados sejam compatíveis com a conformidade dos dados, é necessário implementar políticas de uso de dados. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing das quais você tem permissão para ou tem restrição para executar em dados dentro do Experience Platform.
exl-id: 1b372aa5-3e49-4741-82dc-5701a4bc8469
source-git-commit: 0c78b5dc420a1346c92bf9ed7864fa1733422a83
workflow-type: tm+mt
source-wordcount: '1121'
ht-degree: 0%

---

# Visão geral das políticas de uso de dados

Para que os rótulos de uso de dados sejam compatíveis com a conformidade dos dados, é necessário implementar políticas de uso de dados. As políticas de uso de dados são regras que descrevem os tipos de ações de marketing das quais você tem permissão para ou tem restrição para executar em dados dentro de [!DNL Experience Platform].

Há dois tipos de políticas disponíveis:

* **[!UICONTROL Política de gestão de dados]**: Restrinja a ativação de dados com base na ação de marketing que está sendo executada e nos rótulos de uso de dados transportados pelos dados em questão.
* **[!UICONTROL Política de consentimento]**: Filtre os perfis que podem ser ativados para [destinos](../../destinations/home.md) com base no consentimento ou nas preferências dos clientes

Este documento fornece uma visão geral de alto nível das políticas de uso de dados e fornece links para documentação adicional sobre como trabalhar com políticas na interface do usuário ou na API.

## Ações de marketing {#marketing-actions}

As ações de marketing (também chamadas de casos de uso de marketing) no contexto da estrutura de governança de dados são ações que [!DNL Experience Platform] o consumidor de dados pode assumir, para o qual sua organização deseja restringir o uso de dados. Dessa forma, uma política de uso de dados é definida pelo seguinte:

1. Uma ação de marketing específica
2. As condições em que essa ação é limitada ao exercício

Um exemplo de uma ação de marketing pode ser o desejo de exportar um conjunto de dados para um serviço de terceiros. Se houver uma política em vigor informando que tipos específicos de dados (como Informações pessoais identificáveis (PII)) não podem ser exportados e você tentar exportar um conjunto de dados que contenha um rótulo &quot;I&quot; (Dados de identidade), você receberá uma resposta da [!DNL Policy Service] informando que uma política de uso de dados foi violada.

>[!NOTE]
>
>As ações de marketing por si só não restringem o uso de dados. Eles devem ser incluídos nas políticas de uso de dados ativadas para que essas ações sejam avaliadas em caso de violações de política.

Quando o uso de dados ocorre no serviço da organização, as ações de marketing relevantes devem ser indicadas para que qualquer violação de política possa ser identificada. Em seguida, você pode usar o [API do serviço de política](https://www.adobe.io/experience-platform-apis/references/policy-service/) para verificar violações de política na integração.

>[!NOTE]
>
>Você pode configurar casos de uso de marketing em destinos para automatizar a aplicação de políticas. Consulte a [documentação de destinos](../../destinations/home.md) para obter mais informações sobre as opções de configuração para seu destino específico.

Ver o apêndice a este documento para obter uma lista de [ações de marketing disponíveis definidas pelo Adobe](#core-actions). Você também pode definir suas próprias ações de marketing personalizadas usando o [!DNL Policy Service] API ou [!DNL Experience Platform] interface do usuário. Mais informações sobre como trabalhar com ações e políticas de marketing são fornecidas na próxima seção.

<!-- (Add after AAM DEC mapping doc is published)
### Inheritance from Adobe Audience Manager Data Export Controls

Experience Platform has the ability to share segments with Adobe Audience Manager. Any Data Export Controls that have been applied to Audience Manager segments are translated to equivalent marketing use cases recognized by Experience Platform Data Governance.

For a reference on how specific Data Export Controls map to marketing actions in Platform, please refer to the [Audience Manager documentation](https://experienceleague.adobe.com/docs/audience-manager/user-guide/features/data-export-controls.html).
-->

## Gerenciamento de políticas de uso de dados {#manage}

Depois que os rótulos de uso de dados forem aplicados, os assistentes de dados poderão usar o [!DNL Policy Service] API ou [!DNL Experience Platform] Interface do usuário para gerenciar e avaliar políticas relacionadas às ações de marketing que estão sendo executadas em dados que contêm rótulos de uso de dados. Você pode criar e atualizar políticas, determinar o status de uma política e trabalhar com ações de marketing para avaliar se uma ação específica viola uma política de uso de dados.

>[!IMPORTANT]
>
>Todas as políticas de uso de dados (incluindo as políticas principais fornecidas pelo Adobe) são desativadas por padrão. Para que uma política individual seja considerada para imposição, você deve habilitar manualmente essa política por meio da API ou da interface do usuário.

Para obter instruções passo a passo sobre como trabalhar com ações de marketing e políticas de uso de dados na API, consulte o tutorial em [criação e avaliação de políticas de uso de dados](create.md). Para obter mais informações, as principais operações fornecidas pela [!DNL Policy Service] API, consulte o [Guia do desenvolvedor do Serviço de políticas](../api/getting-started.md).

Para obter informações sobre como trabalhar com ações e políticas de marketing no [!DNL Platform] interface do usuário, consulte a [guia do usuário da política de uso de dados](./user-guide.md).

## Próximas etapas

Este documento forneceu uma introdução às políticas de uso de dados dentro da estrutura de Governança de dados. Agora você pode continuar a ler a documentação do processo vinculada a este guia para saber mais sobre como trabalhar com políticas na API e na interface do usuário.

## Apêndice

A seção a seguir fornece informações adicionais sobre as políticas de uso de dados.

### Ações de marketing definidas por Adobe {#core-actions}

A tabela abaixo descreve as principais ações de marketing fornecidas prontas para uso pelo Adobe.

>[!NOTE]
>
>As ações principais de marketing devem ser vistas como um ponto de partida para ajudar a identificar quais políticas de uso devem ser criadas e verificar se há violações. As definições e a forma como são interpretadas dependem das necessidades e políticas de sua organização.

| Ação de marketing | Descrição |
| --- | --- |
| Analytics | Uma ação que usa dados para fins de análise, como medir, analisar e criar relatórios sobre o uso pelos clientes dos sites ou aplicativos de sua organização. |
| Combinar com dados diretamente identificáveis | Uma ação que combina informações pessoais identificáveis (PII) com dados anônimos. Os contratos para dados provenientes de redes de anúncios, servidores de anúncios e provedores de dados de terceiros frequentemente incluem proibições contratuais específicas sobre o uso desses dados com dados diretamente identificáveis. |
| Direcionamento entre sites | Uma ação que usa dados para o direcionamento de anúncios entre sites. A combinação de dados de vários sites, incluindo uma combinação de dados no local e dados fora do site ou uma combinação de dados de várias fontes fora do site, é chamada de dados entre sites. Os dados entre sites geralmente são coletados e processados para fazer inferências sobre os interesses dos usuários. |
| Ciência de dados | Uma ação que usa dados para fluxos de trabalho da ciência de dados. Alguns contratos incluem proibições explícitas sobre a utilização de dados para a ciência de dados. Às vezes, elas são redigidas em termos que proíbem o uso de dados para Inteligência Artificial (AI), aprendizado de máquina (ML) ou modelagem. |
| Direcionamento de email | Uma ação que usa dados em campanhas de segmentação de email. |
| Exportar para Terceiros | Uma ação que exporta dados para processadores e entidades que não têm relacionamento direto com os clientes. Muitos provedores de dados têm termos nos contratos que proíbem a exportação de dados de onde eles foram coletados originalmente. Por exemplo, os contratos de rede social geralmente restringem a transferência de dados que você recebe deles. |
| Publicidade no site | Uma ação que usa dados para anúncios no site, incluindo a seleção e a entrega de anúncios nos sites ou aplicativos de sua organização, ou para medir a entrega e a eficácia de tais anúncios. |
| Personalização no site | Uma ação que usa dados para personalização de conteúdo no site. A personalização no site é qualquer dado usado para fazer inferências sobre os interesses dos usuários e é usado para selecionar qual conteúdo ou anúncios são exibidos com base nessas inferências. |
| Correspondência de segmentos | Uma ação que usa dados para a Correspondência de segmentos do Adobe Experience Platform, que permite que dois ou mais usuários da Plataforma troquem dados de segmentos. Ao ativar as políticas que fazem referência a essa ação, é possível restringir quais dados são usados para a Correspondência de segmentos. Por exemplo, se a política principal &quot;Restringir o compartilhamento de dados&quot; estiver ativada, quaisquer dados com uma [Rótulo C11](../labels/reference.md#c11) não pode ser usado para Correspondência de segmentos. |
| Personalização de identidade única | Uma ação que requer que uma única identidade seja usada para fins de personalização, em vez de compilar identidades de várias fontes. |
