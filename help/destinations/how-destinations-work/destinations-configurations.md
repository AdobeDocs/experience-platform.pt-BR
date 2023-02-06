---
title: Configurações configuráveis e comuns de exportação em destinos
description: Saiba quais configurações de exportação em destinos são configuráveis em um nível de destino e quais são fixas e não podem ser editadas.
source-git-commit: 04322d10a88b27d5641ab9474c8387945aab9982
workflow-type: tm+mt
source-wordcount: '829'
ht-degree: 0%

---


# Configurações configuráveis e comuns de exportação em destinos

Ao pensar no comportamento de exportação para destinos Experience Platform, você precisa considerar três níveis separados nos quais as configurações agem.

* Em um primeiro nível, algumas das configurações relacionadas ao comportamento de exportação de perfil e às configurações de configuração são comuns em todos os destinos pertencentes a um tipo de destino. Essas configurações se referem ao que aciona uma exportação de destino e ao que está incluído em uma exportação e não pode ser editado por desenvolvedores de destino ou usuários de CDP em tempo real.
* Em um segundo nível, algumas configurações podem ser personalizadas em um nível de destino pelo desenvolvedor de destino ao criar destinos usando o Destination SDK.
* Em um terceiro nível, há configurações que os usuários da CDP em tempo real podem definir nos workflows de ativação.

![Diagrama que mostra a interação entre configurações de exportação comuns e configuráveis para destinos](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Esta página descreve ou vincula a todas as configurações de exportação comuns e configuráveis para destinos, nos três níveis descritos acima.

## Configurações comuns de exportação em tipos de destino {#common-settings-across-destination-types}

O comportamento de exportação de destino é consistente em todos os destinos pertencentes a um tipo de destino no que diz respeito a *o que aciona uma exportação de destino* e *o que está incluído nas exportações de destino*. As exportações de destino são acionadas pelas notificações que o serviço de destinos recebe do [Serviço de Perfil do cliente em tempo real upstream](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html?lang=en#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

O que está incluído nas exportações de destino varia um pouco entre os tipos de destino. Leia mais sobre o [padrões comuns de comportamento de exportação por tipo de destino](/help/destinations/how-destinations-work/profile-export-behavior.md). Essas configurações não podem ser editadas por desenvolvedores de destino ou usuários de CDP em tempo real.

## Configurações de exportação personalizáveis por desenvolvedores de destino {#customizable-settings-by-destination-developers}

Os desenvolvedores de destino podem usar [Destination SDK](/help/destinations/destination-sdk/overview.md) para criar destinos personalizados ou produzidos (privados ou públicos). O Destination SDK oferece aos desenvolvedores grande flexibilidade para configurar destinos com base nos recursos downstream de seus pontos de extremidade de API e sistemas de recepção de arquivos. Com base nos recursos downstream, os desenvolvedores de destino têm as seguintes opções de configuração disponíveis ao configurar um destino usando o Destination SDK:

* Determine quais atributos e identidades podem ser exportados do Experience Platform para o destino. Determine também quais identidades são exigidas pelos destinos para uma exportação de dados bem-sucedida.
* Defina uma política de agregação, que determina por quanto tempo o Experience Platform deve aguardar ao agregar mensagens HTTP a serem enviadas para integrações de API. Os desenvolvedores de destino podem configurar diferentes tipos de agregação para determinar quantos perfis devem ser incluídos nas mensagens HTTP de saída e por quanto tempo o Experience Platform deve aguardar até que a mensagem HTTP seja despachada. Encontre informações extensas sobre o [opções de configuração da política de agregação](/help/destinations/destination-sdk/destination-configuration.md#aggregation) disponível para desenvolvedores de destino na documentação do Destination SDK.
* Determine se as exportações de mensagem HTTP devem incluir perfis qualificados para segmentos, removidos dos segmentos ou ambos.
* Determine quais configurações de nome de arquivo e formatação de arquivo devem estar disponíveis para os usuários ao exportar arquivos.

## Configurações em um nível de fluxo de dados personalizáveis pelos usuários {#settings-on-dataflow-level}

Além das configurações não editáveis que dependem do tipo de destino e das configurações definidas pelo desenvolvedor de destino, há determinadas configurações de exportação que os usuários podem configurar no fluxo de trabalho de ativação. Essas configurações estão relacionadas à programação de exportação de um determinado fluxo de dados para um destino, aos atributos e campos de identidade que devem ser exportados em um fluxo de dados ou às opções de formatação de arquivo para arquivos exportados.

As configurações que estão disponíveis para os usuários ao se conectar a um destino dependem de como o destino foi configurado pelo desenvolvedor de destino e quais configurações eles disponibilizaram para os usuários.

Por exemplo, para [destinos de transmissão](/help/destinations/destination-types.md#streaming-destinations), um desenvolvedor de destino pode configurar quais identidades o destino aceita e somente essas identidades serão exibidas ao usuário em [etapa de mapeamento do fluxo de trabalho de ativação](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), conforme mostrado abaixo:

![Gravação de tela da seleção de identidade do campo de destino na etapa de mapeamento do fluxo de trabalho de ativação. ](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

Da mesma forma, para [destinos com base em arquivo](/help/destinations/destination-types.md#file-based), o desenvolvedor de destino pode determinar qual [opções de anexação do nome do arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) Querem disponibilizar para o seu destino, ou que [opções de formatação de arquivo](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) eles desejam se tornar disponíveis e o usuário poderá selecionar apenas uma dessas opções, conforme mostrado abaixo:

![Gravação de tela da opção de formatação de arquivo ao se conectar a um destino com base em arquivo.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![Gravação de tela da opção de anexação do nome de arquivo na etapa de agendamento do fluxo de trabalho de ativação. ](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

Leia mais sobre as diferentes opções e etapas disponíveis no fluxo de trabalho de ativação:

* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Ativar dados de público-alvo para destinos corporativos](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [Ativar os dados do público-alvo para os destinos de exportação do segmento de fluxo](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Exportar arquivos sob demanda para destinos em lote](/help/destinations/ui/export-file-now.md)
* [(Beta) Exportar conjuntos de dados para destinos de armazenamento em nuvem](/help/destinations/ui/export-datasets.md)

## Próximas etapas {#next-steps}

Após a leitura deste documento, você sabe quais configurações de exportação para destinos são comuns entre os tipos de destino, que podem ser configuradas em um nível de destino individual pelos desenvolvedores, e quais configurações podem ser editadas pelos usuários no fluxo de trabalho de ativação.

Para desenvolvedores de destino, você pode [introdução](/help/destinations/destination-sdk/getting-started.md) com Destination SDK. Para usuários que desejam ativar os dados, você pode fazer check-out de todos os destinos disponíveis no [catálogo](/help/destinations/catalog/overview.md).