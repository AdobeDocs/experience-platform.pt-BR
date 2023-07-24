---
title: Visão geral dos fluxos de dados
description: Conecte sua integração do SDK da Experience Platform do lado do cliente aos produtos da Adobe e destinos de terceiros.
keywords: configuração;datastreams;datastreamId;borda;datastream id;Configurações de ambiente;edgeConfigId;identidade;id de sincronização habilitada;ID de sincronização de contêiner;Sandbox;Entrada de streaming;Conjunto de dados de evento;destino;código do cliente;Token de propriedade;ID de ambiente de destino;Cookie Destinos;url Destinos;Configurações do Analytics ID do conjunto de relatórios de bloco;Preparação de dados para coleção de dados;Preparador de dados;Mapeador;Mapeador XDM;Mapeador na borda;
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 5f2358c2e102c66a13746004ad73e2766e933705
workflow-type: tm+mt
source-wordcount: '780'
ht-degree: 5%

---


# Visão geral dos fluxos de dados

Uma sequência de dados representa a configuração do lado do servidor ao implementar os SDKs móveis e da Web da Adobe Experience Platform. Embora a [comando configure](../edge/fundamentals/configuring-the-sdk.md) no SDK controla itens que devem ser manipulados no cliente (como o `edgeDomain`), os fluxos de dados lidam com todas as outras configurações para o SDK. Quando uma solicitação é enviada para a Rede de borda da Adobe Experience Platform, a variável `edgeConfigId` é usado para fazer referência ao fluxo de dados. Isso permite atualizar a configuração do lado do servidor sem precisar fazer alterações de código no site.

Você pode criar e gerenciar fluxos de dados selecionando **[!UICONTROL Datastreams]** na navegação à esquerda na interface do usuário do Adobe Experience Platform ou na interface da Coleção de dados.

![Guia Fluxos de dados na interface](assets/overview/datastreams-tab.png)

Para obter mais informações sobre como configurar um fluxo de dados na interface, consulte a [guia de configuração](./configure.md).

## Manipulação de dados sigilosos em sequências de dados {#sensitive}

>[!IMPORTANT]
>
>O conteúdo deste documento não é um aconselhamento jurídico e não se destina a substituir tal aconselhamento. Consulte o departamento jurídico da sua empresa para obter aconselhamento sobre o tratamento de dados confidenciais.

As políticas de gerenciamento de dados corporativos e os requisitos normativos estão aumentando as restrições sobre como os dados confidenciais do cliente podem ser coletados, processados e usados. Isso inclui a coleta, o processamento e o uso de PHI (Protected Health Data, dados protegidos de saúde), que estão sujeitos a regulamentos como a HIPAA (Health Insurance Portability and Accountability Act, lei de responsabilidade e mobilidade de seguros de saúde).

As sequências de dados fornecem três métodos para ajudá-lo a lidar com os dados confidenciais com segurança:

* [Criptografia aprimorada](#encryption)
* [Governança de dados](#governance)
* [Logs de auditoria](#audit-logs)

### Criptografia aprimorada {#encryption}

Todos os dados em trânsito pela rede de borda são conduzidos por conexões seguras e criptografadas usando [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Se a sequência de dados estiver trazendo dados para o Experience Platform, os dados serão criptografados em repouso no data lake de Experience Platform. Consulte o documento sobre [criptografia de dados no Experience Platform](../landing/governance-privacy-security/encryption.md) para obter mais informações.

### Governança de dados {#governance}

As sequências de dados usam os recursos de governança de dados integrados do Experience Platform para impedir que dados confidenciais sejam enviados para serviços que não estão prontos para HIPAA. Ao rotular campos específicos que contêm dados confidenciais nos esquemas de fluxo de dados, você pode ter controle granular sobre quais campos de dados podem ser usados para fins específicos.

O vídeo a seguir fornece uma breve visão geral de como as restrições de uso de dados são configuradas e aplicadas aos fluxos de dados na interface do usuário:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

No Experience Platform, é possível aplicar [rótulos de uso de dados confidenciais](../data-governance/labels/reference.md#sensitive) a esquemas e campos que contêm dados que sua organização considera confidenciais. Por exemplo, a variável `RHD` rótulo é utilizado para indicar as Informações de Saúde Protegidas (PHI), e a `S1` rótulo representa dados de geolocalização.

>[!NOTE]
>
>Para obter detalhes sobre como aplicar rótulos de uso de dados na [!UICONTROL Esquemas] na interface do Experience Platform ou na interface da Coleção de dados, consulte a [tutorial de rotulagem de esquema](../xdm/tutorials/labels.md).

Ao criar um novo fluxo de dados, se o esquema selecionado contiver rótulos de uso de dados confidenciais, o fluxo de dados só poderá ser configurado para enviar esses dados para destinos prontos para HIPAA. Atualmente, o único destino pronto para HIPAA compatível com fluxos de dados é o Adobe Experience Platform. Outros serviços de destino, incluindo Adobe Target, Adobe Analytics, Adobe Audience Manager, encaminhamento de eventos e destinos de borda são desativados para sequências de dados que contêm rótulos de uso de dados confidenciais.

Se um esquema estiver sendo usado em um fluxo de dados existente com serviços não prontos para HIPAA, tentar adicionar um rótulo de uso de dados confidenciais ao esquema resultará em uma mensagem de violação de política e a ação será impedida. A mensagem especifica qual sequência de dados acionou a violação e sugere remover quaisquer serviços não prontos para HIPAA da sequência de dados para resolver o problema.

### Logs de auditoria

No Experience Platform, as atividades de fluxo de dados podem ser monitoradas na forma de logs de auditoria. Um log de auditoria informa **quem** realizada **o que** ação e **quando**, juntamente com outros dados contextuais que podem ajudá-lo a solucionar problemas relacionados a fluxos de dados para ajudar sua empresa a cumprir as políticas corporativas de gerenciamento de dados e os requisitos normativos.

Sempre que um usuário cria, atualiza ou exclui um fluxo de dados, um log de auditoria é criado para registrar a ação. O mesmo ocorre sempre que um usuário cria, atualiza ou exclui um mapeamento por meio de [Preparação de dados para coleção de dados](./data-prep.md). Independentemente de ter sido um fluxo de dados ou um mapeamento atualizado, o log de auditoria resultante é categorizado em [!UICONTROL Datastreams] tipo de recurso.

Consulte a documentação em [logs de auditoria](../landing/governance-privacy-security/audit-logs/overview.md) para obter mais informações sobre como interpretar logs de fluxos de dados e outros serviços compatíveis.

## Próximas etapas

Este guia forneceu uma visão geral de alto nível dos fluxos de dados e sua utilização na coleta de dados e no processamento de dados confidenciais. Para obter etapas sobre como configurar um novo fluxo de dados, consulte a [guia de configuração da sequência de dados](./configure.md).
