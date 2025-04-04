---
keywords: Experience Platform;página inicial;tópicos populares;Veeva CRM;veeva
solution: Experience Platform
title: Criar uma conexão com o Veeva CRM Source na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Veeva CRM usando a interface do Adobe Experience Platform.
exl-id: 4ef76c28-9bd2-4e54-a3d6-dceb89162337
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '427'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL Veeva CRM] na interface

Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados de CRM originados externamente de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Veeva CRM] usando a interface do usuário [!DNL Experience Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conta válida do [!DNL Veeva CRM], ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/crm.md).

### Coletar credenciais necessárias

| Credencial | Descrição |
| ---------- | ----------- |
| `environmentUrl` | A URL da instância de origem [!DNL Veeva CRM]. |
| `username` | O nome de usuário da conta de usuário [!DNL Veeva CRM]. |
| `password` | A senha da conta de usuário [!DNL Veeva CRM]. |
| `securityToken` | O token de segurança para a conta de usuário [!DNL Veeva CRM]. |

Para obter mais informações sobre a introdução, consulte este [[!DNL Veeva CRM] documento](https://developer.veevacrm.com/doc/Content/rest-api.htm).

## Conectar sua conta do [!DNL Veeva CRM]

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL Veeva CRM] ao [!DNL Experience Platform].

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL CRM], selecione **[!UICONTROL Veeva CRM]** e **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/veeva/catalog.png)

A página **[!UICONTROL Conectar a conta do Veeva CRM]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Veeva CRM] com a qual deseja criar um novo fluxo de dados e clique em **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/veeva/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais do [!DNL Veeva CRM]. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/veeva/new.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Veeva CRM]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Experience Platform](../../dataflow/crm.md).
