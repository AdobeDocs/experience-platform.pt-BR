---
keywords: Experience Platform;página inicial;tópicos populares;identidade;Identidade;gráficos XDM;serviço de identidade;serviço de identidade
solution: Experience Platform
title: Visão geral do serviço de identidade
description: O Serviço de identidade da Adobe Experience Platform ajuda você a obter uma melhor visualização do cliente e do comportamento dele, unindo as identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.
exl-id: a22dc3f0-3b7d-4060-af3f-fe4963b45f18
source-git-commit: ad9fb0bcc7bca55da432c72adc94d49e3c63ad6e
workflow-type: tm+mt
source-wordcount: '1839'
ht-degree: 10%

---

# Visão geral do [!DNL Identity Service]

Para fornecer experiências digitais relevantes, é necessário ter uma compreensão completa do cliente. Isso se torna mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;.

O Identity Service da Adobe Experience Platform fornece uma visão abrangente dos clientes e seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo fornecer experiências digitais pessoais de impacto em tempo real.

Com [!DNL Identity Service], você pode:

- Garanta que seus clientes recebam uma experiência consistente, personalizada e relevante em cada interação.
- Combine várias identidades diferentes de fontes diferentes e crie uma visualização abrangente dos clientes.
- Utilize um gráfico de identidade para mapear diferentes namespaces de identidade, fornecendo uma representação visual de como seus clientes interagem com sua marca em diferentes canais.

## Introdução

Antes de mergulhar nos detalhes de [!DNL Identity Service], aqui está um breve resumo dos termos principais:

| Termo | Definição |
| --- | --- |
| Identidade | Uma identidade são dados exclusivos de uma entidade, normalmente uma pessoa individual. Uma identidade, como uma ID de logon, ECID ou ID de fidelidade, também é chamada de &quot;identidade conhecida&quot;. |
| ECID | ID de Experience Cloud (ECID) é um namespace de identidade compartilhada usado em aplicativos Experience Platform e Adobe Experience Cloud. A ECID fornece uma base para a identidade do cliente e é usada como a ID primária para dispositivos e como um nó base para gráficos de identidade. Consulte a [Visão geral da ECID](./ecid.md) para obter mais informações. |
| Namespace de identidade | Um namespace de identidade serve para distinguir o contexto ou o tipo de uma identidade. Por exemplo, uma identidade distingue “name<span>@email.com” como um endereço de email ou “443522” como uma ID de CRM numérica. Os namespaces de identidade são usados para pesquisar identidades individuais e fornecer o contexto para valores de identidade. Isso permite determinar que dois [!DNL Profile] fragmentos que contêm IDs primárias diferentes, mas compartilham o mesmo valor para a variável `email` namespace de identidade, são, na verdade, o mesmo indivíduo. Consulte a [visão geral do namespace de identidade](./namespaces.md) para obter mais informações. |
| Gráfico de identidade | Um gráfico de identidade é um mapa dos relacionamentos entre identidades diferentes, que permite visualizar e entender melhor quais identidades do cliente são unidas e como. Veja o tutorial sobre [uso do visualizador de gráficos de identidade](./ui/identity-graph-viewer.md) para obter mais informações. |
| Informações pessoais identificáveis (PII) | PII são informações que podem identificar diretamente um cliente, como um endereço de email ou um número de telefone. Os valores de PII geralmente são usados para corresponder. as várias identidades de um cliente em diferentes sistemas. |
| Identidades desconhecidas ou anônimas | Identidades desconhecidas ou anônimas são indicadores que isolam dispositivos sem identificar a pessoa real que está usando o dispositivo. As identidades desconhecidas e anônimas incluem informações como o endereço IP e a ID do cookie de um visitante. Embora identidades desconhecidas e anônimas possam fornecer dados comportamentais, elas são limitadas até que um cliente forneça suas PII. |

## O que é o [!DNL Identity Service]?

Todos os dias, os clientes interagem com seus negócios e estabelecem uma relação cada vez maior com sua marca. Um cliente típico pode estar ativo em qualquer número de sistemas na infraestrutura de dados de sua organização, como sistemas de comércio eletrônico, fidelização e help desk. Esse mesmo cliente também pode se envolver anonimamente em qualquer número de dispositivos. [!DNL Identity Service] O permite reunir uma imagem completa do cliente, agregando dados relacionados que podem ser armazenados em silos em sistemas diferentes.

Considere um exemplo diário do relacionamento de um consumidor com sua marca:

- Mary tem uma conta em seu site de comércio eletrônico em que ela concluiu alguns pedidos no passado. Ela normalmente usa seu laptop pessoal para fazer compras, onde ela faz login todas as vezes. No entanto, durante uma de suas visitas, ela usa o tablet para comprar sandálias, mas não faz um pedido e não faz logon.
- Nesse ponto, a atividade de Mary aparece como dois perfis separados:
   - Seu logon de comércio eletrônico
   - Seu tablet, talvez identificado pela ID do dispositivo
