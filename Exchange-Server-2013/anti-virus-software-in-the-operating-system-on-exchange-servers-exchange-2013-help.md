---
title: 'Software Antivírus no Sistema Operacional em Servidores do Exchange: Exchange 2013 Help'
TOCTitle: Software Antivírus no Sistema Operacional em Servidores do Exchange
ms:assetid: 7cef6017-7a55-41f3-a636-1ca4fce575b1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Bb332342(v=EXCHG.150)
ms:contentKeyID: 50485992
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Software Antivírus no Sistema Operacional em Servidores do Exchange

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-07-22_

Este tópico descreve os efeitos de programas antivírus em nível de arquivo, em computadores que executam o Microsoft Exchange Server 2013. Se você implantou as recomendações descritas neste tópico, você poderá ajudar a aprimorar a segurança e a integridade de sua organização do Exchange.

Verificadores de vírus em nível de arquivo são usados com freqüência. No entanto, se forem configurados incorretamente, poderão causar problemas no Exchange 2013. Há dois tipos de verificadores de vírus em nível de arquivo:

  - *Verificação em nível de arquivo residente em memória* refere-se a uma parte de software antivírus em nível de arquivo que sempre é carregada na memória. Ela verifica todos os arquivos utilizados no disco rígido e na memória do computador.

  - *Verificação em nível de arquivo sob demanda* refere-se a uma parte do software antivírus em nível de arquivo que você pode configurar para verificar arquivos no disco rígido manualmente ou com base em uma agenda. Algumas versões de software antivírus iniciam a verificação sob demanda automaticamente depois que assinaturas de vírus são atualizadas, para garantir que todos os arquivos sejam verificados com as assinaturas mais recentes.

Os seguintes problemas podem ocorrer na utilização de verificadores de vírus em nível de arquivo com o Exchange 2013:

  - Verificadores de vírus em nível de arquivo podem verificar um arquivo quando ele estiver sendo usado ou em intervalos agendados. Isso pode fazer com que os verificadores bloqueiem ou coloquem em quarentena um arquivo de log ou banco de dados do Exchange, quando o Exchange 2013 tentar usar o arquivo. Esse comportamento pode causar uma falha grave no Exchange 2013 e também pode gerar erros de log de eventos -1018.

  - Verificadores de vírus em nível de arquivo não oferecem proteção contra vírus de email, como o worm Storm. O worm Storm era um cavalo-de-troia backdoor que se propagava através de emails. O worm fazia o computador infectado entrar em uma botnet, em que o computador era usado para enviar spam em levas periódicas.

## Recomendações para o uso de verificação de nível de arquivo com o Exchange 2013

Se você estiver implantando verificadores de vírus em nível de arquivo em servidores do Exchange 2013, certifique-se de que as exclusões apropriadas, como exclusões de diretório, de processo e de extensão de nome de arquivo, estejam no lugar para verificações residentes na memória e em nível de arquivo. Esta seção descreve as exclusões de diretório recomendadas, exclusões de processos e exclusões de nomes de arquivo.

**Sumário**

Directory exclusions

Process exclusions

File name extension exclusions

## Exclusões de diretório

