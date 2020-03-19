---
title: Página Detalhes de Destinos
seo-title: Página Detalhes de Destinos
description: 'A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino, como nome do destino, ID, segmentos mapeados para o destino e controles para editar a ativação e ativar e desativar o fluxo de dados. '
seo-description: 'A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino, como nome do destino, ID, segmentos mapeados para o destino e controles para editar a ativação e ativar e desativar o fluxo de dados. '
translation-type: tm+mt
source-git-commit: b784b67092ea8d30ad00cda9a40779b3890862fd

---


# Página de detalhes do destino {#destinations-details-page}

A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino, como nome do destino, ID, segmentos mapeados para o destino e controles para editar a ativação e ativar e desativar o fluxo de dados. Para exibir esses detalhes, vá para **Destinos** > **Procurar** e clique no nome do destino com o qual deseja trabalhar.

Os componentes principais de um destino individual são:

* 1 - Nome e ID de destino
* 2 - Segmentos ativados para o destino
* 3 - Informação sobre o painel direito
* 4 - Controles para editar a ativação e ativar/desativar o fluxo de dados

![Página de destinos numerada](/help/rtcdp/destinations/assets/destination-page-numbered.png)

Navegue até uma página de destino individual para obter uma visão geral dos detalhes de destino, como:

## 1. Nome e ID do destino

Você pode ver o nome de destino no cabeçalho da página e a ID de destino no URL da página.

## 2. Segmentos ativados para o destino

Esta seção exibe quais segmentos estão mapeados no momento para o destino, bem como mais informações sobre esses segmentos. Consulte a tabela abaixo para obter mais informações:

| Item | Descrição |
---------|----------|
| Nome do segmento | Nome do segmento. |
| Descrição do segmento | A descrição do seu segmento. |
| Data inicial | A data em que esses segmentos estão sendo ativados para o destino. |
| Data final | A data em que esses segmentos pararão de ser ativados para o destino. |
| ID de mapeamento | *Não disponível para destinos* de marketing por email. Indica a ID pela qual o segmento é conhecido na plataforma de destino. |

## 3. Informações sobre o painel direito

O painel direito inclui informações sobre seu destino. Consulte a tabela abaixo para obter mais informações:

| Item | Descrição |
---------|----------|
| Plataforma | Representa a plataforma de destino para a qual os públicos-alvo são enviados. Consulte Catálogo [de](/help/rtcdp/destinations/destinations-catalog.md) destinos para obter mais informações. |
| Descrição | Você pode editar a descrição do fluxo de destino. |
| Categoria | Indica o tipo de destino. Consulte Catálogo [de](/help/rtcdp/destinations/destinations-catalog.md) destinos para obter mais informações. |
| Tipo de conexão | Indica em qual formulário seus públicos-alvo estão sendo enviados para o destino. Pode ser **Cookie** ou baseado em **perfil**. |
| Frequência | Indica a frequência com que os públicos-alvo são enviados para o destino. Pode ser **Streaming** ou **Batch**. |
| Identidade | Representa o namespace de identidade aceito pelo destino. Por exemplo, o campo Identidade pode ser GAID, IDFA, email. Para todos os namespaces de identidade aceitos, consulte os namespaces padrão na visão geral [do namespace de](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md)identidade. |
| Criado por | Indica o usuário que criou esse fluxo de destino. |
| Criado | Indica a data e a hora UTC em que esse fluxo de destino foi criado. |

## 4. Controles para editar a ativação e ativar/desativar o fluxo de dados

O controle de ativação Editar permite que você edite quais segmentos são mapeados para o destino. Pressione Editar ativação para abrir o fluxo de trabalho [de ativação do](/help/rtcdp/destinations/activate-destinations.md)segmento.

Use o **botão Ativar/Desativar** para iniciar e pausar a exportação de dados para um destino.