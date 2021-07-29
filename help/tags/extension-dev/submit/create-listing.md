---
title: Criar uma lista do Exchange para uma extensão
description: Saiba como adicionar sua extensão ao catálogo público no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '1162'
ht-degree: 59%

---

# Criar uma lista do Exchange para uma extensão

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

O Adobe Experience Platform tem um único catálogo unificado onde os usuários podem exibir extensões de tags disponíveis para instalação. Este catálogo está disponível no produto e contém extensões de três tipos:

1. **Extensões públicas**: são extensões concluídas projetadas para uso de produção por qualquer usuário.
1. **Extensões privadas**: são extensões concluídas projetadas para produção, mas foram desenvolvidas por outros usuários em sua empresa e só estão disponíveis para usuários em sua empresa.
1. **Extensões de desenvolvimento**: essas extensões estão em desenvolvimento ativo e só estão disponíveis na empresa e em uma propriedade designada especificamente como uma propriedade de desenvolvimento.

Separadas das extensões no catálogo de produtos, algumas extensões também têm listagens no [Experience Cloud Exchange Marketplace](https://exchange.adobe.com/experiencecloud.experience-platform-launch.html#product).

Essas listas permitem que os desenvolvedores de extensões publiquem informações de suporte, links para suporte ou documentação adicionais e comercializem suas extensões para usuários potenciais que talvez não conheçam sua empresa ou a funcionalidade de sua extensão. Neste marketplace, sua extensão terá uma lista pública que pode ser visualizada sem que o usuário seja autenticado no Platform.  Muitos desenvolvedores acham útil desenvolver uma listagem do Exchange, mas não é uma etapa necessária.

Se você não tiver uma empresa para fazer upload e testar seu pacote de extensão, será necessário registrar-se no programa Exchange e iniciar uma lista.  Isso acionará a criação de uma conta de empresa (leva algum tempo; você receberá um email quando estiver concluído) que poderá usar para fazer upload e testar sua extensão.  Nunca é preciso tornar a lista pública.

Se você já tiver uma conta da empresa ou se não planeja concluir a lista, ignore o resto desta etapa e prossiga para [fazer upload e testar sua extensão](./upload-and-test.md).

## Criar uma lista

>[!NOTE]
>
>O processo a seguir detalha a criação de uma lista de aplicativos no programa Adobe Exchange. Este é o termo usado para as várias integrações e extensões no Adobe Experience Platform.

![Localização de link do Experience Cloud App Manager](../images/getting-started/app-mgr-link.png)

1. Fazer logon no [site do Exchange Partner](https://partners.adobe.com/exchangeprogram/experiencecloud). Depois de fazer logon, selecione o link **App Manager** ao lado do seu nome.
1. Selecione a guia **Criar novo aplicativo** e selecione **Criar novo aplicativo** para uma solução personalizada ou selecione um modelo aplicável.
1. Forneça suas informações de lista. Para obter informações detalhadas sobre o App Manager, leia todo o [artigo](https://adobeexchangeec.zendesk.com/hc/en-us/articles/360024197931). As informações de listagem devem ser muito claras sobre o que a extensão faz e por que são úteis. A listagem funciona como um espaço de marketing para seu aplicativo. Promova sua extensão aqui usando descrições claras, links para landing pages do site, links para documentos de ajuda ou endereços de email de suporte e assim por diante. Embora o espaço nas exibições de extensão seja limitado, a listagem do Exchange oferece uma oportunidade de promover sua extensão e sua empresa. Veja a seguir sugestões para melhorar a promoção da extensão:
   - **Ícone de aplicativo** - Verifique se o ícone da lista do Exchange tem as dimensões apropriadas, 512 x 512 para png ou proporção 1:1 para jpg.

   >[!NOTE]
   >
   >Este é um formato de arquivo diferente do usado no código de extensão. A própria extensão conterá um arquivo svg como o [ícone](../manifest.md).

   - **Imagem em destaque**  - Obtenha atenção usando uma imagem que pode ser independente e mostrará sua marca e destacará seu aplicativo. A Imagem em destaque é aquela que aparece quando alguém compartilha um link com sua listagem do Exchange ou posta sobre ela em redes sociais. Portanto, precisa ser uma representação modelo de sua marca.
   - **Logotipo do App Publisher** - este é o logotipo corporativo. Verifique se o ícone tem as dimensões apropriadas de 1280 x 720 ou 2560 x 1440 (16:9) em formato png ou jpg.
   - **Instruções de configuração**  - Informe aos clientes como configurar sua extensão do Adobe Experience Platform. Certifique-se de que eles entendam as configurações necessárias e as próximas etapas quando sua [visualização de configuração](../configuration.md) for exibida imediatamente após a instalação da extensão em uma propriedade. 
   - **Tags** - na primeira página de edição da sua lista, inclua a palavra &quot;Launch&quot; no campo &quot;Tags personalizadas&quot;. Isso fará com que sua listagem apareça em pesquisas por tags no Exchange Marketplace:
      ![](../images/getting-started/custom-tags.jpg)
   - **Sandboxes**  - Seu acesso às Soluções do Adobe é por meio de uma conta de sandbox onde você tem acesso a uma versão totalmente funcional do Adobe Experience Platform. Essas contas de sandbox são solicitadas à medida que você cria sua lista de aplicativos. Na seção **Connections** selecione as conexões específicas aplicáveis ao aplicativo que você criou (sua extensão de tag) e, ao pressionar **Save**, a solicitação de sandbox será gerada se necessário.
1. Envie sua lista. A equipe do Adobe Exchange verificará seu aplicativo e fornecerá feedback se atualizações forem necessárias. Se marcar a caixa de seleção **publicar imediatamente** ao enviar sua listagem, ela será publicada imediatamente após a aprovação. Se desejar publicar seu aplicativo posteriormente, deixe a caixa de seleção desmarcada. Quando sua lista de extensão for aprovada, um botão azul **Publicar** aparecerá ao lado dele na página de listagens do seu aplicativo (extensão).

### Criar uma lista eficaz

Consulte a [Diretriz de envio de aplicativo](https://partners.adobe.com/exchangeprogram/experiencecloud/build/ec-exchange.html) para obter informações detalhadas sobre como criar a lista mais envolvente.

#### Após enviar sua lista do Exchange

Depois de enviada, a equipe do Adobe Exchange revisará o aplicativo e aprovará o aplicativo ou responderá com comentários sobre as alterações. Esse processo é detalhado nas Diretrizes de envio do aplicativo.

Se você não tiver um logon no site do Exchange, verifique se seu email está registrado para o programa do Exchange seguindo as instruções no [Guia de registro do programa](https://partners.adobe.com/content/mcp/us/en/home/reg-guide.html). Cada usuário deve associar seu email à conta do parceiro de sua empresa. As perguntas sobre esse processo podem ser direcionadas por email para <ExchangeHelpEC@adobe.com>.

#### Atualizar sua lista do Exchange após aprovação inicial

Ao atualizar sua extensão ou se precisar apenas atualizar sua lista do Exchange, faça logon no [Portal do parceiro](https://partners.adobe.com/exchangeprogram/experiencecloud) e selecione o botão App Manager próximo ao seu nome. Em seguida, selecione seu aplicativo e siga o fluxo acima que foi usado inicialmente para criar a lista. Depois de reenviada, a equipe do Adobe Exchange revisará as alterações e as aprovará ou responderá com comentários sobre as alterações.

## Vincular o pacote de extensão à lista

Depois que a lista for aprovada e estiver disponível publicamente, recomendamos que você forneça um link para a lista pública no campo `exchange_url` do arquivo `extension.json` em seu pacote de extensão.  Isso criará um link &quot;Mais informações&quot; no catálogo de extensões de tag para que os usuários no produto possam encontrar sua listagem e suas informações adicionais.
