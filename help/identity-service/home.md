---
keywords: Experience Platform;home;popular topics;identity;Identity;XDM graphs;identity service;Identity service
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
description: O Adobe Experience Platform Identity Service ajuda você a obter uma melhor visualização de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real.
translation-type: tm+mt
source-git-commit: 8b1b61b6446b28f92d6cf221003674fa09716c53
workflow-type: tm+mt
source-wordcount: '1711'
ht-degree: 0%

---


# [!DNL Identity Service]visão geral

Fornecer experiências digitais relevantes requer uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;. A Adobe Experience Platform [!DNL Identity Service] ajuda você a obter uma melhor visualização de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real.

## Noções básicas do [!DNL Identity Service]

A cada dia, os clientes interagem com a sua empresa e estabelecem um relacionamento cada vez maior com a sua marca. Um cliente típico pode estar ativo em qualquer número de sistemas dentro da infraestrutura de dados de sua organização, como seu eCommerce, fidelidade e sistemas de suporte técnico. Esse mesmo cliente também pode se envolver anonimamente em qualquer número de dispositivos. [!DNL Identity Service] permite que você reúna uma imagem completa do seu cliente, agregando dados relacionados que podem ser colocados em sistemas diferentes.

Considere um exemplo diário da relação de um consumidor com a sua marca:

Mary tem uma conta em seu site de comércio eletrônico onde ela completou alguns pedidos no passado. Ela geralmente usa seu laptop pessoal para fazer compras, onde ela faz login a cada vez. No entanto, durante uma de suas visitas, ela usa seu tablet para comprar sandálias, mas não faz um pedido e não faz login.

Nesse ponto, a atividade de Maria aparece como dois perfis separados: seu login de eCommerce e seu tablet, talvez identificado pela ID do dispositivo.

Mary, mais tarde, retoma sua sessão em tablet e fornece seu endereço de email enquanto assina seu boletim informativo. Ao fazer isso, a ingestão em streaming acrescenta uma nova identidade como dados de registro dentro de seu perfil. Como resultado, [!DNL Identity Service] agora relaciona a atividade do tablet de Maria ao histórico de sua conta de comércio eletrônico.

Ao clicar em seu tablet, seu conteúdo direcionado pode refletir o perfil e a história completos de Mary, em vez de apenas um tablet usado por um comprador desconhecido.

Os relacionamentos de identidade que [!DNL Identity Service] definem e mantêm são aproveitados [!DNL Real-time Customer Profile] para criar uma imagem completa de um cliente e suas interações com sua marca. Para obter mais informações, consulte a visão geral [do Perfil do cliente em tempo](../profile/home.md)real.

### Identidades

Uma identidade são dados exclusivos de uma entidade, geralmente uma pessoa individual. Uma identidade como ID de login, ECID ou ID de fidelidade é chamada de identidade **** conhecida.

As PII, como endereço de email e número de telefone, servem para identificar diretamente um cliente. Como resultado, a PII é usada para corresponder as múltiplas identidades de um cliente nos sistemas.

**Identidades** desconhecidas ou anônimas identificam um dispositivo sem identificar a pessoa real que o utiliza. Esta categoria inclui informações como o endereço IP do visitante e a ID do cookie. Embora os dados comportamentais possam ser coletados de um dispositivo usando identidades desconhecidas, a associação dessas identidades em dispositivos ou mídias é limitada até que o cliente forneça PII durante sua jornada.

