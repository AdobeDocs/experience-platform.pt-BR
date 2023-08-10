---
title: Notas de versão da Adobe Experience Platform de novembro de 2020
description: As notas de versão de novembro de 2020 para Adobe Experience Platform.
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
exl-id: 29179b56-e49a-44e8-8c64-a7c383c2eaaf
source-git-commit: b66a50e40aaac8df312a2c9a977fb8d4f1fb0c80
workflow-type: tm+mt
source-wordcount: '2181'
ht-degree: 10%

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
- [[!DNL Destinations] Serviço de](#destinations)
- [[!DNL Intelligent Services]](#intelligent-services)
- [[!DNL Real-Time Customer Profile]](#profile)
- [[!DNL Sources]](#sources)

## Migração para o Adobe Experience Platform Data Lake {#migration}

Enquanto o Adobe está migrando o Data Lake de Gen1 para Gen2, os usuários poderão ler a partir do Data Lake, mas todos os recursos que gravam no Data Lake serão afetados. O Adobe entrará em contato com os administradores do sistema para discutir o impacto da migração em detalhes e confirmar as datas e horas da migração para organizações específicas.

Para obter mais informações, leia a [Guia de migração do Data Lake](../../landing/adls2-gen2-migration.md).

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] aproveita [Adobe Admin Console](https://adminconsole.adobe.com) perfis de produto para vincular usuários com permissões e sandboxes. As permissões controlam o acesso a uma variedade de recursos da Platform, incluindo modelagem de dados, gerenciamento de perfis e administração de sandbox.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Permissões | No [!DNL Admin Console], a guia em um [!DNL Platform] O perfil de produto permite personalizar qual [!DNL Platform] Os recursos do estão disponíveis para os usuários anexados a esse perfil. As categorias de permissão disponíveis incluem: **[!UICONTROL Modelagem de dados]**, **[!UICONTROL Gerenciamento de dados]**, **[!UICONTROL Gerenciamento de perfis]**, **[!UICONTROL Identity Management]**, **[!UICONTROL Monitoramento de dados]**, **[!UICONTROL Administração de sandbox]**, **[!UICONTROL Destinos]**, **[!UICONTROL Assimilação de dados]**, **[!UICONTROL Data Science Workspace]**, **[!UICONTROL Serviço de consulta]**, e **[!UICONTROL Governança de dados]**. |
| Acesso a sandboxes | A variável **[!UICONTROL Permissões]** em um [!DNL Platform] o perfil de produto pode conceder aos usuários acesso a sandboxes específicas. Consulte a seção sobre [sandboxes](#sandboxes) abaixo para obter mais informações. |

Para obter mais informações, consulte [visão geral do controle de acesso](../../access-control/home.md).

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] é um serviço de aplicativos integrado à [!DNL Experience Platform]. Ele permite aproveitar [!DNL Platform] para fornecer a melhor oferta e experiência aos seus clientes em todos os pontos de contato na hora certa.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Biblioteca de ofertas centralizada | A interface em que você cria e gerencia os diferentes elementos que compõem suas ofertas e define suas regras e restrições. |
| Mecanismo do Offer Decisioning | O mecanismo do Offer Decision aproveita [!DNL Platform] dados e [!DNL Real-Time Customer Profiles], juntamente com a Biblioteca de ofertas, para selecionar o momento certo, os clientes e canais para os quais as ofertas serão entregues. |

Para obter mais informações, consulte [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=pt-BR) documentação.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] O foi criado para enriquecer aplicativos de experiência digital em escala global. As empresas geralmente executam vários aplicativos de experiência digital em paralelo e precisam atender ao desenvolvimento, ao teste e à implantação desses aplicativos enquanto garantem a conformidade operacional. A fim de dar resposta a esta [!DNL Experience Platform] O fornece sandboxes que particionam uma única [!DNL Platform] em ambientes virtuais separados para ajudar a desenvolver aplicativos de experiência digital.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Sandbox de produção | [!DNL Experience Platform] O fornece uma única sandbox de produção, que não pode ser excluída ou redefinida. O número total de sandboxes disponíveis, produção e não produção, é determinado pela licença adquirida. |
| Sandboxes de não produção | Várias sandboxes de não produção podem ser criadas para um único [!DNL Platform] , permitindo testar recursos, executar experimentos e fazer configurações personalizadas sem afetar sua sandbox de produção. |
| Seletor de sandbox | No [!DNL Experience Platform] , o alternador de sandbox no canto superior esquerdo da tela permite alternar entre sandboxes disponíveis por meio de um menu suspenso. O alternador de sandbox também fornece uma função de pesquisa que permite filtrar pelas sandboxes disponíveis. |
| `x-sandbox-name` cabeçalho | Todas as chamadas para [!DNL Experience Platform] Agora, as APIs devem incluir a nova `x-sandbox-name` cabeçalho, cujo valor faz referência ao `name` atributo da sandbox em que a operação ocorrerá. |

Para obter mais informações, consulte [visão geral das sandboxes](../../sandboxes/home.md).

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Operações iterativas | [!DNL Data Prep] O mapeador agora permite executar operações iterativas em uma hierarquia. |
| Função do mapeador | [!DNL Data Prep] O mapeador agora tem a capacidade de **não** copie um atributo do XDM de origem para o de destino. |

Para obter mais informações, consulte [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Espaço de trabalho do Data Science {#dsw}

O Data Science Workspace usa aprendizado de máquina e inteligência artificial para criar insights a partir de seus dados. Integrado à Adobe Experience Platform, o Data Science Workspace ajuda a fazer previsões usando seu conteúdo e ativos de dados nas soluções da Adobe. Uma das maneiras pelas quais o Data Science Workspace consegue isso é usando [!DNL JupyterLab]. [!DNL JupyterLab] é uma interface de usuário baseada na Web para [[!DNL Project Jupyter]](https://jupyter.org/) e está totalmente integrado ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo com o qual os cientistas de dados trabalham [!DNL Jupyter] blocos de anotações, código e dados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| [!DNL JupyterLab] Modelo do Construtor de fórmula | Uso de requisitos do Notebook para receita e versões atualizadas. [!DNL Python] A imagem base do Tempo de Execução de ML foi atualizada para uso [!DNL Python] 3.6.7 e a [!DNL Conda] ambiente exclusivamente. |

Para obter mais informações, leia o documento em [criação de uma fórmula usando o Jupyter Notebooks](../../data-science-workspace/jupyterlab/create-a-model.md).

## [!DNL Destinations] Serviço de {#destinations}

Entrada [Real-time Customer Data Platform](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| Braze | O Brasil é uma plataforma abrangente de engajamento do cliente que promove experiências relevantes e memoráveis entre os clientes e as marcas que eles adoram. |
| Microsoft Bing | O destino do Microsoft Bing ajuda a executar campanhas digitais direcionadas por público e redirecionamento em anúncios de exibição do Microsoft. |
| A Trade Desk | A Trade Desk é uma plataforma de autoatendimento para compradores de anúncios para executar campanhas digitais direcionadas por público e redirecionamento em fontes de inventário para exibição, vídeo e dispositivos móveis. |

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atualizações de UX de detalhes de destino | O fluxo de trabalho de destino do Real-Time CDP agora inclui monitoramento em linha para que você possa ver quais ativações em lote foram bem-sucedidas. Esse recurso permitirá que os usuários resolvam problemas diretamente no fluxo de trabalho para destinos em lote por meio de alertas e um painel de monitoramento para rastrear erros no pipeline de processamento. |
| Criptografia de arquivo | Para destinos baseados em arquivo, os usuários agora podem adicionar criptografia aos arquivos exportados. |
| Agendamento de arquivo | Para destinos de armazenamento na nuvem e com base em email, os usuários podem criar uma exportação única ou instantâneos diários. |
| Campos obrigatórios | Os usuários podem marcar campos como obrigatórios, garantindo que apenas os campos que contêm o campo obrigatório sejam exportados. |

Para obter mais informações, consulte [Visão geral dos destinos](../../destinations/home.md).

## Serviços inteligentes {#intelligent-services}

Os Serviços inteligentes capacitam analistas e profissionais de marketing a aproveitar o potencial da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing definam previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de conhecimento especializado em ciência de dados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Conjunto de dados de Eventos de experiência do consumidor (CEE) | A criação de um conjunto de dados CEE agora permite adicionar campos de identidade ao conjunto de dados com o Editor de esquemas. O Attribution AI e a IA do cliente usam a identidade principal para combinar eventos. |

Para obter mais informações, leia a seção sobre [adição de campos de identidade a um conjunto de dados](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) no guia de preparação de dados dos Serviços inteligentes.

### IA de atribuição

O Attribution AI, como parte dos Serviços inteligentes, é um serviço de atribuição de vários canais e algoritmos que calcula a influência e o impacto incremental das interações com o cliente em relação aos resultados especificados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Link da fonte de dados | O link para a origem do conjunto de dados original pode ser visualizado e navegado para o a partir do painel direito de uma instância de serviço selecionada. |
| Editar nome da instância | Agora você pode modificar o nome de uma instância do Attribution AI existente. |
| Clonar instância | Copia a configuração da instância de serviço selecionada no momento e permite modificações. |
| Modificar parâmetros de configuração da instância | Agora é possível modificar a configuração de uma instância do Attribution AI existente se ela ainda não tiver começado a pontuar. |
| Pontuação única | Agora você pode acionar a pontuação do modelo ad-hoc em suas instâncias do Attribution AI. |
| Passar pelas colunas | Agora é possível configurar colunas adicionais que serão adicionadas aos arquivos de pontuação de saída bruta para adicionar dimensões extras às visualizações da ferramenta BI. |
| Ativação e desativação de instâncias | Agora você pode ativar e desativar o treinamento e a pontuação programados do modelo de suas instâncias do Attribution AI. |
| Rastreamento de direitos | Você pode encontrar o valor total dos insights de atribuição consumidos pela sua conta no container criar instância. |
| Detalhamento do ponto de contato por posição | Um novo gráfico de insights que fornece uma análise de pontos de contato por posições de caminho de conversão. |
| Principais caminhos de conversão | Um novo gráfico de insights localizado na guia Análise de caminho. O gráfico contém uma lista dos cinco principais caminhos de conversão mostrando a sequência de pontos de contato do canal de marketing que levou ao maior número de conversões. |
| Eficácia do ponto de contato | Fornece insights detalhados das três variáveis mais importantes pelas quais seu modelo avalia a eficácia do ponto de contato. As variáveis são a proporção de caminhos positivos e negativos tocados, a eficiência do ponto de contato e o volume do ponto de contato. |

Para obter mais informações, leia a [visão geral do Attribution AI](../../intelligent-services/attribution-ai/overview.md).

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

Para obter mais informações, leia a [Visão geral do Customer AI](../../intelligent-services/customer-ai/overview.md).

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite gerar experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, é possível ter uma visão integral de cada cliente ao combinar dados de vários canais, incluindo online, offline, CRM e de terceiros. [!DNL Profile] O permite consolidar dados diferentes do cliente em uma visualização unificada, oferecendo uma conta acionável com carimbo de data e hora de cada interação com o cliente.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Fluxo de trabalho de políticas de mesclagem atualizado | A Platform atualizou a configuração da política de mesclagem para um novo fluxo de trabalho em etapas. Esse fluxo de trabalho permite que os usuários reúnam fragmentos de dados de vários conjuntos de dados do Perfil e definam a prioridade de como os dados são mesclados nesses conjuntos de dados para criar uma visualização abrangente de cada indivíduo. Os usuários podem mesclar conjuntos de dados selecionados do Perfil individual XDM selecionando o método de mesclagem apropriado (carimbo de data e hora ordenado ou precedência do conjunto de dados) e anexando conjuntos de dados ExperienceEvent aos conjuntos de dados do Perfil. |
| Visualização do esquema de união | Na interface do usuário do Experience Platform, os usuários podem encontrar mais facilmente informações sobre todos os esquemas e conjuntos de dados que contribuem para o esquema de união, bem como destacar atributos-chave, como campos de identidade e relacionamento. Essas atualizações melhoram a capacidade de solucionar problemas e validar se os perfis estão configurados corretamente, se as identidades estão compiladas corretamente e se os dados foram assimilados com êxito. |

Para obter mais informações sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com a [!DNL Profile] dados, leia os [Visão geral do Perfil do cliente em tempo real](../../profile/home.md).

## [!DNL Sources] {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform]A fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novas fontes**

| Recurso | Descrição |
| ------- | ----------- |
| [!DNL Shopify] | Agora você pode se conectar [!DNL Shopify] para [!DNL Experience Platform] usando o [!DNL Flow Service] API ou a interface do usuário. Consulte a [Visão geral do Shopify Connector](../../sources/connectors/ecommerce/shopify.md) para obter mais informações. |

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atualizar informações de conexão | Agora você pode atualizar os nomes, descrições e credenciais das conexões de lote existentes usando o [!DNL Flow Service] API e a interface do usuário. Para obter mais informações, consulte o tutorial em [atualização de conexões usando a API do Serviço de fluxo](../../sources/tutorials/api/update.md) e [editar detalhes da conta usando a interface](../../sources/tutorials/ui/monitor.md). |
| Excluir conexões | As conexões em lote que contêm erros ou se tornaram desnecessárias agora podem ser excluídas usando o [!DNL Flow Service] API e a interface do usuário. Para obter mais informações, consulte o tutorial em [exclusão de conexões usando a API de serviço de fluxo](../../sources/tutorials/api/delete.md) e [exclusão de contas usando a interface](../../sources/tutorials/ui/delete-accounts.md). |
| Mapeamento hierárquico | Você pode visualizar um arquivo de origem hierárquico, como JSON ou Parquet, durante o processo de assimilação de dados. Veja o tutorial sobre [configuração de um fluxo de dados para conectores de armazenamento em nuvem na interface](../../sources/tutorials/ui/dataflow/batch/cloud-storage.md) para obter mais informações. |
| Suporte de API para mapeamento em fontes de transmissão | Agora você pode usar APIs para executar funções de mapeamento com fontes de transmissão. |
| Suporte à API para delimitadores personalizados para fontes de armazenamento em nuvem | Agora é possível coletar arquivos não delimitados por CSV usando fontes de armazenamento na nuvem. É possível usar qualquer delimitador de coluna única, como tabulação, vírgula, barra vertical, ponto e vírgula ou hash, para coletar arquivos simples em qualquer formato. |
| Suporte à sandbox para o conector do Adobe Audience Manager | O conector Audience Manager agora é sensível à sandbox. Os usuários podem permitir que o conector roteie conjuntos de dados de Audience Manager para a sandbox de sua escolha (incluindo sandboxes de não produção). A configuração é limitada a uma sandbox por organização. |
| Melhorias de UX | A assimilação baseada em arquivo agora pode ser acessada por meio do catálogo de fontes. |

Para saber mais sobre fontes, consulte a [visão geral das origens](../../sources/home.md).