Você deve excluir diretórios específicos de cada servidor Exchange em que um verificador antivírus em nível de arquivo seja executado. Esta seção descreve os diretórios que você deve excluir da verificação no nível de arquivo.

  - **servidores de Caixa de Correio**
    
      - **Bancos de dados de caixa de correio**
        
          - Bancos de dados, arquivos de ponto de verificação e arquivos de log do Exchange. Por padrão, eles estão localizados em subpastas da pasta %ExchangeInstallPath%Mailbox. Para determinar a localização de um banco de dados de caixa de correio, log de transações e arquivo de ponto de verificação, execute o seguinte comando: `Get-MailboxDatabase -Server <servername>| Format-List *path*`
        
          - Índices de conteúdo de banco de dados. Por padrão, eles estão na mesma pasta que o arquivo do banco de dados.
        
          - Arquivos de métrica de grupo. Por padrão, eles estão localizados na pasta %ExchangeInstallPath%GroupMetrics.
        
          - Arquivos de log gerais, como arquivos de log de controle de mensagens e de reparo de calendário. Por padrão, esses arquivos estão localizados em subpastas nas pastas %ExchangeInstallPath%TransportRoles\\Logs e %ExchangeInstallPath%Logging. Para determinar os caminhos de log que estão sendo utilizados, execute o seguinte comando no Shell de Gerenciamento do Exchange: `Get-MailboxServer <servername> | Format-List *path*`
        
          - Os arquivos de catálogo de endereços offline. Por padrão, eles estão localizados em subpastas na pasta %ExchangeInstallPath%ClientAccess\\OAB.
        
          - Arquivos de sistema IIS na pasta %SystemRoot%\\System32\\Inetsrv.
        
          - A pasta temporária de banco de dados de Caixa de Correio: %ExchangeInstallPath%Mailbox\\MDBTEMP
    
      - **Membros de Grupos de Disponibilidade de Banco de Dados**
        
          - Todos os itens listados em **Bancos de dados de caixa de correio** e o banco de dados de quórum de cluster que existe em %Windir%\\Cluster.
        
          - Os arquivos do diretório testemunha. Esses arquivos estão localizados em outro servidor no ambiente, normalmente em um servidor de Acesso para Cliente que não está instalado no mesmo computador que um servidor de Caixa de Correio. Por padrão, os arquivos de diretório testemunha estão localizados em %SystemDrive%:\\DAGFileShareWitnesses\\\<DAGFQDN\>.
    
      - **Serviço de Transporte**
        
          - Arquivos de log, por exemplo, rastreamento de mensagens e logs de conectividade. Por padrão, esses arquivos estão localizados em subpastas na pasta %ExchangeInstallPath%TransportRoles\\Logs. Para determinar os caminhos de log que estão sendo utilizados, execute o seguinte comando no Shell de Gerenciamento do Exchange: `Get-TransportService <servername> | Format-List *logpath*,*tracingpath*`
        
          - Pastas do diretório de mensagem de retirada e repetição. Por padrão, essas pastas estão localizadas na pasta % Caminhoinstalaçãoexchange % TransportRoles. Para determinar os caminhos que está sendo usados, execute o seguinte comando no Exchange Shell de gerenciamento: `Get-TransportService <servername>| Format-List *dir*path*`
        
          - Os bancos de dados de fila, pontos de verificação e arquivos de log. Por padrão, eles estão localizados na pasta %ExchangeInstallPath%TransportRoles\\Data\\Queue.
        
          - O banco de dados da Reputação do Remetente da função de servidor de transporte, ponto de verificação e arquivos de log. Por padrão, eles estão localizados na pasta %ExchangeInstallPath%TransportRoles\\Data\\SenderReputation.
        
          - As pastas temporárias que são utilizadas para realizar conversões:
            
              - Por padrão, as conversões de conteúdo são realizadas na pasta %TMP% do servidor do Exchange.
            
              - Por padrão, o formato rich text (RTF) para conversões de MIME/HTML são executadas na pasta %ExchangeInstallPath%\\Working\\OleConverter.
        
          - O componente de verificação de conteúdo é usado pelo agente de Malware e pela prevenção de perda de dados (DLP). Por padrão, esses arquivos estão localizados na pasta %ExchangeInstallPath%FIP-FS.
    
      - **Serviço de Transporte de Caixa de Correio**
        
          - Arquivos de log, por exemplo, logs de conectividade. Por padrão, esses arquivos estão localizados em subpastas na pasta %ExchangeInstallPath%TransportRoles\\Logs\\Mailbox. Para determinar os caminhos de log que estão sendo utilizados, execute o seguinte comando no Shell de Gerenciamento do Exchange: `Get-MailboxTransportService <servername> | Format-List *logpath*`
    
      - **Unificação de Mensagens**
        
          - Os arquivos de gramática para localidades diferentes, por exemplo, en-EN ou es-ES. Por padrão, eles são armazenados nas subpastas na pasta %ExchangeInstallPath%UnifiedMessaging\\grammars.
        
          - Os prompts de voz, saudações e arquivos de mensagem informativa. Por padrão, eles são armazenados nas subpastas na pasta %ExchangeInstallPath%UnifiedMessaging\\Prompts
        
          - Os arquivos de caixa postal são temporariamente armazenados na pasta %ExchangeInstallPath%UnifiedMessaging\\voicemail.
        
          - Os arquivos temporários gerados pela Unificação de mensagens. Por padrão, eles são armazenados na pasta %ExchangeInstallPath%UnifiedMessaging\\temp.
    
      - **Instalação**
        
          - Arquivos temporários de instalação do Exchange Server. Normalmente, esses arquivos estão localizados na pasta % SystemRoot%\\Temp\\ExchangeSetup.
    
      - **Serviço de pesquisa do Exchange**
        
          - Arquivos temporários usados pelo serviço de pesquisa do Exchange e Microsoft Filter Pack para realizar a conversão de arquivo em um ambiente de área restrita. Esses arquivos estão localizados em %SystemRoot%\\Temp\\OICE\_*\<GUID\>*\\.

