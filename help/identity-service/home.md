---
keywords: Experience Platform, home, tópicos populares, identidade, identidade, gráficos XDM, serviço de identidade, serviço de identidade
solution: Experience Platform
title: Visão geral do serviço de identidade
topic-legacy: overview
description: O serviço de identidade da Adobe Experience Platform ajuda você a obter uma melhor visão de seu cliente e de seu comportamento ao unir identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: 947d8803416cee584b35a8d480929e2684d0057f
workflow-type: tm+mt
source-wordcount: '1807'
ht-degree: 0%

---

# [!DNL Identity Service] visão geral

Fornecer experiências digitais relevantes requer ter uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

O serviço de identidade da Adobe Experience Platform fornece uma visão abrangente dos clientes e do comportamento deles ao unir identidades entre dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.

Com [!DNL Identity Service], você pode:

- Certifique-se de que os clientes recebam uma experiência consistente, personalizada e relevante em cada interação.
- Reúna várias identidades diferentes de fontes diferentes e crie uma exibição abrangente dos clientes.
- Utilize um gráfico de identidade para mapear diferentes namespaces de identidade, fornecendo uma representação visual de como seus clientes interagem com a marca em diferentes canais.

## Introdução

Antes de entrar nos detalhes de [!DNL Identity Service], veja um breve resumo dos termos principais:

| Termo | Definição |
| --- | --- |
| Identidade | Uma identidade são dados exclusivos de uma entidade, normalmente uma pessoa individual. Uma identidade, como uma ID de logon, ECID ou ID de fidelidade, também é chamada de &quot;identidade conhecida&quot;. |
| ECID | Experience Cloud ID (ECID) é um namespace de identidade compartilhada usado em aplicativos Experience Platform e Adobe Experience Cloud. A ECID fornece uma base para a identidade do cliente e é usada como a ID primária para dispositivos e como um nó base para gráficos de identidade. Consulte a [Visão geral da ECID](./ecid.md) para obter mais informações. |
| Namespace de identidade | Um namespace de identidade serve para distinguir o contexto ou o tipo de uma identidade. Por exemplo, uma identidade distingue &quot;name<span>@email.com&quot; como um endereço de email ou &quot;443522&quot; como uma ID de CRM numérica. Os namespaces de identidade são usados para buscar identidades individuais e fornecer o contexto para valores de identidade. Isso permite determinar se dois fragmentos [!DNL Profile] que contêm IDs primárias diferentes, mas compartilham o mesmo valor para o namespace de identidade `email`, são, de fato, o mesmo indivíduo. Consulte a [visão geral do namespace de identidade](./namespaces.md) para obter mais informações. |
| Gráfico de identidade | Um gráfico de identidade é um mapa de relacionamentos entre diferentes identidades, permitindo visualizar e entender melhor quais identidades de cliente são unidas e como. Consulte o tutorial em [usando o visualizador de gráfico de identidade](./ui/identity-graph-viewer.md) para obter mais informações. |
| Informações pessoais identificáveis (PII) | PII são informações que podem identificar diretamente um cliente, como um endereço de email ou um número de telefone. Os valores de PII geralmente são usados para corresponder. várias identidades de um cliente em diferentes sistemas. |
| Identidade única | Uma identidade exclusiva é uma identidade que existe somente em uma sandbox específica. |
| Identidades desconhecidas ou anônimas | Identidades desconhecidas ou anônimas são indicadores que isolam dispositivos sem identificar a pessoa real que usa o dispositivo. Identidades desconhecidas e anônimas incluem informações como o endereço IP de um visitante e a ID do cookie. Embora identidades desconhecidas e anônimas possam fornecer dados comportamentais, elas são limitadas até que um cliente forneça suas PII. |

## O que é o [!DNL Identity Service]?

A cada dia, os clientes interagem com seus negócios e estabelecem um relacionamento em constante crescimento com sua marca. Um cliente típico pode estar ativo em qualquer número de sistemas dentro da infraestrutura de dados de sua organização, como seu comércio eletrônico, fidelidade e sistemas de suporte técnico. Esse mesmo cliente também pode se envolver anonimamente em qualquer número de dispositivos. [!DNL Identity Service] O permite reunir uma imagem completa do cliente, agregando dados relacionados que podem ser colocados em silos entre sistemas diferentes.

Considere um exemplo diário do relacionamento do consumidor com a sua marca:

