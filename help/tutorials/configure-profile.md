---
keywords: Experience Platform;home;popular topics;Real-time Customer Perfil;Identity Service;
solution: Experience Platform
title: Tutoriais em tempo real do Perfil do cliente
topic: tutorial
type: Tutorial
description: Este documento descreve as etapas envolvidas e fornece links para tutoriais para a conclusão de cada fluxo de trabalho individual.
translation-type: tm+mt
source-git-commit: 0aa59a5375757f81d63ac43d778ff2c7179d449b
workflow-type: tm+mt
source-wordcount: '795'
ht-degree: 0%

---


# Configurar [!DNL Real-time Customer Profile]

Para configurar [!DNL Real-time Customer Profile] para a sua organização, é necessário concluir vários workflows separados. Este documento descreve as etapas envolvidas e fornece links para tutoriais para a conclusão de cada fluxo de trabalho individual.

Para saber mais sobre [!DNL Real-time Customer Profile], comece lendo a [visão geral do Perfil](../profile/home.md).

## Visão geral da interface do usuário do Perfil do cliente em tempo real

O Perfil de cliente em tempo real cria uma visualização holística de cada um de seus clientes individuais, combinando dados de vários canais, incluindo dados online, offline, CRM e de terceiros.

**Este guia o ajudará a:**
- Entenda a interface do usuário [!UICONTROL Perfis] e os recursos disponíveis.
- Visualização e gerenciamento dos dados do Perfil.

Para saber mais, visite o [Guia do usuário do Perfil do cliente em tempo real](../profile/ui/user-guide.md)

## API de Perfil do cliente em tempo real

A API de Perfil do cliente em tempo real inclui vários pontos de extremidade. Leia a [Visão geral da API do Perfil do cliente em tempo real](../profile/api/overview.md) para obter mais informações sobre cada um dos pontos finais disponíveis e seus casos de uso.

Para saber mais e obter os valores necessários para executar operações CRUD com a API Perfil do cliente em tempo real, visite o [guia de introdução](../profile/api/getting-started.md).

## Habilitar um schema para os serviços [!DNL Profile] e [!DNL Identity]

Para que os dados possam ser ingeridos no Adobe Experience Platform e usados na criação de [!DNL Real-time Customer Profiles], um schema deve ser criado para fornecer a estrutura dos dados que serão ingeridos e esse schema deve ser habilitado para uso em [!DNL Profile] e Adobe Experience Platform [!DNL Identity Service].

**Este guia o ajudará a:**
- Navegue pelos schemas existentes.
- Crie e nomeie um schema.
- Adicione e defina misturas XDM.
- Defina os campos do schema como campos de identidade.
- Ative o Perfil para o seu schema.

Para obter instruções passo a passo sobre como criar um schema que esteja ativado para [!DNL Profile] e [!DNL Identity Service], consulte os tutoriais para [criar um schema usando a API do Registro do Schema](../xdm/tutorials/create-schema-api.md) ou [criar um schema usando a interface do usuário do Construtor de Schemas](../xdm/tutorials/create-schema-ui.md).

## Configurar um conjunto de dados para [!DNL Profile] e [!DNL Identity]

Para começar a assimilar dados em [!DNL Profile], você deve ter um conjunto de dados que tenha sido configurado corretamente para uso com [!DNL Real-time Customer Profile] e [!DNL Identity Service].

**Este guia o ajudará a:**
- Crie um conjunto de dados habilitado para o Perfil.
- Configure os conjuntos de dados existentes.
- Insira dados no conjunto de dados.
- Confirme se o conjunto de dados está habilitado para Perfil e usando o Serviço de identidade.

Para começar, siga o tutorial da API para [configurar um conjunto de dados para Perfil e Identity](../profile/tutorials/dataset-configuration.md).

## Configurar políticas de mesclagem

A Adobe Experience Platform permite que você reúna dados de várias fontes e os combine para ver uma visualização completa de cada um de seus clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] usa para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada.

**Este guia o ajudará a:**
- Criar novas políticas de mesclagem.
- Gerenciar políticas de mesclagem existentes.
- Defina uma política de mesclagem padrão para sua organização.
- Entenda as violações da política de mesclagem.

Para trabalhar com políticas de mesclagem na interface do usuário [!DNL Platform], visite o [guia do usuário de políticas de mesclagem](../profile/ui/merge-policies.md). Para trabalhar com políticas de mesclagem usando a API Perfil do cliente em tempo real, consulte o [guia do desenvolvedor de políticas de mesclagem](../profile/api/merge-policies.md).

## Configurar projeções de borda

Para direcionar experiências coordenadas, consistentes e personalizadas para seus clientes em vários canais em tempo real, os dados certos precisam estar prontamente disponíveis e atualizados continuamente à medida que as mudanças acontecem. Adobe [!DNL Experience Platform] permite esse acesso em tempo real aos dados por meio do uso de bordas conhecidas como bordas. Uma borda é um servidor localizado geograficamente que armazena dados e os torna facilmente acessíveis aos aplicativos. Os dados são roteados para uma borda por uma projeção, com um destino de projeção definindo a borda para a qual os dados serão enviados e uma configuração de projeção definindo a informação específica que será disponibilizada na borda.

**Este guia o ajudará a:**
- Lista, criação, visualização, atualização e exclusão de um destino de projeção de borda.
- Lista e crie uma configuração de projeção de borda.
- Entenda os seletores.

Para obter mais informações e começar a trabalhar com bordas, consulte o subguia [!DNL Real-time Customer Profile] da API [em projeções de borda](../profile/api/edge-projections.md).

## Personalizar como os dados do Perfil são exibidos na interface do usuário

Na interface do usuário do Experience Platform, você pode visualização e interagir com os dados do Perfil do cliente em tempo real na forma de perfis do cliente. As informações do perfil exibidas na interface do usuário foram unidas de vários fragmentos de perfil para formar uma única visualização de cada cliente individual. Isso inclui detalhes como atributos básicos, identidades vinculadas e preferências de canal. Os campos padrão mostrados nos perfis também podem ser alterados em nível organizacional para exibir os atributos preferenciais do Perfil.

**Este guia o ajudará a:**
- Reorganize, redimensione, edite e remova cartões.
- Adicione atributos.
- Adicione um novo cartão.
- Restaurar padrões.

Para saber mais sobre como personalizar os dados do perfil, visite a [documentação de personalização do Perfil](../profile/ui/profile-customization.md)

## Próximas etapas

Depois de configurar [!DNL Real-time Customer Profile] para sua organização, você pode começar a adicionar dados a perfis individuais do cliente e criar segmentos de audiência com base em atributos específicos do cliente. Para começar, consulte os seguintes tutoriais:

- [Adicionar dados ao Perfil do cliente em tempo real](../profile/tutorials/add-profile-data.md)
- [Criar um segmento](../segmentation/tutorials/create-a-segment.md)