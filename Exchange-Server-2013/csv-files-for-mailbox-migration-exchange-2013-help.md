---
title: 'Arquivos CSV para migração de caixa de correio: Exchange 2013 Help'
TOCTitle: Arquivos CSV para migração de caixa de correio
ms:assetid: e67b3455-3946-4335-b80c-97823c76ac54
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn170437(v=EXCHG.150)
ms:contentKeyID: 54651953
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Arquivos CSV para migração de caixa de correio

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2017-11-16_

Você pode usar um arquivo CSV para em massa migrar um grande número de caixas de correio do usuário. Quando você usar o Centro de administração do Exchange (EAC) ou o cmdlet **New-MigrationBatch** no Shell de Gerenciamento do Exchange para criar um lote de migração, você pode especificar um arquivo CSV. Usando um CSV para especificar vários usuários para migrar um lote de migração tem suporte nos seguintes cenários de migração:

  - **Move em organizações do local Exchange**
    
      - **Movimentação local:**  Uma movimentação local é onde você move caixas de correio do banco de dados de uma caixa de correio para outro. Uma movimentação local ocorre em uma única floresta.
    
      - **Enterprise entre florestas mover:**  Em uma movimentação entre florestas enterprise, caixas de correio são movidas para uma floresta diferente. Movimentações entre florestas são iniciadas a partir da floresta de destino, que é a floresta que você deseja mover as caixas de correio, ou de floresta de origem, que é a floresta que atualmente hospeda as caixas de correio.

  - **Inclusão e exclusão no Exchange Online**
    
      - **Migração de movimentação remota de inclusão:**  Em uma implantação híbrida Exchange, você pode mover caixas de correio de uma organização local do Exchange para Exchange Online. Isso também é conhecido como uma migração de movimentação remota de *inclusão* porque você onboard caixas de correio para Exchange Online.
    
      - **Migração de movimentação remota de exclusão:**  Você também pode realizar uma migração de movimentação remota de *exclusão* , onde você migra caixas de correio de Exchange Online à sua organização de Exchange local.
        

        > [!TIP]
        > As migrações por movimentação com inclusão e exclusão remotas são iniciadas em sua organização do Exchange Online.

    
      - **Migração do Exchange testados:**  Você também pode migrar um subconjunto de caixas de correio de uma organização local do Exchange para Exchange Online. Isso é outro tipo de migração de inclusão. Você pode migrar apenas Exchange 2003 e Exchange 2007 caixas de correio usando uma migração em estágios Exchange. Migrando Exchange 2010 e Exchange 2013 caixas de correio não é suportado usando uma migração em estágios. Antes de executar uma migração em estágios, você precisa usar a sincronização de diretório ou algum outro método para provisionar usuários de email em sua organização de Exchange Online.
    
      - **Migração IMAP:**  Esse tipo de inclusão de migração migra dados de caixa de correio de um servidor IMAP (incluindo Exchange ) para Exchange Online. Para uma migração de IMAP, você deve provisionar caixas de correio em Exchange Online para que possa migrar dados de caixa de correio.


> [!TIP]
> Uma migração de substituição Exchange não oferece suporte a um usando um arquivo CSV porque todas as caixas de correio de usuário de local são migradas para o Exchange Online em um único lote.



## Atributos suportados para arquivos CSV para movimentações em massa ou migrações

A primeira linha ou a linha de cabeçalho de um arquivo CSV usada para listas de usuários migrando os nomes do atributos, ou dos campos, especificados nas linhas seguintes. Cada nome do atributo é separada por uma vírgula. Cada linha sob a linha de cabeçalho representa um usuário individual e fornece as informações exigidas para a migração. Os atributos em cada linha de usuário individual devem ser na mesma ordem em que os nomes de atributo na linha de cabeçalho. Cada valor do atributo é separada por uma vírgula. Se o valor do atributo de um registro específico for nulo, não digite nada para o atributo. No entanto, certifique-se de que você inclua a vírgula para separar o valor nulo do atributo do próximo.

Valores de atributo no arquivo CSV substituem o valor do parâmetro correspondente ao mesmo parâmetro é usado ao criar um lote de migração com o EAC ou o Shell de Gerenciamento do Exchange. Para obter mais informações e exemplos, consulte a seção valores de atributo no arquivo CSV substituem os valores para o lote de migração.


> [!TIP]
> Você pode usar qualquer editor de texto para criar o arquivo CSV, mas usar um aplicativo como o Microsoft Excel irá facilitar a importar dados, configurar e organizar arquivos CSV. Certifique-se de salvar arquivos CSV como um arquivo. csv ou. txt.



