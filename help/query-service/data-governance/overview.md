---
title: Governança de dados no serviço de query
description: Esta visão geral aborda os principais elementos do controle de dados no Experience Platform Query Service.
feature: Data Governance
source-git-commit: ec063a0f5600729d3575f98898ade04443f29f2a
workflow-type: tm+mt
source-wordcount: '2667'
ht-degree: 0%

---

# Governança de dados no Serviço de query

O Adobe Experience Platform reúne dados de vários sistemas corporativos e permite limpar, modelar, manipular e enriquecer os dados por meio do Serviço de query de acordo com suas necessidades. Isso permite que os profissionais de marketing identifiquem, entendam e envolvam os clientes de uma maneira melhor. Garantir o controle adequado dos dados é um aspecto essencial do tratamento de informações pessoais, pois alguns dados podem estar sujeitos a restrições de uso com base em políticas organizacionais e regulamentos legais. É importante garantir que seus dados assimilados e suas operações relacionadas estejam em conformidade com as políticas de uso de dados definidas.

O controle de dados no Serviço de query permite gerenciar os dados do cliente e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados. Isso desempenha um papel fundamental ao garantir que as políticas de uso tenham sido aplicadas de acordo com os regulamentos definidos pela sua empresa.

As organizações que rotineiramente realizam processamento de dados são recomendadas para esboçar, praticar e aplicar essas diretrizes para criar um ambiente com consciência de privacidade para todos os usuários.

As seguintes categorias são fundamentais para seguir as regras de conformidade de dados ao usar o Serviço de query:

1. Segurança
1. Auditoria
1. Uso de dados
1. Privacidade
<!-- 1. Data hygiene -->

Este documento examina cada uma das diferentes áreas de controle e demonstra como facilitar a conformidade dos dados ao usar o Serviço de query. Consulte a [visão geral de governança, privacidade e segurança](../../landing/governance-privacy-security/overview.md) para obter mais informações sobre como o Experience Platform permite gerenciar os dados do cliente e garantir a conformidade.

## Segurança

A segurança de dados é o processo de proteção de dados contra acesso não autorizado e de garantia de acesso seguro durante todo o seu ciclo de vida. O acesso seguro é mantido no Experience Platform por meio da aplicação de funções e permissões por recursos como controle de acesso baseado em funções e controle de acesso baseado em atributos. Credenciais, SSL e criptografia de dados também são usadas para garantir a proteção de dados na plataforma.

A segurança em relação ao Serviço de query é dividida nas seguintes categorias:

