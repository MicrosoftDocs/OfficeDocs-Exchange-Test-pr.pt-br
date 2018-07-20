---
title: 'Usar a migração de lote para migrar pastas públicas do Exchange 2013 para grupos do Office 365: Exchange 2013 Help'
TOCTitle: Usar a migração de lote para migrar pastas públicas do Exchange 2013 para grupos do Office 365
ms:assetid: 1d800576-957d-4916-ae2a-55c08ca75be1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt843873(v=EXCHG.150)
ms:contentKeyID: 74468735
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usar a migração de lote para migrar pastas públicas do Exchange 2013 para grupos do Office 365

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2018-03-26_

**Resumo:**  como mover suas pastas públicas do Exchange 2013 para grupos do Office 365.

Por meio de um processo conhecido como *migração de lote*, você pode mover algumas ou todas as suas pastas públicas do Exchange 2013 aos grupos do Office 365. Grupos é uma nova colaboração oferta da Microsoft que oferece determinadas vantagens sobre pastas públicas. Consulte [Migrar suas pastas públicas para o Office 365 grupos](migrate-your-public-folders-to-office-365-groups-exchange-2013-help.md) para obter uma visão geral das diferenças entre pastas públicas e grupos e motivos pelos quais a sua organização pode ou não pode se beneficiar de alternar para grupos.

Este artigo contém os procedimentos passo a passo para executar a migração de lote real de suas pastas públicas do Exchange 2013.

## O que você precisa saber antes de começar?

