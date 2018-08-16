---
title: 'MAPI sobre HTTP: Exchange 2013 Help'
TOCTitle: MAPI sobre HTTP
ms:assetid: 4663b5db-5b30-4a5a-a302-be6fef7fe5da
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn635177(v=EXCHG.150)
ms:contentKeyID: 61203503
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# MAPI sobre HTTP

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2017-05-10_

Messaging Application Programming Interface (MAPI) sobre HTTP é um novo protocolo de transporte implementado no MicrosoftExchange Server 2013 Service Pack 1 (SP1). MAPI sobre HTTP melhora a confiabilidade e a estabilidade das conexões Outlook e Exchange ao mover a camada de transporte para o modelo HTTP padrão do setor. Isso permite que um nível mais alto de visibilidade de erros de transporte e capacidade de recuperação avançada. Funcionalidade adicional inclui suporte para uma função de pausar e continuar explícita. Isso permite que os clientes com suporte alterar redes ou retornar da hibernação, mantendo o mesmo contexto de servidor.

Implementar MAPI sobre HTTP não significa que é o único protocolo que pode ser usado para Outlook para acessar Exchange. Outlook clientes que não sejam MAPI sobre HTTP capaz ainda podem usar Outlook em qualquer lugar (RPC sobre HTTP) para acessar o Exchange através de um servidor de acesso para cliente habilitado a MAPI.

## Benefícios de MAPI sobre HTTP

MAPI sobre HTTP oferece os seguintes benefícios para clientes com suporte:

  - Permite inovação futura em autenticação usando um protocolo baseado em HTTP.

  - Oferece tempos de reconexão mais rápidos após uma interrupção nas comunicações porque somente conexões TCP, e não conexões RPC, precisam ser recriadas. Exemplos de uma interrupção de comunicação incluem:
    
      - Hibernação do dispositivo
    
      - Alterar de uma rede com fio para uma rede sem fio ou celular

  - Oferece um contexto de sessão que não depende da conexão. O servidor mantém o contexto de sessão por um período configurável, mesmo se o usuário trocar de redes.

## Implantar MAPI sobre HTTP

Considere os seguintes requisitos para habilitar MAPI sobre HTTP.

  - **Capacidade de suporte**   Verifique se as versões de configuração desejadas são compatíveis.

  - **Pré-requisitos**   Verifique se o seu ambiente foi atualizado e se está preparado para MAPI sobre HTTP.

  - **Configuração**   Configure os diretórios virtuais e habilite MAPI para sua organização.

## Capacidade de suporte

Use a matriz a seguir para verificar se seus clientes e servidores oferecem suporte a MAPI sobre HTTP.


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
<th>Produto</th>
<th>Exchange 2013 SP1</th>
<th>Exchange 2013 RTM</th>
<th>Exchange 2010 SP3</th>
<th>Exchange 2007 SP3</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Outlook 2013 SP1</p></td>
<td><ul>
<li><p>MAPI sobre HTTP</p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
<td><p>Outlook em Qualquer Lugar</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2013 RTM</p></td>
<td><p>Outlook em Qualquer Lugar</p></td>
<td><p>Outlook em Qualquer Lugar</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2010 SP2 e atualizações KB2956191 e KB2965295 (14 de abril de 2015)</p></td>
<td><ul>
<li><p>MAPI sobre HTTP<span></span></p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
<td><p>Outlook em Qualquer Lugar</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Outlook 2010 SP2 e versões anteriores</p></td>
<td><p>Outlook em Qualquer Lugar</p></td>
<td><p>Outlook em Qualquer Lugar</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Outlook 2007</p></td>
<td><p>Outlook em Qualquer Lugar</p></td>
<td><p>Outlook em Qualquer Lugar</p></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
<td><ul>
<li><p>RPC</p></li>
<li><p>Outlook em Qualquer Lugar</p></li>
</ul></td>
</tr>
</tbody>
</table>


## Pré-requisitos

Conclua as etapas a seguir para preparar os clientes e servidores para oferecer suporte a MAPI sobre HTTP.

1.  Atualize clientes OutlookOutlook 2013 SP1 ou Outlook 2010 SP2 e atualizações KB2956191 e KB2965295 (14 de abril de 2015).

2.  Atualize servidores de Acesso para Cliente e de Caixa de Correio para o Exchange 2013 SP1. Para obter informações sobre como atualizar, consulte [Atualizar o Exchange 2013 para a atualização cumulativa ou pacote de serviço mais recente](upgrade-exchange-2013-to-the-latest-cumulative-update-or-service-pack-exchange-2013-help.md).
    

    > [!NOTE]
    > Todos os servidores de Acesso para Cliente devem ser atualizados para Exchange 2013 SP1 antes da habilitação de MAPI sobre HTTP. Caso contrário, poderá ocorrer uma falha durante a conexão do Outlook a caixas de correio.<BR>Se todos os servidores de Caixa de Correio em um Grupo de Disponibilidade de Banco de Dados (DAG) não forem atualizados, poderá haver atrasos de email e o cliente solicitará a reinicialização do Outlook em caso de um failover do banco de dados.



