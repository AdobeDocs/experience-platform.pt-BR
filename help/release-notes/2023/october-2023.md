---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão de outubro de 2023 para o Adobe Experience Platform.
exl-id: e9cf5299-8350-4b40-8f56-05e598846875
source-git-commit: f2d0848952902d94b441566da677ef174518192e
workflow-type: tm+mt
source-wordcount: '1068'
ht-degree: 32%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 25 de outubro de 2023**

Atualizações dos recursos já existentes na Experience Platform:

- [Painéis](#dashboards)
- [Coleção de dados](#data-collection)
- [Destinos](#destinations)
- [Sandboxes](#sandboxes)
- [Serviço de segmentação](#segmentation)
- [Origens](#sources)

## Painéis {#dashboards}

A Adobe Experience Platform fornece vários painéis para você visualizar insights importantes sobre os dados de sua organização, que são capturados por instantâneos diários.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Métricas de uso de destinos | Novas métricas foram adicionadas ao painel de uso de licença. A variável **[!UICONTROL Tamanho do Audience Activation]** e **[!UICONTROL Tamanho da exportação de dados]** As métricas fornecem uma maneira conveniente de rastrear a quantidade de dados exportados da Platform em relação aos direitos de uso de licença. Consulte a [métricas disponíveis](../../dashboards/guides/license-usage.md#available-metrics) documentação para obter descrições dessas e de outras métricas de uso de licença. |

{style="table-layout:auto"}

Para obter mais informações sobre painéis, incluindo como conceder permissões de acesso e criar widgets personalizados, comece lendo a [visão geral dos painéis](../../dashboards/home.md).

## Coleção de dados {#data-collection}

A Adobe Experience Platform fornece um conjunto de tecnologias que permitem coletar dados da experiência do cliente e enviá-los à Rede de borda da Adobe Experience Platform, onde eles podem ser enriquecidos, transformados e distribuídos para destinos da Adobe ou de outras empresas.

**Recursos novos ou atualizados**

| Tipo | Recurso | Descrição |
| --- | --- | --- |
| Extensões | [!DNL Meta] Aprimoramento da API de conversões | Há três aprimoramentos na [API de meta conversões](/help/tags/extensions/server/meta/overview.md) extensão: <ul><li>Integração com [[!DNL Meta Business Extension (MBE)]](/help/tags/extensions/server/meta/overview.md#integration-with-meta-business-extension-mbe): cria uma experiência de logon contínua, permitindo que você compartilhe seu pixelID e token de acesso para a integração da API de conversões com o Adobe.</li><li>Integração com [[!DNL Event Match Quality Score (EMQ)]](/help/tags/extensions/server/meta/overview.md#integration-with-event-quality-match-score-emq): permite enviar anúncios para pessoas com maior probabilidade de concluir uma ação desejada e vincular a ação de volta aos anúncios entregues.</li><li>Integração com [[!DNL LiveRamp (Alpha)]](/help/tags/extensions/server/meta/overview.md#integration-with-liveramp-alpha): permite passar a RampID do LiveRamp no campo CIP, eliminando a necessidade de compartilhar PII diretamente com parceiros ou Meta. </li></ul> |
| Extensões | [!DNL LinkedIn] API de conversões | A variável [[!DNL LinkedIn] API de conversões](../../tags/extensions/server/linkedin/overview.md) A extensão do permite avaliar a eficácia de suas campanhas de marketing do LinkedIn, encaminhando dados do evento Experience Platform para a LinkedIn. |
| Segredo | [!DNL LinkedIn] Segredo do OAuth 2 | A variável [[!DNL LinkedIn] Segredo do OAuth 2](../../tags/ui/event-forwarding/secrets.md#linkedin-oauth-2) permite enviar interações servidor-servidor para [!DNL LinkedIn] no encaminhamento de eventos. |
| Encaminhamento de eventos | Atualização de tags e encaminhamento de eventos | Para preservar [Tags](https://experienceleague.adobe.com/docs/experience-platform/tags/home.html?lang=pt-BR) e [Encaminhamento de evento](https://experienceleague.adobe.com/docs/experience-platform/tags/event-forwarding/overview.html) desempenho na Platform, somente as builds mais recentes de Desenvolvimento e Preparo, bem-sucedidas e malsucedidas, serão mantidas. Todas as builds que não estão mais em uso serão removidas. Além disso, a limitação e a limitação de taxa foram implementadas para garantir que alguns usos intensos de API não prejudiquem o desempenho da API para outros. |
| Extensões | Elementos, regras e extensões | [Elementos, regras e extensões](https://experienceleague.adobe.com/docs/experience-platform/tags/extensions/overview.html?lang=pt-BR) agora são classificados na saída da biblioteca para garantir mais consistência entre várias builds e implantações da mesma biblioteca. |

Para obter mais informações sobre a coleção de dados, leia a [visão geral das coleções de dados](../../tags/home.md).

## Destinos {#destinations}

[!DNL Destinations] são integrações pré-construídas com plataformas de destino que permitem a ativação perfeita de dados da Adobe Experience Platform. É possível usar destinos para ativar seus dados conhecidos e desconhecidos para campanhas de marketing entre canais, campanhas de email, publicidade direcionada e muitos outros casos de uso.

**Destinos novos ou atualizados** {#new-updated-destinations}

| Destino | Novo ou atualizado | Descrição |
| ----------- |----------------|----------- |
| [[!DNL MoEngage]](/help/destinations/catalog/mobile-engagement/moengage.md) | Novo | Use o destino do Moengage para conectar e mapear seus dados do Adobe (atributos de usuário, segmentos e eventos) para o MoEngage em tempo real. Os clientes podem então agir com base nesses dados, fornecendo experiências personalizadas e direcionadas. |
| [[!DNL Qualtrics Automations]](/help/destinations/catalog/survey/qualtrics-automations.md) | Novo | Use a agregação de várias fontes de dados operacionais no Adobe Experience Platform como uma entrada na Experience ID do Qualtrics para entender melhor seus clientes e permitir que o alcance direcionado feche a lacuna quando se trata de entender a intenção, a emoção e os impulsionadores de experiência. |

{style="table-layout:auto"}

**Funcionalidades novas ou atualizadas** {#destinations-new-updated-functionality}

| Funcionalidade | Descrição |
| ----------- | ----------- |
| (Beta) Suporte para funções de hash em campos calculados | Além das funções específicas para [exportação de matrizes](../../destinations/ui/export-arrays-calculated-fields.md) ou elementos de uma matriz, agora é possível usar recursos [funções de hash](../../destinations/ui/export-arrays-calculated-fields.md#hashing-functions) aos atributos de hash nos arquivos exportados. As funções de hash compatíveis são: `sha`, `sha256`, `sha512`, `hash`, `md5`, `crc32`. |
| (Disponibilidade limitada) Ativar públicos-alvo da conta para determinados destinos | Os clientes B2B do Real-Time CDP agora podem ativar [públicos-alvo da conta](../../segmentation/ui/account-audiences.md) para certos destinos. Para obter mais informações sobre esse recurso, leia a [tutorial para ativar públicos-alvo da conta](/help/destinations/ui/activate-account-audiences.md). |

{style="table-layout:auto"}

**Correções e aprimoramentos** {#destinations-fixes-and-enhancements}

Para obter informações mais gerais sobre destinos, consulte a [visão geral de destinos](../../destinations/home.md).

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
