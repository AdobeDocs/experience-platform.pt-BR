---
solution: Experience Platform
title: Aprenda a criar e compartilhar seus próprios manuales usando o Assistente de IA.
description: Como criar e compartilhar seus próprios manuales de casos de uso.
role: User
exl-id: 0bc49710-ad9e-4509-b7e6-55f9b9037aa9
source-git-commit: 9583d836d4e295bcb5cc2ce41ba8ba6d2046b114
workflow-type: tm+mt
source-wordcount: '1679'
ht-degree: 0%

---


# Autor e compartilhe seus próprios manuales (beta)

O [!DNL Playbook Authoring Framework]assistente de IA em Adobe Experience Platform permite criar, gerenciar e compartilhar manualmente com eficiência dentro Adobe Experience Platform.

A estrutura segue um processo de três etapas:

1. **Captura de metadados**: use o Assistente de IA ou o formulário da Web para capturar metadados do manual.

2. **Associação técnica**: adicione ativos técnicos específicos, como jornadas ou públicos-alvo, ao manual. Você mantém controle total sobre o processo de criação de manuais em sua sandbox de desenvolvimento, garantindo o alinhamento com seus esquemas e outras estruturas de dados exclusivas.

3. **Distribuição do manual**: compartilhe manuais de reprodução em diferentes organizações. Por exemplo, o Centro de Excelência Martech da ACME na Alemanha pode criar um manual &quot;dourado&quot; e distribuí-lo para organizações regionais na Tailândia, Austrália etc. para ajudar a padronizar o caso de uso de marketing.

## Criar um manual

Você pode criar um manual de duas maneiras: usando o Assistente de IA ou manualmente. Leia as seções a seguir para saber como criar um manual com o Assistente de IA.

### Visão geral do manual

Siga estas etapas para criar um manual com o Assistente de IA:

No painel de navegação esquerdo, selecione **[!UICONTROL Livros de reprodução]**.

