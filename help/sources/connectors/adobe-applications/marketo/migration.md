---
title: Migrar mapeamento de ECID de pessoa para atividade usando a origem do Marketo Engage
description: Saiba como migrar seu mapeamento ECID do conjunto de dados de pessoa para o conjunto de dados de atividade usando a fonte Marketo Engage.
source-git-commit: 0c695e11e7d7c14ef7e047cd007668e1099bf127
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 0%

---

# Migrar mapeamento ECID de [!DNL Person] conjunto de dados para [!DNL Activity] conjunto de dados

Você pode migrar o mapeamento ECID de sua [!DNL Marketo Engage Person] conjunto de dados para seu [!DNL Activity] conjunto de dados para fornecer um comportamento mais estável de assimilação de dados e gerenciamento de identidade. Além disso, essa migração aborda o seguinte:

| Problema | Solução |
| --- | --- |
| Quando o [!DNL Marketo Person] tiver links para várias ECIDs, a assimilação de dados falhará quando a variável [o número total de identidades em um registro do Experience Data Model (XDM) excede 20](../../../../identity-service/guardrails.md). | Ao migrar o mapeamento de campo da ECID para [!DNL Activity], você pode garantir que o número de identidades da variável [!DNL Marketo Person] o fluxo de dados permanece dentro do limite e, portanto, permite que a assimilação de dados seja bem-sucedida. |
| Sempre que a variável [!DNL Marketo Person] é assimilado com ECIDs, o carimbo de data e hora em todas as ECIDs do [!DNL Marketo Person] Os conjuntos de dados do são atualizados com o último carimbo de data e hora atualizado do registro de Pessoa. Isso pode resultar na [exclusão incorreta de identidades mais recentes no gráfico de identidade](../../../../identity-service/guardrails.md#understanding-the-deletion-logic-when-an-identity-graph-at-capacity-is-updated). | Ao migrar os mapeamentos de campo ECID para o [!DNL Activity]O, Serviço de identidade pode refletir corretamente o carimbo de data e hora da ECID e o mecanismo &quot;primeiro a entrar, primeiro a sair&quot; do Serviço de identidade fornecerá um comportamento mais estável. |
| Quando as ECIDs são assimiladas por meio do [!DNL Marketo Person] fluxo de dados, as ECIDs recém-adicionadas não são assimiladas no Experience Platform, a menos que haja atualizações no [!DNL Person] gravar em [!DNL Marketo]. | Quando uma nova ECID é vinculada à variável [!DNL Person] gravar em [!DNL Marketo], você pode assimilar esses dados ECID por meio de uma [!DNL Marketo Activity] fluxo de dados e solicitar imediatamente uma atualização do gráfico de identidade no Experience Platform. |

Basicamente, você deve:

* Atualize seu [!DNL Marketo Activity] fluxo de dados.
* Atualize seu [!DNL Marketo Person] fluxo de dados.

## Atualizar [!DNL Marketo Activity] fluxo de dados {#update-activity-dataflow}

Siga as etapas abaixo para atualizar sua [!DNL Marketo Activity] fluxo de dados:

* Na interface do usuário do Experience Platform, navegue até a *Origens* e encontrar seu fluxo de dados existente para [!DNL Marketo Activity] dados.
* Como o fluxo de dados está ativado, selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Atualizar fluxo de dados]**.
* Em seguida, selecione **[!UICONTROL Próxima]** até que você atinja o *Mapeamento* interface.
* No *Mapeamento* , selecione **[!UICONTROL Novo campo]** e selecione **[!UICONTROL Adicionar campo calculado]**. Aqui, você deve adicionar o seguinte:

| Conjunto de dados de origem | Campo de destino XDM |
| --- | --- |
| `iif(${web\.ecid} != null, to_object('ECID', arrays_to_objects('id', explode(last(split(${web\.ecid}, ":")), " "))), null)` | `identityMap` |

>[!NOTE]
>
>Se sua atualização para um existente [!DNL Marketo] O fluxo de dados consiste em adicionar ou remover apenas o campo de mapeamento ECID e, em seguida, o fluxo de dados ignora automaticamente a tarefa de preenchimento retroativo histórico. A nova assimilação de dados só ocorrerá quando ocorrerem tipos de atividade, como &quot;visitar página da Web&quot; e &quot;clicar página da Web&quot;.

## Atualizar [!DNL Marketo Person] fluxo de dados {#update-person-dataflow}

Siga as etapas abaixo para atualizar sua [!DNL Marketo Person] fluxo de dados:

* Na interface do usuário do Experience Platform, navegue até a *Origens* e encontrar seu fluxo de dados existente para [!DNL Marketo Person] dados.
* Como o fluxo de dados está ativado, selecione as reticências (`...`) ao lado do nome do fluxo de dados e selecione **[!UICONTROL Atualizar fluxo de dados]**.
* Em seguida, selecione **[!UICONTROL Próxima]** até que você atinja o *Mapeamento* interface.
* No *Mapeamento* , remova o campo calculado que mapeia para `identityMap` e selecione **[!UICONTROL Próxima]** e **[!UICONTROL Salvar e assimilar]**.

>[!NOTE]
>
>Se sua atualização para um existente [!DNL Marketo] O fluxo de dados consiste em adicionar ou remover apenas o campo de mapeamento ECID e, em seguida, o fluxo de dados ignora automaticamente a tarefa de preenchimento retroativo histórico. O carimbo de data e hora das ECIDs que foram assimiladas anteriormente permanecerá o mesmo. Eles só serão atualizados quando novos dados que correspondem às ECIDs existentes forem assimilados.

## Próximas etapas

Ao ler este documento, agora você sabe como migrar o mapeamento ECID do seu [!DNL Marketo Person] conjunto de dados para [!DNL Marketo Activity] conjunto de dados. Para obter mais informações, leia o seguinte [!DNL Marketo] documentos:

* [Criar um fluxo de dados para assimilar [!DNL Marketo] dados para Experience Platform](../../../tutorials/ui/create/adobe-applications/marketo.md).
* [Guia de mapeamento de campo](../mapping/marketo.md).