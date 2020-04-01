---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Identity Service
topic: overview
translation-type: tm+mt
source-git-commit: df85ea955b7a308e6be1e2149fcdfb4224facc53

---


# Visão geral do Serviço de identidade

Fornecer experiências digitais relevantes requer uma compreensão completa do cliente. Isso fica mais difícil quando os dados do cliente são fragmentados em sistemas diferentes, fazendo com que cada cliente individual pareça ter várias &quot;identidades&quot;. O Adobe Experience Platform Identity Service ajuda você a obter uma melhor visualização de seu cliente e de seu comportamento ao unir identidades entre dispositivos e sistemas, permitindo que você forneça experiências digitais pessoais e de impacto em tempo real.

## Noções básicas sobre o serviço de identidade

A cada dia, os clientes interagem com a sua empresa e estabelecem um relacionamento cada vez maior com a sua marca. Um cliente típico pode estar ativo em qualquer número de sistemas dentro da infraestrutura de dados de sua organização, como seu eCommerce, fidelidade e sistemas de suporte técnico. Esse mesmo cliente também pode se envolver anonimamente em qualquer número de dispositivos. O Serviço de identidade permite que você reúna uma imagem completa do seu cliente, agregando dados relacionados que, de outra forma, poderiam ser colocados em diferentes sistemas.

Considere um exemplo diário da relação de um consumidor com a sua marca:

Mary tem uma conta em seu site de comércio eletrônico onde ela completou alguns pedidos no passado. Ela geralmente usa seu laptop pessoal para fazer compras, onde ela faz login a cada vez. No entanto, durante uma de suas visitas, ela usa seu tablet para comprar sandálias, mas não faz um pedido e não faz login.

Nesse ponto, a atividade de Maria aparece como dois perfis separados: seu login de eCommerce e seu tablet, talvez identificado pela ID do dispositivo.

Mary, mais tarde, retoma sua sessão em tablet e fornece seu endereço de email enquanto assina seu boletim informativo. Ao fazer isso, a ingestão em streaming acrescenta uma nova identidade como dados de registro dentro de seu perfil. Como resultado, o Serviço de Identidade agora relaciona a atividade do tablet de Mary com o histórico de sua conta de eCommerce.

Ao clicar em seu tablet, seu conteúdo direcionado pode refletir o perfil e a história completos de Mary, em vez de apenas um tablet usado por um comprador desconhecido.

Os relacionamentos de identidade que o Serviço de Identidade define e mantém são aproveitados pelo Perfil do Cliente em tempo real para criar uma imagem completa de um cliente e suas interações com sua marca. Para obter mais informações, consulte a visão geral [do Perfil do cliente em tempo](../profile/home.md)real.

### Identidades

Uma identidade são dados exclusivos de uma entidade, geralmente uma pessoa individual. Uma identidade como ID de login, ECID ou ID de fidelidade é chamada de identidade **** conhecida.

As PII, como endereço de email e número de telefone, servem para identificar diretamente um cliente. Como resultado, a PII é usada para corresponder às múltiplas identidades de um cliente nos sistemas.

**Identidades** desconhecidas ou anônimas identificam um dispositivo sem identificar a pessoa real que o utiliza. Esta categoria inclui informações como o endereço IP do visitante e a ID do cookie. Embora os dados comportamentais possam ser coletados de um dispositivo usando identidades desconhecidas, a associação dessas identidades em dispositivos ou mídias é limitada até que o cliente forneça PII durante sua jornada.

