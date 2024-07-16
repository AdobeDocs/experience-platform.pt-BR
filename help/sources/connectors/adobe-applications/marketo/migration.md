---
title: Migrar mapeamento de ECID de pessoa para atividade usando a origem do Marketo Engage
description: Saiba como migrar seu mapeamento ECID do conjunto de dados de pessoa para o conjunto de dados de atividade usando a fonte Marketo Engage.
exl-id: bcc91c53-aeca-4d7c-89b5-cf025d0357a0
source-git-commit: d03fcf06fb63ad2484ded3b85fc11ae45661babc
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Migrar mapeamento ECID do conjunto de dados [!DNL Person] para o conjunto de dados [!DNL Activity]

Você pode migrar seu mapeamento ECID do conjunto de dados [!DNL Marketo Engage Person] para o conjunto de dados [!DNL Activity] a fim de fornecer um comportamento mais estável de assimilação de dados e gerenciamento de identidade. Além disso, essa migração aborda o seguinte:

| Problema | Solução |
| --- | --- |
| Quando o conjunto de dados [!DNL Marketo Person] tem links para várias ECIDs, a assimilação de dados falha quando o [número total de identidades em um registro do Experience Data Model (XDM) excede 20](../../../../identity-service/guardrails.md). | Ao migrar o mapeamento de campos ECID para [!DNL Activity], é possível garantir que o número de identidades do fluxo de dados [!DNL Marketo Person] permaneça dentro do limite e, portanto, permita que a assimilação de dados seja bem-sucedida. |
| Toda vez que o conjunto de dados [!DNL Marketo Person] é assimilado com ECIDs, o carimbo de data e hora em todas as ECIDs do conjunto de dados [!DNL Marketo Person] é atualizado com o último carimbo de data e hora atualizado do registro de Pessoa. Isso pode resultar na [exclusão incorreta de identidades mais recentes do gráfico de identidade](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | Ao migrar os mapeamentos de campo da ECID para o [!DNL Activity], o Serviço de identidade pode refletir corretamente o carimbo de data e hora da ECID, e o mecanismo &quot;primeiro a entrar, primeiro a sair&quot; do Serviço de identidade fornecerá um comportamento mais estável. |
| Quando as ECIDs são assimiladas por meio do fluxo de dados [!DNL Marketo Person], as ECIDs recém-adicionadas não são assimiladas no Experience Platform, a menos que haja atualizações para o registro [!DNL Person] em [!DNL Marketo]. | Quando uma nova ECID é vinculada ao registro [!DNL Person] em [!DNL Marketo], você pode assimilar esses dados da ECID por meio de um fluxo de dados [!DNL Marketo Activity] e solicitar imediatamente uma atualização do gráfico de identidade no Experience Platform. |

Basicamente, você deve:

* Atualize seu fluxo de dados do [!DNL Marketo Activity].
* Atualize seu fluxo de dados do [!DNL Marketo Person].

## Atualizar fluxo de dados [!DNL Marketo Activity] {#update-activity-dataflow}

Siga as etapas abaixo para atualizar seu fluxo de dados do [!DNL Marketo Activity]:

* Na interface do usuário do Experience Platform, navegue até o espaço de trabalho *Fontes* e localize seu fluxo de dados existente para os dados [!DNL Marketo Activity].
* Como o fluxo de dados está habilitado, selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Atualizar fluxo de dados]**.
* Em seguida, selecione **[!UICONTROL Avançar]** até chegar à interface *Mapeamento*.
* Na interface *Mapping*, selecione **[!UICONTROL Novo campo]** e **[!UICONTROL Adicionar campo calculado]**. Aqui, você deve adicionar o seguinte:

| Conjunto de dados do Source | Campo de destino XDM |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Se a atualização para um fluxo de dados [!DNL Marketo] existente consistir apenas em adicionar ou remover o campo de mapeamento ECID, o fluxo de dados ignorará automaticamente o trabalho de preenchimento retroativo histórico. A nova assimilação de dados só ocorrerá quando ocorrerem tipos de atividade, como &quot;visitar página da Web&quot; e &quot;clicar página da Web&quot;.

## Atualizar fluxo de dados [!DNL Marketo Person] {#update-person-dataflow}

Siga as etapas abaixo para atualizar seu fluxo de dados do [!DNL Marketo Person]:

* Na interface do usuário do Experience Platform, navegue até o espaço de trabalho *Fontes* e localize seu fluxo de dados existente para os dados [!DNL Marketo Person].
* Como o fluxo de dados está habilitado, selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Atualizar fluxo de dados]**.
* Em seguida, selecione **[!UICONTROL Avançar]** até chegar à interface *Mapeamento*.
* Na interface *Mapeamento*, remova o campo calculado que mapeia para `identityMap` e selecione **[!UICONTROL Avançar]** e **[!UICONTROL Salvar e Assimilar]**.

>[!NOTE]
>
>Se a atualização para um fluxo de dados [!DNL Marketo] existente consistir apenas em adicionar ou remover o campo de mapeamento ECID, o fluxo de dados ignorará automaticamente o trabalho de preenchimento retroativo histórico. O carimbo de data e hora das ECIDs que foram assimiladas anteriormente permanecerá o mesmo. Eles só serão atualizados quando novos dados que correspondem às ECIDs existentes forem assimilados.

## Próximas etapas

Ao ler este documento, agora você sabe como migrar seu mapeamento ECID do conjunto de dados [!DNL Marketo Person] para o conjunto de dados [!DNL Marketo Activity]. Para obter mais informações, leia os [!DNL Marketo] documentos a seguir:

* [Criar um fluxo de dados para assimilar [!DNL Marketo] dados no Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Guia de mapeamento de campos](../mapping/marketo.md).
