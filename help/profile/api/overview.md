---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, solução de problemas, API, perfil unificado, perfil unificado, unificado, perfil, rtcp, ativar perfil, Ativar perfil
title: Guia da API do perfil do cliente em tempo real
description: A API de perfil do cliente em tempo real permite que os desenvolvedores explorem e trabalhem com dados de perfil, incluindo perfis de exibição, criem e atualizem políticas de mesclagem, exportem ou exemplificem dados de perfil, e excluam dados de perfil que não são mais necessários ou foram adicionados com erro. Siga este manual para saber como executar operações importantes usando a API.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 3b34cf37182ae98545651a7b54f586df7d811f34
workflow-type: tm+mt
source-wordcount: '963'
ht-degree: 1%

---

# [!DNL Real-time Customer Profile] Manual da API

[!DNL Real-time Customer Profile] O permite ver uma exibição holística de cada um dos clientes individuais no Adobe Experience Platform. [!DNL Profile] O permite consolidar dados diferentes do cliente de vários canais, como dados online, offline, CRM e de terceiros, em uma visualização unificada que oferece uma conta acionável com carimbo de data e hora de cada interação do cliente.

A API [!DNL Real-time Customer Profile] inclui vários endpoints, descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte o [guia de introdução](getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

Para visualizar todos os endpoints e operações CRUD disponíveis, visite o [Swagger de referência da API do perfil do cliente em tempo real](https://www.adobe.com/go/profile-apis-en).

Para obter um guia sobre como trabalhar com dados [!DNL Real-time Customer Profile] na interface do usuário [!DNL Experience Platform], consulte o [Guia do usuário de perfil](../ui/user-guide.md).

## (Alfa) Atributos calculados {#computed-attributes}

>[!IMPORTANT]
>
>A funcionalidade de atributo calculado está em alfa e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Atributos calculados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são calculadas automaticamente para que possam ser usadas na segmentação, ativação e personalização.

Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil. Esses cálculos ajudam você a responder facilmente perguntas relacionadas a coisas como valor de compra vitalícia, tempo entre compras ou número de aberturas de aplicativos, sem exigir a execução manual de cálculos complexos sempre que as informações forem necessárias. Esses valores de atributos calculados podem ser visualizados em um perfil, usados para criar um segmento ou acessados por meio de vários padrões de acesso diferentes.

Você pode criar, exibir, editar e excluir atributos calculados usando o endpoint `config/computedAttributes`. Para saber como usar atributos calculados, consulte a [visão geral dos atributos calculados](../computed-attributes/overview.md). Para operações de API, visite o [guia do endpoint da API de atributos calculados](../computed-attributes/ca-api.md).

## Projeções de borda {#edge-projections}

O Adobe Experience Platform permite a personalização em tempo real das experiências do cliente, tornando os dados facilmente acessíveis em servidores estrategicamente localizados, chamados de &quot;bordas&quot;. A API [!DNL Real-time Customer Profile] fornece endpoints para trabalhar com bordas por meio de componentes chamados &quot;projeções&quot;. Isso inclui configurações de projeção para determinar quais dados devem ser projetados para cada borda, bem como destinos de projeção para definir onde rotear uma projeção. Para obter informações detalhadas sobre como trabalhar com projeções de borda, visite o [guia de configurações e pontos de extremidade de projeção](edge-projections.md).

## Entidades ([!DNL Profile] acesso) {#entities}

Por meio do Adobe Experience Platform, você pode acessar os dados [!DNL Real-time Customer Profile] usando as APIs RESTful ou a interface do usuário. Para saber como acessar entidades, mais comumente conhecidas como &quot;perfis&quot;, usando a API, siga as etapas descritas no [guia de ponto de extremidade de entidades](entities.md). Para acessar perfis usando a interface [!DNL Platform], consulte o [Guia do usuário de perfil](../ui/user-guide.md).

## Exportar tarefas ([!DNL Profile] exportar) {#profile-export}

[!DNL Real-time Customer Profile] os dados podem ser exportados para um conjunto de dados para processamento adicional, como exportar segmentos de público-alvo para ativação ou atributos de perfil para relatórios. Exportar tarefas para segmentos de público-alvo fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Leia o [guia do endpoint de tarefas de exportação de segmentação](../../profile/api/export-jobs.md) para saber mais. Para obter instruções passo a passo sobre como criar e gerenciar tarefas de exportação para atributos de perfil, visite o [guia de endpoint de tarefas de exportação](export-jobs.md).

## Mesclar políticas {#merge-policies}

Ao reunir dados de várias fontes em [!DNL Experience Platform], as políticas de mesclagem são as regras que [!DNL Platform] usa para determinar como os dados serão priorizados e quais dados serão combinados para criar perfis de clientes individuais. Usando a API [!DNL Real-time Customer Profile], você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para trabalhar com políticas de mesclagem usando a API, visite o [guia do ponto de extremidade de políticas de mesclagem](merge-policies.md).

Para saber mais sobre as políticas de mesclagem e sua função na Plataforma, comece lendo a [visão geral das políticas de mesclagem](../merge-policies/overview.md).

## Visualizar o status da amostra ([!DNL Profile] pré-visualização) {#profile-preview}

À medida que os dados são assimilados no Platform, um trabalho de amostra é executado para atualizar a contagem de perfis e outras métricas relacionadas aos dados do Perfil do cliente em tempo real. Os resultados desse trabalho de amostra podem ser exibidos usando o endpoint `/previewsamplestatus`, parte da API do Perfil do cliente em tempo real. Esse endpoint também pode ser usado para listar distribuições de perfil pelo conjunto de dados e namespace de identidade, bem como para gerar vários relatórios para ganhar visibilidade sobre a composição da Loja de perfis da sua organização.  Para começar a usar o endpoint `/profilepreviewstatus`, consulte o [guia do endpoint de status de amostra de visualização](preview-sample-status.md).

## Tarefas do sistema de perfil {#profile-system-jobs}

Os dados habilitados para perfil assimilados em [!DNL Platform] são armazenados no [!DNL Data Lake], bem como no armazenamento de dados [!DNL Real-time Customer Profile]. Ocasionalmente, pode ser necessário excluir um conjunto de dados ou lote do armazenamento [!DNL Profile] para remover dados que você não precisa mais ou que foram adicionados com erro. Isso requer o uso da API para criar um [!DNL Profile System Job], também conhecido como &quot;[!DNL delete request]&quot;, que pode ser modificado, monitorado ou excluído, se necessário. Para saber como trabalhar com solicitações de exclusão usando o endpoint `/system/jobs` na API [!DNL Real-time Customer Profile], siga as etapas descritas no [guia do endpoint de tarefas do sistema de perfil](profile-system-jobs.md).

## Atualizar atributos de perfis {#update-profile}

Ocasionalmente, pode ser necessário atualizar os dados na Loja de perfis de sua organização. Por exemplo, talvez seja necessário corrigir registros ou alterar um valor de atributo. Isso pode ser feito por meio de assimilação em lote ou streaming e requer um conjunto de dados habilitado para perfil configurado com uma tag de atualização. Para obter mais informações sobre como configurar um conjunto de dados para atualizações de atributos, consulte o tutorial para [ativar um conjunto de dados para Perfil e sert](../../catalog/datasets/enable-upsert.md).

## Próximas etapas {#next-steps}

Para começar a fazer chamadas usando a API [!DNL Real-time Customer Profile], leia o [guia de introdução](getting-started.md) e selecione um dos guias de ponto de extremidade para saber como usar endpoints específicos relacionados a [!DNL Profile]. Para trabalhar com dados [!DNL Profile] usando a interface [!DNL Experience Platform], consulte o [Guia do usuário do Perfil do cliente em tempo real](../ui/user-guide.md).
