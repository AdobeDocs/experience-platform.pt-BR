---
keywords: Experience Platform;página inicial;tópicos populares;Imposição de política;Imposição automática;Imposição baseada em API;governança de dados
solution: Experience Platform
title: Aplicação automática de política
description: Este documento aborda como as políticas de uso de dados são aplicadas automaticamente ao ativar públicos para destinos no Experience Platform.
exl-id: c6695285-77df-48c3-9b4c-ccd226bc3f16
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2126'
ht-degree: 0%

---

# Aplicação automática de política

Os rótulos e políticas de uso de dados estão disponíveis para todos os usuários do Adobe Experience Platform. Defina políticas de uso de dados e aplique rótulos de uso de dados para garantir que todos os dados confidenciais, identificáveis ou contratuais sejam tratados com precisão. Essas medidas ajudam a aplicar as regras de governança de dados de sua organização sobre como os dados podem ser acessados, processados, armazenados e compartilhados.

Para ajudar a proteger sua organização contra possíveis riscos e passivos, a Experience Platform impõe automaticamente políticas de uso caso ocorram violações ao ativar públicos para destinos.

>[!IMPORTANT]
>
>As políticas de consentimento e a aplicação automática da política de consentimento só estão disponíveis para organizações que compraram o **Adobe Healthcare Shield** ou o **Adobe Privacy &amp; Security Shield**.

Este documento se concentra na aplicação da governança de dados e das políticas de consentimento. Para obter informações sobre políticas de controle de acesso, consulte a documentação em [controle de acesso baseado em atributos](../../access-control/abac/overview.md).

## Pré-requisitos

Este guia requer uma compreensão funcional dos serviços da Experience Platform envolvidos na aplicação automática. Consulte a documentação a seguir para saber mais antes de continuar com este guia:

* [Governança de dados do Adobe Experience Platform](../home.md): a estrutura pela qual o Experience Platform impõe conformidade com o uso de dados por meio do uso de rótulos e políticas.
* [Perfil de cliente em tempo real](../../profile/home.md): fornece um perfil de cliente unificado em tempo real com base em dados agregados de várias fontes.
* [Serviço de segmentação do Adobe Experience Platform](../../segmentation/home.md): o mecanismo de segmentação do [!DNL Experience Platform] usado para criar públicos-alvo a partir dos perfis do cliente com base nos comportamentos e atributos do cliente.
* [Destinos](../../destinations/home.md): os destinos são integrações pré-criadas com aplicativos comumente usados que permitem a ativação contínua de dados do Experience Platform para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muito mais.

## Fluxo de imposição {#flow}

O diagrama a seguir ilustra como a aplicação de políticas é integrada ao fluxo de dados da ativação de público-alvo:

![Uma ilustração de como a imposição de política está integrada ao fluxo de dados de ativação de público-alvo.](../images/enforcement/enforcement-flow.png)

Quando um público é ativado pela primeira vez, o [!DNL Policy Service] verifica as políticas aplicáveis com base nos seguintes fatores:

* Os rótulos de uso de dados aplicados aos campos e conjuntos de dados no público-alvo a ser ativado.
* A finalidade de marketing do destino.
* Os perfis que consentiram em ser incluídos na ativação de público, com base nas políticas de consentimento configuradas.

>[!NOTE]
>
>Se houver rótulos de uso de dados que tenham sido aplicados apenas a determinados campos, a imposição desses rótulos de nível de campo na ativação só ocorrerá se pelo menos uma das seguintes condições for atendida:
>
>* Os campos são usados no público-alvo.
>* Os campos são configurados como atributos projetados para o destino.

## Linhagem de dados {#lineage}

A linhagem de dados desempenha um papel fundamental na forma como as políticas são aplicadas no Experience Platform. Em termos gerais, a linhagem de dados se refere à origem de um conjunto de dados e ao que acontece com ela (ou onde ela se move) ao longo do tempo.

No contexto da Governança de dados, a linhagem permite que os rótulos de uso de dados se propaguem de esquemas para serviços downstream que consomem seus dados, como Perfil do cliente em tempo real e Destinos. Isso permite que as políticas sejam avaliadas e aplicadas em vários pontos-chave da jornada de dados por meio do Experience Platform e fornece contexto aos consumidores de dados sobre por que ocorreu uma violação de política.

