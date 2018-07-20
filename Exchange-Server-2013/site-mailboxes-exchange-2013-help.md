---
title: 'Caixas de correio locais: Exchange 2013 Help'
TOCTitle: Caixas de correio locais
ms:assetid: 2c4393f4-d274-4e6c-bd09-9577e68c5a33
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ150499(v=EXCHG.150)
ms:contentKeyID: 50485243
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Caixas de correio locais

 

_**Aplica-se a:** Exchange Online, Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Emails e documentos são tradicionalmente mantidos em dois repositórios de dados exclusivos e separados. A maioria das organizações colabora usando os dois meios. O desafio é que tanto email quanto documentos são acessados usando-se clientes diferentes. Isso geralmente resulta em uma redução da produtividade do usuário e em uma experiência degradada para ele.

A *caixa de correio de site* é um conceito novo no Microsoft Exchange 2013 que tenta resolver esse problema. As caixas de correio de site melhoram a colaboração e a produtividade do usuário, permitindo acesso tanto a documentos do Microsoft SharePoint 2013 quanto a emails do Exchange, usando a mesma interface de cliente. Uma caixa de correio de site é composta funcionalmente pela associação ao site do SharePoint 2013 (proprietários e membros), armazenamento compartilhado através de uma caixa de correio do Exchange 2013 para emails e um site do SharePoint 2013 para documentos e uma interface de gerenciamento que lida com as necessidades de provisionamento e ciclo de vida.