- Mais tarde, Mary retoma sua sessão de tablet e fornece seu endereço de email enquanto assina seu boletim informativo. Ao fazer isso, a assimilação por transmissão adiciona uma nova identidade como dados de registro em seu perfil. Como resultado, [!DNL Identity Service] agora relaciona a atividade do dispositivo tablet de Mary com o histórico de sua conta de comércio eletrônico.
- Ao clicar no tablet dela, o conteúdo direcionado poderá refletir o perfil completo e a história de Mary, em vez de apenas um tablet usado por um comprador desconhecido.

![Compilação de identidade na Platform](./images/identity-service-stitching.png)

Essencialmente, [!DNL Identity Service] O permite reunir uma imagem completa do cliente, agregando dados relacionados que, de outra forma, estariam distribuídos entre sistemas diferentes. As relações de identidade que [!DNL Identity Service] O define e mantém a que o é aproveitado pelo Perfil do cliente em tempo real para criar uma imagem completa de um cliente e suas interações com a sua marca. Para obter mais informações, consulte [Visão geral do Perfil do cliente em tempo real](../profile/home.md).

### Casos de uso

Exemplos de [!DNL Identity Service] As implementações da incluem:

- Uma empresa de telecomunicações pode confiar no valor de &quot;número de telefone&quot;, em que um número de telefone se refere ao mesmo indivíduo de interesse em conjuntos de dados offline e online.
- Uma empresa de varejo pode usar &quot;endereço de email&quot; em conjuntos de dados offline e a ECID em conjuntos de dados online devido à alta porcentagem de visitantes anônimos.
- Um banco pode preferir &quot;número de conta&quot; em conjuntos de dados offline, como transações de filial. Eles podem depender da &quot;ID de logon&quot; em conjuntos de dados online, pois a maioria dos visitantes seria autenticada durante a visita.
- Seus clientes também podem ter IDs proprietárias exclusivas, como GUID ou outros identificadores universalmente exclusivos.

## Namespace de identidade {#identity-namespace}

>[!CONTEXTUALHELP]
>id="platform_identity_namespace"
>title="Namespaces de identidade"
>abstract="Um namespace de identidade serve para distinguir o contexto ou o tipo de uma identidade. Por exemplo, uma identidade distingue “name<span>@email.com” como um endereço de email ou “443522” como uma ID de CRM numérica."
>text="Learn more in documentation"

>[!CONTEXTUALHELP]
>id="platform_identity_value"
>title="Valores de identidade"
>abstract="Um valor de identidade é um identificador que representa uma pessoa, uma organização ou um ativo exclusivo. O contexto ou tipo de identidade que o valor representa é definido por um namespace de identidade correspondente. Ao corresponder dados de registro em fragmentos de perfil, o namespace e o valor de identidade devem corresponder. Ao corresponder dados de registro em fragmentos de perfil, o namespace e o valor de identidade devem corresponder."
>text="Learn more in documentation"

Se você perguntasse a uma pessoa &quot;Qual é a sua ID?&quot; sem qualquer outro contexto, seria difícil para eles dar uma resposta útil. Pela mesma lógica, um valor de string que representa um valor de identidade, seja um ID gerado pelo sistema ou um endereço de email, só é concluído quando fornecido com um qualificador que fornece o contexto do valor de string: o namespace de identidade.

Seus clientes podem interagir com sua marca por meio de uma combinação de canais online e offline, resultando no desafio de como reconciliar essas interações fragmentadas em uma única identidade do cliente.

A compreensão do cliente em vários dispositivos e canais começa com o seu reconhecimento em cada canal. A Platform faz isso usando namespaces de identidade. Um namespace de identidade é um identificador, como email ou telefone, usado para fornecer contexto adicional às identidades do cliente. Os namespaces de identidade são usados para pesquisar ou vincular identidades individuais e fornecer contexto para valores de identidade. Consulte a [visão geral do namespace de identidade](./namespaces.md) para obter mais informações.

## Gráficos de identidade

Um gráfico de identidade é um mapa de relacionamentos entre diferentes namespaces de identidade, que permite visualizar e entender melhor quais identidades de clientes são unidas e como. Veja o tutorial sobre [uso do visualizador de gráficos de identidade](./ui/identity-graph-viewer.md) para obter mais informações.

O vídeo a seguir tem como objetivo fornecer suporte à sua compreensão de identidades e gráficos de identidade.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

## Fornecimento de dados de identidade para [!DNL Identity Service]

Esta seção aborda como os dados fornecidos ao Adobe Experience Platform são processados antes de serem usados pelo [!DNL Identity Service] para criar um gráfico de identidade para cada cliente.

### Decidir sobre campos de identidade

