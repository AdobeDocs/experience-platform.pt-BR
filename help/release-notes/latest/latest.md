---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão de outubro de 2023 para o Adobe Experience Platform.
exl-id: f854f9e5-71be-4d56-a598-cfeb036716cb
source-git-commit: 4ab89ef7cabc9d808fd9dab24b6dbe3fe23e53f3
workflow-type: tm+mt
source-wordcount: '577'
ht-degree: 35%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 25 de outubro de 2023**

Atualizações dos recursos já existentes na Experience Platform:

- [Coleção de dados](#data-collection)
- [Sandboxes](#sandboxes)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Tipo | Recurso | Descrição |
| --- | --- | --- |
| Extensão | [!DNL Meta] Aprimoramento da API de conversões | Há três aprimoramentos na [API de meta conversões](/help/tags/extensions/server/meta/overview.md) extensão: <ul><li>Integração com [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): cria uma experiência de logon contínua, permitindo que você compartilhe seu pixelID e token de acesso para a integração da API de conversões com o Adobe.</li><li>Integração com [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): permite enviar anúncios para pessoas com maior probabilidade de concluir uma ação desejada e vincular a ação de volta aos anúncios entregues.</li><li>Integração com [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): permite passar a RampID do LiveRamp no campo CIP, eliminando a necessidade de compartilhar PII diretamente com parceiros ou Meta. </li></ul> |

Para obter mais informações sobre a coleção de dados, leia a [visão geral das coleções de dados](../../tags/home.md).

## Sandboxes {#sandboxes}

O Adobe Experience Platform foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional. Para atender a essa necessidade, o Experience Platform fornece sandboxes que particionam uma única instância da Platform em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

**Novo recurso**

| Recurso | Descrição |
| --- | --- |
| Ferramentas de sandbox | O recurso de ferramenta de sandbox permite melhorar a precisão da configuração em sandboxes e exportar e importar facilmente configurações de sandbox entre sandboxes. Você pode usar o recurso de ferramenta sandbox para selecionar objetos diferentes e exportá-los em um pacote. Para obter mais informações, consulte [guia da interface do usuário de ferramentas da sandbox](../../sandboxes/ui/sandbox-tooling.md). |

Para obter mais informações sobre sandboxes, consulte a [visão geral das sandboxes](../../sandboxes/home.md).

## Serviço de segmentação {#segmentation}

O [!DNL Segmentation Service] permite segmentar dados relacionados a indivíduos (como clientes, prospectos, usuários ou organizações) que estão armazenados na [!DNL Experience Platform] em públicos-alvo. Você pode criar públicos-alvo por meio de definições de segmento ou outras fontes a partir dos dados do [!DNL Real-Time Customer Profile]. Esses públicos-alvo são configurados e mantidos de forma centralizada na [!DNL Platform] e podem ser acessados a qualquer momento usando as soluções da Adobe.

**Novo recurso**

| Recurso | Descrição |
| ------- | ----------- |
| Públicos-alvo da conta (disponibilidade geral limitada) | No Real-time Customer Data Platform B2B Edition, agora você pode usar a segmentação de conta para trazer a total facilidade e sofisticação da experiência de segmentação de marketing de públicos-alvo com base em pessoas para públicos-alvo com base em conta. Para obter mais informações sobre esse recurso, leia a [visão geral dos públicos-alvo da conta](../../segmentation/ui/account-audiences.md). |

Para saber mais sobre o Serviço de segmentação, leia o [Visão geral do serviço de segmentação](../../segmentation/home.md).

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Autenticação atualizada para a Data Landing Zone | Agora você pode ver a data de expiração designada da Data Landing Zone ao visualizar suas credenciais. Você deve atualizar seu token antes da data de expiração para continuar usando-o em seu aplicativo. Se você não atualizar o token manualmente antes da data de expiração declarada, ele será atualizado automaticamente e fornecerá um novo token na próxima vez que você recuperar suas credenciais. Para obter mais informações, leia a documentação em [uso da Data Landing Zone](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Para saber mais sobre fontes, leia o [visão geral das origens](../../sources/home.md).
