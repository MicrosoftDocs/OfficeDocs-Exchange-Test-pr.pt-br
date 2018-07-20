---
title: 'Supervisor de telefonia para o Exchange 2013: Exchange 2013 Help'
TOCTitle: Supervisor de telefonia para o Exchange 2013
ms:assetid: e9f760f2-5901-4ed2-95a5-724555cc700e
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee364753(v=EXCHG.150)
ms:contentKeyID: 50556307
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Supervisor de telefonia para o Exchange 2013

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2017-07-25_

Unified Messaging (UM) requer integrar o Microsoft Exchange com o sistema de telefonia existente para a sua organização. Uma implantação bem-sucedida requer que você faça uma análise criteriosa da sua infra-estrutura de telefonia existente e executar as etapas de planejamento corretas para implantar a Unificação de mensagens.

A fase de planejamento pode ser um desafio significativo aos administradores Exchange que têm pouca ou nenhuma experiência com uma rede de telefonia. Para ajudar a resolver esse desafio, consulte recursos para obter ajuda com uma implantação híbrida Your posteriormente neste tópico.

Para ver os gateways de VoIP com suporte para Unificação de mensagens, determinar se seu PBX é suportado usando um modelo específico de gateway VoIP ou fabricante, se seu PBX IP é suportada usando uma conexão de SIP direto, ou ver suportado (de controladores de borda de sessão SBCs) para Exchange UM Online, clique em um dos seguintes links:

  - Gateways VoIP com suporte

  - Com suporte PBXs ao usar um gateway AudioCodes VoIP

  - Suporte para PBXs ao usar um gateway de VoIP dialogic
    
      - PBXs suportados ao usar uma série de DMG1000 Gateway de mídia
    
      - PBXs suportados ao usar uma série de 2000 DMG Gateway de mídia
    
      - PBXs suportados ao usar uma série de DMG3000 Gateway de mídia

  - PBXs IP com suporte

  - Suporte para PBXs IP ao usar os gateways de mídia SIP

  - Exchange Unified Messaging, Office Communications Server 2007 R2 e Microsoft Lync Server

## Recursos para ajudá-lo com a implantação da Unificação de mensagens

