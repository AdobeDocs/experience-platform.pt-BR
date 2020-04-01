---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Visão geral da namespace de identidade

As namespaces de identidade são um componente do Serviço [de](./home.md) identidade que serve como indicadores do contexto ao qual uma identidade está relacionada. Por exemplo, eles distinguem um valor de &quot;name<span>@email.com&quot; como um endereço de email ou &quot;443522&quot; como uma ID CRM numérica.

## Introdução

Trabalhar com namespaces de identidade requer uma compreensão dos vários serviços da plataforma Adobe Experience envolvidos. Antes de começar a trabalhar com o namespace, consulte a documentação dos seguintes serviços:

- [Perfil](../profile/home.md)do cliente em tempo real: Fornece um perfil unificado e em tempo real para o cliente, com base em dados agregados de várias fontes.
- [Serviço](./home.md)de identidade: Obtenha uma melhor visualização de clientes individuais e de seu comportamento ao unir identidades entre dispositivos e sistemas.
- [Privacy Service](../privacy-service/home.md): As namespaces de identidade são usadas para cumprir o Regulamento Geral de Proteção de Dados (RGPD), onde os pedidos RGPD podem ser feitos em relação a uma namespace.

## Noções básicas sobre namespaces de identidade

Uma identidade totalmente qualificada inclui um valor de ID e uma namespace. Ao combinar dados de registro em fragmentos de perfil, como quando o Perfil Cliente em tempo real mescla dados de perfil, o valor de identidade e a namespace devem corresponder.

Por exemplo, dois fragmentos de perfil podem conter IDs primárias diferentes, mas compartilham o mesmo valor para a namespace &quot;Email&quot;. Portanto, a Platform pode ver que esses fragmentos são na verdade o mesmo indivíduo e unir os dados no gráfico de identidade do indivíduo.

![](images/identity-service-stitching.png)

### Tipos de identidade

Os dados podem ser identificados por vários tipos de identidade diferentes. O tipo de identidade é especificado no momento em que a namespace de identidade é criada e controla se os dados são persistentes ou não para o gráfico de identidade e quaisquer instruções especiais sobre como esses dados devem ser tratados.

Os seguintes tipos de identidade estão disponíveis na Plataforma:

| Tipo de identidade | Descrição |
| --- | --- |
| Cookie | Essas identidades são críticas para a expansão e constituem a maioria do gráfico de identidade. No entanto, por natureza, eles caem rápido e perdem seu valor ao longo do tempo. A eliminação de cookies é feita especialmente no gráfico de identidade. |
| Entre dispositivos | Isto indica que o Serviço de Identidade deve considerar que se trata de um identificador forte de pessoas e, portanto, preservá-lo para sempre. Os exemplos incluem uma ID de logon, uma CRM ID, uma ID de fidelidade etc. |
| Dispositivo | Inclui IDFA, GAID e outras IDs IOT. Estes podem ser compartilhados por pessoas em lares. |
| Email | Identidades desse tipo incluem informações de identificação pessoal (PII). Essa é uma indicação para o Serviço de identidade para tratar o valor com sensibilidade. |
| Dispositivo móvel | Identidades desse tipo incluem PII. Essa é uma indicação para o Serviço de identidade para tratar o valor com sensibilidade. |
| Não pessoas | Usado para armazenar identificadores que precisam de namespaces, mas não estão vinculados a um cluster de pessoas. Esses identificadores são filtrados a partir do gráfico de identidade. Casos de uso possíveis incluem dados relacionados a produtos, organizações, lojas, etc. (Por exemplo, um SKU de produto.) |
| Telefone | Identidades desse tipo incluem PII. Essa é uma indicação para o Serviço de identidade para tratar o valor com sensibilidade. |

### namespaces padrão

A plataforma Adobe Experience fornece várias namespaces de identidade disponíveis para todas as organizações. Elas são conhecidas como namespaces padrão e são visíveis usando a API do serviço de identidade ou por meio da interface do usuário da plataforma.

Para visualização de namespaces padrão na interface do usuário, clique em **Identidades** no painel esquerdo e clique na guia *Procurar* . Todas as namespaces de identidade acessíveis à sua organização serão exibidas, no entanto, aquelas com &quot;Padrão&quot; como &quot;Proprietário&quot; são as namespaces padrão fornecidas pela Adobe.

Você pode clicar em uma das namespaces listadas para obter detalhes sobre a visualização.

![](./images/standard-namespace-detail.png)

## Gerenciamento de namespaces para sua organização

Dependendo dos dados organizacionais e dos casos de uso, você pode precisar de namespaces personalizadas.

Elas são visíveis na interface do usuário como aquelas namespaces com &quot;Personalizado&quot; como &quot;Proprietário&quot;. namespaces personalizadas podem ser criadas usando a API do Serviço de Identidade ou por meio da interface do usuário.

Para criar uma namespace personalizada usando a interface do usuário, clique em **Criar namespace** de identidade e, em seguida, preencha a caixa de diálogo e clique em **Criar**.

As Namespaces que você definir são privadas para sua organização e exigem um &quot;Símbolo de identidade&quot; (ou &quot;código&quot; se você estiver usando a API) exclusivo para serem criadas com êxito.

![](./images/create-identity-namespace.png)

Semelhante às namespaces padrão, você pode clicar em uma namespace personalizada na guia *Procurar* para visualização de seus detalhes. Entretanto, com uma namespace personalizada, você também pode editar seu Nome de exibição e Descrição na área de detalhes.

>[!NOTE] Depois que uma namespace é criada, ela não pode ser excluída e seu &quot;Símbolo de identidade&quot; (ou &quot;código&quot; na API) e &quot;Tipo&quot; não pode ser alterado.

## Namespaces nos dados de identidade

O fornecimento da namespace para uma identidade depende do método usado para fornecer dados de identidade. Para obter detalhes sobre como fornecer dados de identidade de dados, consulte a seção sobre como [fornecer dados](./home.md#supplying-identity-data-to-identity-service) de identidade na visão geral do Serviço de identidade.
