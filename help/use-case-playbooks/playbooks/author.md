---
solution: Experience Platform
title: Assistente de IA para casos de uso - Crie e compartilhe seus próprios manuais.
description: Como criar e compartilhar seus próprios manuais de casos de uso.
role: User
source-git-commit: f813db7599409a8fc048480f7803ed86c9f397fe
workflow-type: tm+mt
source-wordcount: '1111'
ht-degree: 0%

---


# Crie e compartilhe seus próprios manuais

A **Estrutura de Criação do Manual**, disponibilizada pelo Assistente de IA do Adobe, permite que você crie, gerencie e compartilhe manuais com eficiência no Adobe Experience Platform.

A estrutura segue um processo de três etapas:

1. **Captura de metadados**: use o Assistente de IA ou o [formulário da Web] para capturar metadados do manual.

2. **Associação técnica**: adicione ativos técnicos específicos, como jornadas ou públicos-alvo, ao manual. Você mantém controle total sobre o processo de criação de manuais em sua sandbox de desenvolvimento, garantindo o alinhamento com seus esquemas e outras estruturas de dados exclusivas.

3. **Distribuição do manual**: compartilhe manuais de reprodução em diferentes organizações. Por exemplo, o Centro de Excelência Martech da ACME na Alemanha pode criar um manual &quot;dourado&quot; e distribuí-lo para organizações regionais na Tailândia, Austrália etc. para ajudar a padronizar o caso de uso de marketing.

## Criar um manual com o Assistente de IA do Adobe

### Visão geral do manual

Você pode criar um manual de duas maneiras: usando o Assistente de IA do Adobe ou manualmente.

Siga estas etapas para criar um manual com o Assistente de IA do Adobe:

1. No painel de navegação esquerdo, selecione **Guias de Reprodução**.

![&quot;Guias de Reprodução&quot; realçado no painel de navegação esquerdo na interface do usuário.](/help/use-case-playbooks/assets/playbooks/authoring/playbooks.png)

1. Selecione **Novo manual** e **Gerar manual com o Assistente de IA**.

![Selecione o botão &quot;Novo Manual&quot;.](/help/use-case-playbooks/assets/playbooks/authoring/new-playbook.png)

![Selecione o botão &quot;Gerar manual com o Assistente de IA&quot; realçado.](/help/use-case-playbooks/assets/playbooks/authoring/generate-playbook.png)

1. No campo de prompt, descreva o caso de uso.

**Exemplo**: &quot;Envolva clientes da ACME que navegaram em tênis de corrida, mas não concluíram a compra.&quot;

![Selecione o botão &quot;Gerar manual com o Assistente de IA&quot;.](/help/use-case-playbooks/assets/playbooks/authoring/prompt.png)

1. Selecione **Gerar** para criar os metadados do manual.

![A área de prompt com o botão de manual &quot;Gerar&quot; realçado.](/help/use-case-playbooks/assets/playbooks/authoring/generate.png)

1. Depois de gerado, selecione **[!UICONTROL Editar]** para modificar o título, a descrição e os metadados gerados, conforme necessário.

![O manual gerado com o botão &quot;Editar&quot; realçado.](/help/use-case-playbooks/assets/playbooks/authoring/edit.png)

Para garantir que os engenheiros de dados tenham todos os detalhes necessários para configurar o caso de uso, preencha a seção **[!UICONTROL Detalhes do manual]**. Embora opcionais, esses campos ajudam a capturar informações importantes, facilitando a conexão dos componentes técnicos corretos. Selecione **[!UICONTROL Editar]** para adicionar valores aos seguintes campos:

* **Setor**
* **Público-alvo**
* **Canal de marketing**

![Seção de detalhes do manual com o botão &quot;Editar&quot; realçado.](/help/use-case-playbooks/assets/playbooks/authoring/edit-details.png)

Depois que os metadados forem gerados, selecione o botão **Editar mapa de jornadas** para ajustar as etapas no mapa de jornadas conforme necessário.

![Editar o botão do mapa de jornadas.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map-button.png)

![Edite o mapa de jornadas depois de capturar os metadados do manual.](/help/use-case-playbooks/assets/playbooks/authoring/edit-journey-map.png)

Em seguida, prossiga para associar o manual a ativos técnicos.

Para criar um manual de reprodução, selecione **Criar manual de reprodução**.

![Criar manual de reprodução](/help/use-case-playbooks/assets/playbooks/authoring/create-manually.png)

Um modelo em branco do manual é exibido. Preencha detalhes como **Título** e **Descrição**. Você também pode editar o mapa de jornadas para adicionar eventos e pontos de contato conforme necessário.

## Associar o manual aos ativos técnicos

Independentemente de você criar um manual ou com o Assistente de IA, é necessário associá-lo aos ativos técnicos necessários. Navegue até a guia **[!UICONTROL Assets Técnico]** e selecione o produto necessário. Para este exemplo, escolha **[!UICONTROL Journey Optimizer]**.

