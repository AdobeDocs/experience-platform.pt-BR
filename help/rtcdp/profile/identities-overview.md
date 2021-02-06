---
keywords: identidades rtcdp;rtcdp identities;identidades cdp em tempo real
title: Identidades na plataforma de dados do cliente em tempo real
description: O Adobe Experience Platform Identity Service ajuda você a obter uma melhor visualização de seus clientes e de seu comportamento ao unir identidades entre dispositivos e sistemas.
translation-type: tm+mt
source-git-commit: 36f63cecd49e6a6b39367359d50252612ea16d7a
workflow-type: tm+mt
source-wordcount: '435'
ht-degree: 0%

---


# Identidades na plataforma de dados do cliente em tempo real

A Adobe Experience Platform [!DNL Identity Service] ajuda você a obter uma melhor visualização de seus clientes e de seus comportamentos ao unir identidades entre dispositivos e sistemas. Geralmente, seus clientes interagem com sua marca em vários canais, isso pode incluir a navegação online em seu site, a compra na loja, a entrada em seu programa de fidelidade ou a chamada de um suporte técnico para nomear alguns. Nesses vários sistemas, há uma identidade criada para esse cliente, e [!DNL Identity Service] permite reunir essas identidades para ver a imagem completa.

Agora, em vez de cinco clientes separados interagindo com sua marca em cinco canais diferentes, você pode ver que esse é o mesmo cliente, e você pode garantir que eles recebam uma experiência consistente, personalizada e relevante em cada interação. À medida que mais informações se tornam conhecidas sobre seu cliente (por exemplo, um navegador anônimo do seu site decide se inscrever para obter uma conta e fazer login), essas informações são agrupadas e a imagem do seu cliente se torna cada vez mais clara.

## Namespaces de identidade

As namespaces de identidade são um componente de [!DNL Identity Service] e servem como indicadores que fornecem contexto adicional às identidades do cliente. Um exemplo de uma namespace de ID comumente usada seria o &quot;Email&quot;, onde o uso do mesmo endereço de email em vários sites permite que você junte várias identidades diferentes, cada uma com uma ID de cliente exclusiva, como pertencente ao mesmo cliente. [!DNL Experience Platform] permite usar namespaces de ID para pesquisar perfis individuais na interface do usuário. Para obter mais informações sobre como visualizar perfis, consulte a [visão geral do visualizador do perfil](/help/rtcdp/profile/profile-viewer.md). Para saber mais sobre namespaces de identidade, consulte a [visão geral da namespace de identidade](../../identity-service/namespaces.md).

## Gráficos de identidade

Um gráfico de identidade é um mapa de relações entre diferentes namespaces de identidade, fornecendo uma representação visual de como seu cliente interage com sua marca em diferentes canais. Todos os gráficos de identidade do cliente são gerenciados coletivamente e atualizados por [!DNL Identity Service] em tempo quase real, em resposta à atividade do cliente.

[!DNL Identity Service] gerencia um gráfico de identidade visível somente pela sua organização e criado com base em seus dados, conhecido como gráfico privado. [!DNL Identity Service] aumenta seu gráfico particular quando um registro de dados assimilados contém mais de uma identidade, adicionando uma relação entre as identidades encontradas.

## Próximas etapas

As identidades e as relações entre elas são definidas e mantidas por [!DNL Identity Service] e aproveitadas por [!DNL Real-time Customer Profile] para criar uma visão completa de cada cliente individual e suas interações. Para saber mais, visite a [documentação do Serviço de Identidade](../../identity-service/home.md).