* [Controle de acesso](#access-control): O acesso é controlado por meio de funções e permissões, incluindo permissões de conjunto de dados e nível de coluna.
* Proteção de dados por meio de [conectividade](#connectivity): Os dados são protegidos por meio da Platform e de clientes externos ao obter uma conexão limitada com credenciais que estão expirando ou credenciais que não estão expirando.
* Proteção de dados por meio de [criptografia e chaves de nível de sistema](#encryption): A segurança dos dados é assegurada por meio de criptografia quando os dados estiverem em repouso.

<!-- * Securing data through [encryption and customer-managed keys (CMK)](#encryption-and-customer-managed-keys): Access controlled through encryption when data is at rest. -->

### Controle de acesso {#access-control}

O controle de acesso no Adobe Experience Platform permite usar [Adobe Admin Console](https://adminconsole.adobe.com/) para gerenciar o acesso aos recursos do Serviço de query usando permissões com base em funções. Da mesma forma, é possível controlar o acesso a atributos de dados específicos por meio do gerenciamento de rótulos em esquemas e campos de dados.

Esta seção descreve as permissões de controle de acesso necessárias que um usuário deve ter para utilizar totalmente os recursos do Serviço de query. Veja os documentos em [gerenciamento de permissões](../../access-control/ui/permissions.md) e [gerenciamento de usuários](../../access-control/ui/users.md) para obter instruções detalhadas sobre como atribuir acesso a um perfil de produto.

#### Permissões relevantes

As permissões de controle de acesso relevantes são definidas nas tabelas abaixo de acordo com seu nível de escopo.

**Permissões de execução de query**

Para executar consultas no Serviço de Consulta, é necessário atribuir uma função a um usuário com a seguinte permissão:

| Permissão | Descrição |
|---|---|
| [!UICONTROL Gerenciar Consultas] | Essa permissão permite que os usuários executem consultas de exploração de dados e em lote, que podem ler um conjunto de dados existente ou gravar dados em conjuntos de dados. Isso inclui ambas `CREATE TABLE AS SELECT` (`CTAS`) e `INSERT INTO AS SELECT` (`ITAS`). |

**Permissões do conjunto de dados**

Esta seção serve como um guia para o acesso com base em recursos necessário para acessar conjuntos de dados ao consultar dados por meio do Serviço de query.

Na interface de Permissões, é possível definir o controle de acesso com base em recursos para um conjunto de dados e esquema com as seguintes permissões:

| Permissão | Descrição |
|---|---|
| [!UICONTROL Gerenciar conjuntos de dados] | Essa permissão fornece acesso somente leitura a esquemas e permite acesso para ler, criar, editar e excluir conjuntos de dados para uso com o Serviço de query. |
| [!UICONTROL Visualizar conjuntos de dados] | Essa permissão permite acesso somente leitura para conjuntos de dados e esquemas para uso com o Serviço de query. |

#### Controle de acesso para colunas/campos

O recurso de controle de acesso baseado em atributos permite que os usuários do Serviço de query restrinjam o acesso a dados críticos do usuário. O acesso pode ser concedido ou restrito com base nas permissões atribuídas a uma função. O acesso do usuário a colunas individuais é controlado pelos rótulos de uso de dados relevantes e pelos conjuntos de permissões aplicados às funções atribuídas aos usuários.

A marcação de grupos de campos de esquema e classes com rótulos de uso de dados aplica restrições de uso de dados a todos os esquemas com os mesmos grupos de campos e classes. Consulte a visão geral em [controle de acesso baseado em atributo](../../access-control/abac/overview.md) para obter informações abrangentes sobre esse recurso.

Este recurso permite que você conceda direitos de acesso em colunas confidenciais aos grupos de usuários de sua escolha. O controle de acesso em uma coluna pode restringir os recursos de leitura e gravação de um tipo específico de usuário.

O controle de acesso para colunas pode ser aplicado no nível de schema para schemas padrão e ad hoc. Aplique rótulos de uso de dados a esquemas XDM para restringir o acesso a uma ou mais colunas. A rotulagem de dados é aplicada de forma consistente, mesmo para conjuntos de dados criados pelo Serviço de query usando um esquema predefinido ou um schema ad hoc gerado como parte da operação CTAS.

Depois que o nível apropriado de acesso for aplicado usando rótulos e funções, o seguinte comportamento do sistema ocorrerá quando um usuário tentar acessar os dados não acessíveis:

1. Se um usuário tiver acesso negado a uma das colunas em um schema, ele também terá permissão para ler ou gravar na coluna restrita. Isso se aplica aos seguintes cenários comuns:

   * **Caso 1**: Quando um usuário tenta executar um query afetando apenas uma coluna restrita, o sistema gera um erro informando que a coluna não existe.
   * **Caso 2**: Quando um usuário tenta executar um query com várias colunas, incluindo uma coluna restrita, o sistema retorna a saída somente para todas as colunas não restritas.

1. Se um usuário tentar acessar um campo calculado, ele precisará ter acesso a todos os campos usados na composição ou o sistema também negará acesso ao campo calculado.

#### Controles de acesso para exibições

O Serviço de Consulta fornece a capacidade de utilizar o SQL ANSI padrão para [`CREATE VIEW`](../sql/syntax.md#create-view) instruções. Para workflows de dados altamente confidenciais, você deve aplicar controles apropriados ao criar exibições.

O `CREATE VIEW` palavra-chave define uma view de uma query, mas a view não é materializada fisicamente. Em vez disso, a consulta é executada sempre que a exibição for referenciada em uma query. Quando um usuário cria uma visualização a partir de um conjunto de dados, as regras de controle de acesso baseadas em função e atributo para o conjunto de dados pai são **not** aplicado hierarquicamente. Como resultado, você deve definir explicitamente as permissões em cada uma das colunas quando uma exibição for criada.

### Conectividade {#connectivity}

O Serviço de query é acessível por meio da interface do usuário da plataforma ou formando uma conexão com clientes compatíveis externos. O acesso a todas as fronts disponíveis é controlado por um conjunto de credenciais.

#### Conectividade por meio de clientes externos

O acesso ao Serviço de query usando um cliente de terceiros requer credenciais para autorização. Essas credenciais são obrigatórias para acessar o Serviço de query com qualquer um dos clientes externos compatíveis. Você pode se conectar a clientes externos usando [credenciais que expiram](#expiring-credentials) ou [credenciais que não expiram](#non-expiring-credentials).

#### Tempo de conexão limitado por meio de credenciais de expiração {#expiring-credentials}

[Credenciais de expiração](../ui/credentials.md) permitir que os usuários formem uma conexão temporária com um cliente externo. Este conjunto de credenciais é válido apenas por 24 horas. A expiração desses tipos de credenciais pode ser vista junto com a guia credencial no painel Serviço de query .

![A guia credenciais no espaço de trabalho Serviço de Consulta com credenciais que estão expirando está realçada.](../images/data-governance/overview/expiring-credentials.png)

#### Credenciais que não expiram {#non-expiring-credentials}

[Credenciais que não expiram](../ui/credentials.md#non-expiring-credentials) permite que você forme uma conexão permanente com um cliente externo, facilitando a conexão com o Serviço de query sem precisar de uma senha manual.

Para habilitar a opção de geração de credenciais que não estão expirando, você deve seguir o procedimento descrito [fluxo de trabalho de pré-requisitos](../ui/credentials.md#prerequisites). Como parte desse processo, o administrador da organização deve configurar permissões para o perfil do produto, fornecendo ao administrador controle sobre quais contas têm acesso para usar credenciais que não estão expirando.

As contas de usuário técnico permitidas com credenciais que não expiram podem receber funções para garantir o controle de dados apropriado, definindo o escopo de seu acesso de leitura e gravação com base em suas responsabilidades e necessidades. Consulte a seção anterior em [uso de permissões com base em funções por meio do controle de acesso](#access-control) para gerenciar o acesso ao Serviço de query.

Depois que o fluxo de trabalho de pré-requisito for concluído, os usuários autorizados poderão [gerar as credenciais de conexão necessárias](../ui/credentials.md#generate-credentials).

#### Criptografia de dados SSL

Para maior segurança, o Serviço de Consulta fornece suporte nativo para conexões SSL para criptografar comunicações cliente/servidor. A Platform oferece suporte a várias opções SSL para atender às suas necessidades de segurança de dados e equilibrar a sobrecarga de processamento da criptografia e da troca de chaves.

Consulte o guia sobre [Opções de SSL para conexões de clientes de terceiros com o Serviço de query](../clients/ssl-modes.md) para obter mais informações, incluindo como se conectar usando o `verify-full` Valor do parâmetro SSL.

### Criptografia {#encryption}

<!-- Commented out lines to be included when customer-managed keys is released. Link out to the new document. -->

<!-- ### Encryption and customer-managed keys (CMK) {#encryption-and-customer-managed-keys} -->

A criptografia é o uso de um processo algorítmico para transformar dados em texto codificado e ilegível, para garantir que as informações sejam protegidas e inacessíveis sem uma chave de descriptografia.

A conformidade dos dados do Serviço de query garante que os dados sejam sempre criptografados. Os dados em trânsito são sempre compatíveis com HTTPS e os dados em repouso são criptografados em um armazenamento do Azure Data Lake usando chaves de nível de sistema. Consulte a documentação em [como os dados são criptografados no Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/landing/governance-privacy-security/encryption.html) para obter mais informações. Para obter detalhes sobre como os dados em repouso são criptografados no Armazenamento Azure Data Lake, consulte o [documentação oficial do Azure](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-encryption).

<!-- Data-in-transit is always HTTPS compliant and similarly when the data is at rest in the data lake, the encryption is done with Customer Management Key (CMK), which is already supported by Data Lake Management. The currently supported version is TLS1.2. -->

## Auditoria {#audit}

O Serviço de Consulta registra a atividade do usuário e categoriza essa atividade em diferentes tipos de log. Registra informações de fornecimento em **who** executado **what** e **when**. Cada ação registrada em um log contém metadados que indicam o tipo de ação, a data e a hora, a ID do email do usuário que executou a ação e atributos adicionais relevantes ao tipo de ação.

Qualquer uma das categorias de log pode ser solicitada, conforme desejado, por um usuário da plataforma. Esta seção fornece detalhes sobre o tipo de informações capturadas para o Serviço de query e onde essas informações podem ser acessadas.

### Logs de consulta {#query-logs}

A interface do usuário dos logs de consulta permite monitorar e revisar detalhes de execução de todas as consultas que foram executadas por meio do Editor de consultas ou da API do Serviço de consulta. Isso gera transparência nas atividades do Serviço de query, permitindo verificar os metadados de **all** as consultas que foram executadas no Serviço de query. Ele inclui todos os tipos de queries, seja uma consulta exploratória, em lote ou programada.

Os logs de query podem ser acessados por meio da interface do usuário da plataforma no [!UICONTROL Logs] da guia [!UICONTROL Queries] espaço de trabalho.

![A guia Query log com o painel de detalhes realçado.](../images/data-governance/overview/queries-log.png)

### Logs de auditoria {#audit-logs}

Os logs de auditoria contêm informações mais detalhadas do que os logs de consulta e permitem filtrar logs com base em atributos como usuário, data, tipo de consulta e assim por diante. Além dos detalhes disponíveis na interface do usuário do log de consultas, os Logs de Auditoria armazenam detalhes sobre usuários individuais, juntamente com seus dados de sessão ou conectividade com um cliente de terceiros.

Ao fornecer um registro exato das ações do usuário, uma trilha de auditoria pode ajudar na solução de problemas e ajudar sua empresa a cumprir com eficácia as políticas corporativas de gerenciamento de dados e os requisitos normativos. Os logs de auditoria fornecem um registro de todas as atividades da plataforma. Com logs de auditoria, você pode auditar ações de usuários relacionadas à execução de consultas, modelos e consultas agendadas para aumentar a transparência e a visibilidade de ações executadas por usuários no Serviço de query.

A tabela a seguir indica as categorias de query capturadas pelos logs de auditoria e os tipos de ação que eles registram:

| Categoria | Tipo de ação |
|---|---|
| Consulta | Executar |
| Modelo de consulta | Criar, Excluir, Atualizar |
| Consulta agendada | Criar, Excluir, Atualizar |

Abaixo está uma lista de três logs estendidos do servidor que contêm mais detalhes que aqueles encontrados nos logs de consulta. Os logs estendidos são encontrados nas categorias de consulta de logs de auditoria:

1. **Logs de Meta Query**: Quando um query é executado, várias subconsultas de backend associadas (como análise) são executadas. Esses tipos de queries são conhecidos como queries de &quot;metadados&quot;. Seus detalhes relevantes podem ser encontrados em logs de auditoria.
1. **Logs da sessão**: O sistema cria um log de entrada de sessão para um usuário quando ele faz logon no Serviço de query, independentemente de executar um query.
1. **Registros de conexão de cliente de terceiros**: Um log de auditoria de conectividade é gerado quando um usuário conecta com êxito o Serviço de query a um cliente de terceiros.

Consulte a [visão geral dos logs de auditoria](../../landing/governance-privacy-security/audit-logs/overview.md) para obter mais informações sobre como os logs de auditoria podem ajudar sua organização a abordar a conformidade dos dados.

## Uso de dados {#data-usage}

A estrutura de Governança de dados na plataforma oferece uma maneira uniforme de usar os dados de forma responsável em todas as soluções, serviços e plataformas do Adobe. Ela coordena a abordagem sistêmica para capturar, comunicar e usar metadados em toda a Adobe Experience Cloud. Isso, por sua vez, ajuda os controladores de dados a rotular dados de acordo com as ações de marketing necessárias e as restrições colocadas nesses dados a partir dessas ações de marketing pretendidas. Consulte a visão geral em [rótulos de uso de dados](../../data-governance/labels/overview.md) para obter mais informações sobre como a Governança de dados permite aplicar rótulos de uso de dados a conjuntos de dados e campos.

É uma prática recomendada trabalhar para a conformidade dos dados em cada fase da jornada dos dados. Para isso, os conjuntos de dados derivados que usam esquemas ad hoc devem ser adequadamente rotulados como parte da estrutura de Governança de dados. Há dois tipos de conjuntos de dados derivados formados pelo Serviço de query: conjuntos de dados que usam um esquema padrão e conjuntos de dados que usam um esquema ad hoc.

>[!NOTE]
>
>Os conjuntos de dados criados usando o Serviço de query são chamados de &quot;conjuntos de dados derivados&quot;.

À medida que os esquemas ad hoc são criados por um usuário individual para uma finalidade específica, os campos do esquema XDM são namespacados para esse conjunto de dados específico e não são destinados ao uso em conjuntos de dados diferentes. Como resultado, os esquemas ad hoc não estão visíveis por padrão na interface do usuário do Experience Platform. Embora não haja diferença na aplicação de rótulos de uso de dados entre esquemas padrão e ad hoc, os esquemas ad hoc criados pelo Serviço de query para a finalidade de rotulagem devem primeiro ficar visíveis na interface do usuário da plataforma. Consulte o guia sobre [descoberta de esquemas ad hoc na interface do usuário da plataforma](./ad-hoc-schema-labels.md#discover-ad-hoc-schemas) para obter mais detalhes.

Após acessar o esquema, é possível [aplicar rótulos a campos individuais](../../xdm/tutorials/labels.md). Depois que um esquema é rotulado, todos os conjuntos de dados que derivam desse esquema herdam esses rótulos. A partir daqui, você pode configurar políticas de uso de dados que podem impedir que dados com determinados rótulos sejam ativados para determinados destinos. Para obter mais informações, consulte a visão geral em [políticas de uso de dados](../../data-governance/policies/overview.md).

## Privacidade {#privacy}

[Privacy Service](../../privacy-service/home.md) O ajuda a gerenciar solicitações de clientes para acessar e excluir seus dados de acordo com as regulamentações legais de privacidade. Ele faz isso pesquisando os dados para identificadores pré-existentes e acessa ou exclui esses dados, dependendo do trabalho de privacidade solicitado. Os dados devem ser rotulados corretamente para que o serviço determine quais campos devem ser acessados ou excluídos durante as tarefas de privacidade. Os dados sujeitos a solicitações de privacidade devem conter informações de identidade do cliente para vincular esses dados diferentes à pessoa individual à qual a solicitação de privacidade se aplica. O Serviço de query pode enriquecer os dados que usa com um identificador exclusivo para satisfazer tarefas de privacidade.

As solicitações de privacidade podem ser enviadas para o lago de dados ou o armazenamento de dados do Perfil. Os registros excluídos do lago de dados não resultam na exclusão de perfis que foram criados a partir desses registros. Além disso, um trabalho de privacidade para excluir informações pessoais do lago de dados não exclui seu perfil, portanto, quaisquer informações (que contenham essa ID de perfil) assimiladas após a conclusão do trabalho de privacidade atualizam esse perfil normalmente. Isso reafirma a necessidade de identificar corretamente os dados usados em esquemas ad hoc.

Consulte a documentação do Privacy Service para obter mais informações sobre [dados de identidade para solicitações de privacidade](../../privacy-service/identity-data.md) e como configurar suas operações de dados e aproveitar as tecnologias do Adobe para recuperar efetivamente as informações de identidade apropriadas para solicitações de privacidade do cliente.

Os recursos do Serviço de query para governança de dados simplificam e simplificam o processo de categorização de dados e a adesão aos regulamentos de uso de dados. Depois que os dados forem identificados, o Serviço de query permitirá alocar a identidade primária em todos os conjuntos de dados de saída. Você **must** adicione identidades ao conjunto de dados para facilitar as solicitações de privacidade de dados e trabalhar para a conformidade dos dados.

Os campos de dados de esquema podem ser definidos como um campo de identidade por meio da interface do usuário da plataforma e do Serviço de query também permite [marcar as identidades primárias usando o comando SQL &quot;ALTER TABLE&quot;](../sql/syntax.md#alter-table). Como configurar uma identidade usando a variável `ALTER TABLE` é especialmente útil quando os conjuntos de dados são criados usando SQL em vez de diretamente de um esquema por meio da interface do usuário da plataforma. Consulte a documentação para obter instruções sobre como [definir campos de identidade na interface do usuário](../../xdm/ui/fields/identity.md) ao usar schemas padrão.

<!-- COMMENTING OUT DATA HYGEINE SECTION TEMPORARILY UNTIL IT IS GA. currently it is in Beta only.

## Data hygiene 

"Data hygiene" refers to the process of repairing or removing data that may be outdated, inaccurate, incorrectly formatted, duplicated, or incomplete. It is important to ensure adequate data hygiene along every step of the data's journey and even from the initial data storage location. In Query Service, this is either the data lake or the data warehouse.

It is necessary to assign an identity to a derived dataset to allow their management by the [!DNL Data Hygiene] service. Conversely, when you create aggregated data on an accelerated data store, the aggregated data cannot be used to derive the original data. As a result of this data aggregation, the need to raise data hygiene requests is eliminated. == THIS APPEARS TO BE A PRIVACY USE CASE NAD NOT DATA HYGEINE ++  this is confusing.

An exception to this scenario is the case of deletion. If a data hygiene deletion is requested on a dataset and before the deletion is completed, another derived dataset query is executed, then the derived dataset will capture information from the original dataset. In this case, you must be mindful that if a request to delete a dataset has been sent, you must not execute any new derived dataset queries using the same dataset source. 

See the [data hygiene overview](../../hygiene/home.md) for more information on data hygiene in Adobe Experience Platform. -->
