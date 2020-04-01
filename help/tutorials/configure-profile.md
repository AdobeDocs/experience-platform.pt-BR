---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Tutoriais em tempo real do Perfil do cliente
topic: tutorial
translation-type: tm+mt
source-git-commit: ee08f43400fa72abce95ed52aff879f954f4b4d6

---


# Configurar o Perfil do cliente e o serviço de identidade em tempo real

Para configurar o Perfil do cliente em tempo real para a sua organização, é necessário concluir vários workflows separados. Este documento descreve as etapas envolvidas e fornece links para tutoriais para a conclusão de cada fluxo de trabalho individual. Para saber mais sobre o Perfil do cliente em tempo real, comece lendo a visão geral [do](../profile/home.md)Perfil.

## Ativar schema para Perfil e identidade

Para que os dados possam ser assimilados na Adobe Experience Platform e usados na criação de Perfis do cliente em tempo real, um schema deve ser criado para fornecer a estrutura dos dados que serão assimilados e esse schema deve ser habilitado para uso no Perfil e no Adobe Experience Platform Identity Service. Para obter instruções passo a passo sobre como criar um schema que esteja ativado para Perfil e Serviço de identidade, consulte os tutoriais para [criar um schema usando a API](../xdm/tutorials/create-schema-api.md) do Registro do Schema ou [criar um schema usando a interface do usuário](../xdm/tutorials/create-schema-ui.md)do Construtor de Schemas.

## Configurar um conjunto de dados para Perfil e identidade

Para começar a assimilar dados no Perfil, é necessário ter um conjunto de dados que tenha sido configurado corretamente para uso com o Perfil do cliente em tempo real e o Serviço de identidade. Para começar, siga o tutorial [](../profile/tutorials/dataset-configuration.md)Configurar um conjunto de dados para Perfil e identidade.

## Configurar políticas de mesclagem

A plataforma Adobe Experience permite que você reúna dados de várias fontes e os combine para ver uma visualização completa de cada um de seus clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que a Plataforma usa para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada. Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para trabalhar com políticas de mesclagem na interface do usuário da plataforma, visite o guia [do usuário das políticas de](../profile/ui/merge-policies.md)mesclagem. Para trabalhar com políticas de mesclagem usando a API Perfil do cliente em tempo real, consulte o guia [do desenvolvedor de políticas de](../profile/api/merge-policies.md)mesclagem.

## Configurar projeções de borda

Para direcionar experiências coordenadas, consistentes e personalizadas para seus clientes em vários canais em tempo real, os dados certos precisam estar prontamente disponíveis e atualizados continuamente à medida que as mudanças acontecem. A plataforma Adobe Experience permite esse acesso em tempo real aos dados por meio do uso de bordas conhecidas como bordas. Uma borda é um servidor localizado geograficamente que armazena dados e os torna facilmente acessíveis aos aplicativos. Os dados são roteados para uma borda por uma projeção, com um destino de projeção definindo a borda para a qual os dados serão enviados e uma configuração de projeção definindo a informação específica que será disponibilizada na borda. Para obter mais informações e começar a trabalhar com bordas, consulte o [subguia da API do Perfil do cliente em tempo real sobre projeções](../profile/api/edge-projections.md)de borda.

## Próximas etapas

Depois de configurar o Perfil do cliente em tempo real para sua organização, você pode começar a adicionar dados a perfis individuais do cliente e criar segmentos de audiência com base em atributos específicos do cliente. Para começar, consulte os seguintes tutoriais:

* [Adicionar dados ao Perfil do cliente em tempo real](../profile/tutorials/add-profile-data.md)
* [Criar um segmento](../segmentation/tutorials/create-a-segment.md)