- Mary tem uma conta em seu site de comércio eletrônico onde ela concluiu alguns pedidos no passado. Ela normalmente usa seu laptop pessoal para fazer compras, onde ela faz login sempre. No entanto, durante uma de suas visitas, ela usa seu tablet para comprar sandálias, mas não faz um pedido e não faz login.
- Neste ponto, a atividade de Mary aparece como dois perfis separados:
   - Seu logon de comércio eletrônico
   - Seu tablet, talvez identificado pela ID do dispositivo
- Mary depois retoma sua sessão de tablet e fornece seu endereço de email ao assinar seu informativo. Ao fazer isso, a assimilação de streaming adiciona uma nova identidade como dados de registro em seu perfil. Como resultado, [!DNL Identity Service] agora relaciona a atividade do tablet de Mary com o histórico da conta de comércio eletrônico.
- Ao clicar em seu tablet, seu conteúdo direcionado pode refletir o perfil completo e o histórico de Mary, em vez de apenas um tablet usado por um comprador desconhecido.

![Compilação de identidade na plataforma](./images/identity-service-stitching.png)

Essencialmente, [!DNL Identity Service] permite que você reúna uma imagem completa do seu cliente, agregando dados relacionados que, de outra forma, poderiam estar espalhados por sistemas diferentes. Os relacionamentos de identidade que [!DNL Identity Service] define e mantém são aproveitados pelo Perfil do cliente em tempo real para criar uma imagem completa de um cliente e suas interações com sua marca. Para obter mais informações, consulte a [Visão geral do Perfil do cliente em tempo real](../profile/home.md).

### Casos de uso

Exemplos de implementações [!DNL Identity Service] incluem:

- Uma empresa de telecomunicações pode confiar no valor do &quot;número de telefone&quot;, onde um número de telefone se refere ao mesmo indivíduo de interesse tanto em conjuntos de dados offline quanto online.
- Uma empresa de varejo pode usar &quot;endereço de email&quot; em conjuntos de dados offline e ECID em conjuntos de dados online devido à alta porcentagem de visitantes anônimos.
- Um banco pode preferir &quot;número de conta&quot; em conjuntos de dados offline, como transações de ramificação. Eles podem depender da &quot;ID de logon&quot; em conjuntos de dados online, pois a maioria dos visitantes seria autenticada durante a visita.
- Seus clientes também podem ter IDs proprietárias exclusivas, como GUID ou outros identificadores universalmente exclusivos.

## Namespaces de identidade

Se você perguntou a uma pessoa &quot;Qual é sua ID?&quot; sem qualquer outro contexto, seria difícil para eles dar uma resposta útil. Pela mesma lógica, um valor de string que representa um valor de identidade, seja um ID gerado pelo sistema ou um endereço de email, só é concluído quando fornecido com um qualificador que fornece o contexto do valor da string: o namespace de identidade.


Seus clientes podem interagir com sua marca por meio de uma combinação de canais online e offline, resultando no desafio de como reconciliar essas interações fragmentadas em uma única identidade de cliente.

Entender seu cliente em vários dispositivos e canais começa reconhecendo-os em cada canal. A Platform faz isso usando namespaces de identidade. Um namespace de identidade é um identificador como Email ou Telefone, usado para fornecer contexto adicional às identidades do cliente. Os namespaces de identidade são usados para buscar ou vincular identidades individuais e fornecer contexto para valores de identidade. Consulte a [visão geral do namespace de identidade](./namespaces.md) para obter mais informações.

## Gráficos de identidade

Um gráfico de identidade é um mapa de relacionamentos entre diferentes namespaces de identidade, permitindo visualizar e entender melhor quais identidades de cliente estão reunidas e como. Consulte o tutorial em [usando o visualizador de gráfico de identidade](./ui/identity-graph-viewer.md) para obter mais informações.

O vídeo a seguir destina-se a oferecer suporte à compreensão das identidades e gráficos de identidade. Ela aborda os três recursos da coleta de identidade, gráficos de identidade e a API. Também descreve como os algoritmos determinísticos e probabilísticos são usados para construir gráficos de identidade privada e discute sua função junto com gráficos de terceiros e o Gráfico cooperativo do Serviço de identidade da Adobe Experience Platform.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Fornecimento de dados de identidade para [!DNL Identity Service]

Esta seção aborda como os dados fornecidos ao Adobe Experience Platform são processados antes de serem usados pelo [!DNL Identity Service] para criar um gráfico de identidade para cada cliente.

### Decidir em campos de identidade

Dependendo da estratégia de coleta de dados da empresa, os campos de dados que você rotular como identidades determinam quais dados serão incluídos em seu mapa de identidade. Para obter o máximo benefício do Adobe Experience Platform e as identidades mais abrangentes do cliente possíveis, você deve fazer upload de dados online e offline.

