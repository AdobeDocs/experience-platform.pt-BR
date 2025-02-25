---
title: Interface de configurações de identidade
description: Saiba como usar a interface do usuário de configurações de identidade.
exl-id: 738b7617-706d-46e1-8e61-a34855ab976e
source-git-commit: 7c2e5cad997b7e7b9e0a08d3a3a1f5c9b218329e
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 4%

---

# Interface de configurações de identidade

>[!AVAILABILITY]
>
>As regras de vinculação do gráfico de identidade estão atualmente com Disponibilidade limitada. Entre em contato com a equipe de conta da Adobe para obter informações sobre como acessar o recurso em sandboxes de desenvolvimento.

As configurações de identidade são um recurso na interface do serviço de identidade da Adobe Experience Platform que pode ser usado para designar namespaces exclusivos e configurar a prioridade de namespace.

Leia este guia para saber como definir suas configurações de identidade na interface do usuário.

## Pré-requisitos

Leia os seguintes documentos antes de começar a trabalhar com configurações de identidade:

* [Regras de vinculação do gráfico de identidade](./overview.md)
* [Algoritmo de otimização de identidade](./identity-optimization-algorithm.md)
* [Guia de implementação](./implementation-guide.md)
* [Exemplos de configurações de gráfico](./example-configurations.md)
* [Prioridade de namespace](./namespace-priority.md)
* [Simulação de gráfico](./graph-simulation.md)

## Definir suas configurações de identidade

Para acessar as configurações de identidade, navegue até o espaço de trabalho Serviço de Identidade na interface do usuário do Adobe Experience Platform e selecione **[!UICONTROL Configurações]**.

![Botão de configurações de identidade selecionado.](../images/rules/identities-ui.png)

A página de configurações de identidade está dividida em duas seções: [!UICONTROL Namespaces de pessoa] e [!UICONTROL Namespaces de dispositivo ou cookie]. Os namespaces de pessoa são identificadores de indivíduos únicos. Eles podem ser IDs entre dispositivos, endereços de email e números de telefone. Os namespaces de dispositivo ou cookie são identificadores de dispositivos e navegadores da Web e não podem receber uma prioridade mais alta do que os namespaces de pessoa. Você também não pode designar um dispositivo ou namespace de cookie como um namespace exclusivo.

### Configurar prioridade de namespace

Para configurar a prioridade de namespace, selecione um namespace no menu de configurações de identidade e arraste e solte esse namespace na ordem de sua preferência. Coloque um namespace mais alto na lista para dar a ele uma prioridade mais alta e, inversamente, coloque um namespace mais baixo na lista para dar a ele uma prioridade mais baixa. O namespace com a maior prioridade também deve ser designado como um namespace exclusivo.

![O espaço de trabalho de configurações de identidades com um namespace de pessoa realçado.](../images/rules/namespace-priority.png)

### Designar seu namespace exclusivo

Para designar um namespace exclusivo, marque a caixa de seleção [!UICONTROL Exclusivo por gráfico] que corresponde a esse namespace. Você pode selecionar até três namespaces exclusivos para suas configurações de identidade.

![Dois namespaces selecionados e definidos como exclusivos.](../images/rules/unique-namespace.png)

Depois que os namespaces exclusivos forem estabelecidos, os gráficos não poderão mais ter várias identidades que contenham um namespace exclusivo. Por exemplo, se você designou o CRMID como um namespace exclusivo, um gráfico só poderá ter uma identidade com o namespace CRMID. Para obter mais informações, leia a [visão geral do algoritmo de otimização de identidade](./identity-optimization-algorithm.md#unique-namespace).

Quando você terminar as configurações, selecione **[!UICONTROL Avançar]**. Uma mensagem de confirmação é exibida. Use esta oportunidade para verificar se as configurações estão corretas e selecione **[!UICONTROL Concluir]**.

![Página de validação com Término realçada.](../images/rules/finish.png)

Uma mensagem de aviso é exibida, indicando que os gráficos existentes só serão afetados pelo algoritmo do gráfico se forem atualizados **depois de salvar suas configurações**, e que a identidade principal dos fragmentos de evento no Perfil de cliente em tempo real não será atualizada mesmo após as alterações de prioridade do namespace. Além disso, você receberá uma notificação de que levará até **seis horas** para que suas configurações novas ou atualizadas entrem em vigor. Para confirmar, digite o nome da sua sandbox e selecione **[!UICONTROL Confirmar]**.

![A janela de confirmação que exibe um aviso de atraso de cerca de seis horas antes que as configurações sejam processadas.](../images/rules/confirm-settings.png)

## Próximas etapas

Para obter mais informações sobre regras de vinculação de gráficos de identidade, leia a seguinte documentação:

* [Visão geral das regras de vinculação do gráfico de identidade](./overview.md)
* [Algoritmo de otimização de identidade](./identity-optimization-algorithm.md)
* [Guia de implementação](./implementation-guide.md)
* [Exemplos de configurações de gráfico](./example-configurations.md)
* [Solução de problemas e perguntas frequentes](./troubleshooting.md)
* [Prioridade de namespace](./namespace-priority.md)
* [Interface de simulação de gráfico](./graph-simulation.md)