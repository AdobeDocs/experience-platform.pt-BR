---
title: Notas de versão da extensão do Adobe Analytics
description: As notas de versão mais recentes para a extensão de tag do Adobe Analytics no Adobe Experience Platform.
source-git-commit: 8dfb7bdc16d0654ee1d76dc5f5af50938b122d33
workflow-type: tm+mt
source-wordcount: '1220'
ht-degree: 95%

---

# Notas de versão da extensão do Adobe Analytics

>[!NOTE]
>
>O Adobe Experience Platform Launch está sendo reformulado como um conjunto de tecnologias de coleção de dados na Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

## 6 de agosto de 2020

### Extensão do Adobe Analytics versão 1.8.5

#### Correções de erros

* Quando esse campo ficava em branco, o nome do cookie nas configurações do módulo AAM estava sendo definido incorretamente. Isso foi corrigido.

#### Recursos

* [AppMeasurement atualizado para a versão 2.22.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=pt-BR).
* Pequenas alterações na interface do usuário para que as configurações adicionais agora apareçam recolhidas em forma de acordeão em vez de em uma caixa de seleção.

## 2 de junho de 2020

### Adobe Analytics Extension 1.8.4

#### Correções de erros

* Correção de um erro em que os eventos do carrinho de compras (prodView, scAdd, scView etc.) não eram exibidos na lista suspensa de eventos. Todos esses itens agora devem ser selecionados na lista suspensa.

#### Recursos

* Agora você pode desativar o Activity Map na extensão sem precisar usar o código personalizado. O Activity Map é carregado como um módulo separado (semelhante ao módulo AAM) e você pode desativá-lo se desejar.
* Limpe a interface do usuário minimizando as variáveis de hierarquia e outras opções.
* Adição de um campo para definir IDs de compra da interface do usuário de configuração de extensão.

## 10 de março de 2020

### Adobe Analytics Extension 1.8.3

#### Correções de erros

* Correção de um erro que afetava a configuração da regra e que gerava um erro ao tentar definir variáveis se você estivesse usando uma biblioteca personalizada e seus conjuntos de relatórios não estivessem configurados no Analytics.
* Ao criar uma eVar, havia um erro que não mostrava a opção de &quot;duplicar de&quot; uma prop ou vice-versa. Isso foi corrigido para refletir o comportamento em versões anteriores.

#### Recursos

* [AppMeasurement atualizado para 2.20.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)

## 2 de março de 2020

### Adobe Analytics Extension 1.8.2

#### Correções de erros

* Correção de um problema em que a sintaxe incorreta estava sendo usada para eventos numéricos e moeda serializada

#### Recursos

* [AppMeasurement atualizado para 2.18.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html)
* Atualização da biblioteca DIL no módulo do Audience Manager para a versão 9.4
* Aumento do comprimento dos campos de entrada na extensão
* eVars e props nas configurações de extensão e ação agora mostram o nome amigável do Analytics
* Uma caixa de seleção adicionada na seção &quot;Cookies&quot; da configuração de extensão que permite gravar cookies protegidos
* Adicionadas três novas configurações ao módulo Audience Manager. Adicionada uma configuração para ativar o registro, ativar destinos de URL e ativar destinos de cookie

## 13 de novembro de 2019

### Adobe Analytics Extension 1.8.1

#### Correções de erros

* Correção de um erro em que evars e props premium não eram salvos.

## 1 de novembro de 2019

### Adobe Analytics Extension 1.8.0

#### Correções de erros

* Correção de um bug no qual um pequeno número de clientes não conseguia visualizar as opções do conjunto de relatórios no menu suspenso
* Correção de um erro em que algumas variáveis não estavam sendo configuradas corretamente ao usar ECID

#### Recursos

* Classifica numericamente evars, props e eventos na visualização Extensão
* Alterações feitas no esquema de backend para suportar dados de contexto do Magento

## 6 de setembro de 2019

### Adobe Analytics Extension 1.7.8

#### Correções de erros

* Correção de um erro em que alguns usuários não visualizavam as opções do conjunto de relatórios na lista suspensa
* Correção de um erro em que os eventos não eram acionados corretamente

## 5 de setembro de 2019

### Adobe Analytics Extension 1.7.7

#### Recursos

* AppMeasurement atualizado para 2.17
* Atualização do módulo Gerenciamento de público-alvo para oferecer suporte ao DIL 9.3
* Atualização das larguras de campo para lhe dar mais espaço

#### Correções de erros

* Correção de um erro na configuração de participação/não participação
* Correção de um erro em que as variáveis não estavam sendo definidas corretamente ao usar a ECID

## 18 de julho de 2019

### Adobe Analytics Extension 1.7.6

#### Recursos

* Atualização da extensão do Adobe Analytics para oferecer suporte à DIL 9.2 para o Audience Manager

