---
title: 'Não é possível encontrar um service_RUSMissing de atualização de destinatário'
TOCTitle: Não é possível encontrar um service_RUSMissing de atualização de destinatário
ms:assetid: 920fbf51-d5e4-4ac6-869f-7f1c5d9a3024
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.rusmissing(v=EXCHG.150)
ms:contentKeyID: 50486191
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Não é possível encontrar um service\_RUSMissing de atualização de destinatário

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2016-12-15_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft® Exchange Server 2007 ou Exchange Server 2010 não pode continuar porque não foi possível encontrar o Recipient Update Service (RUS) responsável por um domínio na organização do Exchange existente.

Requer a instalação do Microsoft Exchange que cada domínio na organização do Exchange existente possui uma instância do serviço de atualização de destinatário.

Se uma instância do serviço de atualização de destinatário estiver ausente para um domínio, novos objetos de usuário criados no domínio não receberá os endereços de email emitidos para eles.

Para resolver esse problema, verifique se existe uma instância do serviço de atualização de destinatário para cada domínio e criar uma instância do serviço de atualização de destinatário para os domínios que não têm um e, em seguida, execute novamente a instalação do Microsoft Exchange.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Para criar uma instância de serviço de atualização de destinatário para um domínio</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Abra o Gerenciador de sistema do Exchange.</p></li>
<li><p>Expanda os <strong>destinatários</strong>.</p></li>
<li><p>Clique com botão direito no nó <strong>Recipient Update Services</strong>, clique em <strong>novo</strong> e, em seguida, clique em <strong>Serviço de atualização de destinatário</strong>.</p></li>
<li><p>Na janela do novo objeto, clique em <strong>Procurar</strong> para localizar o nome do domínio.</p></li>
<li><p>Selecione o nome do domínio e clique em <strong>OK</strong>.</p></li>
<li><p>Na janela do novo objeto, clique em <strong>Avançar</strong> e <strong>Concluir</strong>.</p></li>
</ol></td>
</tr>
</tbody>
</table>


Para obter mais informações sobre o serviço de atualização de destinatário, consulte os seguintes artigos da Base de Conhecimento Microsoft:

  - "Como o serviço de atualização de destinatário aplica políticas de destinatário" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=328738](https://go.microsoft.com/fwlink/?linkid=3052&kbid=328738)).

  - "Como o serviço de atualização de destinatário preenche listas de endereços" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253828](https://go.microsoft.com/fwlink/?linkid=3052&kbid=253828)).

  - "Como verificar o andamento do serviço de atualização de destinatário do Exchange" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=246127](https://go.microsoft.com/fwlink/?linkid=3052&kbid=246127)).

  - "Tarefas realizadas pelo serviço de atualização de destinatário do Exchange" ([https://go.microsoft.com/fwlink/?linkid=3052\&kbid=253770](https://go.microsoft.com/fwlink/?linkid=3052&kbid=253770)).

