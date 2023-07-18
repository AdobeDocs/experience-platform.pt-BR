---
keywords: Experience Platform;perfil;perfil do cliente em tempo real;políticas de mesclagem;interface do usuário;carimbo de data/hora ordenado;precedência do conjunto de dados
title: Visão geral das políticas de mesclagem
type: Documentation
description: O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para obter uma visualização completa de seus clientes individuais. Ao reunir esses dados, as políticas de mesclagem são as regras que a Platform usa para determinar como os dados serão priorizados e quais dados serão combinados para criar a visualização unificada.
exl-id: a8ef527a-cfee-4129-9973-e8a212a3ad1e
source-git-commit: 8ae18565937adca3596d8663f9c9e6d84b0ce95a
workflow-type: tm+mt
source-wordcount: '1265'
ht-degree: 0%

---

# Visão geral das políticas de mesclagem

O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para obter uma visualização completa de cada cliente individual. Ao reunir esses dados, as políticas de mesclagem são as regras que [!DNL Platform] O usa o para determinar como os dados serão priorizados e quais dados serão combinados para criar uma visualização unificada.

Usando APIs RESTful ou a interface do usuário, você pode criar novas políticas de mesclagem, gerenciar políticas existentes e definir uma política de mesclagem padrão para sua organização. Este documento fornece uma visão geral das políticas de mesclagem e a função que elas desempenham no Experience Platform.

## Introdução

Este guia requer uma compreensão funcional de vários [!DNL Experience Platform] recursos. Antes de seguir este guia e trabalhar com políticas de mesclagem, revise a documentação dos seguintes serviços:

