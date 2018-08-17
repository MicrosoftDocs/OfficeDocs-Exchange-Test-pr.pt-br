---
title: 'Saiba mais da ferramenta de solução de problemas de UM: Exchange 2013 Help'
TOCTitle: Saiba mais sobre a UM ferramenta de solução de problemas do Exchange
ms:assetid: cc11bf5e-2c87-4495-b2ad-3e9a6bc81dbc
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Gg584301(v=EXCHG.150)
ms:contentKeyID: 56270515
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Saiba mais sobre a UM ferramenta de solução de problemas do Exchange

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

A Microsoft Exchange 2010 Unified Messaging Troubleshooting Tool é um cmdlet do Shell de gerenciamento Exchange chamado **Test-ExchangeUMCallFlow**. Você pode usar essa ferramenta para conduzir uma série de testes de diagnóstico para Unificação de mensagens (UM) em sua organização. Se algum dos testes falhar, a ferramenta relata o motivo para as falha e possíveis soluções corrigir o problema. Você somente pode usar a ferramenta de solução de problemas UM nos Exchange 2010 ou posterior nos servidores.

A Ferramenta de Solução de Problemas UM pode ser usada para testar se o correio de voz está funcionando corretamente em implantações locais e em vários locais. Você pode usar esta ferramenta nas implantações de UM que incluem Microsoft Office Communications Server 2007 R2 ou o Microsoft Lync Server 2010 ou posterior, ou em implantações de UM que incluam gateways VoIP, IP Private Branch eXchanges (IP PBXs), ou controladores de borda de sessão (SBCs).


> [!NOTE]
> A Ferramenta de Solução de Problemas UM é usada para teste e solução de problemas. Já o cmdlet <STRONG>Test-UMConnectivity</STRONG> deve ser usado para monitoramento. O cmdlet <STRONG>Test-UMConnectivity</STRONG> é usado com os pacotes de gerenciamento do with System Center Operations Manager (SCOM) usados para monitorar os servidores de UM do Exchange 2010 ou os servidores de Caixa de Correio e de Acesso do Cliente do Exchange 2013 e os componentes de telefonia. O cmdlet <STRONG>Test-UMConnectivity</STRONG> realiza testes SIP locais e testes de logon locais em caixas de correio, podendo ser executado como uma tarefa SCOM.



