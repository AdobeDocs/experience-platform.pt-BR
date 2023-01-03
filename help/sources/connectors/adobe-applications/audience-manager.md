---
keywords: Experience Platform, home, tópicos populares, conector de Audience Manager, Audience Manager, audience manager
solution: Experience Platform
title: Visão geral da fonte de Audience Manager
topic-legacy: overview
description: A fonte do Adobe Audience Manager transmite dados primários coletados no Audience Manager para o Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# Audience Manager

A fonte do Adobe Audience Manager transmite dados primários coletados no Adobe Audience Manager para ativação no Adobe Experience Platform. A fonte Audience Manager assimila dois tipos de dados para a Plataforma:

- **Dados em tempo real:** Dados capturados em tempo real no servidor de coleta de dados Audience Manager. Esses dados são usados no Audience Manager para preencher características com base em regras e aparecerão na Platform no menor tempo de latência.
- **Dados do perfil:** O Audience Manager usa dados integrados e em tempo real para derivar perfis de clientes. Esses perfis são usados para preencher gráficos de identidade e características em realizações de segmentos.

A fonte de Audience Manager mapeia esses tipos de dados para um esquema do Experience Data Model (XDM) e os envia para a plataforma. Os dados em tempo real são enviados como dados do ExperienceEvent XDM, enquanto os dados do perfil são enviados como dados do Perfil individual XDM.

Para obter mais informações, leia o guia sobre [criação de uma conexão Audience Manager source na interface do usuário](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## O que é o Experience Data Model (XDM)?

O XDM é uma especificação documentada publicamente que fornece uma estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.

O cumprimento dos padrões XDM permite que os dados de experiência do cliente sejam incorporados uniformemente, facilitando a entrega de dados e a coleta de informações.

Para obter mais informações sobre como o XDM é usado no Experience Platform, leia a [Visão geral do sistema XDM](../../../xdm/home.md). Para saber mais sobre como os esquemas XDM são estruturados entre perfis e eventos, leia a [noções básicas da composição do schema](../../../xdm/schema/composition.md).

## Exemplos de esquemas XDM

Abaixo estão exemplos da estrutura do Audience Manager mapeada para XDM ExperienceEvent e XDM Individual Profile na plataforma.

### ExperienceEvent - para dados em tempo real e dados integrados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual XDM - para dados de perfil

![](images/aam-profile-xdm-for-profile-data.png)

Para obter informações sobre como os campos são mapeados do Audience Manager para XDM, leia a documentação em [Campos de mapeamento Audience Manager](./mapping/audience-manager.md).

## Gerenciamento de dados na plataforma

### Conjuntos de dados

Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas) e é disponibilizada por uma conexão de dados. Os dados do Audience Manager consistem em dados em tempo real, dados de entrada e dados do perfil. Para localizar seus conjuntos de dados do Audience Manager, use a função de pesquisa na interface do usuário com as convenções de nomenclatura fornecidas para cada tipo de dados.

Por padrão, os conjuntos de dados do Audience Manager são desativados para Perfil e os usuários podem ativar ou desativar conjuntos de dados com base em seus casos de uso. Não é recomendável desativar conjuntos de dados que serão usados para associação de segmentos no Perfil.

>[!NOTE]
>
>AAM Tempo real é o único conjunto de dados que vai para o lago de dados. Todos os outros conjuntos de dados do Audience Manager vão para [!DNL Profile], se estiverem habilitados para [!DNL Profile]. Se não estiverem habilitados para [!DNL Profile], não receberão dados e serão exibidos como vazios.

