---
title: Identidades e namespaces de identidade
seo-title: Adobe Experience Platform Identity Service
description: descrição
seo-description: descrição da sequência
translation-type: tm+mt
source-git-commit: 5cba5a1e8139dd85f23250d42a1cd8d2318eb916

---


# Identidades na CDP em tempo real

O Adobe Experience Platform Identity Service ajuda você a obter uma melhor visão de seus clientes e de seus comportamentos ao unir identidades entre dispositivos e sistemas. Geralmente, seus clientes interagem com sua marca em vários canais, isso pode incluir navegar em seu site online, fazer uma compra na loja, entrar em seu programa de fidelidade ou ligar para um suporte técnico para nomear alguns. Nesses vários sistemas, há uma identidade criada para esse cliente, e o Serviço de identidade permite reunir essas identidades para ver a imagem completa.

Agora, em vez de cinco clientes separados interagindo com sua marca em cinco canais diferentes, você pode ver que esse é o mesmo cliente, e você pode garantir que eles recebam uma experiência consistente, personalizada e relevante em cada interação. À medida que mais informações se tornam conhecidas sobre seu cliente (por exemplo, um navegador anônimo do seu site decide se inscrever para obter uma conta e fazer login), essas informações são agrupadas e a imagem do seu cliente se torna cada vez mais clara.

## Namespaces de identidade

Os namespaces de identidade são um componente do Serviço de identidade e servem como indicadores que fornecem contexto adicional às identidades do cliente. Um exemplo de um namespace de ID comumente usado seria &quot;Email&quot;, em que o uso do mesmo endereço de email em vários sites permite unir várias identidades diferentes, cada uma com uma ID única do cliente, como pertencente ao mesmo cliente. A Plataforma de experiência permite usar namespaces de ID para procurar perfis individuais na interface do usuário. Para obter mais informações sobre a exibição de perfis, consulte a visão geral [do visualizador de](/help/rtcdp/profile/profile-viewer.md)perfil. Para saber mais sobre namespaces de identidade, consulte a visão geral do namespace de [identidade em E/S](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_namespace_overview/identity_namespace_overview.md)da Adobe.

## Gráficos de identidade

Um gráfico de identidade é um mapa de relacionamentos entre diferentes namespaces de identidade, fornecendo uma representação visual de como o cliente interage com sua marca em diferentes canais. Todos os gráficos de identidade do cliente são gerenciados e atualizados coletivamente pelo Serviço de identidade em tempo quase real, em resposta à atividade do cliente.

O Serviço de identidade gerencia um gráfico de identidade visível somente pela sua organização e criado com base nos seus dados, conhecido como gráfico privado. O Serviço de identidade aumenta seu gráfico particular quando um registro de dados ingeridos contém mais de uma identidade, adicionando uma relação entre as identidades encontradas.

## Próximas etapas

As identidades e as relações entre elas são definidas e mantidas pelo Serviço de identidade e aproveitadas pelo Perfil do cliente em tempo real para criar uma visão completa de cada cliente individual e suas interações. Para saber mais, visite a documentação do Serviço de [identidade em E/S](https://www.adobe.io/apis/experienceplatform/home/profile-identity-segmentation/profile-identity-segmentation-services.html#!api-specification/markdown/narrative/technical_overview/identity_services_architectural_overview/identity_services_architectural_overview.md)da Adobe.