3.  Em todos os servidores de Exchange 2013, você precisa instalar Microsoft.NET Framework 4.5.2. Para obter mais informações, consulte [instalação do .NET Framework](https://go.microsoft.com/fwlink/p/?linkid=518380).

4.  Em todos os servidores de Acesso para Cliente do Exchange 2013 SP1, adicione a variável de ambiente **COMPLUS\_DisableRetStructPinning** do Windows executando as seguintes etapas.
    
    1.  Em uma janela do Prompt de Comando, execute `systempropertiesadvanced` e clique em **Variáveis de ambiente**.
    
    2.  Na seção de **Variáveis de sistema**, clique em **Novo** e insira as seguintes informações.
        
          - **Nome da variável**   `COMPLUS_DisableRetStructPinning`
        
          - **Valor da variável** 1
    
    3.  Quando terminar, clique em **OK**.

## Configuração

Conclua as etapas a seguir para configurar MAPI sobre HTTP para sua organização.

1.  **Configuração de diretório virtual**   Por padrão, o Exchange 2013 SP1 cria um diretório virtual para MAPI sobre HTTP. Use o cmdlet **Set-MapiVirtualDirectory** para configurar o diretório virtual. Você deve configurar uma URL interna, uma URL externa ou ambas. Para mais informações, consulte [Set-MapiVirtualDirectory](https://technet.microsoft.com/pt-br/library/dn595082\(v=exchg.150\)).
    
    Por exemplo, para configurar o diretório virtual MAPI padrão no servidor Exchange local configurando o valor da URL interna como https://contoso.com/mapi e o método de autenticação como `Negotiate`, execute o seguinte comando:
    
        Set-MapiVirtualDirectory -Identity "Contoso\mapi (Default Web Site)" -InternalUrl https://Contoso.com/mapi -IISAuthenticationMethods Negotiate

2.  **Configuração de certificado**   O certificado digital usado por seu ambiente Exchange deve incluir os mesmos valores de *InternalURL* e de *ExternalURL* definidos no diretório virtual MAPI. Para obter mais informações sobre o gerenciamento de certificados do Exchange 2013, consulte [Certificados digitais e SSL](digital-certificates-and-ssl-exchange-2013-help.md). Verifique se o certificado do Exchange é confiável na estação de trabalho cliente do Outlook e se não há erros de certificados, especialmente quando você acessa as URLs configuradas no diretório virtual MAPI.

3.  **Atualizar regras do servidor**   Verifique se seus balanceadores de carga, proxies reversos e firewalls estão configurados para permitir o acesso ao diretório virtual do MAPI sobre HTTP.

4.  **Habilitar MAPI sobre HTTP em sua organização do Exchange**
    
    Execute o seguinte comando:
    
        Set-OrganizationConfig -MapiHttpEnabled $true

## Testar conexões MAPI sobre HTTP

Você pode testar a conexão MAPI sobre HTTP de ponta a ponta usando o cmdlet **Test-OutlookConnectivity**. Para usar o cmdlet **Test-OutlookConnectivity**, o serviço Gerenciador de Integridade do Microsoft Exchange (MSExchangeHM) deve ser iniciado.

O exemplo a seguir testa a conexão MAPI sobre HTTP do servidor Exchange chamado ContosoMail.

    Test-OutlookConnectivity -RunFromServerId ContosoMail -ProbeIdentity OutlookMapiHttpSelfTestProbe

Um teste bem-sucedido retorna um resultado semelhante ao exemplo a seguir:

    MonitorIdentity                                          StartTime              EndTime                Result      Error     Exception
    ---------------                                          ---------              -------                ------      -----     ---------
    OutlookMapiHttp.Protocol\OutlookMapiHttpSelfTestProbe    2/14/2014 7:15:00 AM   2/14/2014 7:15:10 AM   Succeeded

Para obter mais informações, consulte [Test-OutlookConnectivity](https://technet.microsoft.com/pt-br/library/dd638082\(v=exchg.150\)).

Os logs da atividade de MAPI sobre HTTP estão nos seguintes locais:

  - %CaminhoInstalaçãoExchange%Logging\\MAPI Address Book Service\\

  - %CaminhoInstalaçãoExchange%Logging\\MAPI Client Access\\

  - %ExchangeInstallPath%Logging\\HttpProxy\\Mapi\\

## Gerenciar MAPI sobre HTTP

Você pode gerenciar a configuração de MAPI sobre HTTP usando os seguintes cmdlets:

  - [Set-MapiVirtualDirectory](https://technet.microsoft.com/pt-br/library/dn595082\(v=exchg.150\))

  - [Get-MapiVirtualDirectory](https://technet.microsoft.com/pt-br/library/dn595080\(v=exchg.150\))

  - [New-MapiVirtualDirectory](https://technet.microsoft.com/pt-br/library/dn595081\(v=exchg.150\))

  - [Remove-MapiVirtualDirectory](https://technet.microsoft.com/pt-br/library/dn595083\(v=exchg.150\))

