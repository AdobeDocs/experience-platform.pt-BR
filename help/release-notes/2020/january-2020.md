---
title: Notas da versão de janeiro de 2020 da Adobe Experience Platform
description: As notas da versão de janeiro de 2020 da Adobe Experience Platform.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: be2ad7a02d4bdf5a26a0847c8ee7a9a93746c2ad
workflow-type: tm+mt
source-wordcount: '887'
ht-degree: 21%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: quinta-feira, 15 de janeiro de 2020**

Atualizações dos recursos já existentes na Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## Sistema de [!DNL Experience Data Model] (XDM) {#xdm}

A padronização e a interoperabilidade são os principais conceitos por trás do [!DNL Experience Platform]. O [!DNL Experience Data Model] (XDM), orientado pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação documentada publicamente projetada para melhorar o potencial das experiências digitais. Ele fornece estruturas e definições comuns para que qualquer aplicativo se comunique com os serviços na Adobe Experience Platform. Seguindo os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de maneira mais rápida e integrada. Você pode obter insights valiosos sobre ações de clientes, definir públicos-alvo por meio de segmentos e usar atributos de clientes para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Restrições de tipo de campo para campos de hierarquia igual | Depois que um campo XDM é definido como um determinado tipo, todos os outros campos de mesmo nome e hierarquia devem usar o mesmo tipo de campo, independentemente das classes ou dos grupos de campos de esquema em que são usados. Por exemplo, se um grupo de campos para a classe [!DNL Profile] do XDM contiver um campo `profile.age` do tipo &quot;inteiro&quot;, um grupo de campos semelhante para o XDM [!DNL ExperienceEvent] não poderá ter um campo `profile.age` do tipo &quot;cadeia de caracteres&quot;. Para utilizar um tipo de campo diferente, o campo deve ser de uma hierarquia diferente do campo definido anteriormente (por exemplo, `profile.person.age`). Esse recurso destina-se a evitar conflitos quando esquemas são reunidos em uma união. Embora a restrição não afete retroativamente os esquemas existentes, é altamente recomendável que você revise seus esquemas em busca de conflitos de tipo de campo e edite-os conforme necessário. |
| Validação de campo que diferencia maiúsculas de minúsculas | Campos personalizados no mesmo nível devem ter nomes diferentes, independentemente das letras maiúsculas e minúsculas. Por exemplo, se você adicionar e um campo personalizado chamado &quot;Email&quot;, não será possível adicionar outro campo personalizado no mesmo nível chamado &quot;email&quot;. |

**Problemas conhecidos**

* None

Para saber mais sobre como trabalhar com XDM usando a API [!DNL Schema Registry] e a interface de usuário [!DNL Schema Editor], leia a [documentação do Sistema XDM](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

As novas regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação. O Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface para ajudar você a gerenciar essas solicitações de dados de seus clientes. Com o [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados privados ou pessoais dos clientes por meio dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Mudança de identidade visual do [!DNL Privacy Service] | O antigo “Serviço do RGPD” foi reformulado para [!DNL Privacy Service] devido à expansão do serviço para oferecer suporte a outras regulamentações, além do RGPD. |
| Novos pontos de acesso de API | O caminho base da API [!DNL Privacy Service] foi atualizado de `/data/privacy/gdpr` para `/data/core/privacy/jobs`. |
| Nova propriedade `regulation` necessária | Ao criar novos processos na API do [!DNL Privacy Service], é necessário fornecer uma propriedade `regulation` no conteúdo da solicitação para indicar sob qual regulamento monitorar o processo. Os valores aceitos são `gdpr` e `ccpa`. |
| Compatibilidade com o [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] agora aceita solicitações de acesso/exclusão do Adobe [!DNL Primetime Authentication], usando `primetimeAuthentication` como valor de produto. |
| Aprimoramentos na interface do usuário do Privacy Service | Páginas de rastreamento de trabalho separadas para os regulamentos do GDPR e da CCPA. Nova lista suspensa **Tipo de regulamentação** para alternar entre os dados de rastreamento do RGPD e da CCPA. |

**Problemas conhecidos**

* None

Para obter mais informações sobre [!DNL Privacy Service], comece lendo a [visão geral do Privacy Service](../../privacy-service/home.md).

## Origens {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir que você estruture, rotule e aprimore esses dados usando os serviços do [!DNL Experience Platform]. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O [!DNL Experience Platform] fornece uma API RESTful e uma interface do usuário interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de ingestão e gerenciar a taxa de transferência de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Suporte para dados de atributos do cliente | Suporte à interface e à API para criar conectores de transmissão para assimilar dados de atributos do cliente. |
| Suporte adicional a formatos de arquivo para armazenamentos em nuvem | A assimilação de arquivos de armazenamentos em nuvem agora é compatível com os formatos de arquivo Parquet e JSON compatíveis com XDM. |
| Suporte para permissões de controle de acesso | A estrutura de controle de acesso no Adobe Experience Platform fornece as permissões necessárias para conceder acesso às fontes na assimilação de dados. Dependendo do nível de permissão, um usuário pode visualizar fontes, gerenciar fontes ou ter o acesso negado. |

**Permissões de controle de acesso**

| Categoria | Permissão | Descrição |
|--- | --- | ---|
| Assimilação de dados | Gerenciar fontes | Acesso para ler, criar, editar e desativar fontes. |
| Assimilação de dados | Exibir fontes | Acesso somente leitura a fontes disponíveis na guia **[!UICONTROL Catalog]** e fontes autenticadas na guia **[!UICONTROL Browse]**. |

**Problemas conhecidos**

* None

Para obter mais informações sobre origens, consulte a [visão geral das origens](../../sources/home.md)

## Destinos {#destinations}

No [Real-Time CDP](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam dados para esses parceiros de forma contínua.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Suporte para permissões de controle de acesso | A funcionalidade Destinos no Real-Time CDP funciona com permissões de controle de acesso do Adobe Experience Platform. Dependendo do nível de permissão do seu usuário, você pode visualizar, gerenciar e ativar destinos. |

**Permissões de controle de acesso**

| Categoria | Permissão | Descrição |
|--- | --- | ---|
| Destinos | Gerenciar destinos | Acesso para ler, criar, editar e desativar destinos. |
| Destinos | Exibir destinos | Acesso somente leitura aos destinos disponíveis na guia **[!UICONTROL Catalog]** e aos destinos autenticados na guia **Procurar**. |
| Destinos | Ativar destinos | Capacidade de ativar dados para destinos. Essa permissão requer que &quot;Gerenciar destinos&quot; ou &quot;Exibir destinos&quot; sejam adicionados ao perfil do produto. |

**Problemas conhecidos**

* None

Consulte a [Visão geral dos Destinos](../../destinations/home.md) para obter mais informações.
