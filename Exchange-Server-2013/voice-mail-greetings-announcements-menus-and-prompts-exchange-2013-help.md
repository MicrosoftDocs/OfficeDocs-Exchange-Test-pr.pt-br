---
title: 'Saudação da caixa postal, anúncios, menus e prompts: Exchange 2013 Help'
TOCTitle: Saudação da caixa postal, anúncios, menus e prompts
ms:assetid: df61105d-c9d8-452c-b028-50cbda47aecf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124902(v=EXCHG.150)
ms:contentKeyID: 54651986
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Saudação da caixa postal, anúncios, menus e prompts

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-03-09_

Quando você instala a Unificação de mensagens (UM), um conjunto comum padrão de arquivos de áudio usado para o sistema de caixa postal e para comunicados informativos, saudações e prompts de menu é instalado. Embora você possa criar um totalmente funcional auto attendant ou discagem plano UM que usa apenas os prompts de áudio padrão, esses prompts são muito genéricas para servir como uma interface pública aceitável para muitas empresas. Este tópico aborda o sistema e os prompts de menu, saudações e informativos comunicados que são usados pelos planos de discagem de Unificação de mensagens e atendedores automáticos e como elas são usadas quando os chamadores acessar o sistema de caixa postal.

**Sumário**

Visão geral de prompts de áudio e saudações

Prompts de sistema

Anúncios e saudações de plano de discagem de Unificação de mensagens

Saudações Atendedor de automático de Unificação de mensagens, comunicados e os prompts de menu

Personalizar o menu de saudações e anúncios solicita

## Visão geral de prompts de áudio e saudações

Depois de Unificação de mensagens estiver instalado, planos de discagem de arquivos de áudio para Unificação de mensagens e atendedores automáticos são copiados para o servidor de caixa de correio. Por padrão, o programa de instalação copia os arquivos de áudio para a pasta do programa Files\\Microsoft\\Exchange Server\\V15\\Unified Messaging\\Prompts*\\\<language\>* . Se você instalou a versão em inglês dos EUA, uma pasta denominada \\en é criada durante a instalação para armazenar as versões de inglês dos EUA os prompts de sistema. O servidor de caixa de correio é reproduzido esses prompts de sistema para os chamadores para que eles podem ouvir saudações e prompts de menu informativos comunicados e, portanto, eles podem navegar os menus de Unificação de mensagens.

Esses arquivos de áudio do sistema ou prompts nunca devem ser substituídos. No entanto, Unificação de mensagens permite que você personalize UM dial plan e auto attendant boas-vindas saudações, os prompts de menu principal e comunicados informativos.

A tabela a seguir resume os prompts e planos de discagem de saudações usadas com a Unificação de mensagens.

### Planos de discagem de prompts de áudio para Unificação de mensagens

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompts e saudações</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Prompts de sistema</p></td>
<td><p>Não deve ser modificado.</p></td>
</tr>
<tr class="even">
<td><p>Saudação de boas-vindas</p></td>
<td><p>A saudação de boas-vindas padrão é um prompt de sistema que será tocado por padrão. No entanto, você pode usar um arquivo de saudação personalizada que você criar.</p></td>
</tr>
<tr class="odd">
<td><p>Informe</p></td>
<td><p>Por padrão, anúncios informativos são desabilitados. Se você habilitar um informe, você deve especificar um arquivo de saudação personalizada.</p></td>
</tr>
</tbody>
</table>


A tabela a seguir resume os prompts e saudações usadas com atendedores automáticos.

