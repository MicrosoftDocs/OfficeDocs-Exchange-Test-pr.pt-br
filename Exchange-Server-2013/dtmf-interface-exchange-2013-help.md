---
title: 'Interface DTMF: Exchange 2013 Help'
TOCTitle: Interface DTMF
ms:assetid: 2c7c9d8a-ed12-4dcf-a5b7-3cea0e785e49
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996919(v=EXCHG.150)
ms:contentKeyID: 54651933
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Interface DTMF

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Na UM (Unificação de Mensagens), os chamadores podem usar DTMF (Dual Tone Multi-frequency), também conhecido como discagem por tom, e entradas de voz para interagir com o sistema. Os métodos que os chamadores podem usar depende de como os planos de discagem de UM e os atendedores automáticos estão configurados.

A interface DTMF permite que os chamadores usem o teclado numérico do telefone para localizar usuários e navegar no sistema de menu da UM quando eles chamam um número do Outlook Voice Access configurado em um plano de discagem ou quando chamam um número de telefone configurado em um atendedor automático. Este tópico aborda a interface DTMF e como ela é usada por chamadores para localizar usuários e para navegar no sistema de menus de caixa postal da UM.

**Sumário**

DTMF overview

UM dial plans and dial by name

DTMF maps

DTMF maps for users who aren't enabled for Unified Messaging

DTMF maps for users who are enabled for Unified Messaging

For more information

## Visão geral sobre DTMF

DTMF exige que um chamador pressione uma tecla no teclado numérico do telefone que corresponda a uma opção do menu de Unificação de Mensagens ou que insira um nome de usuário ou alias de email usando as letras nas teclas para escrever o nome ou o alias. Os chamadores podem usar DTMF, porque o ASR (Reconhecimento Automático de Fala) não foi habilitado ou porque eles tentaram usar comandos de voz e não conseguiram. Em qualquer um dos casos, as entradas de DTMF são usadas para navegar em menus e procurar usuários.

Por padrão, na UM, as entradas de DTMF são usadas em planos de discagem e são a interface padrão dos chamadores para atendedores automáticos de UM.

Os chamadores podem usar as entradas de DTMF para:

  - Acesso de discagem ao plano de discagem usando o Outlook Voice Access.

  - Consultas e pesquisas do diretório de plano de discagem para localizar usuários.

  - Atendedores automáticos que não sejam habilitados para fala.

  - Atendedores automáticos habilitados para fala que tenham ou não um atendedor automático de fallback de DTMF configurado.

  - Atendedores automáticos de fallback de DTMF (não habilitados para fala).

## Planos de discagem de UM e discagem por nome

Ao criar um plano de discagem de UM, você pode configurar o método de entrada primário e secundário que os chamadores usam para consultar nomes quando procuram um usuário ou desejam entrar em contato com um usuário. Essas configurações estão localizadas na página **Configurações** do plano de discagem e são chamadas de **Modo principal de pesquisar nomes** e **Modo secundário de pesquisar nomes**. As opções a seguir estão disponíveis para os modos principal e secundário de pesquisa de nomes:

  - Sobrenome Nome

  - Nome Sobrenome

  - Endereço SMTP

Além disso, **Nenhum** é uma opção disponível para o modo secundário de pesquisar nomes.

Por padrão, **Sobrenome Nome** está selecionado como o modo principal de pesquisar nomes e **Endereço SMTP** está selecionado como o modo secundário de pesquisar nomes. Portanto, quando um chamador disca um número do Outlook Voice Access configurado no plano de discagem de UM, a mensagem de boas-vindas do plano de discagem é reproduzida e o operador diz algo como, "Bem-vindo ao Contoso Outlook Voice Access. Para acessar sua caixa de correio, digite seu ramal. Para entrar em contato com alguém, pressione a tecla de cerquilha". Depois que o chamador pressionar a tecla \#, o sistema responderá "Soletre o nome da pessoa que você está chamando, sobrenome primeiro, ou, para soletrar o alias do email, pressione a tecla \# duas vezes." Nesse cenário, dependendo de como o plano de discagem está configurado, o sistema solicitará que o chamador insira o sobrenome do usuário e depois o nome (Sobrenome Nome) do usuário ou que soletre o alias do email, excluindo o nome de domínio. Por exemplo, se o alias de email do usuário for tsmith@contoso.com, o chamador digitará tsmith.

