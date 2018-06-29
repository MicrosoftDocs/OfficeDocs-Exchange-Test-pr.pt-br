---
title: 'Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs: Exchange 2013 Help'
TOCTitle: Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs
ms:assetid: 1583674f-5a57-45fd-8125-087d1624e686
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee681657(v=EXCHG.150)
ms:contentKeyID: 50556148
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-12-09_

Esta página fornece links para as notas de configuração que foram criadas e testadas pela Microsoft ou um parceiro de gateway VoIP. Quando Microsoft ou um parceiro implanta a Unificação de mensagens com um novo gateway VoIP e configuração de PBX ou PBX IP, os pré-requisitos e as definições de configuração estão documentadas. Essas informações são usadas para criar uma nota de configuração.

Cada Observação sobre a configuração PBX contém informações sobre como implantar a Unificação de mensagens com uma configuração de telefonia específico e inclui o fabricante, o modelo e a versão de firmware para os gateways VoIP, IP PBXs ou PBXs. Além disso, cada Observação sobre a configuração PBX inclui outras informações, como:

  - Colaboradores na criação de nota de configuração.

  - Pré-requisitos detalhados, incluindo o seguinte:
    
      - Recursos que devem ser habilitados ou desabilitados no PBX.
    
      - Hardware especializada que deve ser instalado.
    
      - Se um gateway VoIP é necessário.
    
      - Recursos que devem estar presentes no gateway VoIP, se necessário.
    
      - Requisitos específicos de cabeamento entre um gateway IP e um PBX.
    
      - Uma lista dos recursos de Unificação de mensagens que podem não estar disponíveis com uma configuração de telefonia determinado.

