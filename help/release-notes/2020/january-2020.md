---
title: 'Notas de versão do Adobe Experience Platform '
description: Notas de versão da plataforma Experience 15 de janeiro de 2020
doc-type: release notes
last-update: January 15, 2020
author: crhoades, ens28527
translation-type: tm+mt
source-git-commit: 2f0f155beacbc6a4ba2892ae211a9c0305e969ac

---


# Notas de versão da Adobe Experience Platform

## Data de lançamento: 15 de janeiro de 2020

## Sistema do Experience Data Model (XDM)

A normalização e a interoperabilidade são conceitos-chave por trás da plataforma da experiência. O Experience Data Model (XDM), desenvolvido pela Adobe, é um esforço para padronizar os dados de experiência do cliente e definir schemas para o gerenciamento da experiência do cliente.

A XDM é uma especificação publicamente documentada projetada para melhorar o poder das experiências digitais. Fornece estruturas e definições comuns para qualquer aplicativo que se comunique com os serviços na Adobe Experience Platform. Ao aderir aos padrões XDM, todos os dados de experiência do cliente podem ser incorporados a uma representação comum, fornecendo insights de forma mais rápida e integrada. Você pode obter informações importantes das ações do cliente, definir audiências do cliente por meio de segmentos e usar atributos do cliente para fins de personalização.

### Novos recursos

| Recurso | Descrição |
|--- | ---|
| Restrições de tipo de campo para campos de hierarquia igual | Depois que um campo XDM é definido como um determinado tipo, qualquer outro campo com o mesmo nome e hierarquia deve usar o mesmo tipo de campo, independentemente das classes ou combinações em que são usados. Por exemplo, se uma combinação para a classe de Perfil XDM contiver um `profile.age` campo do tipo &quot;integer&quot;, uma combinação semelhante para XDM ExperienceEvent não poderá ter um `profile.age` campo do tipo &quot;string&quot;. Para utilizar um tipo de campo diferente, o campo deve ser de uma hierarquia diferente do campo definido anteriormente (por exemplo, `profile.person.age`). Este recurso é feito para evitar conflitos quando schemas são reunidos em uma união. Embora a restrição não afete retroativamente os schemas existentes, é altamente recomendável que você revise seus schemas em busca de conflitos de tipo de campo e edite-os conforme necessário. |
| Validação de campo que diferencia maiúsculas de minúsculas | Campos personalizados no mesmo nível devem ter nomes diferentes, independentemente da capitalização. Por exemplo, se você adicionar um campo personalizado chamado &quot;Email&quot;, não será possível adicionar outro campo personalizado no mesmo nível chamado &quot;email&quot;. |

### Problemas conhecidos

* Nenhum

Para saber mais sobre como trabalhar com o XDM usando a API do Registro do Schema e a interface do usuário do Editor de Schemas, leia a documentação [do Sistema](../../xdm/home.md)XDM.

## Privacy Service

As novas regulamentações legais e organizacionais estão dando aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados mediante solicitação. O Adobe Experience Platform Privacy Service fornece uma API RESTful e uma interface de usuário para ajudá-lo a gerenciar essas solicitações de dados de seus clientes. Com o Privacy Service, você pode enviar solicitações para acessar e excluir dados pessoais ou privados de clientes dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

### Novos recursos

| Recurso | Descrição |
|--- | ---|
| Rebranding do Privacy Service | A antiga chamada &quot;GDPR Service&quot; foi substituída pelo Privacy Service, já que o serviço cresceu para suportar outras regulamentações além do RGPD. |
| Novos pontos de extremidade de API | O caminho básico para a API do Privacy Service foi atualizado de `/data/privacy/gdpr` para `/data/core/privacy/jobs`. |
| Nova propriedade `regulation` obrigatória | Ao criar novos trabalhos na API do Privacy Service, uma `regulation` propriedade deve ser fornecida na carga da solicitação para indicar em qual regulamento rastrear o trabalho. Os valores aceitos são `gdpr` e `ccpa`. |
| Suporte para autenticação do Adobe Primetime | O Privacy Service agora aceita solicitações de acesso/exclusão da Adobe Primetime Authentication, usando `primetimeAuthentication` como valor de produto. |
| Aprimoramentos da interface do usuário do Privacy Service | Separe as páginas de rastreamento de trabalho para os regulamentos de RGPD e CCPA. Novo menu suspenso Tipo _de_ regulamento para alternar entre os dados de rastreamento para RGPD e CCPA. |

### Problemas conhecidos

* Nenhum

Para obter mais informações sobre o Privacy Service, leia a visão geral [](../../privacy-service/home.md)do Privacy Service para obter start.

## Fontes

A plataforma Adobe Experience pode assimilar dados de fontes externas, permitindo que você estruture, rotule e aprimore esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos da Adobe, armazenamentos baseados em nuvem, software de terceiros e seu sistema de CRM.

A plataforma Experience fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem que você se autentique e se conecte a sistemas de armazenamentos externos e serviços CRM, defina horários para execuções de ingestão e gerencie a throughput de ingestão de dados.

### Novos recursos

| Recurso | Descrição |
|--- | ---|
| Suporte para dados de atributos do cliente | Suporte à interface do usuário e à API para criar conectores de transmissão para assimilar dados de atributos do cliente. |
| Suporte adicional ao formato de arquivo para armazenamentos em nuvem | A ingestão de arquivos de armazenamentos em nuvem agora oferece suporte aos formatos de arquivo em conformidade com XDM Parquet e JSON. |
| Suporte para permissões de controle de acesso | A estrutura do controle de acesso na plataforma Adobe Experience fornece as permissões necessárias para conceder acesso às fontes na ingestão de dados. Dependendo do nível de permissão, um usuário pode visualização de fontes, gerenciar fontes ou ter acesso negado totalmente. |

**Permissões do Controle de acesso**

| Categoria | Permissão | Descrição |
|--- | --- | ---|
| Ingestão de dados | Gerenciar fontes | Acesso para ler, criar, editar e desativar fontes. |
| Ingestão de dados | Fontes de Visualização | Acesso somente leitura a fontes disponíveis na guia *Catálogo* e fontes autenticadas na guia *Procurar* . |

### Problemas conhecidos

* Nenhum

Para obter mais informações sobre fontes, consulte a visão geral [das fontes](../../sources/home.md)

## Destinos

Na CDP [em tempo real da](../../rtcdp/overview.md)Adobe, os destinos são integrações pré-criadas com plataformas de destino que ativam os dados para esses parceiros de forma contínua.

### Novos recursos

| Recurso | Descrição |
|--- | ---|
| Suporte para permissões de controle de acesso | A funcionalidade Destinos na CDP em tempo real funciona com permissões de controle de acesso da plataforma Adobe Experience. Dependendo do nível de permissão do usuário, você pode visualização, gerenciar e ativar destinos. |

**Permissões do Controle de acesso**

| Categoria | Permissão | Descrição |
|--- | --- | ---|
| Destinos | Gerenciar destinos | Acesso para ler, criar, editar e desativar destinos. |
| Destinos | Destinos da Visualização | Acesso somente leitura a destinos disponíveis na guia _Catálogo_ e destinos autenticados na guia _Procurar_ . |
| Destinos | Ativar destinos | Capacidade de ativar dados para destinos. Essa permissão requer que &quot;Gerenciar destinos&quot; ou &quot;Destinos de Visualização&quot; sejam adicionados ao perfil do produto. |

### Problemas conhecidos

* Nenhum

Consulte a visão geral [de](../../rtcdp/destinations/destinations-overview.md) Destinos para obter mais informações.