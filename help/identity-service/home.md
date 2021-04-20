---
keywords: Experience Platform, home, tópicos populares, identidade, identidade, gráficos XDM, serviço de identidade, serviço de identidade
solution: Experience Platform
title: Visão geral do serviço de identidade
topic: overview
description: O serviço de identidade da Adobe Experience Platform ajuda você a obter uma melhor visão de seu cliente e de seu comportamento ao unir identidades em dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e impactantes em tempo real.
translation-type: tm+mt
source-git-commit: bb218fc0cca6fe74693e99747963058bd0dc962a
workflow-type: tm+mt
source-wordcount: '1718'
ht-degree: 0%

---


# [!DNL Identity Service]visão geral

Fornecer experiências digitais relevantes requer ter uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;. O Adobe Experience Platform [!DNL Identity Service] ajuda você a obter uma melhor visão de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais impactantes em tempo real.

## Noções básicas do [!DNL Identity Service]

A cada dia, os clientes interagem com seus negócios e estabelecem um relacionamento em constante crescimento com sua marca. Um cliente típico pode estar ativo em qualquer número de sistemas dentro da infraestrutura de dados de sua organização, como seu eCommerce, fidelidade e sistemas de suporte técnico. Esse mesmo cliente também pode se envolver anonimamente em qualquer número de dispositivos. [!DNL Identity Service] O permite reunir uma imagem completa do cliente, agregando dados relacionados que podem ser colocados em silos entre sistemas diferentes.

Considere um exemplo diário do relacionamento do consumidor com a sua marca:

Mary tem uma conta em seu site de comércio eletrônico onde ela concluiu alguns pedidos no passado. Ela normalmente usa seu laptop pessoal para fazer compras, onde ela faz login sempre. No entanto, durante uma de suas visitas, ela usa seu tablet para comprar sandálias, mas não faz um pedido e não faz login.

Neste ponto, a atividade de Mary aparece como dois perfis separados: o logon do eCommerce e do tablet, talvez identificados pela ID do dispositivo.

Mary depois retoma sua sessão de tablet e fornece seu endereço de email ao assinar seu informativo. Ao fazer isso, a assimilação de streaming adiciona uma nova identidade como dados de registro em seu perfil. Como resultado, [!DNL Identity Service] agora relaciona a atividade do tablet de Mary com o histórico da conta de comércio eletrônico.

Ao clicar em seu tablet, seu conteúdo direcionado pode refletir o perfil completo e o histórico de Mary, em vez de apenas um tablet usado por um comprador desconhecido.

Os relacionamentos de identidade que [!DNL Identity Service] define e mantém são aproveitados por [!DNL Real-time Customer Profile] para criar uma imagem completa de um cliente e suas interações com sua marca. Para obter mais informações, consulte a [Visão geral do Perfil do cliente em tempo real](../profile/home.md).

### Identidades

Uma identidade são dados exclusivos de uma entidade, normalmente uma pessoa individual. Uma identidade como uma ID de logon, ECID ou ID de fidelidade é chamada de identidade conhecida.

PII, como endereço de email e número de telefone, serve para identificar diretamente um cliente. Como resultado, a PII é usada para corresponder as várias identidades de um cliente em todos os sistemas.

Identidades desconhecidas ou anônimas identificam um dispositivo sem identificar a pessoa real que o usa. Esta categoria inclui informações como o endereço IP de um visitante e a ID do cookie. Embora os dados comportamentais possam ser coletados de um dispositivo usando identidades desconhecidas, a associação dessas identidades em dispositivos ou mídias é limitada até que o cliente forneça PII durante a jornada.

