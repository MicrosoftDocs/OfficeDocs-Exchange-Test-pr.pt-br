---
title: 'Execute a Ferramenta de Solução de Problemas de UM do Exchange no Windows 7 /8'
TOCTitle: Execute a Ferramenta de Solução de Problemas de UM do Exchange no Windows 7 ou Windows 8
ms:assetid: 98d6869d-ee4a-4088-849d-ef75b0f5d932
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff851872(v=EXCHG.150)
ms:contentKeyID: 56270512
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Execute a Ferramenta de Solução de Problemas de UM do Exchange no Windows 7 ou Windows 8

 

_**Aplica-se a:** Exchange Server 2010 Service Pack 2 (SP2), Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

A ferramenta de solução de problemas de UM do Microsoft Exchange 2010 é um cmdlet do Shell de Gerenciamento do Exchange chamado **Test-ExchangeUMCallFlow**. Use o cmdlet para diagnosticar erros de configuração específicos para os cenários de resposta de chamadas e para testar o funcionamento correto da caixa postal em implantações de UM locais ou entre locais do Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou posterior. Você pode usar esse cmdlet em implantações com o Microsoft Office, o Microsoft Lync Server 2010 ou posterior, ou em implantações de UM com gateways VOIP, PBXs IP ou controladores de borda da sessão (SBCs).

## O que você precisa saber antes de começar?

  - Tempo estimado para finalização: 3 minutos

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o "Servidor de Unificação de MENSAGENS" ou "serviços de Unificação de MENSAGENS? entrada no tópico [Permissões de mensagens unificadas](unified-messaging-permissions-exchange-2013-help.md) .

  - Certifique-se de que seu Exchange 2010 ou a organização do Exchange 2013 atende aos seguintes requisitos:
    
      - Um plano de discagem da UM foi criado. Para instruções detalhadas, consulte [Criar um plano de discagem de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan).
    
      - Uma diretiva de caixa de correio da UM foi criada. Para instruções detalhadas, consulte [Criar uma política de caixa de correio da UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy).
    
      - Um gateway IP do UM foi criado. Para instruções detalhadas, consulte [Criar um gateway IP de UM](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway).
    
      - Um servidor de Unificação de MENSAGENS do Exchange 2010 foi adicionado ao plano de discagem de Unificação de MENSAGENS. Se você estiver usando o Exchange 2013 com o Lync Server, adicione todos os servidores de caixa de correio e de acesso para cliente para os planos de discagem URI do SIP. Para obter etapas detalhadas, consulte [Adicionar um servidor UM a um plano de discagem](https://go.microsoft.com/fwlink/p/?linkid=313051) ou [Adicionar servidores de acesso para cliente e caixa de correio a um plano de discagem URI do SIP](add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md).

  - Se você estiver executando a ferramenta de solução de problemas UM em um servidor de Unificação de MENSAGENS local com o Exchange 2010 SP1 ou posterior ou em um servidor de caixa de correio do Exchange 2013, não talvez seja necessário instalar todos os pré-requisitos listados abaixo. Talvez eles já tenha sido instalados juntamente com a função de servidor de Unificação de MENSAGENS. No entanto, se você estiver instalando a ferramenta de solução de problemas UM em um computador de 64 bits que não seja um servidor que está executando a função de servidor de Unificação de MENSAGENS, você precisará instalar os seguintes componentes:
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1). Consulte [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).
    
      - Se a ferramenta for executada em um computador de Vista ou Windows Server 2008Windows, consulte [Microsoft .NET Framework 3.5 Family Update para Windows Vista x64 e Windows Server 2008 x64](https://go.microsoft.com/fwlink/p/?linkid=178998).
    
      - Windows Remote Management (WinRM) 2.0 e Windows PowerShell V2 (Windows6.0-KB968930.msu). Consulte o artigo 968930 da Base de Conhecimento da Microsoft, [Windows Management Framework Core package (Windows PowerShell 2.0 e WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).
    
      - Microsoft Unified Communications Managed API 2.0 Core Runtime (Ucmaruntimewebdownloadx64). Consulte [Unified Communications Managed API 2.0, Core Runtime (64 bits)](https://go.microsoft.com/fwlink/p/?linkid=198175).

  - Baixe e instale a Ferramenta de solução de problemas da UM.
    
      - Baixe [Unificação de mensagens a ferramenta de solução de problemas](https://go.microsoft.com/fwlink/p/?linkid=182625) do Centro de Download da Microsoft.
    
      - Instale a ferramenta. Para detalhes, consulte [Instalação da Ferramenta de Solução de Problemas de UM do Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).
        

        > [!IMPORTANT]
        > Se você for usar a ferramenta de solução de problemas UM no modo de <CODE>SIPClient</CODE> , existem várias outras Office Communications Server 2007 R2 ou Microsoft requisitos do Lync Server e os pré-requisitos que devem ser atendidos. Para obter mais informações, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=311961">lista de verificação: implantar o Office Communications Server 2007 R2 e o Exchange 2010 Unified Messaging</A>.



  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Execute a Ferramenta de Solução de Problemas de UM no Windows Vista, Windows 7, ou Windows 8

1.  Clique em **Iniciar** \> **Todos os programas** \> **Acessórios** \> **Windows PowerShell**.

2.  Clique com o botão direito do mouse em **Windows PowerShell** e, no menu pop-up, selecione **Executar como administrador**.

3.  No prompt de comando do Windows PowerShell, vá para a pasta onde a Ferramenta de Solução de Problemas de UM foi instalada e execute o seguinte.
    
        C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe -psconsolefile .\Microsoft.Exchange.UM.TroubleshootingToolsnapin.psc1 -noexit -command ". '.\Microsoft.Exchange.UM.TroubleshootingTool.ps1' "

4.  Se você está executando a Ferramenta de Solução de Problemas de UM no Windows Vista, Windows 7, ou Windows 8, no prompt de comando do Windows PowerShell, execute o seguinte.
    
    ```powershell
Set-ExecutionPolicy RemoteSigned
```

5.  No menu **Início**, abra a **Ferramenta de Solução de Problemas de UM do Microsoft Exchange 2010**.

6.  Na janela **Ferramenta de Solução de Problemas da UM do Microsoft Exchange 2010**, no prompt, digite o seguinte e pressione Enter.
    
    ```powershell
$cred=Get-Credential
```

7.  Na janela **Solicitação de Credencial do Windows PowerShell**, digite o nome e a senha do domínio/usuário e depois clique em **OK**.

8.  Na janela **Ferramenta de Solução de Problemas da UM do Microsoft Exchange 2010**, especifique os parâmetros de cmdlet necessários para testar o fluxo da chamada. Por exemplo:
    
        Test-ExchangeUMCallFlow -Mode SIPClient -CallingParty tonysmith@contoso.com - CalledParty jamiestark@contoso.com NextHop ocsfe.contoso.com -Credential $cred

