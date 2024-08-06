---
keywords: Experience Platform;modelo de aprendizado de máquina;Data Science Workspace;Perfil do cliente em tempo real;tópicos populares;insights de aprendizado de máquina
solution: Experience Platform
title: Enriqueça o Perfil do cliente em tempo real com os Insights de aprendizado de máquina
type: Tutorial
description: Este documento fornece um guia sobre como enriquecer o Perfil do cliente em tempo real com insights de aprendizado de máquina.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 923c6f2deb4d1199cfc5dc9dc4ca7b4da154aaaa
workflow-type: tm+mt
source-wordcount: '653'
ht-degree: 0%

---

# Enriquecer [!DNL Real-Time Customer Profile] com insights de aprendizado de máquina

>[!NOTE]
>
>O Data Science Workspace não está mais disponível para compra.
>
>Esta documentação destina-se aos clientes existentes com direitos anteriores ao Data Science Workspace.

O Adobe Experience Platform [!DNL Data Science Workspace] fornece ferramentas e recursos para criar, avaliar e utilizar modelos de aprendizado de máquina para gerar previsões e insights de dados. Quando os insights de aprendizado de máquina são assimilados em um conjunto de dados habilitado para [!DNL Profile], esses mesmos dados também são assimilados como [!DNL Profile] registros que podem ser segmentados usando [!DNL Adobe Experience Platform Segmentation Service].

O processo de segmentação depende do método de avaliação do público-alvo. Se um público-alvo estiver configurado como **transmissão**, ele processará todas as novas atualizações gravadas pelo modelo no perfil em tempo real. No entanto, se um público-alvo estiver configurado para a avaliação de **lote**, os novos valores serão avaliados no próximo lote.

Este documento fornece links para tutoriais que permitem enriquecer o [!DNL Real-Time Customer Profile] com seus insights de aprendizado de máquina.

## Introdução

Para concluir os tutoriais abaixo, você precisa ter uma compreensão funcional da assimilação de dados do [!DNL Profile] e da criação de públicos-alvo. Antes de iniciar este tutorial, revise a documentação dos seguintes serviços:

- [[!DNL Real-Time Customer Profile]](../../profile/home.md): fornece uma representação completa e unificada de cada cliente individual com base em dados agregados de várias fontes.
- [[!DNL Identity Service]](../../identity-service/home.md): Habilita [!DNL Real-Time Customer Profile] unindo identidades de diferentes fontes de dados que estão sendo assimiladas na Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): a estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.

Além dos documentos mencionados acima, é altamente recomendável que você também revise os seguintes guias sobre esquemas e o Editor de esquemas:

- [Noções básicas da composição de esquema](../../xdm/schema/composition.md): descreve esquemas XDM, blocos de construção, princípios e práticas recomendadas para a composição de esquemas a serem usados em [!DNL Experience Platform].
- [Tutorial do Editor de Esquemas](../../xdm/tutorials/create-schema-ui.md): fornece instruções detalhadas para a criação de esquemas usando o Editor de Esquemas em [!DNL Experience Platform].

## Criar e configurar um esquema de saída e um conjunto de dados {#create-an-output-schema-and-dataset}

O primeiro passo para enriquecer o [!DNL Real-Time Customer Profile] com insights de pontuação é saber o que o objeto real (como uma pessoa) seus dados definem. A compreensão de seus dados permite descrever e projetar uma estrutura para adicionar significado, da mesma forma que projetar um banco de dados relacional.

A composição de um esquema começa com a atribuição de uma classe. As classes definem os aspectos comportamentais dos dados que o esquema conterá (registro ou série temporal). Para começar a criar seus próprios esquemas, siga as etapas do tutorial em [criação de um esquema usando o Editor de Esquemas](../../xdm/tutorials/create-schema-ui.md). Observe que antes de habilitar um conjunto de dados para [!DNL Profile], é necessário configurar o esquema do conjunto de dados para ter um campo de identidade primário e, em seguida, habilitar o esquema para [!DNL Profile]. Quando os dados são assimilados em um conjunto de dados habilitado para [!DNL Profile], esses mesmos dados também são assimilados como [!DNL Profile] registros.

Se preferir compor um esquema usando a API [!DNL Schema Registry], comece lendo o [[!DNL Schema Registry] guia do desenvolvedor](../../xdm/api/getting-started.md) antes de tentar o tutorial sobre [criação de um esquema usando a API](../../xdm/tutorials/create-schema-api.md).

Depois que o esquema e o conjunto de dados estiverem preparados, você poderá gerar e assimilar dados de pontuação para o conjunto de dados executando execuções de pontuação usando um modelo apropriado.

## Criar públicos usando o [!DNL Segment Builder] {#create-audiences-using-the-segment-builder}

Depois de gerar e assimilar os insights de dados de pontuação no conjunto de dados habilitado para [!DNL Profile], você pode criar públicos dinâmicos usando o [!DNL Segment Builder].

O [!DNL Segment Builder] fornece um espaço de trabalho avançado que permite a você interagir com elementos de dados [!DNL Profile]. O espaço de trabalho fornece controles intuitivos para criar e editar regras, como arrastar e soltar blocos usados para representar propriedades de dados. Siga o [[!DNL Segment Builder] guia do usuário](../../segmentation/ui/segment-builder.md) para saber mais sobre:

- Criar definições de segmento usando uma combinação de atributos, eventos e públicos-alvo existentes como blocos de construção.
- Uso da tela e dos contêineres do construtor de regras para controlar a ordem em que as regras de público-alvo são executadas.
- Exibir estimativas do público-alvo em potencial, permitindo ajustar as definições de segmento conforme necessário.
- Ativação de todas as definições de segmento para a segmentação programada.
- Ativação de definições de segmento especificadas para a segmentação por transmissão.

## Próximas etapas {#next-steps}

Para saber mais sobre os públicos-alvo e o [!DNL Segment Builder], leia a [Visão geral do Serviço de segmentação](../../segmentation/home.md).

Para saber mais sobre o [!DNL Real-Time Customer Profile], leia a [Visão geral do Perfil do Cliente em Tempo Real](../../profile/home.md)
