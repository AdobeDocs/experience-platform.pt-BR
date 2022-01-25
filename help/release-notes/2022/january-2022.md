---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
source-git-commit: 641fcab89b849d91a075fa5058421950bc7fecd7
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 10%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 26 de janeiro de 2021**

Atualizações dos recursos existentes na Adobe Experience Platform:

- [Alertas](#alerts)
- [Preparação de dados](#data-prep)
- [Sandboxes](#sandboxes)
- [Serviço de segmentação](#segmentation)

## Alertas {#alerts}

O Experience Platform permite assinar alertas baseados em eventos para várias atividades da plataforma. É possível assinar diferentes regras de alerta por meio do [!UICONTROL Alertas] na interface do usuário da plataforma e pode optar por receber mensagens de alerta na própria interface do usuário ou por meio de notificações por email.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Novas regras de alerta | Várias novas regras de alerta estão disponíveis para fluxos de trabalho relacionados à assimilação de dados, identidades, perfis, segmentação e ativação. Consulte a visão geral em [regras de alerta](../../observability/alerts/rules.md) para obter a lista atualizada de tipos de alertas. |

Para obter mais informações sobre alertas na Platform, consulte [visão geral dos alertas](../../observability/alerts/overview.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Experiência de mapeamento consolidado | A nova interface de mapeamento na interface do usuário da plataforma fornece uma experiência de mapeamento consistente para aproveitar as recomendações de mapeamento inteligente, configurar manualmente as regras de mapeamento e depurar todos os erros que ocorrerem nos conjuntos de mapeamento. Para obter mais informações, consulte o [[!DNL Data Prep] Guia da interface do usuário](../../data-prep/home.md). |

Para obter mais informações sobre [!DNL Data Prep]consulte o [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Sandboxes {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer os aplicativos de experiência digital em escala global. Geralmente, as empresas executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, teste e implantação desses aplicativos, além de garantir a conformidade operacional. Para atender a essa necessidade, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Aprimoramentos da interface do usuário de sandboxes | O indicador sandbox agora é integrado no cabeçalho para todos os aplicativos da interface do usuário da plataforma. O indicador sandbox exibe o nome, a região e o tipo da sandbox e também permite acessar um menu suspenso para alternar entre sandboxes. Para obter mais informações, consulte o [guia da interface do usuário da sandbox](../../sandboxes/ui/user-guide.md). |

Para obter mais informações sobre sandboxes, consulte o [visão geral das sandboxes](../../sandboxes/home.md).

## Serviço de segmentação {#segmentation}

[!DNL Segmentation Service] O define um subconjunto específico de perfis ao descrever os critérios que distinguem um grupo comercializável de pessoas dentro da base do cliente. Os segmentos podem se basear em dados de registro (como informações demográficas) ou em eventos de séries cronológicas que representem as interações do cliente com sua marca.

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Correspondência de segmentos | Correspondência de segmentos é um serviço de colaboração de dados que permite que dois ou mais usuários da plataforma troquem dados, com base em identificadores comuns, de forma segura, regida e compatível com a privacidade. Para obter mais informações, consulte o [Visão geral da Correspondência de segmento](../../segmentation/ui/segment-match/overview.md). |

Para obter mais informações sobre [!DNL Segmentation Service]consulte o [Visão geral da segmentação](../../segmentation/home.md).