>[!NOTE]
>
> O suporte para o Real-Time Customer Data Platform será adicionado em uma versão futura.

A guia &quot;Ativos técnicos&quot; do ![ e o botão &quot;Adicionar produto necessário&quot; estão destacados.](/help/use-case-playbooks/assets/playbooks/authoring/technical-assets-add-required-product.png)

Escolha **[!UICONTROL Selecionar um Ativo]** para associar este manual a uma jornada, conforme mostrado na imagem abaixo. Em seguida, selecione **Publicar manual** para finalizar o manual.

![ O botão &quot;Selecionar ativos&quot; foi destacado na guia &quot;Ativos técnicos&quot;](/help/use-case-playbooks/assets/playbooks/authoring/select-assets.png)

![Selecionar uma jornada](/help/use-case-playbooks/assets/playbooks/authoring/journey.png)

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

&quot;Crie uma campanha intitulada &quot;Complete the Look&quot; para aumentar as vendas e o CLV. A campanha incentiva os clientes a adquirir utensílios de cozinha ou mobiliário para concluir uma compra complementar através de recomendações personalizadas e ofertas relacionadas com a sua compra. Primeiro envie uma mensagem aos clientes com recomendações de produto. Se não fizer compras em 7 dias, ele receberá uma segunda mensagem com recomendações e ofertas de produto. Use as notificações por push e o email para entrar em contato com os clientes. Clientes-alvo que efetuaram uma compra nos últimos 7 dias na categoria de utensílios de cozinha ou mobiliário e que não foram visados nos últimos 30 dias. Como parte da campanha, queremos medir KPIs como cliques (email, aplicativo, sms, push), CTR, CTR da E-Wallet, Receita do AOV Conversion.CLV, Eventos de compra total (na loja, digital, call center).&quot;

![Exemplo 1 de prompt](/help/use-case-playbooks/assets/playbooks/authoring/example-prompt.png)

**Exemplo 2:**

&quot;Nome do projeto: Fashion Newsletter
Plano de fundo: (pró-ativo ou resolvendo problemas): uma jornada projetada para enviar informativos de moda para clientes ACME que assinaram a comunicação com informativos.
Objetivo: enviar emails de informativo de moda para clientes da ACME que se inscreveram para comunicação.
Detalhes promocionais: o cliente recebe notícias de moda no canal de email semanalmente. O email deve ser personalizado e as variações de conteúdo devem ser baseadas em gênero, idioma e mercado.
Canais do projeto/Pontos de contato: Email
Público alvo: clientes que assinaram comunicações com o boletim informativo de moda ACME.
KPIs do Target/Métricas de engajamento/ROI: 1. Aumente a receita dos produtos. 2. Impulsionar a fidelidade do cliente.&quot;

![Exemplo 2 de prompt](/help/use-case-playbooks/assets/playbooks/authoring/example-2-prompt.png)

**Exemplo 3:**

&quot;Incentive os compradores a comprar produtos durante uma campanha promocional contínua de produtos.
Interaja com os compradores durante uma promoção contínua enviando comunicações apropriadas por email, SMS ou notificações por push para comprar produtos. Envie a eles um email de lembrete depois de 24 horas sem engajamento na promoção.&quot;

![Exemplo 3 de prompt](/help/use-case-playbooks/assets/playbooks/authoring/example-3-prompt.png)

**Exemplo 4:**

&quot;Vender sapatos para jogadores do ensino médio.&quot;

![Prompt do exemplo 4](/help/use-case-playbooks/assets/playbooks/authoring/example-4-prompt.png)

O Assistente de IA remove todos os detalhes desnecessários, como &quot;Nome do projeto&quot; ou &quot;Plano de fundo&quot;. Ele extrai os elementos principais, como &quot;público-alvo&quot;, &quot;objetivo da campanha&quot; e &quot;canal de marketing&quot; e funciona com qualquer estilo de entrada.

Esses exemplos demonstram como a IA pode refinar e extrair detalhes essenciais de prompts do usuário.

>[!NOTE]
>
> Evite PII ou palavras explícitas ao escrever seus prompts.

## Diretrizes e moderação de conteúdo

Ao criar manuais, lembre-se do idioma e do conteúdo incluídos. Os manuais são visíveis em toda a organização, e qualquer conteúdo ofensivo ou inadequado pode ser sinalizado pelos usuários.

### Sinalização e processo de revisão

Se um manual for sinalizado para conteúdo inadequado ou ofensivo, ele será automaticamente relatado ao Adobe para análise. Em seguida, o Adobe revisa o conteúdo sinalizado e, se ele for considerado inadequado, o cliente é notificado e o Manual é removido.

## Próximas etapas

Agora que você entende como criar e publicar manuais usando o Assistente de IA do Adobe, saiba como começar a usar os manuais disponíveis e escolha o correto para seu caso de uso em [Lista de manuais](/help/use-case-playbooks/playbooks/choose.md).
