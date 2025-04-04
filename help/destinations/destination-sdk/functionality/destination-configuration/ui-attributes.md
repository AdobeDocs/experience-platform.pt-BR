---
description: Saiba como configurar os atributos da interface do usuário, como o link de documentação, a categoria do cartão de destino, o tipo de conexão e a frequência de destino, para destinos criados com o Destination SDK.
title: Atributos da interface
exl-id: aed8d868-c516-45da-b224-c7e99e4bfaf1
source-git-commit: fded2f25f76e396cd49702431fa40e8e4521ebf8
workflow-type: tm+mt
source-wordcount: '802'
ht-degree: 0%

---

# Atributos da interface

Os atributos da interface definem os elementos visuais que o Adobe deve exibir para o cartão de destino na interface do usuário do Adobe Experience Platform, como um logotipo, um link para a página de documentação, uma descrição do destino e sua categoria e tipo.

Para entender onde esse componente se encaixa em uma integração criada com o Destination SDK, consulte o diagrama na documentação das [opções de configuração](../configuration-options.md) ou consulte as seguintes páginas de visão geral da configuração de destino:

* [Usar o Destination SDK para configurar um destino de transmissão](../../guides/configure-destination-instructions.md#create-destination-configuration)
* [Usar o Destination SDK para configurar um destino baseado em arquivo](../../guides/configure-file-based-destination-instructions.md#create-destination-configuration)

Ao [criar um destino](../../authoring-api/destination-configuration/create-destination-configuration.md) por meio do Destination SDK, a seção `uiAttributes` define as seguintes propriedades visuais do cartão de destino:

* A URL da página da documentação de destino no [catálogo de destino](../../../catalog/overview.md).
* A categoria em que o destino estará visível na interface do usuário do Experience Platform.
* A frequência de exportação de dados para seu destino.
* O tipo de conexão de destino, como Amazon S3, Azure Blob etc.
* O URL no qual você hospedou o ícone a ser exibido no cartão do catálogo de destinos.

Você pode configurar atributos de interface do usuário por meio do ponto de extremidade `/authoring/destinations`. Consulte as seguintes páginas de referência de API para obter exemplos detalhados de chamadas de API, onde é possível configurar os componentes mostrados nesta página.

* [Criar uma configuração de destino](../../authoring-api/destination-configuration/create-destination-configuration.md)
* [Atualizar uma configuração de destino](../../authoring-api/destination-configuration/update-destination-configuration.md)

Este artigo descreve todos os atributos de interface do usuário compatíveis que você pode usar para o seu destino e mostra o que os clientes verão na interface do usuário do Experience Platform.

![Captura de tela da interface mostrando os atributos da interface na interface do Experience Platform](../../assets/functionality/destination-configuration/ui-attributes.png)

>[!IMPORTANT]
>
>Todos os nomes e valores de parâmetros com suporte do Destination SDK diferenciam maiúsculas de minúsculas **1}.** Para evitar erros de diferenciação entre maiúsculas e minúsculas, use os nomes e valores dos parâmetros exatamente como mostrado na documentação.

## Tipos de integração compatíveis {#supported-integration-types}

Consulte a tabela abaixo para obter detalhes sobre quais tipos de integrações suportam a funcionalidade descrita nesta página.

| Tipo de integração | Suporte à funcionalidade |
|---|---|
| Integrações em tempo real (streaming) | Sim |
| Integrações baseadas em arquivo (lote) | Sim |

## Parâmetros compatíveis {#supported-parameters}

```json
"uiAttributes":{
      "documentationLink":"http://www.adobe.com/go/YOURDESTINATION-en",
      "category":"cloudStorage",
      "connectionType":"S3",
      "frequency":"batch",
      "isBeta":"true"
   }
```

### `documentationLink` {#documentation-link}

`documentationLink` é um parâmetro de cadeia de caracteres que se refere à página da documentação no [Catálogo de Destinos](../../../catalog/overview.md) para o seu destino. Cada destino do produto no Adobe Experience Platform deve ter uma página de documentação correspondente. [Saiba como criar uma página de documentação de destino](../../docs-framework/documentation-instructions.md) para o seu destino. Observe que isso não é necessário para destinos privados/personalizados.

Use o seguinte formato: `http://www.adobe.com/go/destinations-YOURDESTINATION-en`, onde `YOURDESTINATION` é o nome do seu destino. Para um destino chamado Moviestar, você usaria `http://www.adobe.com/go/destinations-moviestar-en`.

Os usuários podem ver e visitar o link da documentação na página do catálogo de destinos na interface do. Eles precisam navegar até o cartão de destino e selecionar **[!UICONTROL Mais ações]** e **[!UICONTROL Exibir documentação]**, conforme mostrado na imagem abaixo.

![Imagem da interface do usuário mostrando o local do link da documentação.](../../assets/functionality/destination-configuration/ui-attributes-doc-link.png)

>[!NOTE]
>
>Esse link funciona somente depois que o Adobe define seu destino como ativo e a documentação é publicada.

### `category` {#category}

`category` é um parâmetro de cadeia de caracteres que se refere à categoria atribuída ao seu destino no Adobe Experience Platform. Para obter mais informações, leia [Categorias de Destino](../../../destination-types.md). Use um dos seguintes valores: `adobeSolutions, advertising, analytics, cdp, cloudStorage, crm, customerSuccess, database, dmp, ecommerce, email, emailMarketing, enrichment, livechat, marketingAutomation, mobile, personalization, protocols, social, streaming, subscriptions, surveys, tagManagers, voc, warehouses, payments`.

Os usuários podem ver a lista de categorias de destino no lado esquerdo da tela no catálogo de destino, como mostrado na imagem abaixo.

![Imagem da interface do usuário mostrando o local da categoria de destino.](../../assets/functionality/destination-configuration/ui-attributes-category.png)

### `connectionType` {#connection-type}

`connectionType` é um parâmetro de cadeia de caracteres que se refere ao tipo de conexão, dependendo do destino. Valores compatíveis: <ul><li>`Server-to-server`</li><li>`Cloud storage`</li><li>`Azure Blob`</li><li>`Azure Data Lake Storage`</li><li>`S3`</li><li>`SFTP`</li><li>`DLZ`</li></ul>

Os usuários podem ver o tipo de conexão de destino na guia [Procurar](../../../ui/destinations-workspace.md#browse) do espaço de trabalho de destinos.

![Imagem da interface do usuário mostrando o local do tipo de conexão na interface do usuário.](../../assets/functionality/destination-configuration/ui-attributes-connection.png)

### `frequency` {#frequency}

`frequency` é um parâmetro de cadeia de caracteres que se refere ao tipo de exportação de dados com suporte do seu destino. Defina como `Streaming` para integrações baseadas em API ou `Batch` ao exportar arquivos para seus destinos.

Os usuários podem ver o tipo de frequência nas **[!UICONTROL execuções de fluxo de dados]** página de cada conexão de destino.

![Imagem da interface do usuário mostrando o local do tipo de frequência na interface do usuário.](../../assets/functionality/destination-configuration/ui-attributes-frequency.png)

### `isBeta` {#isbeta}

Se o destino que você está criando com o Destination SDK estiver disponível para um número limitado de clientes, talvez você queira marcar o cartão de destino do catálogo de destino como beta.

Para fazer isso, você pode usar o parâmetro `isBeta: "true"` na seção de atributos da interface do usuário da configuração de destino para marcar o cartão de destino adequadamente.

![Imagem da interface do usuário mostrando um cartão de destino marcado como beta.](../../assets/functionality/destination-configuration/ui-attributes-isbeta.png)

### `icon` {#icon}

Você pode adicionar um ícone de logotipo ao seu destino, conforme mostrado na imagem abaixo.

![Imagem da interface do usuário mostrando o local do ícone.](../../assets/functionality/destination-configuration/ui-attributes-icon.png)

Para adicionar um logotipo ao cartão de destino, é necessário compartilhar a imagem desejada com a equipe do Adobe quando você [enviar o destino para revisão](../../guides/submit-destination.md#logo).

## Próximas etapas {#next-steps}

Depois de ler este artigo, você deve entender melhor quais atributos de interface do usuário você pode configurar para seu destino e onde os usuários os verão na interface do usuário do Experience Platform.

Para saber mais sobre os outros componentes de destino, consulte os seguintes artigos:

* [Autenticação do cliente](customer-authentication.md)
* [Autorização OAuth2](oauth2-authorization.md)
* [Campos de dados do cliente](customer-data-fields.md)
* [Configuração do esquema](schema-configuration.md)
* [Configuração do namespace de identidade](identity-namespace-configuration.md)
* [Entrega de destino](destination-delivery.md)
* [Configuração de metadados de público](audience-metadata-configuration.md)
* [Política de agregação](aggregation-policy.md)
* [Configuração em lote](batch-configuration.md)
* [Qualificações do perfil histórico](historical-profile-qualifications.md)
