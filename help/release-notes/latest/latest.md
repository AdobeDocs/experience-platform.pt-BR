---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 11 de novembro de 2020
doc-type: release notes
last-update: November 10, 2020
author: crhoades, ens25212
translation-type: tm+mt
source-git-commit: 7c4b60dad1ad2071bb19a9b9e181f2db495187c2
workflow-type: tm+mt
source-wordcount: '2049'
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

Enquanto a Adobe estiver migrando o Data Lake da Gen1 para a Gen2, os usuários poderão ler a partir do Data Lake, mas todos os recursos que forem gravados no Data Lake serão afetados. O Adobe entrará em contato com os administradores de sistema para discutir o impacto da migração em detalhes e confirmar as datas e horas da migração para organizações IMS específicas.

Para obter mais informações, leia o guia [de migração do](../../landing/adls2-gen2-migration.md)Data Lake.

## [!DNL Access control] {#access-control}

[!DNL Experience Platform] aproveita perfis de produtos [Adobe Admin Console](https://adminconsole.adobe.com) para vincular usuários com permissões e caixas de proteção. As permissões controlam o acesso a uma variedade de recursos da plataforma, incluindo modelagem de dados, gerenciamento de perfis e administração de sandbox.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Permissões | Na guia [!DNL Admin Console], dentro de um perfil de [!DNL Platform] produto, você pode personalizar quais [!DNL Platform] recursos estão disponíveis para os usuários conectados a esse perfil. As categorias de permissão disponíveis incluem: **[!UICONTROL Modelagem]** de dados, **[!UICONTROL Gestão de dados]**, Gerenciamento **[!UICONTROL de]** Perfis, **[!UICONTROL Identity Management]**, Monitoramento **[!UICONTROL de]** dados, Administração, Administração do ************************ Sandbox, Destinos, Ingestão de dados,Data Science Workspace, Serviço de Query, e Governação de dados. |
| Acesso a caixas de proteção | A guia **[!UICONTROL Permissões]** em um perfil de [!DNL Platform] produto pode conceder aos usuários acesso a caixas de proteção específicas. Consulte a seção sobre [caixas de proteção](#sandboxes) abaixo para obter mais informações. |

Para obter mais informações, consulte a visão geral [do](../../access-control/home.md)controle de acesso.

## [!DNL Offer Decisioning] {#offer-decisioning}

[!DNL Offer Decisioning] é um Serviço de Aplicativo integrado ao [!DNL Experience Platform]. Ele permite que você aproveite [!DNL Platform] para oferecer a melhor oferta e experiência aos seus clientes em todos os pontos de contato no momento certo.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Biblioteca de ofertas centralizada | A interface na qual você cria e gerencia os diferentes elementos que compõem suas ofertas e define suas regras e restrições. |
| Mecanismo de decisão de oferta | O Mecanismo de decisão de Oferta aproveita [!DNL Platform] os dados e, [!DNL Real-time Customer Profiles]junto com a Biblioteca de Ofertas, para selecionar o momento certo, os clientes e canais aos quais as ofertas serão entregues. |

Para obter mais informações, consulte a [[!DNL Offer Decisioning]](https://experienceleague.adobe.com/docs/offer-decisioning/using/offer-decisioning-home.html?lang=en) documentação.

## [!DNL Sandboxes] {#sandboxes}

[!DNL Experience Platform] foi criada para enriquecer aplicativos de experiência digital em escala global. O Empresa geralmente executa vários aplicativos de experiência digital em paralelo e precisa atender ao desenvolvimento, teste e implantação desses aplicativos, garantindo a conformidade operacional. Para atender a essa necessidade, [!DNL Experience Platform] fornece caixas de proteção que dividem uma única [!DNL Platform] instância em ambientes virtuais separados para ajudar a desenvolver e desenvolver aplicativos de experiência digital.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Caixa de proteção de produção | [!DNL Experience Platform] fornece uma única caixa de proteção de produção, que não pode ser excluída ou redefinida. O número total de caixas de proteção disponíveis, produção e não produção, é determinado pela licença adquirida. |
| Caixas de proteção de não produção | É possível criar várias caixas de proteção de não produção para uma única [!DNL Platform] instância, permitindo testar recursos, executar experiências e fazer configurações personalizadas sem afetar a caixa de proteção de produção. |
| Comutador Sandbox | Na interface do [!DNL Experience Platform] usuário, o alternador da caixa de proteção no canto superior esquerdo da tela permite alternar entre as caixas de proteção disponíveis por meio de um menu suspenso. O alternador de sandbox também fornece uma função de pesquisa que permite filtrar por meio de caixas de proteção disponíveis. |
| `x-sandbox-name` header | Todas as chamadas para [!DNL Experience Platform] APIs agora devem incluir o novo `x-sandbox-name` cabeçalho, cujo valor faz referência ao `name` atributo da caixa de proteção em que a operação ocorrerá. |

Para obter mais informações, consulte a visão geral [das](../../sandboxes/home.md)caixas de proteção.

## [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] permite que os engenheiros de dados mapeiem, transformem e validem dados para e do Experience Data Model (XDM).

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Operações iterativas | [!DNL Data Prep] O mapeador agora oferece suporte para a execução de operações iterativas em uma hierarquia. |
| Função do mapeador | [!DNL Data Prep] O mapeador agora tem a capacidade de **não** copiar um atributo da origem para o XDM do público alvo. |

Para obter mais informações, consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md).

## Data Science Workspace {#dsw}

A Data Science Workspace usa o aprendizado de máquina e a inteligência artificial para criar insights de seus dados. Integrado ao Adobe Experience Platform, o Data Science Workspace ajuda você a fazer previsões usando seu conteúdo e ativos de dados nas soluções de Adobe. Uma das maneiras de fazer isso é usar a Data Science Workspace [!DNL JupyterLab]. [!DNL JupyterLab] é uma interface de usuário baseada na Web para [[!DNL Project Jupyter]](https://jupyter.org/) e é totalmente integrada ao Adobe Experience Platform. Ele fornece um ambiente de desenvolvimento interativo para que os cientistas de dados trabalhem com [!DNL Jupyter] notebooks, códigos e dados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| [!DNL JupyterLab] Modelo do Recipe Builder | Uso de notebooks para atender aos requisitos de receita e atualização de versões. [!DNL Python] A imagem básica de tempo de execução ML foi atualizada para usar [!DNL Python] 3.6.7 e um [!DNL Conda] ambiente exclusivamente. |

Para obter mais informações, leia o documento sobre como [criar uma receita usando notebooks](../../data-science-workspace/jupyterlab/create-a-recipe.md)de Júpiter.

## [!DNL Destinations] Serviço de {#destinations}

Na Plataforma [de dados do cliente em tempo real do](../../rtcdp/overview.md)Adobe, os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos destinos**

| Destino | Descrição |
| ----------- | ----------- |
| Microsoft Bing | O destino do Microsoft Bing o ajuda a executar o redirecionamento e a audiência de campanhas digitais direcionadas através do Microsoft Display Advertising. |
| A carteira comercial | O Trade Desk é uma plataforma de autoatendimento para que os compradores de anúncios executem redirecionamento e campanhas digitais direcionadas para audiência em fontes de exibição, vídeo e inventário móvel. |

<!-- | Braze | Braze is a comprehensive customer engagement platform that power relevant and memorable experiences between customers and the brands they love. |  -->

**Novos recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Campos obrigatórios | Os usuários podem marcar campos como obrigatórios, garantindo que somente os campos que contêm o campo obrigatório sejam exportados. |

<!-- | File scheduling | For both email based and cloud storage destinations, users can create a one-time export or create daily snapshots. |
| File encryption | For file based destinations, users can now add encryption to their exported files. | -->

Para obter mais informações, consulte a visão geral [de](../../rtcdp/destinations/destinations-overview.md)Destinos.

## Serviços inteligentes {#intelligent-services}

Os Serviços inteligentes capacitam analistas e profissionais de marketing a aproveitar o poder da inteligência artificial e do aprendizado de máquina em casos de uso de experiência do cliente. Isso permite que os analistas de marketing configurem previsões específicas para as necessidades de uma empresa usando configurações de nível empresarial sem a necessidade de especialização em ciência de dados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Conjunto de dados de Eventos de experiência do consumidor (CEE) | A criação de um conjunto de dados CEE agora oferece suporte à adição de campos de identidade ao conjunto de dados com o Editor de Schemas. A IA do cliente e do Attribution AI usam a identidade principal para combinar eventos. |

Para obter mais informações, leia a seção sobre como [adicionar campos de identidade a um conjunto de dados](../../intelligent-services/data-preparation.md#add-identity-fields-to-the-dataset) no guia de preparação de dados do Intelligent Services.

### Attribution AI

Attribution AI, como parte dos Serviços inteligentes, é um serviço de atribuição de vários canais, algorítmico, que calcula a influência e o impacto incremental das interações do cliente em relação aos resultados especificados.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Link da fonte de dados | O link para a fonte original do conjunto de dados pode ser visualizado e navegado até o painel direito de uma instância de serviço selecionada. |
| Editar nome da instância | Agora é possível modificar o nome de uma instância de Attribution AI existente. |
| Instância de clone | Copia a configuração da instância de serviço atualmente selecionada e permite modificações. |
| Modificar parâmetros de configuração da instância | Agora é possível modificar a configuração de uma instância de Attribution AI existente se ela ainda não começou a pontuação. |
| Uma pontuação | Agora você pode acionar a pontuação do modelo ad-hoc em suas instâncias de Attribution AI. |
| Passar por colunas | Agora você pode configurar colunas adicionais que serão adicionadas aos arquivos de pontuação de saída bruta para adicionar dimensões adicionais às visualizações de ferramentas do BI. |
| Ativação de instâncias e desativação | Agora você pode ativar e desativar o treinamento de modelo agendado e a pontuação de suas instâncias de Attribution AI. |
| Rastreamento de direitos | Você pode encontrar a quantidade total de insights de Atribuição consumidos pela sua conta no container de instância de criação. |
| Detalhamento do ponto de contato por posição | Um novo gráfico de insights que fornece uma análise de pontos de contato por posições de caminho de conversão. |
| Caminhos de conversão principais | Um novo gráfico de insights localizado na guia Análise de caminho. O gráfico contém uma lista dos cinco principais caminhos de conversão que mostram a sequência de pontos de contato do canal de marketing que resultaram em mais conversões. |
| Eficácia do ponto de contato | Fornece insights detalhados das três variáveis mais importantes pelas quais seu modelo avalia a eficácia do ponto de contato. As variáveis são a proporção de caminhos positivos e negativos tocados, a eficiência do ponto de contato e o volume do ponto de contato. |

Para obter mais informações, leia a visão geral [do](../../intelligent-services/attribution-ai/overview.md)Attribution AI.

### AI do cliente

A IA do cliente, como parte dos Serviços inteligentes, fornece aos comerciantes o poder de gerar previsões de clientes a nível individual com explicações. Com a ajuda de fatores influentes, a IA do cliente pode informar o que um cliente deve fazer e por que. Além disso, os profissionais de marketing podem se beneficiar das previsões e insights de IA do cliente para personalizar as experiências do cliente, atendendo às ofertas e mensagens mais apropriadas.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Link da fonte de dados | O link para a fonte original do conjunto de dados pode ser visualizado e navegado até o painel direito de uma instância de serviço selecionada. |
| Editar nome da instância | Você pode modificar o nome de uma instância de IA do cliente existente. |
| Modificar parâmetros de configuração da instância | Agora você pode modificar a configuração de uma instância do AI do cliente se ela ainda não tiver iniciado uma pontuação. |
| Instância de clone | Copia a configuração da instância de serviço atualmente selecionada e permite modificações. |
| Rastreamento de direitos | Você pode encontrar a quantidade total de perfis pontuados pela Inteligência Artificial do Cliente para sua conta no container de criação de instância. |
| Objetivo de previsão | A flexibilidade na criação de uma meta de previsão foi aumentada com novas opções para prever se algo &quot;ocorrerá&quot; ou &quot;não ocorrerá&quot;. Além disso, as opções para prever se &quot;todos&quot; os eventos ocorrem ou &quot;qualquer um&quot; dos eventos ocorrem quando vários eventos são usados foram adicionadas. |
| Derivação de fator influente | Os principais compartimentos de fatores influentes de propensão agora contêm detalhamentos. Os detalhamentos são um resumo de nível mais profundo dos valores para cada um dos principais fatores influentes dentro de um bucket de propensão. |

Para obter mais informações, leia a visão geral [da API do](../../intelligent-services/customer-ai/overview.md)cliente.

## Perfil do cliente em tempo real {#profile}

A Adobe Experience Platform permite que você direcione experiências coordenadas, consistentes e relevantes para seus clientes, independentemente de onde ou quando eles interagem com sua marca. Com o Perfil do cliente em tempo real, você pode ver uma visualização holística de cada cliente individual que combina dados de vários canais, incluindo dados online, offline, CRM e de terceiros. [!DNL Profile] permite consolidar seus dados de clientes diferentes em uma visualização unificada, oferecendo uma conta acionável e com carimbos de data e hora de cada interação com o cliente.

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Fluxo de trabalho de políticas de mesclagem atualizado | A plataforma atualizou a configuração da política de mesclagem para um novo fluxo de trabalho gradual. Esse fluxo de trabalho permite que os usuários reúnam fragmentos de dados de vários conjuntos de dados de Perfis e definam prioridade para como os dados são unidos nesses conjuntos de dados, a fim de criar uma visualização abrangente de cada indivíduo. Os usuários podem unir conjuntos de dados de Perfil individual XDM selecionados selecionando o método de mesclagem apropriado (ordem de data e hora ou precedência de conjunto de dados) e anexando conjuntos de dados ExperienceEvent aos conjuntos de dados de Perfil. |
| Visualização schema união | Na interface do usuário do Experience Platform, os usuários podem encontrar mais facilmente informações relacionadas a todos os schemas e conjuntos de dados que contribuem para o schema da união, bem como os principais atributos da superfície, como campos de identidade e relacionamento. Essas atualizações melhoram a capacidade de solucionar problemas e validar se os perfis estão configurados corretamente, se as identidades estão corretamente agrupadas e se os dados foram assimilados com êxito. |

Para obter mais informações sobre o Perfil do cliente em tempo real, incluindo tutoriais e práticas recomendadas para trabalhar com [!DNL Profile] dados, leia a visão geral [do Perfil do cliente em tempo](../../profile/home.md)real.

## [!DNL Sources] {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novas fontes**
| Recurso | Descrição |
| — | — |
| [!DNL Shopify] | Agora você pode se conectar [!DNL Shopify] a [!DNL Experience Platform] usar a [!DNL Flow Service] API ou a interface do usuário. Consulte a visão geral [do conector](../../sources/connectors/ecommerce/shopify.md) Shopify para obter mais informações. |

**Principais recursos**

| Recurso | Descrição |
| ------- | ----------- |
| Atualizar informações de conexão | Agora você pode atualizar os nomes, as descrições e as credenciais das conexões em lote existentes usando a [!DNL Flow Service] API e a interface do usuário. Para obter mais informações, consulte o tutorial sobre como [atualizar conexões usando a API](../../sources/tutorials/api/update.md) do Serviço de Fluxo e [editar detalhes da conta usando a interface do usuário](../../sources/tutorials/ui/monitor.md). |
| Excluir conexões | As conexões em lote que contêm erros ou se tornaram desnecessárias agora podem ser excluídas usando a [!DNL Flow Service] API e a interface do usuário. Para obter mais informações, consulte o tutorial sobre como [excluir conexões usando a API](../../sources/tutorials/api/delete.md) do Serviço de Fluxo e [excluir contas usando a interface do usuário](../../sources/tutorials/ui/delete-accounts.md). |
| Suporte a API para mapeamento em fontes de transmissão | Agora você pode usar as APIs para executar funções de mapeamento com fontes de transmissão. |
| Suporte de API para delimitadores personalizados para fontes de armazenamentos na nuvem | Agora é possível coletar arquivos não delimitados por CSV usando fontes de armazenamentos em nuvem. Você pode usar qualquer delimitador de coluna único, como tabulação, vírgula, barra vertical, ponto-e-vírgula ou hash, para coletar arquivos simples em qualquer formato. O padrão do valor é uma vírgula, se não for fornecida. |
| Suporte a sandbox para conector Adobe Audience Manager | O conector Audience Manager está agora habilitado para a caixa de proteção. Os usuários podem permitir que o conector roteie conjuntos de dados de Audience Manager para a caixa de proteção de sua escolha (incluindo caixas de proteção de não produção). A configuração é limitada a uma caixa de proteção por Organização IMS. |
| Melhorias no UX | A ingestão baseada em arquivo agora está acessível pelo catálogo de fontes. |

Para saber mais sobre fontes, consulte a visão geral [das](../../sources/home.md)fontes.