---
keywords: Experience Platform;home;popular topics
solution: Experience Platform
title: Adobe Experience Platform Privacy Service
topic: overview
translation-type: tm+mt
source-git-commit: bd9884a24c5301121f30090946ab24d9c394db1b
workflow-type: tm+mt
source-wordcount: '596'
ht-degree: 10%

---


# Visão geral do Adobe Experience Platform Privacy Service

Para oferecer melhores experiências aos clientes, é necessário coletar e armazenar os dados pessoais dos clientes. Ao usar esses dados, é importante entender e respeitar a privacidade dos clientes. As novas regulamentações legais e organizacionais estão dando aos usuários o direito de acessar ou excluir seus dados pessoais dos armazenamentos de dados mediante solicitação.

O Adobe Experience Platform Privacy Service fornece uma API RESTful e uma interface de usuário para ajudá-lo a gerenciar essas solicitações de dados de seus clientes. Com o Privacy Service, você pode enviar solicitações para acessar e excluir dados pessoais ou particulares de clientes dos aplicativos da Adobe Experience Cloud, facilitando a conformidade automatizada com as regulamentações legais e organizacionais de privacidade.

## Por que Privacy Service?

A Privacy Service foi desenvolvida em resposta a uma mudança fundamental na forma como as empresas são obrigadas a gerir os dados pessoais dos seus clientes. O objetivo central do Privacy Service é automatizar a conformidade com as regulamentações de privacidade de dados que, quando violadas, podem resultar em multas importantes e interromper as operações de dados para sua empresa.

### Privacy Service e RGPD

O [](https://eugdpr.org/)Regulamento Geral sobre a Proteção de Dados (GDPR) introduziu vários novos direitos de privacidade de dados para os membros da União Europeia, incluindo o **Direito de acesso** e o **Direito de ser esquecido**. Isso significa que qualquer cidadão da UE cujos dados pessoais tenham sido coletados pela sua empresa pode solicitar acesso ou apagar os dados a qualquer momento. Se essas solicitações não forem atendidas dentro de 30 dias, poderá resultar em multas de vários milhões de dólares para sua organização.

O Privacy Service suporta o acesso e a exclusão de solicitações do RGPD e os acompanha separadamente das solicitações feitas no âmbito do regulamento CCPA. Consulte as Perguntas frequentes [do](gdpr/faq.md) RGPD e os documentos [terminológicos](gdpr/terminology.md) para obter mais informações.

### Privacy Service e CCPA

The [California Consumer Privacy Act](https://www.caprivacy.org/about) (CCPA) enhances privacy rights and consumer protection for residents of California, United States. A CCPA fornece novos direitos de privacidade de dados aos residentes da Califórnia, incluindo o direito de acessar e excluir seus dados pessoais, saber se seus dados pessoais são vendidos ou divulgados (e a quem) e o direito de opt out a venda de seus dados a terceiros.

O Privacy Service suporta o acesso e a exclusão de solicitações para o regulamento CCPA e os acompanha separadamente das solicitações do RGPD. O Privacy Service também oferece suporte para o envio de solicitações de não participação na venda para aplicativos Experience Cloud que os suportam. Consulte as Perguntas frequentes [do](ccpa/faq.md) CCPA para obter mais informações.

## Como usar o Privacy Service para gerenciar solicitações de trabalhos de privacidade

O Privacy Service fornece uma API RESTful e uma interface de usuário que permitem gerenciar as solicitações de seus clientes para acessar/excluir seus dados privados ou opt out a venda (também conhecidos como trabalhos **de** privacidade). O serviço também fornece um mecanismo central de auditoria e registro que permite que você visualização o status e os resultados de tarefas de privacidade que envolvem aplicativos Experience Cloud.

>[!NOTE]
>
>Atualmente, as solicitações de cancelamento são suportadas apenas pela API Privacy Service.

### Uso da API

A API [](https://www.adobe.io/apis/experienceplatform/home/api-reference.html#!acpdr/swagger-specs/privacy-service.yaml) Privacy Service permite criar e gerenciar trabalhos de privacidade usando chamadas RESTful API, permitindo que você adote a conformidade com a regulamentação de privacidade de modo programático para seus aplicativos Experience Cloud. Para obter etapas detalhadas sobre como usar a API, consulte o guia [do desenvolvedor da API de](api/getting-started.md)Privacy Service.

### Uso da interface

A interface do usuário do Privacy Service permite que você crie e monitore trabalhos de privacidade usando uma interface gráfica. A interface do usuário inclui um widget Relatório **de** status que fornece uma representação visual do status de todas as solicitações ativas e permite que você crie novas solicitações usando o Construtor **de** solicitações integrado ou fazendo upload de arquivos JSON. Para obter mais informações sobre como usar a interface do usuário, consulte o guia [do usuário do](ui/overview.md)Privacy Service.