Certifique-se de que todas as seguintes condições forem atendidas antes de você começa a preparar a migração.

  - O servidor do Exchange 2013 precisa estar executando o **Exchange 2013 CU15** ou posterior.

  - No Exchange Online, você precisa ser membro do grupo de funções de gerenciamento da organização. Este grupo de função é diferente das permissões atribuídas a você quando você se inscreve para Office 365 ou Exchange Online. Para obter detalhes sobre como habilitar o grupo de funções de gerenciamento da organização, consulte [Gerenciar grupos de função](manage-role-groups-exchange-2013-help.md).

  - No Exchange 2013, você precisa ser membro dos grupos de função de gerenciamento da organização ou servidor de gerenciamento de RBAC. Para obter detalhes, consulte [Adicionar membros a um grupo de funções](https://go.microsoft.com/fwlink/?linkid=299212).

  - Antes de migrar suas pastas públicas para o Office 365 grupos, recomendamos que você primeiro mover caixas de correio do usuário para Office365 para os usuários que precisam de acesso aos grupos do Office 365 após a migração. Para obter mais informações, consulte [maneiras para migrar várias contas de email para o Office 365](https://support.office.com/article/ways-to-migrate-multiple-email-accounts-to-office-365-0a4913fe-60fb-498f-9155-a86516418842).

  - Proxy MRS precisa ser ativado em pelo menos um servidor do Exchange, e nesse servidor também deve hospedar caixas de correio de pasta pública. Consulte [Habilitar o ponto de extremidade do Proxy MRS para movimentações remotas](enable-the-mrs-proxy-endpoint-for-remote-moves-exchange-2013-help.md) para obter detalhes.

  - É possível usar o Centro de administração do Exchange (EAC) ou o Console de gerenciamento do Exchange (EMC) para executar este procedimento. Nos servidores do Exchange 2013, você precisará usar o Shell de gerenciamento do Exchange. Para o Exchange Online, você precisará usar o PowerShell do Exchange Online. Para obter mais informações, consulte [Connect to Exchange Online usando o PowerShell remoto](https://technet.microsoft.com/library/jj984289\(v=exchg.150\).aspx).

  - Apenas pastas públicas de email e calendário de tipo podem ser migradas para Office 365 grupos neste momento. Não há suporte para a migração de outros tipos de pastas públicas. Além disso, os grupos de destino no Office 365 devem ser criados antes da migração.

  - O processo de migração de lote copia somente mensagens e itens de calendário de pastas públicas para migração aos grupos do Office 365. Ele não copia outras entidades de pastas públicas, como diretivas, regras e permissões, desde que aqueles não são suportados no Office 365 grupos.

  - O Office 365 grupos vem com uma caixa de correio de 50GB. Certifique-se de que a soma dos dados de pasta pública que você está migrando totais menor que 50GB. Além disso, o espaço de armazenamento para conteúdo adicional a ser adicionada pelos usuários no futuro, deixe pós-migração. É recomendável que o tamanho da migração de pastas públicas não maiores do que 25GB no total.

  - Isso não é uma migração "tudo ou nada". Você pode escolher as pastas públicas específicas para migrar e apenas as pastas públicas serão migradas. Se a pasta pública está sendo migrada tiver subpastas, as subpastas não serão automaticamente incluídas na migração. Se você precisar migrá-los, você precisará explicitamente incluí-las.

  - As pastas públicas não serão afetadas de qualquer maneira por essa migração. No entanto, uma vez use nosso script bloqueados para tornar as pastas públicas migradas somente leitura, que os usuários serão forçados a usar o Office 365 grupos em vez de pastas públicas.

  - Antes de começar, recomendamos que você leia este artigo mudada, conforme o tempo de inatividade é necessário para algumas etapas.

## Etapa 1: Obter os scripts

A migração de lote para o Office 365 grupos requer a execução de um número de scripts em diferentes pontos a migração, conforme descrito a seguir neste artigo. Baixar os scripts e seus recursos de suporte arquivos [deste local](https://www.microsoft.com/en-us/download/details.aspx?id=55985). Depois de todos os scripts e arquivos baixados, salvá-los no mesmo local, como `c:\PFtoGroups\Scripts`.

Antes de prosseguir, verifique se ter baixado e salvo todos os scripts e arquivos a seguir:


> [!TIP]
> Certifique-se de salvar todos os scripts e arquivos no mesmo local.



  - **AddMembersToGroups.ps1**. esse script adiciona membros e proprietários para o Office 365 grupos baseiam nas entradas de permissão nas pastas públicas fonte.

  - **AddMembersToGroups.strings.psd1**. esse arquivo de suporte é usado pelo script `AddMembersToGroups.ps1`.

  - **LockAndSavePublicFolderProperties.ps1**. esse script torna as pastas públicas somente leitura para impedir que quaisquer modificações e transfere as propriedades de pasta pública relacionados a email (desde que as pastas públicas são habilitados para email) para os grupos de destino, que roteará novamente emails das pastas públicas aos grupos de destino. Esse script também faz backup as entradas de permissão e as propriedades de email antes de modificá-los.

  - **LockAndSavePublicFolderProperties.strings.psd1:**  este arquivo de suporte é usado pelo script `LockAndSavePublicFolderProperties.ps1`.

  - **UnlockAndRestorePublicFolderProperties.ps1**. esse script restaura os direitos de acesso e as propriedades de email das pastas públicas usando arquivos de backup criados por `LockandSavePublicFolderProperties.ps1`.

  - **UnlockAndRestorePublicFolderProperties.strings.psd1**. esse arquivo de suporte é usado pelo script `UnlockAndRestorePublicFolderProperties.ps1`.

  - **WriteLog.ps1**. esse script permite que os três scripts gravar logs.

  - **RetryScriptBlock.ps1**. esse script permite que os scripts `AddMembersToGroups`, `LockAndSavePublicFolderProperties`e `UnlockAndRestorePublicFolderProperties` repetir determinadas ações em caso de erros transitórios.

Para obter detalhes sobre `AddMembersToGroups.ps1`, `LockAndSavePublicFolderProperties.ps1`e `UnlockAndRestorePublicFolderProperties.ps1`e as tarefas a que serem executados em seu ambiente, consulte scripts de migração neste artigo.

## Etapa 2: Preparar-se para a migração

As etapas a seguir são necessárias para preparar sua organização para a migração:

1.  Compile uma lista de pastas públicas (tipos de email e calendário) que você deseja migrar para o Office 365 grupos.

2.  Ter uma lista de grupos de destino correspondente para cada pasta pública está sendo migrado. Você pode criar um novo grupo no Office 365 para cada pasta pública ou usar um grupo existente. Se você estiver criando um novo grupo, consulte [Saiba mais sobre o Office 365 grupos](https://go.microsoft.com/fwlink/p/?linkid=858521) para entender as configurações de que um grupo deve ter. Se uma pasta pública que você está migrando tem a permissão de padrão definido como **autor** ou acima, você deve criar o grupo correspondente no Office 365 com a configuração de privacidade **pública**. No entanto, os usuários vejam o grupo público sob o nó de **grupos** no Outlook, eles ainda terão que ingressar no grupo.

3.  Renomeie quaisquer pastas públicas que contêm uma barra invertida (**\\** ) em seu nome. Caso contrário, as pastas públicas podem serão migradas corretamente.

4.  Você precisa ter o recurso de migração **PAW** habilitados para o locatário do Office 365. Para verificar isso, execute o seguinte comando no PowerShell do Exchange Online:
    
        Get-MigrationConfig
    
    Se a saída em **recursos** lista **PAW**, então, o recurso está habilitado e você pode continuar a *etapa 3: criar o arquivo. csv*.
    
    Se PATA ainda não foi habilitado para seu locatário, poderia ser porque você precisou alguns lotes de migração existentes, lotes lotes de pasta pública ou de usuário. Esses lotes poderia ser qualquer estado, incluindo concluído. Se este for o caso, preencha e remover qualquer lotes de migração existentes até que os registros não forem retornados quando você executar `Get-MigrationBatch`. Depois que todos os lotes existentes são removidos, PATA deve obter habilitada automaticamente. Observe que a alteração pode não refletir no `Get-MigrationConfig` imediatamente, que é okey. Depois que essa etapa for concluída, você pode continuar a criação de novos lotes de migração de usuário.

## Etapa 3: Criar o arquivo. csv

Crie um arquivo. csv que fornecerá a entrada para um dos scripts de migração.

O arquivo. csv precisa conter as seguintes colunas:

  - **FolderPath**. Caminho da pasta pública a ser migrado.

  - **TargetGroupMailbox**. Endereço SMTP do grupo de destino no Office 365. Você pode executar o seguinte comando para ver o endereço SMTP principal.
    
        Get-UnifiedGroup <alias of the group> | Format-Table PrimarySmtpAddress

Um CSV de exemplo:

    "FolderPath","TargetGroupMailbox"
    "\Sales","sales@contoso.onmicrosoft.com"
    "\Sales\EMEA","emeasales@contoso.onmicrosoft.com"

Observe que uma pasta de email e uma pasta de calendário podem ser mescladas em um único grupo no Office 365. No entanto, qualquer outro cenário de várias pastas públicas mesclando em um grupo não é suportado dentro de um lote de migração único. Se você precisar mapear várias pastas públicas no mesmo grupo do Office 365, você pode fazer isso executando lotes de migração diferentes, o que devem ser executadas consecutivamente, um após o outro. Você pode ter até 500 entradas em cada lote de migração.

Uma pasta pública deve ser migrada para apenas um grupo no lote de migração de um.

## Etapa 4: Iniciar a solicitação de migração

Nesta etapa, você colete informações do seu ambiente do Exchange e, em seguida, usar essas informações no PowerShell do Exchange Online para criar um lote de migração. Depois disso, você deve iniciar a migração.

1.  No servidor Exchange 2013, localize o proxy MRS servidor de ponto de extremidade e anote-lo. Você precisará dessas informações posteriormente quando você executa a solicitação de migração.

2.  No PowerShell do Exchange Online, use as informações retornadas acima na etapa 1 para executar os seguintes comandos. As variáveis nesses comandos serão os valores da etapa 1.
    
    1.  Passe a credencial de um usuário com permissões de administrador no ambiente do Exchange 2013 para a variável `$Source_Credential`. Quando você eventualmente executa a solicitação de migração no Exchange Online, você usará essa credencial para obter acesso a seus servidores Exchange 2013 para copiar o conteúdo para o Exchange Online.
        
            $Source_Credential = Get-Credential
            <source_domain>\<PublicFolder_Administrator_Account>
    
    2.  Use as informações do servidor de proxy MRS do seu ambiente do Exchange 2013 que você anotou na etapa 1 acima e passe o valor para a variável `$Source_RemoteServer`.
        
            $Source_RemoteServer = "<MRS proxy endpoint>"

3.  No PowerShell do Exchange Online, execute o seguinte comando para criar um ponto de extremidade de migração:
    
        $PfEndpoint = New-MigrationEndpoint -PublicFolderToUnifiedGroup -Name PFToGroupEndpoint -RemoteServer $Source_RemoteServer -Credentials $Source_Credential

4.  Execute o seguinte comando para criar um novo lote de migração pública de pasta para o Office 365 de grupo. Neste comando:
    
      - **CSVData** é o arquivo. csv criado anteriormente no *etapa 3: criar o arquivo. csv*. Certifique-se de fornecer o caminho completo para esse arquivo. Se o arquivo foi movido por qualquer motivo, certifique-se de verificar e usar o novo local.
    
      - **NotificationEmails** é um parâmetro opcional que pode ser usado para definir os endereços de email que receberão notificações sobre o status e o progresso da migração.
    
      - **AutoStart** é um parâmetro opcional que, quando usado, inicia o lote de migração assim que ele é criado.
    
      - **PublicFolderToUnifiedGroup** é o parâmetro para indicar que se trata de uma pasta pública para o lote de migração do Office 365 grupos.
    
    <!-- end list -->
    
        New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

5.  Inicie a migração, executando o seguinte comando no PowerShell do Exchange Online. Observe que essa etapa é necessária somente se o parâmetro `-AutoStart` não foi usado durante a criação do lote acima na etapa 4.
    
        Start-MigrationBatch PublicFolderToGroupMigration

Enquanto as migrações de lote precisam ser criadas usando o cmdlet `New-MigrationBatch` em PowerShell do Exchange Online, o progresso da migração pode ser exibido e gerenciado no Centro de administração do Exchange. Você também pode exibir o progresso da migração, executando os cmdlets [Get-MigrationBatch](https://technet.microsoft.com/pt-br/library/jj219164\(v=exchg.150\)) e [Get-MigrationUser](https://technet.microsoft.com/pt-br/library/jj218702\(v=exchg.150\)) . O cmdlet `New-MigrationBatch` inicia um usuário de migração para cada caixa de correio de grupo do Office 365 e você pode exibir o status dessas solicitações usando a página de migração de caixa de correio.

Para exibir a página de migração de caixa de correio:

1.  No Exchange Online, abra Centro de administração do Exchange.

2.  Navegue até **destinatários** e selecione **migração**.

3.  Selecione a solicitação de migração que acabou de criar e, no painel de **detalhes**, selecione **Exibir detalhes**.

Quando o status do lote for **concluído**, você pode mover o logon em *etapa 5: adicionar membros a grupos do Office 365 das pastas públicas do*.

## Etapa 5: Adicionar membros a grupos do Office 365 de pastas públicas

Você pode adicionar membros ao grupo de destino no Office 365 manualmente, conforme necessário. No entanto, se você deseja adicionar membros ao grupo baseado nas entradas de permissão em pastas públicas, você precisará fazer isso executando o script `AddMembersToGroups.ps1` no servidor Exchange 2013, como mostra o seguinte comando. Caixas de correio do usuário devem ser sincronizadas para o Exchange Online para ser adicionado como membros de um grupo do Office 365. Para saber quais permissões de pastas públicas são candidatos a ser adicionado como membros de um grupo no Office 365, consulte scripts de migração mais adiante neste artigo.

O seguinte comando:

  - **MappingCsv** é o arquivo. csv criado anteriormente no *etapa 3: criar o arquivo. csv*. Certifique-se de fornecer o caminho completo para esse arquivo. Se o arquivo foi movido por qualquer motivo, certifique-se de verificar e usar o novo local.

  - **BackupDir** é o diretório onde os arquivos de log de migração serão armazenados.

  - **ArePublicFoldersOnPremises** é um parâmetro para indicar se as pastas públicas estão localizados no local ou no Exchange Online.

  - **Credencial** é o Exchange Online nome de usuário e senha.

<!-- end list -->

    .\AddMembersToGroups.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

Depois que os usuários tiverem sido adicionados a um grupo no Office 365, eles poderão começar a usá-lo.

## Etapa 6: Bloquear o público pastas (tempo de inatividade pasta pública necessário)

Quando a maioria dos dados em suas pastas públicas tenha migrado para o Office 365 grupos, você pode executar o script `LockAndSavePublicFolderProperties.ps1` no servidor Exchange 2013 para tornar as pastas públicas somente leitura. Essa etapa garante que nenhum dado novo é adicionado às pastas públicas antes que a migração for concluída.


> [!TIP]
> Se houver pastas públicas habilitadas para email (MEPFs) entre o público pastas sendo migradas, esta etapa copiará algumas propriedades de MEPFs, como endereços SMTP e ao grupo correspondente no Office 365 e, em seguida, a pasta pública de email-disable. Porque o MEPFs migrando vai ser desabilitada para email após a execução desse script, iniciará vendo emails enviados a MEPFs em vez disso, que está sendo recebidos nos grupos correspondentes. Para obter mais detalhes, consulte scripts de migração mais adiante neste artigo.



O seguinte comando:

  - **MappingCsv** é o arquivo. csv criado anteriormente no *etapa 3: criar o arquivo. csv*. Certifique-se de fornecer o caminho completo para esse arquivo. Se o arquivo foi movido por qualquer motivo, certifique-se de verificar e usar o novo local.

  - **BackupDir** é o diretório onde os arquivos de backup para entradas de permissão, propriedades MEPF e arquivos de log de migração serão armazenados. Este backup serão úteis caso seja necessário reverter para pastas públicas.

  - **ArePublicFoldersOnPremises** é um parâmetro para indicar se as pastas públicas estão localizados no local ou no Exchange Online.

  - **Credencial** é o Exchange Online nome de usuário e senha.

<!-- end list -->

    .\LockAndSavePublicFolderProperties.ps1 -MappingCsv <path to .csv file> -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

## Etapa 7: Finalizar a pasta pública à migração de grupos do Office 365

Depois de fazer suas pastas públicas somente leitura, você precisará executar novamente a migração. Isso é necessário para uma cópia incremental final dos seus dados. Antes de executar novamente a migração, você terá que remover o lote existente, que pode ser feito executando o seguinte comando:

    Remove-MigrationBatch <name of migration batch>

Em seguida, crie um novo lote com o mesmo arquivo CSV, executando o seguinte comando. Neste comando:

  - **CsvData** é o arquivo. csv criado anteriormente no *etapa 3: criar o arquivo. csv*. Certifique-se de fornecer o caminho completo para esse arquivo. Se o arquivo foi movido por qualquer motivo, certifique-se de verificar e usar o novo local.

  - **NotificationEmails** é um parâmetro opcional que pode ser usado para definir os endereços de email que receberão notificações sobre o status e o progresso da migração.

  - **AutoStart** é um parâmetro opcional que, quando usado, inicia o lote de migração assim que ele é criado.

<!-- end list -->

    New-MigrationBatch -Name PublicFolderToGroupMigration -CSVData (Get-Content <path to .csv file> -Encoding Byte) -PublicFolderToUnifiedGroup -SourceEndpoint $PfEndpoint.Identity [-NotificationEmails <email addresses for migration notifications>] [-AutoStart]

Depois que o novo lote é criado, inicie a migração, executando o seguinte comando no PowerShell do Exchange Online. Observe que essa etapa será necessária somente se o parâmetro `-AutoStart` não foi usado no comando anterior.

    Start-MigrationBatch PublicFolderToGroupMigration

Depois de concluir esta etapa (o status do lote é **concluído** ), verifique se que todos os dados foi copiado para o Office 365 grupos. Nesse momento, desde que esteja satisfeito com a experiência de grupos, você pode começar a exclusão de pastas públicas migradas do seu ambiente do Exchange 2013.


> [!IMPORTANT]
> Embora haja procedimentos com suporte para Revertendo sua migração e retornando a pastas públicas, isso não é possível depois que as pastas públicas do código-fonte forem excluídas. Consulte como posso reverter a pastas públicas do Office 365 grupos? para obter mais informações.



## Problemas conhecidos

Os seguintes problemas conhecidos podem ocorrer durante um típico pastas públicas para migração de grupos do Office 365.

  - O script que o endereço de SMTP de transferências de pastas públicas habilitadas para email ao grupo do Office 365 apenas adiciona os endereços como e-mail secundário endereços no Exchange Online. Dessa forma, se você tiver o programa de instalação do Exchange Online Protection (EOP) ou o fluxo de email centralizado em seu ambiente, terá problemas de envio de email para a pós-migração de grupos (para os endereços de email secundário).

  - Se o arquivo de mapeamento. csv tiver uma entrada com o caminho da pasta pública inválido, o lote de migração é exibido como **concluído** sem lançar um erro e dados adicionais não são copiados.

## Scripts de migração

Para referência, esta seção fornece descrições detalhadas para três dos scripts de migração e as tarefas a que serem executados em seu ambiente do Exchange. Todos os scripts e arquivos de suporte podem ser [baixado a partir deste local](https://www.microsoft.com/en-us/download/details.aspx?id=55985).

## AddMembersToGroups.ps1

Esse script irá ler as permissões das pastas públicas estão sendo migradas e, em seguida, adicionar membros e proprietários para o Office 365 grupos da seguinte maneira:

  - Usuários com as seguintes funções de permissão serão adicionados como membros a um grupo no Office 365. **Funções de permissão:**  proprietário, PublishingEditor, Editor, PublishingAuthor, autor

  - Além disso, para os usuários acima, com o seguinte acesso mínimo direitos serão também adicionados como membros a um grupo no Office 365. **Direitos de acesso:**  ReadItems, CreateItems, FolderVisible, EditOwnedItems, DeleteOwnedItems

  - Usuários com acesso que à direita "proprietário" será adicionado como proprietários a um grupo e com outros direitos de acesso elegíveis será adicionado como membros.

  - Grupos de segurança não podem ser adicionados como membros a grupos no Office 365. Portanto, eles serão expandidos e, em seguida, os usuários individuais serão adicionados como membros ou proprietários aos grupos com base nos direitos de acesso do grupo de segurança.

  - Quando os usuários em grupos de segurança que tem direitos de acesso via uma pasta pública ter sozinhos permissões explícitas sobre na mesma pasta pública, permissões explícitas receberá preferência. Por exemplo, considere um caso em que um grupo de segurança chamado "SG1" tem membros User1 e User2. Entradas de permissão para a pasta pública "PF1" são:
    
    SG1: Autor no PF1
    
    O Usuário1: Proprietário em PF1
    
    Nesse caso, User1 será adicionado como um proprietário para o grupo no Office 365.

  - Quando a permissão de padrão de uma pasta pública está sendo migrada é 'Autor' ou superior, o script irá sugerir a definição de privacidade do grupo correspondente definindo como 'Public'.

Esse script pode ser executado mesmo após o bloqueio e para baixo de pastas públicas, com o parâmetro `ArePublicFoldersLocked` definido como` $true`. Neste cenário, o script lê as permissões no back up criado durante o bloqueio de arquivo.

## LockAndSavePublicFolderProperties.ps1

Esse script torna as pastas públicas estão sendo migradas somente leitura. Quando habilitado para email de pastas públicas são migradas, eles serão primeiro ser desabilitada para email e seus endereços SMTP serão adicionados aos respectivos grupos no Office 365. Em seguida, as entradas de permissão serão modificadas para torná-las somente leitura. Um backup das propriedades de email de pastas públicas habilitadas para email, bem como as entradas de permissão de todas as pastas públicas, será copiada, antes de executar qualquer modificação neles.

Se houver vários lotes de migração, um diretório de backup separado deve ser usado com cada arquivo. csv de mapeamento.

As seguintes propriedades de email serão armazenadas, juntamente com os respectivas pastas públicas habilitadas para email e grupos do Office 365:

  - PrimarySMTPAddress

  - EmailAddresses

  - ExternalEmailAddress

  - EmailAddressPolicyEnabled

  - GrantSendOnBehalfTo

  - Lista de objeto de confiança SendAs

As propriedades de email acima serão armazenadas em um arquivo. csv, que pode ser usado no rolo volta process (se você deseja retornar ao usar pastas públicas, consulte como posso reverter a pastas públicas do Office 365 grupos? para obter mais informações). Um instantâneo das propriedades dos habilitados para email pastas públicas também será armazenado em um arquivo chamado PfMailProperties.csv. Esse arquivo não é necessário para o processo de reversão, mas ainda pode ser usado para referência.

As seguintes propriedades de email serão migradas para o grupo de destino como parte do bloqueio de:

  - PrimarySMTPAddress

  - EmailAddresses

  - Lista de objeto de confiança SendAs

  - GrantSendOnBehalfTo

O script garante que o PrimarySMTPAddress e EmailAddresses de migrar pastas públicas habilitadas para email serão adicionados como endereços SMTP secundários dos grupos correspondentes no Office 365. Além disso, SendAs e SendOnBehalfTo permissões de usuários em pastas públicas habilitadas para email receberão permissão equivalente em grupos de destino correspondente.

**Direitos de acesso permitidos**

Para os usuários garantir que as pastas públicas são feitas somente leitura para todos os usuários poderão apenas os seguintes direitos de acesso. Eles são armazenados no **ListOfAccessRightsAllowed**.

  - ReadItems

  - CreateSubfolders

  - FolderContact

  - FolderVisible

As entradas de permissão serão modificadas da seguinte maneira:

1.  ###  
    
    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th>Antes de bloqueio</th>
    <th>Depois de bloqueio</th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Nenhum</p></td>
    <td><p>Nenhum</p></td>
    </tr>
    <tr class="even">
    <td><p>AvailabilityOnly</p></td>
    <td><p>AvailabilityOnly</p></td>
    </tr>
    <tr class="odd">
    <td><p>LimitedDetails</p></td>
    <td><p>LimitedDetails</p></td>
    </tr>
    <tr class="even">
    <td><p>Colaborador</p></td>
    <td><p>FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Revisor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>NonEditingAuthor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Aughor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>Editor</p></td>
    <td><p>ReadItems, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>PublishingAuthor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="even">
    <td><p>PublishingEditor</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderVisible</p></td>
    </tr>
    <tr class="odd">
    <td><p>Proprietário</p></td>
    <td><p>ReadItems, CreateSubfolders, FolderContact, FolderVisible</p></td>
    </tr>
    </tbody>
    </table>


2.  Direitos de acesso para os usuários sem permissões de leitura serão mantidos e eles continuarão a ser bloqueado para direitos de leitura.

3.  Para usuários com funções personalizadas, todos os direitos de acesso que não estão na **ListOfAccessRightsAllowed** serão removidos. Se os usuários não têm qualquer direitos de acesso da lista de permissões após a filtragem, direito de acesso dos usuários, esses será definido como 'Nenhum'.

Pode haver uma interrupção no envio de emails para pastas públicas habilitadas para email durante o tempo entre quando as pastas são desabilitada para email e seus endereços SMTP são adicionados aos grupos do Office 365.

## UnlockAndRestorePublicFolderProperties.ps1

Este script novamente atribuirá permissões para pastas públicas, com base no back up executado durante a pasta pública bloqueio de arquivo. Esse script será também ativar o email de pastas públicas que tinham sido desabilitada para email, após ele remove endereços de SMTP das pastas seus respectivos grupos no Office 365. Pode haver ligeiramente tempo de inatividade durante esse processo.

## Como posso reverter a pastas públicas do Office 365 grupos?

Se você mudar de ideia e quiser retornar ao usar pastas públicas após usar os grupos do Office 365, o comando listado abaixo restaurará seu ambiente para o estado era pré-migração. Um rolo volta pode ser executado enquanto os arquivos de backup existirem e desde que você não excluiu a pós-migração de pastas públicas.

No seu servidor Exchange 2013, execute o seguinte comando. Neste comando:

  - **BackupDir** é o diretório onde os arquivos de backup para entradas de permissão, propriedades MEPF e arquivos de log de migração serão armazenados. Verifique se você usa o mesmo local em que você especificou na *etapa 6: bloquear as pastas públicas para substituição (tempo de inatividade pasta pública necessário)*.

  - **ArePublicFoldersOnPremises** é um parâmetro para indicar se as pastas públicas estão localizados no local ou no Exchange Online.

  - **Credencial** é o Exchange Online nome de usuário e senha.

<!-- end list -->

    .\UnlockAndRestorePublicFolderProperties.ps1 -BackupDir <path to backup directory> -ArePublicFoldersOnPremises $true -Credential (Get-Credential)

Lembre-se de que todos os itens adicionados ao grupo do Office 365 ou qualquer operação Editar executadas nos grupos, não são copiados para suas pastas públicas. Portanto, haverá perda de dados, supondo que novos dados foi adicionado enquanto a pasta pública foi um grupo.

Observe também que não é possível restaurar um subconjunto de pastas públicas, o que significa que todas as pastas públicas lá foram migradas deve ser restauradas.

Os grupos correspondentes no Office 365 não serão excluídos como parte do processo de volta rolo. Você terá que limpar ou excluir esses grupos manualmente.

