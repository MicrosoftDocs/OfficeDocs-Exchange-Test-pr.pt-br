---
title: 'Disponibilidade compartilhada em implantações híbridas do Exchange: Exchange 2013 Help'
TOCTitle: Disponibilidade compartilhada em implantações híbridas do Exchange
ms:assetid: bd3884de-80ee-4ff2-a8a3-eacd5aa3e51b
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ650274(v=EXCHG.150)
ms:contentKeyID: 50487124
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Disponibilidade compartilhada em implantações híbridas do Exchange

 

_**Aplica-se a:**Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-04-29_

O compartilhamento de informações de disponibilidade (disponibilidade de calendário) entre usuários localizados na organização local ou na organização do Exchange Online é um dos principais benefícios de uma implantação híbrida. Usuários em ambas as organizações podem visualizar os calendários uns dos outros como se estivessem na mesma organização física. Isso torna o agendamento de reuniões e recursos fácil e eficiente.

São necessários vários componentes em uma implantação híbrida para habilitar o recurso de disponibilidade compartilhada entre a sua organização local do Exchange e o Exchange Online.

  - **Confiança de federação**   Tanto a organização de serviço local quanto a organização do Office 365 precisam ter uma confiança de federação estabelecida com o sistema de autenticação do AD do Azure. Uma confiança de federação é uma relação um-para-um com o sistema de autenticação do AD do Azure que define parâmetros para sua organização do Exchange. O sistema usa esses parâmetros ao atuar como um agente de confiança entre sua organização local e sua organização do serviço do Office 365 para trocar informações de disponibilidade entre usuários das organizações local e do Exchange Online.
    
    Uma confiança de federação com o sistema é automaticamente configurada para a sua organização de serviço do Office 365 quando a conta é criada. O assistente de Configuração Híbrida verifica automaticamente se há uma confiança de federação com o sistema de autenticação do AD do Azure para a organização local. Se houver, a confiança de federação existente será usada para dar suporte à implantação híbrida. Caso contrário, o assistente criará uma confiança de federação para a organização local com o sistema de autenticação do AD do Azure. O assistente também adiciona qualquer domínio selecionado no assistente de Configuração Híbrida à confiança de federação da organização local.
    
    Saiba mais em [Compartilhamento](https://technet.microsoft.com/pt-br/library/dd638083\(v=exchg.150\)).

  - **Relacionamentos de organização**   Relacionamentos de organização são necessários para ambas as organizações local e do Exchange Online e são configurados automaticamente pelo assistente de Configuração Híbrida. Um relacionamento da organização define o nível de informações de disponibilidade compartilhado para uma organização.
    
    Por padrão, o nível de compartilhamento de acesso aos dados de disponibilidade é **Acesso de disponibilidade com hora, mais assunto e local** para ambos os relacionamentos de organização local e do Exchange. Se você deseja modificar o acesso ao compartilhamento de disponibilidade entre os usuários da sua organização local e do Exchange Online, você pode configurar manualmente o nível de acesso ao relacionamento da organização após concluir o assistente de Configuração Híbrida.
    
    Saiba mais em [Compartilhamento](https://technet.microsoft.com/pt-br/library/dd638083\(v=exchg.150\)).

Ao configurar sua organização para uma implantação híbrida, a configuração do acesso ao compartilhamento de informações de calendário sobre disponibilidade será automaticamente definida pelo assistente de Configuração Híbrida em todos os cenários. Criar uma confiança de federação com o sistema de autenticação do AD do Azure e configurar relações da organização para a organização local e do Exchange Online são requisitos para a implantação híbrida. Se você não quiser permitir o compartilhamento de informações sobre disponibilidade entre os usuários da organização local e do Exchange Online na implantação híbrida, você pode desativar manualmente o compartilhamento de informações sobre disponibilidade usando o Shell de Gerenciamento do Exchange e o cmdlet do [Set-HybridConfiguration](https://technet.microsoft.com/pt-br/library/hh529932\(v=exchg.150\)) depois que o assistente de Configuração Híbrida for concluído.

Os recursos de implantação híbrida mostrados na tabela a seguir têm uma dependência em confianças de federação e relacionamentos da organização.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Área de mensagens</th>
<th>Feature</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Cliente de email</p></td>
<td><ul>
<li><p>Controle de mensagens</p></li>
<li><p>MailTips</p></li>
<li><p>Pesquisa de várias caixas de correio</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Conformidade</p></td>
<td><ul>
<li><p>ExchangeArquivamento Online</p></li>
<li><p>Exchange Descoberta eletrônica in-loco</p></li>
</ul></td>
</tr>
</tbody>
</table>

