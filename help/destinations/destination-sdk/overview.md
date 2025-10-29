---
description: O Adobe Experience Platform Destination SDK é um conjunto de APIs de configuração que permitem configurar padrões de integração de destino para que o Experience Platform forneça dados de público-alvo e perfil para seu endpoint ou local de armazenamento, com base nos formatos de dados e autenticação de sua escolha. As configurações são armazenadas no Experience Platform e podem ser recuperadas por meio da API para atualizações adicionais.
title: Adobe Experience Platform Destination SDK
exl-id: 7aca9f40-98c8-47c2-ba88-4308fc2b1798
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '1012'
ht-degree: 0%

---

# Adobe Experience Platform Destination SDK

O Adobe Experience Platform Destination SDK é um conjunto de APIs de configuração que permitem configurar padrões de integração de destino para que o Experience Platform forneça dados de público-alvo e perfil para seu endpoint ou local de armazenamento, com base nos formatos de dados e autenticação de sua escolha. As configurações são armazenadas no Experience Platform e podem ser recuperadas por meio da API para atualizações adicionais.

A documentação do Destination SDK fornece instruções para que você use o Adobe Experience Platform Destination SDK para configurar, testar e lançar uma integração de destino produzida com o Adobe Experience Platform, e fazer com que seu destino se torne parte do catálogo de destinos em constante crescimento. Ao usar o Destination SDK, você também pode criar seu próprio destino privado personalizado para exportar dados personalizados de acordo com suas necessidades.

![Captura de tela da interface do Experience Platform, mostrando o catálogo de destinos.](assets/destinations-catalog-overview.png)

## Início rápido - explore as informações essenciais {#quick-start}

Revise a documentação nos links abaixo para começar rapidamente a configurar e enviar seu destino pelo Destination SDK.

>[!BEGINSHADEBOX]

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Páginas de configuração</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/functionality/configuration-options.md">Todas as opções de configuração explicadas</a></li>
                <li> Configuração do servidor de destino - <a href="/help/destinations/destination-sdk/functionality/destination-server/server-specs.md">especificações do servidor</a> e <a href="/help/destinations/destination-sdk/functionality/destination-server/templating-specs.md">especificações do modelo</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/customer-data-fields.md">Campos de dados do cliente e outros componentes de configuração de destino</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Modelos e macros</a></li>
            </ul>
        </td>
        <td>
            <p><b>Guias</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/overview.md#process">Processo de integração de alto nível</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Configurar um destino de transmissão</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Configurar um destino baseado em arquivo</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-prospect-audience-destination.md">Configurar um destino para exportar perfis de clientes potenciais</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/submit-destination.md">Enviar destino para publicação</a></li>
            </ul>
        </td>
                <td>
            <p><b>Referências de API</b></p>
            <ul>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-servers-and-templates">Referência da API do ponto de extremidade do servidor de destino</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-configurations">Referência de API do ponto de extremidade de destino</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Audience-metadata-templates">Referência da API de metadados de público</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-testing">Referência da API de teste</a></li>
                <li><a href="https://developer.adobe.com/experience-platform-apis/references/destination-authoring/#tag/Destination-publishing">Referência da API de publicação de destino</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>