Para saber mais sobre o Microsoft Unified Communications programa de interoperabilidade aberta infraestrutura de telefonia empresarial, incluindo a localização de gateways PSTN SIP qualificados e PBXs IP e os fornecedores de infraestrutura de telefonia de processo podem usar para ingressar e participar do programa, consulte [Microsoft Unified Communications programa de interoperabilidade aberta](https://go.microsoft.com/fwlink/p/?linkid=132071).

## Gateway de VoIP, IP PBX e notas de configuração de PBX

Microsoft está trabalhando com parceiros de gateway VoIP, AudioCodes e Dialogic, para adicionar à lista de PBXs são testados. Como estamos atualmente testando muitas combinações dos componentes de telefonia, este tópico é atualizado com frequência. Volte a verificar se você não conseguir localizar a observação sobre a configuração apropriada para sua implantação.

As notas de configuração a seguir estão disponíveis:


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><ul>
<li><p>Aastra</p></li>
<li><p>Alcatel</p></li>
<li><p>Avaya</p></li>
<li><p>Cisco</p></li>
<li><p>Inter-Tel</p></li>
<li><p>Intecom</p></li>
<li><p>Mitel</p></li>
<li><p>NEC</p></li>
</ul></td>
<td><ul>
<li><p>NeXspan</p></li>
<li><p>Nortel</p></li>
<li><p>Panasonic</p></li>
<li><p>Rolm</p></li>
<li><p>ShoreTel</p></li>
<li><p>Siemens</p></li>
<li><p>Sonus</p></li>
<li><p>Tadiran</p></li>
<li><p>Toshiba</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Aastra


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra MD110 (anteriormente Ericsson MD110)</p></td>
<td><p>MX1 TSW R2A (também conhecido como BC13)</p></td>
<td><p>Analógico – MD110 Serial</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Baixar</a></p></td>
</tr>
<tr class="even">
<td><p>Aastra MD110 (anteriormente Ericsson MD110)</p></td>
<td><p>MX1 TSW R2A (também conhecido como BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>UM Aastra MX</p></td>
<td><p>4.0</p></td>
<td><p>Conexão SIP direto</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Aastra</p></td>
<td><p><a href="http://www.aastra.com/cps/rde/aareddownload?file_id=4384-14746-_p06_xml%26dsproject=aastra%26mtype=pdf">Baixar</a></p></td>
</tr>
</tbody>
</table>


## Alcatel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>OmniPCX 4400</p></td>
<td><p>R4.2-d2.304-4-h-il-c6s2</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Avaya


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aura</p></td>
<td><p>Gerenciador de comunicação 5.2.1 com SP 5</p>
<p>Gerenciador de sessão 5.2.</p></td>
<td><p>Conexão SIP direto</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/downloads/">Baixar</a></p></td>
</tr>
<tr class="even">
<td><p>CS 2100</p></td>
<td><p>CS 2100 SE13</p></td>
<td><p>Conexão SIP direto</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Avaya</p></td>
<td><p><a href="https://support.avaya.com/css/p8/documents/100149819">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R009i.05.122.4</p></td>
<td><p>Set digital emulação (DNI7434)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Baixar</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 CAS – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Baixar</a></p></td>
</tr>
<tr class="even">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Baixe o</a></p></td>
</tr>
<tr class="odd">
<td><p>Definity G3</p></td>
<td><p>R013i.01.1.628.7</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Merlin Magix</p></td>
<td><p>Versão 1.5 6.0</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>Gerenciador de comunicação de G3xV11 1.3</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>T1 CAS – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Baixe o</a></p></td>
</tr>
<tr class="odd">
<td><p>S8300</p></td>
<td><p>R013x.01.2.632.1</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>Gerenciador de comunicação 3.0 (R013x00.1.346.0)</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>S8500</p></td>
<td><p>Gerenciador de comunicação 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 CAS – em banda DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>S8500</p></td>
<td><p>Gerenciador de comunicação 3.0 (R013x00.1.346.0)</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>S8700</p></td>
<td><p>R011x.02.0.110.4</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Cisco


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciador de chamadas Cisco 4. x</p></td>
<td><p>4.x</p></td>
<td><p>IP-para-IP</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Gerenciador de chamadas Cisco 5.1</p></td>
<td><p>5.1.0.9921-12</p></td>
<td><p>Conexão SIP direto</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco Unified Communications Manager 6.0 e 6.1</p></td>
<td><p>6.x</p></td>
<td><p>Conexão SIP direto</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=225083">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Cisco Unified Communications Manager 7.0</p></td>
<td><p>7.0.2.20000-5</p></td>
<td><p>Conexão SIP direto</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=196361">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>Cisco Unified Communications Manager 8.0</p></td>
<td><p>8.0.3.20000-5</p></td>
<td><p>Conexão SIP direto</p></td>
<td><p>N.A.</p></td>
<td><p>N.A.</p></td>
<td><p>Microsoft</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=213007">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Inter-Tel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>5000</p></td>
<td><p>V 2.1 de inter-Tel 5000</p></td>
<td><p>T1 CAS – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Axxess</p></td>
<td><p>Axxess v 9.0</p></td>
<td><p>T1 CAS – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Intecom


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>PointSpan M6880</p></td>
<td><p>40PS3.5.K.2</p></td>
<td><p>T1 CAS - SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Mitel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>5.1.4.8</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>SX2000</p></td>
<td><p>5.0.24</p></td>
<td><p>Set digital emulação (DNISS430)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008MTLDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>3300</p></td>
<td><p>7</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## NEC


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cadillac Elite 192</p></td>
<td><p>SP034V4.5</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IMX</p></td>
<td><p>versão 7400</p></td>
<td><p>T1 CAS - MCI serial</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IMX &amp; IPX</p></td>
<td><p>versão 7400</p></td>
<td><p>Set digital emulação (DNIDtermIII)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver. R18.06.24.000</p></td>
<td><p>T1 CAS – MCI serial</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver. R18.06.24.000</p></td>
<td><p>Analógico – MCI serial</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>NEAX2400IPX</p></td>
<td><p>Ver.17 Rel.03.46.001</p></td>
<td><p>T1 Q.SIG – MCI serial</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## NeXspan


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>D</p></td>
<td><p>Versão RMS1 R1.3 E1TA</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Nortel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CS1000</p></td>
<td><p>3.0 &amp; 4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Meridiano 81C</p></td>
<td><p>4.5</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>Meridiano 81C</p></td>
<td><p>4.5</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>Versão 25</p></td>
<td><p>Set digital emulação (DNI2616)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>Option11c</p></td>
<td><p>Versão 25</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Option11c</p></td>
<td><p>Versão 25</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>CS - 1000M (sucessivamente)</p></td>
<td><p>Versão 25.40</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Panasonic


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>KX-TDA200</p></td>
<td><p>001-001</p></td>
<td><p>Analógico: DTMF em banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>KX-TDA200</p></td>
<td><p>3</p></td>
<td><p>Analógico: DTMF em banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>KX-TES824</p></td>
<td><p>2.0.2</p></td>
<td><p>Analógico: DTMF em banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Rolm


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>9751</p></td>
<td><p>9005</p></td>
<td><p>Set digital emulação (DNIRP400)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008RLMDNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## ShoreTel


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sistema de telefonia IP</p></td>
<td><p>6.1</p></td>
<td><p>Analógico – SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Sistema de telefonia IP</p></td>
<td><p>7.5</p></td>
<td><p>Analógico – SMDI</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Siemens


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>HiCom 150E</p></td>
<td><p>Rel. 2.2</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>300 HiCom</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>300 HiCom</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>Set digital emulação (DNIOptiset)</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008DNIW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>300 HiCom</p></td>
<td><p>9006.4SMR3</p></td>
<td><p>T1 CAS - DTMF em banda</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 3550</p></td>
<td><p>Rel. 3</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Ver 3.0 SMR5 SMP4</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI QSIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Ver 3.0 SMR5 SMP4</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>HiPath 4000</p></td>
<td><p>Versão 2.0 SMR9 SMP0</p></td>
<td><p>Analógico: DTMF em banda</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>HiPath 4000</p></td>
<td><p>Versão 2.0 SMR9 SMP0</p></td>
<td><p>T1 Q.SIG</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG2030DTIQ</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Sonus


<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de gateway VoIP</th>
<th>Versão de software do gateway de VoIP</th>
<th>Protocolos com suporte</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>SBC 1000/2000</p></td>
<td><p>2.2.1 ou posterior</p></td>
<td><ul>
<li><p>TDM sinalização (ISDN): AT &amp; T 4ESS/5ESS, Nortel DMS-100, Euro ISDN (ETSI 300-102), QSIG, InsNet NTT (Japão), ANSI nacional ISDN-2 (NI-2)</p></li>
<li><p>TDM sinalização (CAS): T1 CAS (E &amp; M, iniciar Loop); E1 CAS (R2)</p></li>
</ul></td>
<td><p>Sonus</p></td>
<td><p><a href="http://www.sonus.net/sites/default/files/sonussbc1k2kconfigo365.pdf">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Tadiran


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>MP 11 x FXO</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS - DTMF em banda</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Coral Flexicom</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 Q.SIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>X FXO MP-11</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>BRI QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="odd">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 CAS – em banda DTMF</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>Coral IPX</p></td>
<td><p>14.67.49</p></td>
<td><p>E1 QSIG</p></td>
<td><p>AudioCodes</p></td>
<td><p>Mediant</p>
<p>1000/2000</p></td>
<td><p>AudioCodes</p></td>
<td><p><a href="https://www.audiocodes.com/solutions/microsoft-unified-messaging">Faça o download</a></p></td>
</tr>
</tbody>
</table>


## Toshiba


<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th>Modelo de PBX</th>
<th>Versão de software do PBX</th>
<th>Protocolo</th>
<th>Fornecedor de gateway</th>
<th>Modelo de gateway</th>
<th>Autor de configuração</th>
<th>Download do arquivo de configuração</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>Analógico – SMDI</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
<tr class="even">
<td><p>CTX</p></td>
<td><p>AR1ME021.00</p></td>
<td><p>Analógico – em banda DTMF</p></td>
<td><p>Dialogic</p></td>
<td><p>DMG1008LSW</p></td>
<td><p>Dialogic</p></td>
<td><p><a href="https://www.dialogic.com/support/helpweb/mg/integration.htm">Faça o download</a></p></td>
</tr>
</tbody>
</table>