As seções a seguir descrevem os atributos com suporte para a linha de cabeçalho de um arquivo CSV para cada tipo de migração. Cada seção inclui uma tabela que lista cada atributo com suporte, se necessário, um exemplo de um valor a ser usado para o atributo e uma descrição.


> [!TIP]
> Nas seções a seguir, o <EM>ambiente de origem</EM> denota o local atual de uma caixa de correio do usuário ou de um banco de dados. <EM>Ambiente de destino</EM> indica o local que será migrada para a caixa de correio ou banco de dados que será movida para a caixa de correio.



## Movimentações locais

A tabela a seguir descreve os atributos com suporte para um arquivo CSV para movimentações locais. Para obter mais informações, consulte [Gerenciar movimentações de local](manage-on-premises-moves-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Obrigatório ou opcional</th>
<th>Valores aceitos</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obrigatório</p></td>
<td><p>Endereço de SMTP para o usuário</p></td>
<td><p>Especifica o usuário que será movido.</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>Opcional</p></td>
<td><p>Nome do banco de dados</p></td>
<td><p>Especifica o banco de dados de caixa de correio que será movida para a caixa de correio principal do usuário. Você pode especificar outro banco de dados nas linhas diferentes do arquivo CSV, que permite mover caixas de correio no lote de migração mesmo aos bancos de dados diferentes.</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>Opcional</p></td>
<td><p>Nome do banco de dados</p></td>
<td><p>Especifica o banco de dados de caixa de correio que será movido para o correio de arquivo morto do usuário (se houver). Você pode especificar outro banco de dados nas linhas diferentes do arquivo CSV, que permite mover caixas de correio de arquivo morto no lote de migração mesmo aos bancos de dados diferentes.</p>

> [!TIP]
> Se você não especificar o banco de dados de arquivamento, a caixa de correio de arquivo morto é movida para o mesmo banco de dados da caixa de correio principal.


</td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Opcional</p></td>
<td><p><code>Unlimited</code> ou um inteiro não negativo de <code>0</code> (padrão) para um valor máximo de <code>2147483647</code></p></td>
<td><p>Especifica o número de itens defeituosos pular se o serviço de migração encontra um item corrompido na caixa de correio. Se você incluir este atributo no arquivo CSV, ele substituirá o valor padrão ou um valor que você especificar se você incluir o parâmetro <em>BadItemLimit</em> ao criar o lote de migração usando o EAC ou o Shell de Gerenciamento do Exchange.</p>

> [!TIP]
> Recomendamos que você use o valor padrão 0 e apenas aumentar o limite de item inválido para um usuário específico se a movimentação ou a migração para o usuário falhar.


<p></p></td>
</tr>
<tr class="odd">
<td><p>MailboxType</p></td>
<td><p>Opcional</p></td>
<td><p>Use um dos seguintes valores:</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (o valor padrão)</p></li>
</ul></td>
<td><p>Especifica se é mover a caixa de correio principal do usuário, caixa de correio de arquivo morto ou ambos.</p></td>
</tr>
</tbody>
</table>


## Migrações de movimentação remota de inclusão em uma implantação híbrida

Em uma implantação híbrida, você pode mover caixas de correio de uma organização local do Exchange para Exchange Online. Quando a inclusão de caixas de correio, o lote de migração é criado na organização Exchange Online e iniciada por um administrador de Exchange Online. Para obter mais informações, consulte [Movimentação de caixas de correio entre organizações locais e do Exchange Online em implantações híbridas](https://technet.microsoft.com/pt-br/library/jj906432\(v=exchg.150\)).

A tabela a seguir descreve os atributos com suporte para um arquivo CSV para migrações de movimentação remota de inclusão.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Obrigatório ou opcional</th>
<th>Valores aceitos</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obrigatório</p></td>
<td><p>Endereço de SMTP para o usuário</p></td>
<td><p>Especifica o endereço de email para o usuário habilitado para email na organização Exchange Online correspondente na caixa de correio de usuário local que serão migradas.</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Opcional</p></td>
<td><p><code>Unlimited</code> ou um inteiro não negativo de <code>0</code> (padrão) para um valor máximo de <code>2147483647</code></p></td>
<td><p>Especifica o número de itens defeituosos pular se o serviço de migração encontra um item corrompido na caixa de correio. Se você incluir este atributo no arquivo CSV, ele substituirá o valor padrão ou o valor que você especificar se você incluir o parâmetro <em>BadItemLimit</em> ao criar o lote de migração usando o EAC ou o Shell de Gerenciamento do Exchange.</p>

> [!TIP]
> Recomendamos que você use o valor padrão 0 e apenas aumentar o limite de item inválido para um usuário específico se a movimentação ou a migração para o usuário falhar.


</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>Opcional</p></td>
<td><p><code>Unlimited</code> ou um inteiro não negativo de <code>0</code> (padrão) para um valor máximo.</p></td>
<td><p>Especifica o número de itens grandes na caixa de correio do usuário que será ignorada. Quando o número de itens grandes excede esse valor, a migração da caixa de correio falhará.</p>
<p>O valor padrão é 0, o que significa que a migração falhará se a caixa de correio contiver quaisquer itens grandes.</p>
<p>Quando os itens de inclusão de caixas de correio para Exchange Online, até 35 MB são migrados.</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>Opcional</p></td>
<td><p>Use um dos seguintes valores:</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (o valor padrão)</p></li>
</ul></td>
<td><p>Especifica se é mover a caixa de correio principal do usuário, caixa de correio de arquivo morto ou ambos.</p></td>
</tr>
</tbody>
</table>


## Move enterprise entre florestas e exclusão remota mover migrações em uma implantação híbrida

Conforme indicadas anteriormente, entre florestas movimentações são iniciadas a partir da floresta de destino ou de floresta de origem. Migrações de movimentação remota de exclusão são iniciadas a partir de sua organização Exchange Online. Para obter mais informações, consulte:

  - [Preparar a caixas de correio para solicitações de movimentação entre florestas](prepare-mailboxes-for-cross-forest-move-requests-exchange-2013-help.md)

  - [Movimentação de caixas de correio entre organizações locais e do Exchange Online em implantações híbridas](https://technet.microsoft.com/pt-br/library/jj906432\(v=exchg.150\))

A tabela a seguir descreve os atributos com suporte para um arquivo CSV para entre florestas corporativos movimentações e migrações de movimentação remota de exclusão em uma implantação híbrida do Exchange.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Obrigatório ou opcional</th>
<th>Valores aceitos</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obrigatório</p></td>
<td><p>Endereço de SMTP para o usuário</p></td>
<td><p>Para movimentações entre florestas enterprise, especifica a caixa de correio ou usuário habilitado para email na floresta de origem.</p>
<p>Para migrações de movimentação remota de exclusão, ele especifica a caixa de correio Exchange Online.</p></td>
</tr>
<tr class="even">
<td><p>TargetDatabase</p></td>
<td><p>Necessário para migrações de movimentação remota de exclusão e para movimentações entre florestas enterprise que são iniciadas a partir da floresta de origem. Como alternativa, este atributo pode ser especificado ao criar o lote de migração no EAC ou usando o Shell de Gerenciamento do Exchange.</p>
<p>Este atributo é opcional para movimentações entre florestas enterprise que são iniciadas a partir da floresta de destino.</p></td>
<td><p>Nome do banco de dados</p></td>
<td><p>Especifica o banco de dados de caixa de correio na floresta de destino que será movida para a caixa de correio principal do usuário. Você pode especificar outro banco de dados nas linhas diferentes do arquivo CSV, que permite mover caixas de correio no lote de migração mesmo aos bancos de dados diferentes.</p></td>
</tr>
<tr class="odd">
<td><p>TargetArchiveDatabase</p></td>
<td><p>Opcional</p></td>
<td><p>Nome do banco de dados</p></td>
<td><p>Especifica o banco de dados de caixa de correio na floresta de destino que será movido para o correio de arquivo morto do usuário. Você pode especificar outro banco de dados nas linhas diferentes do arquivo CSV, que permite mover caixas de correio de arquivo morto no lote de migração mesmo aos bancos de dados diferentes.</p></td>
</tr>
<tr class="even">
<td><p>BadItemLimit</p></td>
<td><p>Opcional</p></td>
<td><p><code>Unlimited</code> ou um inteiro não negativo de <code>0</code> (padrão) para um valor máximo de <code>2147483647</code></p></td>
<td><p>Especifica o número de itens defeituosos pular se o serviço de migração encontra um item corrompido na caixa de correio. Se você incluir este atributo no arquivo CSV, ele substituirá o valor padrão ou o valor que você especificar se você incluir o parâmetro <em>BadItemLimit</em> ao criar o lote de migração usando o EAC ou o Shell de Gerenciamento do Exchange.</p>

> [!TIP]
> Recomendamos que você use o valor padrão 0 e apenas aumentar o limite de item inválido para um usuário específico se a movimentação ou a migração para o usuário falhar.


</td>
</tr>
<tr class="odd">
<td><p>LargeItemLimit</p></td>
<td><p>Opcional</p></td>
<td><p><code>Unlimited</code> ou um inteiro não negativo de <code>0</code> (padrão) para um valor máximo.</p></td>
<td><p>Especifica o número de itens grandes na caixa de correio do usuário que será ignorada. Quando o número de itens grandes excede esse valor, a migração da caixa de correio falhará.</p>
<p>O valor padrão é 0, o que significa que a migração falhará se a caixa de correio contiver quaisquer itens grandes.</p>
<p>Quando os itens de inclusão de caixas de correio para Exchange Online, até 35 MB são migrados.</p></td>
</tr>
<tr class="even">
<td><p>MailboxType</p></td>
<td><p>Opcional</p></td>
<td><p>Use um dos seguintes valores:</p>
<ul>
<li><p><code>PrimaryOnly</code></p></li>
<li><p><code>ArchiveOnly</code></p></li>
<li><p><code>PrimaryAndArchive</code> (o valor padrão)</p></li>
</ul></td>
<td><p>Especifica se é mover a caixa de correio principal do usuário, caixa de correio de arquivo morto ou ambos.</p></td>
</tr>
</tbody>
</table>


## Migrações em estágios do Exchange

Você precisa usar um arquivo CSV para identificar o grupo de usuários para um lote de migração, quando você deseja usar uma migração em estágios do Exchange para migrar do Exchange 2003 e Exchange 2007 caixas de correio para Exchange Online local. Não há um limite para o número de caixas de correio que você pode migrar para a nuvem usando uma migração em estágios do Exchange. No entanto, o arquivo CSV para um lote de migração pode conter um máximo de 1.000 linhas. Para migrar mais de 1.000 caixas de correio, você precisa criar arquivos adicionais de CSV e, em seguida, usar cada uma para criar um novo lote de migração. Para obter mais informações sobre migrações em estágios do Exchange, consulte [Migrar caixas de correio para o Exchange Online com uma migração em estágios](https://technet.microsoft.com/pt-br/library/jj874018\(v=exchg.150\)).

A tabela a seguir descreve os atributos com suporte para um arquivo CSV para uma migração em estágios do Exchange.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Obrigatório ou opcional</th>
<th>Valores aceitos</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obrigatório</p></td>
<td><p>Endereço de SMTP para o usuário</p></td>
<td><p>Especifica o endereço de email para o usuário habilitado para email (ou uma caixa de correio se você estiver tentando novamente a migração) em Exchange Online correspondente na caixa de correio de usuário local que serão migradas. Usuários habilitados para email são criados no Exchange Online como resultado de sincronização de diretório ou outro processo de provisionamento. O endereço de email do usuário habilitado para email deve corresponder à propriedade de <em>WindowsEmailAddress</em> para a caixa de correio correspondente do local.</p></td>
</tr>
<tr class="even">
<td><p>Senha</p></td>
<td><p>Opcional</p></td>
<td><p>Uma senha deve ter um comprimento mínimo de oito caracteres e satisfazer qualquer restrições de senha que são aplicadas à sua organização Office 365.</p></td>
<td><p>Essa senha é definida na conta de usuário, quando o usuário habilitado para email correspondente no Exchange Online é convertido em uma caixa de correio durante a migração.</p></td>
</tr>
<tr class="odd">
<td><p>ForceChangePassword</p></td>
<td><p>Opcional</p></td>
<td><p><code>True</code> ou <code>False</code></p></td>
<td><p>Especifica se um usuário deve alterar a senha na primeira vez que entrarem suas caixas de correio Exchange Online.</p>

> [!TIP]
> Se você implementou uma solução de logon único com a implantação do Active Directory Federation Services 2.0 (AD FS 2.0) em sua organização local, você deve usar <CODE>False</CODE> para o valor desse atributo.


</td>
</tr>
</tbody>
</table>


## Migrações IMAP

Um arquivo CSV para um lote de migração de IMAP pode ter um máximo de 50.000 linhas. Mas é uma boa ideia para migrar usuários em vários lotes menores. Para obter mais informações sobre migrações de IMAP, consulte os tópicos a seguir:

  - [Migrar email de um servidor IMAP para caixas de correio do Exchange Online](https://technet.microsoft.com/pt-br/library/jj874015\(v=exchg.150\))

  - [Arquivos CSV para lotes de migração de IMAP](https://technet.microsoft.com/pt-br/library/jj200730\(v=exchg.150\))

A tabela a seguir descreve os atributos com suporte para um arquivo CSV para uma migração IMAP.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Atributo</th>
<th>Obrigatório ou opcional</th>
<th>Valores aceitos</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>EmailAddress</p></td>
<td><p>Obrigatório</p></td>
<td><p>Endereço de SMTP para o usuário.</p></td>
<td><p>Especifica a ID de usuário de caixa de correio do usuário Exchange Online</p></td>
</tr>
<tr class="even">
<td><p>UserName</p></td>
<td><p>Obrigatório</p></td>
<td><p>Cadeia de caracteres que identifica o usuário no sistema, em um formato suportado pelo servidor IMAP de mensagens IMAP.</p></td>
<td><p>Especifica o nome de logon para a conta do usuário no sistema de mensagens IMAP (ambiente de origem). Além do nome de usuário, você pode usar as credenciais de uma conta que tenha sido atribuída as permissões necessárias para acessar caixas de correio no servidor IMAP. Para obter mais informações, consulte <a href="https://technet.microsoft.com/pt-br/library/jj200730(v=exchg.150)">Arquivos CSV para lotes de migração de IMAP</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Senha</p></td>
<td><p>Obrigatório</p></td>
<td><p>Cadeia de caracteres de senha.</p></td>
<td><p>Especifica a senha da conta de usuário especificada pelo atributo UserName.</p></td>
</tr>
</tbody>
</table>


## Os valores de atributo no arquivo CSV substituir os valores para o lote de migração

Valores de atributo no arquivo CSV substituem o valor do parâmetro correspondente ao mesmo parâmetro é usado ao criar um lote de migração com o EAC ou o Shell de Gerenciamento do Exchange. Se desejar que o valor de lote de migração a ser aplicado a um usuário, você faria deixar aquela célula em branco no arquivo CSV. Isso permite misturar e combinar certos valores de atributo para usuários selecionados em um lote de migração.

Por exemplo, vamos dizer que você cria um lote no Shell de Gerenciamento do Exchange para principal dos usuários de mover para mover uma empresa entre florestas e caixas de correio de arquivo morto para a floresta de destino com o seguinte comando Shell de Gerenciamento do Exchange.

    New-MigrationBatch -Name CrossForestBatch1 -SourceEndpoint ForestEndpoint1 -TargetDeliveryDomain forest2.contoso.com -TargetDatabases @(EXCH-MBX-02,EXCH-MBX-03) -TargetArchiveDatabases @(EXCH-MBX-A02,EXCH-MBX-A03) -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\CrossForestBatch1.csv")) -AutoStart


> [!TIP]
> Como o padrão é para mover principal e arquivar caixas de correio, você não precisa explicitamente especificá-lo no comando Shell de Gerenciamento do Exchange.



Uma parte do arquivo CrossForestBatch1.csv para este lote de migração tem esta aparência:

    EmailAddress,TargetDatabase,TargetArchiveDatabase
    user1@contoso.com,EXCH-MBX-01,EXCH-MBX-A01
    user2@contoso.com,,
    user3@contoso.com,EXCH-MBX-01,
    ...

Como os valores no arquivo CSV substituem os valores para o lote de migração, o principal e caixas de correio de arquivo morto de user1 são movidas para EXCH-MBX-01 e EXCH-MBX-A01, respectivamente, na floresta de destino. O principal e caixas de correio de arquivo morto para Usuário2 são movidas para EXCH-MBX-02 ou EXCH-MBX-03. Caixa de correio primária para user3 é movida EXCH-MBX-01 e a caixa de correio de arquivo morto é movida para EXCH-MBX-A02 ou EXCH-MBX-A03.

Em outro exemplo, vamos supor que você cria um lote para uma migração de movimentação remota de inclusão em uma implantação híbrida para mover caixas de correio de arquivo morto para Exchange Online com o seguinte comando.

    New-MigrationBatch -Name OnBoarding1 -SourceEndpoint RemoteEndpoint1 -TargetDeliveryDomain cloud.contoso.com -CSVData ([System.IO.File]::ReadAllBytes("C:\Users\Administrator\Desktop\OnBoarding1.csv")) -MailboxType ArchiveOnly -AutoStart

Mas você também deseja mover as caixas de correio primárias para usuários selecionados, portanto uma parte do arquivo OnBoarding1.csv para este lote de migração se pareceria com este:

    EmailAddress,MailboxType
    user1@contoso.com,
    user2@contoso.com,
    user3@cloud.contoso.com,PrimaryAndArchive
    user4@cloud.contoso.com,PrimaryAndArchive
    ...

Porque o valor de tipo de caixa de correio no arquivo CSV substitui os valores para o parâmetro *MailboxType* no comando para criar o lote, somente a caixa de correio de arquivo morto para user1 e user2 é migrada para Exchange Online. Mas o principal e caixas de correio de arquivo morto para user3 e user4 são movidas para Exchange Online.

