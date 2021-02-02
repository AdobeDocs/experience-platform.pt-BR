---
keywords: Experience Platform;modelo de aprendizado de máquina;Data Science Workspace;Perfil do cliente em tempo real;tópicos populares;insights de aprendizado de máquina
solution: Experience Platform
title: Enriqueça o Perfil do cliente em tempo real com insights de aprendizado de máquina
topic: tutorial
type: Tutorial
description: Este documento fornece um guia sobre como enriquecer o Perfil do cliente em tempo real com informações aprendidas pela máquina.
translation-type: tm+mt
source-git-commit: 62e6bb7e72637b06808ff87dc21f40af2c4e2d45
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 0%

---


# Enriqueça [!DNL Real-time Customer Profile] com insights de aprendizado de máquina

A Adobe Experience Platform [!DNL Data Science Workspace] fornece as ferramentas e os recursos para criar, avaliar e utilizar modelos de aprendizado automatizado para gerar previsões e insights de dados. Quando insights de aprendizado de máquina são ingeridos em um conjunto de dados habilitado para [!DNL Profile], esses mesmos dados também são ingeridos como [!DNL Profile] registros que podem ser segmentados usando [!DNL Adobe Experience Platform Segmentation Service]. À medida que os dados de perfil e de série cronológica são ingeridos, o Perfil de cliente em tempo real decide automaticamente incluir ou excluir esses dados dos segmentos por meio de um processo contínuo chamado de segmentação de fluxo contínuo, antes de mesclá-los com os dados existentes e atualizar a visualização da união. Como resultado, você pode executar instantaneamente computações e tomar decisões para oferecer experiências aprimoradas e individualizadas aos clientes à medida que eles interagem com sua marca.

Este documento fornece links para tutoriais que permitem enriquecer [!DNL Real-time Customer Profile] com seus insights aprendidos pela máquina.

## Introdução

Para concluir os tutoriais abaixo, é necessário que você tenha um entendimento prático sobre como assimilar [!DNL Profile] dados e criar segmentos. Antes de iniciar este tutorial, reveja a documentação dos seguintes serviços:

- [[!DNL Real-time Customer Profile]](../../profile/home.md): Fornece uma representação completa e unificada de cada cliente individual com base em dados agregados de várias fontes.
- [[!DNL Identity Service]](../../identity-service/home.md): Habilita  [!DNL Real-time Customer Profile] ao fazer a ponte entre identidades de diferentes fontes de dados que estão sendo ingeridas na Plataforma.
- [[!DNL Experience Data Model (XDM)]](../../xdm/home.md): A estrutura padronizada pela qual a Plataforma organiza os dados de experiência do cliente.

Além dos documentos mencionados acima, é altamente recomendável que você também reveja os seguintes guias sobre schemas e o Editor de Schemas:

- [Noções básicas da composição](../../xdm/schema/composition.md) do schema: Descreve schemas XDM, blocos de construção, princípios e práticas recomendadas para a composição de schemas a serem usados em  [!DNL Experience Platform].
- [Tutorial](../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Fornece instruções detalhadas para a criação de schemas usando o Editor de Schemas em  [!DNL Experience Platform].

## Criar e configurar um schema de saída e um conjunto de dados {#create-an-output-schema-and-dataset}

O primeiro passo para enriquecer [!DNL Real-time Customer Profile] com insights de pontuação é saber qual objeto real (como uma pessoa) seus dados definem. Compreender seus dados permite descrever e projetar uma estrutura para adicionar significado, como projetar um banco de dados relacional.

A composição de um schema começa com a atribuição de uma classe. As classes definem os aspectos comportamentais dos dados que o schema conterá (registro ou série cronológica). Para o start de criar seus próprios schemas, siga as etapas no tutorial em [criar um schema usando o Editor de Schemas](../../xdm/tutorials/create-schema-ui.md). Observe que antes de habilitar um conjunto de dados para [!DNL Profile], é necessário configurar o schema do conjunto de dados para que ele tenha um campo de identidade primário e depois habilitar o schema para [!DNL Profile]. Quando os dados são ingeridos em um conjunto de dados habilitado para [!DNL Profile], esses mesmos dados também são ingeridos como registros [!DNL Profile].

Se preferir compor um schema usando a API [!DNL Schema Registry], leia o [[!DNL Schema Registry] guia do desenvolvedor](../../xdm/api/getting-started.md) antes de tentar o tutorial em [criar um schema usando a API](../../xdm/tutorials/create-schema-api.md).

Depois que o schema e o conjunto de dados estiverem preparados, você poderá gerar e assimilar dados de pontuação ao conjunto de dados executando execuções de pontuação usando um modelo apropriado.

## Criar segmentos usando [!DNL Segment Builder] {#create-segments-using-the-segment-builder}

Depois de gerar e assimilar seus insights de dados de pontuação no conjunto de dados habilitado para [!DNL Profile], você pode criar segmentos dinâmicos usando [!DNL Segment Builder].

O [!DNL Segment Builder] fornece um espaço de trabalho avançado que permite interagir com elementos de dados [!DNL Profile]. A área de trabalho fornece controles intuitivos para criar e editar regras, como os blocos de arrastar e soltar usados para representar propriedades de dados. Siga o [[!DNL Segment Builder] guia do usuário](../../segmentation/ui/segment-builder.md) para saber mais sobre:

- Criar definições de segmento usando uma combinação de atributos, eventos e audiências existentes como blocos de construção.
- Usar a tela e os container do construtor de regras para controlar a ordem na qual as regras de segmento são executadas.
- Exibindo estimativas da sua audiência prospetiva, permitindo que você ajuste suas definições de segmento, conforme necessário.
- Ativar todas as definições de segmento para segmentação programada.
- Habilitar definições de segmento especificadas para a segmentação de streaming.

## Próximas etapas {#next-steps}

Para saber mais sobre os segmentos e [!DNL Segment Builder], leia a [visão geral do Serviço de Segmentação](../../segmentation/home.md).

Para saber mais sobre [!DNL Real-time Customer Profile], leia a [Visão geral do Perfil do cliente em tempo real](../../profile/home.md)