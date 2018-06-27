---
title: 'Cmdlets: Exchange 2013 Help'
TOCTitle: Cmdlets
ms:assetid: 1d741dea-1eb8-4909-850f-63d4efaa1a32
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa996589(v=EXCHG.150)
ms:contentKeyID: 50485140
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Cmdlets

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

Um *cmdlet*, pronunciado "command-let", é a menor unidade de funcionalidade do Shell de Gerenciamento do Exchange. Os cmdlets assemelham-se a comandos internos em outros shells, por exemplo, o comando `dir` encontrado no `cmd.exe`. Da mesma forma que esses comandos familiares, os cmdlets podem ser chamados diretamente da linha de comando do Shell e executados no contexto do Shell, não como um processo separado.


> [!TIP]
> Desde o Microsoft Exchange Server 2007, houve alterações na forma como o Exchange 2013 usa os cmdlets internamente devido ao uso da funcionalidade remota do Windows&nbsp;PowerShell. Essas alterações têm pouco ou nenhum impacto sobre a forma como você precisa usar os cmdlets, mas podem oferecer mais flexibilidade na forma como você gerencia seus servidores do Exchange.



Os cmdlets geralmente são desenvolvidos em torno de tarefas administrativas repetitivas, e no Shell, várias centenas de cmdlets são fornecidos para tarefas específicas de gerenciamento do Exchange. Esses cmdlets estão disponíveis, além dos cmdlets de sistema que não são do Exchange incluídos no projeto básico do shell do Windows PowerShell. Para obter informações sobre como abrir o Shell de Gerenciamento do Exchange, consulte [Abra o shell.](https://technet.microsoft.com/pt-br/library/dd638134\(v=exchg.150\)).

Todos os cmdlets do Shell são apresentados em pares verbo-substantivo. O par verbo-substantivo é sempre separado por um hífen (-) sem espaços e os nomes do cmdlet estão sempre no singular. Os verbos se referem à ação que o cmdlet executa. Os substantivos se referem ao objeto no qual o cmdlet executa a ação. Por exemplo, no cmdlet **Get-SystemMessage**, o verbo é **Get** e o substantivo é **SystemMessage**. Todos os cmdlets do Shell que gerenciam um recurso específico compartilham o mesmo substantivo. A tabela a seguir fornece exemplos de alguns verbos disponíveis no Shell.


> [!TIP]
> Por padrão, se o verbo for omitido, o Shell presumirá o verbo <STRONG>Get</STRONG>. Por exemplo, ao chamar <STRONG>Mailbox</STRONG>, recuperará os mesmos resultados que obteria caso tivesse chamado <STRONG>Get-Mailbox</STRONG>.



### Exemplos de verbos do Shell de Gerenciamento do Exchange

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Verbo</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>Disable</strong></p></td>
<td><p>Os cmdlets <strong>Disable</strong> definem o status <code>Enabled</code> do objeto especificado do Exchange como <code>$False</code>. Isso impede que o objeto processe dados ainda que o objeto exista.</p></td>
</tr>
<tr class="even">
<td><p><strong>Enable</strong></p></td>
<td><p>Os cmdlets <strong>Enable</strong> definem o status Habilitado do objeto especificado do Exchange como <code>$True</code>. Isso habilita o objeto a processar dados.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Get</strong></p></td>
<td><p>Os cmdlets <strong>Get</strong> recuperam informações sobre um objeto específico do Exchange.</p>

> [!TIP]
> A maioria dos cmdlets <STRONG>Get</STRONG> retornam apenas informações resumidas quando são executados. Para dizer ao cmdlet <STRONG>Get</STRONG> que retorne informações detalhadas ao executar um comando, canalize o comando para o cmdlet <STRONG>Format-List</STRONG>. Para obter mais informações sobre o comando <STRONG>Format-List</STRONG>, consulte <A href="working-with-command-output-exchange-2013-help.md">Trabalhando com a saída do comando</A>. Para mais informações sobre pipeline, consulte <A href="https://technet.microsoft.com/pt-br/library/aa998260(v=exchg.150)">Pipelining</A>.


</td>
</tr>
<tr class="even">
<td><p><strong>Install</strong></p></td>
<td><p>Os cmdlets <strong>Install</strong> instalam um novo objeto ou recurso em um servidor Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Move</strong></p></td>
<td><p>Os cmdlets <strong>Move</strong> realocam o objeto especificado do Exchange de um contêiner ou servidor para outro.</p></td>
</tr>
<tr class="even">
<td><p><strong>New</strong></p></td>
<td><p>Os cmdlets <strong>New</strong> criam um novo objeto do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Remove</strong></p></td>
<td><p>Os cmdlets <strong>Remove</strong> excluem o objeto especificado do Exchange.</p></td>
</tr>
<tr class="even">
<td><p><strong>Set</strong></p></td>
<td><p>Os cmdlets <strong>Set</strong> modificam as propriedades de um objeto existente do Exchange.</p></td>
</tr>
<tr class="odd">
<td><p><strong>Test</strong></p></td>
<td><p>Os cmdlets <strong>Test</strong> testam componentes específicos do Exchange e fornecem arquivos de log que você pode examinar.</p></td>
</tr>
<tr class="even">
<td><p><strong>Uninstall</strong></p></td>
<td><p>Os cmdlets <strong>Uninstall</strong> removem um objeto ou recurso de um servidor Exchange.</p></td>
</tr>
</tbody>
</table>


A lista a seguir de cmdlets é um exemplo de um conjunto completo de cmdlets. Esse conjunto de cmdlets é usado para gerenciar as mensagens de notificação de status de entrega (DSN) e os recursos de mensagem de cota da caixa de correio do Exchange 2013:

  - **Get-SystemMessage**

  - **New-SystemMessage**

  - **Remove-SystemMessage**

  - **Set-SystemMessage**

