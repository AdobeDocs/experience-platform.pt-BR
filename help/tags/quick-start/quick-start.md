---
title: Manual de início rápido
description: Saiba como começar a usar tags rapidamente no Adobe Experience Platform.
source-git-commit: 010e05968f1d7ad5675b0f0af43d9cfcc1f3a2ff
workflow-type: tm+mt
source-wordcount: '1532'
ht-degree: 42%

---

# Manual de início rápido

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Tags são a próxima geração da tecnologia de gerenciamento de tags da Adobe Experience Platform. Ele foi criado desde o começo para oferecer suporte a um ecossistema aberto e sustentável, onde qualquer pessoa pode criar suas próprias integrações que os clientes do Adobe podem implantar nos sites. É um aplicativo de API First, portanto, tudo o que pode ser feito por meio da interface do usuário também pode ser feito por meio de uma API.

O fluxo de trabalho básico das tags:

1. Configurar grupos e usuários.
2. Fazer logon.
3. Criar uma propriedade.
4. Instalar extensões.
5. Criar elementos de dados e regras.
6. Testar em seu ambiente de desenvolvimento.
7. Promover para produção.

## 1. Configurar grupos e usuários

Tags são totalmente integradas ao seu Adobe ID. As permissões do usuário são gerenciadas por meio do Admin Console com outros produtos e soluções Adobe do [!DNL Creative Cloud], [!DNL Document Cloud] e do Experience Cloud.

As tags têm um sistema de gerenciamento de usuários baseado em direitos. Isso significa que os direitos individuais devem ser explicitamente concedidos. Esses direitos são atribuídos a grupos, depois os usuários são adicionados aos grupos apropriados para obterem acesso. Mesmo que sua organização tenha acesso à interface do usuário da coleta de dados, os usuários individuais não poderão fazer nada até que um Administrador da organização conceda a eles alguns direitos explicitamente.

Para obter instruções detalhadas sobre como criar grupos e adicionar usuários para tags, consulte o documento [permissões do usuário](../ui/administration/user-permissions.md).

## 2. Fazer logon

