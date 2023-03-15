---
keywords: Experience Platform;página inicial;tópicos populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Criar uma conexão de origem do Zoho CRM na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Zoho CRM usando a interface do usuário do Adobe Experience Platform.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: ed92bdcd965dc13ab83649aad87eddf53f7afd60
workflow-type: tm+mt
source-wordcount: '551'
ht-degree: 1%

---

# Criar um [!DNL Zoho CRM] conexão de origem na interface

Os conectores de origem no Adobe Experience Platform fornecem a capacidade de assimilar dados de CRM de origem externa de forma programada. Este tutorial fornece etapas para a criação de um [!DNL Zoho CRM] conector de origem usando o [!DNL Platform] interface do usuário.

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): o quadro normalizado pelo qual [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas da composição do esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os componentes básicos dos esquemas XDM, incluindo princípios fundamentais e práticas recomendadas na composição do esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver um [!DNL Zoho CRM] conta, você pode ignorar o restante deste documento e prosseguir para o tutorial em [configuração de um fluxo de dados](../../dataflow/crm.md).

### Coletar credenciais necessárias

Para se conectar [!DNL Zoho CRM] Para o Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| Endpoint | O endpoint do [!DNL Zoho CRM] servidor ao qual você está fazendo sua solicitação. |
| URL de contas | O URL das contas é usado para gerar os tokens de acesso e atualização. O URL deve ser específico do domínio. |
| ID do cliente | A ID do cliente que corresponde ao seu [!DNL Zoho CRM] conta de usuário. |
| Segredo do cliente | O segredo do cliente que corresponde ao seu [!DNL Zoho CRM] conta de usuário. |
| Token de acesso | O token de acesso autoriza o acesso seguro e temporário aos [!DNL Zoho CRM] conta. |
| Atualizar token | Um token de atualização é um token usado para gerar um novo token de acesso depois que ele expirar. |

Para obter mais informações sobre essas credenciais, consulte a documentação em [[!DNL Zoho CRM] autenticação](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Conecte seu [!DNL Zoho CRM] account

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular [!DNL Zoho CRM] conta para [!DNL Platform].

Na interface do usuário da Platform, selecione **[!UICONTROL Origens]** na barra de navegação esquerda, para acessar a [!UICONTROL Origens] espaço de trabalho. A variável [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

No [!UICONTROL CRM] categoria, selecione **[!UICONTROL Zoho CRM]** e selecione **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/zoho/catalog.png)

A variável **[!UICONTROL Conectar a conta do Zoho CRM]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a variável [!DNL Zoho CRM] conta com a qual deseja criar um novo fluxo de dados e selecione **[!UICONTROL Próxima]** para continuar.

![existente](../../../../images/tutorials/create/zoho/existing.png)

### Nova conta

Se estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas [!DNL Zoho CRM] credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para estabelecer a nova conexão.

>[!TIP]
>
>O domínio da URL das contas deve corresponder ao local de domínio apropriado. A seguir estão os vários domínios e suas URLs de contas correspondentes:<ul><li>Estados Unidos: https://accounts.zoho.com</li><li>Austrália: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>Índia: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

![novo](../../../../images/tutorials/create/zoho/new.png)

## Próximas etapas

Ao seguir este tutorial, você estabeleceu uma conexão com o seu [!DNL Zoho CRM] conta. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](../../dataflow/crm.md).
