---
keywords: RTCDP; CDP; B2B Edition; Real-time Customer Data Platform; plataforma de dados do cliente em tempo real; cdp em tempo real; b2b; cdp
solution: Experience Platform
title: Introdução ao Real-time Customer Data Platform B2B Edition
description: Use esse cenário de exemplo ao configurar sua implementação do Real-time Customer Data Platform B2B Edition.
exl-id: ad9ace46-9915-4b8f-913a-42e735859edf
source-git-commit: eb71896ec049253266685fdc831f941e14f3268a
workflow-type: tm+mt
source-wordcount: '1205'
ht-degree: 0%

---

# Introdução ao Real-time Customer Data Platform B2B Edition

Este documento fornece um fluxo de trabalho completo de alto nível para começar a usar o Real-time Customer Data Platform (CDP) B2B Edition, usando um exemplo de caso de uso para ilustrar os principais conceitos.

A empresa de tecnologia Bodea quer combinar dados de pessoas e contas de diferentes fontes de dados siloados para efetivamente direcionar os clientes com um e-mail e uma campanha publicitária da LinkedIn para seu novo produto. O Bodea usa o Marketo Engage como sua plataforma de automação de marketing e precisa segmentar um público específico de B2B de vários CRMs que contêm dados de clientes.

## Introdução

Este fluxo de trabalho tutorial depende de vários serviços da Adobe Experience Platform como parte da demonstração. Se você quiser seguir em frente, é recomendável ter uma boa compreensão dos seguintes serviços:

- [Experience Data Modal (XDM)](../xdm/home.md)
- [Fontes](../sources/home.md)
- [Segmentação](../segmentation/home.md)
- [Destinos](../destinations/home.md)

## Criar esquemas para seus dados

Como parte da configuração inicial, o departamento de TI da Bodea precisa criar um esquema XDM para garantir que seus dados sigam um formato padrão ao serem trazidos para a Platform e sejam acionáveis em diferentes serviços da plataforma e produtos da Adobe Experience Cloud (como Adobe Analytics e Adobe Target).

>[!WARNING]
>
>Você deve seguir os padrões de ingestão conforme descrito na documentação de fontes relevantes vinculada a este tutorial. Não há garantias de que outros métodos de mapeamento de campo funcionem.

O Adobe Experience Platform permite gerar automaticamente os esquemas e namespaces necessários para fontes de dados B2B. Essa ferramenta garante que os esquemas criados descrevam os dados de forma estruturada e reutilizável. Siga as [Documentação do utilitário de geração automática de namespaces B2B e de esquema](../sources/connectors/adobe-applications/marketo/marketo-namespaces.md) para obter uma referência completa ao processo de configuração.

Na interface do usuário do Adobe Experience Platform, o profissional de marketing do Bodea seleciona **[!UICONTROL Esquemas]** no painel à esquerda, seguido pela variável **[!UICONTROL Procurar]** guia . Como eles usaram o utilitário de geração automática do Marketo Engage, os novos esquemas vazios aparecem na lista e todos têm um prefixo &quot;B2B&quot;.

![Guia de navegação do schema workspace](./assets/b2b-tutorial/empty-b2b-schemas.png)

