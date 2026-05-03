---
title: Visão geral das sequências de dados
description: Saiba como as sequências de dados ajudam a conectar sua integração do Experience Platform SDK no lado do cliente com produtos da Adobe e destinos de terceiros.
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: 79d724eec4903b8a3eee6f717d94fcd70a4ffcb7
workflow-type: tm+mt
source-wordcount: '710'
ht-degree: 48%

---

# Visão geral das sequências de dados

Uma sequência de dados representa a configuração do lado do servidor para os SDKs móveis e da Web do [!DNL Adobe Experience Platform]. Enquanto o comando [`configure`](/help/collection/js/commands/configure/overview.md) no SDK lida com configurações do lado do cliente (como `edgeDomain`), os fluxos de dados gerenciam todas as outras configurações.

Quando você envia uma solicitação para o [!DNL Edge Network], o `datastreamId` faz referência à sequência de dados para a qual os dados são enviados. Você pode atualizar a configuração do lado do servidor sem alterar o código do site.

Você pode criar e gerenciar fluxos de dados selecionando **[!UICONTROL Datastreams]** na navegação à esquerda na interface do usuário [!DNL Adobe Experience Platform] ou na interface da Coleção de Dados.

![Captura de tela da guia Datastreams na interface do usuário do Adobe Experience Platform.](assets/overview/datastreams-tab.png)

Para obter mais informações sobre como configurar uma sequência de dados na interface, consulte o [manual de configuração](/help/datastreams/configure.md).

## Gerenciar dados confidenciais em sequências de dados {#sensitive}

>[!IMPORTANT]
>
>O conteúdo deste documento não é um aconselhamento jurídico e não se destina a substituir tal aconselhamento. Consulte o departamento jurídico da sua empresa para obter aconselhamento sobre o manuseio de dados confidenciais.

As políticas de gerenciamento de dados corporativos e os requisitos normativos estão aumentando as restrições sobre como os dados confidenciais do cliente podem ser coletados, processados e usados. Isso inclui a coleta, o processamento e o uso de PHI (Protected Health Data, dados protegidos de saúde), que estão sujeitos a regulamentos como a HIPAA (Health Insurance Portability and Accountability Act, lei de responsabilidade e mobilidade de seguros de saúde).

As sequências de dados fornecem três métodos para ajudá-lo a lidar com os dados confidenciais de forma segura:

* [Criptografia aprimorada](#encryption)
* [Governança de dados](#governance)
* [Logs de auditorisa](#audit-logs)

### Criptografia aprimorada {#encryption}

Todos os dados em trânsito pelo [!DNL Edge Network] são conduzidos por conexões seguras e criptografadas usando [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Se a sequência de dados estiver trazendo dados para a Experience Platform, eles serão criptografados em repouso no data lake da Experience Platform. Consulte o documento sobre [criptografia de dados na Experience Platform](/help/landing/governance-privacy-security/encryption.md) para obter mais informações.

### Governança de dados {#governance}

As sequências de dados usam os recursos integrados de governança de dados do Experience Platform para impedir que dados confidenciais sejam enviados para serviços que não estão prontos para HIPAA. Ao rotular campos específicos que contêm dados confidenciais nos esquemas de sequência de dados, você pode controlar detalhadamente quais campos de dados podem ser usados para fins específicos.

O vídeo a seguir fornece uma breve visão geral de como as restrições de uso de dados são configuradas e aplicadas às sequências de dados na interface:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

Na Experience Platform, é possível aplicar [rótulos de uso de dados confidenciais](/help/data-governance/labels/reference.md#sensitive) a esquemas e campos que contêm dados que sua organização considera confidenciais. Por exemplo, o rótulo `RHD` é utilizado para identificar dados protegidos de saúde (PHI), e o rótulo `S1` representa dados de geolocalização.

>[!NOTE]
>
>Para obter detalhes sobre como aplicar rótulos de uso de dados na guia [!UICONTROL Schemas] da interface do usuário do Experience Platform ou da Coleção de Dados, consulte o [tutorial de rotulagem de esquemas](/help/xdm/tutorials/labels.md).

Ao criar um fluxo de dados, se o esquema selecionado contiver rótulos de uso de dados confidenciais, você só poderá configurar o fluxo de dados para enviar esses dados para destinos prontos para HIPAA. Atualmente, o único destino pronto para HIPAA com suporte por fluxos de dados é [!DNL Adobe Experience Platform]. Outros serviços de destino, incluindo [!DNL Adobe Target], [!DNL Adobe Analytics], [!DNL Adobe Audience Manager], encaminhamento de eventos e destinos de borda, estão desabilitados para sequências de dados que contêm rótulos de uso de dados confidenciais.

Se um esquema estiver sendo usado em uma sequência de dados existente com serviços que não estão prontos para HIPAA, tentar adicionar um rótulo de uso de dados confidenciais ao esquema resultará em uma mensagem de violação de política e a ação será impedida. A mensagem especifica qual sequência de dados acionou a violação e sugere a remoção de quaisquer serviços não prontos para HIPAA da sequência de dados para resolver o problema.

### Logs de auditoria {#audit-logs}

Na Experience Platform, as atividades da sequência de dados podem ser monitoradas na forma de logs de auditoria. Os logs de auditoria indicam **quem** executou a ação **o que** e **quando**, juntamente com outros dados contextuais que podem ajudá-lo a solucionar problemas relacionados às sequências de dados para ajudar sua empresa a cumprir as políticas corporativas de gerenciamento de dados e os requisitos regulatórios.

Sempre que um usuário cria, atualiza ou exclui uma sequência de dados, um log de auditoria é criado para registrar a ação. O mesmo ocorre sempre que um usuário cria, atualiza ou exclui um mapeamento por meio do [preparo de dados para a coleção de dados](/help/datastreams/data-prep.md). Independentemente de ter sido uma sequência de dados ou um mapeamento atualizado, o log de auditoria resultante é categorizado sob o tipo de recurso [!UICONTROL Datastreams].

Consulte a documentação sobre [logs de auditoria](/help/landing/governance-privacy-security/audit-logs/overview.md) para obter mais informações sobre como interpretar logs de sequências de dados e outros serviços compatíveis.

## Próximas etapas {#next-steps}

Este manual forneceu uma visão geral de alto nível das sequências de dados e sua utilização na coleta de dados e no processamento de dados confidenciais. Para obter etapas sobre como configurar uma nova sequência de dados, consulte o [manual de configuração de sequências de dados](/help/datastreams/configure.md).
