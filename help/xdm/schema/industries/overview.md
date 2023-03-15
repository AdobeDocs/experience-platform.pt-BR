---
solution: Experience Platform
title: Visão geral dos modelos de dados do setor
description: Saiba mais sobre os modelos de dados padronizados para vários setores verticais que podem ser construídos usando componentes padrão do Experience Data Model (XDM).
exl-id: 8fa9a610-36b5-470f-ad63-f2a4a060e0f1
source-git-commit: 60c0bd62b4effaa161c61ab304718ab8c20a06e1
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 1%

---

# Visão geral dos modelos de dados do setor

O Experience Data Model (XDM) permite criar esquemas altamente personalizáveis para capturar os principais dados de experiência do cliente relacionados à sua empresa. Para ajudar a simplificar o processo de modelagem de seus dados para que estejam em conformidade com o XDM, a Adobe Experience Platform fornece um conjunto versátil de componentes XDM padrão, que capturam conceitos normalmente usados em vários setores.

>[!NOTE]
>
>Novos componentes XDM padrão estão sendo lançados continuamente para melhor atender às necessidades do consumidor. Para obter uma lista dos componentes mais atualizados, é possível [explorar os recursos existentes na interface do usuário](../../ui/explore.md) ou consulte o [repositório XDM oficial](https://github.com/adobe/xdm/tree/master/components) no GitHub.

Dependendo do setor em que sua empresa opera, alguns componentes XDM serão mais relevantes para suas necessidades do que outros. Além disso, os relacionamentos estabelecidos entre seus esquemas XDM variam de acordo com o setor.

Para ajudar a orientar sua estratégia de modelagem de dados com base em seu setor específico, este guia fornece uma referência de ERDs (Diagramas de Relacionamento de Entidade) para vários setores industriais compatíveis.

## Pré-requisitos

Para ler os ERDs referenciados neste guia, você deve ter uma compreensão funcional de como os componentes XDM interagem para formar esquemas e como os esquemas XDM operam no Experience Platform como um todo. Certifique-se de ter lido a seguinte documentação de visão geral antes de continuar:

* [Visão geral do sistema XDM](../../home.md): saiba como o XDM opera no ecossistema da plataforma.
* [Noções básicas da composição do esquema](../../schema/composition.md): saiba como os componentes XDM (como grupos de campos de esquema, classes e tipos de dados) contribuem para a estrutura de um esquema, bem como a função dos campos de identidade.

Também é recomendável que você revise o [guia de práticas recomendadas de modelagem de dados](../../schema/best-practices.md) para obter diretrizes gerais sobre como mapear seus dados para o XDM.

## ERDs de modelo de dados do setor {#erds}

Os ERDs são fornecidos para os seguintes setores verticais:

* [[!UICONTROL Varejo]](./retail.md)
* [[!UICONTROL Serviços financeiros]](./financial.md)
* [[!UICONTROL Assistência médica]](./healthcare.md)
* [[!UICONTROL Telecomunicações]](./telecom.md)
* [[!UICONTROL Viagens e hospitalidade]](./travel-hospitality.md)

## Próximas etapas

Este documento forneceu uma visão geral do modelo de dados do setor sobre os ERDs e como interpretá-los. Para visualizar um ERD, selecione um na lista acima.
