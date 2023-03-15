---
keywords: Experience Platform;página inicial;tópicos populares;conector de Audience Manager;Audience manager;audience manager
solution: Experience Platform
title: Visão geral da origem do Audience Manager
description: A origem do Adobe Audience Manager transmite dados primários coletados no Audience Manager para o Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: 59dfa862388394a68630a7136dee8e8988d0368c
workflow-type: tm+mt
source-wordcount: '1059'
ht-degree: 0%

---

# origem do Audience Manager

A origem do Adobe Audience Manager transmite dados primários coletados no Adobe Audience Manager para ativação no Adobe Experience Platform. A fonte de Audience Manager assimila dois tipos de dados para a Platform:

- **Dados em tempo real:** Dados capturados em tempo real no servidor de coleta de dados do Audience Manager. Esses dados são usados no Audience Manager para preencher características com base em regras e aparecerão na Platform no menor tempo de latência.
- **Dados do perfil:** O Audience Manager usa dados integrados e em tempo real para derivar perfis de clientes. Esses perfis são usados para preencher gráficos de identidade e características nas realizações do segmento.

A fonte de Audience Manager mapeia esses tipos de dados para um esquema do Experience Data Model (XDM) e os envia para a Platform. Os dados em tempo real são enviados como dados XDM ExperienceEvent, enquanto os dados de perfil são enviados como dados de perfil individual XDM.

Para obter mais informações, leia o guia em [criação de uma conexão de origem de Audience Manager na interface](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## O que é o Experience Data Model (XDM)?

O XDM é uma especificação documentada publicamente que fornece uma estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.

A adesão aos padrões XDM permite que os dados de experiência do cliente sejam incorporados uniformemente, facilitando a entrega de dados e a coleta de informações.

Para obter mais informações sobre como o XDM é usado no Experience Platform, leia o [Visão geral do sistema XDM](../../../xdm/home.md). Para saber mais sobre como os esquemas XDM são estruturados entre perfis e eventos, leia o [noções básicas da composição do esquema](../../../xdm/schema/composition.md).

## Exemplos de esquemas XDM

Abaixo estão exemplos da estrutura de Audience Manager mapeada para o ExperienceEvent XDM e o Perfil individual XDM na plataforma.

### ExperienceEvent - para dados em tempo real e dados integrados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual XDM - para dados de perfil

![](images/aam-profile-xdm-for-profile-data.png)

Para obter informações sobre como os campos são mapeados do Audience Manager para o XDM, leia a documentação em [campos de mapeamento de Audience Manager](./mapping/audience-manager.md).

## Gerenciamento de dados na plataforma

### Conjuntos de dados

Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas) e é disponibilizada por uma conexão de dados. Os dados de Audience Manager consistem em dados em tempo real, dados de entrada e dados de Perfil. Para localizar seus conjuntos de dados de Audience Manager, use a função de pesquisa na interface do usuário com as convenções de nomenclatura fornecidas para cada tipo de dados.

Os conjuntos de dados do Audience Manager são desativados para Perfil por padrão e os usuários têm a capacidade de ativar ou desativar conjuntos de dados com base em seus casos de uso. Não é recomendável desativar conjuntos de dados que serão usados para associação de segmento no Perfil.

>[!NOTE]
>
>O Tempo real do AAM é o único conjunto de dados que vai para o data lake. Todos os outros conjuntos de dados de Audience Manager vão para [!DNL Profile], se estiverem ativados para [!DNL Profile]. Se não estiverem ativados para [!DNL Profile], eles não receberão nenhum dado e serão exibidos como vazios.

