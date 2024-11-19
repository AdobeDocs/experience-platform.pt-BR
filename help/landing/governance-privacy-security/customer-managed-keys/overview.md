---
title: Chaves gerenciadas pelo cliente no Adobe Experience Platform
description: Saiba como configurar suas próprias chaves de criptografia para dados armazenados no Adobe Experience Platform.
role: Developer
feature: Privacy
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: c0eb5b5c3a1968cae2bc19b7669f70a97379239b
workflow-type: tm+mt
source-wordcount: '752'
ht-degree: 0%

---

# Chaves gerenciadas pelo cliente no Adobe Experience Platform

Os dados armazenados no Adobe Experience Platform são criptografados em repouso usando chaves de nível de sistema. Se você estiver usando um aplicativo criado sobre a Platform, poderá optar por usar suas próprias chaves de criptografia, fornecendo maior controle sobre a segurança dos dados.

>[!NOTE]
>
>Os dados do perfil do cliente armazenados no [!DNL Azure Data Lake] da plataforma e no armazenamento de perfil do [!DNL Azure Cosmos DB] são criptografados exclusivamente usando CMK, uma vez habilitados. A revogação de chaves em seus armazenamentos de dados primários pode levar de **alguns minutos a 24 horas**, e pode demorar mais, **até 7 dias** para armazenamentos de dados transitórios ou secundários. Para obter detalhes adicionais, consulte a [seção implicações da revogação do acesso à chave](#revoke-access).

Este documento fornece uma visão geral de alto nível do processo de ativação do recurso de chaves gerenciadas pelo cliente (CMK) na Platform e as informações de pré-requisitos necessárias para concluir essas etapas.

>[!NOTE]
>
>Para clientes do Customer Journey Analytics, siga as instruções na [documentação do Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=pt-BR).

## Pré-requisitos

Para exibir e visitar a seção [!UICONTROL Criptografia] no Adobe Experience Platform, você deve ter criado uma função e atribuído a permissão [!UICONTROL Gerenciar chave gerenciada pelo cliente] a essa função. Qualquer usuário com a permissão [!UICONTROL Gerenciar Chave gerenciada pelo cliente] pode habilitar o CMK para sua organização.

Para obter mais informações sobre atribuição de funções e permissões no Experience Platform, consulte a [documentação sobre configuração de permissões](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Para habilitar o CMK, o Cofre de Chaves do [!DNL Azure] deve ser configurado com as seguintes configurações:

* [Habilitar proteção para limpeza](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Habilitar exclusão reversível](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configurar acesso usando [!DNL Azure] controle de acesso baseado em função](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Leia a documentação vinculada para entender melhor o processo.

## Resumo do processo {#process-summary}

A CMK está incluída nas ofertas Healthcare Shield e Privacy and Security Shield da Adobe. Depois que sua organização comprar uma licença para uma dessas ofertas, você poderá iniciar um processo único para configurar o recurso.

>[!WARNING]
>
>Após configurar o CMK, não é possível reverter para chaves gerenciadas pelo sistema. Você é responsável por gerenciar com segurança suas chaves e fornecer acesso ao Cofre da Chave, Chave e aplicativo CMK no [!DNL Azure] para evitar a perda de acesso aos seus dados.

O processo é o seguinte:

1. [Configure um [!DNL Azure] Cofre de Chaves](./azure-key-vault-config.md) com base nas políticas da sua organização e [gere uma chave de criptografia](./azure-key-vault-config.md#generate-a-key) que será compartilhada com o Adobe.
1. Configure o aplicativo CMK com seu locatário [!DNL Azure] por meio de [chamadas de API](./api-set-up.md#register-app) ou da [interface](./ui-set-up.md#register-app).
1. Envie sua ID de chave de criptografia para o Adobe e inicie o processo de habilitação do recurso [na interface](./ui-set-up.md#send-to-adobe) ou com uma [chamada de API](./api-set-up.md#send-to-adobe).
1. Verifique o status da configuração para verificar se o CMK foi habilitado [na interface](./ui-set-up.md#check-status) ou com uma [chamada de API](./api-set-up.md#check-status).

Quando o processo de configuração estiver concluído, todos os dados integrados na Platform em todas as sandboxes serão criptografados usando a configuração de chave do [!DNL Azure]. Para usar o CMK, você aproveitará a funcionalidade [!DNL Microsoft Azure] que pode fazer parte do [programa de visualização pública](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## Implicações da revogação do acesso à chave {#revoke-access}

Revogar ou desabilitar o acesso ao Cofre da chave, chave ou aplicativo CMK pode resultar em interrupções significativas, que incluem alterações nas operações da sua plataforma. Depois que essas chaves forem desativadas, os dados na Platform poderão se tornar inacessíveis e qualquer operação downstream que depende desses dados deixará de funcionar. É fundamental entender totalmente os impactos downstream antes de fazer qualquer alteração nas principais configurações.

Se você decidir revogar o acesso da Platform aos seus dados, poderá fazê-lo removendo a função de usuário associada ao aplicativo do Cofre de Chaves no [!DNL Azure].

### Linhas do tempo de propagação {#propagation-timelines}

Depois que o acesso à chave for revogado do Cofre de Chaves do [!DNL Azure], as alterações serão propagadas da seguinte maneira:

| **Tipo de armazenamento** | **Descrição** | **Linha do tempo** |
|---|---|---|
| Armazenamentos de dados principais | Esses armazenamentos incluem os armazenamentos Azure Data Lake e Azure Cosmos DB Profile. Quando o acesso à chave é revogado, os dados ficam inacessíveis. | De **alguns minutos a 24 horas**. |
| Armazenamento de dados em cache/transitório | Inclui armazenamentos de dados usados para desempenho e funcionalidade de aplicativos principais. O impacto da revogação de chave está atrasado. | **Até 7 dias**. |

Por exemplo, o painel Perfil continuará exibindo dados de seu cache por até sete dias antes de os dados expirarem e serem atualizados. Da mesma forma, a reativação do acesso ao aplicativo leva o mesmo tempo para restaurar a disponibilidade dos dados nesses armazenamentos.

>[!NOTE]
>
>Há duas exceções específicas de caso de uso para a expiração do conjunto de dados de sete dias em dados não primários (em cache/transitórios). Consulte a respectiva documentação para obter mais informações sobre esses recursos.<ul><li>[Encurtador de URL do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html?lang=pt-BR#message-preset-sms)</li><li>[Projeções do Edge](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Próximas etapas

Para iniciar o processo, comece [configurando um [!DNL Azure] Cofre de Chaves](./azure-key-vault-config.md) e [gerando uma chave de criptografia](./azure-key-vault-config.md#generate-a-key) para compartilhar com o Adobe.
