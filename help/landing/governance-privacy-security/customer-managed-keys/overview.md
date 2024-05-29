---
title: Chaves gerenciadas pelo cliente no Adobe Experience Platform
description: Saiba como configurar suas próprias chaves de criptografia para dados armazenados no Adobe Experience Platform.
exl-id: cd33e6c2-8189-4b68-a99b-ec7fccdc9b91
source-git-commit: e52eb90b64ae9142e714a46017cfd14156c78f8b
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 0%

---

# Chaves gerenciadas pelo cliente no Adobe Experience Platform

Os dados armazenados no Adobe Experience Platform são criptografados em repouso usando chaves de nível de sistema. Se você estiver usando um aplicativo criado sobre a Platform, poderá optar por usar suas próprias chaves de criptografia, fornecendo maior controle sobre a segurança dos dados.

>[!NOTE]
>
>Os dados no data lake e no armazenamento de perfis da Adobe Experience Platform são criptografados usando CMK. Eles são considerados seus principais armazenamentos de dados.

Este documento fornece uma visão geral de alto nível do processo de ativação do recurso de chaves gerenciadas pelo cliente (CMK) na Platform e as informações de pré-requisitos necessárias para concluir essas etapas.

>[!NOTE]
>
>Para clientes do Customer Journey Analytics, siga as instruções no [Documentação do Customer Journey Analytics](https://experienceleague.adobe.com/docs/analytics-platform/using/cja-privacy/cmk.html?lang=pt-BR).

## Pré-requisitos

Para visualizar e visitar o [!UICONTROL Criptografia] no Adobe Experience Platform, você deve ter criado uma função e atribuído a [!UICONTROL Gerenciar Chave Gerenciada Pelo Cliente] permissão para essa função. Qualquer usuário que tenha o [!UICONTROL Gerenciar Chave Gerenciada Pelo Cliente] permissão pode habilitar o CMK para sua organização.

Para obter mais informações sobre atribuição de funções e permissões no Experience Platform, consulte o [configurar documentação de permissões](https://experienceleague.adobe.com/docs/platform-learn/getting-started-for-data-architects-and-data-engineers/configure-permissions.html).

Para habilitar o CMK, seu [!DNL Azure] O Cofre da Chave deve ser configurado com as seguintes configurações:

* [Habilitar proteção contra limpeza](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview#purge-protection)
* [Habilitar exclusão reversível](https://learn.microsoft.com/en-us/azure/key-vault/general/soft-delete-overview)
* [Configure o acesso usando [!DNL Azure] controle de acesso baseado em função](https://learn.microsoft.com/en-us/azure/role-based-access-control/)

Leia a documentação vinculada para entender melhor o processo.

## Resumo do processo {#process-summary}

A CMK está incluída nas ofertas Healthcare Shield e Privacy and Security Shield da Adobe. Depois que sua organização comprar uma licença para uma dessas ofertas, você poderá iniciar um processo único para configurar o recurso.

>[!WARNING]
>
>Após configurar o CMK, não é possível reverter para chaves gerenciadas pelo sistema. Você é responsável por gerenciar com segurança suas chaves e fornecer acesso ao Cofre da chave, Chave e aplicativo CMK no [!DNL Azure] para evitar a perda de acesso aos seus dados.

O processo é o seguinte:

1. [Configurar um [!DNL Azure] Cofre da Chave](./azure-key-vault-config.md) com base nas políticas de sua organização, em seguida [gerar uma chave de criptografia](./azure-key-vault-config.md#generate-a-key) que será compartilhado com o Adobe.
1. Configure o aplicativo CMK com seu [!DNL Azure] inquilino por meio de [Chamadas de API](./api-set-up.md#register-app) ou o [IU](./ui-set-up.md#register-app).
1. Envie sua ID de chave de criptografia para o Adobe e inicie o processo de ativação do recurso [na interface](./ui-set-up.md#send-to-adobe) ou com um [Chamada de API](./api-set-up.md#send-to-adobe).
1. Verifique o status da configuração para verificar se o CMK foi ativado [na interface](./ui-set-up.md#check-status) ou com um [Chamada de API](./api-set-up.md#check-status).

Quando o processo de configuração estiver concluído, todos os dados integrados na Platform em todas as sandboxes serão criptografados usando o [!DNL Azure] configuração de chave. Para usar CMK, você aproveitará [!DNL Microsoft Azure] funcionalidade que pode fazer parte do seu [programa de visualização pública](https://azure.microsoft.com/en-ca/support/legal/preview-supplemental-terms/).

## Revogar acesso {#revoke-access}

Se quiser revogar o acesso do Platform aos seus dados, você poderá remover a função de usuário associada à aplicação do cofre de chaves no [!DNL Azure].

>[!WARNING]
>
>Desabilitar o cofre de chaves, a Chave ou o aplicativo CMK pode resultar em uma mudança radical. Quando o cofre de chaves, a chave ou o aplicativo CMK estiverem desativados e os dados não estiverem mais acessíveis na Platform, nenhuma operação downstream relacionada a esses dados será mais possível. Certifique-se de entender os impactos de downstream da revogação do acesso da Platform à sua chave antes de fazer alterações na configuração.

Após remover o acesso à chave ou desabilitar/excluir a chave do [!DNL Azure] cofre de chaves, pode levar de alguns minutos a 24 horas para que essa configuração se propague para os armazenamentos de dados principais. Os fluxos de trabalho da plataforma também incluem armazenamentos de dados em cache e transitórios, necessários para o desempenho e a funcionalidade principal do aplicativo. A propagação da revogação de CMK por meio desses armazenamentos em cache e transitórios pode levar até sete dias, conforme determinado por seus workflows de processamento de dados. Por exemplo, isso significa que o painel Perfil manteria e exibiria dados de seu armazenamento de dados em cache e levaria sete dias para expirar os dados mantidos nos armazenamentos de dados em cache como parte do ciclo de atualização. O mesmo atraso se aplica para que os dados fiquem disponíveis novamente ao reativar o acesso ao aplicativo.

>[!NOTE]
>
>Há duas exceções específicas de caso de uso para a expiração do conjunto de dados de sete dias em dados não primários (em cache/transitórios). Consulte a respectiva documentação para obter mais informações sobre esses recursos.<ul><li>[Encurtador de URL do Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/sms/sms-configuration.html#message-preset-sms)</li><li>[Projeções de borda](https://experienceleague.adobe.com/docs/experience-platform/profile/home.html#edge-projections)</li></ul>

## Próximas etapas

Para iniciar o processo, comece em [configurar um [!DNL Azure] Cofre da Chave](./azure-key-vault-config.md) e [gerar uma chave de criptografia](./azure-key-vault-config.md#generate-a-key) para compartilhar com o Adobe.
