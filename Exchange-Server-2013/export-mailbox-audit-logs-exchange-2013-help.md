---
title: 'Exportar logs de auditoria de caixas de correio: Exchange Online Help'
TOCTitle: Exportar logs de auditoria de caixas de correio
ms:assetid: b458a95a-3321-4647-8884-cf97f8e7186a
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150552(v=EXCHG.150)
ms:contentKeyID: 50484815
ms.date: 04/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Exportar logs de auditoria de caixas de correio

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-04-07_

Quando a auditoria de caixas de correio é habilitada para uma caixa de correio, o Microsoft Exchange registra informações no *log de auditoria de caixas de correio* sempre que um usuário, que não for o proprietário, acessar a caixa de correio. Cada entrada de log inclui informações sobre quem acessou a caixa de correio e quando ela foi acessada, as ações executadas pelo não proprietário e se a ação foi bem-sucedida. Entradas no log de auditoria de caixa de correio são mantidas por 90 dias, por padrão. Você poderá usar o log de auditoria de caixas de correio quando um usuário, que não for o proprietário, tiver acessado uma caixa de correio.

Quando você exporta entradas dos logs de auditoria de caixas de correio, o Microsoft Exchange salva as entradas em um arquivo XML e o anexa a uma mensagem de email enviada aos destinatários especificados.

**Sumário**

Antes de começar

Configurar o log de auditoria de caixas correio

Exportar o log de auditoria de caixas de correio

Exibir o log de auditoria de caixas de correio

Mais informações

## Antes de começar

  - Tempo estimado para concluir cada procedimento: Os tempos variam. No Exchange Online, o log de auditoria de caixa de correio é enviado alguns dias depois de exportado.

  - No Exchange Online, é preciso usar o Windows PowerShell remoto para executar muitos dos procedimentos descritos neste tópico. Para saber mais, confira [Conectar-se ao Exchange Online usando o PowerShell Remoto](https://technet.microsoft.com/pt-br/library/jj984289\(v=exchg.150\)).

  - Os procedimentos neste tópico exigem permissões específicas. Consulte cada procedimento para ver informações sobre permissões.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Configurar o log de auditoria de caixas correio

Você precisa habilitar o log de auditoria de caixas de correio em cada caixa de correio que desejar auditar para poder exportar e exibir os logs de auditoria de caixas de correio. É necessário configurar também o Microsoft Outlook Web App para permitir que anexos de XML utilizem o Outlook Web App para acessar o log de auditoria.

## Etapa 1: Habilitar log de auditoria de caixas de correio

Você precisa habilitar o log de auditoria de caixas de correio em cada caixa de correio para a qual desejar executar um relatório de acesso não proprietário. Se o log de auditoria de caixas de correio não for habilitado para uma caixa de correio, você não obterá nenhum resultado para ela ao exportar o log de auditoria de caixas de correio.

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Log de auditoria de caixas de correio" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

Para habilitar o log de auditoria de caixas de correio para uma única caixa de correio, execute o seguinte comando no Shell:

    Set-Mailbox <Identity> -AuditEnabled $true

Para habilitar os logs de auditoria de caixas de correio para todas as caixas de correio de usuário da sua organização, execute os seguintes comandos:

    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}

    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}

## Etapa 2: Configurar o Outlook Web App para permitir anexos de XML

Quando você exporta o log de auditoria de caixas de correio, o Microsoft Exchange anexa o log de auditoria, que é um arquivo XML, a uma mensagem de email. No entanto, o Outlook Web App bloqueia anexos de XML por padrão. Para acessar o log de auditoria exportado, é necessário usar o Microsoft Outlook ou configurar o Outlook Web App para permitir anexos de XML.

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Políticas de caixa de correio do Outlook Web App", no tópico [Permissões de dispositivos móveis e clientes](clients-and-mobile-devices-permissions-exchange-2013-help.md).

Execute os procedimentos a seguir para permitir anexos XML no Outlook Web App. No Exchange Server 2013, use o valor `Default` para o parâmetro *Identity*.

1.  Execute o seguinte comando para adicionar XML à lista de tipos de arquivos permitidos no Outlook Web App.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -AllowedFileTypes @{add='.xml'}