No Experience Platform, a aplicação de políticas está preocupada com a seguinte linhagem:

1. Os dados são assimilados na Experience Platform e armazenados em **conjuntos de dados**.
1. Os perfis de clientes são identificados e construídos a partir desses conjuntos de dados mesclando fragmentos de dados de acordo com a **política de mesclagem**.
1. Grupos de perfis são divididos em **públicos-alvo** com base em atributos comuns.
1. Os públicos-alvo estão ativados para **destinos** downstream.

Cada etapa da linha do tempo acima representa uma entidade que pode contribuir para a aplicação de políticas, conforme descrito na tabela abaixo:

| Estágio de linhagem de dados | Função na aplicação da política |
| --- | --- |
| Conjunto de dados | Os conjuntos de dados contêm rótulos de uso de dados (aplicados no nível de campo do esquema ou no nível de conjunto de dados inteiro) que definem para quais casos de uso o conjunto de dados inteiro ou campos específicos podem ser usados. Violações de política ocorrerão se um conjunto de dados ou campo contendo determinados rótulos for usado para uma finalidade restrita por uma política.<br><br>Todos os atributos de consentimento coletados dos clientes também são armazenados em conjuntos de dados. Se você tiver acesso às políticas de consentimento, todos os perfis que não atenderem aos requisitos de atributo de consentimento de suas políticas serão excluídos dos públicos-alvo ativados para um destino. |
| Política de mesclagem | As políticas de mesclagem são as regras que a Experience Platform usa para determinar como os dados serão priorizados ao mesclar fragmentos de vários conjuntos de dados. Violações de política ocorrerão se suas políticas de mesclagem forem configuradas para que os conjuntos de dados com rótulos restritos sejam ativados para um destino. Consulte a [visão geral das políticas de mesclagem](../../profile/merge-policies/overview.md) para obter mais informações. |
| Público-alvo | As regras de segmentação definem quais atributos devem ser incluídos nos perfis do cliente. Dependendo dos campos incluídos por uma definição de segmento, o público-alvo herdará os rótulos de uso aplicados para esses campos. Violações de política ocorrerão se você tentar ativar um público-alvo cujos rótulos herdados são restritos pelas políticas aplicáveis do destino, com base no caso de uso de marketing. |
| Destino | Ao configurar um destino, uma ação de marketing (às vezes chamada de caso de uso de marketing) pode ser definida. Esse caso de uso correlaciona-se a uma ação de marketing conforme definido em uma política. Em outras palavras, a ação de marketing que você define para um destino determina quais políticas de uso de dados e de consentimento são aplicáveis a esse destino.<br><br>As violações da política de uso de dados ocorrem se você tentar ativar um público cujos rótulos de uso são restritos para a ação de marketing do destino.<br><br>(Beta) Quando um público é ativado, todos os perfis que não contêm os atributos de consentimento necessários para a ação de marketing (conforme definido pelas suas políticas de consentimento) são excluídos do público ativado. |

>[!IMPORTANT]
>
>Algumas políticas de uso de dados podem especificar dois ou mais rótulos com uma relação AND. Por exemplo, uma política pode restringir uma ação de marketing se os rótulos `C1` E `C2` estiverem presentes, mas não restringe a mesma ação se apenas um desses rótulos estiver presente.
>
>Quando se trata de aplicação automática, a estrutura de governança de dados não considera a ativação de públicos-alvo separados para um destino como uma combinação de dados. Portanto, a política `C1 AND C2` de exemplo é **NOT** imposta se esses rótulos forem incluídos em públicos separados. Em vez disso, essa política só é aplicada quando ambos os rótulos estão presentes no mesmo público-alvo na ativação.

Quando ocorrem violações de política, as mensagens resultantes que aparecem na interface fornecem ferramentas úteis para explorar a linhagem de dados de contribuição da violação para ajudar a resolver o problema. Mais detalhes são fornecidos na próxima seção.

## Mensagens de aplicação de política {#enforcement}

As seções abaixo descrevem as diferentes mensagens de aplicação de política exibidas na interface do usuário do Experience Platform:

