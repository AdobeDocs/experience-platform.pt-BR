---
keywords: Experience Platform;home;popular topics;ativar dados de entrada;preencher perfil;preencher rtcp;preencher perfil unificado
solution: Experience Platform
title: Ativar dados de origem de entrada para preencher Perfis de clientes na interface do usuário
topic: overview
type: Tutorial
description: Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os dados de Perfil do cliente em tempo real.
translation-type: tm+mt
source-git-commit: c7fb0d50761fa53c1fdf4dd70a63c62f2dcf6c85
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 0%

---


# Ativar dados de origem de entrada para preencher perfis de clientes

Os dados de entrada do seu conector de origem podem ser usados para enriquecer e preencher seus dados [!DNL Real-time Customer Profile].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

- [[!DNL Experience Data Model (XDM)] Sistema](../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   - [Noções básicas da composição](../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md) do Editor de schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [[!DNL Real-time Customer Profile]](../../../profile/home.md): Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Além disso, este tutorial requer que você já tenha criado e configurado um conector de origem.  Uma lista de tutoriais para criar conectores diferentes na interface do usuário pode ser encontrada na [visão geral dos conectores de origem](../../home.md).

## Preencha seus dados [!DNL Real-time Customer Profile]

Para enriquecer os perfis do cliente, o schema de origem do conjunto de dados do público alvo deve ser compatível para uso em [!DNL Real-time Customer Profile]. Um schema compatível satisfaz os seguintes requisitos:

- O schema tem pelo menos um atributo especificado como uma propriedade de identidade.
- O schema tem uma propriedade de identidade definida como a identidade primária.
- Existe um mapeamento no fluxo de dados no qual a identidade primária é um atributo de público alvo.

Na área de trabalho Fontes, clique na guia **[!UICONTROL Procurar]** para lista das conexões básicas. Na lista exibida, localize a conexão que contém o fluxo de dados com o qual você deseja preencher perfis. Clique no nome da conexão para acessar seus detalhes.

![](../../images/tutorials/dataflow/cloud-storage/batch/browse.png)

A tela **[!UICONTROL atividade de origem]** da conexão é exibida, exibindo os conjuntos de dados nos quais a conexão está assimilando os dados de origem. Clique no nome do conjunto de dados que deseja ativar para [!DNL Profile].

![](../../images/tutorials/dataflow/cloud-storage/batch/dataset-dataflow.png)

A tela **[!UICONTROL atividade do conjunto de dados]** é exibida. A coluna **[!UICONTROL Propriedades]** no lado direito da tela exibe os detalhes do conjunto de dados e inclui um switch **[!UICONTROL Perfil]** e um link para o schema ao qual o conjunto de dados adere. Clique no nome do schema para visualização de sua composição.

![](../../images/tutorials/dataflow/cloud-storage/batch/select-dataset-schema.png)

O **[!UICONTROL Editor de Schemas]** é exibido, mostrando a estrutura do schema na tela central. Na tela de desenho, selecione o campo a ser definido como a identidade primária. Na guia **[!UICONTROL Propriedades do campo]** que é exibida, marque a caixa de seleção **[!UICONTROL Identidade]** e **[!UICONTROL Identidade primária]**. Finalmente, selecione uma **[!UICONTROL namespace de identidade]** apropriada e clique em **[!UICONTROL Aplicar]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/set-schema-identity.png)

Clique no objeto de nível superior da estrutura do schema e a coluna **[!UICONTROL propriedades do Schema]** será exibida. Ative o schema para [!DNL Profile], alternando o switch **[!UICONTROL Perfil]**. Clique em **[!UICONTROL Salvar]** para finalizar as alterações.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-profile.png)

Agora que o schema está ativado para [!DNL Profile], volte à tela **[!UICONTROL atividade do conjunto de dados]** e ative o conjunto de dados para [!DNL Profile] clicando no alternador **[!UICONTROL Perfil]** na coluna **[!UICONTROL Propriedades]**.

![](../../images/tutorials/dataflow/cloud-storage/batch/enable-dataset-profile.png)

Com o schema e o conjunto de dados habilitados para [!DNL Profile], os dados ingeridos nesse conjunto de dados também preencherão os perfis do cliente.

>[!NOTE]
>
>Os dados existentes em um conjunto de dados recentemente habilitado não são consumidos por [!DNL Profile].

## Próximas etapas

Ao seguir este tutorial, você ativou com êxito os dados de entrada para a população [!DNL Profile]. Para obter mais informações, consulte [[!DNL Real-time Customer Profile] overview](../../../profile/home.md).