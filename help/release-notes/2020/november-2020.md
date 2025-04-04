---
title: Notas de versão da Adobe Experience Platform de novembro de 2020
description: As notas de versão de novembro de 2020 da Adobe Experience Platform.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '2178'
ht-degree: 8%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 11 de novembro de 2020**

Novos recursos na Adobe Experience Platform:

- [Migração para o Adobe Experience Platform Data Lake](#migration)
- [[!DNL Access control]](#access-control)
- [[!DNL Offer Decisioning]](#offer-decisioning)
- [[!DNL Sandboxes]](#sandboxes)

Atualizações dos recursos existentes:

- [[!DNL Data Prep]](#data-prep)
- [[!DNL Data Science Workspace]](#dsw)
- [Serviço [!DNL Destinations]](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Migração para o Adobe Experience Platform Data Lake {#migration}

Enquanto a Adobe está migrando o Data Lake de Gen1 para Gen2, os usuários poderão ler a partir do Data Lake, mas todos os recursos que gravam no Data Lake serão afetados. A Adobe entrará em contato com os administradores do sistema para discutir o impacto da migração em detalhes e confirmar as datas e horas da migração para organizações específicas.

Para obter mais informações, leia o [guia de migração do Data Lake](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] aproveita perfis de produto do [Adobe Admin Console](https://adminconsole.adobe.com) para vincular usuários com permissões e sandboxes. As permissões controlam o acesso a vários recursos do Experience Platform, incluindo modelagem de dados, gerenciamento de perfis e administração de sandbox.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Permissões | No [!DNL Admin Console], a guia em um perfil de produto [!DNL Experience Platform] permite personalizar quais recursos do [!DNL Experience Platform] estão disponíveis para os usuários anexados a esse perfil. As categorias de permissão disponíveis são: **[!UICONTROL Modelagem de Dados]**, **[!UICONTROL Gerenciamento de Dados]**, **[!UICONTROL Gerenciamento de Perfis]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Monitoramento de Dados]**, **[!UICONTROL Administração de Sandbox]**, **[!UICONTROL Destinos]**, **[!UICONTROL Assimilação de Dados]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Serviço de Consulta]** e **[!UICONTROL Governança de Dados]**. |
| Acesso a sandboxes | A guia **[!UICONTROL Permissões]** em um perfil de produto [!DNL Experience Platform] pode conceder aos usuários acesso a sandboxes específicas. Consulte a seção sobre [sandboxes](#sandboxes) abaixo para obter mais informações. |

Para obter mais informações, consulte a [visão geral do controle de acesso](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] é um Serviço de Aplicativo integrado a [!DNL Experience Platform]. Ele permite que você use o [!DNL Experience Platform] para fornecer a melhor oferta e experiência aos seus clientes em todos os pontos de contato na hora certa.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Biblioteca de ofertas centralizada | A interface em que você cria e gerencia os diferentes elementos que compõem suas ofertas e define suas regras e restrições. |
| Mecanismo do Offer Decisioning | O mecanismo do Offer Decision aproveita os dados do [!DNL Experience Platform] e o [!DNL Real-Time Customer Profiles], juntamente com a Biblioteca de ofertas, para selecionar o momento, os clientes e os canais certos aos quais as ofertas serão entregues. |

Para obter mais informações, consulte a documentação de [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=pt-BR).

## [!DNL Sandboxes] {#sandboxes}

O [!DNL Experience Platform] foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional. Para atender a essa necessidade, o [!DNL Experience Platform] fornece sandboxes que particionam uma única instância do [!DNL Experience Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Sandbox de produção | [!DNL Experience Platform] fornece uma única sandbox de produção, que não pode ser excluída ou redefinida. O número total de sandboxes disponíveis, produção e não produção, é determinado pela licença adquirida. |
| Sandboxes de não produção | Várias sandboxes de não produção podem ser criadas para uma única instância do [!DNL Experience Platform], permitindo que você teste recursos, execute experimentos e faça configurações personalizadas sem afetar a sandbox de produção. |
| Seletor de sandbox | Na interface do usuário do [!DNL Experience Platform], o alternador de sandbox no canto superior esquerdo da tela permite alternar entre sandboxes disponíveis em um menu suspenso. O alternador de sandbox também fornece uma função de pesquisa que permite filtrar pelas sandboxes disponíveis. |
| Cabeçalho `x-sandbox-name` | Todas as chamadas a APIs [!DNL Experience Platform] agora devem incluir o novo cabeçalho `x-sandbox-name`, cujo valor faz referência ao atributo `name` da sandbox em que a operação ocorrerá. |

Para obter mais informações, consulte a [visão geral das sandboxes](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

O [!DNL Data Prep] permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Operações iterativas | O Mapeador [!DNL Data Prep] agora dá suporte à execução de operações iterativas em uma hierarquia. |
| Função do mapeador | O Mapeador [!DNL Data Prep] agora pode **não** copiar um atributo da origem para o XDM de destino. |

Para obter mais informações, consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Espaço de trabalho do Data Science {#dsw}

O Data Science Workspace usa aprendizagem de máquina e inteligência artificial para criar insights a partir de seus dados. Integrado à Adobe Experience Platform, o Data Science Workspace ajuda a fazer previsões usando seus ativos de conteúdo e dados nas soluções da Adobe. Uma das maneiras pelas quais a Data Science Workspace consegue isso é usando o [!DNL JupyterLab]. [!DNL JupyterLab] é uma interface de usuário baseada na Web para [[!DNL Project Jupyter]](https://jupyter.org/) e está totalmente integrada ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para cientistas de dados trabalharem com blocos de anotações, código e dados do [!DNL Jupyter].

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| [!DNL JupyterLab] modelo do Construtor de fórmula | Uso de requisitos do Notebook para receita e versões atualizadas. A imagem base de Tempo de Execução de [!DNL Python] ML foi atualizada para usar exclusivamente o [!DNL Python] 3.6.7 e um ambiente [!DNL Conda]. |

Para obter mais informações, leia o documento sobre [Criação de uma fórmula usando o Jupyter Notebooks](../../data-science-workspace/jupyterlab/create-a-model.md).

## Serviço [!DNL Destinations] {#destinations}

No [Real-Time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam dados para esses parceiros de forma contínua.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| Braze | O Brasil é uma plataforma abrangente de engajamento do cliente que promove experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram. |
| Microsoft Bing | O destino do Microsoft Bing ajuda a executar campanhas digitais direcionadas por público e redirecionamento no Microsoft Display Advertising. |
| A Trade Desk | A Trade Desk é uma plataforma de autoatendimento para compradores de anúncios para executar campanhas digitais direcionadas por público e redirecionamento em fontes de inventário para exibição, vídeo e dispositivos móveis. |

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atualizações de UX de detalhes de destino | O fluxo de trabalho de destino do Real-Time CDP agora inclui monitoramento em linha para que você possa ver quais ativações em lote foram bem-sucedidas. Esse recurso permitirá que os usuários resolvam problemas diretamente no fluxo de trabalho para destinos em lote por meio de alertas e um painel de monitoramento para rastrear erros no pipeline de processamento. |
| Criptografia de arquivo | Para destinos baseados em arquivo, os usuários agora podem adicionar criptografia aos arquivos exportados. |
| Agendamento de arquivo | Para destinos de armazenamento na nuvem e com base em email, os usuários podem criar uma exportação única ou instantâneos diários. |
| Campos obrigatórios | Os usuários podem marcar campos como obrigatórios, garantindo que apenas os campos que contêm o campo obrigatório sejam exportados. |

Para obter mais informações, consulte a [Visão geral dos Destinos](../../destinations/home.md).

## Serviços inteligentes {#intelligent-services}

Os Serviços inteligentes capacitam analistas e profissionais de marketing a aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing estabeleçam previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial, sem a necessidade de uma especialização em ciência de dados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Conjunto de dados de Eventos de experiência do consumidor (CEE) | A criação de um conjunto de dados CEE agora permite adicionar campos de identidade ao conjunto de dados com o Editor de esquemas. A IA de atribuição e a IA do cliente usam a identidade principal para combinar eventos. |

Para obter mais informações, leia a seção sobre [adição de campos de identidade a um conjunto de dados](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) no guia de preparação de dados dos Serviços inteligentes.

### IA de atribuição

A IA de atribuição, como parte dos Serviços inteligentes, é um serviço de atribuição de vários canais e algoritmos que calcula a influência e o impacto incremental das interações com o cliente em relação aos resultados especificados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Link da fonte de dados | O link para a origem do conjunto de dados original pode ser visualizado e navegado para o a partir do painel direito de uma instância de serviço selecionada. |
| Editar nome da instância | Agora você pode modificar o nome de uma instância existente da IA de atribuição. |
| Clonar instância | Copia a configuração da instância de serviço selecionada no momento e permite modificações. |
| Modificar parâmetros de configuração da instância | Agora é possível modificar a configuração de uma instância existente da IA de atribuição se ela ainda não tiver começado a pontuar. |
| Pontuação única | Agora você pode acionar a pontuação do modelo ad-hoc nas instâncias da IA de atribuição. |
| Passar pelas colunas | Agora é possível configurar colunas adicionais que serão adicionadas aos arquivos de pontuação de saída bruta para adicionar dimensões extras às visualizações da ferramenta BI. |
| Ativação e desativação de instâncias | Agora você pode ativar e desativar o treinamento e a pontuação programados do modelo das instâncias da IA de atribuição. |
| Rastreamento de direitos | Você pode encontrar o valor total dos insights de atribuição consumidos pela sua conta no container criar instância. |
| Detalhamento do ponto de contato por posição | Um novo gráfico de insights que fornece uma análise de pontos de contato por posições de caminho de conversão. |
| Principais caminhos de conversão | Um novo gráfico de insights localizado na guia Análise de caminho. O gráfico contém uma lista dos cinco principais caminhos de conversão mostrando a sequência de pontos de contato do canal de marketing que levou ao maior número de conversões. |
| Eficácia do ponto de contato | Fornece insights detalhados das três variáveis mais importantes pelas quais seu modelo avalia a eficácia do ponto de contato. As variáveis são a proporção de caminhos positivos e negativos tocados, a eficiência do ponto de contato e o volume do ponto de contato. |

Para obter mais informações, leia a [visão geral da IA de atribuição](../../intelligent-services/attribution-ai/overview.md).

### IA do cliente

A IA do cliente, como parte dos Serviços inteligentes, fornece aos profissionais de marketing o poder de gerar previsões de clientes individualmente com explicações. Com a ajuda de fatores influentes, a IA do cliente pode informar o que um cliente deve fazer e por quê. Além disso, os profissionais de marketing podem se beneficiar das previsões e insights da IA do cliente para personalizar as experiências do cliente, disponibilizando as ofertas e mensagens mais apropriadas.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Link da fonte de dados | O link para a origem do conjunto de dados original pode ser visualizado e navegado para o a partir do painel direito de uma instância de serviço selecionada. |
| Editar nome da instância | Você pode modificar o nome de uma instância existente da IA do cliente. |
| Modificar parâmetros de configuração da instância | Agora é possível modificar a configuração de uma instância existente da IA do cliente se ela ainda não tiver iniciado uma pontuação. |
| Clonar instância | Copia a configuração da instância de serviço selecionada no momento e permite modificações. |
| Rastreamento de direitos | Você pode encontrar a quantidade total de perfis pontuados pela IA do cliente para sua conta no container criar instância. |
| Meta de previsão | A flexibilidade na criação de uma meta de previsão foi aumentada com novas opções para prever se algo &quot;ocorrerá&quot; ou &quot;não ocorrerá&quot;. Além disso, foram adicionadas as opções para prever se &quot;todos&quot; os eventos acontecem ou &quot;qualquer um&quot; dos eventos quando vários eventos são usados. |
| Detalhamento influente de fator | Os compartimentos de fatores influentes principais de propensão agora contêm detalhamentos. Detalhes são um resumo de nível mais profundo dos valores de cada um dos principais fatores influentes em um intervalo de propensão. |

Para obter mais informações, leia a [Visão geral da IA do cliente](../../intelligent-services/customer-ai/overview.md).

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, é possível ter uma visão integral de cada cliente ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. O [!DNL Profile] permite consolidar seus dados diferentes de clientes em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Fluxo de trabalho de políticas de mesclagem atualizado | A Experience Platform atualizou a configuração da política de mesclagem para um novo fluxo de trabalho em etapas. Esse fluxo de trabalho permite que os usuários reúnam fragmentos de dados de vários conjuntos de dados do Perfil e definam a prioridade de como os dados são mesclados nesses conjuntos de dados para criar uma visualização abrangente de cada indivíduo. Os usuários podem mesclar conjuntos de dados selecionados do Perfil individual XDM selecionando o método de mesclagem apropriado (carimbo de data e hora ordenado ou precedência do conjunto de dados) e anexando conjuntos de dados ExperienceEvent aos conjuntos de dados do Perfil. |
| Visualização do esquema de união | Na interface do usuário do Experience Platform, os usuários podem encontrar mais facilmente informações sobre todos os esquemas e conjuntos de dados que contribuem para o esquema de união, bem como atributos de chave de superfície, como campos de identidade e relacionamento. Essas atualizações melhoram a capacidade de solucionar problemas e validar se os perfis estão configurados corretamente, se as identidades estão compiladas corretamente e se os dados foram assimilados com êxito. |

Para obter mais informações sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com dados do [!DNL Profile], leia a [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir que você estruture, rotule e aprimore esses dados usando os serviços do [!DNL Experience Platform]. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O [!DNL Experience Platform] fornece uma API RESTful e uma interface do usuário interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novas fontes**

| Recurso | Descrição |
| ------- | ----------- |
| [!DNL Shopify] | Agora você pode conectar [!DNL Shopify] a [!DNL Experience Platform] usando a API [!DNL Flow Service] ou a interface do usuário. Consulte a [Visão geral do conector do Shopify](../../sources/connectors/ecommerce/shopify.md) para obter mais informações. |

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atualizar informações de conexão | Agora você pode atualizar os nomes, descrições e credenciais das conexões em lote existentes usando a API [!DNL Flow Service] e a interface do usuário. Para obter mais informações, consulte o tutorial sobre [atualização de conexões usando a API de Serviço de Fluxo](../../sources/tutorials/api/update.md) e [edição de detalhes da conta usando a interface](../../sources/tutorials/ui/monitor.md). |
| Excluir conexões | As conexões em lote que contêm erros ou se tornaram desnecessárias agora podem ser excluídas usando a API [!DNL Flow Service] e a interface do usuário. Para obter mais informações, consulte o tutorial sobre [exclusão de conexões usando a API de Serviço de Fluxo](../../sources/tutorials/api/delete.md) e [exclusão de contas usando a interface](../../sources/tutorials/ui/delete-accounts.md). |
| Mapeamento hierárquico | Você pode visualizar um arquivo de origem hierárquico, como JSON ou Parquet, durante o processo de assimilação de dados. Consulte o tutorial sobre [configuração de fluxo de dados para conectores de armazenamento em nuvem na interface](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obter mais informações. |
| Suporte de API para mapeamento em fontes de transmissão | Agora você pode usar APIs para executar funções de mapeamento com fontes de transmissão. |
| Suporte à API para delimitadores personalizados para fontes de armazenamento em nuvem | Agora é possível coletar arquivos não delimitados por CSV usando fontes de armazenamento na nuvem. É possível usar qualquer delimitador de coluna única, como tabulação, vírgula, barra vertical, ponto e vírgula ou hash, para coletar arquivos simples em qualquer formato. |
| Suporte à sandbox para o conector do Adobe Audience Manager | O conector do Audience Manager agora é sensível à sandbox. Os usuários podem permitir que o conector roteie conjuntos de dados do Audience Manager para a sandbox de sua escolha (incluindo sandboxes de não produção). A configuração é limitada a uma sandbox por organização. |
| Melhorias de UX | A assimilação baseada em arquivo agora pode ser acessada por meio do catálogo de fontes. |

Para saber mais sobre fontes, consulte a [visão geral das fontes](../../sources/home.md).
