---
title: (Beta) Envolver e adquirir novos clientes por meio de casos de uso de prospecção
description: Saiba como envolver e adquirir novos clientes por meio de casos de uso de prospecção, habilitados pelo suporte a dados de parceiros no Real-Time CDP.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: d0227dd8dc3d79674d954899e2724d2893e16b73
workflow-type: tm+mt
source-wordcount: '1953'
ht-degree: 15%

---

# Envolver e adquirir novos clientes por meio de casos de uso de prospecção

>[!AVAILABILITY]
>
>* Essa funcionalidade beta está disponível para clientes que possuem o Real-Time CDP (Serviço de aplicativo), Ativação da Adobe Experience Platform, Real-time CDP, Real-Time CDP Prime ou Real-Time CDP Ultimate licenciados. Leia mais sobre esses pacotes nas [descrições do produto](https://helpx.adobe.com/legal/product-descriptions.html?lang=pt-BR) e entre em contato com a pessoa representante da Adobe para obter mais informações.

Use o suporte a dados de terceiros no Real-Time CDP para expandir sua base de perfis com perfis de prospecto de parceiros de dados e interagir com eles para adquirir ou alcançar novos clientes.

![Visão geral visual de alto nível do caso de uso de prospecção de clientes.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-overview.png)

## Pré-requisitos e planejamento {#prerequisites-and-planning}

Ao considerar entrar em contato com novos clientes e adquiri-los usando o suporte a dados de parceiros no Real-Time CDP, considere os seguintes pré-requisitos no processo de planejamento:

* Qual é a cadência com que você espera que os perfis fornecidos pelo parceiro sejam assimilados na Real-Time CDP e atualizados?
* Quais identidades seus destinos downstream exigem?
* Verifique se os identificadores assimilados são acionáveis downstream
* Os dados do parceiro que você está assimilando estão vinculados a um identificador durável amplamente aceito, como Informações pessoais identificáveis (PII), PII com hash ou um identificador de parceiro?
* Quais políticas de uso de dados você precisa conhecer da perspectiva do parceiro e de sua própria equipe jurídica, de privacidade ou de conformidade?

## Como atingir o caso de uso: visão geral de alto nível {#achieve-the-use-case-high-level}

Antes de expandir o Real-Time CDP para engajar e adquirir novos clientes, certifique-se de usar o Real-Time CDP para criar uma base robusta para seus dados originais. Os fluxos de trabalho para obter esse caso de uso são semelhantes aos fluxos de trabalho para interagir com seus clientes conhecidos.

![Visão geral visual de alto nível do caso de uso de prospecção de clientes.](/help/rtcdp/assets/partner-data/prospecting/prospecting-use-case-steps.png)

1. Como um **cliente**, você licencia perfis de cliente potencial de um ou mais **parceiros de dados** para ajudar a liderar a aquisição de clientes no funil.
2. Como um **cliente**, você estende os dados do seu perfil e o modelo de governança para assimilar a **parceiro**- lista fornecida de perfis de prospecto.
3. Como um **cliente**, você carrega perfis de prospecto no Real-Time CDP e cria políticas de governança para garantir um uso responsável.
4. Como um **cliente**, você cria públicos-alvo focados a partir da lista de perfis de prospecto.
5. Como um **cliente**, você ativa públicos-alvo de prospecto para destinos que estão aceitando as identidades disponíveis em sua lista de prospetos.
6. Se necessário, trabalhe com a **parceiro de dados** para ativação da última milha de públicos-alvo para os destinos de mídia paga desejados.

## Como atingir o caso de uso: instruções passo a passo {#step-by-step-instructions}

Leia as seções abaixo, que incluem links para documentação adicional, para concluir cada uma das etapas da visão geral de alto nível acima.

### Funcionalidade e elementos da interface do usuário que você usará {#ui-functionality-and-elements}

Ao concluir as etapas para implementar o caso de uso, você usará a seguinte funcionalidade do Real-Time CDP e os elementos da interface do usuário (listados na ordem em que serão usados). Verifique se você tem as permissões de controle de acesso baseadas em atributos necessárias para todas essas áreas ou peça ao administrador do sistema para conceder as permissões necessárias.

* [Identidades](/help/identity-service/namespaces.md)
* [Esquemas](/help/xdm/home.md)
* [Rótulos de uso de dados](/help/data-governance/labels/overview.md)
* [Conjuntos de dados](/help/catalog/datasets/overview.md)
* [Fontes](/help/sources/home.md)
* Perfis (link para perfis de cliente potencial)
* Públicos (link para públicos-alvo potenciais)
* [Destinos](/help/destinations/home.md)

### Detalhes do perfil de terceiros da licença do parceiro {#license-profiles-from-partner}

Esta etapa é abordada na seção [pré-requisitos](#prerequisites-and-planning) A e a Adobe pressupõem que você tenha os contratos certos em vigor com fornecedores de dados confiáveis para assimilar perfis de prospecto fornecidos pelo parceiro de dados.

### Estender os dados do perfil e o modelo de governança para acomodar os perfis de prospecto fornecidos pelo parceiro {#extend-governance-model}

Como preparo para receber perfis de prospecto do seu parceiro de dados, você deve estender a estrutura de gerenciamento de dados no Real-Time CDP para acomodar esse novo tipo de perfil.

Os componentes de identidade, gerenciamento de dados e governança que você usará são:

* Um novo **[!UICONTROL ID do Parceiro]** tipo de identidade para os perfis fornecidos pelo parceiro
* Um novo **[!UICONTROL Perfil de cliente potencial individual XDM]** Classe XDM
* **(A documentação será disponibilizada em breve)** Grupos de campos personalizados para o suporte a dados de parceiros
* **(A documentação será disponibilizada em breve)** Rótulos de terceiros que você adicionará aos atributos provenientes de parceiros

#### Criar um namespace de identidade da ID de parceiro

Comece criando um novo tipo de identidade para os perfis que você receberá do parceiro. Para fazer isso, na seção Identity, você deve criar um novo namespace de identidade do tipo **[!UICONTROL ID do Parceiro]**.

![Criar um novo namespace de identidade da ID de parceiro.](/help/rtcdp/assets/partner-data/prospecting/create-partner-identity-namespace.png)

* Leia mais sobre os namespaces da ID de parceiro na [seção de tipos de identidade](/help/identity-service/namespaces.md).
* Leia sobre [como definir campos de identidade](/help/xdm/ui/fields/identity.md) na interface da Experience Platform.

#### Crie um novo esquema com o **[!UICONTROL Perfil de cliente potencial individual XDM]** classe

Próximo, em **[!UICONTROL Gerenciamento de dados]** > **[!UICONTROL Esquemas]**, crie um novo esquema e atribua a ele a função **[!UICONTROL Perfil de cliente potencial individual XDM]** classe.

![Pesquise a classe Perfil de cliente potencial individual XDM no construtor de esquema XDM.](/help/rtcdp/assets/partner-data/prospecting/xdm-individual-prospect-class.png)

Ler como [criar e editar esquemas na interface](/help/xdm/ui/resources/schemas.md) e obtenha informações completas sobre a classe Perfil de cliente potencial individual XDM (link futuro).

A variável **[!UICONTROL Perfil de cliente potencial individual XDM]** A classe vem pré-configurada com os campos mostrados abaixo. Para enriquecer seu esquema com atributos fornecidos pelo parceiro para os perfis de cliente potencial, você pode criar um novo grupo de campos com os atributos esperados e adicioná-lo ao esquema ou usar um dos grupos de campos pré-configurados fornecidos pelo Adobe.

![Campos pré-configurados para a classe de Perfil de Cliente Potencial Individual XDM.](/help/rtcdp/assets/partner-data/prospecting/preconfigured-fields-individual-prospect-class.png)

Em seguida, selecione a identidade partnerID criada anteriormente como a identidade principal do esquema. Os registros de perfil devem ter um identificador principal. Essa etapa é necessária para garantir que os dados de prospecto possam ser carregados no armazenamento de perfis e disponibilizados para segmentação e ativação.

>[!AVAILABILITY]
>
>Os perfis de clientes potenciais são restritos automaticamente a usar somente namespaces de ID do tipo de ID do parceiro. Isso ocorre por design e garante uma separação clara entre os perfis originais e de prospecto.

![Selecione a ID do parceiro configurada anteriormente como identidade principal no esquema.](/help/rtcdp/assets/partner-data/prospecting/select-partner-id-as-primary-identity.gif)

Observe que o esquema ainda não está ativado para o perfil. Alterne o botão de perfil para habilitar este esquema para inclusão no serviço de perfil. Para obter mais informações sobre como ativar o esquema para uso no Perfil do cliente em tempo real, leia o [criar tutorial de esquema.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Habilitar esquema para perfil.](/help/rtcdp/assets/partner-data/prospecting/enable-schema-for-profile.png)

#### Adicione o rótulo de governança de dados de terceiros a todos os campos no esquema

Considere adicionar rótulos de governança de dados de terceiros a todos os campos que compõem o esquema. Isso é importante para garantir o uso responsável de dados de terceiros e minimizar o risco de vazamento de dados. Encontre mais informações sobre rótulos de governança de dados de terceiros (adicione link para documentos da Jordânia)

Para fazer isso, siga as etapas abaixo:

1. Navegue até o esquema criado e selecione o **[!UICONTROL Rótulos]** guia.
2. Selecione todos os campos neste esquema usando o botão de caixa de seleção na parte superior e, em seguida, clique no ícone de lápis à direita para aplicar rótulos de governança de dados a este esquema.
3. Selecione o **[!UICONTROL Ecossistema de parceiros]** Etiqueta das categorias à esquerda.
4. Escolha o rótulo chamado **[!UICONTROL Terceiros]** e selecione **[!UICONTROL Salvar]**.
5. Observe que todos os campos no esquema agora carregam o rótulo selecionado na etapa anterior.

>[!SUCCESS]
>
>Seu esquema agora está pronto para uso e você pode prosseguir para a próxima etapa para assimilar dados de prospecto do seu parceiro de dados.

Além disso, nesta etapa, pense em como seu modelo de governança de dados mudará à medida que você expande sua estratégia de gerenciamento de dados para incluir dados de terceiros fornecidos por parceiros. Explore as considerações nos links da documentação abaixo:

* (**Em breve**) Mantenha os dados de terceiros em um conjunto de dados separado para que seja fácil excluí-los e desfazer integrações.
* (**Em breve**) Use a funcionalidade [expiração do conjunto de dados](/help/hygiene/ui/dataset-expiration.md) no conjunto de dados para clientes que adquiriram o complemento de higiene de dados.
* (**Em breve**) Tenha cuidado ao criar conjuntos de dados derivados que extraem dados de terceiros, pois uma vez misturados, a única solução para remover os dados de terceiros é excluir todo o conjunto de dados derivado.

### Carregar a lista de perfis de cliente potencial e inspecionar a exibição de perfis de cliente potencial

Depois de preparar seu modelo de dados para gerenciar perfis de clientes potenciais, é hora de assimilar os dados.

#### Criar um conjunto de dados e carregar dados de cliente potencial de amostra

Para carregar alguns dados de amostra e preencher perfis de cliente potencial, crie um conjunto de dados e faça upload de um arquivo recebido do parceiro de dados. Conclua as etapas abaixo:

1. Navegue até **[!UICONTROL Gerenciamento de dados]** > **[!UICONTROL Conjuntos de dados]** e selecione **[!UICONTROL Criar conjunto de dados]**.
2. Selecione Criar conjunto de dados a partir do esquema
3. Selecione o schema criado em uma etapa anterior
4. Dê um nome e, opcionalmente, uma descrição ao conjunto de dados.
5. Selecione **[!UICONTROL Concluir]**.

![Uma gravação das etapas para criar um conjunto de dados para perfis de cliente potencial.](/help/rtcdp/assets/partner-data/prospecting/create-dataset-for-prospect-profiles.gif)

Observe que, semelhante à etapa para criar um esquema, é necessário ativar o conjunto de dados para ser incluído no Perfil do cliente em tempo real. Para obter mais informações sobre como ativar o conjunto de dados para uso no Perfil do cliente em tempo real, leia o [criar tutorial de esquema.](/help/xdm/tutorials/create-schema-ui.md#profile)

![Ativar conjunto de dados para perfil.](/help/rtcdp/assets/partner-data/prospecting/enable-dataset-for-profile.png)

Para carregar um arquivo recebido do parceiro no conjunto de dados, selecione o conjunto de dados, role para baixo no painel direito e selecione **[!UICONTROL Adicionar dados]**. Você pode arrastar e soltar o arquivo ou selecionar **[!UICONTROL Escolher arquivos]** para navegar até o local do arquivo e selecione-o.

![Adicionar arquivo ao conjunto de dados.](/help/rtcdp/assets/partner-data/prospecting/add-file-to-dataset.png)

Depois de carregar a lista de perfis do parceiro de dados na Real-Time CDP, prossiga para a [Inspect na seção de perfis de cliente potencial carregados](#inspect-profiles) para verificar se os perfis de cliente potencial estão preenchendo na interface do usuário.

#### Assimilar dados de prospecto por meio de conectores de origem

Você pode configurar importações de arquivos recorrentes para assimilar dados do parceiro por meio de um conector de origem e trazer a lista de perfis de prospecto para a Real-Time CDP.

Alguns conectores de origem recomendados para essa finalidade estão listados abaixo, mas observe que qualquer método de assimilação baseado em arquivo no Real-Time CDP funciona para a sua finalidade.

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

Depois de carregar a lista de perfis do parceiro de dados no Real-Time CDP, prossiga para a próxima seção para verificar se os perfis de prospecto estão sendo preenchidos na interface do usuário.

#### Inspect os perfis de cliente potencial carregados {#inspect-profiles}

Para ver a lista de perfis de cliente potencial, navegue até **[!UICONTROL Clientes potenciais]** > **[!UICONTROL Perfis]** no painel esquerdo.

Observe que pode levar até duas horas para que os perfis de cliente potencial que você acabou de carregar no Real-Time CDP sejam exibidos no **[!UICONTROL Procurar]** exibição da tela Perfil de Cliente Potencial. Se a página exibir a mensagem &quot;Não há perfis de prospecto a serem navegados no momento&quot;, tente novamente depois de algum tempo. Depois de algum tempo de espera, perfis de prospecto devem começar a aparecer no **[!UICONTROL Procurar]** exibição.

>[!TIP]
>
>Observe a presença do **[!UICONTROL Namespace de identidade]** coluna. Se você estiver trabalhando com vários fornecedores de dados, use essa coluna para inferir a origem dos perfis de prospecto.

![Exibição dos perfis de cliente potencial carregados no Real-Time CDP.](/help/rtcdp/assets/partner-data/prospecting/prospect-profiles-view.png)

Você também pode selecionar qualquer perfil de cliente potencial para inspeção adicional, conforme mostrado abaixo.

![Exibição de como inspecionar perfis de cliente potencial.](/help/rtcdp/assets/partner-data/prospecting/inspect-prospect-profile.gif)

(**Em breve**) Leia mais sobre perfis de clientes potenciais.

### Criar públicos-alvo potenciais {#create-prospect-audiences}

Use a funcionalidade de segmentação no Real-Time CDP para criar públicos-alvo a partir de perfis de clientes potenciais. Use as regras de segmentação desejadas para criar públicos-alvo personalizados.

Para começar e criar públicos-alvo compostos de perfis de prospecto, acesse **[!UICONTROL Clientes potenciais]** > **[!UICONTROL Públicos-alvo]**.

![Exibição de públicos-alvo potenciais.](/help/rtcdp/assets/partner-data/prospecting/prospect-audiences.png)

Observe que a experiência de criação de público-alvo para perfis de prospecto é diferente da experiência de criação de públicos-alvo de seus clientes primários conhecidos. Essa visualização está limitada a:

* Atributos da classe de cliente potencial criada anteriormente.
* Somente avaliação do perfil de lote.
* Não é compatível com a criação de públicos-alvo com base em eventos de série temporal.

(**Em breve**) Leia mais sobre públicos-alvo potenciais.

### Ativar perfis de cliente potencial para destinos {#activate-to-destinations}

Use os públicos potenciais exportando-os para destinos. Atualmente, apenas certos destinos, como [Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) ou o [!BADGE Alfa]{type=Informative}[LiveRamp](/help/destinations/catalog/advertising/liveramp-onboarding.md) suporte de destino à ativação de perfis de cliente potencial.

## Outros casos de uso obtidos por meio da compatibilidade com dados de parceiros {#other-use-cases}

Conheça outros casos de uso habilitados por meio da compatibilidade com dados de parceiros na Real-Time CDP:

* [!BADGE Beta]{type=Informative}[Suplemente perfis próprios com atributos de parceiros de dados confiáveis para melhorar sua base de dados, obter novos insights sobre sua base de clientes e aprimorar a otimização do público-alvo.](/help/rtcdp/partner-data/supplement-first-party-profiles.md)
* (**Em breve**) [!BADGE Beta]{type=Informative}**Aproveite o reconhecimento auxiliado por parceiros** para personalizar experiências no site durante a visita e para redirecionamento fora do site após a visita, sem a necessidade de autenticação do usuário ou um histórico anterior com sua marca.