* Atualização da extensão para oferecer suporte ao [AppMeasurement 2.15.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html#version-2.15.0)
* A caixa de seleção a seguir foi removida, pois não há mais suporte: &quot;Não anexe o IFRAME de publicação de destino aos destinos DOM ou fire&quot;

## 4 de junho de 2019

### Adobe Analytics Extension 1.7.5

#### Recursos

* Atualização da extensão do Adobe Analytics para o [AppMeasurement 2.14.0](https://experienceleague.adobe.com/docs/analytics/implementation/appmeasurement-updates.html?lang=pt-BR#version-2.14.0), que inclui uma correção para um problema conhecido de clearVars
* Adição de um link Exchange à extensão. É possível acessar a listagem do Exchange selecionando o menu suspenso e escolhendo &quot;informações de extensão&quot;

#### Correções de erros

* Correção de um erro na interface do usuário que exibia a eVar incorreta como excluída de uma lista
* Correção de um bug que exigia um servidor de rastreamento do SSL ao tentar adicionar vários conjuntos de relatórios. Ao adicionar vários conjuntos de relatórios, é necessário um servidor de rastreamento, mas o campo do servidor de rastreamento do SSL é opcional.

## 15 de abril de 2019

### Adobe Analytics Extension 1.7.4

#### Correções de erros

* A extensão foi revertida depois que um erro foi encontrado no appMeasurement 2.13.0. O appMeasurement 2.13.0 estava causando um problema que não enviava o ECID. Se você instalou a versão 1.7.3, recomendamos a atualização para a 1.7.4 de forma a evitar esse problema. Observe que clearVars continuará até que uma versão atualizada do appMeasurement seja lançada

## 12 de abril de 2019

### Adobe Analytics Extension 1.7.3

#### Correções de erros

* Atualização da extensão do Adobe Analytics para appMeasurement 2.13.0, que inclui uma correção para um problema conhecido de clearVars.

## 21 de março de 2019

### Adobe Analytics Extension 1.7.2

#### Recursos

* Atualização da extensão do Adobe Analytics para DIL 9.1.
* Atualização da extensão do Adobe Analytics para appMeasurement 2.12.
* Atualização da exibição de extensão do Adobe Analytics para o React-Spectrum.
* Ao configurar os conjuntos de relatórios na página de configuração, você verá uma lista suspensa de todos os conjuntos de relatórios na empresa para facilitar a seleção do conjunto de relatórios apropriado.

## 7 de março de 2019

### Adobe Analytics Extension 1.7.1

#### Correções de erros

* Reversão da extensão para a versão 1.6 depois que um erro foi encontrado na 1.7.

## 11 de fevereiro de 2019

### Adobe Analytics Extension 1.6

#### Recursos

* Atualização da extensão Adobe Analytics para DIL 9.0, que oferecerá suporte para opt-in.
* Atualização da extensão do Adobe Analytics para AppMeasurement 2.11 para oferecer suporte à aceitação.

#### Correções de erros

* Correção de um conflito com o JS de protótipo. A extensão do Analytics oferecerá suporte a bibliotecas prototype.js padrão.

## 9 de novembro de 2018

### Adobe Analytics Extension 1.5.1

#### **Correções de erros**

* Regressão do módulo DIL para 7.0 de forma a corrigir um problema que causava problemas com os beacons do Analytics não serem acionados

## 5 de novembro de 2018

### Adobe Analytics Extension 1.5

#### **Recursos**

* Atualização da extensão do Adobe Analytics para oferecer suporte à DIL 8.0 no Audience Manager
* Separação do campo &quot;Serializar do valor&quot; em dois, &quot;ID do evento&quot; e &quot;Valor do evento&quot;. Isso corrigirá o problema que atribuía um valor em vez de serializar um evento
   * Observação: se estiver usando o campo atual para adicionar uma ID usando uma cadeia de caracteres (ex.: Event7=3:abc123) será necessário atualizar sua entrada para refletir a ID no campo &quot;ID do evento&quot;

#### **Correções de erros**

* Correção de um erro que não permitia que o código de moeda fosse preenchido corretamente

## 11 de outubro de 2018

### Adobe Analytics Extension 1.4

#### **Recursos**

* Migração do nome do cookie de rastreamento para a configuração da extensão.

#### **Correções de erros**

* Correção de um erro para que as variáveis definidas não falhassem quando nenhum objeto trackerProperties estava disponível.

## 5 de junho de 2018

### Adobe Analytics Extension 1.3

#### **Recursos**

* Atualização da extensão do Adobe Analytics para oferecer suporte ao AppMeasurement 2.9.
* Adição do recurso &quot;Tornar o rastreador globalmente acessível&quot; na extensão do Adobe Analytics, o que permite que o rastreador seja controlado globalmente no `windows.s`.

#### **Correções de erros**

* Correção de um erro que fazia com que a exibição de lista fosse redefinida ao retornar da exibição de detalhes
* Correção de alguns erros para melhorar o carregamento de recursos no seletor de revisão
* Correção de um erro em que várias regras estavam substituindo s.events na extensão do Adobe Analytics

## 20 de março de 2018

### Adobe Analytics Extension 1.2

#### **Recursos**

* Atualiza o AppMeasurement.js para 2.8.0
* Adiciona suporte para encaminhamento do lado do servidor

## 8 de fevereiro de 2018

### Adobe Analytics Extension 1.1

#### **Recursos**

* O AppMeasurement foi atualizado para a versão 2.6
* O rastreador inicializado do Analytics agora é exposto por meio de um módulo compartilhado na extensão de tag do Adobe Experience Platform para que outras extensões possam incluir o código para interagir com ele.

#### **Correções de erros**

* Correção de um erro na extensão do Adobe Analytics que fazia com que &quot;Erro, ID do conjunto de relatórios ausente na inicialização do AppMeasurement&quot; aparecesse no console do navegador.
