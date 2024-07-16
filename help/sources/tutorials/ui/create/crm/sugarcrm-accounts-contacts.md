---
title: Criar uma conexão de origem de Contas e Contatos do SugarCRM na interface
description: Saiba como criar uma conexão de origem de Contas e Contatos do SugarCRM usando a interface do Adobe Experience Platform.
exl-id: 45840d7e-4c19-4720-8629-be446347862d
source-git-commit: 0de4b32ac2ddc90dabefd469b6658388a4532e0d
workflow-type: tm+mt
source-wordcount: '764'
ht-degree: 2%

---

# Criar uma conexão de origem [!DNL SugarCRM Accounts & Contacts] na interface

Este tutorial fornece etapas para criar uma conexão de origem [!DNL SugarCRM Accounts & Contacts] usando a interface do usuário do Adobe Experience Platform.

## Introdução

Este tutorial requer um entendimento prático dos seguintes componentes do Experience Platform:

* [[!DNL Experience Data Model (XDM)] Sistema](../../../../../xdm/home.md): a estrutura padronizada pela qual o [!DNL Experience Platform] organiza os dados de experiência do cliente.
   * [Noções básicas sobre a composição de esquema](../../../../../xdm/schema/composition.md): saiba mais sobre os blocos de construção básicos de esquemas XDM, incluindo princípios-chave e práticas recomendadas na composição de esquema.
   * [Tutorial do Editor de esquemas](../../../../../xdm/tutorials/create-schema-ui.md): saiba como criar esquemas personalizados usando a interface do Editor de esquemas.
* [[!DNL Real-Time Customer Profile]](../../../../../profile/home.md): Fornece um perfil de consumidor unificado em tempo real com base em dados agregados de várias fontes.

Se você já tiver uma conta válida do [!DNL SugarCRM], ignore o restante deste documento e prossiga para o tutorial em [configurando um fluxo de dados](../../dataflow/crm.md).

### Coletar credenciais necessárias

Para conectar [!DNL SugarCRM Accounts & Contacts] à Platform, você deve fornecer valores para as seguintes propriedades de conexão:

| Credencial | Descrição | Exemplo |
| --- | --- | --- |
| `Host` | O ponto de extremidade da API do SugarCRM ao qual a origem se conecta. | `developer.salesfusion.com` |
| `Username` | Seu nome de usuário da conta de desenvolvedor do SugarCRM. | `abc.def@example.com@sugarmarketdemo000.com` |
| `Password` | A senha da sua conta de desenvolvedor do SugarCRM. | `123456789` |

### Criar um esquema da Platform

Antes de criar uma conexão de origem do [!DNL SugarCRM], você também deve garantir que primeiro crie um esquema da Platform para usar em sua origem. Consulte o tutorial sobre [criação de um esquema da Platform](../../../../../xdm/schema/composition.md) para obter etapas abrangentes sobre como criar um esquema.

O [!DNL SugarCRM Accounts & Contacts] dá suporte a várias APIs. Isso significa que é necessário criar um esquema separado, dependendo do tipo de objeto que você está utilizando. Consulte os exemplos abaixo para os esquemas de contas e contatos:

>[!BEGINTABS]

>[!TAB Contas]

![Captura de tela da interface da plataforma mostrando um exemplo de esquema para Contas](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-accounts.png)

>[!TAB Contatos]

![Captura de tela da Interface do Usuário da Plataforma mostrando um exemplo de esquema para Contatos](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarcrm-schema-contacts.png)

>[!ENDTABS]

## Conectar sua conta do [!DNL SugarCRM Accounts & Contacts]

Na interface da Platform, selecione **[!UICONTROL Fontes]** na barra de navegação esquerda para acessar o espaço de trabalho [!UICONTROL Fontes]. A tela [!UICONTROL Catálogo] exibe uma variedade de fontes com as quais você pode criar uma conta.

Você pode selecionar a categoria apropriada no catálogo no lado esquerdo da tela. Como alternativa, você pode encontrar a fonte específica com a qual deseja trabalhar usando a opção de pesquisa.

Na categoria *CRM*, selecione **[!UICONTROL Contas e Contatos do SugarCRM]** e **[!UICONTROL Adicionar dados]**.

