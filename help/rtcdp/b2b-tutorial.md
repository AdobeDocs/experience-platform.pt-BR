---
keywords: RTCDP;CDP;B2B Edition;Real-time Customer Data Platform;real time customer data platform;real time cdp;b2b;cdp
solution: Experience Platform
title: Introdução à Real-time Customer Data Platform B2B Edition
description: Use esse cenário como exemplo ao configurar sua implementação do Adobe Real-time Customer Data Platform B2B Edition.
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '1206'
ht-degree: 0%

---

# Introdução à Real-time Customer Data Platform B2B Edition

Este documento fornece um fluxo de trabalho completo de alto nível para a introdução ao Real-time Customer Data Platform (CDP) B2B Edition, usando um exemplo de caso de uso para ilustrar os principais conceitos.

A empresa de tecnologia Bodea quer combinar dados pessoais e de conta de diferentes fontes de dados em silos para direcionar os clientes com eficiência a uma campanha de anúncio por email e LinkedIn para seu novo produto. A Bodea usa o Marketo Engage como sua plataforma de automação de marketing e precisa segmentar um público específico de B2B de vários CRMs que contêm dados de clientes.

## Introdução

Este fluxo de trabalho tutorial depende de vários serviços da Adobe Experience Platform como parte da demonstração. Se desejar acompanhar, é recomendável compreender bem os seguintes serviços:

- [Modal de dados de experiência (XDM)](../xdm/home.md)
- [Fontes](../sources/home.md)
- [Segmentação](../segmentation/home.md)
- [Destinos](../destinations/home.md)

## Criar esquemas para seus dados

Como parte da configuração inicial, o departamento de TI da Bodea precisa criar um esquema XDM para garantir que seus dados sigam um formato padrão ao serem trazidos para a Platform e sejam acionáveis em diferentes serviços da Platform e produtos da Adobe Experience Cloud (como Adobe Analytics e Adobe Target).

>[!WARNING]
>
>Você deve seguir os padrões de assimilação conforme descrito na documentação de fontes relevantes vinculada a este tutorial. Não há garantias de que outros métodos de mapeamento de campo funcionarão.

O Adobe Experience Platform permite gerar automaticamente os esquemas e namespaces necessários para fontes de dados B2B. Essa ferramenta garante que os esquemas criados descrevam os dados de forma estruturada e reutilizável. Siga as [Documentação do utilitário de geração automática de esquemas e namespaces B2B](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) para obter uma referência completa ao processo de configuração.

Na interface do Adobe Experience Platform, o profissional de marketing do Bodea seleciona **[!UICONTROL Esquemas]** no painel esquerdo, seguido pelo botão **[!UICONTROL Procurar]** guia. Como eles usaram o utilitário de geração automática Marketo Engage, os novos esquemas vazios aparecem na lista e todos têm o prefixo &quot;B2B&quot;.

![Guia Procurar no espaço de trabalho de esquema](./assets/b2b-tutorial/empty-b2b-schemas.png)

