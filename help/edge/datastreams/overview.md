---
title: Visão geral dos conjuntos de dados
description: Conecte sua integração do SDK da Experience Platform do lado do cliente aos produtos da Adobe e destinos de terceiros.
keywords: configuração; datastreams; datastreamId; edge; datastream id; Configurações do ambiente; edgeConfigId; identidade; sincronização de id ativada; ID do contêiner de sincronização de ID; Sandbox; Streaming Inlet; Conjunto de dados de eventos; target; código do cliente; ID do ambiente do Target; Destinos de cookies; Destinos de url; ID do conjunto de relatórios de configurações do Analytics; Predefinição de dados para dados Coleção; Preparação de dados; Mapeador; Mapeador XDM; Mapeador no Edge;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 2cec87d3f45b1b774925a9b669b53a958e65e57a
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 5%

---

# Visão geral dos conjuntos de dados

Uma sequência de dados representa a configuração do lado do servidor ao implementar os SDKs móveis e da Web da Adobe Experience Platform. Enquanto a variável [comando configurar](../fundamentals/configuring-the-sdk.md) no SDK controla os itens que devem ser manipulados no cliente (como `edgeDomain`), os conjuntos de dados lidam com todas as outras configurações do SDK. Quando uma solicitação é enviada para a rede de borda da Adobe Experience Platform, a variável `edgeConfigId` é usada para fazer referência ao armazenamento de dados. Isso permite atualizar a configuração do lado do servidor sem precisar fazer alterações de código no site.

Você pode criar e gerenciar conjuntos de dados selecionando **[!UICONTROL Datastreams]** na navegação à esquerda na interface do usuário do Adobe Experience Platform ou na interface do usuário da coleta de dados.

![Guia Datastreams na interface do usuário](../assets/datastreams/overview/datastreams-tab.png)

Para obter mais informações sobre como configurar um armazenamento de dados na interface do usuário, consulte o [guia de configuração](./configure.md).

## Tratamento de dados confidenciais em conjuntos de dados {#sensitive}

>[!IMPORTANT]
>
>O conteúdo deste documento não é um aconselhamento jurídico e não se destina a substituir tal aconselhamento. Consulte o departamento jurídico da sua empresa para obter aconselhamento sobre o tratamento de dados sensíveis.

As políticas corporativas de gerenciamento de dados e os requisitos normativos estão aumentando as restrições sobre como os dados confidenciais do cliente podem ser coletados, processados e usados. Isso inclui a coleta, o processamento e a utilização de Dados de Saúde Protegidos (PHI), que estão sujeitos a regulamentos como o Health Insurance Portability and Accountability Act (HIPAA).

Os Datastreams fornecem três métodos para ajudá-lo a lidar com seus dados confidenciais com segurança:

* [Criptografia aprimorada](#encryption)
* [Governança de dados](#governance)
* [Logs de auditoria](#audit-logs)

### Criptografia aprimorada {#encryption}

Todos os dados em trânsito pela Rede de Borda são conduzidos por conexões seguras e criptografadas usando [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Se o armazenamento de dados estiver trazendo dados para o Experience Platform, os dados serão criptografados em repouso no lago de dados do Experience Platform. Consulte o documento em [criptografia de dados no Experience Platform](../../landing/governance-privacy-security/encryption.md) para obter mais informações.

### Governança de dados {#governance}

Os Datastreams usam os recursos integrados de governança de dados do Experience Platform para impedir que dados confidenciais sejam enviados para serviços não prontos para HIPAA. Ao rotular campos específicos que contêm dados confidenciais em seus esquemas de conjunto de dados, é possível assumir um controle granular sobre quais campos de dados podem ser usados para fins específicos.

O vídeo a seguir fornece uma breve visão geral de como as restrições de uso de dados são configuradas e aplicadas em conjuntos de dados na interface do usuário:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

No Experience Platform, você pode aplicar [rótulos de uso de dados confidenciais](../../data-governance/labels/reference.md#sensitive) para esquemas e campos que contêm dados que sua organização considera confidenciais. Por exemplo, a variável `RHD` é usada para indicar Informações de Integridade Protegidas (PHI) e a variável `S1` representa dados de geolocalização.

>[!NOTE]
>
>Para obter detalhes sobre como aplicar rótulos de uso de dados no [!UICONTROL Esquemas] na interface do usuário do Experience Platform ou na interface do usuário da coleta de dados, consulte [tutorial de rotulagem de schema](../../xdm/tutorials/labels.md).

Ao criar um novo armazenamento de dados, se o esquema selecionado contiver rótulos de uso de dados confidenciais, o conjunto de dados só poderá ser configurado para enviar esses dados para destinos prontos para HIPAA. Atualmente, o único destino pronto para HIPAA compatível com datastreams é o Adobe Experience Platform. Outros serviços de destino, incluindo Adobe Target, Adobe Analytics, Adobe Audience Manager, encaminhamento de eventos e destinos de borda, são desativados para conjuntos de dados que contêm rótulos confidenciais de uso de dados.

Se um esquema estiver sendo usado em um armazenamento de dados existente com serviços não prontos para HIPAA, tentar adicionar um rótulo de uso de dados confidencial ao esquema resultará em uma mensagem de violação de política e a ação será impedida. A mensagem especifica qual datastream acionou a violação e sugere remover quaisquer serviços não prontos para HIPAA do datastream para resolver o problema.

### Logs de auditoria

No Experience Platform, as atividades de armazenamento de dados podem ser monitoradas na forma de logs de auditoria. Um log de auditoria informa **who** executado **what** e **when**, juntamente com outros dados contextuais que podem ajudá-lo a solucionar problemas relacionados a conjuntos de dados para ajudar sua empresa a cumprir as políticas corporativas de gerenciamento de dados e os requisitos normativos.

Sempre que um usuário cria, atualiza ou exclui um conjunto de dados, um log de auditoria é criado para registrar a ação. O mesmo ocorre sempre que um usuário cria, atualiza ou exclui um mapeamento por [Preparação de dados para coleta de dados](./data-prep.md). Independentemente de se tratar de um datastream ou de um mapeamento que foi atualizado, o log de auditoria resultante é categorizado na variável [!UICONTROL Datastreams] tipo de recurso.

Consulte a documentação em [logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md) para obter mais informações sobre como interpretar logs de conjuntos de dados e outros serviços compatíveis.

## Próximas etapas

Este guia forneceu uma visão geral de alto nível dos conjuntos de dados e seu uso na Coleta de dados e no processamento de dados confidenciais. Para obter etapas sobre como configurar um novo armazenamento de dados, consulte o [guia de configuração do datastream](./configure.md).
