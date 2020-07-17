---
keywords: Experience Platform;profile;real-time customer profile;troubleshooting;API
solution: Adobe Experience Platform
title: Guia do desenvolvedor da API do Perfil do cliente em tempo real
topic: guide
translation-type: tm+mt
source-git-commit: f910351d49de9c4a18a444b99b7f102f4ce3ed5b
workflow-type: tm+mt
source-wordcount: '624'
ht-degree: 0%

---


# [!DNL Real-time Customer Profile] Guia do desenvolvedor da API

[!DNL Real-time Customer Profile] permite que você veja uma visualização holística de cada um de seus clientes individuais no Adobe Experience Platform. [!DNL Profile] permite consolidar dados de clientes diferentes de vários canais, como dados online, offline, CRM e de terceiros, em uma visualização unificada que oferece uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

A [!DNL Real-time Customer Profile] API inclui vários pontos de extremidade, descritos abaixo. Visite os guias de ponto de extremidade individuais para obter detalhes e consulte o guia [de](getting-started.md) introdução para obter informações importantes sobre cabeçalhos necessários, como ler chamadas de API de amostra e muito mais.

Para visualização de todos os pontos de extremidade e operações CRUD disponíveis, consulte o swagger [de referência da API do Perfil do cliente em tempo](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/real-time-customer-profile.yaml)real.

## (Alfa) Atributos calculados

>[!IMPORTANT]
>
>
>A funcionalidade de atributo calculado está em alfa e não está disponível para todos os usuários. A documentação e funcionalidade estão sujeitas a alterações.

Os atributos calculados permitem calcular automaticamente o valor dos campos com base em outros valores, cálculos e expressões. Os atributos calculados operam no nível do perfil, o que significa que você pode agregação valores em todos os registros e eventos. Cada atributo calculado contém uma expressão, ou &quot;regra&quot;, que avalia os dados recebidos e armazena o valor resultante em um atributo de perfil ou em um evento. Esses cálculos ajudam você a responder facilmente perguntas relacionadas a coisas como valor de compra vitalícia, tempo entre compras ou número de aberturas de aplicativos, sem exigir a execução manual de cálculos complexos sempre que as informações forem necessárias. Você pode criar, visualização, editar e excluir atributos calculados usando o `config/computedAttributes` terminal. Para saber como usar esse terminal, visite o guia [de ponto de extremidade de atributos](computed-attributes.md)computados.

## Projeções de borda

O Adobe Experience Platform permite a personalização em tempo real das experiências do cliente, tornando os dados facilmente acessíveis em servidores estrategicamente localizados chamados &quot;bordas&quot;. A [!DNL Real-time Customer Profile] API fornece pontos de extremidade para trabalhar com bordas por meio de componentes chamados &quot;projeções&quot;. Isso inclui configurações de projeção para determinar quais dados devem ser projetados para cada borda, bem como destinos de projeção para definir onde rotear uma projeção. Para obter informações detalhadas sobre como trabalhar com projeções de borda, visite o guia [de configurações de](edge-projections.md)projeção e pontos de extremidade de destino.

## Entidades (acesso ao Perfil) {#entities}

Por meio do Adobe Experience Platform, você pode acessar [!DNL Real-time Customer Profile] dados usando RESTful APIs ou a interface do usuário. Para saber como acessar entidades, mais comumente conhecidas como &quot;perfis&quot;, usando a API, siga as etapas descritas no guia [de endpoint das](entities.md)entidades. Para acessar perfis usando a interface do usuário, consulte o guia [!DNL Platform] do usuário do [](../ui/user-guide.md)Perfil.

## Mesclar políticas

Ao reunir dados de várias fontes, as políticas de mesclagem são as regras que [!DNL Experience Platform][!DNL Platform] usam para determinar como os dados serão priorizados e quais dados serão combinados para criar perfis individuais do cliente. Usando a [!DNL Real-time Customer Profile] API, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Para saber mais sobre como trabalhar com políticas de mesclagem usando a API, visite o guia [de ponto de extremidade de políticas de](merge-policies.md)mesclagem.

Para obter um guia para trabalhar com políticas de mesclagem usando a [!DNL Platform] interface do usuário, consulte o guia [do usuário](../ui/merge-policies.md)Mesclar políticas.

## trabalhos do sistema Perfil

Os dados ingeridos [!DNL Platform] são armazenados no armazenamento [!DNL Data Lake] e no [!DNL Real-time Customer Profile] armazenamento de dados. Ocasionalmente, pode ser necessário excluir um conjunto de dados ou lote do [!DNL Profile] armazenamento para remover dados que não são mais necessários ou que foram adicionados por erro. Isso requer o uso da API para criar um [!DNL Profile System Job], conhecido como &quot;[!DNL delete request]&quot;, que também pode ser, modificado, monitorado ou excluído, se necessário. Para saber como trabalhar com solicitações de exclusão usando o `/system/jobs` ponto de extremidade na [!DNL Real-time Customer Profile] API, siga as etapas descritas no guia [de ponto de extremidade de tarefas do sistema de](profile-system-jobs.md)perfis.

## Próximas etapas

Para começar a fazer chamadas usando a [!DNL Real-time Customer Profile] API, leia o guia [de](getting-started.md) introdução e selecione um dos guias de endpoint para saber como usar endpoints específicos [!DNL Profile]relacionados. Para saber mais sobre como trabalhar com [!DNL Profile] dados usando a [!DNL Platform] interface do usuário, consulte o guia [do usuário do Perfil do cliente em tempo](../ui/user-guide.md)real.