| Nome do conjunto de dados | Descrição | Classe |
| --- | --- | --- |
| AAM em tempo real | Esse conjunto de dados contém dados coletados por ocorrências diretas em pontos de extremidade do Audience Manager DCS e mapas de identidade para Perfis de Audience Manager. Mantenha esse conjunto de dados habilitado para assimilação de perfil. | Evento de experiência |
| Atualizações de perfil do AAM em tempo real | Esse conjunto de dados permite o direcionamento em tempo real de características e segmentos de Audience Manager. Inclui informações para o roteamento regional, características e associação de segmento do Edge. Mantenha esse conjunto de dados habilitado para assimilação de perfil. Os dados não estão visíveis como lotes no conjunto de dados. Você pode ativar o **[!UICONTROL Perfil]** alternar, para assimilar os dados diretamente no Perfil. | Gravar |
| Dados de dispositivos AAM | Dados do dispositivo com ECIDs e realizações de segmento correspondentes agregados em Audience Manager. Os dados não estão visíveis como lotes no conjunto de dados. Você pode ativar o **[!UICONTROL Perfil]** alternar, para assimilar os dados diretamente no Perfil. | Gravar |
| Dados de perfil do dispositivo AAM | Usado para diagnósticos do conector Audience Manager. Os dados não estão visíveis como lotes no conjunto de dados. Você pode ativar o **[!UICONTROL Perfil]** alternar, para assimilar os dados diretamente no Perfil. | Gravar |
| Perfis autenticados por AAM | Este conjunto de dados contém perfis autenticados Audience Manager. Os dados não estão visíveis como lotes no conjunto de dados. Você pode ativar o **[!UICONTROL Perfil]** alternar, para assimilar os dados diretamente no Perfil. | Gravar |
| Metadados de perfis autenticados por AAM | Usado para diagnósticos do conector de Audience Manager. Os dados não estão visíveis como lotes no conjunto de dados. Você pode ativar o **[!UICONTROL Perfil]** alternar, para assimilar os dados diretamente no Perfil. | Gravar |
| Preenchimento retroativo de dados de dispositivos AAM | Conjunto de dados que traz dados de dispositivos anteriores. Ela contém ECIDs e realizações de segmento correspondentes agregados em Audience Manager. Os dados não estão visíveis como lotes no conjunto de dados. Você pode ativar o **[!UICONTROL Perfil]** Alterne para assimilar os dados diretamente no Perfil. | Gravar |
| Preenchimento retroativo de perfis autenticados por AAM | Conjunto de dados de trazer dados autenticados anteriores. Ele contém perfis autenticados Audience Manager. Os dados não estão visíveis como lotes no conjunto de dados. Você pode ativar o **[!UICONTROL Perfil]** Alterne para assimilar os dados diretamente no Perfil. | Gravar |

### Conexões

O Adobe Audience Manager cria uma conexão no Catálogo: Audience Manager Connection. Catálogo é o sistema de registros para localização e linhagem de dados no Adobe Experience Platform. Uma conexão é um objeto de Catálogo que é uma instância de conectores específica do cliente. Leia as [Visão geral do Serviço de catálogo](../../../catalog/home.md) para obter mais informações sobre Catálogo, conexões e conectores.

### População do segmento para impacto do perfil

Os tamanhos de preenchimento de segmento têm um impacto direto nos números de perfil quando você envia um segmento de Audience Manager para a Platform pela primeira vez. Isso significa que selecionar todos os segmentos pode causar sobreposições de perfil que excedem seus direitos de uso de licença. A Platform também distingue novos dados de dados históricos para assimilação de perfis. Um segmento com 100 identidades primárias criará 100 perfis. No entanto, se a população desse mesmo segmento foi aumentada para 150 e foi assimilada na Platform, o número de perfis só aumentará em 50, pois há apenas 50 novos perfis.

Você também pode verificar o uso do perfil que sua conta tem disponível por meio da [Painel de Uso da Licença](../../../dashboards/guides/license-usage.md).

## Qual é a latência esperada para dados de Audience Manager na plataforma?

| Dados do Audience Manager | Tipo | Latência | Notas |
| --- | --- | --- | --- |
| Dados em tempo real | Eventos | &lt;25 minutos | Tempo desde a captura no nó Audience Manager Edge até a exibição no data lake. |
| Dados em tempo real | Atualizações de perfil | &lt;10 minutos | Tempo de acesso ao Perfil do cliente em tempo real. |
| Dados integrados e em tempo real | Atualizações de perfil | 24 a 36 horas | Tempo desde a captura pelos dados de borda e dados integrados do DCS/PCS, processamento em um perfil de usuário até a exibição no Perfil do cliente em tempo real. Atualmente, esses dados não chegam diretamente ao data lake. A alternância de perfil pode ser ativada para conjuntos de dados de perfil do Audience Manager para assimilar esses dados diretamente no Perfil do cliente em tempo real. |