Após adicionar os direitos de tag à Adobe ID, é necessário fazer logon na interface do usuário da coleta de dados. Você pode fazer isso navegando diretamente para a [tela de logon do Experience Cloud](https://experiencecloud.adobe.com) e selecionando a interface do usuário da coleta de dados na guia Acesso rápido .

>[!NOTE]
>
>Se você tiver uma única conta com direitos para várias organizações, a organização poderá ser alterada selecionando o nome da organização na barra de controle na parte superior da tela e escolhendo uma organização diferente da lista suspensa.

## 3. Criar uma propriedade

Depois de fazer logon na interface do usuário da coleta de dados, a primeira coisa a fazer é criar uma propriedade. Basicamente, uma propriedade é basicamente um container que você preenche com extensões, regras, elementos de dados e bibliotecas à medida que implanta tags no site. Muitas pessoas criam uma propriedade para cada site (ou grupo de sites intimamente relacionados) em que desejam implantar o mesmo conjunto de tags.

Para obter mais informações sobre a criação de propriedades, consulte [Criar uma propriedade](../ui/administration/companies-and-properties.md).

## 4. Instalar extensões

Uma extensão é uma integração criada pelo Adobe ou por um parceiro de Adobe que adiciona opções novas e infinitas para as tags que você pode implantar nos sites. Se você pensar em uma tag como um sistema operacional, as extensões são os aplicativos que você instala para fazer o que precisa fazer.

Todas as novas propriedades são fornecidas com a [Extensão principal](../extensions/web/core/overview.md) instalada. As propriedades móveis são fornecidas com extensões adicionais. A extensão principal é criada pelo Adobe para fornecer um conjunto padrão robusto de tipos de elementos de dados para a camada de dados e tipos de evento para as regras. A maioria das ações que você desejará executar (obter uma ECID, enviar beacons do [!DNL Adobe Analytics], carregar a mbox global do [!DNL Target], etc.) será proveniente de extensões instaladas no catálogo.

O que torna as tags na Platform realmente exclusivas é que essas extensões podem ser criadas por qualquer pessoa. Você precisa soltar um pixel de remarketing do Facebook em seu site? Confira a extensão que o Facebook criou. Deseja o mesmo para Twitter ou Linked In? Use essas extensões. Você precisa executar uma pesquisa? Veja o Question Pro ou Foresee. Você precisa gerenciar a privacidade e o consentimento dos usuários finais para ajudar com [!DNL GDPR]? Dê uma boa olhada no Evidon e no Trust Arc. Deseja ver um insight granular sobre o comportamento de usuários individuais no site? Talvez você deva dar uma olhada no Clicktale. Para obter mais informações, consulte a seção sobre [adicionar uma nova extensão](../ui/managing-resources/extensions/overview.md#add-a-new-extension).

## 5. Criar elementos de dados e regras

Os **elementos de dados** são indicadores para as informações que você deseja coletar e enviar para diferentes locais na sua página:

* Uma camada de dados definida no JSON
* Elementos de DOM
* Cookies
* Sessão e armazenamento local
* Praticamente tudo mais

Depois que o elemento de dados é definido, você pode usá-lo em qualquer lugar na interface do usuário da coleta de dados para qualquer extensão. Consulte a documentação em [Elementos de dados](../ui/managing-resources/data-elements.md) para obter informações mais detalhadas.

As **regras** representam a essência lógica da implementação e controlam o que, quando, onde e como de todas as tags do site. Defina um evento, ajuste as condições e exceções, então defina as ações e a ordem. Por último, publique suas alterações para ver os resultados. Para obter mais informações, consulte [Regras](../ui/managing-resources/rules.md).

## 6. Testar em seu ambiente de desenvolvimento

### Bibliotecas e criações

As builds de tags nunca são publicadas automaticamente. Cada conjunto de alterações efetuadas é encapsulado em uma [biblioteca](../ui/publishing/libraries.md). Cada biblioteca criada automaticamente herda tudo a montante (publicações, aprovações ou envios) como uma linha de base; portanto, basta definir as alterações que deseja fazer. Essa biblioteca serve de blueprint para uma [criação](../ui/publishing/builds.md). Uma criação é o conjunto real de arquivos JavaScript implantados e utilizados.

É importante entender a relação entre a página da Web, o local de hospedagem e as tags.

1. O servidor de host fornece um local para publicar a build. A própria build contém os arquivos JavaScript necessários para a biblioteca.

   Cada ambiente tem uma relação com um host e ele fornece um terminal indicando onde fornecer a criação. O host pode pertencer a apenas uma propriedade, embora uma propriedade possa ter muitos hosts.

2. Um código incorporado é fornecido na tag `<script>` do formulário que vai para as seções `<head>` do HTML do site.

   Ao criar um ambiente e anexar um host, o ambiente gera automaticamente um código integrado exclusivo que permite integrar a build atribuída ao site. O código `<script>` é usado para implantar a build da biblioteca no tempo de execução.

3. Quando um usuário navega em seu site, a tag `<script>` do código de incorporação recupera a criação do servidor de host e executa as ações definidas no navegador.

### Hosts

Um host é uma conexão entre uma propriedade de tag e seu local de hospedagem. Atualmente, as tags são compatíveis com a hospedagem gerenciada pelo Adobe por meio de um host [!DNL Akamai] ou com a hospedagem própria por meio de um host SFTP. Sempre que você produz uma criação, as tags se conectam ao servidor definido pelo host e fornecem a criação.

Se você for auto-hospedagem, uma build de tag pode enviar diretamente para seus servidores por meio do SFTP ou você pode enviá-la para [!DNL Akamai] e baixá-la usando a opção Arquivamento do ambiente.

Para obter mais informações, consulte [Hosts](../ui/publishing/hosts/hosts-overview.md).

### Ambientes

Cada biblioteca é criada dentro de um ambiente. Um ambiente define a aparência desejada da sua criação quando ela for publicada. É possível especificar:

* **Host:** cada ambiente precisa de um host que determine o ponto de extremidade onde quaisquer builds criadas neste ambiente serão enviadas.
* **Arquivamento:** a configuração padrão é implantar sua build como um arquivo minified.js. Se você estiver usando o código personalizado, é possível ter vários arquivos que fazem referência uns aos outros. Eles podem ser combinados em um único arquivo zip e criptografados.

Após salvar o ambiente, ele gera o código de inserção que você pode copiar e colar no site. Observe que o código incorporado não funcionará até que você tenha criado uma biblioteca e produzido uma build. Para obter mais informações, consulte [Ambientes](../ui/publishing/environments.md).

### Publicar uma criação no Desenvolvimento

O processo de publicação é descrito nas etapas abaixo.

1. Crie um host.
1. Criar um ambiente de desenvolvimento usando o host que você criou.
1. Implantar o código de inserção do ambiente de desenvolvimento no site de teste de desenvolvimento.
1. Criar uma biblioteca e atribui-la ao ambiente de desenvolvimento que você criou.
1. Criar sua biblioteca.

## 7. Promover para produção

Depois de testar a build no ambiente de desenvolvimento, crie os ambientes de preparo e produção e coloque os códigos incorporados nos locais necessários. Você pode reutilizar hosts existentes para essa finalidade.

Promover uma biblioteca até a produção normalmente requer coordenação entre diferentes pessoas com os direitos apropriados.

* Um Desenvolvedor (alguém com o direito de Desenvolver) envia a biblioteca, que muda a biblioteca para o estado Enviado.
* Um Aprovador (alguém com o direito de Aprovar) pode criar a biblioteca para o ambiente de armazenamento temporário e aprová-la após testar. Essa ação muda a biblioteca para o estado aprovado. Somente uma biblioteca pode ser enviada e aprovada de cada vez.
* Um Editor (alguém com o direito de Publicar) pode criar a biblioteca para o ambiente de produção.

Você pode atribuir todos esses direitos a uma única pessoa.

Para obter mais informações sobre os diferentes estados e opções disponíveis durante o processo de publicação, consulte [Fluxo de trabalho de aprovação](../ui/publishing/publishing-flow.md).

## Recursos adicionais

Para saber mais sobre tags, consulte estes recursos:

* **[Comunidade](https://forums.adobe.com/community/experience-cloud/platform/launch)** de coleta de dados: Faça e responda perguntas, envie ideias e vote nas ideias de outras pessoas. Faça logon com a Adobe ID.
* **[Documentos](https://developer.adobelaunch.com/)** do desenvolvedor: envolva-se com a comunidade do desenvolvedor de tags para criar extensões ou usar as APIs de tags
* **[Visão geral](https://experienceleague.adobe.com/docs/launch-learn/tutorials/overview.html?lang=pt-BR)** do Tutorials: Esses documentos apresentam a você conceitos de tags, incluindo encaminhamento de eventos e SDK móvel em aplicativos Android.
