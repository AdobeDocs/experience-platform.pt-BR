---
title: Página Detalhes de Destinos
seo-title: Página Detalhes de Destinos
description: 'A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino, como nome do destino, ID, segmentos mapeados para o destino e controles para editar a ativação e ativar e desativar o fluxo de dados. '
seo-description: 'A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino, como nome do destino, ID, segmentos mapeados para o destino e controles para editar a ativação e ativar e desativar o fluxo de dados. '
translation-type: tm+mt
source-git-commit: 6f680a60c88bc5fee6ce9cb5a4f314c4b9d02249
workflow-type: tm+mt
source-wordcount: '505'
ht-degree: 1%

---


# Página de detalhes do destino {#destinations-details-page}

A página de detalhes de um destino individual fornece uma visão geral dos detalhes do destino, como nome do destino, ID, segmentos mapeados para o destino e controles para editar a ativação e ativar e desativar o fluxo de dados. Para visualização desses detalhes, vá para **[!UICONTROL Destinos]** > **[!UICONTROL Procurar]** e clique no nome do destino com o qual você deseja trabalhar.

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
| Nome do segmento | O nome do seu segmento. |
| Descrição do segmento | A descrição do seu segmento. |
| Data do Start | A data em que esses segmentos estão sendo ativados para o destino. |
| Data final | A data em que esses segmentos pararão de ser ativados para o destino. |
| ID de mapeamento | *Não disponível para destinos* de marketing por email. Indica a ID pela qual o segmento é conhecido na plataforma de destino. |

## 3. Informações sobre o painel direito

O painel direito inclui informações sobre seu destino. Consulte a tabela abaixo para obter mais informações:

| Item | Descrição |
---------|----------|
| Plataforma | Representa a plataforma de destino para a qual o audiência é enviado. Consulte Catálogo [de](/help/rtcdp/destinations/destinations-catalog.md) destinos para obter mais informações. |
| Descrição | Você pode editar a descrição do fluxo de destino. |
| Categoria | Indica o tipo de destino. Consulte Catálogo [de](/help/rtcdp/destinations/destinations-catalog.md) destinos para obter mais informações. |
| Tipo de conexão | Indica em qual formulário suas audiências estão sendo enviadas para o destino. Pode ser **[!UICONTROL Cookie]** ou baseado em **[!UICONTROL Perfis]**. |
| Frequência | Indica com que frequência as audiências são enviadas para o destino. Pode ser **[!UICONTROL Streaming]** ou **[!UICONTROL Batch]**. |
| Identidade | Representa a namespace de identidade aceita pelo destino. Por exemplo, o campo Identidade pode ser GAID, IDFA, email. Para obter todas as namespaces de identidade aceitas, consulte namespaces padrão na visão geral [da namespace de](../../identity-service/namespaces.md)identidade. |
| Criado por | Indica o usuário que criou esse fluxo de destino. |
| Criado | Indica a data e a hora UTC em que esse fluxo de destino foi criado. |

## 4. Controles para editar a ativação e ativar/desativar o fluxo de dados

O controle Editar ativação permite editar quais segmentos são mapeados para o destino. Pressione Editar ativação para abrir o fluxo de trabalho [da ativação de](/help/rtcdp/destinations/activate-destinations.md)segmentos.

Use a opção **Ativar/Desativar** para alternar para o start e pausar a exportação de dados para um destino.