Se você desejar alterar essa configuração, pois a definição padrão não atende às suas necessidades, poderá alterá-la para permitir que os chamadores insiram o alias de email do usuário primeiro ou o nome do usuário seguido por seu sobrenome. Nesse caso, você configurará o **Modo principal de pesquisar nomes** com a configuração **Endereço SMTP** e o **Modo secundário de pesquisar nomes** com a configuração **Nome Sobrenome**. As configurações dos métodos de discagem por nome também se aplicarão a todos os atendedores automáticos de UM que estejam associados ao plano de discagem. Para que os chamadores possam inserir o nome do usuário usando as entradas de DTMF ou as teclas do teclado numérico do telefone, um mapa DTMF e os valores para o usuário deverão existir no diretório de sua organização.

Para obter mais informações sobre como alterar os métodos principal e secundário de discagem por nome em um plano de discagem da UM, consulte [Configurar a principal maneira para os usuários do Outlook Voice Access pesquisar](configure-the-primary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md) e [Configurar o modo secundário para os usuários do Outlook Voice Access pesquisar](configure-the-secondary-way-for-outlook-voice-access-users-to-search-exchange-2013-help.md).

Voltar ao início

## Mapas DTMF

Em uma organização do Exchange, um atributo denominado **msExchUMDtmfMap** é associado a cada usuário criado no diretório. A Unificação de Mensagens usa esse atributo para mapear o nome, sobrenome e alias de email do usuário para um conjunto de números. Esse mapeamento é chamado de mapa DTMF. Um mapa DTMF permite que um chamador insira os dígitos no teclado numérico do telefone correspondentes às letras do nome do usuário ou do alias de email. Esse atributo contém os valores necessários para criar um mapa DTMF para o nome do usuário seguido por seu sobrenome, para o sobrenome do usuário seguido por seu nome e para o alias de email do usuário.

A tabela a seguir mostra os valores do mapa DTMF que são armazenados no Active Directory no atributo **msExchUMDtmfMap** para um usuário habilitado para UM, chamado Tony Smith, com um alias tsmith@contoso.com.

**Os valores de DTMF armazenados para um usuário habilitado para UM chamado Tony Smith**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Entrada de diretório</th>
<th>Nome do usuário</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><ul>
<li><p>firstNameLastName:866976484</p></li>
</ul></td>
<td><p>tonysmith</p></td>
</tr>
<tr class="even">
<td><ul>
<li><p>lastNameFirstName:764848669</p></li>
</ul></td>
<td><p>smithtony</p></td>
</tr>
<tr class="odd">
<td><ul>
<li><p>emailAddress:876484</p></li>
</ul></td>
<td><p>tsmith</p></td>
</tr>
</tbody>
</table>


Os nomes e os aliases de email podem conter outros caracteres não alfanuméricos, como vírgulas, hifens, sublinhados ou pontos. Caracteres como esses não serão usados em um mapa DTMF de um usuário. Por exemplo, se o alias de email para Tony Smith for tony-smith@contoso.com, o valor do mapa DTMF será 866976484, e o hífen não será incluído. No entanto, se o alias de email de um usuário contiver um ou mais números, por exemplo, tonysmith123@contoso.com, os números serão usados no mapa DTMF criado. O mapa DTMF para tonysmith123 será 866976484123.

É necessário ter um mapa DTMF de um usuário, para que os chamadores possam inserir o nome do usuário ou o alias de email. No entanto, nem todos os usuários terão um mapa DTMF associado a suas contas.

Voltar ao início

## Mapas DTMF para usuários que não estão habilitados para Unificação de Mensagens

