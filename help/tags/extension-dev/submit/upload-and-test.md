---
title: Fazer upload e implementar testes completos para uma extensão
description: Saiba como validar, carregar e testar a extensão na Adobe Experience Platform.
exl-id: 6176a9e1-fa06-447e-a080-42a67826ed9e
source-git-commit: 1b507e9846a74b7ac2d046c89fd7c27a818035ba
workflow-type: tm+mt
source-wordcount: '2344'
ht-degree: 84%

---

# Fazer upload e implementar testes completos

>[!NOTE]
>
>O Adobe Experience Platform Launch foi reformulado como um conjunto de tecnologias de coleta de dados na Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Para testar extensões de tags na Adobe Experience Platform, use a API de tags e/ou as ferramentas de linha de comando para fazer upload dos pacotes de extensão. Em seguida, use a interface do usuário do Experience Platform ou da Coleção de dados para instalar o pacote de extensão em uma propriedade e usar seus recursos em uma build e uma biblioteca de tags.

Este documento aborda como implementar testes completos para sua extensão.

>[!NOTE]
>
>Este guia pressupõe que você esteja usando o macOS com Node.js e npm instalados e disponíveis.

## Validar sua extensão {#validate}

Quando sua equipe estiver satisfeita com o desempenho da extensão e com os resultados da ferramenta [Sandbox](https://www.npmjs.com/package/@adobe/reactor-sandbox#running-the-sandbox), você estará pronto para fazer upload dos pacotes de extensão para tags.

Antes de fazer upload, valide se os campos ou configurações necessários estão presentes. Por exemplo, é uma prática recomendada consultar o [manifesto de extensão](../manifest.md), a [configuração de extensão](../configuration.md), as [exibições](../web/views.md) e os [módulos de biblioteca](../web/format.md), no mínimo.

Um exemplo específico é o arquivo de logotipo: Adicione uma linha `"iconPath": "example.svg",` ao arquivo `extension.json` e inclua esse arquivo de imagem de logotipo no projeto. Esse é o caminho relativo do ícone que será exibido para a extensão. Não deve começar com uma barra. Ele deve fazer referência a um arquivo SVG com uma extensão `.svg`. O SVG deve ser mostrado normalmente quando renderizado como quadrado e pode ser dimensionado pela interface do usuário. Consulte o artigo [Como dimensionar SVG](https://css-tricks.com/scale-svg/) para obter mais detalhes.

>[!NOTE]
>
>Para extensões públicas, inclua um item em seu `extension.json` com um link para sua lista do Exchange. Seu [manifesto de extensão](../manifest.md) deve incluir uma entrada como esta: `"exchangeUrl":"https://www.adobeexchange.com/experiencecloud.details.12345.html"` apontando para o URL da sua lista do Exchange.

## Criar uma integração do Adobe I/O {#integration}

Para usar a API ou as ferramentas de linha de comando, é necessário ter uma conta técnica do Adobe I/O. Você deve criar a conta técnica no console do I/O e usar a ferramenta Uploader para fazer upload do pacote de extensão.

Para obter informações sobre como criar uma conta técnica para usar com tags na Adobe Experience Platform, consulte o guia de [Introdução à API do Reator](../../api/getting-started.md).

>[!IMPORTANT]
>
>Para criar uma integração no Adobe I/O, você deve ser um Administrador de organização da Experience Cloud ou um Desenvolvedor de organização da Experience Cloud.

Se não for possível criar uma integração, provavelmente você não terá as permissões corretas. Isso exigirá que um Administrador da organização conclua as etapas ou atribua a você a função de desenvolvedor.

## Fazer upload do pacote de extensão {#upload}

Agora que tem credenciais, você está pronto para testar o pacote de extensão de ponta a ponta.

Quando você faz upload do pacote de extensão pela primeira vez, ele entra em um estado de `development`. Isso significa que ele só é visível para sua própria organização e somente com uma propriedade que foi marcada para desenvolvimento de extensão.

Use a linha de comando para executar o comando a seguir no diretório que contém o pacote .zip.

```bash
npx @adobe/reactor-uploader
```

`npx` permite baixar e executar um pacote npm sem instalá-lo na sua máquina. Essa é a maneira mais simples de executar o Uploader.

>[!NOTE]
> Por padrão, o carregador espera credenciais do Adobe I/O para um fluxo Oauth de servidor para servidor. As credenciais `jwt-auth` herdadas
> &#x200B;> O pode ser usado executando o `npx @adobe/reactor-uploader@v5.2.0` até a desativação em 1º de janeiro de 2025. Os parâmetros necessários
> &#x200B;> para executar a versão `jwt-auth` pode ser encontrado [aqui](https://github.com/adobe/reactor-uploader/tree/cdc27f4f0e9fa3136b8cd5ca8c7271428b842452).

O carregador requer que você insira apenas algumas informações. Os `clientId` e `clientSecret` podem ser recuperados do console do Adobe I/O. Navegue até a [página Integrações](https://console.adobe.io/integrations) no console do I/O. Selecione a organização correta na lista suspensa, localize a integração apropriada e selecione **[!UICONTROL View]**.

- Qual é o seu `clientId`? Copie e cole isso do Console do I/O.
- Qual é o seu `clientSecret`? Copie e cole isso do Console do I/O.
- Se você chamar o carregador do diretório que contém o pacote .zip, poderá selecioná-lo na lista em vez de digitar o caminho.

Seu pacote de extensão será carregado e o carregador fornecerá a ID do extension_package.

>[!NOTE]
>
>Observação: ao fazer upload ou aplicar patches, os pacotes de extensão são colocados em um estado pendente enquanto o sistema extrai o pacote de forma assíncrona e faz a implantação. Enquanto esse processo está em andamento, você pode pesquisar o status da ID do `extension_package` usando a API e na interface do usuário. Você verá um cartão de extensão no catálogo marcado como Pendente.

>[!NOTE]
>
>Caso você planeje executar o Uploader com frequência, poderá ser difícil incluir sempre todas essas informações. Também é possível passá-las como argumentos na linha de comando. Consulte a seção [Argumentos de linha de comando](https://www.npmjs.com/package/@adobe/reactor-uploader#command-line-arguments) dos documentos do NPM para obter mais informações.

Se você quiser gerenciar o upload direto da sua extensão usando a API, veja as chamadas de exemplo para [criação](../../api/endpoints/extension-packages.md#create) ou [atualização](../../api/endpoints/extension-packages.md#update) de um pacote de extensão nos documentos da API para obter mais detalhes.

## Criar uma propriedade de desenvolvimento {#property}

Depois que você entrar na interface e selecionar **[!UICONTROL Tags]** na navegação à esquerda, a tela [!UICONTROL Properties] será exibida. Uma propriedade é um container para as tags que você deseja implantar e pode ser usada em um ou vários sites.

![](../images/getting-started/properties-screen.png)

Você não verá propriedades na tela na primeira vez que fizer logon. Selecione **Nova propriedade** para criar uma. Insira um nome e um URL. Use a URL do site de teste ou a página na qual você testará a extensão. Esse campo de domínio pode ser usado por algumas extensões ou por uma condição que usa a extensão principal.

>[!NOTE]
>
>`localhost` não funcionará como um valor de URL. Em vez disso, use qualquer valor de modelo para testar se você está usando uma URL `localhost`. Por exemplo, example.com

Para usar essa propriedade para o teste de desenvolvimento de extensão, é necessário expandir as **OPÇÕES AVANÇADAS** e verificar se você marcou a caixa para **Configurar para desenvolvimento de extensão**.

![](../images/getting-started/launch-create-a-dev-property.png)

Selecione **Salvar** na parte inferior para salvar a nova propriedade.

A tela Propriedades é exibida. Selecione o nome da propriedade que você acabou de criar. A tela Visão geral da propriedade é exibida. Ela fornece links para cada área do sistema, com os links de navegação global na coluna à esquerda.

## Instalar a extensão {#install-extension}

Para instalar a extensão nessa propriedade, selecione o link **Extensões** nos links de navegação principal na coluna à esquerda. A extensão **Principal** é exibida na tela **Instalado**. A extensão Principal contém toda a funcionalidade de gerenciamento de tags na coleção de dados.

![](../images/getting-started/extensions.png)

Para adicionar a extensão, selecione a guia **Catálogo**.

![](../images/getting-started/catalog.png)

O catálogo exibe ícones de cartão para cada extensão disponível. Se a extensão não for exibida no catálogo, verifique se você concluiu as etapas acima nas seções Configuração do console de administração da Adobe e Criação do pacote de extensão. O pacote de extensão também poderá aparecer como Pendente se o Experience Platform não tiver concluído o processamento inicial.

Se tiver seguido as etapas anteriores e ainda não vir um pacote de extensão Pendente ou com Falha no catálogo, você deverá verificar o status do pacote de extensão diretamente usando a API. Para obter informações sobre como fazer a chamada de API apropriada, leia [Buscar um ExtensionPackage](../../api/endpoints/extension-packages.md#lookup) na documentação da API.

Após concluir o processamento do pacote de extensão, selecione **Instalar** na parte inferior do cartão.

![](../images/getting-started/install-extension.png)

A tela de configuração será aberta (se a extensão tiver uma). Adicione todas as informações necessárias para configurar a extensão e selecione **Salvar** na parte inferior. O exemplo de tela de configuração visto aqui usa a extensão do Facebook, que requer uma ID do Pixel.

![](../images/getting-started/fb-extension.png)

Agora você deve ver a tela de extensões **Instaladas** com a extensão Principal e a sua extensão.

![](../images/getting-started/extension-installed.png)

## Criar recursos para testar sua extensão {#resources}

As extensões fornecem novos recursos aos usuários da Adobe Experience Platform. Normalmente, são exibidas em Elementos de dados ou no Construtor de regras.

### Elementos de dados

A finalidade dos elementos de dados de tag é ajudar os usuários a tornar os valores persistentes. Cada elemento de dados é um mapeamento ou ponteiro para dados de origem. Um único elemento de dados é uma variável cujo valor pode ser mapeado para sequências de consulta, URLs, valores de cookie, variáveis JavaScript e assim por diante. Selecione **Elementos de dados** na barra de navegação à esquerda e **Criar novo elemento de dados**.

![](../images/getting-started/data-element-create-new-link.png)

As extensões podem definir tipos de elementos de dados, se necessário, para que sua extensão funcione, ou simplesmente como uma conveniência para os usuários. Quando uma extensão fornece tipos de elementos de dados, eles são mostrados em uma lista suspensa para usuários na tela **Criar novo elemento de dados**:

![](../images/getting-started/create-data-element.png)

Quando um usuário seleciona sua extensão na lista suspensa **Extensão**, a lista suspensa **Tipo de elemento de dados** é preenchida com quaisquer tipos de elementos fornecidos pela extensão. O usuário pode mapear cada elemento de dados para seu valor de origem. Os elementos de dados podem ser usados ao criar regras no Evento de alteração de elemento de dados ou no Evento de código personalizado para acionar a execução de uma regra. Um elemento de dados também pode ser usado na Condição do elemento de dados ou em outras Condições, Exceções ou Ações em uma regra.

Depois que o elemento de dados é criado (o mapeamento é configurado), os usuários podem fazer referência aos dados de origem simplesmente referenciando o elemento de dados. Se a origem do valor mudar (novos projetos de site etc.), os usuários só precisarão atualizar o mapeamento uma vez na interface, e todos os elementos de dados receberão automaticamente o novo valor de origem.

### Regras

Selecione o link **Regras** na barra de navegação à esquerda e, então, **Criar nova regra**.

![](../images/getting-started/rules-link.png)

Primeiro, insira um nome descritivo para a regra. A tela **Criar regra** é configurada como uma instrução `if-then`.

![](../images/getting-started/create-new-rule.png)

Se ocorrer um evento, as condições forem aprovadas e não houver exceções, a ação será acionada. Esse mesmo fluxo existe em extensões em que você pode criar ou aproveitar eventos, condições, exceções, elementos de dados ou ações.

Usando o exemplo de extensão do Facebook, adicione um evento para cada vez que uma página for carregada no site de teste.

![](../images/getting-started/load-event.png)

O `Window Loaded` **Tipo de evento** garante que, sempre que uma página for carregada no site de teste, essa regra será acionada. Selecione **Manter alterações**. Para este exemplo, ignore **Condições**, pois a regra deve ser acionada para qualquer página no site de teste.

Em **AÇÕES**, selecione **Adicionar**. A tela **Configuração de ação** é exibida. Em seguida, você deve escolher a extensão à qual a regra deve ser aplicada e a ação a ser executada quando a regra for acionada. Selecione **Facebook Pixel** na lista suspensa **Extensão** e **Enviar exibição de página** na lista suspensa **Tipo de ação**. Selecione **Manter alterações** e **Salvar** na seguinte tela **Editar regra**.

![](../images/getting-started/action-configuration.png)

Ao testar a extensão, selecione eventos, condições etc. que sejam relevantes. fornecido pela sua extensão em qualquer número de regras.

## Publicar suas alterações {#publish}

Na navegação principal, selecione **Publicação** e, em seguida, selecione o link **Adicionar nova biblioteca**:

![](../images/getting-started/add-new-library.png)

Uma biblioteca é um conjunto de instruções sobre como as extensões, os elementos de dados e as regras interagem entre si e com um site. As bibliotecas são compiladas em criações. Uma biblioteca pode conter quantas alterações o usuário quiser criar ou testar simultaneamente.

Na tela **Criar biblioteca**, adicione um nome ao campo de texto **Nome**. As tags fornecem um ambiente de desenvolvimento padrão chamado **Desenvolvimento**. Selecione **Desenvolvimento** na lista suspensa **Ambiente**. Para simplificar, adicione todos os recursos disponíveis. Selecione **Adicionar todos os recursos alterados** e **Salvar**.

>[!NOTE]
>
>Quando você adiciona um recurso a uma biblioteca, um instantâneo desse recurso nesse momento exato é criado e adicionado à biblioteca. Ao fazer alterações em seus recursos posteriormente (por exemplo, como resultado de correções que devem ser feitas), você também precisará atualizar a biblioteca para incluir as alterações mais recentes em seus recursos. O botão **Adicionar todos os recursos alterados** também é útil para essa finalidade.

![](../images/getting-started/create-new-library.png)

Agora que todas as alterações foram incluídas na biblioteca recém-criada (chamada de **dev** no exemplo fornecido), selecione **Salvar e criar no desenvolvimento**.

![](../images/getting-started/build-for-dev.png)

Depois que o processo de criação for concluído, um indicador verde de **sucesso** será exibido próximo ao nome da biblioteca.

![](../images/getting-started/successful-build.png)

A biblioteca de tags foi publicada e está disponível para uso. A página de teste deve usar a biblioteca recém-criada a fim de testar o comportamento da página para o usuário final em um navegador.

## Instalar tags em um site de teste {#install-data-collection-tags}

As instruções de instalação estão disponíveis na guia Ambientes. Essa página exibe todos os ambientes disponíveis e também permite criar outros. Como a biblioteca foi publicada no ambiente de desenvolvimento, marque o ícone de caixa na coluna **INSTALAR** na linha **Desenvolvimento**.

![](../images/getting-started/launch-installation-instructions.png)

A caixa de diálogo **Instruções de instalação da Web** do ambiente de desenvolvimento é exibida. Marque o ícone de cópia para copiar toda a tag `<script>`.

![](../images/getting-started/launch-installation-instructions-dialogue.png)

Conclua a instalação inserindo essa tag única `<script>` na seção `<head>` do documento ou modelo de site. Em seguida, acesse o site de teste para examinar o comportamento da biblioteca de tags publicada.

## Teste {#test}

Veja a seguir uma lista de comandos úteis do console para validar a extensão na página de teste ou no site.

- `_satellite.setDebug(true);` habilitará o modo de depuração e efetuará a saída de instruções de log úteis para o console.
- O objeto `_satellite._container` contém diversas informações úteis sobre a biblioteca implementada, incluindo detalhes sobre build, elementos de dados, regras e extensões incluídas.

O objetivo desse teste é verificar a funcionalidade da biblioteca implementada e garantir que o pacote de extensão se comporte conforme esperado depois de ter sido compilado em uma biblioteca.

Quando você descobre alterações que precisam ser feitas no pacote de extensão, o processo de iteração é semelhante ao de desenvolvimento.

1. Faça alterações no código do projeto.
1. Valide as alterações com a ferramenta Sandbox.
1. Use a ferramenta Packager para criar um novo pacote .zip
1. Use a ferramenta Uploader para fazer upload do novo pacote .zip. O processo segue as mesmas instruções de antes em relação ao upload inicial. No entanto, você observará que, como já existe um pacote de extensão com esse nome no modo de desenvolvimento, o novo pacote substituirá a versão mais antiga em vez de criar um novo.

   >[!NOTE]
   >
   >Argumentos podem ser passados na linha de comando para economizar tempo, evitando a inserção repetida de credenciais. Para obter mais informações sobre isso, leia a [documentação do carregador do Reactor](https://www.npmjs.com/package/@adobe/reactor-uploader).
1. A etapa de instalação pode ser ignorada ao ser atualizado um pacote existente.
1. Modificar recursos: se a configuração de qualquer um dos componentes da extensão tiver sido alterada, será necessário atualizar esses recursos na interface do usuário.
1. Adicione as alterações mais recentes à biblioteca e crie novamente.
1. Realize outra rodada de testes.
