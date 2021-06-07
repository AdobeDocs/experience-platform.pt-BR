---
solution: Experience Platform
title: ERD do Modelo de Dados do Setor dos Serviços Financeiros
topic-legacy: overview
description: Exibir um diagrama de relacionamento de entidade (ERD) que descreve um modelo de dados padronizado para o setor bancário, de serviços financeiros e de seguros (BFSI). Esse modelo de dados é compatível com o Experience Data Model (XDM) para uso no Adobe Experience Platform.
exl-id: 2e8f6b2a-10e7-4394-b45f-c03db0f25400
source-git-commit: 88c17992a391b24a76c3e387d3033df4c75a6aa6
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 0%

---

# [!UICONTROL ERD do modelo de dados do setor ] de serviços financeiros

O seguinte diagrama de relacionamento de entidade (ERD) representa um modelo de dados padronizado para o setor bancário, dos serviços financeiros e dos seguros (BFSI). O ERD é intencionalmente apresentado de forma desnormalizada e considerando como os dados são armazenados no Adobe Experience Platform.

Use a seguinte legenda para interpretar este ERD:

* Cada entidade mostrada no é baseada em uma classe [Experience Data Model (XDM) subjacente](../composition.md#class).
* Para uma determinada entidade, cada linha marcada em **bold** representa um grupo de campos ou um tipo de dados, com os campos relevantes que ela fornece listados abaixo em texto sem negrito.
* Os campos mais importantes para uma determinada entidade são destacados em vermelho.
* Todas as propriedades que podem ser usadas para identificar clientes individuais são marcadas como &quot;identidade&quot;, com uma dessas propriedades marcadas como &quot;identidade primária&quot;.
* Os relacionamentos de entidade são marcados como não dependentes, já que os eventos baseados em cookies geralmente não podem determinar a pessoa ou o indivíduo que fez a transação.

![](../../images/industries/financial.png)

>[!NOTE]
>
>A entidade Evento de experiência inclui um campo &quot;_ID&quot;, que representa o atributo identificador exclusivo (`_id`) fornecido pela classe XDM ExperienceEvent. Consulte o documento de referência em [XDM ExperienceEvent](../../classes/experienceevent.md) para obter mais detalhes sobre o que é esperado para esse valor.