---
keywords: Experience Platform, home, tópicos populares, Perfil do cliente em tempo real, Serviço de identidade;
solution: Experience Platform
title: Tutoriais de perfil do cliente em tempo real
topic-legacy: tutorial
type: Tutorial
description: Este documento descreve as etapas envolvidas e fornece links para tutoriais para concluir cada fluxo de trabalho individual.
exl-id: cda6e7a7-9498-454c-94df-c6271a5a4fd4
translation-type: tm+mt
source-git-commit: 5d449c1ca174cafcca988e9487940eb7550bd5cf
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 0%

---

# Configurar [!DNL Real-time Customer Profile]

Para configurar [!DNL Real-time Customer Profile] para sua organização, é necessário concluir vários workflows separados. Este documento descreve as etapas envolvidas e fornece links para tutoriais para concluir cada fluxo de trabalho individual.

Para saber mais sobre [!DNL Real-time Customer Profile], comece lendo a [Visão geral do perfil](../profile/home.md).

## Visão geral da interface do usuário do perfil do cliente em tempo real

O Perfil do cliente em tempo real cria uma visualização holística de cada cliente individual, combinando dados de vários canais, incluindo dados online, offline, CRM e de terceiros.

**Este guia ajudará você a:**
- Entenda a interface do usuário [!UICONTROL Profiles] e os recursos disponíveis.
- Visualize e gerencie os dados do seu perfil.

Para saber mais, visite o [Guia do usuário do Perfil do cliente em tempo real](../profile/ui/user-guide.md)

## API de perfil do cliente em tempo real

A API do Perfil do cliente em tempo real inclui vários endpoints. Leia a [Visão geral da API do perfil do cliente em tempo real](../profile/api/overview.md) para obter mais informações sobre cada um dos endpoints disponíveis e seus casos de uso.

Para saber mais e obter os valores necessários para executar operações CRUD com a API do Perfil do cliente em tempo real, visite o [guia de introdução](../profile/api/getting-started.md).

## Ativar um esquema para [!DNL Profile] e [!DNL Identity] Serviço

Para que os dados possam ser assimilados no Adobe Experience Platform e usados na criação de [!DNL Real-time Customer Profiles], um schema deve ser criado para fornecer a estrutura dos dados que serão assimilados e esse schema deve ser habilitado para uso em [!DNL Profile] e Adobe Experience Platform [!DNL Identity Service].

**Este guia ajudará você a:**
- Procurar esquemas existentes.
- Criar e nomear um esquema.
- Adicione e defina mixins XDM.
- Defina os campos de esquema como campos de identidade.
- Ative o Perfil para o esquema.

Para obter instruções passo a passo sobre a criação de um esquema habilitado para [!DNL Profile] e [!DNL Identity Service], consulte os tutoriais para [criar um esquema usando a API do Registro de Esquema](../xdm/tutorials/create-schema-api.md) ou [criar um esquema usando a interface do usuário do Construtor de Esquemas](../xdm/tutorials/create-schema-ui.md).

## Configurar um conjunto de dados para [!DNL Profile] e [!DNL Identity]

Para começar a assimilar dados em [!DNL Profile], você deve ter um conjunto de dados que tenha sido configurado corretamente para uso com [!DNL Real-time Customer Profile] e [!DNL Identity Service].

**Este guia ajudará você a:**
- Crie um conjunto de dados habilitado para o Perfil.
- Configurar conjuntos de dados existentes.
- Assimilar dados no conjunto de dados.
- Confirme se o conjunto de dados está habilitado para Perfil e usando o Serviço de identidade.

Para começar, siga o tutorial de API para [configurar um conjunto de dados para Perfil e Identidade](../profile/tutorials/dataset-configuration.md).

## Configurar políticas de mesclagem

O Adobe Experience Platform permite reunir dados de várias fontes e combiná-los para ver uma visualização completa de cada um dos clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] usa para determinar como os dados serão priorizados e quais dados serão combinados para criar essa exibição unificada.

**Este guia ajudará você a:**
- Crie novas políticas de mesclagem.
- Gerencie as políticas de mesclagem existentes.
- Defina uma política de mesclagem padrão para sua organização.
- Entenda as violações da política de mesclagem.

Para trabalhar com políticas de mesclagem na interface do usuário [!DNL Platform], visite o [guia do usuário de políticas de mesclagem](../profile/ui/merge-policies.md). Para trabalhar com políticas de mesclagem usando a API de Perfil do cliente em tempo real, consulte o [guia do desenvolvedor de políticas de mesclagem](../profile/api/merge-policies.md).

## Configurar projeções de borda

Para direcionar experiências coordenadas, consistentes e personalizadas para seus clientes em vários canais em tempo real, os dados certos precisam estar prontamente disponíveis e atualizados continuamente conforme as mudanças acontecem. Adobe [!DNL Experience Platform] permite esse acesso em tempo real aos dados por meio do uso de bordas conhecidas como . Uma borda é um servidor localizado geograficamente que armazena dados e a torna acessível para os aplicativos. Os dados são roteados para uma borda por uma projeção, com um destino de projeção definindo a borda para a qual os dados serão enviados e uma configuração de projeção definindo as informações específicas que serão disponibilizadas na borda.

**Este guia ajudará você a:**
- Liste, crie, exiba, atualize e exclua um destino de projeção de borda.
- Liste e crie uma configuração de projeção de borda.
- Entenda os seletores.

Para obter mais informações e começar a trabalhar com bordas, consulte o [!DNL Real-time Customer Profile] sub-guia da API [em projeções de borda](../profile/api/edge-projections.md).

## Personalizar como os dados do Perfil são exibidos na interface do usuário

Na interface do usuário do Experience Platform, é possível visualizar e interagir com os dados do Perfil do cliente em tempo real na forma de perfis do cliente. As informações de perfil exibidas na interface do usuário foram unidas de vários fragmentos de perfil para formar uma única visualização de cada cliente individual. Isso inclui detalhes como atributos básicos, identidades vinculadas e preferências de canal. Os campos padrão mostrados nos perfis também podem ser alterados em um nível organizacional para exibir os atributos preferenciais do perfil.

**Este guia ajudará você a:**
- Reordenar, redimensionar, editar e remover cartões.
- Adicionar atributos.
- Adicione um novo cartão.
- Restaurar padrões.

Para saber mais sobre como personalizar dados de perfil, visite a [Documentação de personalização de perfil](../profile/ui/profile-customization.md)

## Próximas etapas

Depois de configurar [!DNL Real-time Customer Profile] para sua organização, você pode começar a adicionar dados a perfis de clientes individuais e criar segmentos de público-alvo com base em atributos específicos do cliente. Para começar, consulte os seguintes tutoriais:

- [Adicionar dados ao perfil do cliente em tempo real](../profile/tutorials/add-profile-data.md)
- [Criar um segmento](../segmentation/tutorials/create-a-segment.md)