![Captura de tela da interface da plataforma para catálogo com o cartão Contas e Contatos do SugarCRM](../../../../images/tutorials/create/sugarcrm-accounts-contacts/catalog-sugarcrm-accounts-contacts.png)

A página **[!UICONTROL Conectar Contas e Contatos do SugarCRM]** é exibida. Nesta página, você pode usar credenciais novas ou existentes.

### Conta existente

Para usar uma conta existente, selecione a conta [!DNL SugarCRM Accounts & Contacts] com a qual deseja criar um novo fluxo de dados e clique em **[!UICONTROL Avançar]** para continuar.

![Captura de tela da interface do usuário da plataforma para contas e contatos do Connect SugarCRM com uma conta existente](../../../../images/tutorials/create/sugarcrm-accounts-contacts/existing.png)

### Nova conta

Se você estiver criando uma nova conta, selecione **[!UICONTROL Nova conta]** e forneça um nome, uma descrição opcional e suas credenciais. Quando terminar, selecione **[!UICONTROL Conectar à origem]** e aguarde algum tempo para que a nova conexão seja estabelecida.

![Captura de tela da interface do usuário da plataforma para contas e contatos do Connect SugarCRM com uma nova conta](../../../../images/tutorials/create/sugarcrm-accounts-contacts/new.png)

### Selecionar dados

Finalmente, você deve selecionar o tipo de objeto que deseja assimilar na Platform.

| Tipo de objeto | Descrição |
| --- | --- |
| `Accounts` | As empresas com as quais sua organização tem um relacionamento. |
| `Contacts` | As pessoas individuais com as quais sua organização tem um relacionamento estabelecido. |

>[!BEGINTABS]

>[!TAB Contas]

![Captura de tela da interface do usuário da plataforma para contas e contatos do SugarCRM mostrando a configuração com a opção Conta selecionada](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-accounts.png)

>[!TAB Contatos]

![Captura de tela da interface do usuário da plataforma para contas e contatos do SugarCRM mostrando a configuração com a opção Contatos selecionada](../../../../images/tutorials/create/sugarcrm-accounts-contacts/configuration-contacts.png)

>[!ENDTABS]

## Próximas etapas

Seguindo este tutorial, você estabeleceu uma conexão com sua conta do [!DNL SugarCRM Accounts & Contacts]. Agora você pode seguir para o próximo tutorial e [configurar um fluxo de dados para trazer dados para a Platform](../../dataflow/crm.md).

## Recursos adicionais

As seções abaixo fornecem recursos adicionais que você pode consultar ao usar a origem [!DNL SugarCRM].

### Medidas de proteção {#guardrails}

As taxas de limitação da API [!DNL SugarCRM] são de 90 chamadas por minuto ou 2000 chamadas por dia, o que ocorrer primeiro. No entanto, essa restrição foi contornada adicionando um parâmetro na especificação da conexão que atrasará o tempo de solicitação para que o limite da taxa nunca seja atingido.

### Validação {#validation}

Para validar se você configurou corretamente a origem e se os dados de [!DNL SugarCRM Accounts & Contacts] estão sendo assimilados, siga as etapas abaixo:

* Na interface da Platform, selecione **[!UICONTROL Exibir Fluxos de Dados]** ao lado do menu de cartão [!DNL SugarCRM Accounts & Contacts] no catálogo de fontes. Em seguida, selecione **[!UICONTROL Visualizar conjunto de dados]** para verificar os dados que foram assimilados.

* Dependendo do tipo de objeto com o qual você está trabalhando, é possível verificar os dados agregados nas contas visíveis nas [!DNL SugarMarket] páginas Contas ou Contatos abaixo:

>[!BEGINTABS]

>[!TAB Contas]

![Captura de tela da página Contas do SugarMarket exibindo a lista de contas](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-accounts.png)

>[!TAB Contatos]

![Captura de tela da página Contatos do SugarMarket exibindo a lista de contatos](../../../../images/tutorials/create/sugarcrm-accounts-contacts/sugarmarket-contacts.png)

>[!ENDTABS]

>[!NOTE]
>
>As páginas [!DNL SugarMarket] não incluem as contagens de objetos excluídos. No entanto, os dados recuperados por meio dessa fonte também incluirão a contagem de excluídos, que seria marcada com um sinalizador excluído.
