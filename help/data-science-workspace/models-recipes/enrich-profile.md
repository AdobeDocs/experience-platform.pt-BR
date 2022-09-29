---
keywords: Experience Platform, modelo de aprendizado de máquina, Data Science Workspace, Perfil do cliente em tempo real, tópicos populares, insights de aprendizado de máquina
solution: Experience Platform
title: Enriqueça o perfil do cliente em tempo real com os insights de aprendizado da máquina
topic-legacy: tutorial
type: Tutorial
description: Este documento fornece um guia sobre como enriquecer o Perfil do cliente em tempo real com insights de aprendizado de máquina.
exl-id: 397023c9-383d-4a21-b58a-0f920631ac56
source-git-commit: 89a9b64f2fb238c08a281f29a035ce0b24b34804
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 0%

---

# Enriquecer [!DNL Real-time Customer Profile] com insights de aprendizado de máquina

Adobe Experience Platform [!DNL Data Science Workspace] O fornece as ferramentas e os recursos para criar, avaliar e utilizar modelos de aprendizado de máquina para gerar previsões e insights de dados. Quando os insights de aprendizado de máquina são assimilados em um [!DNL Profile]conjunto de dados habilitado para , que os mesmos dados também sejam assimilados como [!DNL Profile] registros que podem então ser segmentados usando [!DNL Adobe Experience Platform Segmentation Service].

Este documento fornece links para tutoriais que permitem enriquecer [!DNL Real-time Customer Profile] com seus insights de aprendizado de máquina.

## Introdução

Para concluir os tutoriais abaixo, você deve ter uma compreensão funcional da assimilação [!DNL Profile] dados e criação de segmentos. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece uma representação completa e unificada de cada cliente individual com base em dados agregados de várias fontes.
- [[!DNL Identity Service]](../../identity-service/home.md): Habilitar [!DNL Real-time Customer Profile] ao fazer a ponte de identidades de fontes de dados diferentes que estão sendo assimiladas na Platform.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Platform organiza os dados de experiência do cliente.

Além dos documentos mencionados acima, é altamente recomendável revisar os seguintes guias sobre schemas e o Editor de esquema:

- [Noções básicas da composição do schema](../../xdm/schema/composition.md): Descreve esquemas XDM, blocos de construção, princípios e práticas recomendadas para compor schemas a serem usados em [!DNL Experience Platform].
- [Tutorial do Editor de esquemas](../../xdm/tutorials/create-schema-ui.md): Fornece instruções detalhadas para criar esquemas usando o Editor de esquemas dentro do [!DNL Experience Platform].

## Criar e configurar um schema de saída e um conjunto de dados {#create-an-output-schema-and-dataset}

Primeiro passo para o enriquecimento [!DNL Real-time Customer Profile] com insights de pontuação, o é saber qual objeto do mundo real (como uma pessoa) seus dados definem. Compreender seus dados permite descrever e projetar uma estrutura para adicionar significado, como projetar um banco de dados relacional.

A composição de um schema começa pela atribuição de uma classe. As classes definem os aspectos comportamentais dos dados que o schema conterá (registro ou série de tempo). Para começar a criar seus próprios schemas, siga as etapas no tutorial em [criação de um esquema usando o Editor de esquemas](../../xdm/tutorials/create-schema-ui.md). Observe que, antes de poder ativar um conjunto de dados para [!DNL Profile], é necessário configurar o esquema do conjunto de dados para ter um campo de identidade primário e, em seguida, habilitar o esquema para [!DNL Profile]. Quando os dados são assimilados em um [!DNL Profile]conjunto de dados habilitado para , que os mesmos dados também sejam assimilados como [!DNL Profile] registros.

Se preferir compor um schema usando o [!DNL Schema Registry] Em vez disso, comece lendo a API [[!DNL Schema Registry] guia do desenvolvedor](../../xdm/api/getting-started.md) antes de tentar o tutorial em [criação de um schema usando a API](../../xdm/tutorials/create-schema-api.md).

Quando o esquema e o conjunto de dados estiverem preparados, você poderá gerar e assimilar dados de pontuação no conjunto de dados executando execuções de pontuação usando um modelo apropriado.

## Crie segmentos usando a [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Depois de gerar e assimilar seus insights de dados de pontuação para [!DNL Profile]conjunto de dados habilitado para , é possível criar segmentos dinâmicos usando a variável [!DNL Segment Builder].

O [!DNL Segment Builder] O fornece um espaço de trabalho avançado com o qual você pode interagir [!DNL Profile] elementos de dados. O espaço de trabalho oferece controles intuitivos para criar e editar regras, como blocos de arrastar e soltar usados para representar propriedades de dados. Siga as [[!DNL Segment Builder] guia do usuário](../../segmentation/ui/segment-builder.md) para saber mais sobre:

- Criar definições de segmento usando uma combinação de atributos, eventos e públicos-alvo existentes como blocos de construção.
- Usar a tela e os contêineres do construtor de regras para controlar a ordem em que as regras de segmento são executadas.
- Visualizar estimativas do seu público-alvo potencial, permitindo que você ajuste as definições do segmento, conforme necessário.
- Ativar todas as definições de segmento para segmentação agendada.
- Ativar definições de segmento especificadas para a segmentação de fluxo.

## Próximas etapas {#next-steps}

Para saber mais sobre os segmentos e a [!DNL Segment Builder]leia a [Visão geral do serviço de segmentação](../../segmentation/home.md).

Para saber mais sobre [!DNL Real-time Customer Profile]leia a [Visão geral do perfil do cliente em tempo real](../../profile/home.md)
