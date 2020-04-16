---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Ativar dados de origem de entrada para preencher perfis de clientes
topic: overview
translation-type: tm+mt
source-git-commit: d6d2faf3d5eabcd8e948d3717fd8f8df4b9cb85a

---


# Ativar dados de origem de entrada para preencher perfis de clientes

Os dados de entrada do conector de origem podem ser usados para enriquecer e preencher os dados de Perfil do cliente em tempo real.

## Introdução

Este tutorial requer uma compreensão prática dos seguintes componentes da Adobe Experience Platform:

- [Sistema](../../../xdm/home.md)do Experience Data Model (XDM): A estrutura padronizada pela qual a plataforma Experience organiza os dados da experiência do cliente.
   - [Noções básicas da composição](../../../xdm/schema/composition.md)do schema: Saiba mais sobre os elementos básicos dos schemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   - [Tutorial](../../../xdm/tutorials/create-schema-ui.md)do Editor de Schemas: Saiba como criar schemas personalizados usando a interface do editor de Schemas.
- [Perfil](../../../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o consumidor, com base em dados agregados de várias fontes.

Além disso, este tutorial requer que você já tenha criado e configurado um conector de origem.  Uma lista de tutoriais para criar conectores diferentes na interface do usuário pode ser encontrada na visão geral [dos conectores de](../../home.md)origem.

## Preencha seus dados de Perfil do cliente em tempo real

Para enriquecer os perfis do cliente, o schema de origem do conjunto de dados do público alvo deve ser compatível para uso no Perfil do cliente em tempo real. Um schema compatível satisfaz os seguintes requisitos:

- O schema tem pelo menos um atributo especificado como uma propriedade de identidade.
- O schema tem uma propriedade de identidade definida como a identidade primária.
- Existe um mapeamento no fluxo de dados no qual a identidade primária é um atributo de público alvo.

Na área de trabalho Fontes, clique na guia **Procurar** para lista das conexões básicas. Na lista exibida, localize a conexão que contém o fluxo de dados com o qual você deseja preencher perfis. Clique no nome da conexão para acessar seus detalhes.

![](../../images/tutorials/dataflow/cloud-storage/browse.png)

A tela atividade ** de origem da conexão é exibida, exibindo os conjuntos de dados nos quais a conexão está assimilando os dados de origem. Clique no nome do conjunto de dados que deseja ativar para o Perfil.

![](../../images/tutorials/dataflow/cloud-storage/dataset-dataflow.png)

A tela atividade *do Conjunto* de Dados é exibida. A coluna *Propriedades* no lado direito da tela exibe os detalhes do conjunto de dados e inclui um switch de **Perfil** e um link para o schema ao qual o conjunto de dados obedece. Clique no nome do schema para visualização de sua composição.

![](../../images/tutorials/dataflow/cloud-storage/select-dataset-schema.png)

O Editor *de* Schemas é exibido, mostrando a estrutura do schema na tela central. Na tela de desenho, selecione o campo a ser definido como a identidade primária. Na guia Propriedades *do* campo que é exibida, marque a caixa de seleção **Identidade** e, em seguida, a identidade **** Principal. Por fim, selecione uma namespace **de** identidade apropriada e clique em **Aplicar**.

![](../../images/tutorials/dataflow/cloud-storage/set-schema-identity.png)

Clique no objeto de nível superior da estrutura do schema e a coluna de propriedades *do* Schema será exibida. Ative o schema para o Perfil, alternando a chave do **Perfil** . Clique em **Salvar** para finalizar as alterações.

![](../../images/tutorials/dataflow/cloud-storage/enable-profile.png)

Agora que o schema está ativado para o Perfil, volte à tela de atividade *do* Conjunto de Dados e ative o conjunto de dados para o Perfil clicando no botão de alternância do **Perfil** na coluna *Propriedades* .

![](../../images/tutorials/dataflow/cloud-storage/enable-dataset-profile.png)

Com o schema e o conjunto de dados habilitados para o Perfil, os dados ingeridos nesse conjunto de dados também preencherão os perfis do cliente.

>[!NOTE] Os dados existentes em um conjunto de dados recentemente habilitado não são consumidos pelo Perfil

## Próximas etapas

Ao seguir este tutorial, você ativou com êxito os dados de entrada para a população do Perfil. Para obter mais informações, consulte a visão geral [do Perfil do cliente em tempo](../../../profile/home.md)real.