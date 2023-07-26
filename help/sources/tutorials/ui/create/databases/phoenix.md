---
title: Conecte sua conta Phoenix usando a interface do usuário do Experience Platform
description: Saiba como conectar sua conta Phoenix e trazer dados do banco de dados Phoenix para o Experience Platform usando a interface do usuário do.
exl-id: 2ed469bc-1c72-4f04-a5f0-6a0bb519a6c2
source-git-commit: b7e42eb180b8f16344afedadf763c33bcf22fa35
workflow-type: tm+mt
source-wordcount: '604'
ht-degree: 1%

---

# Conecte seu [!DNL Phoenix] conta para Experience Platform usando a interface do usuário

Este tutorial fornece etapas sobre como conectar seus [!DNL Phoenix] e traga dados de sua conta [!DNL Phoenix] banco de dados para Experience Platform.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o Experience Platform organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Phoenix] conta, ignore o restante deste documento e prossiga para o tutorial em [configuração de um fluxo de dados para um banco de dados](../../dataflow/databases.md).

### Coletar credenciais necessárias

Para acessar seu [!DNL Phoenix] conta no Experience Platform, você deve fornecer os seguintes valores:

| Credencial | Descrição |
| --- | --- |
| Host | O endereço IP ou o nome de host do [!DNL Phoenix] servidor. |
| Porta | A porta TCP que o [!DNL Phoenix] O servidor usa o para detectar conexões de clientes. Se você estiver se conectando ao [!DNL Azure HDInsights]e especifique a porta como 443. Se esse parâmetro não for fornecido, o valor padrão será 8765. |
| Caminho HTTP | O URL parcial correspondente à variável [!DNL Phoenix] servidor. Especifique /hbasephoenix0 se estiver usando o [!DNL Azure HDInsights] cluster. |
| Nome de usuário | O nome de usuário que você usa para acessar o [!DNL Phoenix] servidor. |
| Senha | A senha que corresponde ao usuário. |
| Enable SSL | Um botão que especifica se as conexões com o servidor são criptografadas usando SSL. |

Para obter mais informações sobre a introdução, consulte [este [!DNL Phoenix] documento](https://python-phoenixdb.readthedocs.io/en/latest/api.html).

Depois de obter as credenciais necessárias, siga as etapas abaixo para conectar seu [!DNL Phoenix] conta para Experience Platform.

## Conecte seu [!DNL Phoenix] account

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na navegação à esquerda, para acessar o espaço de trabalho de fontes. A variável *[!UICONTROL Catálogo]* A tela exibe uma variedade de fontes disponíveis no catálogo de fontes do Experience Platform.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar uma fonte específica usando a opção de pesquisa.

Selecionar **[!UICONTROL Bancos de dados]** na lista de categorias de origens e selecione **[!UICONTROL Adicionar dados]** do [!DNL Phoenix] cartão.

>[!TIP]
>
>As origens no catálogo de origens podem exibir prompts diferentes, dependendo do status da origem.
> 
>* **[!UICONTROL Adicionar dados]** significa que há contas autenticadas existentes associadas à origem selecionada.
>
>* **[!UICONTROL Configurar]** significa que você deve fornecer credenciais e autenticar uma nova conta para usar a fonte selecionada.

![O catálogo de origens na interface do usuário do Experience Platform com o cartão de origem Phoenix selecionado.](../../../../images/tutorials/create/phoenix/catalog.png)

A variável **[!UICONTROL Conectar-se a Phoenix]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

>[!BEGINTABS]

>[!TAB Usar uma conta existente do Phoenix]

Para usar uma conta existente, selecione [!UICONTROL Conta existente] e, em seguida, selecione a conta que deseja usar na lista exibida. Quando terminar, selecione [!UICONTROL Próxima] para continuar.

![Uma lista de contas autenticadas do banco de dados Phoenix que já existem em sua organização.](../../../../images/tutorials/create/phoenix/existing.png)

>[!TAB Criar uma nova conta do Phoenix]

Para usar uma nova conta, selecione [!UICONTROL Nova conta] e forneça um nome, uma descrição e sua [!DNL Phoenix] credenciais de autenticação. Quando terminar, selecione [!UICONTROL Conectar à origem] e aguarde alguns segundos para que a nova conexão seja estabelecida.

![A nova interface de conta, onde você pode fornecer credenciais de autenticação e criar uma conta Phoenix.](../../../../images/tutorials/create/phoenix/new.png)

>[!ENDTABS]

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Phoenix] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para o Experience Platform](../../dataflow/databases.md).
