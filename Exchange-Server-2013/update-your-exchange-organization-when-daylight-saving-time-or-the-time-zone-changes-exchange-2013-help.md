---
title: 'Atualizar sua organização do Exchange quando o Horário de Verão entrar em vigor ou o fuso horário mudar: Exchange 2013 Help'
TOCTitle: Atualizar sua organização do Exchange quando o Horário de Verão entrar em vigor ou o fuso horário mudar
ms:assetid: 5b12615c-24cf-4f46-bf3c-2334dc734ef8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh530051(v=EXCHG.150)
ms:contentKeyID: 66457124
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Atualizar sua organização do Exchange quando o Horário de Verão entrar em vigor ou o fuso horário mudar

 

_**Aplica-se a:** Exchange Online, Exchange Server, Exchange Server 2010, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Se o país ou a região onde sua organização ou parte de seus usuários residem alterou a política de reconhecimento do Horário de Verão (DST) ou a diferença de horário em relação ao UTC, talvez seja necessário atualizar o Microsoft Windows, o Microsoft Exchange, o Microsoft Outlook ou outros programas para acomodar essas alterações.

Para mais informações sobre alterações no DST em todo o mundo, incluindo links, confira o [Centro de Ajuda e Suporte para Horário de Verão da Microsoft](https://go.microsoft.com/fwlink/p/?linkid=99640). Visite também os sites de suporte dos fornecedores de outros softwares instalados para verificar se eles exigem atualizações adicionais.

Mesmo que seu fuso horário não tenha mudado, se você interagir com outros computadores ou usuários espalhados pelo mundo, seu computador deve ser capaz de realizar cálculos de data e hora precisos para eventos em outros locais.

A instalação imediata das atualizações de fuso horário minimiza o número de reuniões ou compromissos que são agendados durante a transição da hora e data antiga para a nova.

## Como fazer isso?

## Etapa 1: Instalar a atualização do Windows DST em todos os computadores cliente e desktop

Como o sistema de autenticação do Office 365 é atualizado quando o DST ou um fuso horário muda, todos os computadores cliente com Office 365 precisam ser atualizados. Caso contrário, podem apresentar problemas de conectividade.

  - Verifique se todos os computadores cliente e desktop têm a atualização do Windows DST instalada. Para mais informações, confira [Como configurar o horário de verão para os sistemas operacionais Microsoft Windows](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=914387).

## Etapa 2: Instalar a atualização do Windows DST em todos os servidores

1.  Atualize todos os servidores no local com a atualização do Windows DST.

2.  Se estiver executando o Office 365, atualize qualquer servidor que interaja com o sistema de autenticação do Office 365, como servidores DirSync ou AD FS. Esses servidores devem ser atualizados para garantir o tempo de atividade.

**Observação**   Se estiver atualizando clusters de servidor, siga o processo normal de atualização de clusters. Atualize o servidor passivo primeiro, transfira o processamento para o servidor passivo (que se torna ativo) e, depois, atualize o servidor que estava ativo (que, agora, é o passivo). Para mais informações sobre como atualizar clusters de servidor e clusters de servidor de alta disponibilidade, confira [Atualizar Clusters do Exchange Server e Servidores de Alta Disponibilidade](https://technet.microsoft.com/pt-br/library/hh530052\(v=exchg.150\)) e [Como atualizar os clusters de failover do Windows Server](https://support.microsoft.com/pt-br/help/174799/how-to-update-windows-server-failover-clusters).

## Etapa 3: Atualizar o Exchange e o Outlook, onde necessário, em todos os computadores cliente e desktop

1.  Se os usuários estiverem usando o Outlook 2007 ou clientes mais antigos, determine quais ferramentas de fuso horário do Exchange ou o do Outlook devem ser executadas usando a tabela fornecida após este procedimento.

2.  Envie uma mensagem para os usuários que precisam atualizar seus computadores fornecendo a eles um link para a ferramenta apropriada.

A tabela a seguir mostra quando os usuários devem executar a [Ferramenta de Atualização do Calendário do Exchange](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879) ou a [Ferramenta de Atualização de Dados de Fuso Horário para Microsoft Office Outlook](http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667). Descubra qual versão os servidores da sua organização estão executando e, seguida, determine quais programas cliente seus usuários estão executando.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p><strong>Versão do Cliente</strong></p></td>
<td></td>
</tr>
<tr class="even">
<td><p><strong>Versão da organização</strong></p></td>
<td><p><strong>Outlook 2003 ou Outlook 2007</strong></p></td>
<td><p><strong>Outlook 2010</strong></p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2003 local</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879">Ferramenta de Calendário do Exchange</a> ou</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Ferramenta de Atualização de Dados de Fuso Horário para Microsoft Office Outlook</a></p></td>
<td><p>Nenhuma ação é necessária</p></td>
</tr>
<tr class="even">
<td><p><strong>Exchange 2007 no local</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879">Ferramenta de Calendário do Exchange</a> ou</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Ferramenta de Atualização de Dados de Fuso Horário para Microsoft Office Outlook</a></p></td>
<td><p>Nenhuma ação é necessária</p></td>
</tr>
<tr class="odd">
<td><p><strong>Exchange 2010 no local</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=930879">Ferramenta de Calendário do Exchange</a> ou</p>
<p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Ferramenta de Atualização de Dados de Fuso Horário para Microsoft Office Outlook</a></p></td>
<td><p>Nenhuma ação é necessária</p></td>
</tr>
<tr class="even">
<td><p><strong>Exchange 2013 local</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Ferramenta de Atualização de Dados de Fuso Horário para Microsoft Office Outlook</a></p></td>
<td><p>Nenhuma ação é necessária</p></td>
</tr>
<tr class="odd">
<td><p><strong>BPOS-S (Exchange 2007)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Ferramenta de Atualização de Dados de Fuso Horário para Microsoft Office Outlook</a></p></td>
<td><p>Nenhuma ação é necessária</p></td>
</tr>
<tr class="even">
<td><p><strong>BPOS-D (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Ferramenta de Atualização de Dados de Fuso Horário para Microsoft Office Outlook</a></p></td>
<td><p>Nenhuma ação é necessária</p></td>
</tr>
<tr class="odd">
<td><p><strong>Office 365 (Exchange 2010)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Ferramenta de Atualização de Dados de Fuso Horário para Microsoft Office Outlook</a> (não compatível com o Outlook 2003)</p></td>
<td><p>Nenhuma ação é necessária</p></td>
</tr>
<tr class="even">
<td><p><strong>Office 365 (Exchange 2013)</strong></p></td>
<td><p><a href="http://go.microsoft.com/fwlink/p/?linkid=3052%26kbid=931667">Ferramenta de Atualização de Dados de Fuso Horário para Microsoft Office Outlook</a> (não compatível com o Outlook 2003)</p></td>
<td><p>Nenhuma ação é necessária</p></td>
</tr>
<tr class="odd">
<td></td>
<td></td>
<td></td>
</tr>
</tbody>
</table>

