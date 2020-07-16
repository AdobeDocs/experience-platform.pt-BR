---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriais em tempo real do Perfil do cliente
topic: tutorial
translation-type: tm+mt
source-git-commit: 5c5f6c4868e195aef76bacc0a1e5df3857647bde
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 0%

---


# Configurar [!DNL Real-time Customer Profile] e [!DNL Identity Service]

Para configurar [!DNL Real-time Customer Profile] para a sua organização, é necessário concluir vários workflows separados. Este documento descreve as etapas envolvidas e fornece links para tutoriais para a conclusão de cada fluxo de trabalho individual. Para saber mais sobre [!DNL Real-time Customer Profile], comece lendo a visão geral [do](../profile/home.md)Perfil.

## Ativar schema para [!DNL Profile] e [!DNL Identity]

Antes que os dados possam ser ingeridos no Adobe Experience Platform e usados na criação do [!DNL Real-time Customer Profiles], um schema deve ser criado para fornecer a estrutura dos dados que serão ingeridos e esse schema deve ser habilitado para uso em [!DNL Profile] e Adobe Experience Platform [!DNL Identity Service]. Para obter instruções passo a passo sobre como criar um schema que esteja ativado tanto para [!DNL Profile] quanto para [!DNL Identity Service], consulte os tutoriais para [criar um schema usando a API](../xdm/tutorials/create-schema-api.md) de Registro do Schema ou para [criar um schema usando a interface do usuário](../xdm/tutorials/create-schema-ui.md)do Construtor de Schemas.

## Configurar um conjunto de dados para [!DNL Profile] e [!DNL Identity]

Para começar a assimilar dados no [!DNL Profile], é necessário ter um conjunto de dados que tenha sido configurado corretamente para uso com [!DNL Real-time Customer Profile] e [!DNL Identity Service]. Para começar, siga o tutorial [](../profile/tutorials/dataset-configuration.md)Configurar um conjunto de dados para Perfil e identidade.

## Configurar políticas de mesclagem

O Adobe Experience Platform permite que você reúna dados de várias fontes e os combine para ver uma visualização completa de cada um de seus clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] usam para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada. Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para trabalhar com políticas de mesclagem na [!DNL Platform] interface do usuário, visite o guia [do usuário das políticas de](../profile/ui/merge-policies.md)mesclagem. Para trabalhar com políticas de mesclagem usando a API Perfil do cliente em tempo real, consulte o guia [do desenvolvedor de políticas de](../profile/api/merge-policies.md)mesclagem.

## Configurar projeções de borda

Para direcionar experiências coordenadas, consistentes e personalizadas para seus clientes em vários canais em tempo real, os dados certos precisam estar prontamente disponíveis e atualizados continuamente à medida que as mudanças acontecem. A Adobe [!DNL Experience Platform] permite esse acesso em tempo real aos dados por meio do uso de bordas conhecidas como bordas. Uma borda é um servidor localizado geograficamente que armazena dados e os torna facilmente acessíveis aos aplicativos. Os dados são roteados para uma borda por uma projeção, com um destino de projeção definindo a borda para a qual os dados serão enviados e uma configuração de projeção definindo a informação específica que será disponibilizada na borda. Para obter mais informações e começar a trabalhar com bordas, consulte o [!DNL Real-time Customer Profile] subguia da API [sobre projeções](../profile/api/edge-projections.md)de borda.

## Próximas etapas

Depois de configurar [!DNL Real-time Customer Profile] para sua organização, você pode começar a adicionar dados a perfis individuais do cliente e criar segmentos de audiência com base em atributos específicos do cliente. Para começar, consulte os seguintes tutoriais:

* [Adicionar dados ao Perfil do cliente em tempo real](../profile/tutorials/add-profile-data.md)
* [Criar um segmento](../segmentation/tutorials/create-a-segment.md)