Usuários, incluindo os habilitados para caixa de correio, não estão habilitados para Unificação de Mensagens por padrão. O atributo **msExchUMDtmfMap** é preenchido com os valores necessários para os mapas DTMF para usuários que não foram habilitados para UM. Por padrão, os mapas de DTMF a seguir foram criados para todos os usuários quando uma caixa de correio foi criada para eles:

1.  emailAddress

2.  firstNameLastName

3.  lastNameFirstName

Se um usuário não tiver valores de mapa DTMF definidos para sua conta, os chamadores não poderão entrar em contato com o usuário quando pressionarem uma tecla do telefone em um menu de atendedor automático da UM ou quando realizarem uma pesquisa de diretório. Além disso, usuários habilitados para UM não poderão enviar mensagens ou transferir chamadas para usuários que não tenham um mapa DTMF, a menos que eles possam usar o Reconhecimento Automático de Fala (ASR). Para que os chamadores transfiram chamadas ou entrem em contato com usuários não habilitados para UM usando o teclado numérico do telefone, é preciso criar os valores necessários para o mapa DTMF desses usuários. Você pode usar o cmdlet **Set-User** com o parâmetro *-CreateDtmfMap* para criar e atualizar um mapa DTMF de usuário único ou atualizar um mapa DTMF para um usuário se o nome do usuário tiver sido alterado após a criação de um mapa DTMF. Opcionalmente, você poderá criar um script do Shell de Gerenciamento do Exchange usando esse cmdlet para atualizar os valores do mapa DTMF para vários usuários.

Para obter mais informações sobre o cmdlet **Set-User**, consulte [Set-User](https://technet.microsoft.com/pt-br/library/aa998221\(v=exchg.150\)).

Voltar ao início

## Mapas DTMF para usuários que não estão habilitados para Unificação de Mensagens

Por padrão, um mapa DTMF é criado para um usuário quando ele está habilitado para Unificação de Mensagens. Isto possibilita que as chamadas sejam transferidas de chamadores externos para um usuário habilitado para UM, de usuários não habilitados para UM e de outros usuários habilitados para UM que usam o teclado numérico do telefone para escrever o nome do usuário ou o alias de email.

Depois que os valores do mapa DTMF forem criados para um usuário habilitado para UM, os chamadores poderão usar o recurso de pesquisa de diretório. Os chamadores usam a pesquisa de diretório quando usam o teclado numérico do telefone nas seguintes situações:

  - Para identificar ou procurar um usuário quando ele liga para um número do Outlook Voice Access.

  - Para localizar ou transferir chamadas para um usuário habilitado para UM quando ele liga para um atendedor automático de UM.

Para obter mais informações sobre como habilitar um usuário para Unificação de Mensagens, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

Às vezes, o nome, o sobrenome ou o alias de email de um usuário mudam depois que ele é habilitado para UM. Os valores do mapa DTMF do usuário não são atualizados automaticamente. Se um chamador inserir o novo sobrenome ou alias de email do usuário, e o mapa DTMF do usuário não tiver sido atualizado para refletir a alteração no nome ou no alias de email, o chamador não conseguirá localizar o usuário no diretório, enviar uma mensagem ao usuário ou transferir chamadas para o usuário. Se tiver que atualizar o mapa DTMF de um usuário depois que ele tiver sido habilitado para UM, você poderá usar o cmdlet **Set-User** com o parâmetro *-CreateDtmfMap*. Você também poderá criar um script do Shell de Gerenciamento do Exchange usando esse cmdlet se desejar atualizar os mapas DTMF para vários usuários habilitados para UM.


> [!WARNING]
> Não recomendamos alterar manualmente os valores de DTMF para usuários usando uma ferramenta como ADSI Edit, pois poderão ocorrer configurações inconsistentes ou outros erros. Recomendamos que você use apenas o cmdlet <STRONG>Set-UMService</STRONG> ou o cmdlet <STRONG>Set-User</STRONG> para criar ou atualizar os mapas DTMF para os usuários.



## Para obter mais informações

[Visão geral do Adsiedit](https://go.microsoft.com/fwlink/p/?linkid=73175)

