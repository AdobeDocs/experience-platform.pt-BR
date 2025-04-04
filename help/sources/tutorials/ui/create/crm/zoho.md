---
keywords: Experience Platform;página inicial;tópicos populares;Zoho CRM;zoho crm;Zoho;zoho
solution: Experience Platform
title: Criar uma conexão Zoho CRM Source na interface
type: Tutorial
description: Saiba como criar uma conexão de origem do Zoho CRM usando a interface do usuário do Adobe Experience Platform.
exl-id: c648fc3e-beea-4030-8d36-dd8a7e2c281e
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL Zoho CRM] na interface

>[!WARNING]
>
>A origem [!DNL Zoho CRM] será substituída no final de junho de 2025.

Os conectores do Source no Adobe Experience Platform fornecem a capacidade de assimilar dados de CRM originados externamente de forma programada. Este tutorial fornece etapas para a criação de um conector de origem [!DNL Zoho CRM] usando a interface do usuário [!DNL Experience Platform].

## Introdução

Este tutorial requer uma compreensão funcional dos seguintes componentes do Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conta válida do [!DNL Zoho CRM], ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/crm.md).

### Coletar credenciais necessárias

Para conectar [!DNL Zoho CRM] ao Experience Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição |
| --- | --- |
| Endpoint | O ponto de extremidade do servidor [!DNL Zoho CRM] ao qual você está fazendo sua solicitação. |
| URL de contas | O URL das contas é usado para gerar os tokens de acesso e atualização. O URL deve ser específico do domínio. |
| ID de cliente | A ID do cliente que corresponde à sua conta de usuário do [!DNL Zoho CRM]. |
| Segredo do cliente | O segredo do cliente que corresponde à conta de usuário [!DNL Zoho CRM]. |
| Token de acesso | O token de acesso autoriza seu acesso seguro e temporário à sua conta do [!DNL Zoho CRM]. |
| Atualizar token | Um token de atualização é um token usado para gerar um novo token de acesso depois que ele expirar. |

Para obter mais informações sobre essas credenciais, consulte a documentação sobre [[!DNL Zoho CRM] autenticação](https://www.zoho.com/crm/developer/docs/api/v2/oauth-overview.html).

## Conectar sua conta do [!DNL Zoho CRM]

Depois de obter as credenciais necessárias, siga as etapas abaixo para vincular sua conta do [!DNL Zoho CRM] ao [!DNL Experience Platform].

Na interface do usuário do Experience Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria [!UICONTROL CRM], selecione **[!UICONTROL Zoho CRM]** e **[!UICONTROL Adicionar dados]**.

![catálogo](../../../../images/tutorials/create/zoho/catalog.png)

A página **[!UICONTROL Conectar Zoho CRM account]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL Zoho CRM] com a qual deseja criar um novo fluxo de dados e clique em **[!UICONTROL Avançar]** para continuar.

![existente](../../../../images/tutorials/create/zoho/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais do [!DNL Zoho CRM]. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

>[!TIP]
>
>O domínio da URL das contas deve corresponder ao local de domínio apropriado. A seguir estão os vários domínios e suas URLs de contas correspondentes:<ul><li>Estados Unidos: https://accounts.zoho.com</li><li>Austrália: https://accounts.zoho.com.au</li><li>Europa: https://accounts.zoho.eu</li><li>Índia: https://accounts.zoho.in</li><li>China: https://accounts.zoho.com.cn</li></ul>

![novo](../../../../images/tutorials/create/zoho/new.png)

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL Zoho CRM]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Experience Platform](../../dataflow/crm.md).
