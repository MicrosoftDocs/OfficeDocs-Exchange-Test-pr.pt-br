---
title: 'Usar o Script RollAlternateserviceAccountCredential.ps1 no Shell'
TOCTitle: Usando o Script de RollAlternateserviceAccountCredential.ps1 no Shell
ms:assetid: 6ac55aae-472a-4ed6-83df-2d0e7b48e05c
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff808311(v=EXCHG.150)
ms:contentKeyID: 63965576
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Usando o Script de RollAlternateserviceAccountCredential.ps1 no Shell

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Você pode usar o script RollAlternateServiceAccountPassword.ps1 Exchange Server 2013 fto atualização uma credencial de conta de serviço alternativa (credencial ASA) e distribuir a atualização para os servidores de acesso para cliente especificados.


> [!TIP]  
> Exchange Shell de gerenciamento não carrega automaticamente scripts. Você precisa preceder todos os scripts com "./\" por exemplo, para executar o script RollAlternateServiceAccountPassword.ps1, digite <code>.\RollAlternateServiceAccountPassword.ps1</code>.




> [!TIP]  
> Esse script é fornecido apenas em inglês.



Para obter mais informações sobre como usar e escrever scripts, consulte [Script com o Shell de Gerenciamento do Exchange](https://technet.microsoft.com/pt-br/library/bb123798\(v=exchg.150\)).

## Sintaxe

    RollAlternateServiceAccountPassword.ps1 -Scope <Object> -Identity <Object> -Source <Object> -

## Descrição detalhada

Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada de "Segurança de acesso do cliente" no tópico Client Access Permissions.

## Detalhes técnicos do Script de credencial de conta de serviço alternativa

Esse script facilita a instalação e manutenção da credencial ASA. Depois que você criou a credencial ASA e definir os nomes de princípio de serviço apropriado, você pode usar o script para distribuir as credenciais a serem todos os servidores de acesso para cliente de destino.

Para usar o script, você precisa identificar quais servidores que você deseja direcionar e quais credenciais que você deseja usar como sua credencial ASA.

## Escopo de servidor

Você pode optar por ter o script de todos os servidores de acesso para cliente na floresta de destino todos os membros de uma matriz de servidores de acesso para cliente específica ou servidores específicos. Os parâmetros disponíveis são *ToEntireForest*, *ToArraryMembers*e *ToSpecificServers*. Se você direcione o script para servidores específicos ou membros de uma matriz de servidores específicos, o parâmetro *Identity* precisa ser especificada com os servidores ou nomes de matriz de servidores, que você deseja direcionar.

## Origem da credencial

O script pode copiar a senha da conta de serviço alternativa de um servidor existente. Ou então, você pode especificar a conta que você deseja usar e deixar o script gerar uma nova senha para a conta. Os parâmetros disponíveis são *GenerateNewPasswordFor* e *CopyFrom*. O parâmetro *GenerateNewPasswordFor* requer que você especifique uma cadeia de caracteres de conta no seguinte formato: domínio \\ nome. Se você estiver usando uma conta de computador, você precisará acrescentar "$" ao final do nome da conta, por exemplo o CONTOSO\\ClientServerAcct$. O parâmetro *CopyFrom* utiliza o nome de um servidor de acesso para cliente existente como a fonte de credencial.

## Gerando uma nova senha para uma credencial

A senha é criada pelo script. Nenhuma entrada do usuário é necessária. O script tentará distribuir a senha para todos os computadores de destino e, então, tentar atualizar as credenciais de conta Active Directory com a senha recentemente gerado.

A senha recentemente gerado 73 caracteres de comprimento e atendem aos requisitos de senha forte standard. Se seus requisitos de senha forem diferentes, você precisará definir a senha manualmente e copie-o para os servidores de destino.

Para impedir a interrupção do serviço, o script examina cada servidor de acesso para cliente e mantém a senha atual, bem como a adição a nova senha. Depois que o script foi executado, a credencial ASA compartilhada poderão usar qualquer uma das 2 senhas: a senha atual como armazenado em Active Directory ou a nova senha que ainda não tiver sido definida no Active Directory.

Todas as senhas que não são mais válidas, como uma senha expirada, serão removidas dos servidores de destino. Se a senha na Active Directory não pode ser alterada, talvez porque a senha expirou, o script tentará uma redefinição de senha. Isso exigirá a conta que executa o script para ter permissões para redefinir senhas de contas de computador Active Directory ou senhas de contas de usuário, dependendo se a sua conta de serviço alternativa é uma conta de computador ou uma conta de usuário.

Se as senhas não são alteradas com sucesso para todos os servidores de acesso para cliente de destino, atualizar a senha Active Directory pode causar uma falha de autenticação. Se o script for executado no modo autônomo, ele não atualizar a senha de Active Directory com a nova senha, a menos que todos os servidores de acesso para cliente de destino foram atualizados com êxito. Se o script é executado no modo assistido, você será solicitado se você deseja atualizar a senha no Active Directory.

## Criar uma tarefa agendada para automatizar a manutenção de senha

Se desejar que o script para criar uma tarefa agendada para manter a senha constantemente, use o parâmetro *CreateScheduledTask* . Este parâmetro requer uma cadeia de caracteres para o nome da tarefa à qual que você deseja criar.


> [!TIP]  
> Execute o script e verificar se ela funciona corretamente no modo assistido antes de criar a tarefa agendada autônoma.



O script cria um arquivo. cmd na pasta onde o script está localizado. Em seguida, ele cria uma tarefa para executar esse arquivo. cmd a cada três semanas. Você pode usar Windows Agendador de tarefas para modificar a tarefa agendada, por exemplo, para definir sua execução mais ou menos freqüentemente. Por padrão, a tarefa será executado como o usuário conectado no momento. Além disso, o script só será executado quando o usuário está conectado ao computador. Recomendamos que você modifique a tarefa agendada seja executada se o usuário está conectado ou não. Você também pode optar por executá-lo em uma conta diferente, se essa conta tem permissões de Active Directory para redefinir senhas, bem como a função de administrador do Exchange Enterprise. Ao criar uma tarefa agendada, o script será executado automaticamente no modo autônomo.

## Tarefas fora do escopo do Script

O script não gerencia os SPNs da credencial ASA ou permite remover uma conta de serviço alternativa de um servidor. Para remover uma conta de serviço alternativa de um servidor, consulte a seção de [autenticação Kerberos ativar desativado](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md) no [Configurando a autenticação Kerberos para servidores de acesso para cliente com balanceamento de carga](configuring-kerberos-authentication-for-load-balanced-client-access-servers-exchange-2013-help.md).

## O Script de solução de problemas

Recomendamos que você execute o script e verificar se ela funciona corretamente no modo assistido antes de criar a tarefa agendada autônoma. Para obter informações de solução de problemas, consulte [O Script RollAlternateServiceAccountCredential.ps1 de solução de problemas](troubleshooting-the-rollalternateserviceaccountcredential-ps1-script-exchange-2013-help.md).

## Validando o script.

A saída do script quando você executá-lo interativamente com o sinalizador-verbose deve indicar quais operações de script foram bem-sucedidas. Para confirmar que os servidores de acesso para cliente foram atualizados, você pode verificar o último carimbo de hora modificado na credencial ASA. O exemplo a seguir gera uma lista de servidores de acesso para cliente e a última vez em que a conta de serviço alternativa for atualizada.

    Get-ClientAccessServer -IncludeAlternateServiceAccountCredentialstatus |Fl Name, AlternateServiceAccountConfiguration

Você também pode examinar o log de eventos no computador no qual o script é executado. As entradas de log de eventos para o script são no log de eventos do aplicativo e da fonte *MSExchange Management Application*. A tabela a seguir lista os eventos que são registrados e o que significam os eventos.

### IDs de evento de script e suas explicações

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Evento</th>
<th>Explicação</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>14001</p></td>
<td><p>Iniciar</p></td>
</tr>
<tr class="even">
<td><p>14002</p></td>
<td><p>Sucesso (informações)</p></td>
</tr>
<tr class="odd">
<td><p>14003</p></td>
<td><p>Mas bem-sucedida com avisos.</p>
<p>O script alguns problemas encontrados mas conseguiu superá-los ou confirmação de entrada do usuário não foram necessárias. Se o script está sendo executado no modo interativo, leia a saída do script para obter mais detalhes de aviso.</p></td>
</tr>
<tr class="even">
<td><p>14004</p></td>
<td><p>Com falha</p></td>
</tr>
</tbody>
</table>


Se o script é executado como uma tarefa agendada, seus resultados são registrados na pasta de **log** do servidor Exchange em uma subpasta chamada **RollAlternateServiceAccountPassword**.

Você pode usar o log para confirmar que a tarefa foi executada com êxito.

## Parâmetros


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Parâmetro</th>
<th>Obrigatório</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>ToEntireForest</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>ToEntireForest</em> refere-se o script para todos os servidores de acesso para cliente na floresta.</p></td>
</tr>
<tr class="even">
<td><p><em>ToArrayMembers</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>ToArrayMembers</em> refere-se o script para todos os membros de uma matriz de servidores de acesso para cliente específico.</p>

> [!TIP]  
> Se você estiver usando o parâmetro <EM>ToArrayMembers</EM> ou <EM>ToSpecificServers</EM> , você precisará especificar os nomes do servidor ou os nomes de matriz de servidores usando o parâmetro <EM>Identity</EM> .


</td>
</tr>
<tr class="odd">
<td><p><em>ToSpecificServers</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>ToSpecificServers</em> refere-se o script para servidores específicos.</p>

> [!TIP]  
> Se você estiver usando o parâmetro <EM>ToArrayMembers</EM> ou <EM>ToSpecificServers</EM> , você precisará especificar os nomes do servidor ou os nomes de matriz de servidores usando o parâmetro <EM>Identity</EM> .


</td>
</tr>
<tr class="even">
<td><p><em>Identity</em></p></td>
<td><p>Obrigatório</p></td>
<td><p>O parâmetro <em>Identity</em> Especifica o nome da matriz de servidor acesso para cliente ou os nomes dos servidores específicos que você está direcionando.</p></td>
</tr>
<tr class="odd">
<td><p><em>GenerateNewPasswordFor&lt;String&gt;</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>GenerateNewPasswordFor</em> Especifica que o script deve gerar uma nova senha para o ASA. O valor de cadeia de caracteres precisa ser a conta ASA no seguinte formato: domínio \ nome. Se você estiver usando uma conta de computador, você precisará acrescentar o caractere $ ao final do nome da conta.</p></td>
</tr>
<tr class="even">
<td><p><em>CopyFrom&lt;String&gt;</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>CopyFrom</em> Especifica que a credencial é copiada de outro servidor de acesso para cliente. O valor de cadeia de caracteres especificado é o nome do servidor acesso para cliente.</p></td>
</tr>
<tr class="odd">
<td><p><em>Mode</em></p></td>
<td><p>Opcional</p></td>
<td><p>A opção de <em>Mode</em> Especifica se o script é executado no modo assistido ou autônomo. Modo autônomo não solicita entrada do usuário e escolhe automaticamente uma estimativa conservadora mais opções, quando necessário.</p></td>
</tr>
<tr class="even">
<td><p><em>CreateScheduledTask&lt;String&gt;</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>CreateScheduledTask</em> informa ao script para criar uma tarefa agendada para executar a atualização de credencial ASA. O valor de cadeia de caracteres é o nome da tarefa agendada que será criado.</p>

> [!TIP]  
> Esse script cria um arquivo. cmd na pasta onde o script está localizado. A tarefa agendada será executado o arquivo. cmd uma vez a cada três semanas. Você pode editar a tarefa diretamente no Windows Agendador de tarefas para alterar a frequência da tarefa.


</td>
</tr>
<tr class="odd">
<td><p><em>WhatIf</em></p></td>
<td><p>Opcional</p></td>
<td><p>A opção <em>WhatIf</em> instrui o comando a simular as ações que ele executaria no objeto. Exiba as alterações que podem ocorrer usando a opção <em>WhatIf</em>, sem que seja necessário aplicar qualquer uma delas. Você não precisa especificar um valor com a opção.<em>WhatIf</em>.</p></td>
</tr>
<tr class="even">
<td><p><em>Confirm</em></p></td>
<td><p>Opcional</p></td>
<td><p>A opção <em>Confirm</em> faz com que o comando pause o processamento e exige que você confirme o que o comando realizará, para que o processamento continue. Você não precisa especificar um valor com a opção <em>Confirm</em>.</p></td>
</tr>
<tr class="odd">
<td><p><em>Verbose</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>Verbose</em> informa ao script para realizar o registro em log detalhado, para que as informações adicionais sobre ações do script são gravadas no arquivo de log.</p></td>
</tr>
<tr class="even">
<td><p><em>Debug</em></p></td>
<td><p>Opcional</p></td>
<td><p>O parâmetro <em>Debug</em> informa ao script a ser executado no modo de depuração. Este parâmetro deve ser usado para determinar por que o script falha.</p></td>
</tr>
</tbody>
</table>


## Exemplos

## Exemplo 1

Este exemplo usa o script para enviar as credenciais para todos os servidores de acesso para cliente na floresta para a instalação pela primeira vez.

    .\RollAlternateserviceAccountPassword.ps1 -ToEntireForest -GenerateNewPasswordFor "Contoso\ComputerAccount$" -Verbose

## Exemplo 2

Este exemplo gera uma nova senha para uma credencial ASA de conta de usuário e distribui a senha para todos os membros da matriz do servidor de acesso para cliente onde o nome corresponde \* \* caixa de correio.

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers *mailbox* -GenerateNewPasswordFor "Contoso\UserAccount" -Verbose

## Exemplo 3

Este exemplo agenda uma tarefa agendada de senha de uma vez por mês automatizado roll chamada "RollAsa do Exchange". Ele atualizará a credencial ASA para todos os servidores de acesso para cliente em toda a floresta com uma nova senha gerado pelo script. A tarefa agendada é criada, mas o script não é executado. Quando a tarefa agendada é executada, o script é executado no modo autônomo.

    .\RollAlternateServiceAccountPassword.ps1 -CreateScheduledTask "Exchange-RollAsa" -ToEntireForest -GenerateNewPasswordFor 'contoso\computerAccount$'

## Exemplo 4

Este exemplo atualiza a credencial ASA para todos os servidores de acesso para cliente pela matriz de servidores de acesso para cliente nomeado CAS01. Ela obtém a credencial da conta de computador do Active Directory ServiceAc1 no domínio Contoso.

    .\RollAlternateserviceAccountPassword.ps1 -ToArrayMembers "CAS01" -GenerateNewPasswordFor "CONTOSO\ServiceAc1$" 

## Exemplo 5

Este exemplo mostra como você pode usar o script para distribuir o ASA para um novo computador ou em um computador que está sendo colocado novamente em serviço porque você aumentar o tamanho da sua matriz de servidores ou novamente você está apresentando membros da matriz após a manutenção.

Você precisa atualizar a credencial ASA antes que o servidor de acesso para cliente recebe o tráfego. Copie a credencial ASA compartilhada de qualquer servidor de acesso para cliente que já está configurado corretamente. Por exemplo, se servidor A tem atualmente uma credencial ASA de trabalho e servidor B recém adicionada à matriz, você pode usar o script para copiar a credencial (incluindo a senha) de servidor A para servidor B. Isso é útil se o servidor B foi pressionada ou ainda não é um membro da matriz quando a senha foi revertida a última vez.

    .\RollAlternateServiceAccountPassword.ps1 -CopyFrom ServerA -ToSpecificServers ServerB -Verbose

