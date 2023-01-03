---
keywords: Experience Platform, perfil, perfil do cliente em tempo real, políticas de mesclagem, interface do usuário, interface do usuário, carimbo de data e hora solicitado, precedência do conjunto de dados
title: Visão geral das políticas de mesclagem
type: Documentation
description: O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para ver uma exibição completa de seus clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que a Platform usa para determinar como os dados serão priorizados e quais dados serão combinados para criar a exibição unificada.
exl-id: a8ef527a-cfee-4129-9973-e8a212a3ad1e
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Visão geral das políticas de mesclagem

O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para ver uma visualização completa de cada um dos clientes individuais. Ao unir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] O usa o para determinar como os dados serão priorizados e quais dados serão combinados para criar uma visualização unificada.

Usando RESTful APIs ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Este documento fornece uma visão geral das políticas de mesclagem e o papel que elas desempenham no Experience Platform.

## Introdução

Este guia requer uma compreensão funcional de vários [!DNL Experience Platform] recursos. Antes de seguir este guia e trabalhar com políticas de mesclagem, revise a documentação dos seguintes serviços:

* [Perfil do cliente em tempo real](../home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.
* [Serviço de identidade da Adobe Experience Platform](../../identity-service/home.md): Habilita o Perfil do cliente em tempo real ao unir identidades de fontes de dados diferentes que estão sendo assimiladas no [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): O quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

## Noções básicas sobre políticas de mesclagem

O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para ver uma visualização completa e unificada de cada um dos clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que a Platform usa para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada.

Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparece em vários conjuntos de dados. Quando esses fragmentos são assimilados na Platform, eles são mesclados para criar um único perfil para esse cliente.

Quando os dados de várias fontes estão em conflito (por exemplo, um fragmento lista o cliente como &quot;único&quot; enquanto o outro lista o cliente como &quot;casado&quot;), a política de mesclagem determina quais informações devem ser incluídas no perfil do indivíduo.

As políticas de mesclagem são privadas para a organização, permitindo que você crie políticas diferentes para mesclar schemas de acordo com as maneiras específicas de que precisa. Você também pode especificar uma política de mesclagem padrão que será usada se não for fornecida explicitamente. Consulte a seção sobre [políticas de mesclagem padrão](#default-merge-policy) mais tarde neste documento para saber mais. Observe que há no máximo cinco políticas de mesclagem permitidas por organização.

## Métodos de mesclagem {#merge-methods}

Cada fragmento de perfil contém informações para apenas uma identidade do número total de identidades que podem existir para um indivíduo. Ao mesclar esses dados para formar um perfil de cliente, há a possibilidade de essas informações entrarem em conflito e a prioridade deve ser especificada.

Selecionar um método de mesclagem permite especificar quais atributos de conjunto de dados priorizar se ocorrer um conflito de mesclagem entre conjuntos de dados.

Há dois métodos de mesclagem possíveis disponíveis para políticas de mesclagem. Cada um desses métodos é resumido abaixo com detalhes adicionais fornecidos nas seções a seguir:

* **[!UICONTROL Precedência do conjunto de dados]:** Em caso de conflito, dê prioridade aos fragmentos de perfil com base no conjunto de dados de onde eles vieram. Ao selecionar essa opção, você deve escolher os conjuntos de dados relacionados e sua ordem de prioridade. Saiba mais sobre o [precedência do conjunto de dados](#dataset-precedence) método merge .
* **[!UICONTROL Carimbo de data e hora ordenado]:** Em caso de conflito, é dada prioridade ao fragmento de perfil que foi atualizado mais recentemente. Saiba mais sobre o [timestamp pedido](#timestamp-ordered) método merge .

### Precedência do conjunto de dados {#dataset-precedence}

When **[!UICONTROL Precedência do conjunto de dados]** for selecionado como o método de mesclagem para uma política de mesclagem, você poderá dar prioridade aos fragmentos de perfil com base no conjunto de dados de onde eles vieram. Um exemplo de uso seria se sua organização tivesse informações presentes em um conjunto de dados preferido ou confiável sobre os dados em outro conjunto de dados.

Para criar uma política de mesclagem usando **[!UICONTROL Precedência do conjunto de dados]**, você deve selecionar os conjuntos de dados do Perfil e do ExperienceEvent incluídos e, em seguida, pode ordenar manualmente os conjuntos de dados do Perfil para precedência. Depois que os conjuntos de dados forem selecionados e ordenados, o conjunto de dados principal terá a prioridade mais alta, o segundo conjunto de dados será o segundo mais alto e assim por diante.

### Carimbo de data e hora ordenado {#timestamp-ordered}

À medida que os registros de perfil são assimilados no Experience Platform, um carimbo de data e hora do sistema é obtido no momento da assimilação e adicionado ao registro. When **[!UICONTROL Carimbo de data e hora ordenado]** for selecionado como o método de mesclagem para uma política de mesclagem, os perfis serão mesclados com base no carimbo de data e hora do sistema. Em outras palavras, a mesclagem é feita com base no carimbo de data e hora de quando o registro foi assimilado na Platform.

## Compilação de identidade {#id-stitching}

Compilação de identidade ([!UICONTROL Compilação de ID]) é o processo de identificação de fragmentos de dados e sua combinação para formar um registro de perfil completo. Para ajudar a ilustrar os diferentes comportamentos de costura, considere um único cliente que interage com uma marca usando dois endereços de email diferentes.

* **[!UICONTROL Nenhum]:** Quando essa opção é selecionada, as IDs não serão compiladas. Quando a segmentação ocorrer, as identidades que podem pertencer à mesma pessoa não serão unidas e a segmentação considerará apenas os atributos anexados a cada ID individual ao determinar se um cliente se qualifica para associação de segmento. Isso pode resultar em um único cliente com vários perfis e cada perfil pode se qualificar para segmentos diferentes, resultando no envio de várias mensagens de marketing para o mesmo cliente.
* **[!UICONTROL Gráfico privado]:** Quando o gráfico privado é selecionado, várias identidades relacionadas ao mesmo indivíduo são unidas. Isso resulta no cliente ter um único perfil e permite que a segmentação considere vários atributos de várias identidades relacionadas ao determinar a qualificação de segmento. Nesse cenário, o cliente provavelmente terá um único perfil, se qualificará para um segmento com base na combinação de atributos entre identidades e receberá apenas uma mensagem de marketing.

Para saber mais sobre identidades e sua função na geração de perfis e segmentos, comece lendo a variável [Visão geral do Serviço de identidade](../../identity-service/home.md).

## Política de mesclagem padrão {#default-merge-policy}

Uma organização pode criar uma política de mesclagem padrão para a organização usar ao mesclar fragmentos de perfil. Isso permite que os usuários selecionem facilmente a política padrão ao executar ações no Experience Platform, como visualizar perfis de clientes ou criar segmentos. Na maioria dos casos, a menos que outra política de mesclagem seja especificada, a política de mesclagem padrão será usada.

Cada organização pode criar várias políticas de mesclagem relacionadas a uma única classe de esquema XDM, no entanto, só pode ter uma política de mesclagem padrão declarada para cada classe. Por exemplo, sua organização pode ter uma política de mesclagem padrão relacionada ao [!DNL XDM Individual Profile] classe e uma política de mesclagem padrão diferente para uma classe de Inventário de Produto criada personalmente.

Se você criar uma nova política de mesclagem e configurá-la como padrão, a política de mesclagem padrão anterior será atualizada automaticamente pelo sistema para não ser mais o padrão.

>[!WARNING]
>
>As contagens de perfil e os segmentos com uma política de mesclagem padrão existente associada podem ser afetados. Qualquer segmento que tenha uma política de mesclagem padrão aplicada será atualizado para a nova política de mesclagem padrão.

## Próximas etapas

Depois de ler este guia, você sabe agora o que são as políticas de mesclagem e o papel que elas desempenham no Experience Platform. Para começar a trabalhar com políticas de mesclagem na interface do usuário do Experience Platform, consulte o [guia da interface do usuário de políticas de mesclagem](ui-guide.md). Para trabalhar com políticas de mesclagem usando a API, visite o [guia do endpoint da API de políticas de mesclagem](../api/merge-policies.md).
