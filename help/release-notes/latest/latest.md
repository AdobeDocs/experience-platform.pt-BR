---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão mais recentes do Adobe Experience Platform.
source-git-commit: 0209d7ef1c82915bc11f07518194e3dd68c63de9
workflow-type: tm+mt
source-wordcount: '458'
ht-degree: 9%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 27 de outubro de 2021**

## Atualizações no Experience Platform

Atualizações no Experience Platform.

### Interface do usuário {#ui}

A interface do usuário foi atualizada com as seguintes alterações:

| Recurso | Descrição |
| --- | --- |
| Tema escuro | Use a troca de tema escuro para alternar entre temas claros e escuros na interface da plataforma. O switch está localizado no perfil do usuário abaixo do nome de usuário e email. |
| Alternar navegação à esquerda | Use a alternância de navegação aprimorada na parte superior do cabeçalho do aplicativo para mostrar ou ocultar o menu que exibe seus recursos do Experience Platform. O sistema lembra da última seleção e mostra apenas os recursos aos quais você tem acesso. |
| Visibilidade de acesso | A barra de navegação esquerda mostra apenas os recursos que você pode acessar. Em versões anteriores do Adobe Experience Platform, os itens indisponíveis ficavam visíveis, mesmo se você não conseguisse acessá-los. |

Consulte a [Guia da interface do usuário da plataforma](../../landing/ui-guide.md) para saber mais.

## Atualizações dos recursos existentes

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Fontes](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Função `contains_key`  | O `contains_key` foi introduzida, permitindo verificar se o objeto existe na fonte. Essa função substitui `is_set` , que agora está obsoleta. |
| Mensagens de erro | Mensagens de erro retornadas pela `/mappingSets/preview` endpoint na API de preparação de dados agora são consistentes com as mensagens de erro geradas durante o tempo de execução. |

Consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md) para saber mais sobre esse serviço.

### Fontes {#sources}

A Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, permitir estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma RESTful API e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e se conectar a sistemas de armazenamento externos e serviços CRM, definir horários para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| [!DNL Amazon S3] melhorias na fonte | Agora você pode usar o `s3SessionToken` para conectar seu [!DNL Amazon S3] conta para a Platform usando credenciais de segurança temporárias. Esse token permite que você forneça acesso temporário e de curto prazo ao seu [!DNL Amazon S3] recursos para usuários em ambientes não confiáveis. Consulte a [[!DNL Amazon S3] documentação](../../sources/connectors/cloud-storage/s3.md#prerequisites) para obter mais informações. |
| [!DNL Generic REST API] (Beta) | Agora você pode criar um [!DNL Generic REST API] conexão de origem usando o [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) ou [interface do usuário](../../sources/tutorials/ui/create/protocols/generic-rest.md) para trazer dados de um aplicativo REST genérico para a plataforma. Consulte a [[!DNL Generic REST API] visão geral](../../sources/connectors/protocols/generic-rest.md) para obter mais informações. |
| [!DNL Zoho CRM] (Beta) | Agora você pode criar um [!DNL Zoho CRM] conexão de origem usando o [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) ou [interface do usuário](../../sources/tutorials/ui/create/crm/zoho.md) para trazer dados do [!DNL Zoho CRM] para a Platform. Consulte a [[!DNL Zoho CRM] visão geral](../../sources/connectors/crm/zoho.md) para obter mais informações. |

Para saber mais sobre fontes, consulte o [visão geral das fontes](../../sources/home.md).
