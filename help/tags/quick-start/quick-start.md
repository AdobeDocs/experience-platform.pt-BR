---
title: Manual de início rápido
description: Saiba como começar a usar as tags na Adobe Experience Platform.
exl-id: 490ee344-3b18-4189-9293-2378f86fb10d
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1473'
ht-degree: 88%

---

# Manual de início rápido

As tags são a próxima geração da tecnologia de gerenciamento de tags da Adobe Experience Platform. Elas foram criadas do zero para dar suporte a um ecossistema aberto e sustentável, em que qualquer pessoa pode criar suas próprias integrações, que os clientes da Adobe poderão implantar em seus sites. É um aplicativo de API First, portanto, tudo o que pode ser feito por meio da interface do usuário também pode ser feito por meio de uma API.

O fluxo de trabalho básico das tags é:

1. Configurar grupos e usuários.
2. Fazer logon.
3. Criar uma propriedade.
4. Instalar extensões.
5. Criar elementos de dados e regras.
6. Testar em seu ambiente de desenvolvimento.
7. Promover para produção.

## &#x200B;1. Configurar grupos e usuários

As tags são totalmente integradas a seu Adobe ID. As permissões do usuário são gerenciadas por meio do Admin Console com outros produtos e soluções da Adobe presentes na [!DNL Creative Cloud], [!DNL Document Cloud] e na Experience Cloud.

As tags têm um sistema de gerenciamento de usuários baseado em direitos. Isso significa que os direitos individuais devem ser explicitamente concedidos. Esses direitos são atribuídos a grupos, depois os usuários são adicionados aos grupos apropriados para obterem acesso. Mesmo que sua organização tenha acesso à Coleção de dados, os usuários individuais não poderão fazer nada até que um administrador conceda a eles alguns direitos explicitamente.

Para obter instruções detalhadas sobre como criar grupos e adicionar usuários para tags, consulte o [guia de permissões de coleta de dados](../../collection/permissions.md).

## &#x200B;2. Fazer logon

