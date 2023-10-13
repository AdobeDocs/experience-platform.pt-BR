---
title: Configurar um Cofre de Chaves do Azure
description: Saiba como criar uma nova conta corporativa com o Azure ou usar uma conta corporativa existente e criar o Cofre da Chave.
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: 4ec87482c5a38404217ecd910b6a27ee2d0e00eb
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%

---

# Configurar um [!DNL Azure] Cofre da Chave

As chaves gerenciadas pelo cliente (CMK) só aceitam chaves de um [!DNL Microsoft Azure] Cofre da Chave. Para começar, você deve trabalhar com o [!DNL Azure] para criar uma nova conta corporativa ou usar uma conta corporativa existente, siga as etapas abaixo para criar o Cofre da Chave.

>[!IMPORTANT]
>
>Somente os níveis de serviço Premium e Standard para [!DNL Azure] O Cofre de Chaves é compatível. [!DNL Azure Managed HSM], [!DNL Azure Dedicated HSM] e [!DNL Azure Payments HSM] não são compatíveis. Consulte a [[!DNL Azure] documentação](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) para obter mais informações sobre os principais serviços de gerenciamento oferecidos.

>[!NOTE]
>
>A documentação abaixo cobre apenas as etapas básicas para criar o Cofre da Chave. Fora dessa orientação, você deve configurar o Cofre da Chave de acordo com as políticas da organização.

Faça logon no [!DNL Azure] portal e use a barra de pesquisa para localizar **[!DNL Key vaults]** na lista de serviços.

![O recurso de pesquisa no [!DNL Microsoft Azure] com [!DNL Key vaults] destacado nos resultados da pesquisa.](../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

A variável **[!DNL Key vaults]** será exibida após selecionar o serviço. Aqui, selecione **[!DNL Create]**.

![A variável [!DNL Key vaults] painel em [!DNL Microsoft Azure] com [!DNL Create] destacado.](../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Usando o formulário fornecido, preencha os detalhes básicos do Cofre da Chave, incluindo um nome e um grupo de recursos atribuído.

>[!WARNING]
>
>Embora a maioria das opções possa ser deixada como seus valores padrão, **certifique-se de ativar as opções de exclusão reversível e de proteção de limpeza**. Se você não ativar esses recursos, poderá correr o risco de perder o acesso aos seus dados se o Cofre da Chave for excluído.
>
>![A variável [!DNL Microsoft Azure] [!DNL Create a Key Vault] fluxo de trabalho com proteção de exclusão reversível e limpeza realçada.](../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

A partir daqui, continue percorrendo o fluxo de trabalho de criação do Cofre de Chaves e configure as diferentes opções de acordo com as políticas da sua organização.

Uma vez que você chegar ao **[!DNL Review + create]** etapa, você pode revisar os detalhes do Cofre da Chave enquanto ele passa pela validação. Depois que a validação for aprovada, selecione **[!DNL Create]** para concluir o processo.

![A página Verificar e criar cofres de chave do Microsoft Azure com Criar realçada.](../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Configurar acesso {#configure-access}

Em seguida, habilite o controle de acesso baseado em função do Azure para seu cofre de chaves. Selecionar **[!DNL Access configuration]** no [!DNL Settings] da navegação à esquerda, selecione **[!DNL Azure role-based access control]** para ativar a configuração. Essa etapa é essencial, pois o aplicativo CMK deve ser associado posteriormente a uma função do Azure. A atribuição de uma função está documentada no [API](./api-set-up.md#assign-to-role) e [IU](./ui-set-up.md#assign-to-role) fluxos de trabalho.

![A variável [!DNL Microsoft Azure] painel com [!DNL Access configuration] e [!DNL Azure role-based access control] destacado.](../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Configurar opções de rede {#configure-network-options}

Se o Cofre da Chave estiver configurado para restringir o acesso público a determinadas redes virtuais ou desabilitar completamente o acesso público, você deverá conceder [!DNL Microsoft] uma exceção de firewall.

Selecionar **[!DNL Networking]** no painel de navegação esquerdo. Em **[!DNL Firewalls and virtual networks]**, marque a caixa de seleção **[!DNL Allow trusted Microsoft services to bypass this firewall]** e selecione **[!DNL Apply]**.

![A variável [!DNL Networking] guia de [!DNL Microsoft Azure] com [!DNL Networking] e [!DNL Allow trusted Microsoft surfaces to bypass this firewall] exceção destacada.](../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Gerar uma chave {#generate-a-key}

Depois de criar um Cofre de Chaves, você pode gerar uma nova chave. Navegue até a **[!DNL Keys]** e selecione **[!DNL Generate/Import]**.

![A variável [!DNL Keys] guia de [!DNL Azure] com [!DNL Generate import] destacado.](../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Use o formulário fornecido para fornecer um nome para a chave e selecione **RSA** para o tipo de chave. No mínimo, a variável **[!DNL RSA key size]** deve ser pelo menos **3072** bits conforme exigido pelo [!DNL Cosmos DB]. [!DNL Azure Data Lake Storage] também é compatível com o RSA 3027.

>[!NOTE]
>
>Lembre-se do nome fornecido para a chave, pois ele é necessário para enviar a chave ao Adobe.

Use os controles restantes para configurar a chave que deseja gerar ou importar conforme desejado. Quando terminar, selecione **[!DNL Create]**.

![A janela Criar um painel de chaves com [!DNL 3072] bits realçados.](../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

A chave configurada é exibida na lista de chaves do Vault.

![A variável [!DNL Keys] espaço de trabalho com o nome da chave realçado.](../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Próximas etapas

Para continuar o processo único de configuração do recurso de chaves gerenciadas pelo cliente, continue com o [API](./api-set-up.md) ou [IU](./ui-set-up.md) guias de configuração de chaves gerenciadas pelo cliente.
