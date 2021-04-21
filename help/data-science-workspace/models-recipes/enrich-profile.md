---
keywords: Experience Platform, modelo de aprendizado de máquina, Data Science Workspace, Perfil do cliente em tempo real, tópicos populares, insights de aprendizado de máquina
solution: Experience Platform
title: Enriqueça o perfil do cliente em tempo real com os insights de aprendizado da máquina
topic-legacy: tutorial
type: Tutorial
description: Este documento fornece um guia sobre como enriquecer o Perfil do cliente em tempo real com insights de aprendizado de máquina.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# Enriqueça [!DNL Real-time Customer Profile] com insights de aprendizado de máquina

O Adobe Experience Platform [!DNL Data Science Workspace] fornece as ferramentas e os recursos para criar, avaliar e utilizar modelos de aprendizado de máquina para gerar previsões e insights de dados. Quando os insights de aprendizado de máquina são assimilados em um conjunto de dados habilitado para [!DNL Profile], os mesmos dados também são assimilados como registros [!DNL Profile] que podem ser segmentados usando [!DNL Adobe Experience Platform Segmentation Service]. Conforme os dados do perfil e da série de tempo são assimilados, o Perfil do cliente em tempo real decide automaticamente incluir ou excluir esses dados dos segmentos por meio de um processo contínuo chamado de segmentação de fluxo, antes de mesclá-los com os dados existentes e atualizar a visualização da união. Como resultado, você pode executar instantaneamente os cálculos e tomar decisões para oferecer experiências aprimoradas e individualizadas aos clientes, à medida que eles interagem com a sua marca.

Este documento fornece links para tutoriais que permitem enriquecer [!DNL Real-time Customer Profile] com seus insights de aprendizado de máquina.

## Introdução

Para concluir os tutoriais abaixo, você deve ter uma compreensão funcional da assimilação de dados [!DNL Profile] e da criação de segmentos. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece uma representação completa e unificada de cada cliente individual com base em dados agregados de várias fontes.
- [[!DNL Identity Service]](../../identity-service/home.md): Permite  [!DNL Real-time Customer Profile] por meio da ligação de identidades de diferentes fontes de dados que estão sendo assimiladas na Plataforma.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.

Além dos documentos mencionados acima, é altamente recomendável revisar os seguintes guias sobre schemas e o Editor de esquema:

- [Noções básicas da composição](../../xdm/schema/composition.md) do schema: Descreve esquemas XDM, blocos de construção, princípios e práticas recomendadas para compor schemas a serem usados no  [!DNL Experience Platform].
- [Tutorial](../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Fornece instruções detalhadas para criar esquemas usando o Editor de esquemas no  [!DNL Experience Platform].

## Criar e configurar um esquema de saída e um conjunto de dados {#create-an-output-schema-and-dataset}

O primeiro passo para enriquecer [!DNL Real-time Customer Profile] com insights de pontuação é saber qual objeto real (como uma pessoa) seus dados definem. Compreender seus dados permite descrever e projetar uma estrutura para adicionar significado, como projetar um banco de dados relacional.

A composição de um schema começa pela atribuição de uma classe. As classes definem os aspectos comportamentais dos dados que o schema conterá (registro ou série de tempo). Para começar a criar seus próprios esquemas, siga as etapas no tutorial em [criar um esquema usando o Editor de esquemas](../../xdm/tutorials/create-schema-ui.md). Observe que, antes de habilitar um conjunto de dados para [!DNL Profile], é necessário configurar o esquema do conjunto de dados para ter um campo de identidade primário e, em seguida, habilitar o esquema para [!DNL Profile]. Quando os dados são assimilados em um conjunto de dados habilitado para [!DNL Profile], os mesmos dados também são assimilados como registros [!DNL Profile].

Se preferir compor um schema usando a API [!DNL Schema Registry], comece lendo o [[!DNL Schema Registry] guia do desenvolvedor](../../xdm/api/getting-started.md) antes de tentar o tutorial em [criar um schema usando a API](../../xdm/tutorials/create-schema-api.md).

Quando o esquema e o conjunto de dados estiverem preparados, você poderá gerar e assimilar dados de pontuação no conjunto de dados executando execuções de pontuação usando um modelo apropriado.

## Crie segmentos usando o [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Depois de gerar e assimilar seus insights de dados de pontuação no conjunto de dados habilitado para [!DNL Profile], você pode criar segmentos dinâmicos usando o [!DNL Segment Builder].

O [!DNL Segment Builder] fornece um espaço de trabalho avançado que permite interagir com elementos de dados [!DNL Profile]. O espaço de trabalho oferece controles intuitivos para criar e editar regras, como blocos de arrastar e soltar usados para representar propriedades de dados. Siga o [[!DNL Segment Builder] guia do usuário](../../segmentation/ui/segment-builder.md) para saber mais sobre:

- Criar definições de segmento usando uma combinação de atributos, eventos e públicos-alvo existentes como blocos de construção.
- Usar a tela e os contêineres do construtor de regras para controlar a ordem em que as regras de segmento são executadas.
- Visualizar estimativas do seu público-alvo potencial, permitindo que você ajuste as definições do segmento, conforme necessário.
- Ativar todas as definições de segmento para segmentação agendada.
- Ativar definições de segmento especificadas para a segmentação de fluxo.

## Próximas etapas {#next-steps}

Para saber mais sobre segmentos e o [!DNL Segment Builder], leia a [Visão geral do Serviço de segmentação](../../segmentation/home.md).

Para saber mais sobre [!DNL Real-time Customer Profile], leia a [Visão geral do Perfil do cliente em tempo real](../../profile/home.md)