O utilitário de geração automática definiu a estrutura do modelo de dados para os esquemas usando classes B2B XDM padrão (como [Conta de negócios XDM](../xdm/classes/b2b/business-account.md) e [Oportunidade de negócios XDM](../xdm/classes/b2b/business-opportunity.md)) que capturam entidades de dados B2B fundamentais. Além disso, os esquemas B2B gerados automaticamente baseados nessas classes têm relações preestabelecidas que permitem casos de uso de segmentação avançada. Quaisquer grupos de campos adicionais necessários para a estrutura de dados podem ser facilmente feitos aqui por meio da interface do usuário. Consulte a [Guia da interface do XDM, adicionando grupos de campos a uma seção de esquema](../xdm/ui/resources/schemas.md#add-field-groups) para obter mais informações.

>[!NOTE]
> 
>Se você não estiver usando o utilitário gerador automático ou se uma nova relação precisar ser criada, consulte o tutorial em [criação de relacionamentos entre esquemas B2B](../xdm/tutorials/relationship-b2b.md).

O Perfil do cliente em tempo real mescla dados de fontes diferentes para criar perfis consolidados das principais entidades B2B. Como os perfis são gerados com base em uma única classe, o utilitário de geração automática configura os relacionamentos entre esquemas com base em casos de uso de negócios comuns. Como resultado, a equipe do Bodea agora está pronta para assimilar dados com base em seus schemas B2B.

>[!NOTE]
> 
>Os namespaces de identidade padrão, as chaves primárias e as relações criadas para os esquemas pelo utilitário de geração automática são facilmente detectáveis no espaço de trabalho Esquema.
>
>![exibição da identidade do esquema padrão e da interface do usuário do relacionamento](./assets/b2b-tutorial/schema-identity-relationship.png)

## Assimilar seus dados no Experience Platform

Em seguida, o profissional de marketing Bodea usa o [conector Marketo Engage](../sources/connectors/adobe-applications/marketo/marketo.md) para assimilar dados na Platform para uso em serviços downstream. Você também pode assimilar dados usando uma das fontes aprovadas para o Real-Time CDP B2B Edition.

>[!NOTE]
> 
>Para saber quais conectores de origem estão disponíveis para sua organização, é possível visualizar o catálogo de origens na interface do usuário da Platform. Para acessar o catálogo, selecione **Origens** na navegação à esquerda, selecione **Catálogo**.

Para criar uma conexão entre uma conta do Marketo e a Platform, você deve adquirir credenciais de autenticação. Consulte a [guia sobre como obter credenciais de autenticação do conector de origem do Marketo](../sources/connectors/adobe-applications/marketo/marketo-auth.md) para obter instruções detalhadas.

Depois de adquirir credenciais de autenticação, o profissional de marketing Bodea cria uma conexão entre a conta do Marketo e sua organização do Platform IMS. Consulte a documentação para obter instruções sobre [como conectar uma conta do Marketo usando a interface do usuário da plataforma](../sources/tutorials/ui/create/adobe-applications/marketo.md).

O conector de origem do Marketo Engage fornece um recurso de mapeamento automático para facilitar muito o processo de mapeamento de todos os campos de dados para os esquemas recém-criados.

>[!NOTE]
> 
>Se você tiver feito grupos de campos personalizados em seus esquemas XDM, talvez tenha campos desconectados nesta fase do processo. Verifique todos os valores que estão preenchendo seus grupos de campos personalizados.

O profissional de marketing do Bodea verifica se todos os grupos de campos estão mapeados corretamente e continua o processo de configuração das fontes inicializando um fluxo de dados. Ao criar um fluxo de dados para trazer os dados do Marketo, os dados recebidos podem ser usados pelos serviços downstream da plataforma. Durante o processo inicial de assimilação, os dados são trazidos para o Experience Platform como um lote. Depois disso, os dados assimilados subsequentes são transmitidos ao Perfil com atualizações quase em tempo real.

## Criar um segmento para avaliar seus dados

A próxima tarefa é criar um público-alvo para a nova campanha de marketing por email do Bodea com base em atributos específicos de entidades relacionadas nos dados de origem. Na interface do Platform, o profissional de marketing do Bodea seleciona primeiro **[!UICONTROL Segmentos]** na navegação à esquerda, **[!UICONTROL Criar segmento]**.

Neste exemplo, o segmento encontra todas as pessoas que trabalham no departamento de vendas e estão relacionadas a qualquer conta que tenha pelo menos uma oportunidade aberta. Este segmento requer um link entre a classe Perfil individual XDM, a classe Conta de negócios XDM e a classe Oportunidade de negócios XDM.

![Segmento de caso de uso](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Para obter instruções sobre como criar segmentos para avaliar seus dados, consulte a [Guia da interface do usuário do Construtor de segmentos](../segmentation/ui/segment-builder.md). Para casos de uso mais específicos de segmentação B2B, consulte o [visão geral da segmentação para o Real-Time CDP B2B Edition](./segmentation/b2b.md).

O Construtor de segmentos permite criar um público-alvo comercializável a partir dos dados do Perfil do cliente em tempo real e exibir estimativas de seu público-alvo potencial com base na combinação de atributos, eventos e públicos-alvo existentes definidos.

## Ativar os dados avaliados para um destino

Depois que o segmento é criado com sucesso, um resumo é fornecido na [!UICONTROL Detalhes] seção do espaço de trabalho. Como nenhum destino está ativado no momento para o segmento, o profissional de marketing Bodea precisa exportar o público-alvo para um conjunto de dados em que ele possa ser acessado e reagido.

No prazo de [!UICONTROL Segmentos] da interface do usuário da Platform, o profissional de marketing do Bodea seleciona **[!UICONTROL Ativar para destino]**.

![Ativar o segmento para um destino](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Veja o tutorial sobre [ativar um segmento para um destino](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) para obter etapas abrangentes sobre como fazer isso.

O profissional de marketing do Bodea ativa o segmento para o destino do Marketo, o que permite que ele envie dados de segmento da Platform para o Marketo Engage no formato de uma lista estática. Consulte o guia no [Destino do Marketo](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) para obter mais informações.

## Próximas etapas

Ao seguir este tutorial, você aproveitou com êxito os vários serviços da Adobe Experience Platform usados pelo Real-Time CDP B2B Edition. Como resultado, você aprendeu a assimilar, segmentar, avaliar e exportar seus dados B2B como públicos acionáveis que podem ser envolvidos em diferentes canais.
