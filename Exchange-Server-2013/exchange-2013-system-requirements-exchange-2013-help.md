---
title: 'Requisitos de sistema do Exchange 2013: Exchange 2013 Help'
TOCTitle: Requisitos de sistema do Exchange 2013
ms:assetid: 1e80857c-b870-4a6d-a0f4-ff7b3a7be037
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996719(v=EXCHG.150)
ms:contentKeyID: 50485090
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Requisitos de sistema do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Saiba mais sobre os requisitos do Exchange 2013 que você precisa saber antes de instalar o Exchange 2013. Por exemplo, você aprenderá sobre os requisitos de hardware, rede e sistema operacional.

Antes de instalar o Microsoft Exchange Server 2013, recomendamos que você leia este tópico para garantir que rede, hardware, software, clientes e outros elementos atendam aos requisitos do Exchange 2013. Além disso, entenda os cenários de coexistência suportados para o Exchange 2013 e versões anteriores do Exchange.

## Cenários de coexistência suportados

A tabela a seguir lista os cenários em que a há suporte para a coexistência entre o Exchange 2013 e versões anteriores do Exchange.

### Coexistência de versões anteriores do Exchange Server e o Exchange 2013

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versão do Exchange</th>
<th>Coexistência da organização do Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 e versões anteriores</p></td>
<td><p>Sem suporte</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>Compatível com as seguintes versões mínimas do Exchange:</p>
<ul>
<li><p>1Pacote cumulativo de atualizações 10 do Exchange 2007 Service Pack 3 (SP3) em todos os servidores Exchange 2007 da organização, inclusive nos servidores de Transporte de Borda.</p></li>
<li><p>Atualização Cumulativa 2 (CU2) ou posterior do Exchange 2013 em todos os servidores Exchange 2013 da organização.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Compatível com as seguintes versões mínimas do Exchange:</p>
<ul>
<li><p>2 Exchange 2010 SP3 em todos os servidores Exchange 2010, inclusive nos servidores de Transporte de Borda.</p></li>
<li><p>CU2 ou posterior do Exchange 2013 em todos os servidores Exchange 2013 da organização.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Organização mista do Exchange 2010 e do Exchange 2007</p></td>
<td><p>Compatível com as seguintes versões mínimas do Exchange:</p>
<ul>
<li><p>1Pacote cumulativo de atualizações 10 do Exchange 2007 SP3 em todos os servidores Exchange 2007 da organização, inclusive nos servidores de Transporte de Borda.</p></li>
<li><p>2 Exchange 2010 SP3 em todos os servidores Exchange 2010, inclusive nos servidores de Transporte de Borda.</p></li>
<li><p>CU2 ou posterior do Exchange 2013 em todos os servidores Exchange 2013 da organização.</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Para criar uma inscrição do EdgeSync entre um servidor de Transporte de Hub do Exchange 2007 e um servidor de Transporte de Borda do Exchange 2013 SP1, você deve instalar o pacote cumulativo de atualizações 13 do Exchange 2007 SP3 ou posterior no servidor de Transporte de Hub do Exchange 2007.

2   Para criar uma inscrição do EdgeSync entre um servidor de Transporte de Hub do Exchange 2010 e um servidor de Transporte de Borda do Exchange 2013 SP1, você deve instalar o pacote cumulativo de atualizações 5 do Exchange 2010 SP3 ou posterior no servidor de Transporte de Hub do Exchange 2010.

## Cenários de implantação híbrida suportados

