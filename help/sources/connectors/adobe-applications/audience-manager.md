---
keywords: 'Experience Platform;home;popular topics;conector de Audience Manager;gerenciador de Audiência;gerenciador de audiência;home;popular topics;conector de ;gerenciador de ;gerenciador de '
solution: Experience Platform
title: Visão geral do conector de origem do Audience Manager
topic: overview
description: O conector de origem Adobe Audience Manager transmite dados primários coletados no Audience Manager para a Adobe Experience Platform.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '875'
ht-degree: 0%

---


# conector Audience Manager

O conector de dados Adobe Audience Manager transmite dados primários coletados no Adobe Audience Manager para o Adobe Experience Platform. O conector Audience Manager ingere duas categorias de dados na Plataforma:

- **Dados em tempo real:** dados capturados em tempo real no servidor de coleta de dados do Audience Manager. Esses dados são usados no Audience Manager para preencher características com base em regras e aparecerão na Plataforma no menor tempo de latência.
- **Dados do perfil: o** Audience Manager usa dados em tempo real e integrados para derivar perfis do cliente. Esses perfis são usados para preencher gráficos de identidade e características nas execuções de segmentos.

O conector Audience Manager mapeia essas categorias de dados para o schema Experience Data Model (XDM) e as envia para a Plataforma. Os dados em tempo real são enviados como dados XDM ExperienceEvent, enquanto os dados do Perfil são enviados como Perfis individuais XDM.

Para obter instruções sobre como criar uma conexão com o Adobe Audience Manager usando a interface do usuário da plataforma, consulte o tutorial [conector do Audience Manager](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## O que é o Experience Data Model (XDM)?

O XDM é uma especificação documentada publicamente que fornece uma estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.

A adesão aos padrões XDM permite que os dados de experiência do cliente sejam uniformemente incorporados, facilitando a entrega de dados e a coleta de informações.

Para obter mais informações sobre como o XDM é usado no Experience Platform, consulte a [visão geral do sistema XDM](../../../xdm/home.md). Para saber mais sobre como os Schemas XDM como Perfil e ExperienceEvent estão estruturados, consulte as [noções básicas da composição do schema](../../../xdm/schema/composition.md).

## Exemplos de schemas XDM

Abaixo estão exemplos da estrutura de Audience Manager mapeada para o Perfil XDM ExperienceEvent e XDM Individual na plataforma.

### ExperienceEvent - para dados em tempo real e dados integrados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual XDM - para dados de Perfil

![](images/aam-profile-xdm-for-profile-data.png)

## Como os campos são mapeados do Adobe Audience Manager para o XDM?

Consulte a documentação dos campos de mapeamento de [Audience Manager](./mapping/audience-manager.md) para obter mais informações.

## Gestão de dados na plataforma

### Conjuntos de dados

Os conjuntos de dados são uma construção de armazenamento e gerenciamento para uma coleção de dados, geralmente uma tabela, que contém schemas (colunas) e campos (linhas) e é disponibilizada por uma conexão de dados. Os dados de Audience Manager consistem em dados em tempo real, dados de entrada e dados de Perfil. Para localizar seus conjuntos de dados de Audience Manager, use a função de pesquisa na interface do usuário com as convenções de nomenclatura fornecidas para cada tipo de dados.

Por padrão, os conjuntos de dados de Audience Manager são desativados para o Perfil e os usuários podem ativar ou desativar os conjuntos de dados com base em seus casos de uso. Não é recomendável desativar conjuntos de dados que serão usados para associação de segmentos no Perfil.

| Nome do conjunto de dados | Descrição |
| ------------ | ----------- |
| Tempo real AAM | Este conjunto de dados contém dados coletados por ocorrências diretas em pontos de extremidade DCS Audience Manager e mapas de identidade para Perfis Audience Manager. Manter este conjunto de dados ativado para ingestão de Perfis. |
| Atualizações do Perfil em tempo real AAM | Esse conjunto de dados permite o direcionamento em tempo real de características e segmentos de Audience Manager. Ele inclui informações sobre o roteamento regional do Edge, características e associação a segmentos. Manter este conjunto de dados ativado para ingestão de Perfis. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a alternância **[!UICONTROL Perfil]** para assimilar diretamente os dados ao Perfil. |
| Dados de dispositivos AAM | Dados do dispositivo com ECIDs e correspondentes execuções de segmentos agregados no Audience Manager. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a alternância **[!UICONTROL Perfil]** para assimilar diretamente os dados ao Perfil. |
| Dados do Perfil do dispositivo AAM | Usado para diagnóstico do conector de Audience Manager. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a alternância **[!UICONTROL Perfil]** para assimilar diretamente os dados ao Perfil. |
| perfis autenticados AAM | Este conjunto de dados contém perfis autenticados por Audience Manager. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a alternância **[!UICONTROL Perfil]** para assimilar diretamente os dados ao Perfil. |
| Metadados de Perfis autenticados AAM | Usado para diagnóstico do conector do Audience Manager. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a alternância **[!UICONTROL Perfil]** para assimilar diretamente os dados ao Perfil. |
| Preenchimento retroativo de dados de dispositivos AAM | O conjunto de dados não traz dados de dispositivos anteriores. Contém os ECIDs e as correspondentes realizações de segmentos agregadas em Audience Manager. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a alternância **[!UICONTROL Perfil]** para assimilar diretamente os dados ao Perfil. |
| Preenchimento retroativo de Perfis autenticados AAM | O conjunto de dados não traz dados autenticados passados. Ele contém perfis autenticados por Audience Manager. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a alternância **[!UICONTROL Perfil]** para assimilar diretamente os dados ao Perfil. |

### Conexões

A Adobe Audience Manager cria uma conexão no Catálogo: Conexão Audience Manager. Catálogo é o sistema dos registros para localização e linhagem de dados no Adobe Experience Platform. Uma conexão é um objeto de Catálogo que é uma instância específica do cliente dos Conectores. Consulte a [visão geral do serviço de catálogo](../../../catalog/home.md) para obter mais informações sobre Catálogo, conexões e conectores.

## Qual é a latência esperada para os dados de Audience Manager na plataforma?

| Dados de Audience Manager | Latência | Notas |
| --- | --- | --- |
| Dados em tempo real | &lt; 35 minutos. | O tempo de ser capturado no nó Audience Manager Edge para aparecer no Platform Data Lake. |
| dados do perfil | &lt; 2 dias | O tempo de ser capturado por meio de dados de borda DCS/PCS e dados integrados, sendo processados para um perfil do usuário, para aparecer no Perfil. Esses dados não chegam diretamente no Platform Data Lake hoje. A alternância de perfil pode ser ativada para conjuntos de dados de Perfis Audience Manager para assimilar esses dados diretamente no Perfil. |