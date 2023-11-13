---
keywords: Experience Platform;perfil;perfil de cliente em tempo real;solução de problemas;API;perfil unificado;Perfil unificado;perfil;habilitar perfil;perfil;Habilitar perfil;perfil;perfil;profile;Unified Profile;unified;Profile;rtcp;enable profile
title: Guia da API do Perfil do cliente em tempo real
description: A API de perfil do cliente em tempo real permite que os desenvolvedores explorem e trabalhem com dados de perfil, incluindo a visualização de perfis, a criação e a atualização de políticas de mesclagem, a exportação ou a amostragem de dados de perfil e a exclusão de dados de perfil que não são mais necessários ou que foram adicionados por engano. Siga este manual para saber como executar operações importantes usando a API.
exl-id: ce39b95b-cff7-46cf-a14c-8203017c8826
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '961'
ht-degree: 1%

---

# [!DNL Real-Time Customer Profile] Manual da API

[!DNL Real-Time Customer Profile] O permite que você veja uma visualização integral de cada cliente individual na Adobe Experience Platform. [!DNL Profile] O permite consolidar dados diferentes do cliente de vários canais, como dados online, offline, CRM e de terceiros, em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

A variável [!DNL Real-Time Customer Profile] A API inclui vários endpoints, descritos abaixo. Acesse os manuais de endpoint individuais para obter detalhes e consulte a [guia de introdução](getting-started.md) para obter informações importantes sobre cabeçalhos necessários, ler chamadas de API de exemplo e muito mais.

