---
title: 'Testando e Solucionando problemas com a ferramenta de solução de problemas UM: Exchange 2013 Help'
TOCTitle: Testando e Solucionando problemas com a ferramenta de solução de problemas UM
ms:assetid: 1fab2e52-bd2d-4e46-b222-53fee9d34cba
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg621148(v=EXCHG.150)
ms:contentKeyID: 56270506
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Testando e Solucionando problemas com a ferramenta de solução de problemas UM

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

A ferramenta de solução de problemas de UM do Microsoft Exchange 2010 é um cmdlet do Shell de Gerenciamento do Exchange chamado **Test-ExchangeUMCallFlow**. Use o cmdlet para diagnosticar erros de configuração específicos para os cenários de resposta de chamadas e para testar o funcionamento correto da caixa postal em implantações de UM locais ou entre locais do Microsoft Exchange Server 2010 Service Pack 1 (SP1) ou posterior. Você pode usar esse cmdlet em implantações com o Microsoft Office, o Microsoft Lync Server 2010 ou posterior, ou em implantações de UM com gateways VOIP, PBXs IP ou controladores de borda da sessão (SBCs).

## Visão Geral

Este cmdlet emula chamadas e executa uma série de testes de diagnóstico que ajudam os administradores de local para identificar erros de configuração em equipamentos de telefonia, Exchange 2010 SP1 ou posteriores configurações de Unificação de mensagens e problemas de conectividade entre o local e as implantações de locais cruzados do Exchange 2010 SP1 ou posterior Unificação de mensagens.

Ao executar o cmdlet, ele identifica as possíveis soluções para os problemas que foram detectados. Ele também exibe métricas gerais de qualidade de áudio para o diagnóstico de problemas de qualidade de áudio relacionados à conectividade da rede, tais como jitter e perda de pacotes média. O cmdlet **Test-ExchangeUMCallFlow** dá suporte para teste de componentes de UM nas chamadas `Secured`, `SIP Secured` e `Unsecured`, e pode ser executado nos modos `Gateway` ou `SIPClient` .

Por padrão, quando você está executando a ferramenta UM solução de problemas, ele usa as credenciais que são usadas quando você fizer logon no computador. As credenciais usadas são aquelas que são especificados do chamador. Você deve definir ou especifique as credenciais a serem usadas quando você está executando a ferramenta de solução de problemas UM no modo `SIPClient` . No entanto, você não precisa definir as credenciais ao executar a ferramenta de solução de problemas UM no modo de `Gateway` . Se você for usar a ferramenta de solução de problemas UM no modo de `SIPClient` , requisitos de várias outras Lync Server ou Office Communications Server 2007 R2 e os pré-requisitos devem ser atendidos. Para obter mais informações, consulte [lista de verificação: implantar o Office Communications Server 2007 R2 e o Exchange 2010 Unified Messaging](https://go.microsoft.com/fwlink/p/?linkid=311961) ou [Lista de verificação: Integrar o UM do Exchange 2013 com o Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md).


> [!IMPORTANT]
> O cmdlet <STRONG>Test-ExchangeUMCallFlow</STRONG> deve ser usado para testar apenas a funcionalidade de caixa postal de um servidor de Unificação de mensagens de Exchange Server 2010 Microsoft que tenha Exchange 2010 Service Pack 1 (SP1) instalado ou Microsoft Exchange 2013.



O cmdlet **Test-ExchangeUMCallFlow** pode ser instalado em um servidor local de Unificação de Mensagens do Exchange 2010, em um servidor de Caixa de Correio do Exchange 2013 ou em outro computador de 64 bits que esteja executando:

  - O sistema operacional Windows 7 ou Windows 8

  - O sistema operacional Windows Server 2008 ou Windows Server 2008 R2

  - O sistema operacional Windows Server 2012 ou Windows Server 2012 R2

O cmdlet **Test-ExchangeUMCallFlow** exije os seguintes componentes para ser instalado em um computador de 64-bits com Windows 7, Windows 8, Windows Server 2008, ou Windows Server 2012 antes da instalação do cmdlet:

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1). Para baixar o service pack, consulte [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).

  - Microsoft .NET Framework 3.5 Family Update para Windows Vista x64 e Windows Server 2008 x64 atualiza se a ferramenta for executada em um computador Windows Vista ou Windows Server 2008. Para baixar a atualização, consulte [Microsoft .NET Framework 3.5 Family Update para Windows Vista x64 e Windows Server 2008 x64](https://go.microsoft.com/fwlink/p/?linkid=178998).

  - Windows Gerenciamento Remoto (WinRM) 2.0 e Windows PowerShell V2 (Windows6.0-KB968930.msu). Para mais informações, consulte o artigo 968930 da Base de Conhecimento da Microsoft, [Pacote principal do Windows Management Framework (Windows PowerShell 2.0 e WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=968930).

  - Comunicações unificadas gerenciadas AP1 2.0, Core Runtime (64 bits). Para baixar o arquivo de programa Ucmaruntimewebdownloadx64, consulte [Unified Communications Managed API 2.0, Core Runtime (64 bits)](https://go.microsoft.com/fwlink/p/?linkid=198175).

O cmdlet **Test-ExchangeUMCallFlow** não está incluído no Exchange 2010 SP1 DVD, o Exchange 2010 SP1 somente para download ou mídia de instalação do Exchange 2013; No entanto, você pode baixar o cmdlet do [Centro de Download Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625).

Para mais informações sobre a sintaxe e os parâmetros, consulte [Test-ExchangeUMCallFlow](https://technet.microsoft.com/pt-br/library/ff630913\(v=exchg.150\)).