<!-- end list -->

  - **Servidores de Acesso para Cliente**
    
      - **Componentes Web**
        
          - Para servidores usando o IIS (Serviços de Informações da Internet) 7.0, a pasta de compactação que é utilizada com o Microsoft Outlook Web App. Por padrão, a pasta de compactação no IIS 7.0 está localizada em %UnidadeDoSistema%\\inetpub\\temp\\Arquivos temporários compactados do IIS.
        
          - Arquivos de sistema IIS na pasta %SystemRoot%\\System32\\Inetsrv
        
          - Inetpub\\logs\\logfiles\\w3svc
        
          - Subpastas nos arquivos do ASP.NET %SystemRoot%\\Microsoft.NET\\Framework64\\v4.0.30319\\Temporary
    
      - **Registro em log dos protocolos POP3 e IMAP4**
        
          - Pasta POP3: %ExchangeInstallPath%Logging\\POP3
        
          - Pasta IMAP4: %ExchangeInstallPath%Logging\\IMAP4
    
      - **Serviço de Transporte de Front End**
        
          - Arquivos de log, por exemplo, logs de conectividade e logs de protocolo. Por padrão, esses arquivos estão localizados em subpastas na pasta %ExchangeInstallPath%TransportRoles\\Logs\\FrontEnd. Para determinar os caminhos de log que estão sendo utilizados, execute o seguinte comando no Shell de Gerenciamento do Exchange: `Get-FrontEndTransportService <servername> | Format-List *logpath*`
    
      - **Instalação**
        
          - Arquivos temporários de instalação do Exchange Server. Normalmente, esses arquivos estão localizados na pasta % SystemRoot%\\Temp\\ExchangeSetup.

Voltar ao início

## Exclusões de processos