<table style="border: 0;">
  <tbody>
    <tr>
        <td>
            <p><b>Configurar um destino de transmissão - folha de características</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-destination-instructions.md">Configurar um guia completo do destino de transmissão</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-server/message-format.md">Entender a transformação de dados por meio de modelos Pebble</a> e <a href="/help/destinations/destination-sdk/functionality/destination-server/supported-functions.md">exibir funções de modelo com suporte</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/aggregation-policy.md">Entender as políticas de agregação de dados</a></li>
                <li><a href="https://experienceleague.adobe.com/en/docs/experience-platform/destinations/destination-sdk/functionality/destination-server/message-format">Exemplo de configuração em tempo real</a></li>
                <li><a href="/help/destinations/destination-sdk/testing-api/streaming-destinations/streaming-destination-testing-overview.md">Testar o destino de streaming</a></li>
            </ul>
        </td>
        <td>
            <p><b>Configurar um destino baseado em arquivo — gabarito</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/guides/configure-file-based-destination-instructions.md">Configurar um guia completo do destino baseado em arquivos</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-file-formatting-options.md">Configurar formatos de arquivo para os arquivos exportados</a></li>
                <li><a href="/help/destinations/destination-sdk/guides/batch/configure-amazon-s3-destination-with-predefined-file-formatting.md">Exemplo de configuração em tempo real para um destino do Amazon S3</a></li>
                <li><a href="/help/destinations/destination-sdk/functionality/destination-configuration/batch-configuration.md">Configuração em lote</a> para agendamento de exportação de arquivo e nomenclatura de arquivo</li>
                <li><a href="/help/destinations/destination-sdk/testing-api/batch-destinations/file-based-destination-testing-overview.md">Testar seu destino baseado em arquivo</a></li>
            </ul>
        </td>
        <td>
            <p><b>Outras informações essenciais</b></p>
            <ul>
                <li><a href="/help/destinations/destination-sdk/getting-started.md#obtain-authentication-credentials">Obter as credenciais de autenticação necessárias para usar a API</a></li>
                <li><a href="/help/destinations/destination-sdk/integration-prerequisites.md">Pré-requisitos de integração</a></li>
                <li><a href="/help/destinations/destination-sdk/glossary.md">Glossário de termos do Destination SDK</a></li>                
                <li><a href="/help/destinations/destination-sdk/functionality/rate-limiting-retry-policy.md">Limites de taxa e política de nova tentativa</a></li>
                <li><a href="/help/destinations/destination-sdk/docs-framework/self-service-template.md">Modelo de autoatendimento para documentar seu destino</a></li>
            </ul>
        </td>
    </tr>
  </tbody>
</table>


>[!ENDSHADEBOX]

## Integrações produzidas e personalizadas {#productized-custom-integrations}

>[!IMPORTANT]
>
> Esta funcionalidade para criar destinos personalizados privados está disponível somente para clientes do [Adobe Real-Time Customer Data Platform Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=pt-BR).

Como parceiro da Destination SDK, você pode se beneficiar adicionando seu destino de produção ao [catálogo do Experience Platform](../catalog/overview.md):

1. Padronize as configurações de integração entre clientes com parâmetros pré-configurados e simplifique a experiência de configuração para os clientes.
2. Apresente um cartão de destino de marca no catálogo de destinos do Experience Platform para simplificar a configuração e o reconhecimento do cliente.
3. Seja apresentado como uma integração de destino produtivo com o Adobe Experience Platform e o Adobe Real-Time Customer Data Platform.

Como cliente do Experience Platform, você também pode criar seu próprio destino personalizado privado, que pode atender melhor às suas necessidades de ativação.

![Diagrama de visão geral que mostra como os desenvolvedores de destino interagem com o Destination SDK e como os clientes do Real-Time CDP se beneficiam de destinos produzidos e privados.](assets/destination-sdk-visual.png)

## Tipos de integração compatíveis {#supported-integration-types}

### Integrações em tempo real (streaming) {#real-time-integrations}

Por meio do Destination SDK, o Adobe Experience Platform oferece suporte a integrações em tempo real (também chamadas de transmissão) com destinos que têm um endpoint da REST API. A integração em tempo real com o Experience Platform oferece suporte a recursos como:

* Transformação e agregação de mensagens
* Preenchimento retroativo de perfil
* Integração de metadados configurável para inicializar a configuração do público e a transferência de dados
* Autenticação configurável
* Um conjunto de APIs de teste e validação para você testar e iterar as configurações de destino

### Integrações baseadas em arquivo {#file-based-integrations}

Por meio do Destination SDK, você também pode configurar integrações para exportar arquivos periodicamente para o local de armazenamento de sua escolha. A integração baseada em arquivos com o Experience Platform oferece suporte a recursos como:

