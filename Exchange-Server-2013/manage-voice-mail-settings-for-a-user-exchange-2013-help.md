---
title: 'Gerenciar configurações de caixa postal de um usuário: Exchange 2013 Help'
TOCTitle: Gerenciar configurações de caixa postal de um usuário
ms:assetid: 73957938-048a-4f9c-bd0f-a3c2c3dcd638
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998851(v=EXCHG.150)
ms:contentKeyID: 50485927
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciar configurações de caixa postal de um usuário

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2013-02-22_

Você pode exibir ou definir os recursos de correio de voz e Unificação de mensagens (UM) e definições de configuração de um usuário que foi habilitado para Unificação de mensagens e caixa postal. Por exemplo, você pode fazer o seguinte:

  - Redefina seu PIN do Outlook Voice Access.

  - Adicione um número de ramal do operador pessoal.

  - Adicione outros números de ramal.

  - Ativar ou desativar o reconhecimento automático de fala (ASR).

  - Habilitar ou desabilitar regras de atendimento de chamadas.

  - Habilitar ou desabilitar o acesso ao seu email ou calendário.


> [!TIP]
> Algumas das configurações e recursos só podem ser configuradas usando o Shell.



Para conhecer tarefas de gerenciamento adicionais relacionadas a usuários habilitados para caixa postal, consulte [Procedimentos do usuário habilitado para email de voz](voice-mail-enabled-user-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme se um plano de discagem da UM foi criado. Para obter etapas detalhadas, consulte [Criar um plano de discagem de UM](create-a-um-dial-plan-exchange-2013-help.md).

  - Antes de executar esses procedimentos, verifique se uma política de caixa de correio de UM foi criada. Para obter etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](create-a-um-mailbox-policy-exchange-2013-help.md).

  - Antes de executar esses procedimentos, confirme que o usuário existente no momento é habilitado para Unificação de mensagens. Para obter etapas detalhadas, consulte [Habilitar um usuário para caixa postal](enable-a-user-for-voice-mail-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Usar o EAC para exibir ou configurar as propriedades de um usuário habilitado

1.  No EAC, navegue até **Destinatários** \> **Caixas de correio**.

2.  Na visualização de lista, selecione a caixa de correio para a qual você quer mudar a política de caixa de correio da UM.

3.  No painel de detalhes, em **Telefone e Características de Voz** \> **Unificação de Mensagens**, clique em **Ver detalhes**.

4.  Na página **Caixa de Correio de UM**, clique em **Configurações de caixa de correio de UM** para exibir ou alterar as propriedades de UM para um usuário habilitado para UM existente:
    
      - **Status do PIN**    Este campo apenas para exibição mostra o status da caixa de correio do usuário. Por padrão, quando um usuário está habilitado, o status do PIN está listado como **não bloqueada**. No entanto, se o usuário tem entrada um incorretas Outlook PIN Voice Access várias vezes, o status é listado como **Bloqueada**.
    
      - **Política de caixa de correio de UM**   Esta caixa mostra o nome da política de caixa de correio de UM associada ao usuário habilitado para UM. Você pode clicar em **Procurar** para localizar e especificar a política a ser associada a essa caixa de correio de UM.
    
      - **Ramal pessoal do operador**   Use esta caixa para especificar o número do ramal de operador para o usuário. Por padrão, o número do ramal não está configurado. O tamanho do número do ramal pode ser de 1 a 20 caracteres. Isso permite que as chamadas de entrada para o usuário habilitado para UM sejam encaminhadas ao número de ramal especificado nessa caixa.
        
        Você pode configurar outros tipos de números de ramal do operador em planos de discagem e atendedores automáticos. No entanto, essas extensões geralmente são destinadas recepcionistas de toda a empresa ou operadores. A configuração de extensão do operador pessoal pode ser usada quando um assistente administrativo ou um assistente pessoal atende às chamadas recebidas antes que eles estiver atendidos para que um usuário específico.

5.  Na página **Caixa de Correio de UM**, em **Outras extensões**, você pode adicionar, alterar e exibir números de ramal para o usuário.
    
      - Para adicionar um número de ramal, clique em **Adicionar**![Ícone Adicionar](images/JJ218640.c1e75329-d6d7-4073-a27d-498590bbb558(EXCHG.150).gif "Ícone Adicionar"). Na página **Adicionar outra extensão**, use **Procurar** para selecionar o plano de discagem de UM e digite o número do ramal na caixa **Número do ramal**.
    
      - Para remover um número de ramal, selecione o número que deseja remover e clique em **Remover**![ícone Remover](images/JJ657492.479b6ced-8d64-4277-a725-f17fea202b28(EXCHG.150).gif "ícone Remover").

6.  Se fizer alterações, clique em **Salvar**.

## Usar o Shell para configurar recursos de um usuário habilitado para UM

Este exemplo desabilita a tocar no telefone e notificações de chamadas perdidas, mas permite notificações de mensagem (SMS) do texto.


> [!TIP]
> Para o local e híbrido implantações, quando você estiver integrando a Unificação de mensagens e o Lync Server, chamada não atendida notificações não estão disponíveis para usuários que têm uma caixa de correio localizada em um servidor Exchange 2007 ou caixa de correio do Exchange 2010. Uma notificação de chamada perdida é gerada quando um usuário se desconecta antes que a chamada será enviada para um servidor de caixa de correio.



    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -MissedCallNotificationEnabled $false -PlayonPhoneEnabled $false -SMSMessageWaitingNotificationEnabled $true

Este exemplo impede que um usuário acesse o calendário, mas permite o acesso a email quando o usuário está usando Outlook Voice Access.

    Set-UMMailbox -Identity tony@contoso.com -UMEnabled $true -UMMailboxPolicy AdminPolicy -Extension 523456 -FAXEnabled $true -TUIAccessToCal $false -TUIAccessToEmail True

Este exemplo impede que um usuário acesse o calendário e email quando o usuário está usando Outlook Voice Access.

    Set-UMMailbox -Identity tony@contoso.com -TUIAccessToCalendarEnabled $false -TUIAccessToEmailEnabled $false

Este exemplo impede que um usuário criem chamada atendimento regras, receba faxes de entrada e usando o Outlook Voice Access, mas permite o reconhecimento automático de fala (ASR).

    Set-UMMailbox -Identity tony@contoso.com -AutomaticSpeechRecognitionEnabled $true -CallAnsweringRulesEnabled $false -FaxEnabled $false -SubscriberAccessEnabled $false 

## Usar o Shell para exibir as propriedades de um usuário habilitado

Este exemplo exibe uma lista de todas as caixas habilitado na floresta em uma lista formatada.

    Get-UMMailbox | Format-List

Este exemplo exibe as propriedades da caixa de correio da UM de tonysmith@contoso.com.

    Get-UMMailbox -Identity tonysmith@contoso.com


> [!IMPORTANT]
> Quando você está executando o Exchange 2007 e Exchange 2013 e caixa de correio do usuário está localizado em uma caixa de correio do Exchange 2007 server, executando o cmdlet <STRONG>Get-UMMailbox</STRONG> não funcionarão corretamente. Para resolver o problema, execute o cmdlet de <STRONG>Get-UMMailbox</STRONG> de um servidor Exchange 2007 ou em um computador que execute as ferramentas administrativas do Exchange 2007.