Para exibir todos os endpoints e operações CRUD disponíveis, visite o [Swagger de referência da API de perfil do cliente em tempo real](https://www.adobe.com/go/profile-apis-en).

Para obter um guia para trabalhar com [!DNL Real-Time Customer Profile] dados no [!DNL Experience Platform] Interface do usuário do, consulte a [Guia do usuário do perfil](../ui/user-guide.md).

## [!BADGE Beta]{type=Informative} atributos computados {#computed-attributes}

>[!IMPORTANT]
>
A funcionalidade de atributo computado está na versão beta e não está disponível para todos os usuários. A documentação e a funcionalidade estão sujeitas a alterações.

Os atributos computados são funções usadas para agregar dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas na segmentação, ativação e personalização.

Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil. Esses cálculos ajudam a responder facilmente a perguntas relacionadas a coisas como valor de compra vitalício, tempo entre compras ou número de aberturas de aplicativo, sem exigir que você realize cálculos complexos manualmente sempre que as informações forem necessárias. Esses valores de atributos calculados podem ser exibidos em um perfil, usados para criar um público ou acessados por meio de vários padrões de acesso diferentes.

Você pode criar, exibir, editar e excluir atributos calculados usando a `ca/attributes/` terminal. Para saber como usar atributos calculados, consulte a [visão geral dos atributos computados](../computed-attributes/overview.md). Para operações de API, visite o [manual de endpoint da API de atributos computados](../computed-attributes/api.md).

## Projeções de borda {#edge-projections}

O Adobe Experience Platform permite a personalização em tempo real das experiências do cliente, tornando os dados facilmente acessíveis em servidores localizados estrategicamente, chamados de &quot;bordas&quot;. A variável [!DNL Real-Time Customer Profile] A API fornece endpoints para trabalhar com bordas por meio de componentes chamados &quot;projeções&quot;. Isso inclui configurações de projeção para determinar quais dados devem ser projetados para cada borda, bem como destinos de projeção para definir onde rotear uma projeção. Para obter informações detalhadas sobre como trabalhar com projeções de borda, visite o [guia de endpoints de configurações e destinos de projeção](edge-projections.md).

## Entidades ([!DNL Profile] access) {#entities}

Por meio do Adobe Experience Platform, você pode acessar [!DNL Real-Time Customer Profile] usando APIs RESTful ou a interface do usuário do. Para saber como acessar entidades, mais comumente conhecidas como &quot;perfis&quot;, usando a API, siga as etapas descritas na seção [manual de endpoint de entidades](entities.md). Para acessar perfis usando o [!DNL Platform] consulte a [Guia do usuário do perfil](../ui/user-guide.md).

## Exportar trabalhos ([!DNL Profile] export) {#profile-export}

[!DNL Real-Time Customer Profile] os dados podem ser exportados para um conjunto de dados para processamento adicional, como exportar públicos para ativação ou atributos de perfil para relatórios. Os trabalhos de exportação para públicos-alvo fazem parte da [!DNL Adobe Experience Platform Segmentation Service] API, leia as [guia de ponto de extremidade de trabalhos de exportação de segmentação](../../profile/api/export-jobs.md) para saber mais. Para obter instruções passo a passo sobre como criar e gerenciar trabalhos de exportação para atributos de perfil, visite o [guia de endpoint de trabalhos de exportação](export-jobs.md).

## Políticas de mesclagem {#merge-policies}

Ao reunir dados de várias fontes no [!DNL Experience Platform], as políticas de mesclagem são as regras que [!DNL Platform] O usa o para determinar como os dados serão priorizados e quais dados serão combinados para criar perfis de clientes individuais. Usar o [!DNL Real-Time Customer Profile] , você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para trabalhar com políticas de mesclagem usando a API, visite o [manual de ponto de extremidade das políticas de mesclagem](merge-policies.md).

Para saber mais sobre as políticas de mesclagem e sua função na Platform, comece lendo o [visão geral das políticas de mesclagem](../merge-policies/overview.md).

## Visualizar status da amostra ([!DNL Profile] preview) {#profile-preview}

À medida que os dados são assimilados na Platform, um trabalho de amostra é executado para atualizar a contagem de perfis e outras métricas relacionadas aos dados do Perfil do cliente em tempo real. Os resultados deste trabalho de amostra podem ser exibidos usando o `/previewsamplestatus` endpoint, parte da API de Perfil do cliente em tempo real. Esse endpoint também pode ser usado para listar distribuições de perfil por conjunto de dados e namespace de identidade, bem como para gerar vários relatórios para obter visibilidade sobre a composição da Loja de perfis da sua organização.  Para começar a usar o `/profilepreviewstatus` endpoint, consulte a [visualizar guia de endpoint de status de amostra](preview-sample-status.md).

## Trabalhos do sistema de perfil {#profile-system-jobs}

Dados habilitados para perfil que são assimilados em [!DNL Platform] é armazenado no [!DNL Data Lake] bem como a [!DNL Real-Time Customer Profile] armazenamento de dados. Ocasionalmente, pode ser necessário excluir um conjunto de dados ou lote do [!DNL Profile] armazene para remover dados que não são mais necessários ou que foram adicionados por engano. Isso requer o uso da API para criar uma [!DNL Profile System Job], também conhecido como &quot;[!DNL delete request]&quot;, que pode ser modificado, monitorado ou excluído, se necessário. Para saber como trabalhar com solicitações de exclusão usando o `/system/jobs` endpoint na variável [!DNL Real-Time Customer Profile] , siga as etapas descritas na seção [guia de ponto de extremidade de trabalhos do sistema de perfis](profile-system-jobs.md).

## Atualizar atributos de perfis {#update-profile}

Ocasionalmente, pode ser necessário atualizar os dados na Loja de perfis da sua organização. Por exemplo, talvez seja necessário corrigir registros ou alterar um valor de atributo. Isso pode ser feito por meio da assimilação em lote e requer um conjunto de dados habilitado para perfil configurado com uma tag upsert. Para obter mais informações sobre como configurar um conjunto de dados para atualizações de atributo, consulte o tutorial para [ativar um conjunto de dados para Perfil e substituição](../../catalog/datasets/enable-upsert.md).

## Próximas etapas {#next-steps}

Para começar a fazer chamadas usando o [!DNL Real-Time Customer Profile] API, leia as [guia de introdução](getting-started.md) em seguida, selecione um dos manuais de endpoint para saber como usar [!DNL Profile]endpoints relacionados ao. Para trabalhar com [!DNL Profile] dados usando o [!DNL Experience Platform] Interface do usuário do, consulte a [Guia do usuário do Perfil do cliente em tempo real](../ui/user-guide.md).