O Exchange 2013 suporta implantações híbridas com locatários do Office 365 que foram atualizados para a versão mais recente do Office 365. Para obter mais informações sobre implantações híbridas específicas, consulte [Pré-requisitos de implantação híbrida](https://technet.microsoft.com/pt-br/library/hh534377\(v=exchg.150\)).

## Servidores de rede e de diretório

A tabela a seguir lista os requisitos para os servidores de rede e de diretório da sua organização do Exchange 2013:

**Requisitos de servidor de rede e diretório para o Exchange 2013**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Mestre de esquema</p></td>
<td><p>Por padrão, o mestre de esquema é executado no primeiro controlador de domínio do Active Directory instalado em uma floresta. O controlador de esquemas precisa estar executando qualquer um destes:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard ou Datacenter1</p></li>
<li><p>Windows Server 2012 Standard ou Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard ou Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM ou posterior</p></li>
<li><p>Windows Server 2008 Standard ou Enterprise (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2008 Datacenter RTM ou posterior</p></li>
<li><p>Windows Server 2003 Standard Edition com Service Pack 2 (SP2) ou posterior (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2003 Enterprise Edition com SP2 ou posterior (32 bits ou 64 bits)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Servidor de catálogo global</p></td>
<td><p>Em cada site do Active Directory em que você pretende instalar o Exchange 2013, deve haver pelo menos um servidor de catálogo global executando um destes:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard ou Datacenter1</p></li>
<li><p>Windows Server 2012 Standard ou Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard ou Enterprise</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM ou posterior</p></li>
<li><p>Windows Server 2008 Standard ou Enterprise (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2008 Datacenter RTM ou posterior</p></li>
<li><p>Windows Server 2003 Standard Edition com Service Pack 2 (SP2) ou posterior (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2003 Enterprise Edition com SP2 ou posterior (32 bits ou 64 bits)</p></li>
</ul>
<p>Para saber mais sobre servidores de catálogo global, confira <a href="https://go.microsoft.com/fwlink/p/?linkid=178996">O que é o Catálogo Global</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Controlador de domínio</p></td>
<td><p>Em cada site do Active Directory em que você pretende instalar o Exchange 2013, deve haver pelo menos um controlador de domínio gravável executando um destes:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard ou Datacenter1</p></li>
<li><p>Windows Server 2012 Standard ou Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard ou Enterprise SP1 ou posterior</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM ou posterior</p></li>
<li><p>Windows Server 2008 Standard ou Enterprise SP1 ou posterior (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2008 Datacenter RTM ou posterior</p></li>
<li><p>Windows Server 2003 Standard Edition com Service Pack 2 (SP2) ou posterior (32 bits ou 64 bits)</p></li>
<li><p>Windows Server 2003 Enterprise Edition com SP2 ou posterior (32 bits ou 64 bits)</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Floresta de Active Directory</p></td>
<td><p>O Active Directory deve estar em modo de funcionalidade de floresta do Windows Server 2003 ou superior2.</p></td>
</tr>
<tr class="odd">
<td><p>Suporte de namespace de DNS</p></td>
<td><p>O Exchange 2013 suporta os seguintes namespaces de sistema de nomes de domínio (DNS):</p>
<ul>
<li><p>Contíguos</p></li>
<li><p>Não contíguos</p></li>
<li><p>Domínios de rótulo único</p></li>
<li><p>Separado</p></li>
</ul>
<p>Para obter mais informações sobre namespaces de DNS suportados pelo Exchange, consulte o artigo 2269838 da Base de Dados de Conhecimento da Microsoft, <a href="http://go.microsoft.com/fwlink/?linkid=3052&kbid=2269838">Compatibilidade do Microsoft Exchange com Domínios de Rótulo Único, Namespaces Separados e Namespaces Não Contíguos</a>.</p></td>
</tr>
<tr class="even">
<td><p>Suporte a IPv6</p></td>
<td><p>No Exchange 2013, o IPv6 é suportado apenas quando o IPv4 também é instalado e habilitado. Se o Exchange 2013 for implantado nessa configuração, e a rede suportar IPv4 e IPv6, todos os servidores Exchange poderão enviar e receber dados de dispositivos, servidores e clientes que usem endereços IPv6. Para obter mais informações, consulte <a href="ipv6-support-in-exchange-2013-exchange-2013-help.md">Suporte a IPv6 no Exchange 2013</a>.</p></td>
</tr>
</tbody>
</table>


1   O Windows Server 2012 R2 tem suporte apenas no Exchange 2013 SP1 ou posterior.

2   O modo de funcionalidade da floresta do Windows Server 2012 R2 tem suporte apenas no Exchange 2013 SP1 ou posterior.

## Arquitetura do servidor de diretórios

O uso de controladores de domínio de 64 bits do Active Directory aumenta o desempenho do serviço de diretório do Exchange 2013.


> [!NOTE]
> Em ambientes com vários domínios, em controladores de domínio do Windows Server 2008 que tenham a localidade de idioma do Active Directory definida como japonês, os seus servidores podem não receber alguns atributos armazenados em um objeto durante a replicação de entrada. Para mais informações, consulte o artigo da Base de Dados de Conhecimento da Microsoft 949189, <A href="http://go.microsoft.com/fwlink/p/?linkid=3052&kbid=949189">Um controlador de domínio do Windows Server 2008 configurado com a localidade do idioma japonês pode não aplicar atualizações a atributos em um objeto durante a replicação de entrada</A>.



## Instalar o Exchange 2013 em servidores de diretório

Por motivos de segurança e desempenho, recomendamos que você instale o Exchange 2013 somente em servidores membros e não em servidores de diretório do Active Directory. No entanto, não é possível executar a DCPromo em um computador que esteja executando o Exchange 2013. Após a instalação do Exchange 2013, não será possível alterar sua função de um servidor membro para um servidor de diretório ou vice-versa.

## Hardware

Os requisitos de hardware recomendados para os servidores do Exchange 2013 variam de acordo com diversos fatores, incluindo as funções de servidor que estão instaladas e a carga antecipada que será imposta aos servidores.

Para obter informações detalhadas sobre como dimensionar e configurar sua implantação corretamente, consulte [Recomendações de configuração e dimensionamento do Exchange 2013](exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md).

Para obter informações sobre como implantar o Exchange em um ambiente virtualizado, consulte [Virtualização do Exchange 2013](exchange-2013-virtualization-exchange-2013-help.md).

**Requisitos de hardware para o Exchange 2013**


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Requisito</th>
<th>Observações</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Processador</p></td>
<td><ul>
<li><p>Computador baseado na arquitetura x64 com processador Intel que oferece suporte para a arquitetura Intel 64 (anteriormente conhecida como Intel EM64T)</p></li>
<li><p>Processador AMD que oferece suporte para a plataforma AMD64</p></li>
<li><p>Processadores Intel Itanium IA64 não aceitos</p></li>
</ul></td>
<td><p>Consulte a seção &quot;Sistema operacional&quot;, mais adiante neste tópico, para sistemas operacionais suportados.</p></td>
</tr>
<tr class="even">
<td><p>Memória</p></td>
<td><p>Varia dependendo das funções do Exchange instaladas:</p>
<ul>
<li><p><strong>Caixa de Correio</strong> mínimo de 8 GB</p></li>
<li><p><strong>Acesso para Cliente</strong> mínimo de 4 GB</p></li>
<li><p><strong>Caixa de Correio e Acesso para Cliente combinados</strong> mínimo de 8 GB</p></li>
<li><p><strong>Transporte de Borda</strong> Mínimo de 4 GB</p></li>
</ul></td>
<td><p>Nenhum(a).</p></td>
</tr>
<tr class="odd">
<td><p>Tamanho do arquivo de paginação</p></td>
<td><p>Os tamanhos de arquivo de página mínimo e máximo devem ser definidos como RAM física mais 10 MB, para um tamanho máximo de 32778 MB se você estiver usando mais de 32 GB de RAM.</p></td>
<td><p>Para obter recomendações detalhadas sobre o arquivo de paginação, consulte a seção &quot;Arquivo de Paginação&quot; em <a href="exchange-2013-sizing-and-configuration-recommendations-exchange-2013-help.md">Recomendações de configuração e dimensionamento do Exchange 2013</a>.</p></td>
</tr>
<tr class="even">
<td><p>Espaço em disco</p></td>
<td><ul>
<li><p>Pelo menos 30 GB na unidade em que você instalar o Exchange</p></li>
<li><p>500 MB adicionais de espaço em disco disponível para cada pacote de idiomas de UM (Unificação de Mensagens) que você planeja instalar</p></li>
<li><p>São necessários 200 MB de espaço em disco disponível na unidade do sistema</p></li>
<li><p>Um disco rígido que armazena o banco de dados de mensagens, com pelo menos 500 MB de espaço livre.</p></li>
</ul></td>
<td><p>Para obter informações detalhadas sobre as recomendações de armazenamento, consulte <a href="exchange-2013-storage-configuration-options-exchange-2013-help.md">Opções de configuração de armazenamento do Exchange 2013</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Unidade</p></td>
<td><p>Unidade de DVD-ROM, local ou acessível por rede</p></td>
<td><p>Nenhum(a).</p></td>
</tr>
<tr class="even">
<td><p>Resolução de tela</p></td>
<td><p>1024 x 768 pixels ou mais</p></td>
<td><p>Nenhum(a).</p></td>
</tr>
<tr class="odd">
<td><p>Formato de arquivo</p></td>
<td><p>Partições de disco formatadas como sistemas de arquivos NTFS, que se aplica às seguintes partições:</p>
<ul>
<li><p>Partição do sistema</p></li>
<li><p>Partições que armazenam arquivos ou arquivos binários do Exchange gerados pelo log de diagnóstico do Exchange</p></li>
</ul>
<p>Partições de disco que contêm os seguintes tipos de arquivos podem ser formatadas como ReFS:</p>
<ul>
<li><p>Partições contendo arquivos de log de transações</p></li>
<li><p>Partições que contêm arquivos de banco de dados</p></li>
<li><p>Partições que contêm os arquivos de indexação de conteúdo</p></li>
</ul></td>
<td><p>Nenhum(a).</p></td>
</tr>
</tbody>
</table>


## Sistema operacional

A tabela a seguir lista os sistemas operacionais compatíveis com o Exchange 2013.


> [!IMPORTANT]
> Nós não suportamos a instalação do Exchange 2013 em um computador que está funcionando no modo Windows Server Core. O computador deve estar executando a instalação completa do Windows Server. Se você quiser instalar o Exchange 2013 em um computador funcionando no modo Windows Server Core, você deve converter o servidor para uma instalação completa do Windows Server, executando um destes procedimentos: 
> <UL>
> <LI>
> <P><STRONG>Windows Server 2008 R2</STRONG>&nbsp;&nbsp;&nbsp;Reinstale o Windows Server e selecione a opção <STRONG>Instalação Completa</STRONG>.</P>
> <LI>
> <P><STRONG>Windows Server 2012 R2</STRONG>&nbsp;ou <STRONG>Windows Server 2012</STRONG>&nbsp;&nbsp;Converta o seu servidor para o modo Windows Server Core em uma instalação completa executando o comando a seguir.</P>
  ```powershell
    Install-WindowsFeature Server-Gui-Mgmt-Infra, Server-Gui-Shell -Restart
  ```  
> </LI>
> </UL>



**Sistemas operacionais compatíveis com o Exchange 2013**


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Componente</th>
<th>Requisito</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Funções de servidor Caixa de Correio, Acesso para Cliente e Transporte de Borda</p></td>
<td><p>Uma destas opções:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard ou Datacenter1</p></li>
<li><p>Windows Server 2012 Standard ou Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard com Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Enterprise com Service Pack 1 (SP1)</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM ou posterior</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Ferramentas de gerenciamento</p></td>
<td><p>Uma destas opções:</p>
<ul>
<li><p>Windows Server 2012 R2 Standard ou Datacenter1</p></li>
<li><p>Windows Server 2012 Standard ou Datacenter</p></li>
<li><p>Windows Server 2008 R2 Standard com SP1</p></li>
<li><p>Windows Server 2008 R2 Enterprise com SP1</p></li>
<li><p>Windows Server 2008 R2 Datacenter RTM ou posterior</p></li>
<li><p>Edição de 64 bits do Windows 8.12</p></li>
<li><p>Edição de 64 bits do Windows 8</p></li>
<li><p>Edição de 64 bits do Windows 7 com Service Pack 1</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   O Windows Server 2012 R2 é compatível apenas com o Exchange 2013 SP1 ou posterior.

2   O Windows 8.1 é compatível apenas com o Exchange 2013 SP1 ou posterior.

**Versões do Windows Management Framework compatíveis com Exchange 2013**

O Exchange 2013 só é compatível com a versão do Windows Management Framework que está inserida na versão do Windows em que você está instalando o Exchange. Não instale versões do Windows Management Framework que estão disponíveis como downloads autônomos em servidores que executam o Exchange.

## .NET Framework

É altamente recomendável que você use a versão mais recente do .NET Framework compatível com a versão do Exchange que você está instalando.


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
<th>Versão do Exchange</th>
<th>.NET Framework 4.7.1</th>
<th>.NET Framework 4.6.2</th>
<th>.NET Framework 4.6.1</th>
<th>.NET Framework 4.5.2</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange 2013 CU19</p></td>
<td><p>X</p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU16 - CU18</p></td>
<td><p></p></td>
<td><p>X</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Clientes suportados

O Exchange 2013 oferece suporte às seguintes versões do Outlook e do Entourage para Mac:

  - Outlook 2016

  - Outlook 2013

  - Outlook 2010

  - Outlook 2007

  - Entourage 2008 para Mac, Web Services Edition

  - Outlook para Mac do Office 365

  - Outlook para Mac 2011

Para obter uma lista de versões do Outlook que oferecem suporte ao Exchange, confira [Atualizações do Outlook](https://go.microsoft.com/fwlink/p/?linkid=513459).


> [!IMPORTANT]
> Recomendamos enfaticamente que você instale os service packs e as atualizações mais recentes disponíveis, de modo que os usuários tenham a melhor experiência possível ao se conectarem ao Exchange.



Os clientes do Outlook anteriores ao Outlook 2007 não têm suporte. Não há suporte para clientes de email de sistemas operacionais Mac que exigem DAV, como o Entourage 2008 for Mac RTM e o Entourage 2004.

O Outlook Web App dá suporte para vários navegadores em diversos sistemas operacionais e dispositivos. Para obter informações detalhadas, consulte [Novidades do Outlook Web App no Exchange 2013](what-s-new-for-outlook-web-app-in-exchange-2013-exchange-2013-help.md).

