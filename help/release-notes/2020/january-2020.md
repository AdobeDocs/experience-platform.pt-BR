---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão de Experience Platform 15 de janeiro de 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: c6c5ada52321b11543254f80399c38365f0fb9d7
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 5%

---


# Notas de versão da Adobe Experience Platform

**Data de lançamento: 15 de janeiro de 2020**

Atualizações dos recursos existentes no Adobe Experience Platform:

* [Sistema do [!DNL Experience Data Model (XDM)]](#xdm)
* [[!DNL Privacy Service]](#privacy)
* [[!Fontes DNL]](#sources)
* [[!Destinos DNL]](#destinations)

## [!DNL Experience Data Model] Sistema (XDM) {#xdm}

A normalização e a interoperabilidade são conceitos fundamentais subjacentes [!DNL Experience Platform]. [!DNL Experience Data Model] (XDM), impulsionado pelo Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

A XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo que se comunique com os serviços da Adobe Experience Platform. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações importantes das ações do cliente, definir audiências do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Restrições de tipo de campo para campos de hierarquia igual | Depois que um campo XDM é definido como um determinado tipo, qualquer outro campo com o mesmo nome e hierarquia deve usar o mesmo tipo de campo, independentemente das classes ou combinações em que são usados. Por exemplo, se uma mistura para a [!DNL Profile] classe XDM contiver um `profile.age` campo do tipo &quot;integer&quot;, uma mistura semelhante para XDM [!DNL ExperienceEvent] não poderá ter um `profile.age` campo do tipo &quot;string&quot;. Para utilizar um tipo de campo diferente, o campo deve ser de uma hierarquia diferente do campo definido anteriormente (por exemplo, `profile.person.age`). Este recurso é feito para evitar conflitos quando schemas são reunidos em uma união. Embora a restrição não afete retroativamente os schemas existentes, é altamente recomendável que você revise seus schemas em busca de conflitos de tipo de campo e edite-os conforme necessário. |
| Validação de campo que diferencia maiúsculas de minúsculas | Campos personalizados no mesmo nível devem ter nomes diferentes, independentemente da capitalização. Por exemplo, se você adicionar um campo personalizado chamado &quot;Email&quot;, não será possível adicionar outro campo personalizado no mesmo nível chamado &quot;email&quot;. |

**Problemas conhecidos**

* None

Para saber mais sobre como trabalhar com o XDM usando a [!DNL Schema Registry] API e a interface do [!DNL Schema Editor] usuário, leia a documentação [do Sistema](../../xdm/home.md)XDM.

## [!DNL Privacy Service] {#privacy}

As novas regulamentações legais e organizacionais estão dando aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados mediante solicitação. A Adobe Experience Platform [!DNL Privacy Service] fornece uma API RESTful e uma interface de usuário para ajudá-lo a gerenciar essas solicitações de dados de seus clientes. Com [!DNL Privacy Service]o, você pode enviar solicitações para acessar e excluir dados pessoais ou particulares de clientes de aplicativos Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| [!DNL Privacy Service] nova marca | A antiga chamada &quot;GDPR Service&quot; foi substituída por [!DNL Privacy Service] que o serviço cresceu para suportar outras regulamentações além do RGPD. |
| Novos pontos de extremidade de API | O caminho básico para a [!DNL Privacy Service] API foi atualizado de `/data/privacy/gdpr` para `/data/core/privacy/jobs`. |
| Nova propriedade `regulation` obrigatória | Ao criar novos trabalhos na [!DNL Privacy Service] API, uma `regulation` propriedade deve ser fornecida na carga da solicitação para indicar em qual regulamento rastrear o trabalho. Os valores aceitos são `gdpr` e `ccpa`. |
| Suporte para [!DNL Adobe Primetime Authentication] | [!DNL Privacy Service] agora aceita solicitações de acesso/exclusão do Adobe [!DNL Primetime Authentication], usando `primetimeAuthentication` como valor do produto. |
| Aprimoramentos da interface do Privacy Service | Separe as páginas de rastreamento de trabalho para os regulamentos de RGPD e CCPA. Novo menu suspenso Tipo _de_ regulamento para alternar entre os dados de rastreamento para RGPD e CCPA. |

**Problemas conhecidos**

* None

Para obter mais informações sobre [!DNL Privacy Service], leia a visão geral [do](../../privacy-service/home.md)Privacy Service.

## Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando [!DNL Platform] serviços. Você pode assimilar dados de várias fontes, como aplicativos de Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

[!DNL Experience Platform] fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Suporte para dados de atributos do cliente | Suporte à interface do usuário e à API para criar conectores de transmissão para assimilar dados de atributos do cliente. |
| Suporte adicional ao formato de arquivo para armazenamentos em nuvem | A ingestão de arquivos de armazenamentos em nuvem agora oferece suporte aos formatos de arquivo em conformidade com XDM Parquet e JSON. |
| Suporte para permissões de controle de acesso | A estrutura do controle de acesso no Adobe Experience Platform fornece as permissões necessárias para conceder acesso a fontes na ingestão de dados. Dependendo do nível de permissão, um usuário pode visualização de fontes, gerenciar fontes ou ter acesso negado totalmente. |

**Permissões do controle de acesso**

| Categoria | Permissão | Descrição |
|--- | --- | ---|
| Ingestão de dados | Gerenciar fontes | Acesso para ler, criar, editar e desativar fontes. |
| Ingestão de dados | Fontes de visualização | Acesso somente leitura a fontes disponíveis na guia **[!UICONTROL Catálogo]** e fontes autenticadas na guia **[!UICONTROL Procurar]** . |

**Problemas conhecidos**

* None

Para obter mais informações sobre fontes, consulte a visão geral [das fontes](../../sources/home.md)

## Destinos {#destinations}

No [Adobe Real-time CDP](../../rtcdp/overview.md), os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de uma forma contínua.

**Novos recursos**

| Recurso | Descrição |
|--- | ---|
| Suporte para permissões de controle de acesso | A funcionalidade Destinos no CDP em tempo real funciona com permissões de controle de acesso Adobe Experience Platform. Dependendo do nível de permissão do usuário, você pode visualização, gerenciar e ativar destinos. |

**Permissões do controle de acesso**

| Categoria | Permissão | Descrição |
|--- | --- | ---|
| Destinos | Gerenciar destinos | Acesso para ler, criar, editar e desativar destinos. |
| Destinos | Destinos da visualização | Acesso somente leitura a destinos disponíveis na guia [!UICONTROL _Catálogo_] e destinos autenticados na guia _Procurar_ . |
| Destinos | Ativar destinos | Capacidade de ativar dados para destinos. Essa permissão requer que &quot;Gerenciar destinos&quot; ou &quot;Destinos de Visualização&quot; sejam adicionados ao perfil do produto. |

**Problemas conhecidos**

* None

Consulte a visão geral [de](../../rtcdp/destinations/destinations-overview.md) Destinos para obter mais informações.