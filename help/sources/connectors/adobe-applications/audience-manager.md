---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: conector Audience Manager
topic: overview
translation-type: tm+mt
source-git-commit: fb4ffa2c95365905f5417586fa7ecf88523009a0
workflow-type: tm+mt
source-wordcount: '742'
ht-degree: 1%

---


# conector Audience Manager

O conector de dados Adobe Audience Manager transmite dados primários coletados em Adobe Audience Manager para Adobe Experience Platform. O conector Audience Manager ingere três categorias de dados à Platform:

- **Dados em tempo real:** Dados capturados em tempo real no servidor de coleta de dados do Audience Manager. Esses dados são usados no Audience Manager para preencher características com base em regras e aparecerão no Platform no menor tempo de latência.
- **Dados integrados:** Esses são os arquivos carregados por um usuário em um local Amazon S3 hospedado pelo Audience Manager. O Audience Manager usa esses dados para preencher características integradas usando o método de arquivo de entrada e terá alguma latência.
- **Dados do Perfil:** O Audience Manager usa dados em tempo real e integrados para derivar perfis do cliente. Esses perfis são usados para preencher gráficos de identidade e características nas execuções de segmentos.

O conector Audience Manager mapeia essas categorias de dados para o schema Experience Data Model (XDM) e as envia para a Platform. Os dados em tempo real e os dados onboard são enviados como dados XDM ExperienceEvent, enquanto os dados do Perfil são enviados como Perfis individuais XDM.

Para obter instruções sobre como criar uma conexão com o Adobe Audience Manager usando a interface do usuário do Platform, consulte o tutorial [do conector do](../../tutorials/ui/create/adobe-applications/audience-manager.md)Audience Manager.

## O que é o Experience Data Model (XDM)?

O XDM é uma especificação documentada publicamente que fornece uma estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.

A adesão aos padrões XDM permite que os dados de experiência do cliente sejam uniformemente incorporados, facilitando a entrega de dados e a coleta de informações.

Para obter mais informações sobre como o XDM é usado no Experience Platform, consulte a visão geral [do Sistema](../../../xdm/home.md)XDM. Para saber mais sobre como os Schemas XDM como Perfil e ExperienceEvent são estruturados, consulte as [noções básicas da composição](../../../xdm/schema/composition.md)do schema.

## Exemplos de schemas XDM

Abaixo estão exemplos da estrutura de Audience Manager mapeada para o Perfil XDM ExperienceEvent e XDM Individual no Platform.

### ExperienceEvent - para dados em tempo real e dados integrados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual XDM - para dados de Perfil

![](images/aam-profile-xdm-for-profile-data.png)

## Como os campos são mapeados de Adobe Audience Manager para XDM?

Consulte a documentação para obter mais informações sobre os campos [de mapeamento de](./mapping/audience-manager.md) Audience Manager.

## Gestão de dados no Platform

### Conjuntos de dados

Os conjuntos de dados são uma construção de armazenamento e gerenciamento para uma coleção de dados, geralmente uma tabela, que contém schemas (colunas) e campos (linhas) e é disponibilizada por uma conexão de dados. Os dados de Audience Manager consistem em dados em tempo real, dados de entrada e dados de Perfil. Para localizar seus conjuntos de dados de Audience Manager, use a função de pesquisa na interface do usuário com as convenções de nomenclatura fornecidas para cada tipo de dados.

Por padrão, os conjuntos de dados de Audience Manager são desativados para o Perfil e os usuários podem ativar ou desativar os conjuntos de dados com base em seus casos de uso. Não é recomendável desativar conjuntos de dados que serão usados para associação de segmentos no Perfil.

| Nome do conjunto de dados | Descrição |
| ------------ | ----------- |
| Audience Manager Realtime | Este conjunto de dados contém dados coletados por ocorrências diretas em pontos de extremidade DCS Audience Manager e mapas de identidade para Perfis Audience Manager. Manter este conjunto de dados ativado para ingestão de Perfis. |
| Atualizações do Perfil em tempo real do Audience Manager | Esse conjunto de dados permite o direcionamento em tempo real de características e segmentos de Audience Manager. Ele inclui informações sobre o roteamento regional do Edge, características e associação a segmentos. Manter este conjunto de dados ativado para ingestão de Perfis. |
| Dados de dispositivos Audience Manager | Dados do dispositivo com ECIDs e correspondentes execuções de segmentos agregados no Audience Manager. |
| Dados de Perfil do dispositivo Audience Manager | Usado para diagnóstico do conector de Audience Manager. |
| Perfis autenticados pelo Audience Manager | Este conjunto de dados contém perfis autenticados por Audience Manager. |
| Metadados de Perfis autenticados por Audience Manager | Usado para diagnóstico do conector do Audience Manager. |
| {ID da fonte de dados} de entrada de Audience Manager **(obsoleto)** | Este conjunto de dados representa registros onboard no Audience Manager por meio do método de arquivo de entrada. Esse fluxo de dados está obsoleto e será removido em uma versão subsequente. |
| Metadados de entrada de Audience Manager **(obsoleto)** | Usado para diagnóstico do conector de Audience Manager. Esse fluxo de dados está obsoleto e será removido em uma versão subsequente. |

### Conexões

O Adobe Audience Manager cria uma conexão no Catálogo: **Conexão** Audience Manager. Catálogo é o sistema dos registros para localização e linhagem de dados no Adobe Experience Platform. Uma conexão é um objeto de Catálogo que é uma instância específica do cliente dos Conectores. Consulte a visão geral [do Serviço de](../../../catalog/home.md) catálogo para obter mais informações sobre Catálogo, conexões e conectores.

## Qual é a latência esperada para os dados de Audience Manager no Platform?

| Dados de Audience Manager | Latência | Notas |
| --- | --- | --- |
| Dados em tempo real | &lt; 35 minutos. | Tempo de ser capturado no nó Realtime para aparecer no Platform Data Lake. |
| Dados de entrada | &lt; 13 horas | Tempo de ser capturado em baldes S3 para aparecer no Platform Data Lake. |
| dados do Perfil | &lt; 2 dias | Tempo desde a captura dos dados em tempo real/de entrada até a adição a um perfil de usuário e, por fim, a exibição no Platform Data Lake. |