Como mostrado na imagem abaixo, identidades conhecidas e anônimas são componentes importantes dos gráficos [de](#identity-graphs)identidade, que são discutidos posteriormente neste documento.

![Ajuste de identidade na plataforma](./images/identity-service-stitching.png)

Exemplos de implementações do Serviço de identidade incluem:

- Uma empresa de telecom pode depender do valor do &quot;número de telefone&quot;, onde um número de telefone se refere ao mesmo indivíduo de interesse tanto em conjuntos de dados offline quanto online.
- Uma empresa de varejo pode usar &quot;endereço de email&quot; em conjuntos de dados offline e ECID em conjuntos de dados online devido à alta porcentagem de visitantes anônimos.
- Um banco pode preferir &quot;número de conta&quot; em conjuntos de dados offline, como transações de ramificação. Eles podem depender da &quot;ID de login&quot; em conjuntos de dados online, pois a maioria dos visitantes seria autenticada durante a visita.
- Seus clientes também podem ter IDs exclusivas, como GUID ou outros identificadores universalmente exclusivos.

### Dados de identidade

Se você perguntasse a uma pessoa &quot;Qual é a sua identificação?&quot; sem qualquer outro contexto, seria difícil para eles dar uma resposta útil. Pela mesma lógica, um valor de string que representa um valor de identidade, seja ele uma ID gerada pelo sistema ou um endereço de email, só é concluído quando fornecido com um qualificador que fornece o contexto do valor da string: a namespace de identidade.

## namespaces de identidade e gráficos de identidade

Os clientes podem interagir com a sua marca através de uma combinação de canais online e offline, resultando no desafio de como reconciliar essas interações fragmentadas em uma única identidade de cliente.

A plataforma Experience soluciona esse desafio através de dois conceitos: namespaces [de](#identity-namespaces) identidade e gráficos [de](#identity-graphs)identidade.

### namespaces de identidade

Quando seu cliente interage com sua marca em vários canais, incluindo Web, aplicativos móveis, call center ou uma loja, pode ser difícil entendê-los e servi-los caso você não consiga observar e rastrear a atividade nos canais.

Entendendo seu cliente em vários dispositivos e start, reconhecendo-os em cada canal. A Adobe Experience Platform consegue isso usando namespaces de identidade.
Uma namespace de identidade é um identificador, como ID de dispositivo ou ID de email, usado para fornecer o contexto de onde os dados se originam. As namespaces de identidade são usadas para procurar ou vincular identidades individuais e fornecem contexto para valores de identidade para evitar colisões de dados. Por exemplo, a ID &quot;123456&quot; pode se referir a uma pessoa em seu sistema de comércio eletrônico e a outra pessoa em seu sistema de suporte técnico. Para obter mais informações, consulte a visão geral [da namespace de](./namespaces.md)identidade.

### Gráficos de identidade

Um gráfico de identidade é um mapa de relações entre diferentes namespaces de identidade, fornecendo uma representação visual de como seu cliente interage com sua marca em diferentes canais.

Todos os gráficos de identidade do cliente são gerenciados e atualizados coletivamente pelo Serviço de identidade em tempo quase real, em resposta à atividade do cliente.

O Serviço de identidade gerencia um gráfico de identidade visível somente pela sua organização e criado com base nos seus dados, conhecido como gráfico privado. O Serviço de identidade aumenta seu gráfico particular quando um registro de dados ingeridos contém mais de uma identidade, adicionando uma relação entre as identidades encontradas.

Como exemplo dos possíveis tipos de fatores a serem considerados ao fornecer e rotular dados de identidade, o uso de números de telefone como &quot;telefone de trabalho&quot; pode resultar em mais relacionamentos do que você pretende no gráfico de identidade. Você pode achar que muitos funcionários se referem ao mesmo número para o trabalho, e que &quot;casa&quot; e &quot;móvel&quot; servem melhor para manter relações o mais precisas possível.

## Fornecimento de dados de identidade ao Serviço de Identidade

Esta seção aborda como os dados fornecidos à Adobe Experience Platform são processados antes de serem usados pelo Serviço de identidade para criar um gráfico de identidade para cada cliente.

### Decidir sobre campos de identidade

Dependendo da sua estratégia de coleta de dados corporativos, os campos de dados rotulados como identidades determinam quais dados são incluídos no mapa de identidade. Para obter o máximo benefício da Adobe Experience Platform e as identidades de clientes mais abrangentes possíveis, faça upload de dados online e offline.

- Dados online são dados que descrevem a presença e o comportamento online, como nomes de usuário e endereços de email.

- Os dados offline se referem a dados que não estão diretamente relacionados à presença online, como IDs de sistemas CRM. Esse tipo de dados torna suas identidades mais robustas e oferece suporte à coesão de dados entre seus diferentes sistemas.

### Criar namespaces de identidade adicionais

Embora a Experience Platform oferta uma variedade de namespaces padrão, talvez seja necessário criar namespaces adicionais para categorizar suas identidades corretamente. Para obter mais informações, consulte a seção sobre como [visualizar e criar namespaces para sua organização](./namespaces.md) na visão geral da namespace de identidade.

>[!NOTE] namespaces de identidade são qualificadores de identidades. Como resultado, uma vez que uma namespace é criada, ela não pode ser excluída.

### Incluir dados de identidade no Modelo de Dados de Experiência (XDM)

Como a estrutura padronizada pela qual a Plataforma organiza os dados do cliente, o Experience Data Model (XDM) permite que os dados sejam compartilhados e compreendidos na Experience Platform e em outros serviços que interagem com a Plataforma. Para obter mais informações, consulte a visão geral [do Sistema](../xdm/home.md)XDM.

Os schemas de registro e de série cronológica fornecem os meios para incluir dados de identidade. À medida que os dados são ingeridos, o gráfico de identidade criará novas relações entre fragmentos de dados de diferentes namespaces, se forem encontrados para compartilhar dados de identidade comuns.

### Marcar campos XDM como identidade

Qualquer campo do tipo `string` nos schemas que implementam classes XDM de registro ou de série de tempo pode ser rotulado como um campo de identidade. Como resultado, todos os dados ingeridos nesse campo seriam considerados dados de identidade.

Os campos de identidade também permitem a vinculação de identidades se compartilharem dados PII comuns.
Por exemplo, ao rotular os campos de número de telefone como campos de identidade, o Serviço de identidade automaticamente atribui gráficos às relações com os outros indivíduos que se encontram usando o mesmo número de telefone.

>[!NOTE] A namespace das identidades resultantes é fornecida no momento em que o campo é rotulado.

### Configurar um conjunto de dados para o serviço de identidade

Durante o processo de ingestão em streaming, o Serviço de identidade extrai automaticamente os dados de identidade dos dados de registro e da série de tempo. No entanto, antes que os dados possam ser ingeridos, eles devem estar habilitados para o Serviço de identidade. Consulte o tutorial sobre como [configurar um conjunto de dados para o Perfil do cliente em tempo real e o serviço de identidade usando APIs](../profile/tutorials/dataset-configuration.md) para obter mais informações.

### Ingressar dados no Serviço de identidade

O Serviço de identidade consome dados compatíveis com XDM enviados para a Experience Platform por ingestão [em](../ingestion/batch-ingestion/overview.md) lote ou ingestão em [streaming](../ingestion/streaming-ingestion/overview.md).

## Governação de dados

A plataforma Adobe Experience foi criada pensando na privacidade e inclui uma estrutura de controle de dados para proteger os dados de PII do cliente. Os dados de identidade na namespace &quot;email&quot; ou &quot;telefone&quot; são criptografados por padrão, mas para garantir que os dados confidenciais sejam criptografados antes de serem persistentes, os rótulos de uso de dados podem ser aplicados aos dados à medida que são ingeridos ou quando chegam à Plataforma. Para obter mais informações, leia a visão geral [do](../data-governance/home.md)Data Governance.

## Próximas etapas

Agora que você entende os conceitos principais do Serviço de identidade e sua função na plataforma Experience, é possível começar a aprender a trabalhar com seu gráfico de identidade usando a API [do Serviço de](./api/getting-started.md)identidade.