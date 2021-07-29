---
title: Copiar recursos
description: Saiba como criar um novo recurso de tag usando as configurações de um recurso de tag existente no Adobe Experience Platform.
source-git-commit: 7e27735697882065566ebdeccc36998ec368e404
workflow-type: tm+mt
source-wordcount: '785'
ht-degree: 84%

---

# Copiar recursos

>[!NOTE]
>
>A Adobe Experience Platform Launch foi reformulada como um conjunto de tecnologias de coleta de dados no Adobe Experience Platform. Como resultado, várias alterações de terminologia foram implementadas na documentação do produto. Consulte o seguinte [documento](../../term-updates.md) para obter uma referência consolidada das alterações de terminologia.

Às vezes, é conveniente criar um novo recurso usando as configurações de um recurso existente. Nesses casos, você pode fazer uma cópia.

Propriedades, extensões, regras e elementos de dados podem ser copiados.

Copiar um recurso cria uma duplicata desse recurso no destino especificado. Essa ação é discreta e única e não há relacionamento contínuo entre o recurso original e as cópias que tiverem sido feitas.

## Iniciar uma cópia

É possível iniciar uma cópia de uma extensão visualizando as extensões instaladas, selecionando a seta suspensa no botão **[!UICONTROL Configurar]** e selecionando **[!UICONTROL Copiar]**.

![Como copiar a extensão do Analytics](../../images/copy-initiate-extension.png)

Para propriedades, regras e elementos de dados, basta selecionar o recurso que deseja copiar e clicar em **[!UICONTROL Copiar]** no menu de ações.

![Como copiar minha regra do Analytics](../../images/copy-initiate-rule.png)

Se estiver copiando uma regra ou um elemento de dados, na caixa de diálogo de cópia, você poderá usar o menu suspenso para selecionar uma Propriedade de destino para a qual deseja copiar (a configuração padrão é a propriedade atual). As extensões não podem ser copiadas para a mesma propriedade, portanto, elas não fornecerão essa opção.

>[!NOTE]
>
>Na interface do usuário da coleta de dados, não é possível copiar recursos para outra propriedade, se uma propriedade estiver configurada para desenvolvimento de extensão e a outra propriedade não estiver.

Depois de configurar o comportamento desejado, clique em **[!UICONTROL Copiar]**.

## Copiando propriedades

Quando você faz uma cópia de uma propriedade completa, há algumas coisas que você deve entender sobre o processo.

* As configurações de propriedade serão copiadas exatamente como estão (domínios, configurações avançadas etc.)
* Regras, elementos de dados e extensões da propriedade de origem serão copiados para a nova propriedade de destino. Adaptadores, ambientes e bibliotecas não serão copiados.
* As extensões necessárias (extensões exigidas por quaisquer elementos de dados existentes ou componentes de regras) serão copiadas para a propriedade-alvo mesmo se tiverem sido desinstaladas da propriedade de origem.
* A cópia de uma propriedade pode levar algum tempo. Esse processo acontece em segundo plano. Você pode monitorar o progresso da cópia ou continuar com outras tarefas enquanto ele acontece.
* Se você modificar um recurso individual depois de já ter sido copiado para a propriedade de destino (mas antes da cópia ser concluída), as novas modificações não serão copiadas.

## Como copiar extensões

Ao copiar uma extensão para outra propriedade, há algumas coisas que você precisa saber.

* Se a propriedade de destino não tiver a extensão instalada, ela será instalada usando as mesmas configurações que a propriedade de origem.
* Se a propriedade de destino já tiver a extensão instalada, apenas as configurações serão copiadas.
* Se a propriedade de destino tiver uma versão inferior da extensão instalada, você receberá um aviso de que precisa atualizar a extensão na propriedade de destino, antes de poder executar a cópia. Os desenvolvedores de extensão podem adicionar configurações a suas extensões ao longo do tempo, de modo que as configurações de uma extensão mais nova não podem ser aplicadas de forma confiável às versões anteriores.
* Se a propriedade de destino tiver uma versão mais alta da extensão instalada, as configurações são copiadas, mas não é feito o downgrade. A propriedade de destino ainda mantém o número de versão atual.

## Como copiar regras e elementos de dados

Todas as regras e elementos de dados são fornecidos por uma extensão, portanto, ao copiar para as propriedades, a Platform deverá contabilizar essas extensões subjacentes.

![Como copiar uma regra para minha propriedade de demonstração](../../images/copy-rules-dialog1.png)

A caixa de diálogo Copiar fornece uma explicação sobre exatamente o que ocorrerá antes de você começar a copiar. A caixa de diálogo acima é para uma regra, mas o mesmo se aplica a elementos de dados.

1. **As extensões necessárias para essas regras são copiadas.** Isso permite saber que as extensões necessárias irão juntamente com a regra. Essas cópias seguem as mesmas regras que uma cópia de extensão normal descrita acima.
1. **As configurações de extensão NÃO serão copiadas se a extensão já estiver instalada.** Isso significa que, se as extensões necessárias já existirem na propriedade de destino, a extensão permanecerá como está. Se você quiser copiar as configurações de extensão também, poderá usar a opção **Substituir configurações de extensão na propriedade de destino** e a explicação será atualizada adequadamente.
1. **Os elementos de dados exigidos por essas regras NÃO serão copiados.** Essa explicação se aplica somente às regras. As regras geralmente dependem de elementos de dados para funcionar corretamente. Se você copiar uma regra para uma nova propriedade, também precisará copiar todos os elementos de dados necessários como uma ação separada.
