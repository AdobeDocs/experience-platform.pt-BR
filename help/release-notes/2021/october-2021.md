---
title: Notas de versão da Adobe Experience Platform de outubro de 2021
description: As notas de versão de outubro de 2021 para o Adobe Experience Platform.
exl-id: 8f8bcb24-6478-4281-9362-9559158384af
source-git-commit: ce967ae176fce81aa26d92b3f0ee8be006808657
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 10%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 27 de outubro de 2021**

## Atualizações no Experience Platform

Atualizações no Experience Platform.

### Interface do usuário {#ui}

A interface do usuário do foi atualizada com as seguintes alterações:

| Recurso | Descrição |
| --- | --- |
| Tema escuro | Use o switch de tema escuro para alternar entre temas claros e escuros na interface da Platform. O comutador está localizado no perfil de usuário abaixo do nome de usuário e e-mail. |
| Alternar navegação à esquerda | Use o botão de navegação aprimorado na parte superior do cabeçalho do aplicativo para mostrar ou ocultar o menu que exibe seus recursos de Experience Platform. O sistema lembra da última seleção e mostra apenas os recursos aos quais você tem acesso. |
| Visibilidade de acesso | A barra de navegação esquerda mostra apenas os recursos que você pode acessar. Em versões anteriores do Adobe Experience Platform, os itens indisponíveis estavam visíveis, mesmo se você não conseguisse acessá-los. |

Consulte a [Guia da interface do usuário da Platform](../../landing/ui-guide.md) para saber mais.

## Atualizações dos recursos existentes

Atualizações dos recursos existentes na Adobe Experience Platform:

- [[!DNL Data Prep]](#data-prep)
- [Fontes](#sources)

### [!DNL Data Prep] {#data-prep}

[!DNL Data Prep] O permite que os engenheiros de dados mapeiem, transformem e validem dados de e para o Experience Data Model (XDM).

**Recursos atualizados**

| Recurso | Descrição |
| --- | --- |
| Função `contains_key`  | A variável `contains_key` foi introduzida, que permite verificar se o objeto existe dentro da origem. Esta função substitui a `is_set` função, que agora está obsoleta. |
| Mensagens de erro | Mensagens de erro retornadas pelo `/mappingSets/preview` Os pontos de extremidade na API de preparação de dados agora são consistentes com as mensagens de erro geradas durante o tempo de execução. |

Consulte a [[!DNL Data Prep] visão geral](../../data-prep/home.md) para saber mais sobre este serviço.

### Fontes {#sources}

O Adobe Experience Platform pode assimilar dados de fontes externas e, ao mesmo tempo, estruturar, rotular e aprimorar esses dados usando os serviços da plataforma. Você pode assimilar dados de várias fontes, como aplicativos Adobe, armazenamento baseado em nuvem, software de terceiros e seu sistema de CRM.

O Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir tempos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

| Recurso | Descrição |
| --- | --- |
| [!DNL Amazon S3] aprimoramentos na origem | Agora você pode usar o `s3SessionToken` parâmetro para conectar seu [!DNL Amazon S3] para a Platform usando credenciais de segurança temporárias. Esse token permite fornecer acesso temporário a curto prazo aos [!DNL Amazon S3] recursos para usuários em ambientes não confiáveis. Consulte a [[!DNL Amazon S3] documentação da](../../sources/connectors/cloud-storage/s3.md#prerequisites) para obter mais informações. |
| [!DNL Generic REST API] (Beta) | Agora você pode criar um [!DNL Generic REST API] conexão de origem usando o [[!DNL Flow Service] API](../../sources/tutorials/api/create/protocols/generic-rest.md) para trazer dados de um aplicativo REST genérico para a Platform. Consulte a [[!DNL Generic REST API] visão geral das ](../../sources/connectors/protocols/generic-rest.md) para obter mais informações. |
| [!DNL Zoho CRM] (Beta) | Agora você pode criar um [!DNL Zoho CRM] conexão de origem usando o [[!DNL Flow Service] API](../../sources/tutorials/api/create/crm/zoho.md) ou o [interface do usuário](../../sources/tutorials/ui/create/crm/zoho.md) para trazer dados de seu [!DNL Zoho CRM] para a Platform. Consulte a [[!DNL Zoho CRM] visão geral das ](../../sources/connectors/crm/zoho.md) para obter mais informações. |

Para saber mais sobre fontes, consulte a [visão geral das origens](../../sources/home.md).