Após adicionar os direitos de tag à Adobe ID, é necessário fazer logon na interface do usuário da Experience Platform ou na interface da Coleção de dados. Você pode fazer isso navegando diretamente para a [tela de logon do Experience Cloud](https://experience.adobe.com/) e selecionando **[!UICONTROL Data Collection]** ou **[!UICONTROL Experience Platform]**.

>[!NOTE]
>
>Se você tiver uma única conta com direitos para várias organizações, para alterar a organização, selecione o nome dela na barra de controle na parte superior da tela e escolha outra organização na lista suspensa.

## &#x200B;3. Criar uma propriedade

Depois de fazer logon na interface do usuário, a primeira ação a ser executada é criar uma propriedade. Basicamente, uma propriedade é basicamente um container que você preenche com extensões, regras, elementos de dados e bibliotecas à medida que implanta tags no site. Muitas pessoas criam uma propriedade para cada site (ou grupo de sites intimamente relacionados) em que desejam implantar o mesmo conjunto de tags.

Para obter mais informações sobre a criação de propriedades, consulte [Criar uma propriedade](../ui/administration/companies-and-properties.md).

## &#x200B;4. Instalar extensões

Uma extensão é uma integração criada pela Adobe ou por um parceiro da Adobe que adiciona opções novas e infinitas às tags que podem ser implantadas em seus sites. Comparando a tag a um sistema operacional, as extensões são os aplicativos que você instala para executar ações específicas necessárias.

Todas as novas propriedades são fornecidas com a [Extensão principal](../extensions/client/core/overview.md) instalada. As propriedades móveis são fornecidas com extensões adicionais. A extensão principal é criada pela equipe da Adobe a fim de fornecer um conjunto padrão robusto de tipos de elemento de dados para sua camada de dados e tipos de evento para suas regras. A maioria das ações que você desejará executar (obter uma ECID, enviar beacons do [!DNL Adobe Analytics], carregar a mbox global do [!DNL Target], etc.) será proveniente de extensões instaladas no catálogo.

O que torna as tags na Experience Platform realmente únicas é que essas extensões podem ser criadas por qualquer pessoa. Você precisa soltar um pixel de remarketing do Facebook em seu site? Confira a extensão que o Facebook criou. Deseja o mesmo para Twitter ou Linked In? Use essas extensões. Você precisa executar uma pesquisa? Veja o Question Pro ou Foresee. Você precisa gerenciar a privacidade e o consentimento dos usuários finais para ajudar no [!DNL GDPR]? Dê uma boa olhada no Evidon e no Trust Arc. Deseja obter uma visão detalhada do comportamento de usuários individuais no site? Talvez você deva dar uma olhada no Clicktale. Para obter mais informações, consulte a seção sobre [adição de uma nova extensão](../ui/managing-resources/extensions/overview.md#add-a-new-extension).

## &#x200B;5. Criar elementos de dados e regras

Os **elementos de dados** são indicadores para as informações que você deseja coletar e enviar para diferentes locais na sua página:

* Uma camada de dados definida no JSON
* Elementos de DOM
* Cookies
* Sessão e armazenamento local
* Praticamente tudo mais

Depois que o elemento de dados é definido, você pode usá-lo em qualquer lugar da interface do para qualquer extensão. Consulte a documentação sobre [Elementos de dados](../ui/managing-resources/data-elements.md) para obter informações mais detalhadas.

As **regras** representam a essência lógica da implementação e controlam o que, quando, onde e como de todas as tags do site. Defina um evento, ajuste as condições e exceções, então defina as ações e a ordem. Por último, publique suas alterações para ver os resultados. Para obter mais informações, consulte [Regras](../ui/managing-resources/rules.md).

## &#x200B;6. Testar em seu ambiente de desenvolvimento

### Bibliotecas e criações

As tags criadas não são publicadas automaticamente. Cada conjunto de alterações efetuadas é encapsulado em uma [biblioteca](../ui/publishing/libraries.md). Cada biblioteca criada automaticamente herda tudo a montante (publicações, aprovações ou envios) como uma linha de base; portanto, basta definir as alterações que deseja fazer. Essa biblioteca serve de blueprint para uma [criação](../ui/publishing/builds.md). Uma criação é o conjunto real de arquivos JavaScript implantados e utilizados.

É importante entender a relação entre a página da Web, o local de hospedagem e as tags.

1. O servidor de host fornece um local para publicar o build. O próprio build contém os arquivos JavaScript necessários à biblioteca.

   Cada ambiente tem uma relação com um host, o qual fornece um endpoint para indicar onde o build deve ser entregue. O host pode pertencer a apenas uma propriedade, embora ela possa ter muitos hosts.

2. Um código incorporado é fornecido na tag `<script>` do formulário que vai para as seções `<head>` do HTML do site.

   Quando você cria um ambiente e anexa um host, o ambiente gera automaticamente um código incorporado exclusivo que permite integrar o build atribuído ao site. O código `<script>` é usado para implantar o build da biblioteca no tempo de execução.

3. Quando um usuário navega em seu site, a tag `<script>` do código incorporado recupera o build do servidor de host e executa as ações definidas pelo navegador.

### Hosts

Um host é uma conexão entre uma propriedade de tag e seu local de hospedagem. Atualmente, as tags são compatíveis com a hospedagem gerenciada da Adobe por meio de um host [!DNL Akamai] ou com a hospedagem própria por meio de um host SFTP. Sempre que você produz um build, as tags se conectam ao servidor definido pelo host e o build é entregue.

Se você estiver usando a auto-hospedagem, um build de tag poderá enviar diretamente a seus servidores por meio de SFTP ou você poderá enviar ao [!DNL Akamai] e baixar usando a opção Arquivar do ambiente.

Para obter mais informações, consulte [Hosts](../ui/publishing/hosts/hosts-overview.md).

### Ambientes

Cada biblioteca é criada dentro de um ambiente. Um ambiente define a aparência desejada da sua criação quando ela for publicada. É possível especificar:

* **Host:** cada ambiente precisa de um host que determine o endpoint para o qual os builds criados nesse ambiente serão enviados.
* **Arquivar:** na configuração padrão, o build é implantado como um arquivo .js minimizado. Se estiver usando código personalizado, você poderá ter vários arquivos que fazem referência uns aos outros. Eles podem ser combinados em um único arquivo compactado e criptografado.

Após salvar o ambiente, ele gera o código incorporado que você pode copiar e colar no site. Observe que o código incorporado não funcionará até que você tenha criado uma biblioteca e produzido um build. Para obter mais informações, consulte [Ambientes](../ui/publishing/environments.md).

### Publicar uma criação no Desenvolvimento

O processo de publicação está descrito nas etapas abaixo.

1. Criar um host.
1. Criar um ambiente de desenvolvimento usando o host que você criou.
1. Implantar o código incorporado do ambiente de desenvolvimento no site de teste de desenvolvimento.
1. Criar uma biblioteca e atribui-la ao ambiente de desenvolvimento que você criou.
1. Criar sua biblioteca.

## &#x200B;7. Promover para produção

Depois de testar o build no ambiente de desenvolvimento, crie os ambientes de preparo e de produção e coloque os códigos integrados nos locais necessários. Você pode reutilizar hosts existentes para essa finalidade.

Promover uma biblioteca até a produção normalmente requer coordenação entre diferentes pessoas com os direitos apropriados.

* Um Desenvolvedor (alguém com o direito de Desenvolver) envia a biblioteca, que muda a biblioteca para o estado Enviado.
* Um Aprovador (alguém com o direito de Aprovar) pode criar a biblioteca para o ambiente de armazenamento temporário e aprová-la após testar. Essa ação muda a biblioteca para o estado aprovado. Somente uma biblioteca pode ser enviada e aprovada de cada vez.
* Um Editor (alguém com o direito de Publicar) pode criar a biblioteca para o ambiente de produção.

Você pode atribuir todos esses direitos a uma única pessoa.

Para obter mais informações sobre os diferentes estados e opções disponíveis durante o processo de publicação, consulte [Fluxo de trabalho de aprovação](../ui/publishing/publishing-flow.md).

## Recursos adicionais

Para saber mais sobre tags, consulte estes recursos:

* **[Comunidade da Coleção de dados](https://experienceleaguecommunities.adobe.com/t5/adobe-experience-platform-data/ct-p/adobe-launch-community?profile.language=pt)**: faça e responda perguntas, envie ideias e vote nas ideias de outras pessoas. Faça logon com seu Adobe ID.
* **[Documentos do desenvolvedor](../api/overview.md)**: envolva-se com a comunidade do desenvolvedor de tags para criar extensões ou usar as APIs de tags
* **[Visão geral dos tutoriais](https://experienceleague.adobe.com/docs/launch-learn/tutorials/overview.html?lang=pt-BR)**: esses documentos apresentam conceitos de tags, incluindo encaminhamento de eventos e SDK móvel em aplicativos Android.
