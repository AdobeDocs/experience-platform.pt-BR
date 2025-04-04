---
keywords: Experience Platform;página inicial;tópicos populares;conector do Audience Manager;Audience manager;audience manager
solution: Experience Platform
title: Visão geral do Audience Manager Source
description: A origem do Adobe Audience Manager transmite dados primários coletados no Audience Manager para o Adobe Experience Platform.
exl-id: be90db33-69e1-4f42-9d1a-4f8f26405f0f
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1137'
ht-degree: 1%

---

# Origem do Audience Manager

>[!IMPORTANT]
>
>Na configuração inicial, a origem Adobe Audience Manager retorna uma mensagem de erro que explica que um namespace de identidade com determinado `namespaceCode={VALUE}` não existe. **Observação**: no back-end, `namespaceCode` é usado para fazer referência ao símbolo de identidade. Para concluir a integração, você deve:
>
>- [Crie um namespace personalizado no Serviço de Identidade](../../../identity-service/features/namespaces.md#create-custom-namespaces) com o símbolo de identidade especificado (`VALUE`).
>- Assimile novamente seus dados.

A origem do Adobe Audience Manager transmite dados primários coletados no Adobe Audience Manager para ativação no Adobe Experience Platform. A fonte do Audience Manager assimila dois tipos de dados para o Experience Platform:

- **Dados em tempo real:** dados capturados em tempo real no servidor de coleta de dados da Audience Manager. Esses dados são usados no Audience Manager para preencher características com base em regras e aparecerão no Experience Platform no menor tempo de latência.
- **Dados do perfil:** o Audience Manager usa dados integrados e em tempo real para derivar perfis de clientes. Esses perfis são usados para preencher gráficos de identidade e características nas realizações do segmento.

A origem do Audience Manager mapeia esses tipos de dados para um esquema do Experience Data Model (XDM) e os envia para a Experience Platform. Os dados em tempo real são enviados como dados XDM ExperienceEvent, enquanto os dados de perfil são enviados como dados de perfil individual XDM.

Para obter mais informações, leia o manual sobre [criação de uma conexão de origem do Audience Manager na interface](../../tutorials/ui/create/adobe-applications/audience-manager.md).

## O que é o Experience Data Model (XDM)?

O XDM é uma especificação documentada publicamente que fornece uma estrutura padronizada pela qual a Experience Platform organiza os dados de experiência do cliente.

A adesão aos padrões XDM permite que os dados de experiência do cliente sejam incorporados uniformemente, facilitando a entrega de dados e a coleta de informações.

Para obter mais informações sobre como o XDM é usado no Experience Platform, leia a [Visão geral do sistema XDM](../../../xdm/home.md). Para saber mais sobre como os esquemas XDM são estruturados entre perfis e eventos, leia as [noções básicas da composição de esquema](../../../xdm/schema/composition.md).

## Exemplos de esquemas XDM

Abaixo estão exemplos da estrutura do Audience Manager mapeada para o ExperienceEvent XDM e o Perfil individual XDM no Experience Platform.

### ExperienceEvent - para dados em tempo real e dados integrados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual XDM - para dados de perfil

![](images/aam-profile-xdm-for-profile-data.png)

Para obter informações sobre como os campos são mapeados do Audience Manager para o XDM, leia a documentação em [campos de mapeamento do Audience Manager](./mapping/audience-manager.md).

## Gerenciamento de dados no Experience Platform

### Conjuntos de dados

Um conjunto de dados é uma construção de armazenamento e gerenciamento para uma coleção de dados, normalmente uma tabela, que contém um esquema (colunas) e campos (linhas) e é disponibilizada por uma conexão de dados. Os dados do Audience Manager consistem em dados em tempo real, dados de entrada e dados de perfil. Para localizar seus conjuntos de dados do Audience Manager, use a função de pesquisa na interface do usuário com as convenções de nomenclatura fornecidas para cada tipo de dados.

Por padrão, os conjuntos de dados do Audience Manager são desativados para o Perfil e os usuários têm a capacidade de ativar ou desativar conjuntos de dados com base em seus casos de uso. Não é recomendável desativar conjuntos de dados que serão usados para associação de segmento no Perfil.

>[!NOTE]
>
>O Tempo real da AAM é o único conjunto de dados que vai para o data lake. Todos os outros conjuntos de dados do Audience Manager vão para [!DNL Profile], se estiverem habilitados para [!DNL Profile]. Se não estiverem habilitados para [!DNL Profile], eles não receberão nenhum dado e serão exibidos como vazios.

| Nome do conjunto de dados | Descrição | Classe |
| --- | --- | --- |
| AAM em tempo real | Esse conjunto de dados contém dados coletados por ocorrências diretas em pontos de extremidade do Audience Manager DCS e mapas de identidade para perfis do Audience Manager. Mantenha esse conjunto de dados habilitado para assimilação de perfil. | Evento de experiência |
| Atualizações de perfil em tempo real do AAM | Esse conjunto de dados permite o direcionamento em tempo real de características e segmentos do Audience Manager. Inclui informações para o roteamento regional, características e associação de segmento da Edge. Mantenha esse conjunto de dados habilitado para assimilação de perfil. Os dados não estão visíveis como lotes no conjunto de dados. Você pode habilitar a opção de alternância **[!UICONTROL Perfil]** para assimilar os dados diretamente no Perfil. | Registro |
| Dados de dispositivos AAM | Dados do dispositivo com ECIDs e realizações de segmento correspondentes agregados no Audience Manager. Os dados não estão visíveis como lotes no conjunto de dados. Você pode habilitar a opção de alternância **[!UICONTROL Perfil]** para assimilar os dados diretamente no Perfil. | Registro |
| Dados de perfil do dispositivo AAM | Usado para diagnósticos do conector Audience Manager. Os dados não estão visíveis como lotes no conjunto de dados. Você pode habilitar a opção de alternância **[!UICONTROL Perfil]** para assimilar os dados diretamente no Perfil. | Registro |
| Perfis autenticados do AAM | Este conjunto de dados contém perfis autenticados do Audience Manager. Os dados não estão visíveis como lotes no conjunto de dados. Você pode habilitar a opção de alternância **[!UICONTROL Perfil]** para assimilar os dados diretamente no Perfil. | Registro |
| Metadados de perfis autenticados do AAM | Usado no diagnóstico Audience Manager Connector. Os dados não estão visíveis como lotes no conjunto de dados. Você pode habilitar a opção de alternância **[!UICONTROL Perfil]** para assimilar os dados diretamente no Perfil. | Registro |
| Preenchimento retroativo de dados de dispositivos AAM | Conjunto de dados que traz dados de dispositivos anteriores. Ela contém ECIDs e realizações de segmento correspondentes agregadas no Audience Manager. Os dados não estão visíveis como lotes no conjunto de dados. Você pode habilitar o botão de alternância **[!UICONTROL Perfil]** para assimilar os dados diretamente no Perfil. | Registro |
| Preenchimento retroativo de perfis autenticados do AAM | Conjunto de dados de trazer dados autenticados anteriores. Ele contém perfis autenticados do Audience Manager. Os dados não estão visíveis como lotes no conjunto de dados. Você pode habilitar o botão de alternância **[!UICONTROL Perfil]** para assimilar os dados diretamente no Perfil. | Registro |

### Conexões

O Adobe Audience Manager cria uma conexão no Catálogo: Audience Manager Connection. Catálogo é o sistema de registros para localização e linhagem de dados no Adobe Experience Platform. Uma conexão é um objeto de Catálogo que é uma instância de conectores específica do cliente. Leia a [Visão geral do Serviço de Catálogo](../../../catalog/home.md) para obter mais informações sobre Catálogo, conexões e conectores.

### População do segmento para impacto do perfil

Os tamanhos de preenchimento de segmento têm um impacto direto nos números de perfil ao enviar um segmento do Audience Manager pela primeira vez para a Experience Platform. Isso significa que selecionar todos os segmentos pode causar sobreposições de perfil que excedem seus direitos de uso de licença. O Experience Platform também distingue novos dados dos dados históricos para assimilação de perfis. Um segmento com 100 identidades primárias criará 100 perfis. No entanto, se a população desse mesmo segmento foi aumentada para 150 e foi assimilada no Experience Platform, o número de perfis só aumentará em 50, pois há apenas 50 novos perfis.

Você também pode verificar o uso de perfil que sua conta tem disponível através do [Painel de Uso de Licenças](../../../dashboards/guides/license-usage.md).

## Qual é a latência esperada para dados do Audience Manager no Experience Platform?

| Dados do Audience Manager | Tipo | Latência | Notas |
| --- | --- | --- | --- |
| Dados em tempo real | Eventos | &lt;25 minutos | Tempo desde a captura no nó do Audience Manager Edge até a exibição no data lake. |
| Dados em tempo real | Atualizações de perfil | &lt;10 minutos | Tempo de acesso ao Perfil do cliente em tempo real. |
| Dados integrados e em tempo real | Atualizações de perfil | 24 a 36 horas | Tempo decorrido desde a captura por meio de dados DCS/PCS Edge e dados integrados, processamento em um perfil de usuário até a exibição no Perfil do cliente em tempo real. Atualmente, esses dados não chegam diretamente ao data lake. A alternância de perfil pode ser ativada para que os conjuntos de dados de perfil da Audience Manager assimilem esses dados diretamente no Perfil do cliente em tempo real. |
