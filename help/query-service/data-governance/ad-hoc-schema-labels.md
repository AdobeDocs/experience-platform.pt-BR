---
title: Suporte de controle de acesso baseado em atributos para esquemas ad hoc
description: Um guia para restringir o acesso a campos de dados em esquemas ad hoc gerados pelo Serviço de consulta da Adobe Experience Platform.
exl-id: d675e3de-ab62-4beb-9360-1f6090397a17
source-git-commit: f129c215ebc5dc169b9a7ef9b3faa3463ab413f3
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 2%

---

# Suporte de controle de acesso baseado em atributos para esquemas ad hoc

Quaisquer dados trazidos para o Adobe Experience Platform são encapsulados por esquemas do Experience Data Model (XDM) e podem estar sujeitos a restrições de uso definidas por sua organização ou por regulamentos legais.

Executando uma consulta CTAS por meio do Serviço de consulta quando nenhum esquema é especificado, um esquema ad hoc é gerado automaticamente. Muitas vezes, é necessário restringir o uso de determinados campos, ou conjuntos de dados, de esquemas ad hoc para controlar o acesso a dados pessoais confidenciais e a informações de identificação pessoal. O Adobe Experience Platform facilita esse controle de acesso permitindo rotular campos de esquema por meio da interface do usuário do Experience Platform usando o recurso de controle de acesso baseado em atributos.

Os rótulos podem ser aplicados a qualquer momento, proporcionando flexibilidade na maneira como você escolhe controlar os dados. Embora, seja uma prática recomendada rotular os dados assim que eles forem assimilados na Experience Platform ou assim que estiverem disponíveis para uso no Experience Platform.

A rotulagem baseada em esquema é um componente importante do controle de acesso baseado em atributos para gerenciar melhor o acesso fornecido a usuários ou grupos de usuários. O Adobe Experience Platform permite restringir o acesso a qualquer campo de um esquema ad hoc criando e aplicando rótulos.

Este documento fornece um tutorial para gerenciar o acesso a dados confidenciais aplicando rótulos a campos de dados de esquemas ad hoc gerados por meio do Serviço de consulta.

## Introdução

Este manual necessita de uma compreensão funcional dos seguintes componentes da Adobe Experience Platform:

* [Sistema do Experience Data Model (XDM)](../../xdm/home.md): a estrutura padronizada pela qual a Experience Platform organiza os dados de experiência do cliente.
   * [[!DNL Schema Editor]](../../xdm/ui/overview.md): Saiba como criar e gerenciar esquemas e outros recursos na interface do Experience Platform.
* [[!DNL Data Governance]](../../data-governance/home.md): saiba como o [!DNL Data Governance] permite gerenciar dados de clientes e garantir a conformidade com regulamentos, restrições e políticas aplicáveis ao uso de dados.
* [Controle de acesso baseado em atributos](../../access-control/abac/overview.md): o controle de acesso baseado em atributos é um recurso da Adobe Experience Platform que permite aos administradores controlar o acesso a objetos e/ou recursos específicos com base em atributos. Os atributos podem ser metadados adicionados a um objeto, como um rótulo adicionado a um campo de esquema ad hoc ou regular. Um administrador define políticas de acesso que incluem atributos para gerenciar permissões de acesso do usuário.

## Criar um esquema ad hoc

Depois que a consulta for executada e os resultados forem gerados, um esquema ad hoc será gerado automaticamente e adicionado ao inventário do esquema.

Para adicionar um rótulo de dados, navegue até a guia [!UICONTROL Esquemas] do painel de navegação selecionando [!UICONTROL Esquemas] no painel esquerdo da interface do Experience Platform. O inventário do esquema é exibido.

>[!NOTE]
>
>Esquemas ad hoc não são exibidos por padrão no inventário de esquemas.

## Descobrir esquemas ad hoc no inventário de esquemas da interface do usuário do Experience Platform {#discover-ad-hoc-schemas}

Para habilitar a exibição de esquemas ad hoc na interface do usuário do Experience Platform, selecione o ícone de filtro (![Um ícone de filtro.](/help/images/icons/filter.png)) à esquerda do campo de pesquisa e selecione **[!UICONTROL Mostrar esquemas adhoc] no painel esquerdo exibido.