- Dados online são dados que descrevem a presença e o comportamento online, como nomes de usuário e endereços de email.

- Os dados offline se referem a dados que não estão diretamente relacionados à presença online, como IDs de sistemas CRM. Esse tipo de dado torna suas identidades mais robustas e oferece suporte à coesão de dados em diferentes sistemas.

### Criar namespaces de identidade adicionais

Embora o Experience Platform ofereça uma variedade de namespaces padrão, talvez seja necessário criar namespaces adicionais para categorizar adequadamente suas identidades. Para obter mais informações, consulte a seção sobre [visualizar e criar namespaces para sua organização](./namespaces.md) na visão geral do namespace de identidade.

>[!NOTE]
>
>Os namespaces de identidade são um qualificador para identidades. Como resultado, depois que um namespace é criado, ele não pode ser excluído.

### Incluir dados de identidade em [!DNL Experience Data Model] (XDM)

Como a estrutura padronizada pela qual [!DNL Platform] organiza os dados do cliente, [!DNL Experience Data Model] (XDM) permite que os dados sejam compartilhados e compreendidos entre o Experience Platform e outros serviços que interagem com [!DNL Platform]. Para obter mais informações, consulte a [Visão geral do sistema XDM](../xdm/home.md).

Os esquemas de registro e de série de tempo fornecem os meios para incluir dados de identidade. À medida que os dados são assimilados, o gráfico de identidade criará novas relações entre fragmentos de dados de diferentes namespaces, se for encontrado que eles compartilham dados de identidade comuns.

### Marcar campos XDM como identidade

Qualquer campo do tipo `string` em esquemas que implementam classes XDM de registro ou de série de tempo pode ser rotulado como um campo de identidade. Como resultado, todos os dados assimilados nesse campo seriam considerados dados de identidade.

>[!NOTE]
>
>Os campos do tipo matriz e mapa não são suportados e não podem ser marcados e rotulados como campos de identidade.

Os campos de identidade também permitem a vinculação de identidades se compartilharem dados PII comuns.
Por exemplo, ao rotular os campos de número de telefone como campos de identidade, [!DNL Identity Service] define automaticamente as relações com os outros indivíduos que estiverem usando o mesmo número de telefone.

>[!NOTE]
>
>O namespace das identidades resultantes é fornecido no momento em que o campo é rotulado.

### Configurar um conjunto de dados para [!DNL Identity Service]

Durante o processo de assimilação de streaming, [!DNL Identity Service ]extrai automaticamente os dados de identidade dos dados de registro e da série de tempo. No entanto, antes que os dados possam ser assimilados, eles devem ser ativados para [!DNL Identity Service]. Consulte o tutorial em [configurar um conjunto de dados para o Perfil do cliente em tempo real e o Serviço de identidade usando APIs](../profile/tutorials/dataset-configuration.md) para obter mais informações.

### Assimilar dados a [!DNL Identity Service]

[!DNL Identity Service] O consome dados compatíveis com XDM enviados para o Experience Platform por ingestão  [de ](../ingestion/batch-ingestion/overview.md) lote ou  [assimilação de streaming](../ingestion/streaming-ingestion/overview.md).

O vídeo a seguir serve para oferecer suporte à compreensão do serviço de identidade. Este vídeo mostra como rotular campos de dados como identidades, assimilar dados de identidade e, em seguida, verificar se os dados foram para o Gráfico privado do serviço de identidade da Adobe Experience Platform.

>[!WARNING]
>
>A interface [!DNL Platform] mostrada no vídeo a seguir está desatualizada. Consulte a documentação para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Governança de dados

A Adobe Experience Platform foi criada pensando na privacidade e inclui uma estrutura de governança de dados para proteger os dados de PII de seus clientes. Os dados de identidade no namespace &quot;email&quot; ou &quot;telefone&quot; são criptografados por padrão, mas para garantir que os dados confidenciais sejam criptografados antes de serem persistentes, os rótulos de uso de dados podem ser aplicados aos dados à medida que são assimilados ou após serem recebidos em [!DNL Platform]. Para obter mais informações, leia a [Visão geral da governança de dados](../data-governance/home.md).

## Próximas etapas

Agora que você entende os principais conceitos de [!DNL Identity Service] e sua função no Experience Platform, pode começar a aprender a trabalhar com o gráfico de identidade usando o [[!DNL Identity Service API]](./api/getting-started.md).
