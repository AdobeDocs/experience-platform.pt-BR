---
title: Lead para correspondência de contas no Real-Time CDP B2B
type: Documentation
description: Uma visão geral e mais informações sobre o lead para o recurso de correspondência de contas no Experience Platform CDP B2B.
feature: Get Started, Profiles, B2B
badgeB2B: label="B2B edition" type="Informative" url="https://helpx.adobe.com/br/legal/product-descriptions/real-time-customer-data-platform-b2b-edition-prime-and-ultimate-packages.html newtab=true"
exl-id: 2f853599-6bca-4ba6-bbba-131a49d8854e
source-git-commit: 4ba609e777716b1b38f5b143587e5476d851e344
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 3%

---

# Lead para correspondência de contas no Real-Time CDP B2B

## Visão geral {#overview}

O marketing baseado em conta é uma estratégia cada vez mais importante para o marketing B2B. O marketing baseado em conta oferece os seguintes benefícios principais para adquirir clientes específicos de alto valor:

- Limpar ROI
- Alinhamento de vendas e marketing
- Uma abordagem personalizada
- Menos desperdício de recursos
- Um ciclo de vendas mais curto

O marketing baseado em conta oferece a capacidade de vincular clientes conhecidos a contas de vendas. Isso permite que as equipes de marketing se envolvam com possíveis leads das contas do target no início da jornada do cliente para aumentar suas chances de conversão. Um registro de pessoa conhecida normalmente inclui parte ou todas as seguintes informações:

- Nome da pessoa
- Endereço de email
- Número de contato
- Nome da empresa
- Site da empresa
- Cargo
- Localização

## Como funciona {#how-it-works}

As ordens de produção de execução diária usam fatores determinísticos e probabilísticos para corresponder perfis de clientes potenciais conhecidos sem associações de conta existentes. Os perfis de clientes potenciais conhecidos terão um dos seguintes atributos disponíveis:

- b2b.companyName
- b2b.companyWebsite
- workEmail

>[!NOTE]
>
> O atributo b2b.personKey.sourceKey deve existir.

Os atributos b2b.companyName, b2b.companyWebsite e b2b.personKey.sourceKey podem estar localizados no grupo de campos b2b no esquema de pessoa B2B.

![Esquema de pessoa B2B mostrando atributos](/help/rtcdp/accounts/images/b2b-person-schema.png)

O atributo workEmail pode ser encontrado como um grupo de campos de nível superior no esquema de pessoa B2B.

![Esquema de pessoa B2B mostrando workEmail](/help/rtcdp/accounts/images/b2b-person-workemail.png)

Os perfis terão melhor correspondência somente se a pontuação de correspondência estiver acima de um limite de confiança interno. Os resultados são salvos em um novo conjunto de dados do sistema do XDM da relação pessoal da conta existente.

O lead para o serviço de correspondência de contas é executado quando um novo instantâneo do perfil de pessoa é disponibilizado, uma vez a cada 24 horas. Consulte a documentação para obter mais informações sobre a [configuração de lead para correspondência de conta](/help/rtcdp/accounts/account-profile-ui-guide.md).

## Como visualizar o lead para a saída de correspondência de contas {#how-to-view}

Após a execução do trabalho, os resultados são salvos em um novo conjunto de dados do XDM da relação pessoal da conta existente.

Para visualizar o conjunto de dados, selecione **[!UICONTROL Visualizar conjunto de dados]** na parte superior direita.

![Novo conjunto de dados](/help/rtcdp/accounts/images/b2b-dataset-output.png)

O conjunto de dados inclui as informações de conta correspondentes, bem como a pontuação de correspondência do conjunto de dados escolhido. O campo **[!UICONTROL Relationship Source]** indica se ele veio do processo de correspondência entre lead e conta.

![Visualizar pontuações e saída de confiança do conjunto de dados](/help/rtcdp/accounts/images/b2b-dataset-preview.png)

## Monitorar lead para trabalhos de correspondência de contas {#monitoring-jobs}

Você pode monitorar o status do trabalho e as métricas associadas para qualquer lead em trabalhos de correspondência de contas por meio do painel.

Consulte a documentação para obter mais informações sobre os [trabalhos de monitoramento para lead para correspondência de contas](/help/dataflows/ui/b2b/monitor-profile-enrichment.md).
