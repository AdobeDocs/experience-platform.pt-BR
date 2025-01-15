---
title: Chaves gerenciadas pelo cliente no Adobe Experience Platform
description: Saiba como configurar suas próprias chaves de criptografia para dados armazenados no Adobe Experience Platform.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: c1a28a4b1ce066a87bb7b34b2524800f9d8f1ca0
workflow-type: tm+mt
source-wordcount: '1098'
ht-degree: 0%

---

# Chaves gerenciadas pelo cliente no Adobe Experience Platform

Os dados armazenados no Adobe Experience Platform são criptografados em repouso usando chaves de nível de sistema. Se você estiver usando um aplicativo criado sobre a Platform, poderá optar por usar suas próprias chaves de criptografia, fornecendo maior controle sobre a segurança dos dados.

>[!AVAILABILITY]
>
>A Adobe Experience Platform oferece suporte a Chaves gerenciadas pelo cliente (CMK) para Microsoft Azure e Amazon Web Services (AWS). O Experience Platform em execução no AWS está atualmente disponível para um número limitado de clientes. Se sua implementação for executada no AWS, você terá a opção de usar o Serviço de Gerenciamento de Chaves (KMS) para criptografia de dados da plataforma. Para obter mais informações sobre a infraestrutura com suporte, consulte a [visão geral de várias nuvens do Experience Platform](https://experienceleague.adobe.com/en/docs/experience-platform/landing/multi-cloud).
>
>Para saber mais sobre a criação e o gerenciamento de chaves de criptografia no AWS KMS, consulte o [Guia de criptografia de dados do AWS KMS](./aws/configure-kms.md). Para implementações do Azure, consulte o [guia de configuração do Cofre de Chaves do Azure](./azure/azure-key-vault-config.md).

>[!NOTE]
>
>Para instâncias da Plataforma hospedada [!DNL Azure], os dados de perfil do cliente armazenados no [!DNL Azure Data Lake] da Plataforma e no armazenamento de perfil do [!DNL Azure Cosmos DB] são criptografados exclusivamente usando CMK depois de habilitados. A revogação de chaves em armazenamentos de dados primários pode levar de **alguns minutos a 24 horas** e **até 7 dias** para armazenamentos de dados transitórios ou secundários. Para obter detalhes adicionais, consulte a [seção implicações da revogação do acesso à chave](#revoke-access).

Este documento fornece uma visão geral de alto nível do processo de habilitação do recurso de Chaves gerenciadas pelo cliente (CMK) na Platform no [!DNL Azure] e na AWS, juntamente com as informações de pré-requisitos necessárias para concluir essas etapas.

>[!NOTE]
>
>Para clientes do Customer Journey Analytics, siga as instruções na [documentação do Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=pt-BR).

## Pré-requisitos

Para habilitar o CMK, o ambiente de hospedagem da sua plataforma ([!DNL Azure] ou AWS) deve atender aos requisitos de configuração específicos:

### Pré-requisitos gerais

Para exibir e acessar a seção [!UICONTROL Criptografia] no Adobe Experience Platform, você deve ter criado uma função e atribuído a permissão [!UICONTROL Gerenciar Chave Gerenciada pelo Cliente] a essa função.  Qualquer usuário com a permissão [!UICONTROL Gerenciar Chave gerenciada pelo cliente] pode habilitar o CMK para sua organização.

Para obter mais informações sobre atribuição de funções e permissões no Experience Platform, consulte a [documentação sobre configuração de permissões](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

### Pré-requisitos específicos do Azure

Para implementações hospedadas pelo Azure, configure o Cofre de Chaves [!DNL Azure] com as seguintes configurações:

- [Habilitar proteção para limpeza](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
- [Habilitar exclusão reversível](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
- [Configurar acesso usando [!DNL Azure] controle de acesso baseado em função](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

### Pré-requisitos específicos do AWS

Para implementações hospedadas pela AWS, configure o ambiente do AWS da seguinte maneira:

- Verifique se você tem permissões para gerenciar chaves de criptografia usando o AWS Identity and Access Management (IAM). Para obter detalhes, consulte as [Políticas do IAM para o AWS KMS](https://docs.aws.amazon.com/kms/latest/developerguide/iam-policies.html).
- Configure o AWS KMS com suporte para CMK. Consulte o [guia de criptografia de dados do AWS KMS](./aws/configure-kms.md).

## Resumo do processo {#process-summary}

O Customer Managed Keys (CMK) está disponível por meio das ofertas Adobe Healthcare Shield e Privacy and Security Shield. No Azure, o CMK é compatível com o Healthcare Shield e o Privacy and Security Shield. No AWS, o CMK é compatível apenas com o Privacy and Security Shield e não está disponível para o Healthcare Shield. Assim que sua organização comprar uma licença para uma dessas ofertas, você poderá iniciar o processo de configuração único para ativar o CMK.

>[!WARNING]
>
>Após configurar o CMK, não é possível reverter para chaves gerenciadas pelo sistema. Você é responsável por gerenciar com segurança as chaves para evitar a perda de acesso aos dados.

O processo é o seguinte:

### Para o Azure {#azure-process-summary}

1. [Configure um [!DNL Azure] Cofre de Chaves](./azure/azure-key-vault-config.md) com base nas políticas da sua organização e [gere uma chave de criptografia](./azure/azure-key-vault-config.md#generate-a-key) para compartilhar com o Adobe.
1. Configure o aplicativo CMK com seu locatário [!DNL Azure] por meio de [chamadas de API](./azure/api-set-up.md#register-app) ou da [interface](./azure/ui-set-up.md#register-app).
1. Envie sua ID de chave de criptografia para o Adobe e inicie o processo de habilitação do recurso, [na interface](./azure/ui-set-up.md#send-to-adobe) ou com uma [chamada de API](./azure/api-set-up.md#send-to-adobe).
1. Verifique o status da configuração para verificar se o CMK foi habilitado, [na interface](./azure/ui-set-up.md#check-status) ou com uma [chamada de API](./azure/api-set-up.md#check-status).

Quando o processo de configuração for concluído para instâncias da Plataforma hospedada pelo Azure, todos os dados integrados na Plataforma em todas as sandboxes serão criptografados usando a configuração de chave [!DNL Azure]. Para usar o CMK, você aproveitará a funcionalidade [!DNL Microsoft Azure] que pode fazer parte do [programa de visualização pública](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

### Para AWS {#aws-process-summary}

1. [Configure o AWS KMS](./aws/configure-kms.md) configurando uma chave de criptografia para ser compartilhada com o Adobe.
2. Siga as instruções específicas do AWS no [guia de configuração da interface](./aws/ui-set-up.md).
3. Valide a configuração para confirmar se os dados da Platform estão criptografados usando a chave hospedada pela AWS.

<!--  Pending: or [API setup guide]() -->

Quando o processo de configuração das instâncias da plataforma hospedada pela AWS for concluído, todos os dados integrados na plataforma em todas as sandboxes serão criptografados usando a configuração do serviço de gerenciamento de chaves (KMS) da AWS. Para usar o CMK no AWS, você usará o Serviço de gerenciamento de chaves da AWS para criar e gerenciar as chaves de criptografia de acordo com os requisitos de segurança da sua organização.

## Implicações da revogação do acesso à chave {#revoke-access}

Revogar ou desabilitar o acesso ao Cofre de Chaves, chave ou aplicativo CMK no Azure ou à chave de criptografia no AWS pode resultar em interrupções significativas, que incluem alterações irrelevantes nas operações da sua plataforma. Depois que as chaves forem desativadas, os dados na Platform poderão ficar inacessíveis e qualquer operação downstream que depende desses dados deixará de funcionar. É fundamental entender totalmente os impactos downstream antes de fazer qualquer alteração nas principais configurações.

Para revogar o acesso da Platform aos seus dados no [!DNL Azure], remova a função de usuário associada ao aplicativo do Cofre de Chaves. Para o AWS, você pode desativar a chave ou atualizar a declaração de política. Para obter instruções detalhadas sobre o processo AWS, consulte a [seção de revogação de chaves](./aws/ui-set-up.md#key-revocation).


### Linhas do tempo de propagação {#propagation-timelines}

Depois que o acesso à chave for revogado do Cofre de Chaves do [!DNL Azure], as alterações serão propagadas da seguinte maneira:

| **Tipo de armazenamento** | **Descrição** | **Linha do tempo** |
|---|---|---|
| Armazenamentos de dados principais | Inclui armazenamentos de Data Lake (Azure Data Lake, AWS S3) e Perfil do Azure Cosmos DB. Quando o acesso à chave é revogado, os dados ficam inacessíveis. | De **alguns minutos a 24 horas**. |
| Armazenamento de dados em cache/transitório | Inclui armazenamentos de dados secundários usados para desempenho e funcionalidade de aplicativos principais. O impacto da revogação de chave está atrasado. | **Até 7 dias**. |

Por exemplo, o painel Perfil continuará exibindo dados de seu cache por até sete dias antes de os dados expirarem e serem atualizados. Da mesma forma, a reativação do acesso ao aplicativo leva o mesmo tempo para restaurar a disponibilidade dos dados nesses armazenamentos.

>[!NOTE]
>
>A reativação do acesso ao aplicativo pode levar o mesmo tempo que a revogação para restaurar a disponibilidade dos dados nesses armazenamentos.

>[!TIP]
>
>Há duas exceções específicas de caso de uso para a expiração do conjunto de dados de sete dias em dados não primários (em cache/transitórios). Consulte a respectiva documentação para obter mais informações sobre esses recursos.<ul><li>[Encurtador de URL do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=pt-BR#message-preset-sms)</li><li>[Projeções do Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Próximas etapas

Para iniciar o processo:

- Para o Azure: comece [configurando um [!DNL Azure] Cofre de Chaves](./azure/azure-key-vault-config.md) e [gerando uma chave de criptografia](./azure/azure-key-vault-config.md#generate-a-key) para compartilhar com o Adobe.
- Para o AWS: [Configure o AWS KMS](./aws/configure-kms.md) e garanta as configurações apropriadas do IAM e do KMS antes de prosseguir para os guias de configuração da interface ou da API.