* [Perfil do cliente em tempo real](../home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.
* [Serviço de identidade da Adobe Experience Platform](../../identity-service/home.md): habilita o Perfil do cliente em tempo real unindo identidades de diferentes fontes de dados que estão sendo assimiladas na [!DNL Platform].
* [Experience Data Model (XDM)](../../xdm/home.md): o quadro normalizado pelo qual [!DNL Platform] organiza os dados de experiência do cliente.

## Noções básicas sobre políticas de mesclagem

O Adobe Experience Platform permite reunir fragmentos de dados de várias fontes e combiná-los para obter uma visualização completa e unificada de cada cliente individual. Ao reunir esses dados, as políticas de mesclagem são as regras que a Platform usa para determinar como os dados serão priorizados e quais dados serão combinados para criar essa visualização unificada.

Por exemplo, se um cliente interagir com sua marca em vários canais, sua organização terá vários fragmentos de perfil relacionados a esse único cliente que aparecem em vários conjuntos de dados. Quando esses fragmentos são assimilados na Platform, eles são mesclados para criar um único perfil para esse cliente.

Quando os dados de várias origens entram em conflito (por exemplo, um fragmento lista o cliente como &quot;único&quot; enquanto o outro lista o cliente como &quot;casado&quot;), a política de mesclagem determina quais informações incluir no perfil do indivíduo.

As políticas de mesclagem são privadas para sua organização, permitindo criar políticas diferentes para mesclar esquemas das maneiras específicas necessárias. Você também pode especificar uma política de mesclagem padrão que será usada se uma política não for fornecida explicitamente. Consulte a seção sobre [políticas de mesclagem padrão](#default-merge-policy) mais adiante neste documento para saber mais. Observe que há um máximo de cinco políticas de mesclagem permitidas por organização.

## Métodos de mesclagem {#merge-methods}

Cada fragmento de perfil contém informações de apenas uma identidade do número total de identidades que podem existir para um indivíduo. Ao mesclar esses dados para formar um perfil de cliente, há o potencial para que essas informações entrem em conflito e a prioridade deve ser especificada.

A seleção de um método de mesclagem permite especificar quais atributos de conjunto de dados priorizar se ocorrer um conflito de mesclagem entre conjuntos de dados.

Há dois métodos de mesclagem possíveis disponíveis para políticas de mesclagem. Cada um desses métodos é resumido abaixo com detalhes adicionais fornecidos nas seções a seguir:

* **[!UICONTROL Prioridade de conjunto de dados]:** No caso de um conflito, dê prioridade aos fragmentos de perfil com base no conjunto de dados de onde eles vieram. Ao selecionar essa opção, você deve escolher os conjuntos de dados relacionados e sua ordem de prioridade. Saiba mais sobre o [precedência do conjunto de dados](#dataset-precedence) método de mesclagem.
* **[!UICONTROL Carimbo de data e hora ordenado]:** Em caso de conflito, é dada prioridade ao fragmento de perfil que foi atualizado mais recentemente. Saiba mais sobre o [carimbo de data e hora ordenado](#timestamp-ordered) método de mesclagem.

### Prioridade de conjunto de dados {#dataset-precedence}

Quando **[!UICONTROL Prioridade de conjunto de dados]** for selecionada como o método de mesclagem para uma política de mesclagem, você poderá dar prioridade aos fragmentos de perfil com base no conjunto de dados de onde eles vieram. Um exemplo de caso de uso seria se sua organização tivesse informações presentes em um conjunto de dados preferencial ou confiável em relação aos dados em outro conjunto de dados.

Para criar uma política de mesclagem usando **[!UICONTROL Prioridade de conjunto de dados]**, você deve selecionar os conjuntos de dados Profile e ExperienceEvent incluídos e, em seguida, pode solicitar manualmente os conjuntos de dados do Perfil por prioridade. Depois que os conjuntos de dados forem selecionados e ordenados, o conjunto de dados principal terá a prioridade mais alta, o segundo será o segundo o mais alto e assim por diante.

### Carimbo de data e hora ordenado {#timestamp-ordered}

À medida que os registros de perfil são assimilados no Experience Platform, um carimbo de data e hora do sistema é obtido no momento da assimilação e adicionado ao registro. Quando **[!UICONTROL Carimbo de data e hora ordenado]** for selecionada como o método de mesclagem para uma política de mesclagem, os perfis serão mesclados com base no carimbo de data e hora do sistema. Em outras palavras, a mesclagem é feita com base no carimbo de data e hora de quando o registro foi assimilado na Platform.

## Identificação de identidade {#id-stitching}

Identificação de identidade ([!UICONTROL Identificação de ID]) é o processo de identificar fragmentos de dados e combiná-los para formar um registro de perfil completo. Para ajudar a ilustrar os diferentes comportamentos de compilação, considere um único cliente que interage com uma marca usando dois endereços de email diferentes.

* **[!UICONTROL Nenhum]:** Quando essa opção é selecionada, as IDs não são compiladas. Quando a segmentação ocorre, as identidades que podem pertencer à mesma pessoa não serão unidas e a segmentação só considerará os atributos anexados a cada ID individual ao determinar se um cliente se qualifica para associação de público-alvo. Isso pode resultar em um único cliente ter vários perfis, e cada perfil pode se qualificar para públicos diferentes, resultando no envio de várias mensagens de marketing para o mesmo cliente.
* **[!UICONTROL Gráfico privado]:** Quando o gráfico privado é selecionado, várias identidades relacionadas ao mesmo indivíduo são unidas. Isso faz com que o cliente tenha um único perfil e permite que a segmentação considere vários atributos de várias identidades relacionadas ao determinar a qualificação do segmento. Nesse cenário, o cliente provavelmente terá um único perfil, se qualificará para um público-alvo com base na combinação de atributos entre as identidades e receberá apenas uma mensagem de marketing.

Para saber mais sobre identidades e seu papel na geração de perfis e públicos, comece lendo o [Visão geral do serviço de identidade](../../identity-service/home.md).

## Política de mesclagem padrão {#default-merge-policy}

Uma organização pode criar uma política de mesclagem padrão para que sua organização use ao mesclar fragmentos de perfil. Isso permite que os usuários selecionem facilmente a política padrão ao executar ações no Experience Platform, como visualizar perfis de clientes ou criar públicos. Na maioria dos casos, a menos que outra política de mesclagem seja especificada, a política de mesclagem padrão será usada.

Cada organização pode criar várias políticas de mesclagem relacionadas a uma única classe de esquema XDM. No entanto, elas só podem ter uma política de mesclagem padrão declarada para cada classe. Por exemplo, sua organização pode ter uma política de mesclagem padrão relacionada ao [!DNL XDM Individual Profile] e uma política de mesclagem padrão diferente para uma classe de Inventário de produto personalizada.

Se você criar uma nova política de mesclagem e defini-la como padrão, a política de mesclagem padrão anterior será atualizada automaticamente pelo sistema para não ser mais o padrão.

>[!WARNING]
>
>As contagens de perfis e os públicos-alvo com uma política de mesclagem padrão associada existente podem ser afetados. Qualquer público-alvo que tenha uma política de mesclagem padrão aplicada será atualizado para a nova política de mesclagem padrão.

## Próximas etapas

Depois de ler este guia, você sabe o que são políticas de mesclagem e o papel que desempenham no Experience Platform. Para começar a trabalhar com políticas de mesclagem na interface do Experience Platform, consulte o [guia da interface do usuário de políticas de mesclagem](ui-guide.md). Para trabalhar com políticas de mesclagem usando a API, visite o [manual de endpoint da API de políticas de mesclagem](../api/merge-policies.md).
