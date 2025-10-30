---
title: Configurações de exportação configuráveis e comuns em destinos
description: Saiba quais configurações de exportação em destinos são configuráveis em um nível de destino e quais são fixas e não podem ser editadas.
exl-id: 3f4706cb-6d51-4567-81f6-5b2bf167b576
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Configurações de exportação configuráveis e comuns em destinos

Ao pensar no comportamento de exportação para destinos do Experience Platform, é necessário considerar três níveis separados nos quais as configurações agem.

* Em um primeiro nível, algumas das configurações relacionadas ao comportamento de exportação do perfil e às configurações são comuns em todos os destinos que pertencem a um tipo de destino. Essas configurações se referem ao que aciona uma exportação de destino e ao que está incluído em uma exportação e não pode ser editado por desenvolvedores de destino ou usuários do Real-Time CDP.
* Em um segundo nível, algumas configurações podem ser personalizadas em um nível de destino pelo desenvolvedor de destino ao criar destinos usando o Destination SDK.
* Em um terceiro nível, há definições de configuração que os usuários do Real-Time CDP podem definir nos workflows de ativação.

![Diagrama mostrando a interação entre configurações de exportação comuns e configuráveis para destinos](/help/destinations/assets/how-destinations-work/profile-export-behavior-diagram.png)

Esta página descreve ou cria links para todas as definições de exportação comuns e configuráveis para destinos, nos três níveis descritos acima.

## Configurações comuns de exportação em tipos de destino {#common-settings-across-destination-types}

O comportamento de exportação de destino é consistente entre destinos pertencentes a um tipo de destino no que diz respeito a *o que aciona uma exportação de destino* e *o que está incluído nas exportações de destino*. As exportações de destino são acionadas por notificações que o serviço de destinos recebe do [serviço upstream de Perfil do Cliente em Tempo Real](https://experienceleague.adobe.com/docs/blueprints-learn/architecture/architecture-overview/platform-applications.html#adobe-experience-platform-%26-applications-detailed-architecture-diagram).

O que está incluído nas exportações de destino varia ligeiramente entre os tipos de destino. Leia mais sobre os [padrões de comportamento de exportação comuns por tipo de destino](/help/destinations/how-destinations-work/profile-export-behavior.md). Essas configurações não podem ser editadas por desenvolvedores de destino ou usuários do Real-Time CDP.

## Configurações de exportação personalizáveis por desenvolvedores de destino {#customizable-settings-by-destination-developers}

Os desenvolvedores de destino podem usar o [Destination SDK](/help/destinations/destination-sdk/overview.md) para criar destinos personalizados ou de produção (privados ou públicos). O Destination SDK fornece aos desenvolvedores grande flexibilidade para configurar destinos com base nos recursos de downstream de seus endpoints de API e sistemas de recepção de arquivos. Com base nos recursos de downstream, os desenvolvedores de destino têm as seguintes opções de configuração disponíveis ao configurar um destino usando o Destination SDK:

* Determine quais atributos e identidades podem ser exportados do Experience Platform para o destino. Determine também quais identidades são exigidas por seus destinos para uma exportação de dados bem-sucedida.
* Defina uma política de agregação, que determina por quanto tempo o Experience Platform deve aguardar ao agregar mensagens HTTP para serem enviadas às integrações de API. Os desenvolvedores de destino podem configurar diferentes tipos de agregação para determinar quantos perfis devem ser incluídos em mensagens HTTP de saída e quanto tempo o Experience Platform deve esperar até que a mensagem HTTP seja despachada. Encontre informações abrangentes sobre as [opções de configuração de política de agregação](../destination-sdk/functionality/destination-configuration/aggregation-policy.md) disponíveis para desenvolvedores de destino na documentação do Destination SDK.
* Determine se as exportações de mensagens HTTP devem incluir perfis qualificados para segmentos, que são removidos de segmentos ou ambos.
* Determine quais configurações de nome de arquivo e formatação de arquivo devem estar disponíveis para os usuários ao exportar arquivos.

## Configurações em nível de fluxo de dados personalizáveis por usuários {#settings-on-dataflow-level}

Além das configurações não editáveis que dependem do tipo de destino e das configurações definidas pelo desenvolvedor de destino, há determinadas configurações de exportação que os usuários podem definir no fluxo de trabalho de ativação. Essas configurações estão relacionadas ao agendamento de exportação para um determinado fluxo de dados para um destino, aos atributos e campos de identidade que devem ser exportados em um fluxo de dados ou às opções de formatação de arquivo para arquivos exportados.

As configurações disponíveis para os usuários ao se conectarem a um destino dependem de como o destino foi definido pelo desenvolvedor de destino e quais configurações eles disponibilizaram para os usuários.

Por exemplo, para [destinos de streaming](/help/destinations/destination-types.md#streaming-destinations), um desenvolvedor de destino pode configurar quais identidades seu destino aceita e somente essas identidades serão exibidas para o usuário na [etapa de mapeamento do fluxo de trabalho de ativação](/help/destinations/ui/activate-segment-streaming-destinations.md#mapping), conforme mostrado abaixo:

![Gravação de tela da seleção de identidade para o campo de destino na etapa de mapeamento do fluxo de trabalho de ativação.](/help/destinations/assets/how-destinations-work/identity-mapping-example.gif)

Da mesma forma, para [destinos baseados em arquivo](/help/destinations/destination-types.md#file-based), o desenvolvedor de destino pode determinar quais [opções de acréscimo de nome de arquivo](/help/destinations/ui/activate-batch-profile-destinations.md#file-names) ele deseja disponibilizar para seu destino ou quais [opções de formatação de arquivo](/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md) ele deseja disponibilizar, e o usuário poderá selecionar apenas dessas opções, conforme mostrado abaixo:

![Gravação de tela da opção de formatação de arquivo ao conectar-se a um destino baseado em arquivo.](/help/destinations/assets/how-destinations-work/file-formatting-options.gif)

![Gravação de tela da opção de acréscimo de nome de arquivo na etapa de agendamento do fluxo de trabalho de ativação.](/help/destinations/assets/how-destinations-work/filename-append-options.gif)

Leia mais sobre as diferentes opções e etapas disponíveis no fluxo de trabalho de ativação:

* [Ativar dados do público-alvo para destinos de exportação de perfil em lote](/help/destinations/ui/activate-batch-profile-destinations.md)
* [Ativar dados de público-alvo para destinos corporativos](/help/destinations/ui/activate-streaming-profile-destinations.md)
* [Ativar dados do público-alvo para streaming de destinos de exportação de público](/help/destinations/ui/activate-segment-streaming-destinations.md)
* [Exportar arquivos por demanda para destinos em lote](/help/destinations/ui/export-file-now.md)
* [Exportar conjuntos de dados para destinos de armazenamento na nuvem](/help/destinations/ui/export-datasets.md)

## Próximas etapas {#next-steps}

Depois de ler este documento, agora você sabe quais configurações de exportação para destinos são comuns entre tipos de destino, quais podem ser configuradas em um nível de destino individual por desenvolvedores e quais configurações podem ser editadas pelos usuários no fluxo de trabalho de ativação.

Em seguida, você pode ler informações mais detalhadas sobre os [padrões comuns de comportamento de exportação por tipo de destino](/help/destinations/how-destinations-work/profile-export-behavior.md).

Para desenvolvedores de destino, você pode [começar](/help/destinations/destination-sdk/getting-started.md) com o Destination SDK. Para usuários que desejam ativar dados, você pode verificar todos os destinos disponíveis no [catálogo](/help/destinations/catalog/overview.md).
