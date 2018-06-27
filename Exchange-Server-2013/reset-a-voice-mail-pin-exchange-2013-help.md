---
title: 'Redefinir um PIN da caixa postal: Exchange 2013 Help'
TOCTitle: Redefinir um PIN da caixa postal
ms:assetid: bf07e6e7-01d2-4933-bff5-c615cc21a480
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb124404(v=EXCHG.150)
ms:contentKeyID: 50556270
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
f1_keywords:
- Microsoft.Exchange.Management.SnapIn.Esm.Recipients.ResetUnifiedMessagingPinPropertyControl
ms.translationtype: MT
---

# Redefinir um PIN da caixa postal

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2013-02-22_

Quando um usuário habilitado para UNIFICAÇÃO de mensagens de email de voz é bloqueado suas caixas de correio usando o Outlook Voice Access porque eles tentaram entrar usando um PIN incorreto várias vezes ou eles esqueceu o seu PIN, você pode usar um dos procedimentos a seguir para redefinir o PIN do usuário. Quando você reinicia Outlook PIN Voice Access um usuário, você pode configurar a Unificação de mensagens para gerar automaticamente um PIN ou você pode especificar manualmente o PIN. O novo PIN é enviado ao usuário no email. Você pode especificar opções de PIN adicionais como exigir que o usuário redefinir seu PIN quando entrarem pela primeira vez no. Os usuários também podem redefinir seu PIN de UM usando Outlook ou Outlook Web App.


> [!TIP]
> Para acessar suas caixas de correio habilitado, os usuários do Outlook Voice Access necessário usar um tom de discagem por tom, também conhecido como dual DTMF (Multifreqüência), entradas. Reconhecimento de fala não está disponível para entrada de PIN.



Para tarefas adicionais relacionadas à segurança do PIN do Outlook Voice Access, consulte [Procedimentos de segurança PIN](pin-security-procedures-exchange-2013-help.md).

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: Menos de 1 minuto.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Caixas de correio da UM" no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## O que você deseja fazer?

## Use o EAT para redefinir um PIN de Unificação de mensagens

1.  No EAC, navegue até **Destinatários**. Na exibição de lista, selecione a caixa de correio de usuário que você deseja atualizar.

2.  No painel de detalhes, em **telefone e recursos de voz**, em **Unificação de mensagens**, clique em **Exibir detalhes**.

3.  Na página de **Correio de UM**, em **configurações de caixa de correio de Unificação de mensagens**, clique em **Redefinir PIN**.

4.  Na página **Redefinir UM PIN de caixa de correio**, use as seguintes opções para redefinir o PIN do usuário habilitado para Unificação de mensagens:
    
      - **Gerar automaticamente um PIN**    Use esta opção para gerar automaticamente o PIN que é usado pelo usuário para acessar suas caixas de correio usando Outlook Voice Access. Por padrão, essa configuração estiver habilitada.
        
        O PIN gerado automaticamente será enviado em uma mensagem de email, a caixa de correio do usuário. Depois que eles recebem o PIN e entrar em suas caixas de correio, eles serão solicitados para alterar o PIN para um PIN que é mais familiar para eles.
        
        Outlook Web App e o Microsoft Outlook também permitem que o usuário redefinir seu PIN. O PIN é gerado automaticamente com base nas diretivas de PIN que são configuradas na diretiva de caixa de correio de Unificação de mensagens que está associado a caixa de correio do usuário. Recomendamos que você gerar automaticamente PINs para os usuários do Voice Access Outlook.
    
      - **Tipo de um PIN**    Use esta opção para especificar manualmente um PIN de um usuário de acesso de voz Outlook. Por padrão, essa configuração é desabilitada.
        
        Se você especificar um PIN de um usuário, o PIN será enviado em uma mensagem de email, a caixa de correio do usuário. Depois que eles recebem o PIN e entrar em suas caixas de correio, eles poderão alterar o PIN, definindo opções pessoais no Outlook Voice Access. No entanto, em Outlook Web App e o Microsoft Outlook, não há nenhuma opção para especificar manualmente um PIN.
    
      - **Exigir que o usuário redefinir seu PIN na primeira vez que entrarem no**    Use esta opção para exigir que o usuário redefinir seu PIN quando eles entrar pela primeira vez Outlook Voice Access. Por padrão, essa opção está habilitada.
        
        Se você selecionar a opção para gerar automaticamente um PIN de um usuário, você pode habilitar essa opção exigir que os usuários alterem o PIN quando eles entrar pela primeira vez Outlook Voice Access. Isso ajuda a proteger o PIN do usuário.

5.  Clique em **Salvar**.

## Use o Shell para redefinir um PIN de Unificação de mensagens

Este exemplo redefine o PIN da caixa postal de Tony Smith como 1985848. No entanto, esse PIN deve ser alterado quando o usuário entra pela primeira vez para Outlook Voice Access.

    Set-UMMailboxPIN -Identity tonysmith@contoso.com -PIN 1985848 -PinExpired $true