Ele é um desafio para criar diretrizes para implantar redes de telefonia. Eles podem ser muito diferentes uns dos outros porque podem incluir gateways VoIP, IP PBXs e PBXs com requisitos, firmware e definições de configuração diferentes. No entanto, vários recursos estão disponíveis para ajudá-lo a implantar com êxito a Unificação de mensagens:

  - **Especialistas de Unificação de mensagens** Especialistas de Unificação de mensagens são integradores de sistemas que tiverem recebido treinamento técnico sobre Exchange Unified Messaging conduzido pela equipe de engenharia de Exchange. Para ajudar a garantir uma transição suave para o Unified Messaging de sistemas de correio de voz herdado, Microsoft recomenda que todos os clientes solicitam um especialista de Unificação de mensagens. Para informações de contato, visite o [Microsoft Exchange Server 2013 Unified Messaging (UM) especialistas](http://go.microsoft.com/fwlink/p/?linkid=262708) ou [Microsoft identifique para Unificação de mensagens](https://go.microsoft.com/fwlink/p/?linkid=261951).

  - **Notas de configuração para os Gateways VoIP com suporte, IP PBXs e PBXs**   Essas notas de configuração contém configurações e outras informações que é muito útil quando você estiver configurando gateways VoIP, IP PBXs e PBXs para se comunicar com os servidores de Unificação de mensagens que estão em sua rede. Para obter mais informações, consulte [Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md).

  - **Notas de configuração para controladores de borda de sessão suportados**   Essas notas de configuração contém configurações e outras informações que é muito útil quando você estiver configurando controladores de borda de sessão (SBCs) para se comunicar com os servidores de Unificação de mensagens híbrido e Exchange Online UM implantações. Para obter mais informações, consulte [Notas de configuração para controladores de borda de sessão suportados](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md).
    

    > [!TIP]
    > Exchange Online UM suporte para sistemas de PBX de terceiros por meio de conexões diretas do cliente operado SBCs será finalizado no de 2018 julho. Consulte o blog da equipe <A href="https://blogs.technet.microsoft.com/exchange/2017/07/18/discontinuation-of-support-for-session-border-controllers-in-exchange-online-unified-messaging/">suporte para controladores de borda de sessão no Exchange Online Descontinuado Unificação de mensagens</A> Exchange para obter mais informações.



Antes que você entre em contato com uma especialista em Unificação de mensagens, você deve ser capaz de atender as principais perguntas que eles vai ser feitas. Ter as respostas para as seguintes perguntas ajudarão a tornar a conversa entre você e a especialista em UM produtivo:

  - Quantos usuários de email de voz ou telefone existente ou ambas, estejam em sua organização?

  - Quantos usuários você pretende fornecer com a Unificação de mensagens?

  - Quais PBX ou PBXs você pretende usar para integração com a Unificação de mensagens?

  - Quantos PBXs sua organização tem? Especifique os fornecedores, tipos (baseado em circuito ou IP), modelos e versões de firmware.

  - Estabelecem PBXs, e eles são centralizados ou localizados em vários locais?

  - Quais sistemas ou o sistema de caixa postal sua organização usa atualmente? Especifique os fornecedores, tipos, modelos e versões de firmware.

  - Como os sistemas de caixa postal integrados ao seus PBXs (analógico, T1/E1, PRI, Digital definir simulação, VoIP, outras)?

  - Você está usando no momento rede de voz?

  - Que tipo de sistema de fax ou sistemas de sua organização usar, e o sistema de fax ou sistemas suporta o roteamento de fax de entrada para Exchange ?

  - Sua organização usa atendedores automáticos?

  - Precisa de suporte para usuários somente de telefone, ou seja, usuários que não têm acesso de email?

## Gateways VoIP com suporte

Integrando a Unificação de mensagens com PBXs requer que você use um ou mais gateways de VoIP para traduzir os protocolos comutadas que são usados pelo TDM-based PBXs para protocolos de comutação de pacotes, baseado em IP que são usados pela Unificação de mensagens. Fornecedores de gateway VoIP com vários modelos de gateways VoIP e mídia foram testados e há suporte para a Unificação de mensagens.

Teste de interoperabilidade da Unificação de mensagens com gateways VoIP, PBXs IP e SBCs é agora integrado com o Microsoft programa de interoperabilidade aberta do Unified Communications. Para obter mais informações, consulte [Microsoft Unified Communications programa de interoperabilidade aberta](http://go.microsoft.com/fwlink/p/?linkid=140722).

O programa de qualificação [Microsoft Unified Communications programa de interoperabilidade aberta](http://go.microsoft.com/fwlink/p/?linkid=140722) para gateways VoIP, IP PBXs e gateways de VoIP avançados garante que os clientes têm uma instalação sem interrupções e o suporte a experiência quando estejam usando telefonia qualificado gateways de VoIP e PBXs IP com Microsoft software de comunicação unificada. Somente os produtos que atendem aos requisitos de testes rigorosos e extensivo e estar de acordo com as especificações e planos de teste recebem qualificação.

Para obter detalhes sobre como configurar gateways VoIP, IP PBXs, PBXs e SBCs suportados, consulte um dos seguintes recursos:

  - [Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs](configuration-notes-for-supported-voip-gateways-ip-pbxs-and-pbxs-exchange-2013-help.md)

  - [Notas de configuração para controladores de borda de sessão suportados](configuration-notes-for-supported-session-border-controllers-exchange-2013-help.md)

Interoperabilidade foi verificada para os seguintes fornecedores de gateway VoIP:

  - AudioCodes

  - Dialogic

  - A tabela a seguir mostra o fornecedor do gateway de VoIP, o modelo de gateway VoIP e os protocolos que são suportados por cada modelo.

### Gateways VoIP com suporte para Unificação de mensagens

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fornecedor</th>
<th>Modelo</th>
<th>Protocolos com suporte</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>MediaPack 114/8 FXO</p></td>
<td><ul>
<li><p>Analógicos com DTMF em banda</p></li>
<li><p>Analógicos com SMDI</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AudioCodes</p></td>
<td><p>Mediant 1000</p></td>
<td><ul>
<li><p>Analógicos com DTMF em banda</p></li>
<li><p>Analógicos com SMDI</p></li>
<li><p>BRI Q.SIG</p></li>
<li><p>Q.SIG T1/E1</p></li>
<li><p>IP-para-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>AudioCodes</p></td>
<td><p>Mediant 2000</p></td>
<td><ul>
<li><p>CAS T1/E1</p></li>
<li><p>Q.SIG T1/E1</p></li>
<li><p>IP-para-IP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG1000PBXDNIW</p></td>
<td><p>Set digital emulação</p></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG1000LSW</p></td>
<td><ul>
<li><p>Analógicos com DTMF em banda</p></li>
<li><p>Analógicos com SMDI</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Dialogic</p></td>
<td><p>DMG2000</p></td>
<td><ul>
<li><p>CAS T1</p></li>
<li><p>Q.SIG T1/E1</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Dialogic</p></td>
<td><p>DMG3000</p></td>
<td><ul>
<li><p>BRI Q.SIG</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NET</p></td>
<td><p>VX1200</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Sonus</p></td>
<td><p>SBC 1000/2000 2.2.1 ou posterior</p></td>
<td><ul>
<li><p>TDM sinalização (ISDN): AT &amp; T 4ESS/5ESS, Nortel DMS-100, Euro ISDN (ETSI 300-102), QSIG, InsNet NTT (Japão), ANSI nacional ISDN-2 (NI-2)</p></li>
<li><p>TDM sinalização (CAS): T1 CAS (E &amp; M, iniciar Loop); E1 CAS (R2)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Quintum</p></td>
<td><p>Série DX operariam</p></td>
<td><ul>
<li><p>T1 Q.SIG</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Com suporte PBXs ao usar um gateway AudioCodes VoIP

A tabela a seguir mostra os PBXs suportados usando gateways AudioCodes VoIP, incluindo MediaPack-114 FXO, MediaPack-118 FXO e Mediant 2000.

### PBXs compatíveis com um gateway AudioCodes VoIP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante do PBX</th>
<th>PBX/tipo de modelo</th>
<th>Modelo de AudioCodes &quot;x&quot; - substitua 4 ou 8 por necessidade &quot;y&quot; - substitua com 1, 2, 4, 8 ou 16 por necessidade</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>OmniPCX 4400</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Aastra</p></td>
<td><p>M1000, M2000</p></td>
<td><ul>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Magix/Merlin</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8300</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>S8700</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Office IP</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>CallManager 4. x</p></td>
<td><ul>
<li><p>Mediant1000/IP-para-IP</p></li>
<li><p>Mediant2000/IP-para-IP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>Cadillac Elite</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>NEAX2400</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant2000/ySpans/SIP/RS232</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>NeXspan</p></td>
<td><p>C</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Comunicação servidor - 1000M, 1000S, 1000E</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridiano 11c, 51c, 61c, 81c</p></td>
<td><ul>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Panasonic</p></td>
<td><p>KX-TES824, KX-TEA308</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Panasonic</p></td>
<td><p>KX-TDA30, KX-TDA100 KX-TDA200, KX-TDA600</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Shortel</p></td>
<td><p>Sistema de telefonia IP</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 150E</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 3550</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Telecomunicações Tadiran</p></td>
<td><p>Coral Flexicom, Coral IPX</p></td>
<td><ul>
<li><p>MediaPack 11 x/FXO/AC/SIP-0</p></li>
<li><p>Mediant1000/ySpans/SIP</p></li>
<li><p>Mediant2000/ySpans/SIP</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Com suporte PBXs ao usar um gateway VoIP Dialogic

Cada modelo de gateway VoIP Dialogic suporta PBXs diferentes. As tabelas a seguir mostrar o PBX fabricante e modelo e qual gateway VoIP Dialogic pode ser usado. Cada gateway VoIP usa os protocolos, densidades e diferentes métodos de sinalização.

## PBXs suportados ao usar uma série de DMG1000 Gateway de mídia

A tabela a seguir mostra os PBXs compatíveis com o Gateway de mídia Dialogic Baixa densidade (DMG1000). No entanto, quando um DMG1000 analógico é usado, a sinalização suplementares (RS232 SMDI, MD110, protocolos MCI, ou DTMF Inband sinalização) é necessária.

### Suportado ao usar um gateway de VoIP Baixa densidade Dialogic DMG1000 série de PBXs

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante do PBX</th>
<th>PBX/tipo de modelo</th>
<th>Modelo de DMG e sinalização adicionais</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>Aastra MD110 (anteriormente Ericsson MD110)</p></td>
<td><p>DMG1008LSW</p>
<p>Conectividade analógica usando o protocolo MD110 RS232</p></td>
</tr>
<tr class="even">
<td><p>Alcatel</p></td>
<td><p>PCX Omni 4400</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Definity G3 S8100, S8300, S8700 e S8710 (v 2.0 do Communications Mgr SW ou versões posteriores)</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Intercomunicação</p></td>
<td><p></p></td>
<td><p>DMG1008LSW</p>
<p>Conectividade analógica usando o protocolo de serial SMDI</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>SX - 200D, SX-200 claro, SX-2000 claro, SX-2000 S, SX-2000 VS, ICP SX-200</p></td>
<td><p>DMG1008MTLDNIW</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2000, 2400, 2400 IPX</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Meridiano 1 - opção 11, 21, 21A, 51, 61, 71 e 81</p>
<p>Meridiano SL1 - X11 genérico, versão 15 ou versões posteriores</p>
<p>Servidor de comunicação Nortel - 1000M, 1000S, 1000E com v 3.0 ou versões posteriores</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>SL 100</p></td>
<td><p>DMG1008LSW</p>
<p>Conectividade analógica usando o protocolo de serial SMDI</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>DMG1008DNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E (europeu)</p></td>
<td><p>DMG1008LSW</p>
<p>Conectividade analógica usando DTMF Inband sinalização</p></td>
</tr>
<tr class="odd">
<td><p>Siemens/ROLM</p></td>
<td><p>8000 (versão SW 80003 ou versões posteriores)<br />
9000 (todas as versões)</p>
<p>9751 (todas as versões do SW versão 9005)</p>
<p>9751 (versão SW 9006.4 ou versões posteriores)</p></td>
<td><p>DMG1008RLMDNIW</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="odd">
<td><p>Toshiba</p></td>
<td><p>CTX (versão SW AR1ME021.00)</p></td>
<td><p>DMG1008LSW</p></td>
</tr>
<tr class="even">
<td><p>Outras pessoas</p></td>
<td><p>Vários</p></td>
<td><p>DMG1008LSW</p>
<p>Conectividade analógica usando Inband DTMF ou SMDI</p></td>
</tr>
</tbody>
</table>


## PBXs suportados ao usar uma série de 2000 DMG Gateway de mídia

A tabela a seguir mostra os PBXs compatíveis com o Gateway de mídia T1/E1 Dialogic (DMG2000). O gateway DMG2000, que vem em um único intervalo (DMG2030DTIQ), dual span (DMG2060DTIQ) ou quad span densidades (DMG2120DTIQ), suporta os seguintes protocolos:

  - CAS T1

  - T1 Q.SIG

  - E1 Q.SIG

  - T1 NI-2

  - T1 5ESS

  - T1 DMS100

Se a sinalização de canal associado sinalização (CAS) for usado, a sinalização suplementares (RS232 SMDI, MD110, protocolos MCI, ou DTMF Inband sinalização) é necessária. Se a sinalização Q.SIG for usado, o PBX deve suportar os serviços complementares que estão associados a chamada e chamadas de informações de terceiros e a transferência de chamada recursos necessários pela Unificação de mensagens.

### PBXs compatíveis com o Gateway de mídia DMG2000

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante do PBX</th>
<th>PBX/tipo de modelo</th>
<th>Versão de software necessárias</th>
<th>Protocolo e sinalização adicionais</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Alcatel</p></td>
<td><p>PCX Omni 4400</p></td>
<td><p>Versão 3.2.712.5</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Definity G3</p></td>
<td><p>Versão 3 ou posterior</p></td>
<td><p>CAS T1</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>S8500</p></td>
<td><p>Manager SW v 2.0 ou versões posteriores</p></td>
<td><p>CAS T1</p>
<p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Ericsson</p></td>
<td><p>MD110</p></td>
<td><p>Versão MX1 TSW R2A (BC13)</p></td>
<td><p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Intercomunicação</p></td>
<td><p></p></td>
<td><p></p></td>
<td><p>CAS (c / protocolo de serial SMDI)</p></td>
</tr>
<tr class="even">
<td><p>NEC</p></td>
<td><p>2400 IMX</p></td>
<td><p>Liberar 5200 dezembro de 92 1b ou versões posteriores</p></td>
<td><p>CAS (c / protocolo de serial MCI)</p></td>
</tr>
<tr class="odd">
<td><p>NEC</p></td>
<td><p>2400 IPX</p></td>
<td><p>R17 Versão 03.46.001</p></td>
<td><p>T1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Nortel</p></td>
<td><p>Meridiano 1 - opção 11</p></td>
<td><p>Versão 15 ou versões posteriores e opções 19 e 46 são necessárias</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Nortel</p></td>
<td><p>Servidor de comunicação 1000</p></td>
<td><p>Versão 2121, versão 4</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiCom 300E CS</p></td>
<td><p>Versão 9006.4 ou posterior (Observação: somente a carga de software na América do Norte)</p></td>
<td><p>CAS T1</p></td>
</tr>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>V2 SMR 9 SMPO</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="even">
<td><p>Mitel</p></td>
<td><p>S SX-2000, VERSUS SX-2000</p></td>
<td><p>LW 34</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
<tr class="odd">
<td><p>Mitel</p></td>
<td><p>3300</p></td>
<td><p>Versão 5.1.4.8</p></td>
<td><p>T1 Q.SIG</p>
<p>E1 Q.SIG</p></td>
</tr>
</tbody>
</table>


## PBXs suportados ao usar uma série de DMG4008BRI Gateway de mídia

A série DMG4000 Gateway de mídia é fornecido com diversas opções de interface TDM. O DMG4008BRI suporta 4-porta/8 canais densidades e suporta os seguintes protocolos:

  - ISDN BRI Q.SIG

  - ETSI-DSS1 (Euro ISDN)

  - NET 3 (Bélgica)

  - VN3 (França)

  - 1TR6 (Alemanha)

  - INS-64 (Japão)

  - Sinalizador 5ESS (América do Norte - AT & T)

  - ISDN Nacional (NI1 - América do Norte)

A tabela a seguir mostra os PBXs suportados usando um Gateway de mídia 4000 Dialogic Series (DMG4008).

### PBXs suportados usando um Gateway de mídia DMG4008BRI

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante do PBX</th>
<th>PBX/tipo de modelo</th>
<th>Versão de software necessárias</th>
<th>Protocolo e sinalização adicionais</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Siemens</p></td>
<td><p>300 HiCom</p></td>
<td><p>SA300-V3.05</p></td>
<td><p>BRI-Q. SIG (ECMAV2)</p></td>
</tr>
<tr class="even">
<td><p>Siemens</p></td>
<td><p>HiPath 4000</p></td>
<td><p>S.0 B4400</p></td>
<td><p>BRI-Q. SIG (ECMAV2)</p></td>
</tr>
</tbody>
</table>


## PBXs IP com suporte

PBXs IP também são suportadas pela Unificação de mensagens. A tabela a seguir mostra o PBXs IP que são suportados usando uma conexão SIP direto para a Unificação de mensagens.

### IP PBXs suportado ao usar uma conexão de SIP direto

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante do PBX</th>
<th>PBX/tipo de modelo</th>
<th>Versão de software necessárias</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Aastra</p></td>
<td><p>UM MX</p></td>
<td><p>4.0</p></td>
</tr>
<tr class="even">
<td><p>Avaya</p></td>
<td><p>Aura</p></td>
<td><p>5.2.1 com Service Pack 5 (SP5)</p></td>
</tr>
<tr class="odd">
<td><p>Avaya</p></td>
<td><p>Servidor de comunicação 2100</p></td>
<td><p>CS2100 SE13</p></td>
</tr>
<tr class="even">
<td><p>Cisco</p></td>
<td><p>Gerente de chamada, gerente de comunicação unificada</p></td>
<td><p>5.1, 6.x, 7.0 and8.0</p></td>
</tr>
</tbody>
</table>


## IP PBXs suportado ao usar o SIP gateways de mídia

IP PBXs usando mídia SIP gateways também são suportados pela Unificação de mensagens. A tabela a seguir mostra o PBXs IP que são suportados usando IP capacidades de IP de gateways de mídia SIP para conectar à Unificação de mensagens.

### IP PBXs suportado ao usar um gateway de mídia SIP

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Fabricante do PBX</th>
<th>PBX/tipo de modelo</th>
<th>Modelo de gateway SIP</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cisco</p></td>
<td><p>Gerenciador de chamadas 4. x</p></td>
<td><p>AudioCodes Mediant 1000/2000 (IP-para-IP habilitado)</p></td>
</tr>
</tbody>
</table>


## Exchange Unified Messaging, Office Communications Server 2007 R2 e Microsoft Lync Server

Para o local e híbrido implantações, Unificação de mensagens do Exchange podem ser implantadas juntamente com Microsoft Office Communications Server 2007 R2, Microsoft Lync Server 2010 ou o Lync Server 2013 para oferecer mensagens, de voz de mensagens Instantâneas, presença avançada do usuário, conferência de áudio e vídeo e um email integrado e experiência de mensagens para usuários em sua organização. Para obter mais informações, consulte:

  - [Implantando a visão geral da Unificação de MENSAGENS do Exchange 2013 e Lync Server](deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md)

  - [Microsoft Lync Server 2013](https://go.microsoft.com/fwlink/p/?linkid=202010)

Para obter mais informações sobre o Microsoft Unified Communications programa de interoperabilidade aberta infraestrutura de telefonia empresarial, incluindo Localizando gateways PSTN SIP qualificados e PBXs IP e o processo para telefonia fornecedores de infra-estrutura para ingressar e participar do programa, consulte [Microsoft Unified Communications programa de interoperabilidade aberta](https://go.microsoft.com/fwlink/p/?linkid=132071).