2.  Execute o seguinte comando para remover XML da lista de tipos de arquivos bloqueados no Outlook Web App.
    
        Set-OwaMailboxPolicy -Identity OwaMailboxPolicy-Default -BlockedFileTypes @{remove='.xml'}

## Como saber se funcionou?

Para verificar se o log de auditoria de caixas de correio foi configurado com sucesso, faça o seguinte:

1.  Execute o comando a seguir para verificar se os logs de auditoria foram configurados para as caixas de correio.
    
        Get-Mailbox | FL Name,AuditEnabled
    
    O valor de `True` referente à propriedade *AuditEnabled* verifica se os logs de auditoria estão habilitados.

2.  Execute o seguinte comando para verificar se são permitidos anexos XML no Outlook Web App.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty AllowedFileTypes
    
    Verifique se `.xml` foi incluído na lista de tipos de arquivos permitidos.

3.  Execute o seguinte comando para garantir que anexos XML sejam removidos da lista de arquivos bloqueados no Outlook Web App.
    
        Get-OwaMailboxPolicy | Select-Object -ExpandProperty BlockedFileTypes
    
    Verifique se `.xml` não foi incluído na lista de tipos de arquivos bloqueados.

Voltar ao início

## Exportar o log de auditoria de caixas de correio

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Registro em log de auditoria do administrador somente leitura" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

1.  No Centro de administração do Exchange (EAC), acesse **Gerenciamento de Conformidade** \> **Auditoria**.

2.  Clique em **Exportar os logs de auditoria de caixas de correio**.

3.  Configure os seguintes critérios de pesquisa para exportar as entradas do log de auditoria de caixas de correio:
    
      - **Datas de início e término**   Selecione o intervalo de data para as entradas para incluir no arquivo exportado.
    
      - **Caixas de correio nas quais procurar logs de auditoria**   Selecione as caixas de correio para as quais recuperar entradas do log de auditoria.
    
      - **Tipo de acesso não proprietário**   Selecione uma das opções a seguir para definir o tipo de acesso não proprietário para o qual recuperar entradas:
        
          - **Todos os não proprietários**   Pesquise o acesso por administradores e usuários delegados dentro da organização e por administradores de datacenter Microsoft no Exchange Online.
        
          - **Usuários externos**   Pesquisa acesso somente por administradores de datacenter Microsoft.
        
          - **Administradores e usuários delegados**   Procura acesso por administradores e usuários delegados dentro da organização.
        
          - **Administradores**   Procura acesso por administradores em sua organização.
    
      - **Destinatários**   Selecione os usuários aos quais enviar o log de auditoria de caixas de correio.

4.  Clique em **Exportar**.
    
    O Microsoft Exchange recupera as entradas do log de auditoria de caixas de correio que atendem aos critérios de pesquisa, salva-as em um arquivo chamado SearchResult.xml e anexa o arquivo XML a uma mensagem de email enviada aos destinatários que você especificar.

## Como saber se funcionou?

Entre na caixa de correio para a qual o log de auditoria de caixas de correio foi enviado. Se você exportou com êxito o log de auditoria, receberá uma mensagem enviada do Exchange. No Exchange Online, pode levar alguns dias para receber essa mensagem. O log de auditoria de caixa de correio (chamado SearchResult.xml) será anexado a esta mensagem. Se você configurou corretamente o Outlook Web App para permitir anexos XML, pode baixar o arquivo XML anexado.

Voltar ao início

## Exibir o log de auditoria de caixas de correio

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Registro em log de auditoria do administrador somente leitura" no tópico [Permissões de infraestrutura do Exchange e do Shell](exchange-and-shell-infrastructure-permissions-exchange-2013-help.md).

Para salvar e exibir o arquivo SearchResult.xml:

1.  Entre na caixa de correio para a qual o log de auditoria de caixas de correio foi enviado.

2.  Na Caixa de Entrada, abra a mensagem com o anexo de arquivo XML enviado pelo Microsoft Exchange. Observe que o corpo da mensagem de email contém os critérios de pesquisa.

3.  Clique no anexo e selecione para baixar o arquivo XML.