* [Violação da política de uso de dados](#data-usage-violation)
* [Avaliação da política de consentimento](#consent-policy-evaluation)

### Violação da política de uso de dados {#data-usage-violation}

Se ocorrer uma violação de política ao tentar ativar um público-alvo (ou [fazer edições em um público-alvo já ativado](#policy-enforcement-for-activated-audiences)), a ação será impedida e um pop-over será exibido indicando que uma ou mais políticas foram violadas. Depois que uma violação é acionada, o botão **[!UICONTROL Salvar]** fica desabilitado para a entidade que você está modificando até que os componentes apropriados sejam atualizados para estar em conformidade com as políticas de uso de dados.

Selecione um nome de política para exibir detalhes dessa violação.

![Uma caixa de diálogo que indica que ocorreu uma violação de política com o nome de política realçado.](../images/enforcement/violation-policy-select.png)

A mensagem de violação fornece um resumo da política que foi violada, incluindo as condições que a política está configurada para verificar, a ação específica que acionou a violação e uma lista de possíveis resoluções para a ocorrência.

![Uma caixa de diálogo de violação de política com o resumo da violação realçado.](../images/enforcement/violation-summary.png)

Um gráfico de linhagem de dados é exibido abaixo do resumo da violação, permitindo visualizar quais conjuntos de dados, políticas de mesclagem, públicos-alvo e destinos estavam envolvidos na violação de política. A entidade que você está alterando no momento está destacada no gráfico, indicando qual ponto no fluxo está causando a violação. Você pode selecionar um nome de entidade no gráfico para abrir a página de detalhes da entidade em questão.

![Uma caixa de diálogo de violação de política com o gráfico de linhagem de dados destacado.](../images/enforcement/data-lineage.png)

Você também pode usar o ícone **[!UICONTROL Filtro]** (![Um ícone de filtro.](/help/images/icons/filter.png)) para filtrar as entidades exibidas por categoria. Pelo menos duas categorias devem ser selecionadas para que os dados sejam exibidos.

![Uma caixa de diálogo de violação de política com o filtro de linhagem de dados e o menu suspenso destacados.](../images/enforcement/lineage-filter.png)

Selecione **[!UICONTROL Exibição de lista]** para exibir a linhagem de dados como uma lista. Para voltar para o gráfico visual, selecione **[!UICONTROL Exibição de caminho]**.

![Uma caixa de diálogo de violação de política com a exibição do caminho de linhagem de dados em destaque.](../images/enforcement/list-view.png)

#### Rótulos aplicados com sucesso {#labels-successfully-applied}

Se você criar políticas de uso de dados antes de rotular os campos do esquema, poderá encontrar uma caixa de diálogo de violação de política de governança assim que aplicar rótulos ao esquema. Nesse caso, você pode rotular parte do esquema com êxito. A guia [!UICONTROL Rótulos aplicados com êxito] indica quais rótulos foram aplicados com êxito, pois não há restrições de política em relação a esse campo.

Use o diagrama de linhagem de dados para entender quais outras alterações de configuração precisam ser feitas antes de você poder adicionar o rótulo ao campo de esquema.

![Uma caixa de diálogo de violação de política com a guia [!UICONTROL Rótulos aplicados com êxito] foi realçada.](../images/enforcement/labels-successfully-applied.png)

### Avaliação da política de consentimento {#consent-policy-evaluation}

Ao ativar um público-alvo para um destino, você pode ver como as [políticas de consentimento](../policies/user-guide.md) afetam o alcance do público-alvo durante o [estágio de revisão do [!UICONTROL fluxo de trabalho Ativar Destinos]](#pre-activation-evaluation).

>[!NOTE]
>
>As políticas de consentimento só estão disponíveis para organizações que compraram o Adobe Healthcare Shield ou o Adobe Privacy &amp; Security Shield.

#### Aprimoramento da política de consentimento para mídia paga {#consent-policy-enhancement}

Foi feito um aprimoramento na aplicação da política de consentimento nos destinos [batch](../../destinations/destination-types.md#file-based) e [streaming](../../destinations/destination-types.md#streaming-destinations), incluindo ativações de mídia paga. Esse aprimoramento está disponível para clientes do Privacy e Security Shield ou Healthcare Shield e remove proativamente perfis de destinos de lote e streaming conforme o status de consentimento é alterado. Também garante que as alterações de consentimento sejam propagadas imediatamente para que o público-alvo correto seja sempre direcionado.

Essas melhorias permitem maior confiança na sua estratégia de marketing, pois removem a necessidade de os profissionais de marketing adicionarem atributos de consentimento manualmente à expressão do segmento. Isso garante que nenhum perfil seja direcionado inadvertidamente para qualquer experiência de marketing depois que o consentimento tiver sido retirado ou não estiver mais qualificado para uma política de consentimento. As políticas de consentimento de marketing que definem regras para como os dados de consentimento ou preferência devem ser gerenciados em vários workflows de marketing agora são aplicadas automaticamente nos workflows de ativação em soluções downstream.

>[!NOTE]
>
>Não há alterações na interface do usuário como resultado desse aprimoramento.

#### Avaliação de pré-ativação {#pre-activation-evaluation}

Depois de atingir a etapa **[!UICONTROL Revisão]** ao [ativar um destino](../../destinations/ui/activation-overview.md), selecione **[!UICONTROL Exibir políticas aplicadas]**.

![Botão Exibir políticas aplicadas no fluxo de trabalho de destino ativado](../images/enforcement/view-applied-policies.png)

Uma caixa de diálogo de verificação de política é exibida, mostrando uma visualização de como suas políticas de consentimento afetam o público-alvo consentido dos públicos a serem ativados.

![Caixa de diálogo de verificação de política de consentimento na interface do usuário do Experience Platform](../images/enforcement/consent-policy-check.png)

A caixa de diálogo mostra o público-alvo consentido para um público-alvo de cada vez. Para exibir a avaliação de política para um público-alvo diferente, use o menu suspenso acima do diagrama para selecionar um na lista.

![O alternador de público-alvo na caixa de diálogo de verificação de política.](../images/enforcement/audience-switcher.png)

Use o painel esquerdo para alternar entre as políticas de consentimento aplicáveis ao público selecionado. As políticas não selecionadas são representadas na seção &quot;[!UICONTROL Outras políticas]&quot; do diagrama.

![Alternador de política na caixa de diálogo de verificação de política](../images/enforcement/policy-switcher.png)

O diagrama exibe a sobreposição entre três grupos de perfis:

1. Perfis qualificados para o público-alvo selecionado
1. Perfis qualificados para a política de consentimento selecionada
1. Perfis qualificados para as outras políticas de consentimento aplicáveis ao público-alvo (referidas como &quot;[!UICONTROL Outras políticas]&quot; no diagrama)

Os perfis qualificados para os três grupos acima representam o público-alvo consentido, resumido no painel direito.

![Seção de resumo na caixa de diálogo de verificação de política](../images/enforcement/summary.png)

Passe o mouse sobre um dos públicos-alvo no diagrama para mostrar o número de perfis que ele contém.

![Realçando uma seção de diagrama na caixa de diálogo de verificação de política](../images/enforcement/highlight-segment.png)

O público consentido é representado pela sobreposição central do diagrama e pode ser destacado como as outras seções.

![Realçando o público consentido no diagrama](../images/enforcement/consented-audience.png)

#### Imposição de execução de fluxo

Quando os dados são ativados para um destino, os detalhes da execução do fluxo mostram o número de identidades que foram excluídas devido a políticas de consentimento ativas.

![Métricas de identidades excluídas para uma execução de fluxo de dados](../images/enforcement/dataflow-run-enforcement.png)

## Imposição de política para públicos ativados {#policy-enforcement-for-activated-audiences}

A aplicação de política ainda se aplica a públicos depois de serem ativados, restringindo quaisquer alterações em um público ou seu destino que resultem em uma violação de política. Devido ao modo como a [linhagem de dados](#lineage) funciona na imposição de política, qualquer uma das seguintes ações pode disparar uma violação:

* Atualização de rótulos de uso de dados
* Alteração de conjuntos de dados para um público
* Alteração de predicados de público
* Alteração das configurações de destino

Se qualquer uma das ações acima acionar uma violação, essa ação será impedida de ser salva e uma mensagem de violação de política será exibida, garantindo que os públicos-alvo ativados continuem em conformidade com as políticas de uso de dados ao serem modificados.

## Próximas etapas

Este documento abordou como a aplicação automática de políticas funciona no Experience Platform. Para obter etapas sobre como integrar programaticamente a imposição de política em seus aplicativos usando chamadas de API, consulte o manual em [Imposição baseada em API](./api-enforcement.md).
