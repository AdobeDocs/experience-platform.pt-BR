---
keywords: exibir perfis rtcdp;exibição de perfil rtcdp;perfis rtcdp
title: Procurar perfis no Real-time Customer Data Platform
description: O Adobe Real-time Customer Data Platform permite navegar pelos dados do Perfil do cliente em tempo real usando a interface do usuário do Adobe Experience Platform.
feature: Get Started, Profiles
exl-id: 8481e286-2ff0-484f-85d2-a8db9b08d8d3
source-git-commit: ea785ffa1dfa0f7c684fe536796a4b7409882159
workflow-type: tm+mt
source-wordcount: '557'
ht-degree: 0%

---


# Procurar perfis no Real-time Customer Data Platform

O Perfil do cliente em tempo real cria uma visualização integral de cada cliente individual, combinando dados de vários canais, inclusive dados online, offline, de CRM e de terceiros. À medida que perfis individuais são agregados com base nos dados trazidos para o sistema de várias fontes, cada perfil se torna uma conta acionável com carimbo de data e hora de cada interação que seu cliente tem com sua marca.

Na interface do usuário do Adobe Experience Platform, você pode visualizar esses perfis somente leitura e ver informações importantes sobre cada cliente individual, incluindo suas preferências, eventos anteriores, interações e os públicos aos quais o indivíduo pertence.

O Adobe Real-time Customer Data Platform é construído sobre o Adobe Experience Platform e, portanto, pode usar os recursos de visualização de perfil na interface do usuário do Experience Platform. Para obter um guia detalhado para visualizar perfis de clientes na interface do usuário da Platform, consulte o [Guia do usuário do Perfil do cliente em tempo real](../../profile/ui/user-guide.md).

## Aprimoramentos de perfil para o Real-Time CDP, B2B Edition

Além dos recursos de navegação de perfil compatíveis com o Adobe Experience Platform, Real-Time CDP, os usuários do B2B Edition podem acessar atributos e eventos B2B no perfil do cliente na [!UICONTROL Atributos] e [!UICONTROL Eventos] guias, respectivamente. Os dados B2B também podem ser usados para executar a segmentação, com esses públicos aparecendo no do cliente [!UICONTROL associação de público] ao lado de públicos-alvo não B2B.

Real-Time CDP, B2B Edition também permite navegar [!UICONTROL Contas], [!UICONTROL Oportunidades], e [!UICONTROL Registros de origem] em todas as fontes da empresa associadas a um cliente individual.

Para explorar esses aprimoramentos, comece seguindo as etapas descritas na seção [Guia do usuário do Perfil do cliente em tempo real](../../profile/ui/user-guide.md) para procurar um perfil por política de mesclagem ou namespace de identidade.

![](images/b2b-browse-profile.png)

Os detalhes do perfil incluem acesso a [!UICONTROL Contas], [!UICONTROL Oportunidades], e [!UICONTROL Registros de origem] guias, além das informações padrão fornecidas no perfil do cliente, que também foram aprimoradas com eventos e atributos B2B.

![](images/b2b-profile-detail.png)

Para saber mais sobre os detalhes do perfil fornecidos na interface do usuário da Platform, consulte o [seção de detalhes da documentação do painel Perfis](../../dashboards/guides/profiles.md#browse-profiles).

### Guia Contas

Selecionar **[!UICONTROL Contas]** para exibir uma lista de contas relacionadas ao perfil. Essa lista inclui informações básicas do perfil da conta, como nome, site e setor da conta, bem como um link para o perfil da conta.

Para obter mais informações sobre como visualizar e explorar perfis de conta, comece lendo o [visão geral dos perfis de conta](../accounts/account-profile-overview.md).

![](images/b2b-profile-accounts.png)

### Guia Oportunidades

A variável **[!UICONTROL Oportunidades]** A guia fornece detalhes relacionados às oportunidades abertas e fechadas relacionadas à conta. Essas oportunidades podem ser assimiladas no Experience Platform de várias fontes. No entanto, o Real-Time CDP, B2B Edition facilita que os profissionais de marketing vejam todas essas oportunidades em um único local.

Cada oportunidade inclui informações como o nome da oportunidade, sua quantidade, estágio e se a oportunidade está em aberto, fechada, ganha ou perdida.

![](images/b2b-profile-opportunities.png)

### Guia Registros de origem

A variável **[!UICONTROL Registros de origem]** permite ver facilmente os vários registros de origem provenientes das fontes da empresa que estão contribuindo para o único perfil do cliente. Além do [!UICONTROL Chave de origem da pessoa] e endereço de email, cada registro de origem também fornece o tipo de registro (por exemplo, um registro &quot;contato&quot; ou &quot;lead&quot;), bem como a origem.

![](images/b2b-profile-source-records.png)