4.  Abra o SearchResult.xml no Microsoft Excel.

Voltar ao início

## Mais informações

  - **Entradas no log de auditoria de caixa de correio**   O exemplo a seguir mostra uma entrada do log de auditoria de caixa de correio contido no arquivo SearchResult.xml. Cada entrada é precedida pela marca XML **\<Event\>** e termina com a marca XML **\</Event\>**. Essa entrada mostra que o administrador eliminou a mensagem com o assunto "**Notification of litigation hold**" da pasta Itens Recuperáveis na caixa de correio de David no dia 30 de abril de 2010.
    
        <Event MailboxGuid="6d4fbdae-e3ae-4530-8d0b-f62a14687939" 
          Owner="PPLNSL-dom\david50001-1363917750" 
          LastAccessed="2010-04-30T11:01:55.140625-07:00" 
          Operation="HardDelete" 
          OperationResult="Succeeded" 
          LogonType="Admin"
         FolderId="0000000073098C3277988F4CB882F5B82EBF64610100A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000"
          FolderPathName="\Recoverable Items\Deletions"
          ClientInfoString="Client=OWA;Action=ViaProxy" 
          ClientIPAddress="10.196.241.168" 
          InternalLogonType="Owner"
          MailboxOwnerUPN="david@contoso.com"
          MailboxOwnerSid="S-1-5-21-290112810-296651436-1966561949-1151" 
          CrossMailboxOperation="false" 
          LogonUserDN="Administrator"
          LogonUserSid="S-1-5-21-290112810-296651436-1966561949-1149">
          <SourceItems>
           <ItemId="0000000073098C3277988F4CB882F5B82EBF64610700A7C317F68C24304BBD18ABE1F185E79B00000026BD4F0000A7C317F68C24304BBD18ABE1F185E79B00000026BD540"
            Subject="Notification of litigation hold"
            FolderPathName="\Recoverable Items\Deletions" /> 
          </SourceItems>
        </Event>

  - **Campos úteis no log de auditoria de caixa de correio**   Eis uma descrição dos campos úteis no log de auditória de caixa de correio. Eles podem ajudar a identificar informações específicas sobre cada instância de acesso não proprietário de uma caixa de correio.
    
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Campo</th>
    <th>Descrição</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><strong>Owner</strong></p></td>
    <td><p>O proprietário da caixa de correio que foi acessada por um não proprietário.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>LastAccessed</strong></p></td>
    <td><p>A data e a hora em que a caixa de correio foi acessada.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Operation</strong></p></td>
    <td><p>A ação que foi executada pelo não proprietário. Para obter mais informações, confira a seção &quot;O que é registrado no log de auditoria de caixas de correio?&quot; em <a href="https://technet.microsoft.com/pt-br/library/jj156300(v=exchg.150)">Saiba mais sobre como executar um relatório de acesso não proprietário da caixa de correio</a>.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>OperationResult</strong></p></td>
    <td><p>Se a ação executada pelo não proprietário foi bem-sucedida ou falhou.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonType</strong></p></td>
    <td><p>O tipo de acesso não proprietário. Isso inclui administrador, delegado e externo.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>FolderPathName</strong></p></td>
    <td><p>O nome da pasta que continha a mensagem que foi afetada pelo não proprietário.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>ClientInfoString</strong></p></td>
    <td><p>Informações sobre o cliente de email usado pelo não proprietário para acessar a caixa de correio.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>ClientIPAddress</strong></p></td>
    <td><p>O endereço IP do computador usado pelo não proprietário para acessar a caixa de correio.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>InternalLogonType</strong></p></td>
    <td><p>O tipo de logon da conta usado pelo não proprietário para acessar essa caixa de correio.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>MailboxOwnerUPN</strong></p></td>
    <td><p>O endereço de email do proprietário da caixa de correio.</p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>LogonUserDN</strong></p></td>
    <td><p>O nome para exibição do não proprietário.</p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Subject</strong></p></td>
    <td><p>A linha de assunto da mensagem de email que foi afetada pelo não proprietário.</p></td>
    </tr>
    </tbody>
    </table>
    
    Voltar ao início