![&quot;Manuales&quot; destacados no painel de navegação à esquerda no interface.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

Selecione **[!UICONTROL Novo manual]** e **Gerar manual com o Assistente de IA**.

![A interface do manual com a opção &quot;Gerar manual com o Assistente de IA&quot; está selecionada.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

Use o campo de prompt para descrever o caso de uso. Por exemplo:

&quot;Envolva os clientes da ACME que navegaram em tênis de corrida, mas não concluíram a compra.&quot;

![A interface do manual com a área de formulário Web realçada.](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

Selecione **[!UICONTROL Gerar]** para criar os metadados do manual.

![A área de prompt com o botão de manual &quot;Gerar&quot; realçado.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

Depois de gerado, selecione **[!UICONTROL Editar]** para modificar o título, a descrição e os metadados gerados, conforme necessário.

![O manual gerado com o botão &quot;Editar&quot; realçado.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

Para garantir que os engenheiros de dados tenham todos os detalhes necessários para configurar o caso de uso, preencha a seção **[!UICONTROL Detalhes do manual]**. Embora opcionais, esses campos ajudam a capturar informações importantes, facilitando a conexão dos componentes técnicos corretos. Selecione **[!UICONTROL Editar]** para adicionar valores aos seguintes campos:

* **Setor**
* **Público-alvo**
* **Canal de marketing**

![A seção de detalhes do manual com o botão &quot;Editar&quot; realçado.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

Depois que os metadados forem gerados, selecione **[!UICONTROL Editar mapa de jornadas]** para ajustar as etapas no mapa de jornadas conforme necessário.

![Editar o botão do mapa de jornadas.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![Edite o mapa de jornadas depois de capturar os metadados do manual.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

Em seguida, prossiga para associar o manual a ativos técnicos. Para criar um manual de reprodução, selecione **[!UICONTROL Criar manual de reprodução]**.

![Criar manual de reprodução](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

Um modelo em branco do manual é exibido. Preencha detalhes como **Título** e **Descrição**. Você também pode editar o mapa de jornadas para adicionar eventos e pontos de contato conforme necessário.

## Associar o manual aos ativos técnicos

Independentemente de você criar um manual ou com o Assistente de IA, é necessário associá-lo aos ativos técnicos necessários. Navegue até a guia **[!UICONTROL Assets Técnico]** e selecione o produto necessário. Para este exemplo, selecione **[!UICONTROL Journey Optimizer]**.

>[!NOTE]
>
> O suporte para CDP em tempo real será adicionado em uma versão futura.

![A guia &quot;Ativos técnica&quot; e a botão &quot;Adicionar produto obrigatório&quot;.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

Escolha **[!UICONTROL Selecionar um ativo]** para associar este manual a uma jornada como mostrado na imagem abaixo. Em seguida, selecione **Publish manual** para finalizar o manual.

![&quot;Selecionar ativos&quot; botão destacado na guia &quot;Technical ativos&quot;](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![Selecione uma jornada](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

Depois de publicado, o manual extrai e associa automaticamente o esquema da jornada e os detalhes do público-alvo.

![Manual publicado](/help/use-case-playbooks/assets/playbooks/authoring/publish-playbook.png)

Todos os manuais criados estão disponíveis na guia **Seus manuais**.

![ Guia &quot;Seus manuais&quot;](/help/use-case-playbooks/assets/playbooks/authoring/your-playbooks-tab.png)

Você pode selecionar qualquer manual do catálogo para criar instâncias para reutilização. Consulte a documentação para [saber como criar instâncias](/help/use-case-playbooks/playbooks/create-share-reuse.md).

A opção ![&quot;Criar instância&quot; é realçada na guia &quot;Visão geral do manual&quot; depois que você seleciona um manual.](/help/use-case-playbooks/assets/playbooks/authoring/create-instance.png)

>[!NOTE]
>
> Depois que um manual é publicado, ele não pode ser editado. Para fazer alterações, exclua o manual e comece novamente.

## Exemplo de prompts

O Assistente de IA pode processar várias estruturas de prompt e extrair detalhes-chave enquanto filtra informações desnecessárias. Abaixo estão alguns exemplos de prompts do usuário e como eles são interpretados pelo sistema:

**Exemplo 1:**

&quot;Criar um campanha intitulado &quot;Todos os Apps o Look&quot; em solicitar para aumentar as vendas e a CLV. A campanha recomenda que os clientes tenham kitchenware ou móveis comprados para realizar uma compra complementar por meio de recomendações personalizadas e ofertas relacionadas à sua compra. Primeiro envie uma mensagem aos clientes com recomendações de produto. Se não fizerem compras dentro de 7 dias, eles receberão uma segunda mensagem com recomendações e ofertas de produtos. Use notificações por push e email para entrar em contato com os clientes. Target clientes que compraram nos últimos 7 dias em kitchenware ou furniture categoria e não foram alvos nos últimos 30 dias. Como parte do campanha, queremos medir KPIs como cliques (email, aplicativo, sms, push), CTR, CTR E-Wallet, AOV Receita de Conversão.CLV, Eventos de compra total (em armazenamento, digitais, central de atendimento)&quot;.

![Exemplo que mostra um prompt longo na caixa de entrada de texto](/help/use-case-playbooks/assets/playbooks/authoring/long-prompt.png)

**Exemplo 2:**

&quot;Nome do projeto: Fashion Newsletter
Plano de fundo: (pró-ativo ou resolvendo problemas): uma jornada projetada para enviar informativos de moda para clientes ACME que assinaram a comunicação com informativos.
Objetivo: enviar emails de informativo de moda para clientes da ACME que se inscreveram para comunicação.
Detalhes promocionais: o cliente recebe notícias de moda no canal de email semanalmente. O email deve ser personalizado e as variações de conteúdo devem ser baseadas em gênero, idioma e mercado.
Canais do projeto/Pontos de contato: Email
Público alvo: clientes que assinaram comunicações com o boletim informativo de moda ACME.
KPIs do Target/Métricas de engajamento/ROI: 1. Aumente a receita dos produtos. 2. Impulsionar a fidelidade do cliente.&quot;

![Exemplo mostrando um prompt organizado na caixa de entrada de texto](/help/use-case-playbooks/assets/playbooks/authoring/organized-list-prompt.png)

**Exemplo 3:**

&quot;Incentive os compradores a comprar produtos durante uma campanha promocional contínua de produtos.
Interaja com os compradores durante uma promoção contínua enviando comunicações apropriadas por email, SMS ou notificações por push para comprar produtos. Envie a eles um email de lembrete depois de 24 horas sem engajamento na promoção.&quot;

![Exemplo mostrando um prompt conciso na caixa de entrada de texto](/help/use-case-playbooks/assets/playbooks/authoring/concise-prompt.png)

**Exemplo 4:**

&quot;Vender sapatos para jogadores do ensino médio.&quot;

![Exemplo mostrando um prompt de uma linha](/help/use-case-playbooks/assets/playbooks/authoring/one-liner-prompt.png)

O Assistente de IA remove todos os detalhes desnecessários, como &quot;Nome do projeto&quot; ou &quot;Plano de fundo&quot;. Ele extrai os elementos principais, como &quot;público-alvo&quot;, &quot;objetivo da campanha&quot; e &quot;canal de marketing&quot; e funciona com qualquer estilo de entrada.

Esses exemplos demonstram como a IA pode refinar e extrair detalhes essenciais de prompts do usuário.

>[!NOTE]
>
> Evite PII ou palavras explícitas ao escrever seus prompts.

## Diretrizes e moderação de conteúdo

Ao criar manuais, lembre-se do idioma e do conteúdo incluídos. Os manuais são visíveis em toda a organização, e qualquer conteúdo ofensivo ou inadequado pode ser sinalizado pelos usuários.

### Sinalização e processo de revisão

Se um manual for sinalizado para conteúdo inadequado ou ofensivo, ele será automaticamente relatado ao Adobe para análise. Em seguida, o Adobe revisa o conteúdo sinalizado e, se ele for considerado inadequado, o cliente é notificado e o Manual é removido.

## Compartilhar manuais entre sandboxes {#share-playbooks-sandboxes}

Ao criar e publicar um manual em uma sandbox, ele se torna disponível automaticamente em todas as sandboxes da organização. Isso elimina a necessidade de compartilhamento manual e permite criar instâncias do manual em qualquer outra sandbox sem problemas.

>[!TIP]
>
>Se o manual referenciar campos que não estão disponíveis no esquema de união da sandbox de destino ou não têm as permissões necessárias, você poderá ver uma mensagem de erro ao tentar criar a instância. Essa mensagem indica os campos ausentes e/ou as permissões ausentes.

Se algum campo estiver ausente do esquema de união, uma caixa de diálogo o destacará durante a importação.

![Campos ausentes do esquema de união listado durante o processo de importação](/help/use-case-playbooks/assets/playbooks/authoring/missing-fields.png)

## Compartilhamento de manuais entre organizações {#sharing-playbooks-organizations}

O compartilhamento de manuais entre organizações ajuda a garantir consistência e eficiência quando várias equipes precisam seguir as mesmas práticas recomendadas. Para compartilhar um manual de uma organização para outra, siga estas etapas:

1. **Faça logon na organização de origem**: navegue até a organização que contém o manual que você criou e deseja compartilhar na guia **[!UICONTROL Seus manuais]**.
2. **Publicar o manual**: se o manual ainda não tiver sido publicado, você deverá publicá-lo antes de compartilhá-lo.

   >[!NOTE]
   >
   >Uma parceria deve ser estabelecida entre as organizações de origem e de destino para permitir o compartilhamento do manual. Saiba como [criar uma solicitação de parceria de organização](/help/sandboxes/ui/sharing-packages-across-orgs.md#create-an-organization-partnership-request).

3. **Iniciar o compartilhamento**: depois que o manual for publicado e uma parceria for estabelecida, selecione **[!UICONTROL Compartilhar Manual]**.
4. **Selecionar a organização de destino**: escolha a organização com a qual deseja compartilhar o manual quando solicitado.
5. **Confirmar e compartilhar**: confirme sua seleção. Você receberá mensagens de confirmação indicando que o compartilhamento foi bem-sucedido.
6. **Verificar a organização de destino**: faça logon na organização de destino para verificar se o manual de reprodução está disponível.
7. **Importar o manual**: selecione **[!UICONTROL Importar]** para trazer o manual para a organização de destino. Você pode exibi-lo na guia **Guias de reprodução**.

Se o manual não for exibido, verifique se ele foi publicado e se a parceria da organização está ativa.

>[!IMPORTANT]
>
>Não há suporte para compartilhamento de playbook transitório. Se você compartilhar um manual de uma organização para outra e, em seguida, importá-lo, ele não poderá ser compartilhado novamente da organização de recebimento para uma terceira organização.

## Permissões necessárias {#required-permissions}

Para acessar a sandbox e usar esse recurso, você precisa das seguintes permissões:

### Permissões de sandbox

Essas permissões são necessárias para acessar o ambiente de sandbox onde o recurso existe:

* **Gerenciar sandbox**
* **Exibir sandbox**

* **Permissões de compartilhamento de pacotes**:

Essas permissões são necessárias para a funcionalidade de compartilhamento interno:

* [**Gerenciar pacote**](/help/sandboxes/ui/sandbox-tooling.md)
* [**Compartilhar pacote**](/help/sandboxes/ui/sharing-packages-across-orgs.md)

Essas permissões permitirão:

* Insira o ambiente de sandbox
* Acessar o recurso na sandbox
* Gerencie e compartilhe pacotes conforme necessário

Essas permissões estão localizadas na **[!UICONTROL seção Sandboxes]** das lista de permissões.

![As permissões lista com as permissões relevantes destacadas.](/help/use-case-playbooks/assets/playbooks/authoring/permissions.png)

### Jornadas e objetos relacionados - permissões

Ao construir Jornadas que usam Manuales, provavelmente você fará referência a outros objetos, como **Canais**, **Audiences** e outras entidades. Cada um deles tem suas próprias permissão definidas.

Essas são as principais permissões para ações relacionadas à Jornada, como:

* **Exibir jornada**
* **Gerenciar jornada**
* Permissões relacionadas a objetos como Públicos-alvo e Canais

Você também precisará das seguintes permissões de público-alvo:

* **Segmento lido**
* **Perfil lido**
* **Conjunto de dados lido**

Como as Jornadas são altamente flexíveis e podem envolver muitos objetos interconectados, suas [permissões completas](https://experienceleague.adobe.com/en/docs/journey-optimizer/using/access-control/privacy/high-low-permissions) são documentadas separadamente e podem variar de acordo com seu caso de uso específico.

## Próximas etapas

Agora que você entende como criar, publicar e compartilhar manuais usando o Assistente de IA, saiba como começar a usar os manuais disponíveis e escolha o correto para seu caso de uso na [Lista de manuais](/help/use-case-playbooks/playbooks/choose.md).