* Exportação de arquivos em vários formatos compatíveis (CSV, Parquet, JSON)
* Opções configuráveis de formatação de arquivo, que permitem estruturar o formato dos arquivos exportados para atender aos requisitos de downstream.

Leia sobre os requisitos técnicos no lado dos destinos no artigo [pré-requisitos de integração](integration-prerequisites.md) e leia sobre todas as configurações compatíveis no artigo [opções de configuração](functionality/configuration-options.md)

## Obter acesso ao Destination SDK {#get-access}

O acesso à Destination SDK varia de acordo com seu status como parceiro ou cliente da Experience Platform e da Real-Time CDP. Consulte a tabela abaixo para obter mais informações.

| Tipo de parceiro ou cliente | Como acessar o Destination SDK |
|---------|----------|
| ISV (Independent Software Vendor, fornecedor independente de software) | Participe do [Programa de parceiro de tecnologia da Adobe](https://partners.adobe.com/technologyprogram/experiencecloud.html) e solicite a obtenção de uma sandbox da Experience Platform provisionada para acessar o Destination SDK. |
| Integrador de sistema (SI) | Você precisa estar no nível Gold ou Platinum no [Programa de parceiro de soluções da Adobe](https://solutionpartners.adobe.com/home.html) para obter uma sandbox da Experience Platform provisionada e acesso à Destination SDK. |
| Cliente do Experience Platform no [pacote do Real-Time CDP Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=pt-BR) | Por padrão, você obtém acesso às sandboxes da Experience Platform e ao Destination SDK, permitindo criar destinos privados para sua organização. |

{style="table-layout:auto"}

## Processo de alto nível {#process}

O processo para configurar seu destino no Experience Platform é descrito abaixo:

1. Se você for um ISV ou SI, consulte as informações de [obtenção de acesso](#get-access) na seção acima. [Pacote do Real-Time CDP Ultimate](https://helpx.adobe.com/legal/product-descriptions/real-time-customer-data-platform.html?lang=pt-BR), os clientes podem ignorar esta etapa.
2. [Solicitação para provisionar uma sandbox do Experience Platform](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360037457812-Adobe-Experience-Platform-Sandbox-Accounts-Access-Adding-Users-and-Support) e habilitar a permissão de criação de destino.
3. Crie sua integração. Siga as instruções na documentação do produto para configurar [destinos de streaming](guides/configure-destination-instructions.md) ou [destinos baseados em arquivo](guides/configure-file-based-destination-instructions.md).
4. Teste sua integração. Siga as instruções na documentação do produto para testar [destinos de streaming](testing-api/streaming-destinations/streaming-destination-testing-overview.md) ou [destinos baseados em arquivo](testing-api/batch-destinations/file-based-destination-testing-overview.md).
5. Se você for um ISV ou um SI que está criando uma [integração produtizada](./overview.md#productized-custom-integrations), [envie sua integração](guides/submit-destination.md) para análise da Adobe (o tempo de resposta padrão é de cinco dias úteis).
6. Se você for um ISV ou um SI que está criando uma integração produzida, use o [processo de documentação de autoatendimento](docs-framework/documentation-instructions.md) para criar uma página de documentação do produto no Experience League para o seu destino.
7. Para integrações produzidas, uma vez aprovada pela Adobe, sua integração será exibida no [catálogo do Experience Platform](../catalog/overview.md).
8. Se quiser atualizar a integração, siga o mesmo processo.

## Referência {#reference}

A Adobe recomenda que você leia e entenda a seguinte documentação do Experience Platform:

* [visão geral dos destinos do Adobe Experience Platform](https://experienceleague.adobe.com/docs/experience-platform/destinations/home.html?lang=pt-BR)
* [Base da composição do esquema XDM](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=pt-BR)
* [Visão geral do namespace de identidade](https://experienceleague.adobe.com/docs/experience-platform/identity/namespaces.html?lang=pt-BR)
