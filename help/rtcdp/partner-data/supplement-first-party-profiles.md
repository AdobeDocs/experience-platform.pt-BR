---
title: Suplementar perfis próprios com atributos fornecidos por parceiros
description: Saiba como suplementar perfis próprios com atributos de parceiros de dados confiáveis para melhorar sua base de dados, obter novos insights sobre sua base de clientes e aprimorar a otimização do público-alvo.
feature: Use Cases, Profile Enrichment
exl-id: ee21b988-88f9-4c8e-bd82-7fc55c37ec24
source-git-commit: 7ee472294e8f255d9de3c15982a6f5d2d3654755
workflow-type: tm+mt
source-wordcount: '1249'
ht-degree: 72%

---

# Suplementar perfis próprios com atributos fornecidos por parceiros

>[!AVAILABILITY]
>
>* Essa funcionalidade está disponível para clientes que licenciaram o Real-Time CDP (Serviço de aplicativo), Adobe Experience Platform Ativation, Real-Time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate. Leia mais sobre esses pacotes nas [descrições do produto](https://helpx.adobe.com/br/legal/product-descriptions.html?lang=pt-BR) e entre em contato com a pessoa representante da Adobe para obter mais informações.

Suplemente perfis próprios com atributos de parceiros de dados confiáveis para melhorar sua base de dados, obter novos insights sobre sua base de clientes e aprimorar a otimização do público-alvo.

![Visão geral de alto nível visual do caso de uso enriquecimento de perfis com atributos fornecidos por parceiros.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-overview.png)

## Por que considerar este caso de uso {#why-this-use-case}

A maioria das marcas, mesmo aquelas ricas com dados primários, pode se beneficiar da simplificação de seus dados e de obter uma compreensão mais diferenciada dos clientes, seus comportamentos, padrões e preferências.

A Adobe Real-time Customer Data Platform pode ajudar as marcas a complementar com responsabilidade seus dados primários com insights, identificadores e atributos valiosos de um ou mais parceiros confiáveis.

A Adobe entende que não há uma abordagem única para todos e permite uma interoperabilidade perfeita com parceiros de dados e identidade para promover um engajamento individualizado e criterioso em todos os estágios do ciclo de vida do cliente. Esses recursos são sustentados por uma estrutura confiável de governança de dados, permitindo um controle aprimorado sobre onde e como os dados do parceiro são usados. Por exemplo, você pode querer usar os insights fornecidos pelo parceiro para segmentação, mas não para personalização.

Por exemplo, siga as etapas descritas neste caso de uso quando precisar enriquecer os registros do cliente com sinais demográficos e de intenção.

## Pré-requisitos e planejamento

Ao considerar suplementar seus perfis próprios com atributos de parceiros de dados, é recomendável discutir e abordar os seguintes detalhes sobre o ciclo de enriquecimento de dados com o parceiro de dados:

* Pense no local fora da Real-Time CDP para onde a lista de públicos-alvo será exportada com o intuito de ser compartilhada com o fornecedor de dados. Este local precisa ter suporte a exportação de arquivos.
* Quais são os identificadores esperados pelo fornecedor de dados para que seja possível criar camadas de atributos adicionais?
* Como o arquivo que contém os atributos fornecidos pelo parceiro será assimilado de volta na Real-Time CDP? Por exemplo, os arquivos podem ser assimilados por meio de conectores de origem de armazenamento na nuvem, como o [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) ou [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* Qual é a frequência com a qual é esperado que os atributos fornecidos pelo parceiro sejam trazidos de volta para a Real-Time CDP e atualizados?

>[!WARNING]
>
>Os atributos adicionais fornecidos pelo parceiro assimilados na Real-Time CDP afetam seu *volume de dados total*. Leia a [Descrição do Produto Real-Time Customer Data Platform](https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform.html?lang=pt-BR) para obter mais informações sobre o volume de dados total.

## Apresentação em vídeo {#video-walkthrough}

Assista ao tutorial em vídeo abaixo para obter uma apresentação de como complementar públicos-alvo primários com atributos fornecidos pelo parceiro:

>[!VIDEO](https://video.tv.adobe.com/v/3452458/?captions=por_br&learn=on)

## Como atingir o caso de uso: visão geral de alto nível {#achieve-the-use-case-high-level}

![Visão geral de alto nível visual do caso de uso enriquecimento de perfis com atributos fornecidos por parceiros.](/help/rtcdp/assets/partner-data/enrichment/enrichment-use-case-steps.png)

1. Como **cliente**, você licencia atributos de **parceiros de dados**.
2. Como **cliente**, você estende seus dados de perfil e o modelo de governança para acomodar atributos fornecidos por **parceiros**.
3. Como **cliente**, você integra os públicos-alvo que deseja enriquecer com o parceiro de dados. Geralmente, esses públicos-alvo são desconectados de identificadores de entrada, como elementos de Informações de identificação pessoal (PII), por exemplo, email, nome, endereço ou outros.
4. O **parceiro** anexa atributos licenciados nos perfis com os quais pode corresponder. De forma opcional, uma [ID do Parceiro](/help/identity-service/features/namespaces.md) pode ser incluída e assimilada no namespace da ID com escopo do parceiro.
5. Como **cliente**, você carrega os atributos do parceiro de dados nos perfis de cliente na Real-Time CDP.

## Como atingir o caso de uso: instruções passo a passo {#step-by-step-instructions}

Leia as seções abaixo, que incluem links para documentação adicional, para concluir cada uma das etapas da visão geral de alto nível acima.

### Atributos de licença do parceiro {#license-attributes-from-partner}

Esta etapa é abordada nos [pré-requisitos](#prerequisites-and-planning) e a Adobe pressupõe que você tenha os contratos certos em vigor, com fornecedores de dados confiáveis, para aprimorar seus perfis próprios.

### Estenda seus dados de perfil e modelo de governança para acomodar os atributos fornecidos por parceiros. {#extend-governance-model}

Neste ponto, você está estendendo sua estrutura de gerenciamento de dados na Real-Time CDP para acomodar os atributos fornecidos por parceiros.

Você tem a opção de criar um novo esquema da classe **[!UICONTROL XDM Individual Profile]** ou estender um esquema existente do mesmo tipo para incluir atributos fornecidos pelo parceiro. A Adobe recomenda criar um novo esquema com um novo conjunto de grupos de campos que melhor representem os atributos adicionais do fornecedor de dados. Isso garante que seus esquemas de dados estejam limpos e possam evoluir independentemente uns dos outros.

Para incluir atributos fornecidos por parceiros a um esquema, é possível criar um novo grupo de campos com os atributos esperados ou usar um dos grupos de campos pré-configurados fornecidos pela Adobe.

Leia as páginas da documentação abaixo para obter mais informações:

* [Noções básicas da composição de esquemas](/help/xdm/schema/composition.md)
* [Visão geral da classe [!UICONTROL XDM Individual Profile]](/help/xdm/classes/individual-profile.md)
* [Criar e editar esquemas na interface](/help/xdm/ui/resources/schemas.md)
* [Criar e editar grupos de campos de esquema na interface](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

Além disso, nesta etapa, pense em como seu modelo de governança de dados mudará à medida que você expande sua estratégia de gerenciamento de dados para incluir dados de terceiros fornecidos por parceiros. Explore as considerações nos links da documentação abaixo:

* (**Em breve**) Mantenha os dados de terceiros em um conjunto de dados separado para que seja fácil excluí-los e desfazer integrações.
* (**Em breve**) Use a funcionalidade [expiração do conjunto de dados](/help/hygiene/ui/dataset-expiration.md) no conjunto de dados para clientes que adquiriram o complemento de higiene de dados.
* (**Em breve**) Tenha cuidado ao criar conjuntos de dados derivados que extraem dados de terceiros, pois uma vez misturados, a única solução para remover os dados de terceiros é excluir todo o conjunto de dados derivado.

>[!TIP]
>
>Se você optar por complementar seus perfis de clientes com um identificador baseado em pessoas do fornecedor de dados, será possível criar um novo tipo de identidade do tipo **[[!UICONTROL Partner ID]](/help/identity-service/features/namespaces.md)**.
>
>Leia mais sobre a ID do parceiro na [seção de tipos de identidade](/help/identity-service/features/namespaces.md).
>Leia sobre [como definir campos de identidade](/help/xdm/ui/fields/identity.md) na interface da Experience Platform.

### Exporte os públicos-alvo que deseja enriquecer ao desconectar informações de identificação pessoal (PII) ou PII com hash {#export-audiences}

Exporte os públicos-alvo que deseja que o parceiro enriqueça. Use os destinos de armazenamento em nuvem fornecidos pela Real-Time CDP, como Amazon S3 ou SFTP. Leia as seguintes páginas de documentação para concluir esta etapa:

* Página da documentação do [destino Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md)
* Página da documentação do [destino SFTP](/help/destinations/catalog/cloud-storage/sftp.md)
* Como [conectar-se a um destino](/help/destinations/ui/connect-destination.md)
* Como [exportar dados para um destino de armazenamento na nuvem](/help/destinations/ui/activate-batch-profile-destinations.md)

### Seu parceiro de dados anexa atributos licenciados aos perfis com os quais ele consegue fazer correspondência {#partner-appends-attributes}

Nesta etapa, seu parceiro de dados anexa atributos licenciados para o público-alvo exportado. A saída geralmente está disponível como um arquivo simples que pode ser assimilado de volta na Real-Time CDP. Leia mais sobre [assimilação de arquivos na Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### A Real-Time CDP anexa atributos enriquecidos ao perfil de cliente {#ingest-data}

Agora é necessário assimilar os dados do parceiro por meio de um conector de origem para trazer os dados enriquecidos de volta para a Real-Time CDP e complementar seus perfis com dados fornecidos pelo parceiro.

Alguns conectores de origem recomendados para essa finalidade podem ser:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Limitações e solução de problemas {#limitations-and-troubleshooting}

Observe as seguintes limitações ao explorar o caso de uso descrito nesta página:

* Se optar por usar IDs do parceiro, saiba que essas IDs não são usadas ao criar o [gráfico de identidade](/help/identity-service/features/identity-graph-viewer.md).

## Outros casos de uso obtidos por meio da compatibilidade com dados de parceiros {#other-use-cases}

Conheça outros casos de uso habilitados por meio da compatibilidade com dados de parceiros na Real-Time CDP:

* Use o suporte a dados de terceiros da Real-Time CDP para [expandir sua base de perfis com perfis de clientes potenciais de parceiros de dados e interaja com eles para adquirir ou alcançar novos clientes](/help/rtcdp/partner-data/prospecting.md).
* [Personalize experiências no site para visitantes desconhecidos usando o reconhecimento de visitante auxiliado por parceiro](/help/rtcdp/partner-data/onsite-personalization.md) durante a visita sem que o usuário se autentique ou tenha um histórico anterior com sua marca.
* [Ativação ampliada de perfis de prospecto e públicos-alvo de prospecto](/help/destinations/ui/activate-prospect-audiences.md) para selecionar destinos.