| Nome do conjunto de dados | Descrição | Classe |
| --- | --- | --- |
| AAM em tempo real | Esse conjunto de dados contém dados coletados por ocorrências diretas em pontos de extremidade Audience Manager DCS e mapas de identidade para perfis Audience Manager. Mantenha esse conjunto de dados habilitado para assimilação de perfil. | Evento de experiência |
| AAM atualizações de perfil em tempo real | Esse conjunto de dados permite o direcionamento em tempo real de características e segmentos do Audience Manager. Ele inclui informações para roteamento regional do Edge, característica e associação a segmentos. Mantenha esse conjunto de dados habilitado para assimilação de perfil. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a variável **[!UICONTROL Perfil]** alternar, para assimilar diretamente os dados no Perfil. | Registro |
| Dados de dispositivos AAM | Dados do dispositivo com ECIDs e realizações de segmento correspondentes agregados no Audience Manager. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a variável **[!UICONTROL Perfil]** alternar, para assimilar diretamente os dados no Perfil. | Registro |
| Dados de perfil do dispositivo AAM | Usado para diagnóstico de conector Audience Manager. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a variável **[!UICONTROL Perfil]** alternar, para assimilar diretamente os dados no Perfil. | Registro |
| Perfis Autenticados AAM | Esse conjunto de dados contém perfis autenticados do Audience Manager. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a variável **[!UICONTROL Perfil]** alternar, para assimilar diretamente os dados no Perfil. | Registro |
| Metadados de perfis autenticados do AAM | Usado para diagnóstico Audience Manager Connector. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a variável **[!UICONTROL Perfil]** alternar, para assimilar diretamente os dados no Perfil. | Registro |
| Preenchimento retroativo de dados de dispositivos AAM | O conjunto de dados não trouxe dados de dispositivos antigos. Ele contém ECIDs e realizações de segmento correspondentes agregadas no Audience Manager. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a variável **[!UICONTROL Perfil]** alterne para assimilar diretamente os dados para Perfil. | Registro |
| AAM preenchimento retroativo de perfis autenticados | O conjunto de dados de trazer dados autenticados anteriormente. Ele contém perfis autenticados do Audience Manager. Os dados não são visíveis como lotes no conjunto de dados. Você pode ativar a variável **[!UICONTROL Perfil]** alterne para assimilar diretamente os dados para Perfil. | Registro |

### Conexões

O Adobe Audience Manager cria uma conexão no Catálogo: Conexão Audience Manager. Catálogo é o sistema dos registros para localização e linhagem de dados no Adobe Experience Platform. Uma conexão é um objeto de Catálogo que é uma instância específica do cliente de conectores. Leia o [Visão geral do serviço de catálogo](../../../catalog/home.md) para obter mais informações sobre Catálogo, conexões e conectores.

### População do segmento para impacto do perfil

Os tamanhos de preenchimento do segmento têm um impacto direto nos números de Perfil ao enviar um segmento de Audience Manager para a Plataforma pela primeira vez. Isso significa que a seleção de todos os segmentos pode causar sobreposições de perfil que excedem seu direito de uso de licença. A Platform também distingue novos dados dos dados históricos para assimilação de perfil. Um segmento com 100 identidades próprias criará 100 perfis. No entanto, se a população desse mesmo segmento foi aumentada para 150 e assimilada na Platform, o número de perfis só aumentará em 50, pois há apenas 50 novos perfis.

Também é possível verificar o uso do perfil que sua conta tem disponível por meio do [Painel de uso de licença](../../../dashboards/guides/license-usage.md).

## Qual é a latência esperada de dados do Audience Manager na plataforma?

| Audience Manager Data | Tipo | Latência | Notas |
| --- | --- | --- | --- |
| Dados em tempo real | Eventos | &lt;25 minutos | Tempo de ser capturado no nó Audience Manager Edge até aparecer no lago de dados. |
| Dados em tempo real | Atualizações do perfil | &lt;10 minutos | Hora de chegar ao Perfil do cliente em tempo real. |
| Dados integrados e em tempo real | Atualizações do perfil | 24 a 36 horas | Tempo de ser capturado por meio de dados DCS/PCS Edge e dados integrados, sendo processado para um perfil de usuário e aparecendo no Perfil do cliente em tempo real. Atualmente, esses dados não chegam diretamente ao lago de dados. A alternância de perfil pode ser ativada para conjuntos de dados de Perfil do Audience Manager para assimilar esses dados diretamente no Perfil do cliente em tempo real. |
