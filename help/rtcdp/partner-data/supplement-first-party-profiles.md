---
title: (Beta) Complementar perfis primários com atributos fornecidos pelo parceiro
description: Saiba como complementar perfis primários com atributos de parceiros de dados confiáveis para melhorar sua base de dados, obter novos insights sobre sua base de clientes e melhorar a otimização do público-alvo.
hide: true
hidefromtoc: true
badgeBeta: label="Beta" type="informative" before-title="true"
source-git-commit: 019ebe0c1cf11a7fb30dced1e10b511bab9b5100
workflow-type: tm+mt
source-wordcount: '1082'
ht-degree: 0%

---

# Suplemente perfis próprios com atributos fornecidos pelo parceiro

>[!AVAILABILITY]
>
>* Essa funcionalidade beta está disponível para clientes que possuem Real-Time CDP (Serviço de aplicativo), Adobe Experience Platform Ativation, Real-time CDP, Real-Time CDP Prime, Real-Time CDP Ultimate licenciados. Leia mais sobre esses pacotes no [descrições do produto](https://helpx.adobe.com/legal/product-descriptions.html) e entre em contato com o representante da Adobe para obter mais informações.

Complemente perfis primários com atributos de parceiros de dados confiáveis para melhorar sua base de dados e obter novos insights sobre sua base de clientes e obter uma melhor otimização do público-alvo.

![Enriqueça os perfis com atributos fornecidos pelo parceiro usando a visão geral de alto nível do caso de uso.](/help/rtcdp/assets/partner-data/enrichment-use-case-overview.png)

## Pré-requisitos e planejamento {#prerequisites-and-planning}

Ao considerar complementar seus próprios perfis primários com atributos de parceiros de dados, você deve discutir e abordar os seguintes detalhes no loop de enriquecimento de dados com o parceiro de dados:

* Pense no local para onde a lista de públicos-alvo será exportada do Real-Time CDP para ser compartilhada com o fornecedor de dados. Este local precisa suportar a exportação de arquivos.
* Quais são os identificadores esperados pelo fornecedor de dados para que ele possa criar camadas de atributos adicionais?
* Como o arquivo que contém os atributos fornecidos pelo parceiro será assimilado de volta na Real-time CDP? Por exemplo, os arquivos podem ser assimilados por meio de conectores de origem de armazenamento na nuvem, como [Amazon S3](/help/sources/connectors/cloud-storage/s3.md) ou [SFTP](/help/sources/connectors/cloud-storage/sftp.md).
* Qual é a cadência com a qual você espera que os atributos fornecidos pelo parceiro sejam trazidos de volta para a Real-Time CDP e atualizados?

>[!WARNING]
>
>Os atributos adicionais fornecidos pelo parceiro assimilados na Real-Time CDP afetam seus *riqueza média do perfil*. Leia o [Descrição do produto Real-time Customer Data Platform](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html) para obter mais informações sobre a riqueza do perfil.

## Como obter o caso de uso: visão geral de alto nível {#achieve-the-use-case-high-level}

![Enriqueça os perfis com atributos fornecidos pelo parceiro usando a visão geral de alto nível do caso de uso.](/help/rtcdp/assets/partner-data/enrichment-use-case-steps.png)

1. Como um **cliente**, os atributos de licença do **parceiro de dados**.
2. Como um **cliente**, você pode estender os dados do seu perfil e o modelo de governança para acomodar **parceiro** atributos fornecidos pelo.
3. Como um **cliente**, você integra os públicos que deseja enriquecer com o parceiro de dados. Geralmente, esses públicos-alvo são destacados por identificadores de entrada como elementos de Informações de identificação pessoal (PII), como email, nome, endereço ou outros.
4. A variável **parceiro** anexa atributos licenciados para os perfis que podem ser correspondidos. Opcionalmente, um [ID do Parceiro](/help/identity-service/namespaces.md) podem ser incluídos e assimilados no namespace da ID com escopo de parceiro.
5. Como um **cliente**, você carrega atributos do parceiro de dados nos perfis do cliente na Real-Time CDP.

## Como obter o caso de uso: instruções passo a passo {#step-by-step-instructions}

Leia as seções abaixo, que incluem links para documentação adicional, para concluir cada uma das etapas da visão geral de alto nível acima.

### Atributos de licença do parceiro {#license-attributes-from-partner}

Esta etapa é abordada na seção [pré-requisitos](#prerequisites-and-planning) O e o Adobe pressupõe que você tenha os contratos certos em vigor com fornecedores de dados confiáveis para aumentar seus perfis primários.

### Estenda seus dados de perfil e o modelo de governança para acomodar os atributos fornecidos pelo parceiro. {#extend-governance-model}

Neste ponto, você está estendendo sua estrutura de gerenciamento de dados no Real-Time CDP para acomodar os atributos fornecidos pelo parceiro.

Você tem a opção de criar um novo schema do **[!UICONTROL Perfil individual XDM]** ou estenda um esquema existente do mesmo tipo para incluir atributos fornecidos pelo parceiro. A Adobe recomenda que você crie um novo esquema com um novo conjunto de grupos de campos que melhor representem os atributos adicionais do fornecedor de dados. Isso garante que seus esquemas de dados estejam limpos e possam evoluir independentemente uns dos outros.

Para incluir atributos fornecidos pelo parceiro em um esquema, você pode criar um novo grupo de campos com os atributos esperados ou usar um dos grupos de campos pré-configurados fornecidos pelo Adobe.

Leia as páginas de documentação abaixo para obter mais informações:

* [Noções básicas da composição do esquema](/help/xdm/schema/composition.md)
* [Visão geral do [!UICONTROL Perfil individual XDM] classe](/help/xdm/classes/individual-profile.md)
* [Criar e editar esquemas na interface](/help/xdm/ui/resources/schemas.md)
* [Criar e editar grupos de campos de esquema na interface](/help/xdm/ui/resources/field-groups.md)

<!--

Commenting out links for now
* [Create and edit schemas using the API](/help/xdm/api/schemas.md#create)
* [Update an existing schema to add field groups using the API](/help/xdm/api/schemas.md#patch)
* Link to new field group documentation page when it exists

-->

Além disso, nesta etapa, pense em como seu modelo de governança de dados muda à medida que você expande sua estratégia de gerenciamento de dados para incluir dados de terceiros fornecidos pelo parceiro. Explore as considerações nos links de documentação abaixo:

* (**Em breve**) Mantenha os dados de terceiros em um conjunto de dados separado para que seja fácil excluí-los e desfazer integrações.
* (**Em breve**) Use o [expiração do conjunto de dados](/help/hygiene/ui/dataset-expiration.md) no conjunto de dados para clientes que compraram o complemento de higiene de dados.
* (**Em breve**) Tenha cuidado ao criar conjuntos de dados derivados que extraem dados de terceiros, pois uma vez misturados, a única solução para remover os dados de terceiros é excluir todo o conjunto de dados derivado.

>[!TIP]
>
>Se você optar por complementar os perfis do cliente com um identificador com base em pessoas do fornecedor de dados, será possível criar um novo tipo de identidade do tipo **[[!UICONTROL ID do Parceiro]](/help/identity-service/namespaces.md)**.
>
>Leia mais sobre a ID de parceiro na [seção de tipos de identidade](/help/identity-service/namespaces.md).
>Ler sobre [como definir campos de identidade](/help/xdm/ui/fields/identity.md) na interface do usuário do Experience Platform.

### Exportar públicos que você deseja que sejam enriquecidos ao serem digitados em Informações pessoais identificáveis (PII) ou PII com hash {#export-audiences}

Exporte os públicos que você deseja que o parceiro enriqueça. Use os destinos de armazenamento em nuvem fornecidos pela Real-time CDP, como Amazon S3 ou SFTP. Leia as seguintes páginas de documentação para concluir esta etapa:

* [Destino do Amazon S3](/help/destinations/catalog/cloud-storage/amazon-s3.md) página da documentação
* [Destino SFTP](/help/destinations/catalog/cloud-storage/sftp.md) página da documentação
* Como [conectar-se a um destino](/help/destinations/ui/connect-destination.md)
* Como [exportar dados para um destino de armazenamento na nuvem](/help/destinations/ui/activate-batch-profile-destinations.md)

### Seu parceiro de dados anexa atributos licenciados aos perfis com os quais ele pode fazer correspondência {#partner-appends-attributes}

Nesta etapa, seu parceiro de dados anexa atributos licenciados para o público-alvo exportado. A saída geralmente está disponível como um arquivo simples que pode ser assimilado de volta no Real-Time CDP. Leia mais sobre [assimilação de arquivos no Real-Time CDP](/help/ingestion/tutorials/ingest-batch-data.md#upload-file).

### O Real-Time CDP anexa atributos enriquecidos ao perfil do cliente {#ingest-data}

Agora é necessário assimilar dados do parceiro por meio de um conector de origem para trazer os dados enriquecidos de volta para o Real-Time CDP e complementar seus perfis com dados fornecidos pelo parceiro.

Alguns conectores de origem recomendados para essa finalidade podem ser:

* [Amazon S3](/help/sources/connectors/cloud-storage/s3.md)
* [SFTP](/help/sources/connectors/cloud-storage/sftp.md)

## Limitações e solução de problemas {#limitations-and-troubleshooting}

Observe as seguintes limitações ao explorar o caso de uso descrito nesta página:

* Se você optar por usar IDs de parceiro, saiba que essas IDs não são usadas ao criar o [gráfico de identidade](/help/identity-service/ui/identity-graph-viewer.md).

## Outros casos de uso obtidos por meio do suporte a dados de parceiros {#other-use-cases}

Explore outros casos de uso ativados por meio do suporte a dados de parceiros no Real-Time CDP:

* (**Em breve**) [!BADGE Beta]{type=Informative}**Aproveitar o reconhecimento auxiliado pelo parceiro** para personalizar experiências no site durante a visita e para redirecionamento fora do site após a visita, sem a autenticação do usuário ou um histórico anterior com sua marca.
* (**Em breve**) [!BADGE Beta]{type=Informative}**Ativação expandida** uso de IDs de parceiros para publicar ecossistemas que não aceitam PII ou PII com hash.