---
title: Interagir e adquirir novos clientes sem depender de cookies de terceiros
description: Saiba como engajar e adquirir novos clientes por meio de casos de uso de prospecção, sem depender de cookies de terceiros.
feature: Use Cases, Customer Acquisition
exl-id: b9e7b3af-2a13-4904-bd12-e3ed05a1988e
source-git-commit: e7c0551276d31d6809ace096c00e0dc2665090e6
workflow-type: tm+mt
source-wordcount: '2027'
ht-degree: 74%

---

# Interagir e adquirir novos clientes sem depender de cookies de terceiros

>[!AVAILABILITY]
>
>* Essa funcionalidade está disponível para clientes que licenciaram o Real-Time CDP (Serviço de aplicativo), Adobe Experience Platform Ativation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Leia mais sobre esses pacotes nas [descrições do produto](https://helpx.adobe.com/br/legal/product-descriptions.html?lang=pt-BR) e entre em contato com a pessoa representante da Adobe para obter mais informações.

Use o suporte a dados de terceiros da Real-Time CDP para expandir sua base de perfis com clientes potenciais de parceiros de dados e interaja com eles para conquistar ou alcançar novos clientes.

![Visão geral de alto nível do caso de uso de prospecção de clientes.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Por que considerar este caso de uso {#why-this-use-case}

As marcas estão enfrentando simultaneamente desafios assustadores de executar com responsabilidade casos de uso de aquisição de clientes topo de linha da funnel sem dependência de cookies de terceiros, orçamentos limitados e maior demanda de transparência e retorno sobre o investimento em anúncios.

A Adobe Real-Time Customer Data Platform pode ajudar as marcas a fazer a transição segura de seus casos de uso compatíveis com a Plataforma de gerenciamento de dados (DMP) para alternativas sem cookies, de uma forma que promova a total sofisticação e o poder da segmentação de autoatendimento, curadoria de público-alvo e ativação em um único sistema. Tudo isso sem comprometer o foco inabalável da Adobe no uso responsável de dados por meio de uma estrutura patenteada de consentimento e governança de dados.

Por exemplo, siga as etapas descritas neste caso de uso quando precisar executar uma campanha para atrair prospetos para se tornarem usuários ou clientes conhecidos.

## Pré-requisitos e planejamento {#prerequisites-and-planning}

Ao considerar entrar em contato com novos clientes e adquiri-los, considere os seguintes pré-requisitos no processo de planejamento:

* Com que frequência se espera que os atributos fornecidos pelo parceiro sejam assimilados na Real-Time CDP e atualizados?
* Quais identidades seus destinos downstream exigem?
* Verifique se os identificadores assimilados são acionáveis no downstream
* Os dados do parceiro que você está assimilando estão vinculados a um identificador durável amplamente aceito, como o PII (Informações pessoais identificáveis), PII com hash ou um identificador de parceiro?
* Quais políticas de uso de dados você precisa conhecer da perspectiva do parceiro e de sua própria equipe jurídica, de privacidade ou de conformidade?

## Como atingir o caso de uso: visão geral de alto nível {#achieve-the-use-case-high-level}

Antes de expandir a Real-Time CDP para engajar e conquistar novos clientes, use-a para criar uma base robusta para seus dados primários. Os fluxos de trabalho que permitem obter esse caso de uso são semelhantes aos usados para interagir com clientes conhecidos.

![Visão geral de alto nível do caso de uso de prospecção de clientes.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. Como **cliente**, você licencia perfis de clientes potenciais de um ou mais **parceiros de dados** para ajudar na conquista de clientes do topo do funil.
2. Como **cliente**, você estende os dados do seu perfil e o modelo de governança para assimilar a lista de perfis de clientes potenciais fornecida pelo **parceiro**.
3. Como **cliente**, você carrega perfis de clientes potenciais na Real-Time CDP e cria políticas de governança para garantir um uso responsável.
4. Como **cliente**, você cria públicos-alvo focados a partir da lista de perfis de clientes potenciais.
5. Como **cliente**, você ativa potenciais públicos-alvo para destinos que aceitam as identidades disponíveis em sua lista de clientes potenciais.
6. Se necessário, trabalhe com o **parceiro de dados** para ativação da última milha de públicos-alvo para os destinos de mídia paga desejados.

## Apresentação em vídeo {#video-walkthrough}

Assista ao tutorial em vídeo abaixo para obter uma apresentação de como alcançar e engajar possíveis públicos-alvo:

>[!VIDEO](https://video.tv.adobe.com/v/3423071/?learn=on)

## Como atingir o caso de uso: instruções passo a passo {#step-by-step-instructions}

Leia as seções abaixo, que incluem links para documentação adicional, para concluir cada uma das etapas da visão geral de alto nível acima.

### Elementos e funcionalidade da interface que serão utilizados {#ui-functionality-and-elements}

Ao concluir as etapas para implementar o caso de uso, você usará a seguinte funcionalidade e elementos da interface da Real-Time CDP (listados na ordem em que serão usados). Verifique se possui as permissões de controle de acesso baseadas em atributos necessárias para todas essas áreas ou solicite ao(à) administrador(a) do sistema que as conceda a você.

* [Identidades](/help/identity-service/features/namespaces.md)
* [Esquemas](/help/xdm/home.md)
* [Rótulos de uso de dados](/help/data-governance/labels/overview.md)
* [Conjuntos de dados](/help/catalog/datasets/overview.md)
* [Origens](/help/sources/home.md)
* [Perfis em potencial](/help/profile/ui/prospect-profile.md)
* [Públicos-alvo em potencial](/help/segmentation/types/prospect-audiences.md)
* [Destinos](/help/destinations/home.md)

### Detalhes de licença de perfil de terceiros do parceiro {#license-profiles-from-partner}

Esta etapa é abordada nos [pré-requisitos](#prerequisites-and-planning) e a Adobe pressupõe que você possui acordos contratuais definidos com fornecedores de dados confiáveis para assimilar os perfis de clientes potenciais fornecidos pelo parceiro de dados.

### Estenda seus dados de perfil e modelo de governança para acomodar os perfis de clientes potenciais fornecidos por parceiros {#extend-governance-model}

Como preparo para receber perfis de clientes potenciais do seu parceiro de dados, você deve estender a estrutura de gerenciamento de dados na Real-Time CDP para acomodar esse novo tipo de perfil.

Os componentes de identidade, gerenciamento de dados e governança que você usará são:

* Um novo tipo de identidade **[!UICONTROL Partner ID]** para os perfis fornecidos pelo parceiro
* Uma nova classe XDM **[!UICONTROL XDM Individual Prospect Profile]**
* **(A documentação será disponibilizada em breve)** Grupos de campos personalizados para oferecer suporte a dados de parceiros
* **(A documentação será disponibilizada em breve)** Rótulos de terceiros que serão adicionados aos atributos provenientes de parceiros

#### Criar um namespace de identidade de ID de parceiro {#create-partner-id-namespace}

Comece criando um novo tipo de identidade para os perfis que você receberá do parceiro. Para fazer isso, na seção Identity, você deve criar um novo namespace de identidade do tipo **[!UICONTROL Partner ID]**.

![Crie um novo namespace de identidade de ID de parceiro.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* Leia mais sobre namespaces de ID de parceiro na [seção de tipos de identidade](/help/identity-service/features/namespaces.md).
* Leia sobre [como definir campos de identidade](/help/xdm/ui/fields/identity.md) na interface da Experience Platform.

#### Criar um novo esquema com a classe **[!UICONTROL XDM Individual Prospect Profile]**

Em seguida, em **[!UICONTROL Data Management]** > **[!UICONTROL Schemas]**, crie um novo esquema e atribua a ele a classe **[!UICONTROL XDM Individual Prospect Profile]**.

![Pesquise a classe Perfil individual de cliente potencial do XDM no construtor de esquemas XDM.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Leia como [criar e editar esquemas na interface](/help/xdm/ui/resources/schemas.md) e obtenha informações completas sobre a classe Perfil individual de cliente potencial do XDM (o link será disponibilizado em breve).

A classe **[!UICONTROL XDM Individual Prospect Profile]** vem pré-configurada com os campos mostrados abaixo. Para enriquecer o esquema com atributos dos perfis de clientes potenciais fornecidos pelo parceiro, você pode criar um novo grupo de campos com os atributos esperados e adicioná-lo ao esquema ou usar um dos grupos de campos pré-configurados fornecidos pela Adobe.

![Campos pré-configurados para a classe Perfil individual de cliente potencial do XDM.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

Em seguida, selecione a identidade partnerID criada anteriormente como a identidade principal do esquema. Os registros de perfil devem ter um identificador principal. Essa etapa é necessária para garantir que os dados de clientes potenciais possam ser carregados no armazenamento de Perfil e disponibilizados para segmentação e ativação.

>[!AVAILABILITY]
>
>Os perfis de clientes potenciais são restritos automaticamente a usar somente namespaces de ID do tipo ID de parceiro. Isso é intencional e garante uma separação clara entre os perfis primários e os clientes potenciais.

![Selecione a ID de parceiro configurada anteriormente como a identidade principal do esquema.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Observe que o esquema ainda não está habilitado para o perfil. Clique no botão de perfil para habilitar este esquema para inclusão no serviço de perfil. Para obter mais informações sobre como habilitar o esquema para uso no perfil do cliente em tempo real, leia o [tutorial de criação de esquema.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Habilitar esquema para o perfil.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Adicione o rótulo de governança de dados de terceiros a todos os campos do esquema

Considere adicionar rótulos de governança de dados de terceiros a todos os campos que compõem o esquema. Isso é importante para garantir o uso responsável de dados de terceiros e minimizar o risco de vazamento de dados. Encontre mais informações sobre [rótulos de governança de dados de terceiros](../../data-governance/labels/reference.md#partner-ecosystem-labels).

Para fazer isso, siga as etapas abaixo:

1. Navegue até o esquema criado e selecione a guia **[!UICONTROL Labels]**.
2. Selecione todos os campos neste esquema usando o botão de caixa de seleção na parte superior e clique no ícone de lápis à direita para aplicar rótulos de governança de dados a este esquema.
3. Selecione o Rótulo **[!UICONTROL Partner Ecosystem]** nas categorias à esquerda.
4. Escolha o rótulo chamado **[!UICONTROL Third Party]** e selecione **[!UICONTROL Save]**.
5. Observe que todos os campos do esquema agora carregam o rótulo selecionado na etapa anterior.

>[!SUCCESS]
>
>O esquema agora está pronto para uso e você pode prosseguir para a próxima etapa para assimilar dados de clientes potenciais de seu parceiro de dados.

Além disso, nesta etapa, pense em como seu modelo de governança de dados mudará à medida que você expande sua estratégia de gerenciamento de dados para incluir dados de terceiros fornecidos por parceiros. Explore as considerações nos links da documentação abaixo:

* (**Em breve**) Mantenha os dados de terceiros em um conjunto de dados separado para que seja fácil excluí-los e desfazer integrações.
* (**Em breve**) Use a funcionalidade [expiração do conjunto de dados](/help/hygiene/ui/dataset-expiration.md) no conjunto de dados para clientes que adquiriram o complemento de higiene de dados.
* (**Em breve**) Tenha cuidado ao criar conjuntos de dados derivados que extraem dados de terceiros, pois uma vez misturados, a única solução para remover os dados de terceiros é excluir todo o conjunto de dados derivado.

### Carregar a lista de perfis de clientes potenciais e inspecionar a exibição de clientes potenciais

Depois de preparar o modelo de dados para gerenciar perfis de clientes potenciais, é hora de assimilar os dados.

#### Criar um conjunto de dados e carregar dados de clientes potenciais de amostra

Para carregar alguns dados de amostra e preencher perfis de clientes potenciais, crie um conjunto de dados e faça upload do arquivo recebido do parceiro de dados. Conclua as etapas abaixo:

1. Navegue até **[!UICONTROL Data Management]** > **[!UICONTROL Datasets]** e selecione **[!UICONTROL Create dataset]**.
2. Selecione Criar conjunto de dados a partir do esquema
3. Selecione o esquema criado em uma etapa anterior
4. Forneça um nome e, opcionalmente, uma descrição ao conjunto de dados.
5. Selecione **[!UICONTROL Finish]**.

![Uma gravação das etapas para criar um conjunto de dados para perfis de clientes potenciais.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Observe que, semelhante à etapa de criação de um esquema, é necessário habilitar a inclusão do conjunto de dados no perfil do cliente em tempo real. Para obter mais informações sobre como habilitar o conjunto de dados para uso no perfil do cliente em tempo real, leia o [tutorial de criação de esquemas.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Habilite o conjunto de dados para o perfil.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Para carregar um arquivo recebido do parceiro no conjunto de dados, selecione o conjunto de dados, role para baixo no painel direito e selecione **[!UICONTROL Add data]**. Você pode arrastar e soltar o arquivo ou selecionar **[!UICONTROL Choose files]** para navegar até o local do arquivo e selecioná-lo.

![Adicione um arquivo ao conjunto de dados.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

Depois de carregar a lista de perfis do parceiro de dados na Real-Time CDP, prossiga para a seção [Inspecionar perfis de clientes potenciais carregados](#inspect-profiles) para verificar se os clientes potenciais estão preenchidos na interface.

#### Assimilar dados de clientes potenciais por meio de conectores de origem

Você pode configurar importações de arquivos recorrentes para assimilar dados do parceiro por meio de um conector de origem e trazer a lista de perfis de clientes potenciais para a Real-Time CDP.

Alguns conectores de origem recomendados para essa finalidade estão listados abaixo, mas observe que qualquer método de ingestão baseado em arquivo na Real-Time CDP funcionará para a sua finalidade.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

Depois de carregar a lista de perfis do parceiro de dados na Real-Time CDP, prossiga para a próxima seção para verificar se os perfis de clientes potenciais estão sendo preenchidos na interface.

#### Inspecione os perfis de clientes potenciais carregados {#inspect-profiles}

Para ver a lista de perfis de cliente potencial, navegue até **[!UICONTROL Prospects]** > **[!UICONTROL Profiles]** no painel esquerdo.

Observe que pode levar até duas horas para que os perfis de cliente potencial que você acabou de carregar no Real-Time CDP sejam mostrados na exibição **[!UICONTROL Browse]** da tela Perfil de Cliente Potencial. Se a página exibir a mensagem “Não foi possível encontrar perfis de clientes potenciais no momento”, tente novamente mais tarde. Depois de algum tempo de espera, perfis de clientes potenciais devem começar a aparecer na exibição **[!UICONTROL Browse]**.

>[!TIP]
>
>Observe a presença da coluna **[!UICONTROL Identity Namespace]**. Se você estiver trabalhando com vários fornecedores de dados, use essa coluna para deduzir a origem dos perfis de clientes potenciais.

![Exibição dos perfis de clientes potenciais carregados na Real-Time CDP.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

Você também pode selecionar qualquer perfil de cliente potencial para uma inspeção adicional, conforme mostrado abaixo.

![Exemplo de como inspecionar perfis de clientes potenciais.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

Leia mais sobre [perfis de clientes potenciais](/help/profile/ui/prospect-profile.md).

### Criar públicos-alvo de clientes potenciais {#create-prospect-audiences}

Use a funcionalidade de segmentação na Real-Time CDP para criar públicos-alvo a partir de perfis de clientes potenciais. Use as regras de segmentação desejadas para criar públicos-alvo personalizados.

Para começar e criar públicos-alvo compostos por perfis de clientes potenciais, navegue até **[!UICONTROL Prospects]** > **[!UICONTROL Audiences]**.

![Exibição de públicos-alvo de clientes potenciais.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

Observe que a experiência de criação de públicos-alvo para perfis de clientes potenciais é diferente da experiência de criação de públicos-alvo a partir de clientes primários conhecidos. Essa visualização está limitada a:

* Atributos da classe de clientes potenciais criada anteriormente.
* Avaliação de perfis em lote, apenas.
* Não permite a criação de públicos-alvo com base em eventos de série temporal.

Leia mais sobre [públicos-alvo em potencial](/help/segmentation/types/prospect-audiences.md).

### Ativar perfis de clientes potenciais para destinos {#activate-to-destinations}

Utilize os públicos-alvo de clientes potenciais exportando-os para destinos. Atualmente, apenas alguns destinos de armazenamento em nuvem oferecem suporte à ativação de perfis de prospecto.

![Destinos que oferecem suporte a públicos-alvo em potencial.](/help/destinations/assets/ui/activate-prospect-audiences/data-types-filter.png)

[Leia mais](/help/destinations/ui/activate-prospect-audiences.md) sobre como ativar clientes potenciais para destinos de armazenamento na nuvem.

## Outros casos de uso obtidos por meio da compatibilidade com dados de parceiros {#other-use-cases}

Conheça outros casos de uso habilitados por meio da compatibilidade com dados de parceiros na Real-Time CDP:

* [Suplemente perfis próprios com atributos de parceiros de dados confiáveis para melhorar sua base de dados, obter novos insights sobre sua base de clientes e aprimorar a otimização do público-alvo.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* [Personalize experiências no site para visitantes desconhecidos usando o reconhecimento de visitante auxiliado por parceiro](/help/rtcdp/partner-data/onsite-personalization.md) durante a visita sem que o usuário se autentique ou tenha um histórico anterior com sua marca.
* [Ativação ampliada de perfis de prospecto e públicos-alvo de prospecto](/help/destinations/ui/activate-prospect-audiences.md) para selecionar destinos.
