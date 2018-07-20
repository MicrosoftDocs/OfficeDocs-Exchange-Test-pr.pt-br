---
title: 'Códigos de discagem, prefixos de número e formatos de número: Exchange Online Help'
TOCTitle: Códigos de discagem, prefixos de número e formatos de número
ms:assetid: 26d61e55-f8dd-4d25-81f1-78a87cf88bad
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb266967(v=EXCHG.150)
ms:contentKeyID: 51407849
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Códigos de discagem, prefixos de número e formatos de número

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-05-04_

Você pode configurar vários códigos de discagem usados pela UM (Unificação de Mensagens) para fazer chamadas internas e externas para usuários habilitados para UM. Com frequência, você desejará configurar um plano de discagem junto com os códigos de discagem ou de acesso, um prefixo de número nacional/regional ou os formatos de número internacionais ou de país/região para que possa controlar a discagem externa para usuários em sua organização. Este tópico discute códigos de discagem, prefixos de número e formatos de número e como é possível usá-los para controlar a discagem externa em sua organização.

**Sumário**

Visão geral

Código de acesso de linha externa

Prefixo de número nacional/regional

Código de acesso de país/região

Código de acesso internacional

Formatos numéricos de país/região e internacionais

## Visão geral

*Discagem externa* é o processo no qual os usuários ligam para um plano de discagem da UM ou atendedor automático da UM e fazem uma chamada para um número de telefone interno ou externo. Quando um usuário liga para um plano de discagem da UM ou um atendedor automático da UM e faz uma chamada, a Unificação de Mensagens usa as definições configuradas no plano de discagem, o atendedor automático e as diretivas de caixa de correio da UM para fazer a chamada. A UM faz uma chamada de saída nas seguintes situações:

  - Quando liga para um número de telefone externo de um chamador

  - Quando transfere uma chamada para um atendedor automático

  - Quando transfere uma chamada para um usuário (habilitado ou não para UM) em sua organização

  - Quando um usuário habilitado para UM usa o recurso Tocar no Telefone

Dois tipos de usuários usam a discagem externa: usuários autenticados e usuários não autenticados. Os usuários não autenticados ligam para um número do Outlook Voice Access configurado em um plano de discagem da UM, mas não entram em suas caixas de correio. Os usuários autenticados também ligam para um número configurado em um atendedor automático da UM. Usuários autenticados ligam para um número do Outlook Voice Access e entram com êxito em suas caixas de correio. Quando usuários ligam para um número do Outlook Voice Access, eles são considerados inicialmente não autenticados, pois não forneceram seus números de ramal e PIN e não entraram em suas caixas de correio. Eles são autenticados depois de fornecer o número de ramal e PIN e entram com êxito em suas caixas de correio.

Quando um usuário não autenticado liga para um atendedor automático da UM e faz uma chamada usando discagem externa, as configurações da discagem externa configuradas no plano de discagem da UM e o atendedor automático são utilizados. Quando um usuário não autenticado liga para um número do Outlook Voice Access configurado em um plano de discagem, apenas as definições configuradas no plano de discagem são usadas. Quando um usuário entra com êxito em sua caixa de correio, as definições de configuração do plano de discagem e a política de caixa de correio da UM associadas ao usuário autenticado são aplicadas ao usuário autenticado.

É necessário definir várias configurações para controlar a discagem externa para sua organização. Para controlar a discagem externa, é necessário configurar os planos de discagem da UM, os atendedores automáticos e as políticas de caixa de correio da UM na Unificação de Mensagens. As seguintes definições podem ser configuradas em planos de discagem da UM, atendedores automáticos e diretivas de caixa de correio da UM para controlar a discagem externa:

  - Códigos de acesso para linha externa, local/região e internacional

  - Prefixos de número nacional/regional

  - Formatos numéricos de país/região e internacionais

  - Grupos de regras de discagem no país/região e internacional

  - Grupos permitidos de regras de discagem do país/região e internacionais

  - Entradas de regras de discagem

Configure os códigos de acesso, prefixos de número e formatos de número em um plano de discagem UM na página **Códigos de Discagem** no Centro de administração do Exchange (EAC). Também é possível definir as configurações usando o cmdlet **Set-UMDialPlan** no Shell de Gerenciamento do Exchange. Você pode optar por configurar todas as definições, nenhuma das definições ou somente algumas das definições. Cada definição controla uma parte específica do processo de discagem externa.

A UM usa códigos de acesso, prefixos de número e formatos de número para determinar o número correto para discagem. Eles podem ser configurados para restringir as chamadas de saída para usuários que discam para um atendedor automático de UM com um plano de discagem de UM ou que discam para o número do Outlook Voice Access configurado no plano de discagem.

Para mais informações sobre discagem externa em Unificação de Mensagens, consulte [Códigos de discagem, prefixos de número e formatos de número](dial-codes-number-prefixes-and-number-formats-exchange-2013-help.md).

Voltar ao início

## Código de acesso de linha externa