Muitos verificadores em nível de arquivo agora suportam a verificação de processos, o que pode afetar negativamente o Microsoft Exchange, se os processos incorretos forem verificados. Portanto, é necessário excluir os seguintes processos dos verificadores de vírus em nível de arquivo.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Processo</th>
<th>Caminho</th>
<th>Comentários</th>
<th>Servidores</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Dsamain.exe</p></td>
<td><p>%SystemRoot%\System32</p></td>
<td><p>Active Directory Lightweight Directory Services (AD LDS) nos servidores de transporte de Borda inscritos.</p></td>
<td><p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="even">
<td><p>EdgeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processo de trabalho do serviço de transporte do Microsoft Exchange</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="odd">
<td><p>fms.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente de verificação conteúdo que é usada pelo agente de Malware e DLP.</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>hostcontrollerservice.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\HostController</p></td>
<td><p>Serviço do controlador de Host de pesquisa do Microsoft Exchange (HostControllerService)</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Acesso para Cliente</p></td>
</tr>
<tr class="odd">
<td><p>inetinfo.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Serviços de Informações da Internet (IIS)</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Acesso para Cliente</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.AntispamUpdateSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de atualização de anti-spam do Microsoft Exchange (MSExchangeAntispamUpdate)</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.ContentFilter.Wrapper.exe</p></td>
<td><p>%ExchangeInstallPath%TransportRoles\agents\Hygiene</p></td>
<td><p>Agente de Filtro de Conteúdo</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Diagnostics.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de diagnóstico do Microsoft Exchange (MSExchangeDiagnostics)</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Acesso para Cliente</p>
<p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Directory.TopologyService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de topologia do Active Directory para Microsoft Exchange (MSExchangeADTopology)</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Acesso para Cliente</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.EdgeCredentialSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de credencial do Microsoft Exchange (MSExchangeEdgeCredential)</p></td>
<td><p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.EdgeSyncSvc.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço Microsoft Exchange EdgeSync (MSExchangeEdgeSync)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Imap4.exe</p></td>
<td><p>ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Serviço IMAP4 do Microsoft Exchange (MSExchangeImap4)</p></td>
<td><p>Servidores de Acesso para Cliente</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Imap4service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Serviço de back-end do Microsoft Exchange IMAP4 (MSExchangeIMAP4BE)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Pop3.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\PopImap</p></td>
<td><p>Serviço Microsoft Exchange POP3 (MSExchangePop3)</p></td>
<td><p>Servidores de Acesso para Cliente</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Pop3service.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\PopImap</p></td>
<td><p>Serviço de back-end do Microsoft Exchange POP3 (MSExchangePOP3BE)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.ProtectedServiceHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de Host de serviço do Microsoft Exchange (MSExchangeServiceHost)</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Acesso para Cliente</p>
<p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.RPCClientAccess.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de acesso para cliente do Microsoft Exchange RPC (MSExchangeRPC)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Search.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de pesquisa do Microsoft Exchange (MSExchangeFastSearch)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Servicehost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de Host de serviço do Microsoft Exchange (MSExchangeServiceHost)</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Acesso para Cliente</p>
<p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.Store.Service.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço do Microsoft Exchange Information Store (MSExchangeIS)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>Microsoft.Exchange.Store.Worker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processo de trabalho do serviço Microsoft Exchange Information Store</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>Microsoft.Exchange.UM.CallRouter.exe</p></td>
<td><p>%ExchangeInstallPath%FrontEnd\CallRouter</p></td>
<td><p>Microsoft Exchange Unified Messaging serviço roteador de chamadas (MSExchangeUMCR)</p></td>
<td><p>Servidores de Acesso para Cliente</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeDagMgmt.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de gerenciamento do Microsoft Exchange DAG (MSExchangeDagMgmt)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeDelivery.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de entrega de transporte de caixa de correio do Microsoft Exchange (MSExchangeDelivery)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeFrontendTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de transporte de front-end do Microsoft Exchange (MSExchangeFrontEndTransport)</p></td>
<td><p>Servidores de Acesso para Cliente</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeHMHost.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de Gerenciador de integridade do Microsoft Exchange (MSExchangeHM)</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Acesso para Cliente</p>
<p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeHMWorker.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processo de trabalho de serviço do Gerenciador de integridade do Microsoft Exchange</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Acesso para Cliente</p>
<p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMailboxAssistants.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de assistentes de caixa de correio do Microsoft Exchange (MSExchangeMailboxAssistants)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeMailboxReplication.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de replicação de caixa de correio do Microsoft Exchange (MSExchangeMailboxReplication)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeMigrationWorkflow.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de fluxo de trabalho de migração do Microsoft Exchange (MSExchangeMigrationWorkflow)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeRepl.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de replicação do Microsoft Exchange (MSExchangeRepl)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeSubmission.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de envio de transporte de caixa de correio do Microsoft Exchange (MSExchangeSubmission)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeTransport.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de transporte do Microsoft Exchange (MSExchangeTransport)</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="even">
<td><p>MSExchangeTransportLogSearch.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de pesquisa de Log de transporte do Microsoft Exchange (MSExchangeTransportLogSearch)</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="odd">
<td><p>MSExchangeThrottling.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de limitação do Microsoft Exchange (MSExchangeThrottling)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>Noderunner.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\Runtime\1.0</p></td>
<td><p>Serviço de pesquisa do Microsoft Exchange (MSExchangeFastSearch)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>OleConverter.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Converte mensagens do rich text format (RTF) para MIME/HTML para destinatários externos.</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>ParserServer.exe</p></td>
<td><p>%ExchangeInstallPath%Bin\Search\Ceres\ParserServer</p></td>
<td><p>Serviço de pesquisa do Microsoft Exchange (MSExchangeFastSearch)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>Powershell.exe</p></td>
<td><p>C:\Windows\System32\WindowsPowerShell\v1.0</p></td>
<td><p>Shell de Gerenciamento do Exchange</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Acesso para Cliente</p>
<p>Servidores de Transporte de Borda</p></td>
</tr>
<tr class="even">
<td><p>ScanEngineTest.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente de verificação conteúdo que é usada pelo agente de Malware e DLP.</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>ScanningProcess.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente de verificação conteúdo que é usada pelo agente de Malware e DLP.</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>TranscodingService.exe</p></td>
<td><p>%ExchangeInstallPath%ClientAccess\Owa\Bin\DocumentViewing</p></td>
<td><p>Exibição de Documento WebReady no Outlook Web App.</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>UmService.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Serviço de Unificação de mensagens do Microsoft Exchange (MSExchangeUM)</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>UmWorkerProcess.exe</p></td>
<td><p>%ExchangeInstallPath%Bin</p></td>
<td><p>Processo de trabalho do serviço de Unificação de mensagens do Microsoft Exchange</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="odd">
<td><p>UpdateService.exe</p></td>
<td><p>%ExchangeInstallPath%FIP-FS\Bin</p></td>
<td><p>Componente de verificação conteúdo que é usada pelo agente de Malware e DLP.</p></td>
<td><p>servidores de Caixa de Correio</p></td>
</tr>
<tr class="even">
<td><p>W3wp.exe</p></td>
<td><p>%SystemRoot%\System32\inetsrv</p></td>
<td><p>Serviços de Informações da Internet (IIS)</p></td>
<td><p>servidores de Caixa de Correio</p>
<p>Servidores de Acesso para Cliente</p></td>
</tr>
</tbody>
</table>


Voltar ao início

## Exclusões de extensão de nome de arquivo

Além de excluir diretórios e processos específicos, você deve excluir as seguinte extensões de nome de arquivo específicas do Exchange, caso as exclusões de diretório falhem ou os arquivos sejam movidos de seus locais-padrão.

  - Extensões relacionadas a aplicativos:
    
      - .config
    
      - .dia
    
      - .wsb

<!-- end list -->

  - Extensões relacionadas a bancos de dados:
    
      - .chk
    
      - .edb
    
      - .jrs
    
      - .jsl
    
      - .log
    
      - .que

<!-- end list -->

  - Extensões relacionadas a Catálogos de Endereços Offline:
    
      - .lzx

<!-- end list -->

  - Extensões relacionadas a Índices de Conteúdo:
    
      - .ci
    
      - .dir
    
      - .wid
    
      - .000
    
      - .001
    
      - .002

<!-- end list -->

  - Extensões relacionadas à Unificação de Mensagens:
    
      - .cfg
    
      - .grxml

<!-- end list -->

  - Extensões relacionadas a Métricas de Grupos:
    
      - .dsc
    
      - .txt

Voltar ao início

