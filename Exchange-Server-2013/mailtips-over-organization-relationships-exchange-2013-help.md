---
title: 'Dicas de email sobre relacionamentos da organização: Exchange 2013 Help'
TOCTitle: Dicas de email sobre relacionamentos da organização
ms:assetid: 1784256f-abe1-4503-b8c4-26d544b73452
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ670165(v=EXCHG.150)
ms:contentKeyID: 50485106
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Dicas de email sobre relacionamentos da organização

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2015-03-09_

O Microsoft Exchange Server 2013 permite configurar relações organizacionais com o Microsoft Exchange Online ou outras organizações do Exchange. O estabelecimento de um relacionamento de organização permite aprimorar a experiência do usuário ao lidar com a outra organização. Por exemplo, você pode compartilhar dados de disponibilidade, configurar um fluxo de mensagens seguro e habilitar o controle de mensagem em ambas as organizações.

## Controlando o nível de acesso às Dicas de Email

É possível restringir certos tipos de Dicas de Email. Você pode permitir que todas as Dicas de Email sejam retornadas ou permitir somente um conjunto limitado que impediria NDRs. É possível definir essa configuração com o parâmetro *MailTipsAccessLevel* no cmdlet **Set-OrganizationRelationship**. A tabela a seguir mostra quais Dicas de email são retornadas na relação organizacional.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Dica de Email</th>
<th>A Dica de Email está disponível quando o nível de acesso é definido como Todos?</th>
<th>A Dica de Email está disponível quando o nível de acesso é definido como Limitado?</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Grande público</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>Respostas Automáticas</p></td>
<td><p>Sim</p>
<p>Se o domínio remoto do destinatário for especificado como interno, a resposta automática interna será exibida. Caso contrário, a resposta automática externa será exibida.</p></td>
<td><p>Sim</p>
<p>A resposta automática externa é exibida.</p></td>
</tr>
<tr class="odd">
<td><p>Destinatário moderado</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>Mensagem com tamanho excessivo</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="odd">
<td><p>Destinatário restrito</p></td>
<td><p>Sim</p></td>
<td><p>Sim</p></td>
</tr>
<tr class="even">
<td><p>Caixa de Correio Cheia</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
</tr>
<tr class="odd">
<td><p>Dicas de Email Personalizadas</p></td>
<td><p>Sim</p></td>
<td><p>Não</p></td>
</tr>
<tr class="even">
<td><p>Destinatários externos</p></td>
<td><p>Sim</p>
<p>Se o domínio remoto do destinatário for especificado como interno, essa Dica de email é suprimida. Caso contrário, a Dica de email externa é retornada.</p></td>
<td><p>Sim</p>
<p>Se o domínio remoto do destinatário for especificado como interno, essa Dica de email é suprimida. Caso contrário, a Dica de email externa é retornada.</p></td>
</tr>
</tbody>
</table>


Para etapas detalhadas sobre como configurar níveis de acesso a Dicas de email, consulte [Gerenciar dicas de email para relacionamentos da organização](manage-mailtips-for-organization-relationships-exchange-2013-help.md).

## Controlando o escopo de acesso às Dicas de Email

Quando você habilita as Dicas de email em uma relação organizacional e define o nível de acesso como `All`, as Dicas de email, a Caixa de correio cheia, as Respostas automáticas e as Dicas de email personalizadas específicas do destinatário são retornadas para todos os usuários. Contudo, talvez você queira permitir essas Dicas de email somente para um conjunto específico de usuários. Por exemplo, se você configurar uma relação organizacional com um parceiro, talvez queira permitir essas Dicas de email somente para os usuários que trabalham com esse parceiro.

Para isso, é preciso primeiro criar um grupo e adicionar todos os usuários com os quais você deseja compartilhar Dicas de email específicas do destinatário. É possível então especificar esse grupo na relação organizacional.

Após implementar essa restrição, os servidores de Acesso para Cliente verificarão primeiro se o destinatário para o qual eles receberam uma consulta de Dicas de email faz parte desse grupo. Se o destinatário for membro desse grupo, os servidores de Acesso para Cliente retornarão um proxy de todas as Dicas de email, incluindo as Dicas de email específicas do destinatário. Caso contrário, eles não incluirão na resposta as Dicas de email específicas do destinatário.

Para etapas detalhadas sobre como configurar níveis de acesso a Dicas de email, consulte [Gerenciar dicas de email para relacionamentos da organização](manage-mailtips-for-organization-relationships-exchange-2013-help.md).