Você pode configurar um código de acesso à linha externa, conhecido também como um *código de acesso ao tronco*, em cada plano de discagem criado. Esse é o número usado para obter acesso a uma linha telefônica externa. Esse número também é configurado nos PBXs (Private Branch eXchanges) ou nos PBXs IP de sua organização. Na maioria das redes telefônicas, os usuários discam o número 9 para obter acesso a uma linha externa e fazer uma chamada para um número de telefone externo.

Você deve configurar um código de acesso de linha externa em cada plano de discagem que criar. Esse código de discagem será aplicado a todos os usuários vinculados a uma política de caixa de correio da UM vinculada, por sua vez, ao plano de discagem de UM. Quando um chamador vinculado ao plano de discagem faz uma chamada e o plano de discagem disca a chamada externa, a UM adiciona o código de acesso de linha externa (normalmente 9) em frente à cadeia de números discados de modo que o PBX ou PBX IP possa discar o número corretamente. Se você não configurar o código de acesso de linha externa, talvez o PBX ou PBX IP não reconheça o número enviado.. Por exemplo, conforme descrito anteriormente, em muitas organizações, o código de acesso que os usuários discam para obter acesso a uma linha externa é 9, e isso está configurado em um PBX ou um PBX IP. A Unificação de Mensagens deve acrescentar o código de acesso de linha externa (9) antes da cadeia de caracteres numéricos de telefone para o PBX ou PBX IP para discar corretamente o número de discagem externa. Se você configurar o código de discagem para que a Unificação de Mensagens acrescente o código de acesso à linha externa, a Unificação de Mensagens poderá usar o código de acesso à linha externa para obter acesso a uma linha externa antes de discar a cadeia de caracteres do número de telefone externo. O código de discagem configurado será aplicado a todos os usuários vinculados a uma política de caixa de correio da UM vinculada ao plano de discagem da UM.

## Prefixo de número nacional/regional

O prefixo de número nacional/regional e o código do país/região também podem ser configurados em um plano de discagem da UM. O número digitado é usado pela Unificação de Mensagens para discar o prefixo de número nacional/regional correto ou o código do país/região quando um usuário faz uma chamada externa com destino no mesmo país/região ou quando faz uma chamada internacional. Por exemplo, quando um usuário da América do Norte faz uma chamada externa internacional para a Europa, a UM acrescentará um prefixo de número nacional/regional à cadeia de caracteres do número que ele envia ao PBX ou PBX IP para fazer a chamada externa. O número 1 é usado como o prefixo de número nacional/regional na América do Norte.

## Código de acesso de país/região

Um código do país/região pode ser configurado em um plano de discagem da UM. O código de acesso do país/região consiste em dígitos associados a um país ou uma região específico. O código de acesso do país/região é usado pela Unificação de Mensagens para discar o número de telefone correto quando uma chamada for feita para um número de telefone de dentro do mesmo país ou região. A UM acrescentará esse número antes da cadeia de caracteres de números que ele envia ao PBX ou ao PBX IP quando faz a chamada externa. Por exemplo, a UM acrescentará o número 1 a uma chamada feita dos Estados Unidos cujo destino for os Estados Unidos. Para o Reino Unido, o código de país/região é 44.

## Código de acesso internacional

Um código de acesso internacional pode ser configurado em um plano de discagem da UM. O código de acesso internacional consiste nos dígitos usados para acessar números de telefone internacionais. O código de acesso internacional é usado pela Unificação de Mensagens para discar o código de acesso internacional correto quando uma chamada for feita de um número de telefone dentro de um país/região e o número que estiver sendo discado estiver localizado em outro país/região. A UM acrescentará esse número antes da cadeia de caracteres de números que ele envia ao PBX ou ao PBX IP quando faz a chamada externa. Por exemplo, a UM usará 011 como o código de acesso internacional para os Estados Unidos. Para a Europa, o código de acesso internacional é 00.

Voltar ao início

## Formatos numéricos de país/região e internacionais

Você pode definir a configuração de chamada de entrada para formatos de número no país/região e internacional em um plano de discagem da UM. Depois de definir essas configurações, a Unificação de Mensagens poderá reconhecer chamadas de entrada de dentro de um país/região e internacionalmente entre planos de discagem da UM dentro da mesma organização. Também é possível adicionar formatos de número para chamadas de entrada feitas dentro de um único plano de discagem. Configurar essas opções permite que sua organização economize dinheiro, impedindo chamadas externas que não devam ser feitas por usuários de dentro da organização e ajuda a evitar fraude na conta. A UM usará as informações que você configurar para examinar o formato de número da chamada de entrada e verificar se o padrão de número corresponde, antes de aceitar a chamada. Por exemplo, você pode ter vários planos de discagem dentro de uma organização. Se você tiver um plano de discagem para os Estados Unidos e outro para o Reino Unido, deverá permitir que a UM dos usuários do plano de discagem nos Estados Unidos faça ligações para usuários localizados no plano de discagem do Reino Unido, mas não permitam que usuários do plano de discagem dos Estados Unidos liguem diretamente para outros países/regiões ou internacionalmente.