![As opções de filtro do painel Esquema ficaram com a opção &#39;Mostrar esquema adhoc&#39; habilitada.](../images/data-governance/adhoc-schema-toggle.png)

Selecione o nome do esquema ad hoc criado recentemente na lista disponível. Uma visualização da estrutura do schema ad hoc é exibida.

![O exemplo de diagrama de estrutura de esquema ad hoc.](../images/data-governance/adhoc-schema-structure-diagram.png)

## Editar rótulos de governança

Para editar rótulos de dados para o esquema ad hoc, selecione a guia [!UICONTROL Rótulos]. O espaço de trabalho de rótulos permite aplicar, criar e editar rótulos para seus campos de esquema ad hoc e controlar permissões de acesso por meio da interface. Todos os campos no esquema ad hoc são representados aqui.

## Editar rótulos para o esquema ou campo

Para editar os rótulos de todo o esquema, selecione o ícone de lápis (![Um ícone de lápis.](/help/images/icons/edit.png)) ao lado do nome do esquema na guia [!UICONTROL Rótulos].

![A exibição de rótulos no espaço de trabalho de esquemas com o ícone de lápis realçado.](../images/data-governance/edit-entire-schema-labels.png)

Para aplicar um rótulo a um campo existente, selecione um ou mais campos na lista seguida por [!UICONTROL Editar rótulos de governança] na barra lateral direita.

![A exibição de rótulos no espaço de trabalho de esquemas com a opção &#39;Editar rótulos de governança&#39; realçada na barra lateral direita.](../images/data-governance/edit-governance-labels.png)

## Popover Editar rótulos

O popover [!UICONTROL Editar rótulos] é exibido. Nesta visualização, é possível criar ou editar rótulos de governança existentes por meio da interface do usuário.

![Popover Editar rótulos.](../images/data-governance/edit-labels-popover.png)

Consulte a documentação para obter orientação sobre como [criar ou editar rótulos para o esquema ou campo selecionado](../../xdm/tutorials/labels.md#edit-the-labels-for-the-schema-or-field).

>[!NOTE]
>
>Criar um novo rótulo ou editar um rótulo existente requer permissões de administrador para sua organização. Se você não tiver privilégios de administrador, entre em contato com o administrador do sistema para obter acesso.

Rótulos também podem ser criados usando o espaço de trabalho de permissões. Consulte o [guia sobre criação de rótulos no espaço de trabalho de permissões](../../access-control/abac/ui/labels.md) para obter instruções.

Depois que o nível apropriado de controle de acesso baseado em atributos for aplicado, o seguinte comportamento do sistema será aplicado a qualquer consulta executada por meio do Serviço de consulta quando um usuário tentar acessar dados não acessíveis:

1. Se um usuário tiver o acesso recusado a um dos campos em um esquema, ele não poderá ler ou gravar no campo restrito. Isso se aplica aos seguintes cenários comuns:

   * Quando um usuário tenta executar uma consulta somente com uma coluna restrita, o sistema emite um erro de que a coluna não existe.
   * Quando um usuário tenta executar uma consulta com várias colunas que incluem uma coluna restrita, o sistema retornará a saída somente para todas as colunas não restritas.

1. Se um usuário solicitar acesso a um campo calculado, será necessário ter acesso a todos os campos usados na composição ou o sistema negará acesso ao campo calculado.

Se uma identidade ou identidade primária for definida no esquema ad hoc, o sistema atenderá automaticamente a todas as solicitações de higiene de dados associadas e limpará os dados nesses conjuntos de dados vinculados à coluna de identidade.

## Próximas etapas

Depois de ler este documento, você compreenderá melhor como adicionar rótulos de uso de dados a esquemas ad hoc criados por meio de consultas CTAS do Serviço de consulta. Se ainda não tiver feito isso, os seguintes documentos são úteis para melhorar a sua compreensão da governança de dados no Serviço de consulta:

* [Identidades de esquema ad hoc](./ad-hoc-schema-identities.md)
* [Governança de dados](../../data-governance/home.md)