Para baixar a ferramenta de solução de problemas UM, consulte [Unified Messaging Troubleshooting Tool](https://go.microsoft.com/fwlink/p/?linkid=182625).

**Conteúdo**

Visão geral

UM troubleshooting architecture

VoIP gateway and IP PBX deployments

Office Communications Server R2 and Microsoft Lync Server deployments

Installing the UM Troubleshooting Tool

Cmdlet parameters

## Visão geral

A Ferramenta de Solução de Problemas UM simplifica o teste e a solução de problemas em ambientes UM. Ao ser executada, a Ferramenta de Solução de Problemas UM gera automaticamente um conjunto de arquivos de rastreamento armazenados na pasta C:\\Users\\%UserProfile%\\AppData\\Roaming\\Microsoft Exchange 2010 UM Troubleshooting. Os seguintes arquivos de rastreamento são gerados pela ferramenta:

  - **UMTool\_Collaboration**   Inclui rastreamentos de pilha RTC.

  - **UMTool\_DiagnosticLog**   Lista todos os testes executados e seus resultados.

  - **UMTool\_S4**   Inclui o S4: rastreamentos de pilha de sinalização.

  - **UMTool\_SIPMessageLogs**   Inclui os rastreamentos SIP completos para a chamada de teste feita.

A Ferramenta de Solução de Problemas de UM conecta-se diretamente a um controlador de borda de sessão (SBC) local, se existir um, ou conecta-se a um SBC em um datacenter e emula uma chamada de entrada como se a chamada estivesse vindo de um PBX através de um gateway de VoIP ou de um IP PBX. A Ferramenta de Solução de Problemas UM pode ser usada para diagnosticar:

  - Configurações incorretas em implantações de UM locais ou entre instalações nas quais o Office Communications Server 2007 R2 ou Microsoft Lync Server sejam implantados.

  - Configurações incorretas em equipamentos de telefonia locais ou entre instalações que incluam gateways de VoIP ou IP PBXs.

  - Problemas com Sistema de Nomes de Domínio (DNS).

  - Problemas de certificado quando você está usando planos de discagem protegido SIP ou UM protegido.

  - Problemas de sinalização e mídia para DTMF (também conhecido como discagem por tom) e áudio.

Se detectar uma falha na configuração, a Ferramenta de Solução de Problemas UM informará o motivo do erro e as possíveis soluções para os erros detectados. Os erros que podem ser informados quando a Ferramenta de Solução de Problemas UM é usada em uma implantação local incluem os seguintes:

  - O limite máximo de chamadas foi atingido.

  - Usuário não habilitado para a Unificação de Mensagens.

  - As informações do gateway IP UM, do plano de discagem ou do grupo de busca não podem ser localizadas.

  - O tipo de segurança não corresponde ao plano de discagem UM.

  - Não há nenhum processo de trabalho disponível para processar a chamada.

  - O serviço de UM ou os serviços de Roteamento de Chamada de UM são interrompidos.

  - Não foi possível localizar a floresta do Active Directory.

  - Não há espaço em disco disponível.

  - Foram usados cabeçalhos SIP na solicitação.

  - Foi feita uma chamada para o servidor do Office Communications Server 2007 R2 ou do Lync Server.

  - O gateway IP de UM está desabilitado.

  - O URI do usuário que está sendo chamado não é válido.

Quando a Ferramenta de Solução de Problemas UM é usada em uma implantação local, os erros que podem ser informados incluem os seguintes:

  - Usuário não habilitado para a Unificação de Mensagens.

  - O gateway IP de UM está desabilitado.

  - O URI do usuário é inválido.

  - O tipo de segurança não corresponde ao plano de discagem UM.

  - Foram usados cabeçalhos SIP na solicitação.

  - As informações do gateway IP UM, do plano de discagem ou do grupo de busca não podem ser localizadas.

A Ferramenta de Solução de Problemas de UM envia um arquivo .wav de amostra por 15 segundos. Após o arquivo de áudio e o fluxo de áudio RTP serem enviados e tocados, a ferramenta relata as métricas gerais de qualidade do áudio para o diagnóstico de problemas na qualidade do áudio relacionados à conectividade de rede, tais como jitter e média da perda de pacotes. Esses relatórios incluem a qualidade do fluxo de mídia para e de um servidor UM e contêm o seguinte:

  - Network Mean Opinion Score (NMOS)

  - Codec

  - Latência em milissegundos (ms)

  - Tremulação em milissegundos (ms)

  - % de perda de pacotes

  - A classificação NMOS e a avaliação que serão usadas para determinar a qualidade de áudio serão:
    
      - NMOS menor que 2 = Insatisfatório
    
      - NMOS maior que 2, mas menor que 3 = Médio
    
      - NMOS maior que 3, mas menor que 4 = Bom
    
      - NMOS maior que 4, mas menor que 5 = Excelente

A Ferramenta de Solução de Problemas UM oferece suporte ao teste de planos de discagem UM que usam chamadas Protegida, Protegida por SIP e Não Protegida. Se você optar por Protegida ou Protegida por SIP, a impressão digital do certificado usado é verificada para determinar se o certificado expirou e o tipo de certificado usado na comunicação do protocolo TLS (Transport Layer Security). O certificado é usado para identificar corretamente e assegurar a identidade do computador remoto. Quando o modo Protegido ou SIP Protegido é selecionado, a Ferramenta de Solução de Problemas UM verifica se o seguinte é verdadeiro:

  - O certificado local foi encontrado no repositório do computador local.

  - O certificado usado é confiável.

  - O nome de destino especificado no certificado é válido.

  - O certificado expirou.

  - O computador remoto confia no certificado.

  - O certificado não foi revogado.

  - O certificado não tem o uso avançado de chave obrigatório.

A Ferramenta de Solução de Problemas de UM pode ser executada nos modos Gateway ou SIPClient, dependendo se o Office Communications Server 2007 R2 ou o Lync Server forem implantados ou se os gateways de VoIP e PBXs ou IP PBXs são usados com os servidores de Unificação de Mensagens. Quando o modo Gateway ou SIPClient é usado, a Ferramenta de Solução de Problemas UM oferece suporte a chamadas usando os formatos a seguir. O formato usado depende do tipo de URI do plano de discagem UM:

  - Ramal telefônico   425-555-1010

  - Números de telefone E.164   +1 (425) 555-1010

  - Endereços SIP   tonysmith@contoso.com

Quando o modo SIPClient é usado, a Ferramenta de Solução de Problemas UM faz uma chamada de memorando de voz. Trata-se de uma chamada que não toca um telefone ou um ponto de extremidade Comunicação Unificada (UC). Em vez disso, ela envia a chamada diretamente para correio de voz. Ao ser executada no modo SIPClient, a Ferramenta de Solução de Problemas UM determina:

  - Qual usuário de destino está sendo chamado.

  - Se a chamada SIP foi estabelecida com êxito.

  - A chamada SIP tendo sido aceita por um servidor de Unificação de Menssagens do Exchange 2010 ou por um servidor de Caixa de Correio do Exchange 2013.

  - Se a sequência DTMF correta foi recebida.

  - O arquivo .wav de diagnóstico tendo sido enviado e recebido por um servidor UM do Exchange 2010 UM ou um servidor de Caixa de Correio do Exchange 2013.

  - A métrica usada quando a mídia ou o fluxo de qualidade do áudio foi recebido.

A Ferramenta de Solução de Problemas UM emula chamadas de entrada e executa uma série de testes de diagnóstico que ajudam administradores locais e locatários a testarem fluxo de chamadas para atendê-las e identificar erros de configuração. Embora posa ser usada em cenários de atendimento de chamada, a Ferramenta de Solução de Problemas UM pode ser usada para testar os seguintes tipos de chamadas:

  - Outlook Chamadas do Voice Access, incluindo chamadas que acessam correio de voz, email, calendário, o diretório, contatos pessoais ou opções pessoais

  - atendedores automáticos da UM

  - Tocar no Telefone

  - Regras de Atendimento de Chamada

  - Envio e recebimento de faxes

  - Provisionamento de prompt

Voltar ao início

## Arquitetura de solução de problemas de UM

A Ferramenta de Solução de Problemas pode ajudar você a solucionar problemas, diagnosticar e reparar problemas de configuração nas implantações entre instalações e você pode também usá-las nas implantações de Unificação de Mensagens. Nas implantações entre instalações, a ferramenta também valida configurações SBC locais. O administrador pode testar todos os componentes da Unificação de Mensagens usados pela Unificação de Mensagens, inclusive os SBCs.

## Implantações de gateway de VoIP e IP PBX

No exemplo a seguir, o modo Gateway é usado para testar o fluxo de chamada em um ambiente que não inclui o Office Communications Server 2007 R2 ou o Lync Server. Este exemplo testa os equipamentos de telefonia, incluindo gateways de VoIP, PBXs e IP PBXs e os componentes de Unificação de Mensagens. Esse exemplo define o modo de segurança VoIP como Unsecured, usa o endereço IP 10.1.1.1 como o próximo salto e inclui um número de ramal nas informações de desvio.

    Test-ExchangeUMCallFlow -Mode Gateway -VoIPSecurity Unsecured -NextHop 10.1.1.1 -Diversion 12345

Voltar ao início

## Implantações do Office Communications Server 2007 R2 e Microsoft Lync Server

A Ferramenta de Solução de Problemas de UM pode ser usada em implantações locais ou entre instalações incluindo o Office Communications Server 2007 R2 ou o Microsoft Lync Server quando o modo SIPClient estiver configurado. O exemplo a seguir usa o modo SIPClient e testa o fluxo de chamada com um plano de discagem de UM seguro em um ambiente que contenha servidores do Office Communications Server 2007 R2 ou do Lync Server. Por padrão, quando você executa a Ferramenta de Solução de Problemas UM, ela usa as credenciais do usuário conectado no momento ao computador. Ao executar o exemplo a seguir, você será solicitado a informar as credenciais que deseja usar ao executar a Ferramenta de Solução de Problemas UM. Para detalhes, consulte [Definir as credenciais a serem usadas com o Exchange UM ferramenta de solução](set-the-credentials-to-use-with-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).

    Test-ExchangeUMCallFlow -Mode SIPClient -VoIPSecurity Secured -CallingParty tony@contoso.com -CalledParty david@contoso.com -Credential $get

## Instalando a Ferramenta de Solução de Problemas UM

A Ferramenta de Solução de Problemas UM pode ser instalada em um servidor Unificação de Mensagens local ou em um outro computador de 64 bits que esteja executando:

  - Os sistemas operacionais Windows 7 ou Windows 8.

  - Os sistemas operacionais Windows Server 2008 ou Windows Server 2008 R2.

  - Os sistemas operacionais Windows Server 2012 ou Windows Server 2012 R2.

Se você estiver usando a Ferramenta de Solução de Problemas de UM em uma versão de 64-bits do Windows 7, Windows 8, ou a edição de 64-bits do Windows Server 2008, os componentes a seguir devem ser instalados antes da instalação da Ferramenta de Solução de Problemas de UM:

  - Microsoft .NET Framework 3.5 Service Pack 1 (SP1) consulte [Microsoft .NET Framework 3.5 Service Pack 1](https://go.microsoft.com/fwlink/p/?linkid=152380).
    

    > [!NOTE]
    > Se a ferramenta for executada em um computador Windows Vista ou Windows Server 2008, consulte <A href="https://go.microsoft.com/fwlink/p/?linkid=178998">Microsoft .NET Framework 3.5 Family Update para Windows Vista x64 e Windows Server 2008 x64</A>.



  - Windows Remote Management (WinRM) 2.0 e Windows PowerShell V2 (Windows6.0-KB968930.msu)   Consulte o artigo 968930 da Base de Conhecimento da Microsoft, [Windows Management Framework Core package (Windows PowerShell 2.0 and WinRM 2.0)](http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=968930).

  - Microsoft Unified Communications Managed API 2.0 Core Runtime (Ucmaruntimewebdownloadx64) consulte [Unified Communications Managed API 2.0, Core Runtime (64 bits)](https://go.microsoft.com/fwlink/p/?linkid=198175).

A UM Troubleshooting Tool (**Test-ExchangeUMCallFlow** cmdlet) não está incluída no Exchange 2010 SP1 DVD, download que inclui somente Exchange 2010 ou mídia de instalação do Exchange 2013. No entanto, você pode baixar a ferramenta de solução de problemas UM partir do [Centro de Download da Microsoft](https://go.microsoft.com/fwlink/p/?linkid=182625).

Para detalhes, consulte [Instalação da Ferramenta de Solução de Problemas de UM do Exchange](install-the-exchange-um-troubleshooting-tool-exchange-2013-help.md).

Voltar ao início

## Parâmetros do cmdlet

A tabela a seguir inclui os parâmetros que é possível usar com o cmdlet **Test-ExchangeUMCallFlow** e as descrições desses parâmetros. Também é possível usar o comando Shell `Get-help Test-ExchangeUMCallFlow -detailed` para localizar informações detalhadas sobre cada parâmetro que pode ser usado com o cmdlet **Test-ExchangeUMCallFlow**, além de exemplos de uso.

### Parâmetros

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Parameter</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>CalledParty</em></p></td>
<td><p>O parâmetro <em>CalledParty</em> especifica a URI de SIP do usuário do Office Communications Server 2007 R2 ou do Lync Server que foi habilitado para o Enterprise Voice. Trata-se do usuário para quem o cmdlet <strong>Test-ExchangeUMCallFlow</strong> fará a chamada de voz, por exemplo: <code>-CalledParty tonysmith@contoso.com</code>. Use este parâmetro se estiver executando a ferramenta no modo SIPClient.</p></td>
</tr>
<tr class="even">
<td><p><em>CallingParty</em></p></td>
<td><p>O parâmetro <em>CallingParty</em> especifica a URI de SIP do usuário do Office Communications Server 2007 R2 ou do Lync Server que foi habilitado para o Enterprise Voice. Trata-se do usuário que faz a chamada de entrada, por exemplo: <code>-CallingParty tonysmith@contoso.com</code>. Use este parâmetro se estiver executando a ferramenta no modo SIPClient.</p></td>
</tr>
<tr class="odd">
<td><p><em>Diversion</em></p></td>
<td><p>O parâmetro <em>Diversion</em> especifica a cadeia de caracteres que deve ser enviada como informações de desvio para a chamada sendo recebida. Isso pode estar no formulário de um cabeçalho de Desvio ou Histórico-Info. As informações de desvio incluídas na chamada de entrada podem ser um número de ramal ou incluir informações de desvio adicionais.</p>
<p>Ao fornecer informações de desvio como cabeçalho de Histórico-Info, verifique o seguinte:</p>
<ul>
<li><p>Há pelo menos duas entradas diferentes com peças de usuário diferentes.</p></li>
<li><p>A última entrada contém o número piloto do plano de discagem de UM associado do usuário.</p></li>
<li><p>A segunda até a última entrada inclui o número de ramal do usuário habilitado para UM. Essa entrada deve ter também o texto do Motivo apropriado. Esse texto deve ter escapes corretos, de acordo com as regras de escape de parâmetro de URL padrão.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><em>Mode</em></p></td>
<td><p>O parâmetro <em>Mode</em> especifica se o modo gateway de VoIP, IP PBX, ou Office Communications Server 2007 R2 ou Lync Server será usado. você pode especificar o modo Gateway quando a sua implantação de UM incluir gateways de VoIP ou IP PBXs ou o modo SIPClient quando a sua implantação de UM incluir o Office Communications Server 2007 R2 ou o Lync Server.</p></td>
</tr>
<tr class="odd">
<td><p><em>NextHop</em></p></td>
<td><p>O parâmetro <em>NextHop</em> especifica o endereço IP ou nome de domínio totalmente qualificado (FQDN) do próximo salto ao qual o cmdlet <strong>Test-ExchangeUMCallFlow</strong> deve se conectar ao emular o gateway de VoIP ou IP PBX. Ao incluir a porta TCP, você deve especificar a porta 5060 para o modo Não Protegido ou a porta 5061 para o modo Protegido ou SIP Protegido. Por exemplo: <code>gateway.contoso.com:5061</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>CertificateThumbprint</em></p></td>
<td><p>O parâmetro <em>CertificateThumbprint</em> especifica a impressão digital do certificado usado para o protocolo TLS. Isso é obrigatório caso o modo SIP Protegido ou Protegido esteja configurado no plano de discagem UM. Este impressão digital de certificado é o certificado que foi exportado do gateway de VoIP, IP PBX ou SBC. Além disso, o computador que tem a Ferramenta de Solução de Problemas de UM instalada e está sendo usado para testar o fluxo de chamadas deve confiar no certificado de autoridade do próximo hop.</p></td>
</tr>
<tr class="odd">
<td><p><em>Credential</em></p></td>
<td><p>O parâmetro <em>Credential</em> especifica as credenciais que serão usadas para executar o cmdlet.</p></td>
</tr>
<tr class="even">
<td><p><em>HuntGroup</em></p></td>
<td><p>O parâmetro <em>HuntGroup</em> especifica o grupo de busca de UM associado com o gateway de VoIP que está sendo emulado. Isso é geralmente um número de ramal. Use este parâmetro se estiver executando a ferramenta no modo Gateway.</p></td>
</tr>
<tr class="odd">
<td><p><em>VoIPSecurity</em></p></td>
<td><p>O parâmetro <em>VoIPSecurity</em> especifica o modo de segurança quando utiliza o cmdlet no modo Gateway. Você pode usar um dos seguintes modos de segurança VoIP:</p>
<ul>
<li><p>Protegido (TLS/SRTP)</p></li>
<li><p>Não Protegido (TCP/RTP) (padrão)</p></li>
<li><p>SIP Protegido (TLS/SRTP)</p></li>
</ul></td>
</tr>
</tbody>
</table>


Voltar ao início

