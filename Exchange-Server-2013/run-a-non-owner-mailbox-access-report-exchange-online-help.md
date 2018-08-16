---
title: 'Executar um relatório de acesso não proprietário da caixa de correio: Exchange 2013 Help'
TOCTitle: Executar um relatório de acesso não proprietário da caixa de correio
ms:assetid: dbbef170-e726-4735-abf1-2857db9bb52d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150575(v=EXCHG.150)
ms:contentKeyID: 50484836
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Executar um relatório de acesso não proprietário da caixa de correio

 

_**Aplica-se a:** Exchange Online_

_**Tópico modificado em:** 2016-12-09_

O relatório de acesso não proprietário da caixa de correio no Centro de administração do Exchange (EAC) lista as caixas de correio que foram acessadas por alguém que não seja o proprietário da caixa de correio. Quando uma caixa de correio é acessada por um não proprietário, o Microsoft Exchange registra informações sobre essa ação em um log de auditoria de caixa de correio é armazenado como uma mensagem de email em uma pasta oculta na caixa de correio estão sendo auditada. Entradas a partir desse log são exibidas como resultados da pesquisa e incluir uma lista de caixas de correio acessadas por um não proprietário, quem acessou a caixa de correio e quando, as ações realizadas pelo não proprietário, e se a ação foi bem-sucedida. Por padrão, as entradas no log de auditoria de caixa de correio são mantidas por 90 dias.

Quando você habilita o log para uma caixa de correio, o Microsoft Exchange ações específicas de logs não proprietários, incluindo os administradores e usuários, chamados *delegada usuários*, que receberam permissões para uma caixa de correio de auditoria de caixa de correio. Você também pode restringir a pesquisa para usuários dentro ou fora da sua organização.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 5 minutos.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "Log de auditoria de caixas de correio" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md).

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>..



## Habilitar log de auditoria de caixas de correio

Você precisa habilitar o log para cada caixa de correio que você deseja executar um relatório de acesso não proprietário da caixa de correio para de auditoria de caixa de correio. Se a auditoria de caixa de correio log não estiver habilitado, você não obtiver nenhum resultado quando você executar um relatório.

Para habilitar a caixa de correio log de auditoria para uma única caixa de correio, execute o seguinte comando no Shell.

    Set-Mailbox <Identity> -AuditEnabled $true

Por exemplo, para habilitar a auditoria de caixa de correio para uma usuária chamada Florence Flipo, execute o seguinte comando.

    Set-Mailbox "Florence Flipo" -AuditEnabled $true

Para habilitar a auditoria de caixas de correio para todas as caixas de correio de usuário da sua organização, execute os seguintes comandos:

```
    $UserMailboxes = Get-mailbox -Filter {(RecipientTypeDetails -eq 'UserMailbox')}
```
```
    $UserMailboxes | ForEach {Set-Mailbox $_.Identity -AuditEnabled $true}
```

## Como saber se funcionou?

Execute o seguinte comando para verificar se você configurou com êxito da caixa de correio log de auditoria.

    Get-Mailbox | FL Name,AuditEnabled

O valor de `True` referente à propriedade *AuditEnabled* verifica se os logs de auditoria estão habilitados.

Voltar ao início

## Executar um relatório de acesso não proprietário da caixa de correio

1.  No EAC, navegue até **Gerenciamento de conformidade** \> **auditoria**.

2.  Clique em **executar um relatório de acesso não proprietário da caixa de correio**.
    
    Por padrão, o Microsoft Exchange executa o relatório de acesso não proprietário para qualquer caixa de correio na organização nas últimas duas semanas. As caixas de correio listadas nos resultados da pesquisa tiverem sido habilitadas para caixa de correio do log de auditoria.

3.  Para exibir o acesso não proprietário para uma caixa de correio específica, selecione a caixa de correio da lista de caixas de correio. Exiba os resultados da pesquisa no painel de detalhes.


> [!TIP]
> Deseja restringir os resultados da pesquisa? Selecione a data de início, data de término ou ambos e marque as caixas de correio específicas para pesquisar. Clique em <STRONG>pesquisa</STRONG> para executar novamente o relatório.



## Pesquisa para tipos específicos de acesso não proprietário

