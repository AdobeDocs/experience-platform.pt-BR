---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 1%

---


# Visão geral da namespace de identidade

As namespaces de identidade são um componente de [!DNL Identity Service](./home.md) que servem como indicadores do contexto a que uma identidade se refere. Por exemplo, eles distinguem um valor de &quot;name<span>@email.com&quot; como um endereço de email ou &quot;443522&quot; como uma ID CRM numérica.

## Introdução

Trabalhar com namespaces de identidade requer uma compreensão dos vários serviços de Adobe Experience Platform. Antes de começar a trabalhar com o namespace, consulte a documentação dos seguintes serviços:

- [!DNL Real-time Customer Profile](../profile/home.md): Fornece um perfil unificado e em tempo real para o cliente, com base em dados agregados de várias fontes.
- [!DNL Identity Service](./home.md): Obtenha uma melhor visualização de clientes individuais e de seu comportamento ao unir identidades entre dispositivos e sistemas.
- [!DNL Privacy Service](../privacy-service/home.md): As namespaces de identidade são usadas para cumprir o Regulamento Geral de Proteção de Dados (RGPD), onde os pedidos RGPD podem ser feitos em relação a uma namespace.

## Noções básicas sobre namespaces de identidade

Uma identidade totalmente qualificada inclui um valor de ID e uma namespace. Ao corresponder dados de registro em fragmentos de perfil, como quando [!DNL Real-time Customer Profile] mescla dados de perfil, o valor de identidade e a namespace devem corresponder.

Por exemplo, dois fragmentos de perfil podem conter IDs primárias diferentes, mas compartilham o mesmo valor para a namespace &quot;Email&quot;, portanto a Platform pode ver que esses fragmentos são na verdade o mesmo indivíduo e unir os dados no gráfico de identidade do indivíduo.

![](images/identity-service-stitching.png)

### Tipos de identidade

Os dados podem ser identificados por vários tipos de identidade diferentes. O tipo de identidade é especificado no momento em que a namespace de identidade é criada e controla se os dados são persistentes ou não para o gráfico de identidade e quaisquer instruções especiais sobre como esses dados devem ser tratados.

Os seguintes tipos de identidade estão disponíveis em [!DNL Platform]:

| Tipo de identidade | Descrição |
| --- | --- |
| Cookie | Essas identidades são críticas para a expansão e constituem a maioria do gráfico de identidade. No entanto, por natureza, eles caem rápido e perdem seu valor ao longo do tempo. A eliminação de cookies é feita especialmente no gráfico de identidade. |
| Entre dispositivos | Isso indica que [!DNL Identity Service] deve considerar que isso é um identificador forte de pessoas e, portanto, preservá-lo para sempre. Os exemplos incluem uma ID de logon, uma CRM ID, uma ID de fidelidade etc. |
| Dispositivo | Inclui IDFA, GAID e outras IDs IOT. Estes podem ser compartilhados por pessoas em lares. |
| Email | Identidades desse tipo incluem informações de identificação pessoal (PII). Esta é uma indicação para tratar [!DNL Identity Service] o valor com sensibilidade. |
| Dispositivo móvel | Identidades desse tipo incluem PII. Esta é uma indicação para tratar [!DNL Identity Service] o valor com sensibilidade. |
| Não pessoas | Usado para armazenar identificadores que precisam de namespaces, mas não estão vinculados a um cluster de pessoas. Esses identificadores são filtrados a partir do gráfico de identidade. Casos de uso possíveis incluem dados relacionados a produtos, organizações, lojas, etc. (Por exemplo, um SKU de produto.) |
| Telefone | Identidades desse tipo incluem PII. Esta é uma indicação para [!DNL Identity Service] tratar o valor com sensibilidade. |

### namespaces padrão

O Adobe Experience Platform fornece várias namespaces de identidade que estão disponíveis para todas as organizações. Elas são conhecidas como namespaces padrão e são visíveis usando a [!DNL Identity Service] API ou por meio da [!DNL Platform] interface do usuário.

Para visualização de namespaces padrão na interface do usuário, clique em **[!UICONTROL Identidades]** no painel esquerdo e clique na guia *[!UICONTROL Procurar]* . Todas as namespaces de identidade acessíveis à sua organização serão exibidas, no entanto, aquelas com &quot;[!UICONTROL Padrão]&quot; como &quot;[!UICONTROL Proprietário]&quot; são as namespaces padrão fornecidas pelo Adobe.

Você pode clicar em uma das namespaces listadas para obter detalhes sobre a visualização.

![](./images/standard-namespace-detail.png)

## Gerenciamento de namespaces para sua organização

Dependendo dos dados organizacionais e dos casos de uso, você pode precisar de namespaces personalizadas.

Elas são visíveis na interface do usuário como aquelas namespaces com &quot;[!UICONTROL Personalizado]&quot; como &quot;[!UICONTROL Proprietário]&quot;. namespaces personalizadas podem ser criadas usando a [!DNL Identity Service] API ou pela interface do usuário.

Para criar uma namespace personalizada usando a interface do usuário, clique em **[!UICONTROL Criar namespace]** de identidade e, em seguida, preencha a caixa de diálogo e clique em **[!UICONTROL Criar]**.

As Namespaces que você definir são privadas para sua organização e exigem um &quot;Símbolo[!UICONTROL de]identidade&quot; exclusivo (ou &quot;código&quot; se você estiver usando a API) para serem criadas com êxito.

![](./images/create-identity-namespace.png)

Semelhante às namespaces padrão, você pode clicar em uma namespace personalizada na guia *[!UICONTROL Procurar]* para visualização de seus detalhes. Entretanto, com uma namespace personalizada, você também pode editar seu Nome de exibição e Descrição na área de detalhes.

>[!NOTE]
>
>Depois que uma namespace é criada, ela não pode ser excluída e seu &quot;Símbolo de identidade&quot; (ou &quot;código&quot; na API) e &quot;Tipo&quot; não pode ser alterado.

## Namespaces nos dados de identidade

O fornecimento da namespace para uma identidade depende do método usado para fornecer dados de identidade. Para obter detalhes sobre como fornecer dados de identidade, consulte a seção sobre como [fornecer dados](./home.md#supplying-identity-data-to-identity-service) de identidade na [!DNL Identity Service] visão geral.
