---
title: Notas de versão da Adobe Experience Platform
description: As notas de versão de outubro de 2023 para o Adobe Experience Platform.
source-git-commit: d024596c7d85139721ef370f9e081911a217d9ba
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 43%

---

# Notas de versão da Adobe Experience Platform

**Data de lançamento: 25 de outubro de 2023**

Atualizações dos recursos já existentes na Experience Platform:

- [Fontes](#sources)

## Origens {#sources}

A Experience Platform fornece uma API RESTful e uma interface interativa que permite configurar conexões de origem para vários provedores de dados com facilidade. Essas conexões de origem permitem autenticar e conectar a sistemas de armazenamento externos e serviços de CRM, definir períodos para execuções de assimilação e gerenciar a taxa de transferência de assimilação de dados.

**Recursos novos ou atualizados**

| Recurso | Descrição |
| --- | --- |
| Autenticação atualizada para a Data Landing Zone | Agora você pode ver a data de expiração designada da Data Landing Zone ao visualizar suas credenciais. Você deve atualizar seu token antes da data de expiração para continuar usando-o em seu aplicativo. Se você não atualizar o token manualmente antes da data de expiração declarada, ele será atualizado automaticamente e fornecerá um novo token na próxima vez que você recuperar suas credenciais. Para obter mais informações, leia a documentação em [uso da Data Landing Zone](../../sources/tutorials/ui/create/cloud-storage/data-landing-zone.md). |

{style="table-layout:auto"}

Para saber mais sobre fontes, leia o [visão geral das origens](../../sources/home.md).
