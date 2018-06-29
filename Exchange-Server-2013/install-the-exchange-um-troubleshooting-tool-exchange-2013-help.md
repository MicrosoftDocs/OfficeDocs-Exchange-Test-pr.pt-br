---
title: 'Instalação da Ferramenta de Solução de Problemas de UM do Exchange: Exchange 2013 Help'
TOCTitle: Instalação da Ferramenta de Solução de Problemas de UM do Exchange
ms:assetid: 84223af0-a717-49ee-add6-86313bb30d17
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff844714(v=EXCHG.150)
ms:contentKeyID: 56270511
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Instalação da Ferramenta de Solução de Problemas de UM do Exchange

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

A ferramenta de solução de problemas de UM do Microsoft Exchange 2010 é um cmdlet do Shell de Gerenciamento do Exchange chamado **Test-ExchangeUMCallFlow**. Use o cmdlet para diagnosticar erros de configuração específicos para os cenários de resposta de chamadas e para testar o funcionamento correto da caixa postal em implantações de UM locais ou entre locais do Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou posterior. Você pode usar esse cmdlet em implantações com o Microsoft Office, o Microsoft Lync Server 2010 ou posterior, ou em implantações de UM com gateways VOIP, PBXs IP ou controladores de borda da sessão (SBCs).

A ferramenta de Solução de Problemas de UM pode ser instalada em um servidor de Unificação de Mensagens local, em um servidor de Caixa de Correio do Exchange 2013 ou em outro computador de 64-bits.

## O que você precisa saber antes de começar?

  - Tempo estimado para finalização: 3 minutos

  - A ferramenta de Solução de Problemas de UM exige que os componentes a seguir estejam instalados em um computador que esteja executando o Windows Vista, Windows 7, Windows 8, ou a edição de 64-bits do Windows Server 2008 ou o Windows Server 2012 ou posterior antes da ferramenta ser instalada:
    
      - Microsoft .NET Framework 3.5 Service Pack 1 (SP1) consulte [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).
    
      - Se a ferramenta for executada em um computador Windows Vista ou Windows Server 2008, consulte [Microsoft .NET Framework 3.5 Family Update para Windows Vista x64 e Windows Server 2008 x64](https://go.microsoft.com/fwlink/p/?linkid=178998).
    
      - Windows Remote Management (WinRM) 2.0 e Windows PowerShell V2 (Windows6.0-KB968930.msu). Consulte o artigo 968930 da Base de Conhecimento da Microsoft, [Windows Management Framework Core package (Windows PowerShell 2.0 and WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930).
    
      - Microsoft Unified Communications Managed API 2.0 Core Runtime (Ucmaruntimewebdownloadx64). Consulte [Unified Communications Managed API 2.0, Core Runtime (64 bits)](https://go.microsoft.com/fwlink/p/?linkid=198175).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Instalar a Ferramenta de Solução de Problemas da UM

1.  Baixe o Unified Messaging Troubleshooting Tool do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625)e clique duas vezes na pasta de instalação Microsoftexchange2010umtroubleshootingtool.

2.  Na página **Bem-vindo ao Assistente para Instalação da Ferramenta de Solução de Problemas da UM do Microsoft Exchange 2010**, clique em **Avançar**.

3.  Na página **Termos de Licença do Usuário Final**, analise os termos de licença do software e, se estiver de acordo, clique em **Aceito os termos de licença**; e, em seguida, clique em **Avançar**.

4.  Na página **Selecionar Pasta de Instalação**, verifique o caminho até a pasta de instalação e clique em **Avançar**.

5.  Na página **Confirmar Instalação**, clique em **Avançar** para iniciar a instalação.

6.  Na página **Instalação Concluída**, clique em **Fechar**.

