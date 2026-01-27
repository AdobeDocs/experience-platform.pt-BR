---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API;perfil unificado;Perfil unificado;perfil;habilitar perfil;perfil;;perfil;perfil em tempo real;solução de problemas;API;perfil unificado;perfil unificado;perfil;unificado;perfil;rtcp;habilitar perfil;Habilitar perfil
title: Guia da API do Perfil do cliente em tempo real
description: A API de perfil do cliente em tempo real permite que os desenvolvedores explorem e trabalhem com dados de perfil, incluindo a visualização de perfis, a criação e a atualização de políticas de mesclagem, a exportação ou a amostragem de dados de perfil e a exclusão de dados de perfil que não são mais necessários ou que foram adicionados por engano. Siga este manual para saber como executar operações importantes usando a API.
role: Developer
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 82a9b405a1d36155c84cd27a005c7ec469164ef3
workflow-type: tm+mt
source-wordcount: '874'
ht-degree: 2%

---

# [!DNL Real-Time Customer Profile] Manual da API

O [!DNL Real-Time Customer Profile] permite que você veja uma visão holística de cada cliente individual dentro da Adobe Experience Platform. O [!DNL Profile] permite consolidar dados diferentes do cliente de vários canais, como dados online, offline, CRM e de terceiros, em uma exibição unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

A API [!DNL Real-Time Customer Profile] inclui vários endpoints, descritos abaixo. Visite os manuais de endpoint individuais para obter detalhes e consulte o [guia de introdução](getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de exemplo e muito mais.

Para exibir todos os pontos de extremidade e operações CRUD disponíveis, visite o [swagger de Referência da API de perfil do cliente em tempo real](https://www.adobe.com/go/profile-apis-en).

Para obter um guia para trabalhar com dados do [!DNL Real-Time Customer Profile] na interface do usuário do [!DNL Experience Platform], consulte o [Guia do usuário do perfil](../ui/user-guide.md).

## Atributos computados {#computed-attributes}

Os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização.

Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil. Esses cálculos ajudam a responder facilmente a perguntas relacionadas a coisas como valor de compra vitalício, tempo entre compras ou número de aberturas de aplicativo, sem exigir que você realize cálculos complexos manualmente sempre que as informações forem necessárias. Esses valores de atributos calculados podem ser exibidos em um perfil, usados para criar um público ou acessados por meio de vários padrões de acesso diferentes.

Você pode criar, exibir, editar e excluir atributos computados usando o ponto de extremidade `ca/attributes/`. Para saber como usar atributos computados, consulte a [visão geral sobre atributos computados](../computed-attributes/overview.md). Para operações de API, visite o [manual de ponto de extremidade de API de atributos computados](../computed-attributes/api.md).

## Entidades (acesso [!DNL Profile]) {#entities}

>[!NOTE]
>
>Você só poderá usar esses endpoints se tiver o Real-Time CDP Ultimate.

Por meio do Adobe Experience Platform, você pode acessar dados do [!DNL Real-Time Customer Profile] usando APIs RESTful ou a interface do usuário. Para saber como acessar entidades, mais comumente conhecidas como &quot;perfis&quot;, usando a API, siga as etapas descritas no [manual de endpoint de entidades](entities.md). Para acessar perfis usando a interface do usuário [!DNL Experience Platform], consulte o [Guia do usuário do perfil](../ui/user-guide.md).

## Exportar trabalhos ([!DNL Profile] exportação) {#profile-export}

Os dados do [!DNL Real-Time Customer Profile] podem ser exportados para um conjunto de dados para processamento adicional, como a exportação de públicos para ativação ou atributos de perfil para relatórios. Os trabalhos de exportação para públicos-alvo fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Leia o [manual de ponto de extremidade de trabalhos de exportação de segmentação](../../profile/api/export-jobs.md) para saber mais. Para obter instruções passo a passo sobre como criar e gerenciar trabalhos de exportação para atributos de perfil, visite o [manual do ponto de extremidade de trabalhos de exportação](export-jobs.md).

## Mesclar políticas {#merge-policies}

Ao reunir dados de várias fontes no [!DNL Experience Platform], as políticas de mesclagem são as regras que o [!DNL Experience Platform] usa para determinar como os dados serão priorizados e quais dados serão combinados para criar perfis de clientes individuais. Usando a API [!DNL Real-Time Customer Profile], você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para trabalhar com políticas de mesclagem usando a API, visite o [manual de ponto de extremidade de políticas de mesclagem](merge-policies.md).

Para saber mais sobre as políticas de mesclagem e sua função na Experience Platform, comece lendo a [visão geral das políticas de mesclagem](../merge-policies/overview.md).

## Visualizar status da amostra ([!DNL Profile] visualização) {#profile-preview}

À medida que os dados são assimilados na Experience Platform, um trabalho de amostra é executado para atualizar a contagem de perfis e outras métricas relacionadas aos dados do Perfil do cliente em tempo real. Os resultados deste trabalho de amostra podem ser exibidos usando o ponto de extremidade `/previewsamplestatus`, parte da API de Perfil do Cliente em Tempo Real. Esse endpoint também pode ser usado para listar distribuições de perfil por conjunto de dados e namespace de identidade, bem como para gerar vários relatórios para obter visibilidade sobre a composição do armazenamento de perfis de sua organização.  Para começar a usar o ponto de extremidade `/profilepreviewstatus`, consulte o [manual do ponto de extremidade do status da amostra de visualização](preview-sample-status.md).

## Trabalhos do sistema de perfil {#profile-system-jobs}

Os dados habilitados para perfil assimilados em [!DNL Experience Platform] são armazenados em [!DNL Data Lake] e no repositório de dados [!DNL Real-Time Customer Profile]. Ocasionalmente, pode ser necessário excluir dados de perfil associados a um conjunto de dados do armazenamento de Perfil para remover dados que não são mais necessários ou foram adicionados por engano. Isso requer o uso da API para criar um [!DNL Profile System Job], também conhecido como &quot;[!DNL delete request]&quot;, que pode ser modificado, monitorado ou excluído, se necessário. Para saber como trabalhar com solicitações de exclusão usando o ponto de extremidade `/system/jobs` na API [!DNL Real-Time Customer Profile], siga as etapas descritas no [guia de ponto de extremidade de trabalhos do sistema de perfil](profile-system-jobs.md).

## Atualizar atributos de perfis {#update-profile}

Ocasionalmente, pode ser necessário atualizar os dados no armazenamento de perfil de sua organização. Por exemplo, talvez seja necessário corrigir registros ou alterar um valor de atributo. Isso pode ser feito por meio da assimilação em lote e requer um conjunto de dados habilitado para perfil configurado com uma tag upsert. Para obter mais informações sobre como configurar um conjunto de dados para atualizações de atributo, consulte o tutorial para [habilitar um conjunto de dados para Perfil e substituição](../../catalog/datasets/enable-upsert.md).

## Próximas etapas {#next-steps}

Para começar a fazer chamadas usando a API [!DNL Real-Time Customer Profile], leia o [guia de introdução](getting-started.md) e selecione um dos manuais de endpoint para saber como usar endpoints específicos relacionados ao [!DNL Profile]. Para trabalhar com os dados do [!DNL Profile] usando a interface do usuário do [!DNL Experience Platform], consulte o [Guia do usuário do Perfil do cliente em tempo real](../ui/user-guide.md).
