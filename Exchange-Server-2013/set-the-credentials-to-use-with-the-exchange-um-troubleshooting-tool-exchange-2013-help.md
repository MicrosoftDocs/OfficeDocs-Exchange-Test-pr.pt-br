---
title: 'Definir credenciais para Ferramenta de Solução de Problemas da UM do Exchange'
TOCTitle: Definir as credenciais a serem usadas com o Exchange UM ferramenta de solução
ms:assetid: 542b7718-9345-40cc-bcb2-e307e70a1fa2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff630916(v=EXCHG.150)
ms:contentKeyID: 56270508
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Definir as credenciais a serem usadas com o Exchange UM ferramenta de solução

 

_**Aplica-se a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

A ferramenta de solução de problemas de UM do Microsoft Exchange 2010 é um cmdlet do Shell de Gerenciamento do Exchange chamado **Test-ExchangeUMCallFlow**. Use o cmdlet para diagnosticar erros de configuração específicos para os cenários de resposta de chamadas e para testar o funcionamento correto da caixa postal em implantações de UM locais ou entre locais do Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou posterior. Você pode usar esse cmdlet em implantações com o Microsoft Office, o Microsoft Lync Server 2010 ou posterior, ou em implantações de UM com gateways VOIP, PBXs IP ou controladores de borda da sessão (SBCs).

Como padrão, ao executar a Ferramenta de solução de problemas da UM, são usadas as credenciais utilizadas ao se fazer logon no computador. As credenciais usadas são as especificadas para o chamador. Você deve definir ou especificar as credenciais a serem usadas ao executar a Ferramenta de solução de problemas da UM no modo `SIPClient`. No entanto, não é necessário definir as credenciais ao executar a Ferramenta de solução de problemas da UM no modo `Gateway`.

## O que você precisa saber antes de começar?

  - Tempo estimado para finalização: 3 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Servidor de Unificação de MENSAGENS" ou "serviços de Unificação de MENSAGENS? entrada no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md) .

  - Certifique-se de que seu Exchange 2010 ou a organização do Exchange 2013 atende aos seguintes requisitos:
    
      - Um plano de discagem da UM foi criado. Para instruções detalhadas, consulte [Criar um plano de discagem de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).
    
      - Uma política de caixa de correio de UM foi criada. Para as etapas detalhadas, consulte [Criar uma política de caixa de correio da UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy).
    
      - Um gateway IP do UM foi criado. Para instruções detalhadas, consulte [Criar um gateway IP de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway).
    
      - Um servidor de Unificação de MENSAGENS do Exchange 2010 foi adicionado ao plano de discagem de Unificação de MENSAGENS. Se você estiver usando o Exchange 2013 com o Lync Server, adicione todos os servidores de caixa de correio e de acesso para cliente para os planos de discagem URI do SIP. Para obter etapas detalhadas, consulte [Adicionar um servidor UM a um plano de discagem](https://go.microsoft.com/fwlink/p/?linkid=313051) ou [Adicionar servidores de acesso para cliente e caixa de correio a um plano de discagem URI do SIP](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md).

  - Instale a Ferramenta de solução de problemas da UM. Para instruções detalhadas, consulte [Instalação da Ferramenta de Solução de Problemas de UM do Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).
    

    > [!IMPORTANT]
    > Se você for usar a ferramenta de solução de problemas UM no modo de <CODE>SIPClient</CODE> , há vários outros Office Communications Server 2007 R2 ou Microsoft Lync Server requisitos e os pré-requisitos. Para obter mais informações, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=311961">lista de verificação: implantar o Office Communications Server 2007 R2 e o Exchange 2010 Unified Messaging</A> ou <A href="checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md">Lista de verificação: Integrar o UM do Exchange 2013 com o Lync Server</A>.



  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Definir as credenciais para utilização com a Ferramenta de solução de problemas da UM

1.  A partir do menu **Início**, abra a **Ferramenta de Solução de Problema de UM do Exchange 2010**.

2.  Na janela **Ferramenta de Solução de Problema de UM do Microsoft Exchange 2010**, no prompt, digite o seguinte e aperte Enter.
    
        $cred=Get-Credential

3.  Na janela **Solicitação de Credencial do Windows PowerShell**, digite o nome de usuário/domínio e a senha e depois clique em **OK**.

4.  Na janela **Ferramenta de Solução de Problemas da UM do Microsoft Exchange 2010**, especifique os parâmetros de cmdlet necessários para testar o fluxo da chamada. Por exemplo:
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