As caixas de correio de site requerem configuração e integração do Exchange 2013 e do SharePoint Server 2013. Para mais informações sobre como configurar sua organização do Exchange 2013 para funcionar com a organização do SharePoint Server 2013, consulte estes tópicos:

  - [Configurar caixas de correio de site no SharePoint Server 2013](https://go.microsoft.com/fwlink/p/?linkid=258264).

  - [Integração com o SharePoint e o Lync](integration-with-sharepoint-and-lync-exchange-2013-help.md)

Para mais informações sobre recursos de colaboração do Exchange Server 2013, consulte [Colaboração](collaboration-exchange-2013-help.md).

**Sumário**

How do site mailboxes work?

Site mailbox provisioning policies

## Como funcionam as caixas de correio de site?

Quando um membro do projeto arquiva emails ou documentos usando a caixa de correio de site, qualquer membro do projeto pode acessar o conteúdo. As caixas de correio de site estão na superfície do Outlook 2013 e oferecem, aos usuários, acesso fácil aos emails e documentos dos projetos de sua responsabilidade. Adicionalmente, o mesmo conjunto de conteúdos pode ser acessado diretamente do site do SharePoint em si. Com caixas de correio de site, o conteúdo fica onde tem que ficar. O Exchange armazena os emails, oferecendo, aos usuários, o mesmo modo de exibição de mensagens para conversas por email que eles usam todos os dias, em suas próprias caixas de correio. Enquanto isso, o SharePoint armazena os documentos, trazendo a coautoria e as versões dos documentos para o jogo. O Exchange sincroniza apenas os metadados suficientes do SharePoint para criar a visualização do documento no Outlook (por exemplo, título do documento, data da última atualização, autor da última modificação, tamanho).

![Diagrama de uso e armazenamento de caixas de correio do site](images/JJ150499.b98be571-d2e0-4ebd-9fe2-440a14e91e35(EXCHG.150).gif "Diagrama de uso e armazenamento de caixas de correio do site")

## Políticas de provisionamento de caixa de correio de site

As cotas de caixa de correio de site podem ser definidas usando-se os cmdlets **SiteMailboxProvisioningPolicy** no Shell de Gerenciamento do Exchange. As políticas de provisionamento de caixa de correio de Site se aplicam somente ao email que enviado de e para a caixa de correio de site e o tamanho da caixa de correio de site no servidor do Exchange. As configurações de repositório de documentos são definidas no SharePoint. Apesar de você poder criar várias políticas de provisionamento de caixa de correio de site, usando o cmdlet **New-SiteMailboxProvisioningPolicy**, somente a política de provisionamento padrão será aplicada a todas as caixas de correio de site. Você não pode aplicar várias políticas dentro de sua organização. As políticas de provisionamento permitem que você defina as seguintes quotas:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Cota</th>
<th>Descrição</th>
<th>Configuração padrão</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>IssueWarningQuota</p></td>
<td><p>O parâmetro <em>IssueWarningQuota</em> especifica o tamanho da caixa de correio de site que aciona a mensagem de aviso para a caixa de correio de site</p></td>
<td><p>4,5 GB</p></td>
</tr>
<tr class="even">
<td><p>MaxReceiveSize</p></td>
<td><p>O parâmetro <em>MaxReceiveSize</em> especifica o tamanho máximo das mensagens de email que podem ser recebidas pela caixa de correio local.</p></td>
<td><p>36 MB</p></td>
</tr>
<tr class="odd">
<td><p>ProhibitSendReceiveQuota</p></td>
<td><p>O parâmetro <em>ProhibitSendReceiveQuota</em> especifica o tamanho no qual a caixa de correio local não pode mais enviar ou receber mensagens.</p></td>
<td><p>5 GB</p></td>
</tr>
</tbody>
</table>


Para mais informações sobre como configurar as políticas de provisionamento de caixa de correio de site, consulte [Gerenciar políticas de provisionamento de caixa de correio do site](manage-site-mailbox-provisioning-policies-exchange-2013-help.md).

Voltar ao início

## Retenção e política de ciclo de vida

O ciclo de vida de uma caixa de correio de site é gerenciado através de um SharePoint. É através do SharePoint que você deve executar todas as tarefas de caixa de correio de site, como criar e remover caixas de correio de site. Além disso, você pode criar uma política de Ciclo de Vida do SharePoint, para gerenciar o ciclo de vida de uma caixa de correio de site. Por exemplo, você pode criar uma política de ciclo de vida no SharePoint que feche automaticamente todas as caixas de correio de site após 6 meses. Se o usuário ainda precisar usar a caixa de correio de site, o usuário poderá reativar a caixa de correio do site através do SharePoint. Recomendamos que você use o aplicativo de Ciclo de vida que está na fazenda. Remover manualmente as caixas de correio de site ativas do Exchange irá resultar em caixas de correio de site órfãs. .

Quando o aplicativo de ciclo de vida no SharePoint fechar uma caixa de correio de site, essa caixa será retida pelo período declarado na política de ciclo de vida no estado fechado. A caixa de correio poderá ser reativada por um usuário final ou por um administrador do SharePoint. Depois do período de retenção, a caixa de correio de site do Exchange que está hospedada no banco de dados de caixa de correio terá **MDEL:**  colocado à frente do seu nome, para indicar que foi marcado para exclusão. Você precisará remover manualmente essas caixas de correio de site do banco de dados de caixa de correio, para liberar espaço de armazenamento e o alias. Se você não tiver habilitado a Política de Ciclo de vida do SharePoint, você perderá a habilidade de determinar que caixas de correio de site estão marcadas para exclusão. Até que a caixa de correio de site tenha sido removida por um administrador, o conteúdo dela ainda poderá ser recuperado.

Você pode usar este comando para procurar e remover caixas de correio de site que foram marcadas para exclusão.

    Get-Mailbox MDEL:* | ?{$_.RecipientTypeDetails -eq "TeamMailbox"} | Remove-Mailbox -Confirm:$false

Caixas de correio de site não suportam a retenção no nível do item. A retenção funciona em um nível de projeto para caixas de correio de site, de forma que, quando toda a caixa de correio for excluída, os itens retidos sejam excluídos.

## Conformidade

Usando o Console de Descoberta Eletrônica no SharePoint, as caixas de correio de site podem ser parte do escopo da Descoberta Eletrônica In-loco, pois você pode fazer pesquisas de palavras-chave em relação a caixas de correio de usuário ou de site. Além disso, você pode colocar uma caixa de correio do site em retenção legal. Para mais informações, consulte [Descoberta Eletrônica In-loco](in-place-ediscovery-exchange-2013-help.md).


> [!TIP]
> Para colocar uma caixa de correio de site em retenção legal em Office 365, ele deve ser atribuído a uma licença Exchange Online (plano 2). Se uma caixa de correio de site é atribuída a uma licença Exchange Online (plano 1), você teria atribuí-lo de uma licença separada Exchange Online arquivamento colocá-lo em espera.



Voltar ao início

## Backup e restauração

O backup e a restauração das caixas de correio de site do Exchange que estão no servidor de caixa de correio irão usar o mesmo método de backup e restauração que você usar para todas as caixas de correio do Exchange. Para mais informações, consulte [Grupos de Disponibilidade do Banco de Dados (DAGs)](database-availability-groups-dags-exchange-2013-help.md).

Para documentos do SharePoint, você deve fazer backup e restauração no mesmo local. Se você restaurar seu conteúdo do SharePoint nas mesmas URLs, a caixa de correio de site irá continuar a funcionar, e nunca configuração adicional será necessária. Se você restaurar para uma URL diferente, precisará executar o cmdlet **Set-SiteMailbox** para atualizar a propriedade *SharePointURL*. Recomendamos que você não restaure o SharePoint para uma nova floresta.

