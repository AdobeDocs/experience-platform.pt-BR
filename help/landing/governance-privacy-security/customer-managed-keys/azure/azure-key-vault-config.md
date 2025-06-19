---
title: Configurar um Cofre de Chaves do Azure para Chaves Gerenciadas pelo Cliente
description: Saiba como criar uma nova conta corporativa com o Azure ou usar uma conta corporativa existente e criar o Cofre da Chave.
role: Developer
feature: Privacy
exl-id: 670e3ca3-a833-4b28-9ad4-73685fa5d74d
source-git-commit: c920f78363ee5f040964dbd3a0d0815474094b07
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Configurar um Cofre de Chaves [!DNL Azure] para Chaves Gerenciadas pelo Cliente

Chaves CMK (Customer Managed Keys) com suporte de [!DNL Microsoft Azure] Cofres de Chaves e AWS [!DNL Key Management Service (KMS)]. Se sua implementação estiver hospedada em [!DNL Azure], siga as etapas abaixo para criar um Cofre da Chave. Para implementações hospedadas pela AWS, consulte o [guia de configuração do AWS KMS](../aws/configure-kms.md).

>[!IMPORTANT]
>
>Somente os níveis de HSM Standard, Premium e Gerenciado para o Cofre de Chaves do [!DNL Azure] são compatíveis. Não há suporte para [!DNL Azure Dedicated HSM] e [!DNL Azure Payments HSM]. Consulte a [[!DNL Azure] documentação](https://learn.microsoft.com/en-us/azure/security/fundamentals/key-management#azure-key-management-services) para obter mais informações sobre os serviços de gerenciamento de chaves oferecidos.

>[!NOTE]
>
>A documentação abaixo cobre apenas as etapas básicas para criar o Cofre da Chave. Fora dessa orientação, você deve configurar o Cofre da Chave de acordo com as políticas da organização.

Faça logon no portal [!DNL Azure] e use a barra de pesquisa para localizar **[!DNL Key vaults]** na lista de serviços.

![O recurso de pesquisa em [!DNL Microsoft Azure] com [!DNL Key vaults] foi realçado nos resultados da pesquisa.](../../../images/governance-privacy-security/customer-managed-keys/access-key-vaults.png)

A página **[!DNL Key vaults]** é exibida após a seleção do serviço. Aqui, selecione **[!DNL Create]**.

![O painel [!DNL Key vaults] em [!DNL Microsoft Azure] com [!DNL Create] realçado.](../../../images/governance-privacy-security/customer-managed-keys/create-key-vault.png)

Usando o formulário fornecido, preencha os detalhes básicos do Cofre da Chave, incluindo um nome e um grupo de recursos atribuído.

>[!WARNING]
>
>Embora a maioria das opções possa ser deixada como seus valores padrão, **habilite as opções de proteção de exclusão reversível e limpeza**. Se você não ativar esses recursos, poderá correr o risco de perder o acesso aos seus dados se o Cofre da Chave for excluído.
>
>![O fluxo de trabalho [!DNL Microsoft Azure] [!DNL Create a Key Vault] com exclusão reversível e proteção contra limpeza foi realçado.](../../../images/governance-privacy-security/customer-managed-keys/basic-config.png)

A partir daqui, continue percorrendo o fluxo de trabalho de criação do Cofre de Chaves e configure as diferentes opções de acordo com as políticas da sua organização.

Depois de chegar à etapa **[!DNL Review + create]**, você pode revisar os detalhes do Cofre da Chave enquanto ele passa pela validação. Depois que a validação for aprovada, selecione **[!DNL Create]** para concluir o processo.

![A página Revisar e criar cofres de Chave do Microsoft Azure com Criar realçada.](../../../images/governance-privacy-security/customer-managed-keys/finish-creation.png)

## Configurar acesso {#configure-access}

Em seguida, habilite o controle de acesso baseado em função do Azure para seu cofre de chaves. Selecione **[!DNL Access configuration]** na seção [!DNL Settings] da navegação à esquerda e **[!DNL Azure role-based access control]** para habilitar a configuração. Essa etapa é essencial, pois o aplicativo CMK deve ser associado posteriormente a uma função do Azure. A atribuição de uma função está documentada nos fluxos de trabalho [API](./api-set-up.md#assign-to-role) e [IU](./ui-set-up.md#assign-to-role).

![O painel [!DNL Microsoft Azure] com [!DNL Access configuration] e [!DNL Azure role-based access control] realçados.](../../../images/governance-privacy-security/customer-managed-keys/access-configuration.png)

## Configurar opções de rede {#configure-network-options}

Se o Cofre da Chave estiver configurado para restringir o acesso público a determinadas redes virtuais ou desabilitar totalmente o acesso público, você deve conceder a [!DNL Microsoft] uma exceção de firewall.

Selecione **[!DNL Networking]** na navegação à esquerda. Em **[!DNL Firewalls and virtual networks]**, marque a caixa de seleção **[!DNL Allow trusted Microsoft services to bypass this firewall]** e selecione **[!DNL Apply]**.

>[!NOTE]
>
>Se o cofre de chaves usa acesso restrito à rede, a Adobe recomenda adicionar o seguinte endereço IP estático: `20.88.123.53`. A adição desse endereço IP permite que os serviços da Adobe monitorem a conectividade com mais eficiência e forneçam alertas na plataforma quando problemas de acesso forem detectados.
>
>Para saber mais sobre quando incluir na lista de permissões o endereço IP da Adobe, como os alertas funcionam e como responder às principais notificações de falha de acesso, consulte [Configurar Alertas e Acesso IP para Azure CMK](./alerts-and-ip-access.md).
>
>Se o cofre de chaves já estiver configurado para permitir o acesso à rede pública, nenhuma outra ação será necessária.

![A guia [!DNL Networking] de [!DNL Microsoft Azure] com [!DNL Networking] e [!DNL Allow trusted Microsoft surfaces to bypass this firewall] exceção realçada.](../../../images/governance-privacy-security/customer-managed-keys/networking.png)

### Gerar uma chave {#generate-a-key}

Depois de criar um Cofre de Chaves, você pode gerar uma nova chave. Navegue até a guia **[!DNL Keys]** e selecione **[!DNL Generate/Import]**.

![A guia [!DNL Keys] de [!DNL Azure] com [!DNL Generate import] realçada.](../../../images/governance-privacy-security/customer-managed-keys/view-keys.png)

Use o formulário fornecido para fornecer um nome para a chave e selecione **RSA** ou **RSA-HSM** para o tipo de chave. Para implementações hospedadas por [!DNL Azure], o **[!DNL RSA key size]** deve ter pelo menos **3072** bits, conforme necessário para [!DNL Azure Cosmos DB]. [!DNL Azure Data Lake Storage] também é compatível com RSA 3027.

>[!NOTE]
>
>Lembre-se do nome fornecido para a chave, pois ele é necessário para enviá-la à Adobe.

Use os controles restantes para configurar a chave que deseja gerar ou importar conforme desejado. Quando terminar, selecione **[!DNL Create]**.

![O painel [!DNL Create a key] com [!DNL 3072] bits realçados.](../../../images/governance-privacy-security/customer-managed-keys/configure-key.png)

A chave configurada é exibida na lista de chaves do Vault.

![O espaço de trabalho [!DNL Keys] com o nome da chave realçado.](../../../images/governance-privacy-security/customer-managed-keys/key-added.png)

## Próximas etapas

Para continuar o processo único de configuração do recurso Chaves gerenciadas pelo cliente, siga os guias de configuração para o ambiente de hospedagem da sua plataforma:

- Para [!DNL Azure], use os guias de instalação da [API](./api-set-up.md) ou da [IU](./ui-set-up.md).
- Para o AWS, consulte o [guia de configuração do KMS do AWS](../aws/configure-kms.md) e o [guia de configuração da interface do usuário](../aws/ui-set-up.md).
