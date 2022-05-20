---
title: Notas de versão da Adobe Experience Platform em janeiro de 2020
description: As notas de versão de janeiro de 2020 para o Adobe Experience Platform.
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
exl-id: e488a50c-2a87-4649-b3a4-f9d45cb12fcb
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 15 de janeiro de 2020**

Atualizações dos recursos existentes na Adobe Experience Platform:

* [[!DNL Experience Data Model (XDM) System]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!DNL Sources]](#sources)
* [[!DNL Destinations]](#destinations)

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

A normalização e a interoperabilidade são conceitos-chave subjacentes [!DNL Experience Platform]. [!DNL Experience Data Model] O (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir esquemas para o gerenciamento da experiência do cliente.

O XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo se comunicar com serviços no Adobe Experience Platform. Ao seguir os padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações valiosas das ações do cliente, definir públicos-alvo do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Restrições de tipo de campo para campos de hierarquia igual | Depois que um campo XDM é definido como um determinado tipo, qualquer outro campo com o mesmo nome e hierarquia deve usar o mesmo tipo de campo, independentemente das classes ou grupos de campo de esquema em que são usados. Por exemplo, se um grupo de campos para o XDM [!DNL Profile] classe contém um `profile.age` campo do tipo &quot;integer&quot;, um grupo de campos semelhante para XDM [!DNL ExperienceEvent] não pode ter um `profile.age` campo do tipo &quot;string&quot;. Para utilizar um tipo de campo diferente, o campo deve ser de uma hierarquia diferente do campo definido anteriormente (por exemplo, `profile.person.age`). Esse recurso tem o objetivo de evitar conflitos quando schemas são reunidos em uma união. Embora a restrição não afete retroativamente os esquemas existentes, é altamente recomendável revisar os esquemas para conflitos do tipo campo e editá-los conforme necessário. |
| Validação de campo sensível a maiúsculas e minúsculas | Os campos personalizados no mesmo nível devem ter nomes diferentes, independentemente da capitalização. Por exemplo, se adicionar um campo personalizado chamado &quot;Email&quot;, não será possível adicionar outro campo personalizado no mesmo nível chamado &quot;email&quot;. |

**Problemas conhecidos**

* None

Para saber mais sobre como trabalhar com o XDM usando o [!DNL Schema Registry] API e [!DNL Schema Editor] interface do usuário, leia a [Documentação do sistema XDM](../../xdm/home.md).

## [!DNL Privacy Service] {#privacy}

As novas regulamentações legais e organizacionais dão aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados, mediante solicitação. Adobe Experience Platform [!DNL Privacy Service] O fornece uma RESTful API e interface do usuário para ajudar você a gerenciar essas solicitações de dados de seus clientes. Com [!DNL Privacy Service], você pode enviar solicitações para acessar e excluir dados pessoais de clientes de aplicativos Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| [!DNL Privacy Service] reformulação da marca | O antigo serviço chamado &quot;GDPR&quot; foi renomeado para [!DNL Privacy Service] à medida que o serviço cresceu para suportar outras regulamentações além do GDPR. |
| Novos endpoints de API | Caminho base para o [!DNL Privacy Service] A API foi atualizada de `/data/privacy/gdpr` para `/data/core/privacy/jobs`. |
| Novo obrigatório `regulation` propriedade | Ao criar novos trabalhos na [!DNL Privacy Service] API, um `regulation` deve ser fornecida na carga da solicitação para indicar em qual regulamento rastrear a tarefa. Os valores aceitos são `gdpr` e `ccpa`. |
| Suporte para [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] agora aceita solicitações de acesso/exclusão do Adobe [!DNL Primetime Authentication], usando `primetimeAuthentication` como valor do produto. |
| Melhorias na interface do usuário do Privacy Service | Páginas de rastreamento de trabalho separadas para regulamentos do GDPR e da CCPA. Novo **Tipo de regulamento **lista suspensa para alternar entre os dados de rastreamento do GDPR e da CCPA. |

**Problemas conhecidos**

* Nenhum

Para obter mais informações sobre [!DNL Privacy Service], comece lendo o [Visão geral do Privacy Service](../../privacy-service/home.md).

## Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] O fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Suporte para dados de atributos do cliente | Suporte a interface do usuário e API para criar conectores de transmissão para assimilar dados de atributos do cliente. |
| Suporte adicional ao formato de arquivo para armazenamento em nuvem | A assimilação de arquivos de armazenamento em nuvem agora é compatível com os formatos de arquivo Parquet e JSON compatíveis com XDM. |
| Suporte para permissões de controle de acesso | A estrutura de controle de acesso no Adobe Experience Platform fornece as permissões necessárias para conceder acesso a fontes na assimilação de dados. Dependendo do nível de permissão, um usuário pode exibir fontes, gerenciar fontes ou ter acesso negado completamente. |

**Permissões de controle de acesso**

| Categoria | Permissão | Descrição |
|--- | --- | ---|
| Assimilação de dados | Gerenciar fontes | Acesso para ler, criar, editar e desativar fontes. |
| Assimilação de dados | Exibir fontes | Acesso somente leitura a fontes disponíveis no **[!UICONTROL Catálogo]** e fontes autenticadas na **[!UICONTROL Procurar]** guia . |

**Problemas conhecidos**

* Nenhum

Para obter mais informações sobre fontes, consulte o [visão geral das fontes](../../sources/home.md)

## Destinos {#destinations}

Em [CDP em tempo real](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Suporte para permissões de controle de acesso | A funcionalidade Destinos na CDP em tempo real funciona com permissões de controle de acesso do Adobe Experience Platform. Dependendo do nível de permissão do usuário, você pode visualizar, gerenciar e ativar destinos. |

**Permissões de controle de acesso**

| Categoria | Permissão | Descrição |
|--- | --- | ---|
| Destinos | Gerenciar destinos | Acesso para ler, criar, editar e desativar destinos. |
| Destinos | Exibir destinos | Acesso somente leitura a destinos disponíveis na **[!UICONTROL Catálogo]** e destinos autenticados no **Procurar** guia . |
| Destinos | Ativar destinos | Capacidade de ativar dados para destinos. Essa permissão requer que &quot;Gerenciar destinos&quot; ou &quot;Exibir destinos&quot; sejam adicionados ao perfil do produto. |

**Problemas conhecidos**

* Nenhum

Consulte a [Visão geral dos destinos](../../destinations/home.md) para obter mais informações.
