---
keywords: Experience Platform; home; tópicos populares; Veeva CRM; veeva
solution: Experience Platform
title: Criar uma conexão de fonte de CRM de tela na interface do usuário
topic-legacy: overview
type: Tutorial
description: Saiba como criar uma conexão de origem do Veeva CRM usando a interface do usuário do Adobe Experience Platform.
source-git-commit: 3235c48ec1f449e45b3f4b096585b67e14600407
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 1%

---

# Criar uma conexão de origem [!DNL Veeva CRM] na interface do usuário

Os conectores de origem no Adobe Experience Platform oferecem a capacidade de assimilar dados de CRM de origem externa de acordo com a programação. Este tutorial fornece etapas para criar um conector de origem [!DNL Veeva CRM] usando a interface do usuário [!DNL Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): A estrutura padronizada pela qual  [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição](../../../../../xdm/schema/composition.md) do schema: Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial](../../../../../xdm/tutorials/create-schema-ui.md) do Editor de esquema: Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conta válida [!DNL Veeva CRM], poderá ignorar o restante deste documento e prosseguir para o tutorial em [configurar um fluxo de dados](../../dataflow/crm.md).

### Obter credenciais necessárias

| Credencial | Descrição |
| ---------- | ----------- |
| `environmentUrl` | O URL da instância de origem [!DNL Veeva CRM]. |
| `username` | O nome de usuário da conta de usuário [!DNL Veeva CRM]. |
| `password` | A senha da conta de usuário [!DNL Veeva CRM]. |
| `securityToken` | O token de segurança para a conta de usuário [!DNL Veeva CRM]. |

Para obter mais informações sobre a introdução, consulte [este documento de Veeva CRM]

## Conecte sua conta [!DNL Veeva CRM]

Depois de coletar suas credenciais necessárias, siga as etapas abaixo para vincular sua conta [!DNL Veeva CRM] a [!DNL Platform].

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL CRM], selecione **[!UICONTROL Veeva CRM]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/veeva/catalog.png)

A página **[!UICONTROL Conectar Veeva CRM account]** é exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Veeva CRM] com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para prosseguir.

![existente](../../../../images/tutorials/create/veeva/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL New account]** e forneça um nome, uma descrição opcional e suas credenciais [!DNL Veeva CRM]. Quando terminar, selecione **[!UICONTROL Connect to source]** e, em seguida, conceda algum tempo para que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/veeva/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com sua conta [!DNL Veeva CRM]. Agora você pode continuar para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a plataforma](../../dataflow/crm.md).
