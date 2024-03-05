---
title: Visão geral das sequências de dados
description: Saiba como os fluxos de dados ajudam a conectar sua integração do SDK do Experience Platform do lado do cliente com produtos Adobe e destinos de terceiros.
exl-id: 736c75cb-e290-474e-8c47-2a031f215a56
source-git-commit: b6e084d2beed58339191b53d0f97b93943154f7c
workflow-type: tm+mt
source-wordcount: '727'
ht-degree: 77%

---

# Visão geral das sequências de dados

Uma sequência de dados representa a configuração do lado do servidor ao implementar os SDKs móveis e da Web da Adobe Experience Platform. Embora a [`configure`](/help/web-sdk/commands/configure/overview.md) comando no SDK controla itens que devem ser manipulados no cliente (como o `edgeDomain`), os fluxos de dados lidam com todas as outras configurações para o SDK. Quando uma solicitação é enviada para a rede de borda da Adobe Experience Platform, o `edgeConfigId` é usado para fazer referência à sequência de dados. Isso permite atualizar a configuração do lado do servidor sem precisar fazer alterações de código no site.

Você pode criar e gerenciar sequências de dados selecionando **[!UICONTROL Sequências de dados]** na navegação à esquerda da interface da Adobe Experience Platform ou da Coleção de dados.

![Guia Sequências de dados na interface](assets/overview/datastreams-tab.png)

Para obter mais informações sobre como configurar uma sequência de dados na interface, consulte o [manual de configuração](./configure.md).

## Gerenciar dados confidenciais em sequências de dados {#sensitive}

>[!IMPORTANT]
>
>O conteúdo deste documento não é um aconselhamento jurídico e não se destina a substituir tal aconselhamento. Consulte o departamento jurídico da sua empresa para obter aconselhamento sobre o manuseio de dados confidenciais.

As políticas de gerenciamento de dados corporativos e os requisitos normativos estão aumentando as restrições sobre como os dados confidenciais do cliente podem ser coletados, processados e usados. Isso inclui a coleta, o processamento e o uso de dados protegidos de saúde (PHI), que estão sujeitos a regulamentos como a Lei de Portabilidade e Responsabilidade de Seguro de Saúde (HIPAA).

As sequências de dados fornecem três métodos para ajudar a lidar com dados confidenciais de maneira segura:

* [Criptografia aprimorada](#encryption)
* [Governança de dados](#governance)
* [Logs de auditoria](#audit-logs)

### Criptografia aprimorada {#encryption}

Todos os dados em trânsito pela rede de borda são conduzidos por conexões seguras e criptografadas usando [HTTPS TLS 1.2](https://datatracker.ietf.org/doc/html/rfc5246). Se a sequência de dados estiver trazendo dados para a Experience Platform, eles serão criptografados em repouso no data lake da Experience Platform. Consulte o documento sobre [criptografia de dados na Experience Platform](../landing/governance-privacy-security/encryption.md) para obter mais informações.

### Governança de dados {#governance}

As sequências de dados usam os recursos integrados de governança de dados do Experience Platform para impedir que dados confidenciais sejam enviados para serviços que não estão prontos para HIPAA. Ao rotular campos específicos que contêm dados confidenciais nos esquemas de sequência de dados, você pode controlar detalhadamente quais campos de dados podem ser usados para fins específicos.

O vídeo a seguir fornece uma breve visão geral de como as restrições de uso de dados são configuradas e aplicadas às sequências de dados na interface:

>[!VIDEO](https://video.tv.adobe.com/v/3409588/?quality=12&learn=on&speedcontrol=on)

Na Experience Platform, é possível aplicar [rótulos de uso de dados confidenciais](../data-governance/labels/reference.md#sensitive) a esquemas e campos que contêm dados que sua organização considera confidenciais. Por exemplo, o rótulo `RHD` é utilizado para identificar dados protegidos de saúde (PHI), e o rótulo `S1` representa dados de geolocalização.

>[!NOTE]
>
>Para obter detalhes sobre como aplicar rótulos de uso de dados na guia [!UICONTROL Esquemas] da interface da Experience Platform ou da Coleção de dados, consulte o [tutorial de rotulagem de esquemas](../xdm/tutorials/labels.md).

Ao criar um fluxo de dados, se o esquema selecionado contiver rótulos de uso de dados confidenciais, você só poderá configurar o fluxo de dados para enviar esses dados para destinos prontos para HIPAA. Atualmente, o único destino pronto para HIPAA compatível com sequências de dados é a Adobe Experience Platform. Outros serviços de destino, como Adobe Target, Adobe Analytics, Adobe Audience Manager, encaminhamento de eventos e os destinos de borda, são desabilitados para sequências de dados que contêm rótulos de uso de dados confidenciais.

Se um esquema estiver sendo usado em uma sequência de dados existente com serviços que não estão prontos para HIPAA, tentar adicionar um rótulo de uso de dados confidenciais ao esquema resultará em uma mensagem de violação de política e a ação será impedida. A mensagem especifica qual sequência de dados acionou a violação e sugere a remoção de quaisquer serviços não prontos para HIPAA da sequência de dados para resolver o problema.

### Logs de auditoria

Na Experience Platform, as atividades da sequência de dados podem ser monitoradas na forma de logs de auditoria. Os logs de auditoria indicam **quem** realizada **o que** ação e **quando**, juntamente com outros dados contextuais que podem ajudá-lo a solucionar problemas relacionados a fluxos de dados para ajudar sua empresa a cumprir as políticas corporativas de gerenciamento de dados e os requisitos normativos.

Sempre que um usuário cria, atualiza ou exclui uma sequência de dados, um log de auditoria é criado para registrar a ação. O mesmo ocorre sempre que um usuário cria, atualiza ou exclui um mapeamento por meio do [preparo de dados para a coleção de dados](./data-prep.md). Independentemente do recurso atualizado ter sido uma sequência de dados ou um mapeamento, o log de auditoria resultante é categorizado no tipo de recurso [!UICONTROL Sequências de dados].

Consulte a documentação sobre [logs de auditoria](../landing/governance-privacy-security/audit-logs/overview.md) para obter mais informações sobre como interpretar logs de sequências de dados e outros serviços compatíveis.

## Próximas etapas

Este manual forneceu uma visão geral de alto nível das sequências de dados e sua utilização na coleta de dados e no processamento de dados confidenciais. Para obter etapas sobre como configurar uma nova sequência de dados, consulte o [manual de configuração de sequências de dados](./configure.md).
