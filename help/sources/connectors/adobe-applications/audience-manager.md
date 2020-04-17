---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Conector do Gerenciador de Audiências
topic: overview
translation-type: tm+mt
source-git-commit: a1161630c8edae107b784f32ee20af225f9f8c46

---


# Conector do Gerenciador de Audiências

O conector de dados do Adobe Audiência Manager transmite dados primários coletados no Adobe Audiência Manager para a Adobe Experience Platform. O conector do Gerenciador de Audiências ingere três categorias de dados na Plataforma:

- **Dados em tempo real:** Dados capturados em tempo real no servidor de coleta de dados do Audiência Manager. Esses dados são usados no Gerenciador de Audiências para preencher características com base em regras e aparecerão na Plataforma no menor tempo de latência.
- **Dados integrados:** Esses são os arquivos carregados por um usuário em um local Amazon S3 hospedado pelo Audiência Manager. O Gerenciador de Audiências usa esses dados para preencher características integradas usando o método de arquivo de entrada e terá alguma latência.
- **Dados do Perfil:** O Gerenciador de Audiências usa dados em tempo real e integrados para derivar perfis de clientes. Esses perfis são usados para preencher gráficos de identidade e características nas execuções de segmentos.

O conector do Audiência Manager mapeia essas categorias de dados para o schema do Experience Data Model (XDM) e as envia para a Plataforma. Os dados em tempo real e os dados onboard são enviados como dados XDM ExperienceEvent, enquanto os dados do Perfil são enviados como Perfis individuais XDM.

Para obter instruções sobre como criar uma conexão com o Gerenciador de Audiências da Adobe usando a interface do usuário da plataforma, consulte o tutorial [do conector do Gerenciador de](../../tutorials/ui/create/adobe-applications/audience-manager.md)Audiências.

## O que é o Experience Data Model (XDM)?

O XDM é uma especificação documentada publicamente que fornece uma estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.

A adesão aos padrões XDM permite que os dados de experiência do cliente sejam uniformemente incorporados, facilitando a entrega de dados e a coleta de informações.

Para obter mais informações sobre como o XDM é usado na plataforma da experiência, consulte a visão geral [do sistema](../../../xdm/home.md)XDM. Para saber mais sobre como os Schemas XDM como Perfil e ExperienceEvent são estruturados, consulte as [noções básicas da composição](../../../xdm/schema/composition.md)do schema.

## Exemplos de schemas XDM

Abaixo estão exemplos da estrutura do Gerenciador de Audiências mapeada para o Perfil individual XDM ExperienceEvent e XDM na plataforma.

### ExperienceEvent - para dados em tempo real e dados integrados

![](images/aam-experience-events-for-dcs-and-onboarding-data.png)

### Perfil individual XDM - para dados de Perfil

![](images/aam-profile-xdm-for-profile-data.png)

## Como os campos são mapeados do Adobe Audiência Manager para o XDM?

Consulte a documentação para obter mais informações sobre os campos [de mapeamento do Gerenciador de][audience-manager-mapping-fields] Audiências.

## Gestão de dados na plataforma

### Conjuntos de dados

Os conjuntos de dados são uma construção de armazenamento e gerenciamento para uma coleção de dados, geralmente uma tabela, que contém schemas (colunas) e campos (linhas) e é disponibilizada por uma conexão de dados. Os dados do Gerenciador de Audiências consistem em dados em tempo real, dados de entrada e dados de Perfil. Para localizar os conjuntos de dados do Gerenciador de Audiências, use a função de pesquisa na interface do usuário com as convenções de nomenclatura fornecidas para cada tipo de dados.

Embora os usuários tenham a capacidade de desativar conjuntos de dados, não é recomendável desativar conjuntos de dados que serão usados para associação de segmentos no Perfil.

| Nome do conjunto de dados | Descrição |
| ------------ | ----------- |
| Tempo Real do Gerenciador de Audiências | Este conjunto de dados contém dados coletados por ocorrências diretas em pontos de extremidade DCS do Audiência Manager e mapas de identidade para Perfis do Audiência Manager. Manter este conjunto de dados ativado para ingestão de Perfis. |
| Atualizações do Perfil em tempo real do Gerenciador de Audiências | Esse conjunto de dados permite o direcionamento em tempo real de características e segmentos do Gerenciador de Audiências. Ele inclui informações sobre o roteamento regional do Edge, características e associação a segmentos. Manter este conjunto de dados ativado para ingestão de Perfis. |
| Dados de dispositivos do Gerenciador de Audiências | Dados do dispositivo com ECIDs e correspondentes execuções de segmentos agregados no Gerenciador de Audiências. |
| Dados do Perfil do dispositivo do Gerenciador de Audiências | Usado para diagnóstico do conector do Audiência Manager. |
| Perfis autenticados pelo Audiência Manager | Este conjunto de dados contém perfis autenticados pelo Gerenciador de Audiências. |
| Metadados de Perfis autenticados do Audiência Manager | Usado para diagnóstico do conector do Audiência Manager. |
| {ID da Fonte de Dados} de Entrada do Gerenciador de Audiências **(Obsoleto)** | Esse conjunto de dados representa registros integrados no Gerenciador de Audiências por meio do método de arquivo de entrada. Esse fluxo de dados está obsoleto e será removido em uma versão subsequente. |
| Metadados de entrada do Gerenciador de Audiências **(obsoleto)** | Usado para diagnóstico do conector do Audiência Manager. Esse fluxo de dados está obsoleto e será removido em uma versão subsequente. |

### Conexões

O Adobe Audiência Manager cria uma conexão no Catálogo: Conexão **do Gerenciador de** Audiências. Catálogo é o sistema dos registros para localização e linhagem de dados na Adobe Experience Platform. Uma conexão é um objeto de Catálogo que é uma instância específica do cliente dos Conectores. Consulte a visão geral [do Serviço de](../../../catalog/home.md) catálogo para obter mais informações sobre Catálogo, conexões e conectores.

## Qual é a latência esperada para os dados do gerenciador de Audiências na plataforma?

| Dados do Gerenciador de Audiências | Latência | Notas |
| --- | --- | --- |
| Dados em tempo real | &lt; 35 minutos. | Tempo de ser capturado no nó Realtime para aparecer no Platform Data Lake. |
| Dados de entrada | &lt; 13 horas | Tempo de ser capturado em baldes S3 para aparecer no Platform Data Lake. |
| dados do Perfil | &lt; 2 dias | Tempo desde a captura dos dados em tempo real/de entrada até a adição a um perfil de usuário e, por fim, a exibição no Lago de dados da plataforma. |