### Prompts de áudio para atendedores automáticos

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Prompts e saudações</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Prompts de sistema</p></td>
<td><p>Não deve ser modificado.</p></td>
</tr>
<tr class="even">
<td><p>Prompts de menu do horário comercial</p></td>
<td><p>Por padrão, o horário comercial prompts de menu é ativado e um prompt de sistema será reproduzido. No entanto, você pode usar um arquivo de saudação personalizada que você criar.</p></td>
</tr>
<tr class="odd">
<td><p>Prompts de menu de horário não comercial</p></td>
<td><p>Por padrão, os prompts de menu horário não comercial são ativados e um prompt de sistema será reproduzido. No entanto, você pode usar um arquivo de saudação personalizada que você criar.</p></td>
</tr>
<tr class="even">
<td><p>Saudação para horário comercial</p></td>
<td><p>Por padrão, um horário comercial saudação está habilitada e um prompt de sistema é reproduzido. No entanto, você pode usar um arquivo de saudação personalizada que você criar. Isso também é conhecido como uma saudação de boas-vindas.</p></td>
</tr>
<tr class="odd">
<td><p>Saudação para horário comercial</p></td>
<td><p>Por padrão, um horário não comercial saudação é ativado e um prompt de sistema será reproduzido. No entanto, você pode usar um arquivo de saudação personalizada que você criar. Isso também é conhecido como uma saudação de boas-vindas.</p></td>
</tr>
<tr class="even">
<td><p>Informe</p></td>
<td><p>Por padrão, anúncios informativos são desabilitados. Se você habilitar um informe, você deve especificar um arquivo de saudação personalizada.</p></td>
</tr>
</tbody>
</table>



> [!CAUTION]
> Modificar os prompts de sistema instalado não é suportado.



Voltar ao início

## Prompts de sistema

A Unificação de mensagens é instalado com um conjunto de prompts de áudio padrão para uso com Outlook acesso de voz, planos de discagem e atendedores automáticos. Centenas de solicitações do sistema para cada idioma estão instaladas em um servidor de caixa de correio. O servidor de caixa de correio reproduz os arquivos de áudio para esses prompts de sistema aos chamadores quando eles acessarem o sistema de caixa postal. Eis alguns exemplos de como esses prompts do sistema:

  - "Por favor, insira seu PIN".

  - "Para acessar sua caixa de correio, insira sua extensão".

  - "Para contatar uma pessoa, pressione a tecla \#".

  - "O nome da pessoa que você está chamando de ortografia, Sobrenome pela primeira vez."

  - "Para acessar uma pessoa específica, basta conte-me o nome."


> [!CAUTION]
> Modificar os prompts de sistema instalado não é suportado.




> [!NOTE]
> Quando o serviço de Unificação de mensagens é iniciado no servidor de caixa de correio, ele verificará todos o sistema solicita que estão disponíveis. Se não for encontrado um prompt do sistema, a Unificação de mensagens retornará um erro. Para corrigir o erro que é retornado, localize o evento usando o Visualizador de eventos e copie o arquivo listado na janela de <STRONG>Propriedades de evento</STRONG> de DVD de instalação para a pasta apropriada no servidor de caixa de correio.



## Anúncios e saudações de plano de discagem de Unificação de mensagens

Depois de instalar o servidor de caixa de correio e criar um plano de discagem de UM, você tem a opção para usar os arquivos de áudio para os prompts de sistema padrão que são criados durante a instalação ou para criar arquivos de áudio personalizados que podem ser usados com os planos de discagem de Unificação de mensagens.

Planos de discagem de Unificação de mensagens tem uma saudação de boas-vindas e um informe opcional que é possível modificar. A saudação de boas-vindas é usada quando um usuário do Outlook Voice Access ou outro chamador chama o número de acesso do assinante. Os chamadores ouvem uma bem-vindo do padrão de saudação que diz: "Bem-vindo, você está conectado à MicrosoftExchange." Talvez você queira alterar a saudação este padrão e oferecem uma alternativa bem-vindo saudação específico para sua empresa, por exemplo, "Bem-vindo ao Outlook Voice Access para Woodgrove Bank". Se você personalizar essa saudação, você pode gravar a saudação personalizada e salvá-lo como um arquivo. wav e, em seguida, você pode configurar o plano de discagem para usar essa saudação personalizada.

A Unificação de mensagens permite um informe a seguir a saudação de boas-vindas. Por padrão, não há nenhuma informe configurado. No entanto, convém fornecer uma para os chamadores. Você pode usar o informe para comunicados gerais que mudam com mais freqüência a saudação de boas-vindas ou anúncios exigidos pelo políticas de conformidade corporativa. Quando é importante que o informe toda é ouvido, você poderá configurá-lo para ser ininterrupto. Isso impede que um chamador pressionar uma tecla ou falando de um comando para interromper e parar o informe.

