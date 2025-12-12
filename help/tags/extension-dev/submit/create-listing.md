---
title: Criar uma lista do Exchange para uma extensão
description: Saiba como adicionar sua extensão ao catálogo público na Adobe Experience Platform.
exl-id: 0395fc99-5e2b-46d6-a067-f8f167733e02
source-git-commit: 44e2b8241a8c348d155df3061d398c4fa43adcea
workflow-type: tm+mt
source-wordcount: '1147'
ht-degree: 65%

---

# Criar uma lista do Exchange para uma extensão

A Adobe Experience Platform tem um catálogo unificado em que os usuários podem encontrar extensões de tag disponíveis para instalação. Este catálogo está disponível no produto e contém extensões de três tipos:

1. **Extensões públicas**: são extensões concluídas projetadas para uso de produção por qualquer usuário.
1. **Extensões privadas**: são extensões concluídas projetadas para produção, mas foram desenvolvidas por outros usuários em sua empresa e só estão disponíveis para usuários em sua empresa.
1. **Extensões de desenvolvimento**: essas extensões estão em desenvolvimento ativo e só estão disponíveis na empresa e em uma propriedade designada especificamente como uma propriedade de desenvolvimento.

Separadas das extensões no catálogo de produtos, as extensões públicas também têm listagens no [Experience Cloud Exchange App Marketplace](https://exchange.adobe.com/apps/browse/ec).

Essas listas permitem que os desenvolvedores de extensões publiquem informações de suporte, links para suporte ou documentação adicionais e comercializem suas extensões para usuários potenciais que talvez não conheçam sua empresa ou a funcionalidade de sua extensão. Neste marketplace, sua extensão terá uma lista pública que pode ser visualizada sem que o usuário seja autenticado no Experience Platform. Para extensões públicas, criar essa lista do Exchange é uma etapa necessária.

>[!TIP]
>
>Quando sua lista do Exchange é publicada, um link é adicionado automaticamente ao conteúdo da lista que permite que seus clientes e clientes potenciais clicem e `Connect with publisher` para obter mais informações sobre seus produtos e serviços. Seu endereço de email de contato não é exibido, pois essas mensagens serão encaminhadas a você pelo sistema do Exchange.

Se você não tiver uma empresa para fazer upload e testar seu pacote de extensão, deverá se registrar no programa Exchange e iniciar uma lista. Isso acionará a criação de uma conta de empresa (leva algum tempo; você receberá um email quando estiver concluído) que poderá usar para fazer upload e testar sua extensão. Novamente, as listagens do Exchange são necessárias somente para extensões públicas.

Se você já tiver uma conta da empresa ou se não precisar de uma lista do Exchange (somente extensões privadas), ignore o resto desta etapa e prossiga para [fazer upload e testar sua extensão](./upload-and-test.md).

## Criar uma lista

>[!NOTE]
>
>O processo a seguir detalha a criação de uma lista de aplicativos no programa Adobe Exchange. Este é o termo usado para as várias integrações e extensões na Adobe Experience Platform.

![Local do link do Gerenciador de aplicativos da Experience Cloud](../images/getting-started/app-mgr-link.png)

1. Fazer logon no [site do Exchange Partner](https://partners.adobe.com/exchangeprogram/experiencecloud). Depois de fazer logon, selecione o link do **Gerenciador de aplicativos** próximo a seu nome.
1. Selecione a guia **Criar novo aplicativo** e selecione **Criar novo aplicativo** para obter uma solução personalizada ou selecione um modelo aplicável.
1. Forneça suas informações de lista. Para obter informações detalhadas sobre o App Manager, leia todo o [artigo](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931). As informações da lista devem ser muito claras sobre o que a extensão faz e por que ela é útil. A lista funciona como um espaço de divulgação para seu aplicativo. Promova sua extensão aqui usando descrições claras, links das páginas de destino de seu site, links de documentos de ajuda e endereços de email de suporte, entre outros. Embora o espaço de exibição de extensões seja limitado, a lista do Exchange oferece uma oportunidade de divulgar a extensão e sua empresa. Veja a seguir sugestões para melhorar a divulgação da extensão:
   - **Ícone de Aplicativo** - Verifique se o ícone da lista do Exchange tem as dimensões apropriadas, 512 x 512 para png ou proporção 1:1 para jpg.

     >[!NOTE]
     >
     >Esse é um formato de arquivo diferente daquele usado no código da extensão. A própria extensão conterá um arquivo svg como o [ícone](../manifest.md).

   - **Imagem em destaque** - Chame atenção usando uma imagem independente que mostre sua marca e destaque seu aplicativo. A Imagem em destaque é aquela mostrada quando alguém compartilha um link para sua lista do Exchange ou posta sobre ela em redes sociais. Portanto, precisa ser uma boa representação de sua marca.
   - **Logotipo do App Publisher** - Este é o logotipo corporativo. Verifique se o ícone tem as dimensões apropriadas de 1280 x 720 ou 2560 x 1440 (16:9) em formato png ou jpg.
   - **Instruções de configuração** — informe aos clientes como configurar sua extensão da Adobe Experience Platform. Certifique-se de que eles entendam as configurações necessárias e as próximas etapas quando sua [visualização de configuração](../configuration.md) for exibida imediatamente após a instalação da extensão em uma propriedade.
   - **Tags** - na primeira página de edição da sua lista, inclua a palavra &quot;Launch&quot; no campo &quot;Tags personalizadas&quot;. Assim, sua lista será mostrada em pesquisas de tags no marketplace do Exchange:
     ![](../images/getting-started/custom-tags.jpg)
   - **Sandboxes** — seu acesso às soluções da Adobe é feito por meio de uma conta de sandbox na qual você tem acesso a uma versão totalmente funcional da Adobe Experience Platform. Essas contas de sandbox são solicitadas à medida que você cria sua lista de aplicativos. Na seção **Conexões** selecione as conexões específicas aplicáveis ao aplicativo criado (sua extensão de tag) e, quando você pressionar **Salvar**, a solicitação da sandbox será gerada, se necessário.
1. Envie sua lista. A equipe do Adobe Exchange verificará seu aplicativo e fornecerá feedback se atualizações forem necessárias. Se você marcar a caixa de seleção **publicar imediatamente** ao enviar a listagem, ela será publicada imediatamente após a aprovação. Se quiser publicar seu aplicativo posteriormente, deixe a caixa de seleção desmarcada. Quando sua lista de extensões for aprovada, um botão azul **Publicar** aparecerá ao lado dela na página de listas do seu aplicativo (extensão).

### Criar uma lista eficaz

Consulte a [Diretriz de envio de aplicativo](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) para obter informações detalhadas sobre como criar a lista mais envolvente.

#### Após enviar sua lista do Exchange

Depois de enviada, a equipe do Adobe Exchange revisará o aplicativo e aprovará o aplicativo ou responderá com comentários sobre as alterações. Esse processo é detalhado nas Diretrizes de envio do aplicativo.

Se você não tiver um logon no site do Exchange, verifique se seu email está registrado para o programa do Exchange seguindo as instruções no [Guia de registro do programa](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html). Cada usuário deve associar seu email à conta de parceiro de sua empresa. As perguntas sobre esse processo podem ser enviadas por email a <ExchangeHelpEC@adobe.com>.

#### Atualizar sua lista do Exchange após aprovação inicial

Ao atualizar sua extensão ou se precisar apenas atualizar sua lista do Exchange, faça logon no [Portal do parceiro](https://partners.adobe.com/exchangeprogram/experiencecloud) e selecione o botão App Manager próximo ao seu nome. Em seguida, selecione seu aplicativo e siga o fluxo acima que foi usado inicialmente para criar a lista. Depois de reenviada, a equipe do Adobe Exchange revisará as alterações e as aprovará ou responderá com comentários sobre as alterações.

## Vincular o pacote de extensão à lista

Depois que a lista for aprovada e estiver disponível publicamente, recomendamos que você forneça um link para a lista pública no campo `exchange_url` do arquivo `extension.json` em seu pacote de extensão.  Isso criará um link &quot;Mais informações&quot; no catálogo de extensão de tag para que os usuários dentro do produto possam encontrar a lista e suas informações adicionais.