O utilitário de geração automática definiu a estrutura do modelo de dados para os esquemas usando classes XDM B2B padrão (como [Conta Comercial XDM](../xdm/classes/b2b/business-account.md) e [Oportunidade de negócios XDM](../xdm/classes/b2b/business-opportunity.md)) que capturam entidades de dados B2B fundamentais. Além disso, os esquemas B2B gerados automaticamente com base nessas classes têm relacionamentos preestabelecidos que permitem casos de uso de segmentação avançada. Todos os grupos de campos adicionais necessários para a estrutura de dados podem ser facilmente feitos aqui por meio da interface do usuário. Consulte a [Guia da interface do usuário do XDM, adição de grupos de campos a uma seção de esquema](../xdm/ui/resources/schemas.md#add-field-groups) para obter mais informações.

>[!NOTE]
> 
>Se você não estiver usando o utilitário autogerador ou se for necessário criar um novo relacionamento, consulte o tutorial em [criação de relações entre esquemas B2B](../xdm/tutorials/relationship-b2b.md).

O Perfil do cliente em tempo real mescla dados de fontes diferentes para criar perfis consolidados de entidades B2B importantes. Como os perfis são gerados com base em uma única classe, o utilitário de geração automática configura os relacionamentos entre schemas com base em casos de uso comerciais comuns. Como resultado, a equipe do Bodea agora está pronta para assimilar dados com base em seus esquemas B2B.

>[!NOTE]
> 
>Os namespaces de identidade padrão, as chaves primárias e os relacionamentos criados para os esquemas pelo utilitário de geração automática são facilmente descobertos na área de trabalho Esquema.
>
>![exibição da interface do usuário do esquema padrão e do relacionamento](./assets/b2b-tutorial/schema-identity-relationship.png)

## Assimilar os dados no Experience Platform

Em seguida, o profissional de marketing do Bodea usa a variável [conector Marketo Engage](../sources/connectors/adobe-applications/marketo/marketo.md) para assimilar dados na Platform para uso em serviços downstream. Você também pode assimilar dados usando uma das fontes aprovadas para a CDP B2B Edition em tempo real.

>[!NOTE]
> 
>Para saber quais conectores de origem estão disponíveis para sua organização, você pode exibir o catálogo de fontes na interface do usuário da plataforma. Para acessar o catálogo, selecione **Fontes** na navegação à esquerda, selecione **Catálogo**.

Para criar uma conexão entre uma conta da Marketo e a Plataforma, você deve adquirir credenciais de autenticação. Consulte a [guia sobre como obter credenciais de autenticação do conector de origem do Marketo](../sources/connectors/adobe-applications/marketo/marketo-auth.md) para obter instruções detalhadas.

Depois de adquirir credenciais de autenticação, o profissional de marketing do Bodea cria uma conexão entre a conta da Marketo e a organização IMS da plataforma. Consulte a documentação para obter instruções sobre [como conectar uma conta do Marketo usando a interface do usuário da plataforma](../sources/tutorials/ui/create/adobe-applications/marketo.md).

O conector de origem do Marketo Engage fornece um recurso de mapeamento automático para facilitar muito o processo de mapeamento de todos os campos de dados para os esquemas recém-criados.

>[!NOTE]
> 
>Se você tiver feito grupos de campos personalizados em seus esquemas XDM, poderá ter campos desconectados nessa etapa do processo. Certifique-se de verificar todos os valores que estão preenchendo seus grupos de campos personalizados.

O profissional de marketing do Bodea verifica se todos os grupos de campos estão mapeados adequadamente e continua o processo de configuração de fontes inicializando um fluxo de dados. Ao criar um fluxo de dados para trazer os dados do Marketo, os dados recebidos podem ser usados pelos serviços downstream da plataforma. Durante o processo de ingestão inicial, os dados são trazidos para o Experience Platform como um lote. Depois disso, os dados assimilados subsequentes serão transmitidos no Perfil com atualizações quase em tempo real.

## Criar um segmento para avaliar seus dados

A próxima tarefa é criar um público-alvo para a nova campanha de marketing por email do Bodea com base em atributos específicos de entidades relacionadas na fonte de dados. Na interface do usuário da plataforma, o profissional de marketing do Bodea seleciona primeiro **[!UICONTROL Segmentos]** na navegação à esquerda, em seguida **[!UICONTROL Criar segmento]**.

Neste exemplo, o segmento encontra todas as pessoas que trabalham no departamento de vendas e estão relacionadas a qualquer conta que tenha pelo menos uma oportunidade aberta. Esse segmento requer um link entre a classe Perfil individual XDM, a classe Conta comercial XDM e a classe Oportunidade comercial XDM.

![Segmento de caso de uso](./assets/b2b-tutorial/use-case-segment.png)

>[!NOTE]
> 
>Para obter instruções sobre como criar segmentos para avaliar seus dados, consulte o [Guia da interface do usuário do Construtor de segmentos](../segmentation/ui/segment-builder.md). Para casos de uso de segmentação B2B mais específicos, consulte [visão geral da segmentação para a CDP B2B em tempo real](./segmentation/b2b.md).

O Construtor de segmentos permite que você crie um público-alvo comercializável a partir dos dados do Perfil do cliente em tempo real e visualize estimativas do seu público-alvo potencial com base na combinação de atributos, eventos e públicos-alvo existentes que você definiu.

## Ativar os dados avaliados para um destino

Depois que o segmento é criado com êxito, um resumo é fornecido no [!UICONTROL Detalhes] da área de trabalho. Como nenhum destino está ativado no momento para o segmento, o profissional de marketing do Bodea precisa exportar o público para um conjunto de dados, onde ele pode ser acessado e tratado.

No [!UICONTROL Segmentos] espaço de trabalho da interface do usuário da plataforma, o profissional de marketing do Bodea seleciona **[!UICONTROL Ativar para destino]**.

![Ativar o segmento para um destino](./assets/b2b-tutorial/activate-to-destination.png)

>[!NOTE]
> 
>Veja o tutorial em [ativação de um segmento para um destino](https://experienceleague.adobe.com/docs/marketo/using/product-docs/core-marketo-concepts/smart-lists-and-static-lists/static-lists/push-an-adobe-experience-cloud-segment-to-a-marketo-static-list.html) para obter etapas abrangentes sobre como fazer isso.

O profissional de marketing do Bodea ativa o segmento para o destino do Marketo, o que permite que ele envie dados de segmento da Plataforma para o Marketo Engage, na forma de uma lista estática. Consulte o guia sobre [Destino do Marketo](https://experienceleague.adobe.com/docs/experience-platform/destinations/catalog/adobe/marketo-engage.html) para obter mais informações.

## Próximas etapas

Ao seguir este tutorial, você aproveitou com sucesso os vários serviços da Adobe Experience Platform usados pela CDP B2B Edition em tempo real. Como resultado, você aprendeu a assimilar, segmentar, avaliar e exportar seus dados B2B como públicos acionáveis que podem ser envolvidos em diferentes canais.