Conforme mostrado na imagem abaixo, identidades conhecidas e anônimas são componentes importantes de [gráficos de identidade](#identity-graphs), que são discutidos posteriormente neste documento.

![Compilação de identidade na plataforma](./images/identity-service-stitching.png)

Exemplos de implementações [!DNL Identity Service] incluem:

- Uma empresa de telecomunicações pode confiar no valor do &quot;número de telefone&quot;, onde um número de telefone se refere ao mesmo indivíduo de interesse tanto em conjuntos de dados offline quanto online.
- Uma empresa de varejo pode usar &quot;endereço de email&quot; em conjuntos de dados offline e ECID em conjuntos de dados online devido à alta porcentagem de visitantes anônimos.
- Um banco pode preferir &quot;número de conta&quot; em conjuntos de dados offline, como transações de ramificação. Eles podem depender da &quot;ID de logon&quot; em conjuntos de dados online, pois a maioria dos visitantes seria autenticada durante a visita.
- Seus clientes também podem ter IDs proprietárias exclusivas, como GUID ou outros identificadores universalmente exclusivos.

### Dados de identidade

Se você perguntou a uma pessoa &quot;Qual é sua ID?&quot; sem qualquer outro contexto, seria difícil para eles dar uma resposta útil. Pela mesma lógica, um valor de string que representa um valor de identidade, seja um ID gerado pelo sistema ou um endereço de email, só é concluído quando fornecido com um qualificador que fornece o contexto do valor da string: o namespace de identidade.

## Namespaces de identidade e gráficos de identidade

Os clientes podem interagir com a marca por meio de uma combinação de canais online e offline, resultando no desafio de como reconciliar essas interações fragmentadas em uma única identidade de cliente.

[!DNL Experience Platform] soluciona esse desafio por meio de dois conceitos:  [espaços de ](#identity-namespaces) nome de identidade e gráficos  [de identidade](#identity-graphs).

O vídeo a seguir destina-se a oferecer suporte à compreensão das identidades e gráficos de identidade. O vídeo a seguir aborda os três recursos da coleção de identidade, gráficos de identidade e as APIs. Também descreve como os algoritmos determinísticos e probabilísticos são usados para construir gráficos de identidade privada e discute a função dos gráficos de identidade privada, do Gráfico cooperativo do Serviço de Identidade da Adobe Experience Platform e de gráficos de terceiros.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### Namespaces de identidade

Quando o cliente interage com a marca em vários canais, incluindo a Web, o aplicativo móvel, a central de atendimento ou uma loja, pode ser difícil entendê-los e servi-los se não for possível observar e acompanhar a atividade deles em todos os canais.

Entender seu cliente em vários dispositivos e canais começa reconhecendo-os em cada canal. O Adobe Experience Platform faz isso usando namespaces de identidade.
Um namespace de identidade é um identificador como ID de dispositivo ou ID de email usado para fornecer o contexto a partir do qual os dados são originados. Os namespaces de identidade são usados para procurar ou vincular identidades individuais e fornecer contexto para valores de identidade para evitar colisões de dados. Por exemplo, a ID &quot;123456&quot; pode se referir a uma pessoa em seu sistema de comércio eletrônico e a uma pessoa diferente em seu sistema de suporte técnico. Para obter mais informações, consulte a [visão geral do namespace de identidade](./namespaces.md).

### Gráficos de identidade

Um gráfico de identidade é um mapa de relacionamentos entre diferentes namespaces de identidade, fornecendo uma representação visual de como seu cliente interage com sua marca em diferentes canais.

Todos os gráficos de identidade do cliente são gerenciados e atualizados coletivamente por [!DNL Identity Service] em tempo quase real, em resposta às atividades do cliente.

[!DNL Identity Service] O gerencia um gráfico de identidade visível somente pela sua organização e criado com base nos seus dados, conhecido como o gráfico privado. [!DNL Identity Service] aumenta seu gráfico privado quando um registro de dados assimilados contém mais de uma identidade, adicionando uma relação entre as identidades encontradas.

Como exemplo dos possíveis tipos de fatores a serem considerados ao fornecer e rotular dados de identidade, usar números de telefone como &quot;telefone de trabalho&quot; pode resultar em mais relacionamentos do que você pretende no gráfico de identidade. Você pode achar que muitos funcionários se referem ao mesmo número para o trabalho, e que a &quot;casa&quot; e a &quot;mobilidade&quot; servem para manter relações o mais precisas possível.

Para obter mais informações, consulte o tutorial em [acessar o visualizador de gráfico de identidade](./ui/identity-graph-viewer.md)

## Fornecimento de dados de identidade para [!DNL Identity Service]

Esta seção aborda como os dados fornecidos ao Adobe Experience Platform são processados antes de serem usados pelo [!DNL Identity Service] para criar um gráfico de identidade para cada cliente.

### Decidir em campos de identidade

Dependendo da estratégia de coleta de dados da empresa, os campos de dados que você rotular como identidades determinam quais dados serão incluídos em seu mapa de identidade. Para obter o máximo benefício do Adobe Experience Platform e as identidades mais abrangentes do cliente possíveis, você deve fazer upload de dados online e offline.

- Dados online são dados que descrevem a presença e o comportamento online, como nomes de usuário e endereços de email.

- Os dados offline se referem a dados que não estão diretamente relacionados à presença online, como IDs de sistemas CRM. Esse tipo de dado torna suas identidades mais robustas e oferece suporte à coesão de dados em diferentes sistemas.

### Criar namespaces de identidade adicionais

Embora [!DNL Experience Platform] ofereça uma variedade de namespaces padrão, talvez seja necessário criar namespaces adicionais para categorizar adequadamente suas identidades. Para obter mais informações, consulte a seção sobre [visualizar e criar namespaces para sua organização](./namespaces.md) na visão geral do namespace de identidade.

>[!NOTE]
>
>Os namespaces de identidade são um qualificador para identidades. Como resultado, depois que um namespace é criado, ele não pode ser excluído.

### Incluir dados de identidade em [!DNL Experience Data Model] (XDM)

Como a estrutura padronizada pela qual [!DNL Platform] organiza os dados do cliente, [!DNL Experience Data Model] (XDM) permite que os dados sejam compartilhados e compreendidos em [!DNL Experience Platform] e outros serviços que interagem com [!DNL Platform]. Para obter mais informações, consulte a [Visão geral do sistema XDM](../xdm/home.md).

Os esquemas de registro e de série de tempo fornecem os meios para incluir dados de identidade. À medida que os dados são assimilados, o gráfico de identidade criará novas relações entre fragmentos de dados de diferentes namespaces, se for encontrado que eles compartilham dados de identidade comuns.

### Marcar campos XDM como identidade

Qualquer campo do tipo `string` em esquemas que implementam classes XDM de registro ou de série de tempo pode ser rotulado como um campo de identidade. Como resultado, todos os dados assimilados nesse campo seriam considerados dados de identidade.

Os campos de identidade também permitem a vinculação de identidades se compartilharem dados PII comuns.
Por exemplo, ao rotular os campos de número de telefone como campos de identidade, [!DNL Identity Service] define automaticamente as relações com os outros indivíduos que estiverem usando o mesmo número de telefone.

>[!NOTE]
>
>O namespace das identidades resultantes é fornecido no momento em que o campo é rotulado.

### Configurar um conjunto de dados para [!DNL Identity Service]

Durante o processo de assimilação de streaming, [!DNL Identity Service ]extrai automaticamente os dados de identidade dos dados de registro e da série de tempo. No entanto, antes que os dados possam ser assimilados, eles devem ser ativados para [!DNL Identity Service]. Consulte o tutorial em [configurar um conjunto de dados para o Perfil do cliente em tempo real e o Serviço de identidade usando APIs](../profile/tutorials/dataset-configuration.md) para obter mais informações.

### Assimilar dados a [!DNL Identity Service]

[!DNL Identity Service] O consome dados compatíveis com XDM enviados para o  [!DNL Experience Platform] por ingestão  [em lote ou ](../ingestion/batch-ingestion/overview.md) assimilação de streaming [ ](../ingestion/streaming-ingestion/overview.md).

O vídeo a seguir serve para oferecer suporte à compreensão do serviço de identidade. Este vídeo mostra como rotular campos de dados como identidades, assimilar dados de identidade e, em seguida, verificar se os dados foram para o Gráfico privado do serviço de identidade da Adobe Experience Platform.

>[!WARNING]
>
>A interface [!DNL Platform] mostrada no vídeo a seguir está desatualizada. Consulte a documentação para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Governança de dados

A Adobe Experience Platform foi criada pensando na privacidade e inclui uma estrutura de governança de dados para proteger os dados de PII de seus clientes. Os dados de identidade no namespace &quot;email&quot; ou &quot;telefone&quot; são criptografados por padrão, mas para garantir que os dados confidenciais sejam criptografados antes de serem persistentes, os rótulos de uso de dados podem ser aplicados aos dados à medida que são assimilados ou após serem recebidos em [!DNL Platform]. Para obter mais informações, leia a [Visão geral da governança de dados](../data-governance/home.md).

## Próximas etapas

Agora que você entende os principais conceitos de [!DNL Identity Service] e sua função em [!DNL Experience Platform], pode começar a aprender a trabalhar com o gráfico de identidade usando o [[!DNL Identity Service API]](./api/getting-started.md).