Dependendo da sua estratégia de coleta de dados da empresa, os campos de dados rotulados como identidades determinam quais dados são incluídos no mapa de identidade. Para obter o máximo de benefícios do Adobe Experience Platform e as identidades mais abrangentes possíveis do cliente, você deve fazer upload de dados online e offline.

- Dados online são dados que descrevem a presença e o comportamento online, como nomes de usuário e endereços de email.

- Os dados offline se referem a dados que não estão diretamente relacionados à presença online, como IDs de sistemas CRM. Esse tipo de dados torna suas identidades mais robustas e oferece suporte à coesão de dados em seus diferentes sistemas.

### Criar namespaces de identidade adicionais

Embora o Experience Platform ofereça uma variedade de namespaces padrão, talvez seja necessário criar namespaces adicionais para categorizar corretamente suas identidades. Para obter mais informações, consulte a seção sobre [exibição e criação de namespaces para sua organização](./namespaces.md) na visão geral do namespace de identidade.

>[!NOTE]
>
>Os namespaces de identidade são um qualificador para identidades. Como resultado, depois que um namespace é criado, ele não pode ser excluído.

### Incluir dados de identidade em [!DNL Experience Data Model] (XDM)

Dado que o quadro normalizado pelo qual se [!DNL Platform] organiza os dados do cliente, [!DNL Experience Data Model] O (XDM) permite que os dados sejam compartilhados e compreendidos no Experience Platform e em outros serviços que interagem com o [!DNL Platform]. Para obter mais informações, consulte a [Visão geral do sistema XDM](../xdm/home.md).

Os esquemas de série de registros e de tempo fornecem os meios para incluir dados de identidade. À medida que os dados são assimilados, o gráfico de identidade criará novos relacionamentos entre fragmentos de dados de namespaces diferentes se eles compartilharem dados de identidade comuns.

### Marcação de campos XDM como identidade

Qualquer campo do tipo `string` em esquemas que implementam classes XDM de série temporal ou de registro, eles podem ser rotulados como um campo de identidade. Como resultado, todos os dados assimilados nesse campo seriam considerados dados de identidade.

>[!NOTE]
>
>Campos de tipo de matriz e mapa não são aceitos e não podem ser marcados e rotulados como campos de identidade.

Os campos de identidade também permitem a vinculação de identidades se compartilharem dados PII comuns.
Por exemplo, ao rotular campos de número de telefone como campos de identidade, [!DNL Identity Service] O gera automaticamente gráficos de relações com os outros indivíduos que estão usando o mesmo número de telefone.

>[!NOTE]
>
>O namespace das identidades resultantes é fornecido no momento em que o campo é rotulado.

### Configurar um conjunto de dados para o [!DNL Identity Service]

Durante o processo de assimilação por transmissão, [!DNL Identity Service]O extrai automaticamente dados de identidade de dados de registro e de séries temporais. No entanto, antes que os dados possam ser assimilados, eles devem ser ativados para [!DNL Identity Service]. Veja o tutorial sobre  [configurar um conjunto de dados para o Perfil do cliente em tempo real e o Serviço de identidade usando APIs](../profile/tutorials/dataset-configuration.md) para obter mais informações.

### Assimilar dados em [!DNL Identity Service]

[!DNL Identity Service] consome dados compatíveis com XDM enviados para o Experience Platform por [assimilação em lote](../ingestion/batch-ingestion/overview.md) ou [assimilação por transmissão](../ingestion/streaming-ingestion/overview.md).

O vídeo a seguir tem como objetivo fornecer suporte à sua compreensão do Serviço de identidade. Este vídeo mostra como rotular campos de dados como identidades, assimilar dados de identidade e, em seguida, verificar se os dados foram para o Gráfico privado do serviço de identidade da Adobe Experience Platform.

>[!WARNING]
>
>A variável [!DNL Platform] A interface mostrada no vídeo a seguir está desatualizada. Consulte a documentação para obter as capturas de tela e a funcionalidade mais recentes da interface.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Governança de dados

O Adobe Experience Platform foi criado com a privacidade em mente e inclui uma estrutura de governança de dados para proteger os dados PII do cliente. Os dados de identidade no namespace &quot;email&quot; ou &quot;telefone&quot; são criptografados por padrão, mas para garantir que os dados confidenciais sejam criptografados antes de serem mantidos, os rótulos de uso de dados podem ser aplicados aos dados à medida que são assimilados ou quando chegam ao [!DNL Platform]. Para obter mais informações, leia a [Visão geral da governança de dados](../data-governance/home.md).

## Próximas etapas

Agora que você entende os principais conceitos do [!DNL Identity Service] e sua função no Experience Platform, você pode começar a aprender a trabalhar com seu gráfico de identidade usando o [[!DNL Identity Service API]](./api/getting-started.md).
