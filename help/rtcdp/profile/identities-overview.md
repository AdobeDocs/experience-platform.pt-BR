---
keywords: identidades rtcdp; identidades rtcdp; identidades cdp em tempo real
title: Identidades na Real-time Customer Data Platform
description: O serviço de identidade da Adobe Experience Platform ajuda você a obter uma melhor visão de seus clientes e de seu comportamento ao unir identidades em dispositivos e sistemas.
exl-id: 2b0d84de-9710-412e-ace7-56e3977245aa
source-git-commit: 34e0381d40f884cd92157d08385d889b1739845f
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 0%

---

# Visão geral das identidades

Adobe Experience Platform [!DNL Identity Service] O ajuda você a obter uma melhor visão de seus clientes e de seu comportamento ao unir identidades em dispositivos e sistemas. Normalmente, seus clientes interagem com sua marca em vários canais, isso pode incluir navegar em seu site online, fazer uma compra na loja, ingressar em seu programa de fidelidade ou chamar um suporte técnico para nomear alguns. Nesses vários sistemas, há uma identidade criada para esse cliente e [!DNL Identity Service] possibilita unir essas identidades para ver a imagem completa.

Agora, em vez de cinco clientes separados interagindo com sua marca em cinco canais diferentes, você pode ver que esse é o mesmo cliente e pode garantir que eles recebam uma experiência consistente, personalizada e relevante em cada interação. À medida que mais informações são conhecidas sobre o cliente (por exemplo, um navegador anônimo do seu site decide se inscrever em uma conta e fazer logon), essas informações são reunidas e a imagem do cliente torna-se cada vez mais clara.

## Namespaces de identidade

Os namespaces de identidade são um componente do [!DNL Identity Service] e servir como indicadores que fornecem contexto adicional para as identidades do cliente. Um exemplo de um namespace de ID comumente usado seria &quot;Email&quot;, em que o uso do mesmo endereço de email em vários sites permite unir várias identidades diferentes, cada uma com uma ID de cliente exclusiva, como pertencente ao mesmo cliente. [!DNL Experience Platform] O permite usar namespaces de ID para procurar perfis individuais na interface do usuário. Para obter mais informações sobre a exibição de perfis, consulte o [visão geral da navegação no perfil](profile-browse.md). Para saber mais sobre os namespaces de identidade, consulte [visão geral do namespace de identidade](../../identity-service/namespaces.md).

## Gráficos de identidade

Um gráfico de identidade é um mapa de relacionamentos entre diferentes namespaces de identidade, fornecendo uma representação visual de como seu cliente interage com sua marca em diferentes canais. Todos os gráficos de identidade do cliente são gerenciados e atualizados coletivamente por [!DNL Identity Service] em tempo quase real, em resposta às atividades do cliente.

[!DNL Identity Service] O gerencia um gráfico de identidade visível somente pela sua organização e criado com base nos seus dados, conhecido como o gráfico privado. [!DNL Identity Service] aumenta seu gráfico privado quando um registro de dados assimilados contém mais de uma identidade, adicionando uma relação entre as identidades encontradas.

## Próximas etapas

As identidades e os relacionamentos entre elas são definidas e mantidas por [!DNL Identity Service] e aproveitado por [!DNL Real-Time Customer Profile] para criar uma imagem completa de cada cliente individual e suas interações. Para saber mais, visite o [Documentação do Serviço de identidade](../../identity-service/home.md).
