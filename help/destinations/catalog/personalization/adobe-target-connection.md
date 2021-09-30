---
keywords: personalização do target; destino; destino do target da experience platform; destino do adobe target;
title: Conexão Adobe Target
description: O Adobe Target é um aplicativo que fornece personalização e experimentação com IA em tempo real, 1:1 e em todas as interações de entrada do cliente em sites, aplicativos móveis e muito mais.
source-git-commit: caccd096c9165139d9b966bbfcb311456276192a
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 2%

---


# Conexão Adobe Target (Beta) {#adobe-target-connection}

## Visão geral {#overview}

>[!IMPORTANT]
>
>A conexão Adobe Target no Adobe Experience Platform está atualmente na versão beta. A documentação e a funcionalidade estão sujeitas a alterações.

O Adobe Target é um aplicativo que fornece personalização e experimentação em tempo real, com recursos de IA, em todas as interações de entrada do cliente em sites, aplicativos móveis e muito mais.

Adobe Target é uma conexão de personalização no Adobe Experience Platform.

## Pré-requisitos {#prerequisites}

Essa integração é disponibilizada pelo [Adobe Experience Platform Web SDK](../../../edge/home.md). Você deve usar esse SDK para usar esse destino.

## Tipo de exportação {#export-type}

**Solicitação de perfil**  - você está solicitando todos os segmentos que estão mapeados no destino Adobe Target para um único perfil.

## Casos de uso {#use-cases}

**Personalização de um banner de página inicial**

Uma empresa de aluguel e vendas da casa deseja personalizar sua página inicial com um banner, com base nas qualificações do segmento do cliente no Adobe Experience Platform. A empresa pode selecionar quais públicos-alvo devem obter uma experiência personalizada e enviá-los para o Adobe Target como critérios de direcionamento para sua oferta do Target.

## Conecte-se ao destino {#connect}

Para se conectar a esse destino, siga as etapas descritas no [tutorial de configuração de destino](../../ui/connect-destination.md).

O Adobe Experience Platform se conecta automaticamente à instância do Adobe Target de sua empresa. Não é necessária nenhuma autenticação.

### Parâmetros de conexão {#parameters}

Enquanto [configurar](../../ui/connect-destination.md) esse destino, você deve fornecer as seguintes informações:

* **Nome**: Preencha o nome preferencial para esse destino.
* **Descrição**: Insira uma descrição para o seu destino. Por exemplo, você pode mencionar para qual campanha está usando esse destino. Este campo é opcional.
* **ID** do conjunto de dados: Isso determina em qual conjunto de dados da Coleta de dados os segmentos serão incluídos na resposta à página. O menu suspenso mostra apenas os conjuntos de dados com a configuração de destino ativada. Consulte [Configurar um conjunto de dados](../../../edge/fundamentals/datastreams.md) para obter mais detalhes.

## Ativar segmentos para este destino {#activate}

Leia [Ativar perfis e segmentos para destinos de solicitação de perfil](../../ui/activate-profile-request-destinations.md) para obter instruções sobre como ativar segmentos de público-alvo para este destino.

## Dados exportados {#exported-data}

O Adobe Target lê os dados do perfil da Adobe Experience Platform Edge Network, de modo que nenhum dado é exportado.

## Uso e governança de dados {#data-usage-governance}

Todos os destinos [!DNL Adobe Experience Platform] são compatíveis com as políticas de uso de dados ao manipular seus dados. Para obter informações detalhadas sobre como [!DNL Adobe Experience Platform] aplica o controle de dados, leia a [Visão geral da governança de dados](https://experienceleague.adobe.com/docs/experience-platform/data-governance/home.html).