A tabela a seguir descreve as saudações de plano de discagem de Unificação de mensagens e comunicados informativos.

### Saudações de plano de discagem de Unificação de mensagens e comunicados informativos

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Saudação</th>
<th>Exemplo de padrão</th>
<th>Exemplo de personalizada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Saudação de boas-vindas</p></td>
<td><p>&quot;Bem-vindo, que você está conectado à MicrosoftExchange.&quot;</p></td>
<td><p>&quot;Bem-vindo à Outlook o acesso de voz do Woodgrove Bank.&quot;</p></td>
</tr>
<tr class="even">
<td><p>Informe</p></td>
<td><p>Por padrão, um informe não está configurado.</p></td>
<td><p>&quot;Usando esse sistema você concorda em cumprir todas as políticas corporativas quando você estiver acessando este sistema.&quot;</p></td>
</tr>
</tbody>
</table>


Quando você estiver personalizando e configurando saudações e avisos, verifique se a configuração de idioma configurada em UM discar plano é o mesmo idioma do custom solicita que você criar. Caso contrário, um chamador pode ouvir uma mensagem ou saudação em um idioma e outra mensagem ou saudação em um idioma diferente.

Voltar ao início

## Saudações Atendedor de automático de Unificação de mensagens, comunicados e os prompts de menu

Como planos de discagem com a Unificação de mensagens, atendedores automáticos têm uma saudação de boas-vindas, um informe opcional e um prompt do menu personalizado opcional. Você pode definir diferentes versões do prompt do menu e saudação de boas-vindas para horário comercial e o horário não comercial. Você pode modificar todos eles.

A saudação de boas-vindas é que a primeira coisa que um chamador ouve quando um atendedor automático de UM atende a chamada. Por padrão, isso diz: "Bem-vindo ao atendedor automático daExchangeMicrosoft." O arquivo de áudio que será tocado para a chamada é o prompt do sistema padrão para o atendedor automático de UM. No entanto, convém fornecer uma alternativa saudação específico para sua empresa, por exemplo, "Obrigado por contatar Woodgrove Bank." Para personalizar essa saudação de boas-vindas, registre a saudação personalizada e salvá-lo como um arquivo. wav e, em seguida, configurar o atendedor automático para usar essa saudação personalizada. Conforme com as saudações de boas-vindas, você também pode personalizar o menu solicita.

A Unificação de mensagens também permite que um informe a seguir uma saudação para horário comercial ou uma saudação horários não-comerciais. Por padrão, nenhuma informe está configurado, mas talvez você queira fornecer um para chamadores. O informe pode anunciar horário comercial da sua empresa, por exemplo, "nosso horário comercial estão das 8:00 às 17:00 horas segunda à sexta e 8:30 A.M. às 1:00 horas no sábado". O informe também pode fornecer as informações necessárias para fins de conformidade com as políticas corporativas, por exemplo, "chamadas podem ser monitoradas para fins de treinamento." Quando é importante que o informe toda é ouvido, você poderá configurá-lo para ser ininterrupto. Isso impede que o chamador do pressionando uma tecla ou falando de um comando para interromper e parar o informe.

A tabela a seguir descreve as saudações Atendedor de automático de Unificação de mensagens e comunicados informativos.