Você também pode especificar o tipo de acesso não proprietário, também chamado o tipo de logon, para pesquisar. Aqui estão as suas opções:

  - **Todos os não proprietários**    Procura acesso por administradores e usuários delegados dentro da organização. Também inclui o acesso de usuário fora da sua organização.

  - **Usuários externos**    Procura acesso por usuários fora da sua organização.

  - **Administradores e usuários delegados**   Procura acesso por administradores e usuários delegados dentro da organização.

  - **Administradores**   Procura acesso por administradores em sua organização.

Voltar ao início

## Como saber se funcionou?

Para verificar que você tenha executado com êxito um relatório de acesso não proprietário da caixa de correio, verifique o painel de resultados da pesquisa. Caixas de correio que você executou o relatório para são exibidas nesse painel. Se não houver nenhum resultado de uma caixa de correio específico, é possível que tenha sido acesso por um não proprietário ou que acesso não proprietário não ocorreu dentro do intervalo de datas especificado. Conforme descrito anteriormente, certifique-se de verificar se os logs de auditoria foram habilitados para as caixas de correio que você deseja pesquisar para acesso por não proprietários.

Voltar ao início

## O que obtém registrado no log de auditoria de caixa de correio?

Quando você executar um relatório de acesso não proprietário da caixa de correio, entradas do log de auditoria de caixa de correio são exibidas nos resultados da pesquisa no EAC. Cada entrada de relatório contém estas informações:

  - Quem acessou a caixa de correio e quando

  - As ações executadas pelo não proprietário

  - A mensagem afetada e seu local de pasta

  - Se a ação foi bem-sucedida

A tabela a seguir lista as ações executadas pelo log de auditoria de não-proprietários que podem ser registrados por caixa de correio. Na tabela, um **Sim** indica que a ação pode ser registrada para esse tipo de logon e um **não** indica que uma ação não puder ser registrada. Um asterisco (**\***) indica que a ação é registrada por padrão quando o log de auditoria de caixa de correio está habilitado para a caixa de correio. Se você deseja controlar as ações que não são registradas por padrão, você precisará usar o PowerShell para habilitar o log dessas ações.


> [!NOTE]
> Um administrador que tenha sido atribuído a permissão de acesso completo à caixa de correio de um usuário é considerado um usuário delegado.




<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Ação</th>
<th>Descrição</th>
<th>Administrador</th>
<th>Usuário delegado</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Copiar</strong></p></td>
<td><p>Uma mensagem foi copiada a outra pasta.</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p><strong>Criar</strong></p></td>
<td><p>Um item é criado nas pastas Calendário, Contatos, Anotações ou Tarefas na caixa de correio; por exemplo, é criada uma nova solicitação de reunião. Observe que a mensagem ou a criação da pasta não são auditadas.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim*</p></td>
</tr>
<tr class="odd">
<td><p><strong>FolderBind</strong></p></td>
<td><p>Uma pasta de caixa de correio foi acessada.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p><strong>Exclusão forçada</strong></p></td>
<td><p>Uma mensagem foi removida da pasta de Itens Recuperáveis.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim*</p></td>
</tr>
<tr class="odd">
<td><p><strong>MessageBind</strong></p></td>
<td><p>Uma mensagem foi exibida no painel de visualização ou aberta.</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p><strong>Mover</strong></p></td>
<td><p>Uma mensagem foi movida para outra pasta.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p><strong>Mover para itens excluídos</strong></p></td>
<td><p>Uma mensagem foi movida para a pasta Itens Excluídos.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p><strong>Enviar como</strong></p></td>
<td><p>Uma mensagem foi enviada usando a permissão SendAs. Isto significa que outro usuário enviou a mensagem apesar de ter vindo do proprietário da caixa de correio.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim*</p></td>
</tr>
<tr class="odd">
<td><p><strong>Enviar em nome de</strong></p></td>
<td><p>Uma mensagem foi enviada usando a permissão SendOnBehalf. Isto significa que outro usuário enviou a mensagem em nome do proprietário da caixa de correio. A mensagem indicará ao destinatário em nome de quem a mensagem foi enviada e quem na verdade enviou a mensagem.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p><strong>Excluído por software</strong></p></td>
<td><p>Uma mensagem foi excluída da pasta Itens Excluídos.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim*</p></td>
</tr>
<tr class="odd">
<td><p><strong>Atualizar</strong></p></td>
<td><p>Uma mensagem foi alterada.</p></td>
<td><p>Sim*</p></td>
<td><p>Sim*</p></td>
</tr>
</tbody>
</table>



> [!NOTE]
> *&nbsp; Auditado por padrão se a auditoria estiver habilitada para uma caixa de correio.



Voltar ao início

