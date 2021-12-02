---
title: Notas de versão da Adobe Experience Platform
description: Notas de versão do Experience Platform 11 de novembro de 2020
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: 38c493e6306e493f4ef5caf90509bda6f4d80023
workflow-type: tm+mt
source-wordcount: '2180'
ht-degree: 3%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 11 de novembro de 2020**

Novos recursos no Adobe Experience Platform:

- [Migração do Adobe Experience Platform Data Lake](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Atualizações dos recursos existentes:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [[!DNL Destinations] Serviço de](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Migração do Adobe Experience Platform Data Lake {#migration}

Enquanto o Adobe está migrando o Data Lake de Gen1 para Gen2, os usuários poderão ler a partir do Data Lake, mas todos os recursos que gravarem no Data Lake serão afetados. O Adobe entrará em contato com os administradores do sistema para discutir o impacto da migração em detalhes e confirmar as datas e horas de migração de determinadas organizações IMS.

Para obter mais informações, leia o [Guia de migração do Data Lake](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] aproveitadores [Adobe Admin Console](https://adminconsole.adobe.com) perfis de produto para vincular usuários com permissões e sandboxes. As permissões controlam o acesso a uma variedade de recursos da plataforma, incluindo modelagem de dados, gerenciamento de perfis e administração de sandbox.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Permissões | No [!DNL Admin Console], a guia em um [!DNL Platform] o perfil do produto permite personalizar qual [!DNL Platform] estão disponíveis para os usuários anexados a esse perfil. As categorias de permissão disponíveis incluem: **[!UICONTROL Modelagem de dados]**, **[!UICONTROL Gerenciamento de dados]**, **[!UICONTROL Gerenciamento de perfis]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Monitoramento de dados]**, **[!UICONTROL Administração de sandbox]**, **[!UICONTROL Destinos]**, **[!UICONTROL Assimilação de dados]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Serviço de query]** e **[!UICONTROL Governança de dados]**. |
| Acesso a sandboxes | O **[!UICONTROL Permissões]** em uma [!DNL Platform] o perfil de produto pode conceder aos usuários acesso a sandboxes específicas. Consulte a seção sobre [sandboxes](#sandboxes) abaixo para obter mais informações. |

Para obter mais informações, consulte o [visão geral do controle de acesso](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] é um Serviço de aplicativos integrado ao [!DNL Experience Platform]. Ele permite aproveitar [!DNL Platform] para oferecer a melhor oferta e experiência aos clientes em todos os pontos de contato na hora certa.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Biblioteca de ofertas centralizada | A interface onde você cria e gerencia os diferentes elementos que compõem suas ofertas e define suas regras e restrições. |
| Mecanismo de decisão da oferta | O mecanismo de decisão da oferta aproveita [!DNL Platform] dados e [!DNL Real-time Customer Profiles], juntamente com a Biblioteca de ofertas, para selecionar o momento certo, os clientes e canais aos quais as ofertas serão entregues. |

Para obter mais informações, consulte o [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=pt-BR) documentação.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] O foi criado para enriquecer os aplicativos de experiência digital em escala global. Geralmente, as empresas executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, teste e implantação desses aplicativos, além de garantir a conformidade operacional. Para dar resposta a esta necessidade, [!DNL Experience Platform] fornece sandboxes que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Sandbox de produção | [!DNL Experience Platform] O fornece uma única sandbox de produção, que não pode ser excluída ou redefinida. O número total de sandboxes disponíveis, produção e não produção, é determinado pela licença adquirida. |
| sandboxes de não produção | É possível criar várias sandboxes de não produção para uma única [!DNL Platform] , permitindo testar recursos, executar experimentos e fazer configurações personalizadas sem afetar sua sandbox de produção. |
| Seletor de sandbox | No [!DNL Experience Platform] interface do usuário, o alternador de sandbox no canto superior esquerdo da tela permite alternar entre sandboxes disponíveis em um menu suspenso. O alternador de sandbox também fornece uma função de pesquisa que permite filtrar por meio de sandboxes disponíveis. |
| `x-sandbox-name` header | Todas as chamadas para [!DNL Experience Platform] As APIs agora devem incluir o novo `x-sandbox-name` cabeçalho, cujo valor faz referência à variável `name` da sandbox em que a operação ocorrerá. |

Para obter mais informações, consulte o [visão geral das sandboxes](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Operações iterativas | [!DNL Data Prep] O mapeador agora oferece suporte para executar operações iterativas em uma hierarquia. |
| Função do mapeador | [!DNL Data Prep] Agora o Mapper tem a capacidade de **not** copie um atributo da origem para o XDM de destino. |

Para obter mais informações, consulte o [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Data Science Workspace {#dsw}

O Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seus ativos de conteúdo e dados nas soluções de Adobe. Uma das maneiras de realizar isso no Data Science Workspace é usando o [!DNL JupyterLab]. [!DNL JupyterLab] é uma interface do usuário baseada na Web para [[!DNL Project Jupyter]](https://jupyter.org/) e é totalmente integrado ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para os cientistas de dados trabalharem com o [!DNL Jupyter] blocos de notas, código e dados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| [!DNL JupyterLab] Modelo do Criador de receita | Notebook para receber requisitos de uso e versões atualizadas. [!DNL Python] A imagem base de tempo de execução do ML foi atualizada para ser usada [!DNL Python] 3.6.7 e a [!DNL Conda] exclusivamente ambiente. |

Para obter mais informações, leia o documento em [criar uma receita usando notebooks Júpiter](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] Serviço de {#destinations}

Em [Real-time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| Bico | O Brasil é uma plataforma abrangente de engajamento do cliente que possibilita experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram. |
| Microsoft Bing | O destino Microsoft Bing ajuda a executar o redirecionamento e campanhas digitais direcionadas ao público-alvo em toda a publicidade de exibição do Microsoft. |
| A Mesa de Comércio | O Trade Desk é uma plataforma de autoatendimento para compradores de anúncios para executar redirecionamento e campanhas digitais direcionadas ao público-alvo em fontes de exibição, vídeo e inventário móvel. |

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atualizações de UX dos detalhes do destino | O fluxo de trabalho de destino da CDP em tempo real agora inclui o monitoramento em linha, para que você possa ver quais ativações em lote foram bem-sucedidas. Esse recurso permitirá que os usuários resolvam problemas diretamente no workflow para destinos em lote por meio de alertas e um painel de monitoramento para rastrear erros no pipeline de processamento. |
| Criptografia de arquivo | Para destinos com base em arquivo, os usuários agora podem adicionar criptografia aos arquivos exportados. |
| Agendamento de arquivo | Para destinos de armazenamento em nuvem e com base em email, os usuários podem criar uma exportação única ou criar instantâneos diários. |
| Campos obrigatórios | Os usuários podem marcar campos como obrigatórios, garantindo que apenas os campos que contêm o campo obrigatório sejam exportados. |

Para obter mais informações, consulte o [Visão geral dos destinos](../../destinations/home.md).

## Serviços inteligentes {#intelligent-services}

Os Serviços inteligentes capacitam analistas e profissionais de marketing a aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso da experiência do cliente. Isso permite que os analistas de marketing configurem previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de experiência em ciência de dados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Conjunto de dados de Eventos de experiência do consumidor (CEE) | A criação de um conjunto de dados CEE agora oferece suporte à adição de campos de identidade ao conjunto de dados com o Editor de esquema. O Attribution AI e o Customer AI usam a identidade primária para combinar eventos. |

Para mais informações, leia a seção sobre [adicionar campos de identidade a um conjunto de dados](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) no guia de preparação de dados dos Serviços inteligentes .

### Attribution AI

O Attribution AI, como parte dos Serviços inteligentes, é um serviço de atribuição de vários canais e algoritmos que calcula a influência e o impacto incremental das interações com o cliente em relação aos resultados especificados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Link da fonte de dados | O link para a fonte do conjunto de dados original pode ser visualizado e navegado até o painel direito de uma instância de serviço selecionada. |
| Editar nome da instância | Agora é possível modificar o nome de uma instância do Attribution AI existente. |
| Clonar instância | Copia a configuração da instância de serviço atualmente selecionada e permite modificações. |
| Modificar parâmetros de configuração da instância | Agora é possível modificar a configuração de uma instância do Attribution AI existente se ela ainda não tiver iniciado a pontuação. |
| Pontuação única | Agora você pode acionar a pontuação do modelo ad-hoc em suas instâncias do Attribution AI. |
| Passar pelas colunas | Agora é possível configurar colunas adicionais que serão adicionadas aos arquivos de pontuação de saída bruta para adicionar dimensões adicionais às visualizações de ferramenta de BI. |
| Ativação e desativação de instância | Agora é possível ativar e desativar o treinamento do modelo agendado e a pontuação de suas instâncias do Attribution AI. |
| Rastreamento de direitos | Você pode encontrar a quantidade total de insights de Atribuição consumidos pela sua conta no contêiner de criação de instância . |
| Detalhamento do ponto de contato por posição | Um novo gráfico de insights que fornece uma análise de pontos de contato por posições de caminho de conversão. |
| Principais caminhos de conversão | Um novo gráfico de insights localizado na guia Análise de caminho. O gráfico contém uma lista dos cinco principais caminhos de conversão que mostram a sequência de pontos de contato do canal de marketing que levaram ao maior número de conversões. |
| Eficácia do ponto de contato | Fornece insights detalhados das três variáveis mais importantes nas quais seu modelo mede a eficácia do ponto de contato. As variáveis são a proporção de caminhos positivos e negativos tocados, a eficiência do ponto de contato e o volume do ponto de contato. |

Para obter mais informações, leia o [Visão geral do Attribution AI](../../intelligent-services/attribution-ai/overview.md).

### Customer AI

O Customer AI, como parte dos Serviços inteligentes, fornece aos profissionais de marketing o poder de gerar previsões de clientes a nível individual com explicações. Com a ajuda de fatores influentes, a AI do cliente pode informar o que um cliente deve fazer e por quê. Além disso, os profissionais de marketing podem se beneficiar das previsões e insights do Customer AI para personalizar as experiências do cliente, disponibilizando as ofertas e mensagens mais apropriadas.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Link da fonte de dados | O link para a fonte do conjunto de dados original pode ser visualizado e navegado até o painel direito de uma instância de serviço selecionada. |
| Editar nome da instância | Você pode modificar o nome de uma instância do Customer AI existente. |
| Modificar parâmetros de configuração da instância | Agora é possível modificar a configuração de uma instância do Customer AI existente se ela ainda não tiver iniciado uma pontuação. |
| Clonar instância | Copia a configuração da instância de serviço atualmente selecionada e permite modificações. |
| Rastreamento de direitos | Você pode encontrar a quantidade total de perfis pontuados pelo Customer AI para sua conta no contêiner de criação de instância . |
| Objetivo da previsão | A flexibilidade na criação de uma meta de previsão foi aumentada com novas opções para prever se algo &quot;ocorrerá&quot; ou &quot;não ocorrerá&quot;. Além disso, foram adicionadas as opções para prever se &quot;todos&quot; os eventos ocorrem ou &quot;qualquer um de&quot; os eventos ocorrem quando vários eventos são usados. |
| Detalhamento do fator influente | Os principais compartimentos de fatores influentes de propensão agora contêm detalhamentos. Os detalhamentos são um resumo de nível mais profundo dos valores para cada um dos principais fatores influentes em um bucket de propensão. |

Para obter mais informações, leia o [Visão geral do Customer AI](../../intelligent-services/customer-ai/overview.md).

## Perfil do cliente em tempo real {#profile}

O Adobe Experience Platform permite que você conduza experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagirem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] O permite consolidar seus dados de clientes diferentes em uma visualização unificada que oferece uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Fluxo de trabalho das políticas de mesclagem atualizado | A Platform atualizou a configuração da política de mesclagem para um novo fluxo de trabalho gradual. Esse fluxo de trabalho permite que os usuários reúnam fragmentos de dados de vários conjuntos de dados de perfil e definam a prioridade de como os dados são unidos nesses conjuntos de dados para criar uma exibição abrangente de cada indivíduo. Os usuários podem mesclar conjuntos de dados de Perfil individual XDM selecionados ao selecionar o método de mesclagem apropriado (carimbo de data e hora solicitado ou precedência do conjunto de dados) e anexar os conjuntos de dados do ExperienceEvent aos conjuntos de dados do Perfil. |
| Exibição do esquema de união | Na interface do usuário do Experience Platform, os usuários podem encontrar mais facilmente informações sobre todos os esquemas e conjuntos de dados que contribuem para o esquema de união, bem como atributos principais de superfície, como campos de identidade e relação. Essas atualizações melhoram a capacidade de solucionar problemas e validar se os perfis estão configurados corretamente, as identidades são compiladas corretamente e os dados foram assimilados com êxito. |

Para obter mais informações sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com a [!DNL Profile] leia os [Visão geral do perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novas fontes**

| Recurso | Descrição |
| ------- | ----------- |
| [!DNL Shopify] | Agora você pode se conectar [!DNL Shopify] para [!DNL Experience Platform] usando o [!DNL Flow Service] API ou a interface do usuário. Consulte a [Visão geral do conector Shopify](../../sources/connectors/ecommerce/shopify.md) para obter mais informações. |

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atualizar informações de conexão | Agora você pode atualizar os nomes, as descrições e as credenciais das conexões em lote existentes usando o [!DNL Flow Service] API e a interface do usuário. Para obter mais informações, consulte o tutorial em [atualização de conexões usando a API do Serviço de Fluxo](../../sources/tutorials/api/update.md) e [editar detalhes da conta usando a interface do usuário](../../sources/tutorials/ui/monitor.md). |
| Excluir conexões | As conexões em lote que contêm erros ou se tornaram desnecessárias agora podem ser excluídas usando o [!DNL Flow Service] API e a interface do usuário. Para obter mais informações, consulte o tutorial em [exclusão de conexões usando a API do Serviço de Fluxo](../../sources/tutorials/api/delete.md) e [excluir contas usando a interface do usuário](../../sources/tutorials/ui/delete-accounts.md). |
| Mapeamento hierárquico | Você pode visualizar um arquivo de origem hierárquico, como JSON ou Parquet, durante o processo de assimilação de dados. Consulte o tutorial em [configuração de um fluxo de dados para conectores de armazenamento em nuvem na interface do usuário do](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obter mais informações. |
| Suporte à API para mapeamento em fontes de transmissão | Agora é possível usar APIs para executar funções de mapeamento com fontes de transmissão. |
| Suporte a API para delimitadores personalizados para fontes de armazenamento em nuvem | Agora é possível coletar arquivos não delimitados por CSV usando fontes de armazenamento em nuvem. Você pode usar qualquer delimitador de coluna único, como uma guia, vírgula, barra vertical, ponto e vírgula ou hash para coletar arquivos simples em qualquer formato. |
| Suporte de sandbox para conector Adobe Audience Manager | O conector Audience Manager agora tem reconhecimento de sandbox. Os usuários podem permitir que o conector roteie conjuntos de dados de Audience Manager para a sandbox de sua escolha (incluindo sandboxes que não sejam de produção). A configuração é limitada a uma sandbox por IMS Org. |
| Melhorias no UX | A assimilação baseada em arquivo agora pode ser acessada pelo catálogo de fontes. |

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