### Saudações Atendedor de automático de Unificação de mensagens, informe e os prompts de menu

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Saudação</th>
<th>Exemplo de padrão</th>
<th>Exemplo de personalizada</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Saudação para horário comercial</p></td>
<td><p>&quot;Bem-vindo para o atendedor automático da Microsoft Exchange.&quot;</p></td>
<td><p>&quot;Obrigado por contatar Woodgrove Bank.&quot;</p></td>
</tr>
<tr class="even">
<td><p>Saudação para horário comercial</p></td>
<td><p>Sem padrão não - saudação para horário comercial é tocado enquanto configurar o horário comercial para o atendedor automático. No entanto, os negócios saudação para horário é reproduzido para chamadores durante todos os horários do dia.</p></td>
<td><p>&quot;Você atingiu Woodgrove Bank após o horário comercial. Nossos horários comerciais são de 8:00 até 17:00 horas, de segunda à sexta-feira.&quot;</p></td>
</tr>
<tr class="odd">
<td><p>Informe</p></td>
<td><p>Por padrão, anúncios informativos não são configurados.</p></td>
<td><p>&quot;Chamadas podem ser monitoradas para fins de treinamento.&quot;</p></td>
</tr>
<tr class="even">
<td><p>Prompt do menu principal de horário comercial</p></td>
<td><p>Sem padrão de expediente prompt do menu principal será reproduzido até configurar mapeamentos de teclas no atendedor automático.</p></td>
<td><p>&quot;Para suporte técnico, pressione ou Fale 1. Para escritórios corporativos e administração, pressione ou Fale 2. Para vendas, pressione ou Fale 3.&quot;</p></td>
</tr>
<tr class="odd">
<td><p>Prompt do menu principal de horário não comercial</p></td>
<td><p>Sem prompt do menu principal de horário não comercial padrão será reproduzido até configurar mapeamentos de teclas e a agenda de horário comercial no atendedor automático.</p></td>
<td><p>&quot;Sua chamada é muito importante para nós. No entanto, você chegou Woodgrove Bank após o horário comercial. Se você deseja deixar uma mensagem, pressione ou dizer 1 e podemos irá retornar sua chamada assim que possível.&quot;</p></td>
</tr>
</tbody>
</table>


Como com planos de discagem de Unificação de mensagens, certifique-se a configuração de idioma configurada no atendedor automático de UM é o mesmo idioma das saudações personalizadas, criar e é definido como o mesmo idioma a UM plano de discagem. Caso contrário, um chamador pode ouvir uma mensagem ou saudação em um idioma e outra mensagem ou saudação em um idioma diferente.

Voltar ao início

## Personalizando saudações, anúncios e os prompts de menu e menus de navegação

Embora os prompts de sistema não deve ser substituídos ou alterados, você provavelmente desejará personalizar as saudações, os anúncios informativos prompts de menu e menus de navegação usados com a Unificação de mensagens, planos de discagem e atendedores automáticos de um. Após a instalação, você pode configurar os planos de discagem de Unificação de mensagens e atendedores automáticos para usar arquivos de áudio personalizados (. wav ou. wma). Para poder habilitar prompts de voz personalizada para os chamadores, você deve seguir estas etapas:

1.  Registre as saudações personalizadas, anúncios e prompts e, em seguida, salvar como arquivos. wav. O PCM Linear (16 bit/amostra), 8 quilohertz (kHz) codec de áudio deve ser usado para codificar os arquivos. wav. Se você não usar esse formato específico para os arquivos. wav, será gerado um erro informando que o arquivo de origem está em um formato sem suporte. Embora um erro é gerado, o erro não aparecerá no Visualizador de eventos.

2.  Configurar UM plano de discagem ou usar as saudações personalizadas, anúncios e prompts de atendedor automático.

Por padrão, quando você cria um atendedor automático de UM, os negócios e saudações de horário não comercial ou prompts não estão configurados e nenhum mapeamentos de teclas são definidos para a empresa ou prompts de menu principal de horário não comercial. Para configurar corretamente personalizadas saudações e prompts para um atendedor automático, você deve:

  - Configure o horário não comercial e negócios na página **horário comercial**.

  - Crie os arquivos de (. wav ou. wma) de áudio de saudação que serão usados para saudações de boas-vindas do horário não comercial e de negócios.

  - Configure os negócios e saudações de boas-vindas do horário não comercial na página **saudações**.

  - Crie os arquivos de saudação que serão usados para saudações prompt do menu principal de horário não comercial e de negócios.

  - Configure os negócios e saudações prompt do menu principal de horário não comercial na página **saudações**.

  - Habilitar e configurar a navegação de menu comerciais e o horário não comercial na página **navegação de Menu**.

Voltar ao início

