---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;solução de problemas;API;perfil unificado;Perfil unificado; unificado;Perfil;rtcp;ativar perfil;Ativar perfil
title: Guia da API do Perfil do cliente em tempo real
topic: guide
description: A API Perfil do cliente em tempo real permite que os desenvolvedores explorem e trabalhem com dados do Perfil, incluindo perfis de visualização, criem e atualizem políticas de mesclagem, exportem ou façam amostras de dados do Perfil e excluam dados do Perfil que não são mais necessários ou foram adicionados por engano. Siga este guia para saber como executar operações principais usando a API.
translation-type: tm+mt
source-git-commit: 24a5af0440f58b4e1db639ec971c4e1611f107d8
workflow-type: tm+mt
source-wordcount: '895'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Guia de API

[!DNL Real-time Customer Profile] permite que você veja uma visualização holística de cada um de seus clientes individuais dentro da Adobe Experience Platform. [!DNL Profile] permite consolidar dados de clientes diferentes de vários canais, como dados online, offline, CRM e de terceiros, em uma visualização unificada que oferece uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

A API [!DNL Real-time Customer Profile] inclui vários pontos de extremidade, descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte o [guia de introdução](getting-started.md) para obter informações importantes sobre cabeçalhos necessários, como ler amostras de chamadas de API e muito mais.

Para visualização de todos os pontos de extremidade e operações CRUD disponíveis, visite o [swagger de referência da API do Perfil do cliente em tempo real](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml).

Para obter um guia para trabalhar com [!DNL Real-time Customer Profile] dados na interface do usuário [!DNL Experience Platform], consulte [Guia do usuário do Perfil](../ui/user-guide.md).

## (Alfa) Atributos calculados {#computed-attributes}

>[!IMPORTANT]
>
>A funcionalidade de atributo calculado está em alfa e não está disponível para todos os usuários. A documentação e funcionalidade estão sujeitas a alterações.

Atributos calculados são funções usadas para agregação de dados no nível do evento em atributos no nível do perfil. Essas funções são computadas automaticamente para que possam ser usadas em segmentação, ativação e personalização.

Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil. Esses cálculos ajudam você a responder facilmente perguntas relacionadas a coisas como valor de compra vitalícia, tempo entre compras ou número de aberturas de aplicativos, sem exigir a execução manual de cálculos complexos sempre que as informações forem necessárias. Esses valores de atributos calculados podem ser exibidos em um perfil, usados para criar um segmento ou acessados por meio de vários padrões de acesso diferentes.

Você pode criar, visualização, editar e excluir atributos calculados usando o endpoint `config/computedAttributes`. Para saber como usar atributos calculados, consulte a [visão geral dos atributos calculados](../computed-attributes/overview.md). Para operações de API, visite o [guia de ponto final da API de atributos calculados](../computed-attributes/ca-api.md).

## Projeções de borda {#edge-projections}

A Adobe Experience Platform permite a personalização em tempo real das experiências do cliente, tornando os dados facilmente acessíveis em servidores estrategicamente localizados chamados de &quot;bordas&quot;. A API [!DNL Real-time Customer Profile] fornece pontos de extremidade para trabalhar com bordas por meio de componentes chamados &quot;projeções&quot;. Isso inclui configurações de projeção para determinar quais dados devem ser projetados para cada borda, bem como destinos de projeção para definir onde rotear uma projeção. Para obter informações detalhadas sobre como trabalhar com projeções de borda, visite o guia [configurações de projeção e pontos finais de destino](edge-projections.md).

## Entidades ([!DNL Profile] acesso) {#entities}

Por meio do Adobe Experience Platform, você pode acessar [!DNL Real-time Customer Profile] dados usando RESTful APIs ou a interface do usuário. Para saber como acessar entidades, mais comumente conhecidas como &quot;perfis&quot;, usando a API, siga as etapas descritas no [guia de endpoint das entidades](entities.md). Para acessar perfis usando a interface de usuário [!DNL Platform], consulte o [guia do usuário do Perfil](../ui/user-guide.md).

## Exportar trabalhos ([!DNL Profile] exportar) {#profile-export}

[!DNL Real-time Customer Profile] os dados podem ser exportados para um conjunto de dados para processamento adicional, como a exportação de segmentos de audiência para atributos de ativação ou perfil para relatórios. As tarefas de exportação para segmentos de audiência fazem parte da API [!DNL Adobe Experience Platform Segmentation Service]. Leia o [guia de ponto de extremidade de tarefas de exportação de segmentação](../../profile/api/export-jobs.md) para saber mais. Para obter instruções passo a passo sobre como criar e gerenciar trabalhos de exportação para atributos de perfil, visite o [guia de ponto de extremidade de trabalhos de exportação](export-jobs.md).

## Mesclar políticas {#merge-policies}

Ao reunir dados de várias fontes em [!DNL Experience Platform], as políticas de mesclagem são as regras que [!DNL Platform] usa para determinar como os dados serão priorizados e quais dados serão combinados para criar perfis individuais do cliente. Usando a API [!DNL Real-time Customer Profile], você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para saber mais sobre como trabalhar com políticas de mesclagem usando a API, visite o [guia de ponto de extremidade de políticas de mesclagem](merge-policies.md).

Para obter um guia para trabalhar com políticas de mesclagem usando a interface do usuário [!DNL Platform], consulte o [guia do usuário das políticas de mesclagem](../ui/merge-policies.md).

## Status de amostra da pré-visualização ([!DNL Profile] pré-visualização) {#profile-preview}

Como os dados ativados para o Perfil, são ingeridos no Experience Platform, eles são armazenados no armazenamento de dados do Perfil. À medida que o número de registros no repositório de Perfis aumenta ou diminui, uma tarefa de amostra é executada que inclui informações sobre quantos fragmentos de perfil e perfis mesclados estão no repositório de dados. Usando a API de Perfil, você pode pré-visualização a amostra mais recente bem-sucedida, bem como a distribuição de perfis por conjunto de dados e por namespace de identidade. Para começar a usar o endpoint `/profilepreviewstatus`, consulte o [guia do endpoint de status da amostra de pré-visualização](preview-sample-status.md).

## Trabalhos do sistema do perfil {#profile-system-jobs}

Os dados habilitados para perfis que são ingeridos em [!DNL Platform] são armazenados em [!DNL Data Lake], bem como no armazenamento de dados [!DNL Real-time Customer Profile]. Ocasionalmente, pode ser necessário excluir um conjunto de dados ou lote do armazenamento [!DNL Profile] para remover dados que não são mais necessários ou que foram adicionados por erro. Isso requer o uso da API para criar um [!DNL Profile System Job], também conhecido como &quot;[!DNL delete request]&quot;, que pode ser modificado, monitorado ou excluído, se necessário. Para saber como trabalhar com solicitações de exclusão usando o endpoint `/system/jobs` na API [!DNL Real-time Customer Profile], siga as etapas descritas no guia [endpoint jobs do sistema de perfis](profile-system-jobs.md).

## Próximas etapas {#next-steps}

Para começar a fazer chamadas usando a API [!DNL Real-time Customer Profile], leia o [guia de introdução](getting-started.md) e selecione um dos guias de ponto de extremidade para saber como usar pontos de extremidade específicos [!DNL Profile]. Para trabalhar com [!DNL Profile] dados usando a interface do usuário [!DNL Experience Platform], consulte o [Guia do usuário do Perfil do cliente em tempo real](../ui/user-guide.md).