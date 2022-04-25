---
keywords: Experience Platform, home, tópicos populares, Quadrado, quadrado
title: Criar uma conexão de origem quadrada na interface do usuário
description: Saiba como criar uma conexão de origem quadrada usando a interface do usuário do Adobe Experience Platform.
source-git-commit: e905b11040c8de33aa757bd5743605bb36a8009b
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 2%

---

# Crie um [!DNL Square] conexão de origem na interface do usuário

Este tutorial fornece etapas para criar um [!DNL Square] conector de origem usando a interface do usuário da plataforma.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): O quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do schema](../../../../../xdm/schema/composition.md): Saiba mais sobre os elementos básicos dos esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição do schema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): Saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado e em tempo real com base em dados agregados de várias fontes.

### Obter credenciais necessárias

Para acessar o [!DNL Square] account Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| --- | --- |
| Host | O URL do [!DNL Square] instância. |
| ID do cliente | A ID do cliente associada à [!DNL Square] conta. |
| Segredo do cliente | O segredo do cliente associado ao seu [!DNL Square] conta. |
| Token de acesso | O token de acesso é usado para autenticar seu [!DNL Square] com autenticação OAuth 2.0. O token de acesso pode ser obtido de [!DNL Square]. |
| Atualizar token | O token de atualização é usado para gerar novos tokens de acesso depois que o token de acesso atual expirar. O token de atualização pode ser obtido de [!DNL Square]. |

Para obter mais informações sobre essas credenciais e como obtê-las, consulte o [[!DNL Square] documentação sobre o OAuth](https://developer.squareup.com/docs/oauth-api/receive-and-manage-tokens).

Depois de reunir suas credenciais necessárias, siga as etapas abaixo para vincular seus [!DNL Square] para a Platform.

## Conecte seu [!DNL Square] account

Na interface do usuário da plataforma, selecione **[!UICONTROL Fontes]** na navegação à esquerda para acessar o [!UICONTROL Fontes] espaço de trabalho. O [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Em [!UICONTROL Pagamentos] categoria , selecione **[!UICONTROL Quadrado]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/square/catalog.png)

O **[!UICONTROL Conectar ao Quadrado]** será exibida. Nesta página, você pode usar novas credenciais ou credenciais existentes.

### Conta existente

Para usar uma conta existente, selecione a [!DNL Square] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próximo]** para continuar.

![existente](../../../../images/tutorials/create/square/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e os valores apropriados para sua [!DNL Square] credenciais. Quando terminar, selecione **[!UICONTROL Conectar-se à origem]** e, em seguida, permitir que a nova conexão seja estabelecida.

![novo](../../../../images/tutorials/create/square/new.png)

## Próximas etapas

Ao seguir este tutorial, você autenticou e criou uma conexão de origem entre os [!DNL Square] conta e plataforma. Agora você pode continuar para o próximo tutorial e [criar um fluxo de dados para trazer dados de pagamentos para a Platform](../../dataflow/payments.md).