Como mostrado na imagem abaixo, identidades conhecidas e anônimas são componentes importantes dos gráficos [de](#identity-graphs)identidade, que são discutidos posteriormente neste documento.

![Ajuste de identidade na plataforma](./images/identity-service-stitching.png)

Exemplos de [!DNL Identity Service] implementações incluem:

- Uma empresa de telecom pode depender do valor do &quot;número de telefone&quot;, onde um número de telefone se refere ao mesmo indivíduo de interesse tanto em conjuntos de dados offline quanto online.
- Uma empresa de varejo pode usar &quot;endereço de email&quot; em conjuntos de dados offline e ECID em conjuntos de dados online devido à alta porcentagem de visitantes anônimos.
- Um banco pode preferir &quot;número de conta&quot; em conjuntos de dados offline, como transações de ramificação. Eles podem depender da &quot;ID de login&quot; em conjuntos de dados online, pois a maioria dos visitantes seria autenticada durante a visita.
- Seus clientes também podem ter IDs exclusivas, como GUID ou outros identificadores universalmente exclusivos.

### Dados de identidade

Se você perguntasse a uma pessoa &quot;Qual é a sua identificação?&quot; sem qualquer outro contexto, seria difícil para eles dar uma resposta útil. Pela mesma lógica, um valor de string que representa um valor de identidade, seja ele uma ID gerada pelo sistema ou um endereço de email, só é concluído quando fornecido com um qualificador que fornece o contexto do valor da string: a namespace de identidade.

## Namespaces de identidade e gráficos de identidade

Os clientes podem interagir com a sua marca através de uma combinação de canais online e offline, resultando no desafio de como reconciliar essas interações fragmentadas em uma única identidade de cliente.

[!DNL Experience Platform] soluciona esse desafio através de dois conceitos: [namespaces](#identity-namespaces) de identidade e gráficos [de](#identity-graphs)identidade.

O vídeo a seguir é destinado a suportar a compreensão de identidades e gráficos de identidade. O vídeo a seguir aborda os três recursos da coleção de identidade, gráficos de identidade e as APIs. Ele também descreve como os algoritmos determinísticos e probabilísticos são usados para construir gráficos de identidade privados e discute a função dos gráficos de identidade privados, do Gráfico de Cooperativa do Adobe Experience Platform Identity Service e de gráficos de terceiros.

>[!IMPORTANT]
>
> Gráficos privados probabilísticos ainda estão em desenvolvimento e estão definidos para serem lançados em uma data posterior.

>[!VIDEO](https://video.tv.adobe.com/v/27841?quality=12&learn=on)

### Namespaces de identidade

Quando seu cliente interage com sua marca em vários canais, incluindo Web, aplicativos móveis, call center ou uma loja, pode ser difícil entendê-los e servi-los caso você não consiga observar e rastrear a atividade nos canais.

Entendendo seu cliente em vários dispositivos e start, reconhecendo-os em cada canal. A Adobe Experience Platform consegue isso usando namespaces de identidade.
Uma namespace de identidade é um identificador, como ID de dispositivo ou ID de email, usado para fornecer o contexto de onde os dados se originam. As namespaces de identidade são usadas para procurar ou vincular identidades individuais e fornecem contexto para valores de identidade para evitar colisões de dados. Por exemplo, a ID &quot;123456&quot; pode se referir a uma pessoa em seu sistema de comércio eletrônico e a outra pessoa em seu sistema de suporte técnico. Para obter mais informações, consulte a visão geral [da namespace de](./namespaces.md)identidade.

### Gráficos de identidade

Um gráfico de identidade é um mapa de relações entre diferentes namespaces de identidade, fornecendo uma representação visual de como seu cliente interage com sua marca em diferentes canais.

Todos os gráficos de identidade do cliente são gerenciados e atualizados coletivamente [!DNL Identity Service] em tempo quase real, em resposta à atividade do cliente.

[!DNL Identity Service] gerencia um gráfico de identidade visível somente pela sua organização e criado com base em seus dados, conhecido como gráfico privado. [!DNL Identity Service] aumenta seu gráfico particular quando um registro de dados assimilados contém mais de uma identidade, adicionando uma relação entre as identidades encontradas.

Como exemplo dos possíveis tipos de fatores a serem considerados ao fornecer e rotular dados de identidade, o uso de números de telefone como &quot;telefone de trabalho&quot; pode resultar em mais relacionamentos do que você pretende no gráfico de identidade. Você pode achar que muitos funcionários se referem ao mesmo número para o trabalho, e que &quot;casa&quot; e &quot;móvel&quot; servem melhor para manter relações o mais precisas possível.

## Fornecimento de dados de identidade para [!DNL Identity Service]

Esta seção aborda como os dados fornecidos à Adobe Experience Platform são processados antes de serem usados [!DNL Identity Service] para criar um gráfico de identidade para cada cliente.

### Decidir sobre campos de identidade

Dependendo da sua estratégia de coleta de dados corporativos, os campos de dados rotulados como identidades determinam quais dados são incluídos no mapa de identidade. Para obter o máximo benefício da Adobe Experience Platform e as identidades de clientes mais abrangentes possíveis, faça upload de dados online e offline.

- Dados online são dados que descrevem a presença e o comportamento online, como nomes de usuário e endereços de email.

- Os dados offline se referem a dados que não estão diretamente relacionados à presença online, como IDs de sistemas CRM. Esse tipo de dados torna suas identidades mais robustas e oferece suporte à coesão de dados entre seus diferentes sistemas.

### Criar namespaces de identidade adicionais

Ao [!DNL Experience Platform] oferta uma variedade de namespaces padrão, talvez seja necessário criar namespaces adicionais para categorizar suas identidades corretamente. Para obter mais informações, consulte a seção sobre como [visualizar e criar namespaces para sua organização](./namespaces.md) na visão geral da namespace de identidade.

>[!NOTE]
>
>Namespaces de identidade são qualificadores de identidades. Como resultado, uma vez que uma namespace é criada, ela não pode ser excluída.

### Incluir dados de identidade em [!DNL Experience Data Model] (XDM)

Como a estrutura padronizada pela qual [!DNL Platform] organiza os dados do cliente, [!DNL Experience Data Model] (XDM) permite que os dados sejam compartilhados e entendidos entre [!DNL Experience Platform] e outros serviços que interagem com [!DNL Platform]. Para obter mais informações, consulte a visão geral [do Sistema](../xdm/home.md)XDM.

Os schemas de registro e de série cronológica fornecem os meios para incluir dados de identidade. À medida que os dados são ingeridos, o gráfico de identidade criará novas relações entre fragmentos de dados de diferentes namespaces, se forem encontrados para compartilhar dados de identidade comuns.

### Marcar campos XDM como identidade

Qualquer campo do tipo `string` nos schemas que implementam classes XDM de registro ou de série de tempo pode ser rotulado como um campo de identidade. Como resultado, todos os dados ingeridos nesse campo seriam considerados dados de identidade.

Os campos de identidade também permitem a vinculação de identidades se compartilharem dados PII comuns.
Por exemplo, ao rotular os campos de número de telefone como campos de identidade, [!DNL Identity Service] o gráfico automaticamente relacionamentos com os outros indivíduos encontrados usando o mesmo número de telefone.

>[!NOTE]
>
>A namespace das identidades resultantes é fornecida no momento em que o campo é rotulado.

### Configurar um conjunto de dados para [!DNL Identity Service]

Durante o processo de ingestão em streaming, extrai [!DNL Identity Service ]automaticamente os dados de identidade dos dados de registro e da série de tempo. No entanto, antes que os dados possam ser ingeridos, eles devem estar habilitados para [!DNL Identity Service]. Consulte o tutorial sobre como [configurar um conjunto de dados para o Perfil do cliente em tempo real e o serviço de identidade usando APIs](../profile/tutorials/dataset-configuration.md) para obter mais informações.

### Ingressar dados em [!DNL Identity Service]

[!DNL Identity Service] consome dados em conformidade com XDM enviados para [!DNL Experience Platform] a ingestão [em](../ingestion/batch-ingestion/overview.md) lote ou a ingestão [em](../ingestion/streaming-ingestion/overview.md)streaming.

O vídeo a seguir é destinado a suportar sua compreensão do Serviço de identidade. Este vídeo mostra como rotular campos de dados como identidades, assimilar dados de identidade e, em seguida, verificar se os dados foram enviados para o Gráfico Privado do Adobe Experience Platform Identity Service.

>[!WARNING]
>
> A [!DNL Platform] interface do usuário exibida no vídeo a seguir está desatualizada. Consulte a documentação para obter as capturas de tela e a funcionalidade mais recentes da interface do usuário.

>[!VIDEO](https://video.tv.adobe.com/v/28167?quality=12&learn=on)

## Governação de dados

A Adobe Experience Platform foi criada pensando na privacidade e inclui uma estrutura de controle de dados para proteger seus dados de PII do cliente. Os dados de identidade na namespace &quot;email&quot; ou &quot;telefone&quot; são criptografados por padrão, mas para garantir que os dados confidenciais sejam criptografados antes de serem persistentes, os rótulos de uso de dados podem ser aplicados aos dados à medida que são ingeridos ou quando chegam [!DNL Platform]. Para obter mais informações, leia a visão geral [do](../data-governance/home.md)Data Governance.

## Próximas etapas

Agora que você entende os conceitos principais de [!DNL Identity Service] e sua função dentro de [!DNL Experience Platform], você pode começar a aprender como trabalhar com seu gráfico de identidade usando a API [[!DNL Identity Service]](./api/getting-started.md).
