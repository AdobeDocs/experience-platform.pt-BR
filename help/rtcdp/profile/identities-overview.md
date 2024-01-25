---
keywords: identidades rtcdp;rtcdp identidades;real-time cdp identidades;identities rtcdp;rtcdp identities;real-time cdp identities
title: Identidades no Real-time Customer Data Platform
description: O Serviço de identidade da Adobe Experience Platform ajuda você a ter uma melhor visão dos clientes e do comportamento deles ao unir as identidades de vários dispositivos e sistemas.
feature: Get Started, Identities
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: ba39f62cd77acedb7bfc0081dbb5f59906c9b287
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# Visão geral das identidades

Adobe Experience Platform [!DNL Identity Service] O ajuda você a obter uma melhor visualização dos clientes e do comportamento deles ao unir as identidades de vários dispositivos e sistemas. Normalmente, seus clientes interagem com sua marca em vários canais, isso pode incluir navegar pelo site online, fazer uma compra na loja, ingressar em seu programa de fidelidade ou ligar para um suporte técnico, para citar alguns. Nesses vários sistemas, há uma identidade criada para esse cliente e [!DNL Identity Service] permite reunir essas identidades para ver o quadro completo.

Agora, em vez de cinco clientes separados interagirem com sua marca em cinco canais diferentes, você pode ver que esse é o mesmo cliente e garantir que eles recebam uma experiência consistente, personalizada e relevante em cada interação. À medida que mais informações sobre o cliente são conhecidas (por exemplo, um navegador anônimo do site decide se cadastrar em uma conta e fazer logon), essas informações são unidas e a imagem do cliente fica cada vez mais clara.

## Namespaces de identidade

Os namespaces de identidade são um componente de [!DNL Identity Service] e servem como indicadores que fornecem contexto adicional para as identidades dos clientes. Um exemplo de namespace de ID usado com frequência seria &quot;Email&quot;, em que o uso do mesmo endereço de email em vários sites permite unir várias identidades diferentes, cada uma com uma ID de cliente exclusiva, como realmente pertencente ao mesmo cliente. [!DNL Experience Platform] O permite usar namespaces de ID para procurar perfis individuais na interface. Para obter mais informações sobre visualização de perfis, consulte a [visão geral de navegação de perfil](profile-browse.md). Para saber mais sobre namespaces de identidade, consulte a [visão geral do namespace de identidade](../../identity-service/features/namespaces.md).

## Gráficos de identidade

Um gráfico de identidade é um mapa dos relacionamentos entre identidades diferentes, que fornece uma representação visual de como o cliente interage com a marca em diferentes canais. Todos os gráficos de identidade do cliente são gerenciados e atualizados coletivamente pelo Serviço de identidade, em resposta à atividade do cliente.

[!DNL Identity Service] O gerencia um gráfico de identidade visível somente para sua organização e criado com base em seus dados. [!DNL Identity Service] aumenta o gráfico quando um registro de dados assimilado contém mais de uma identidade, adicionando uma relação entre as identidades encontradas.

## Próximas etapas

identidades e as relações entre elas são definidas e mantidas por [!DNL Identity Service] e aproveitado por [!DNL Real-Time Customer Profile] para criar uma imagem completa de cada cliente individual e suas interações. Para saber mais, visite o [Documentação do Serviço de identidade](../../identity-service/home.md).
