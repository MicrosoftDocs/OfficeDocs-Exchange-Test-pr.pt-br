---
title: 'Lista de verificação: Atualização do Exchange 2010: Exchange 2013 Help'
TOCTitle: 'Lista de verificação: Atualização do Exchange 2010'
ms:assetid: 06c1045a-5fcf-4e24-a901-1a979302fb8d
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee332309(v=EXCHG.150)
ms:contentKeyID: 51407833
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lista de verificação: Atualização do Exchange 2010

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-04-07_

Use esta lista de verificação para atualizar do Microsoft Exchange 2010 para Exchange 2013. Antes de começar a trabalhar com esta lista de verificação, certifique-se de que estar familiarizado com os conceitos discutidos:

  - [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Novidades do Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md)

Esta lista de verificação é genérica, pois fornece orientações para um cenário de atualização típico.


> [!TIP]  
> O Assistente de Implantação do Exchange Server oferece orientação personalizada passo a passo sobre como implantar o Exchange Server. O Assistente de Implantação pode ajudar a implantar uma nova instalação do Exchange Server 2013, atualizar uma versão anterior para o Exchange 2013 ou configurar uma implantação híbrida do Exchange 2013 e do Exchange Online. Para saber mais, confira <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente de implantação do Exchange Server</A>.



## Lista de verificação para atualizar do Exchange 2010 para o Exchange 2013


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Pronto?</p></td>
<td><p>Tarefa</p></td>
<td><p>Tópico(s)</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. Ler as notas de versão.</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Notas de versão do Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>2. Verificar os requisitos do sistema</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos de sistema do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>3. Confirmar se as etapas de pré-requisitos foram realizadas</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">Lista de verificação de segurança de implantação</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>4. Configurar o namespace separado</p>

> [!TIP]  
> Esta etapa é opcional. É necessária apenas se a sua organização estiver executando um namespace separado.


</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">Configurar a lista de pesquisa de sufixo DNS para um namespace separado</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. Selecione um catálogo de endereços offline para todos os bancos de dados de caixa de correio do Exchange 2010</p></td>
<td><p><a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Set mailbox database properties</a> em <a href="manage-mailbox-databases-in-exchange-2013-exchange-2013-help.md">Gerenciar bancos de dados de caixa de correio no Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. Instalar o Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar o Exchange 2013 usando o Assistente para Configuração</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Instalar a função de Transporte de Borda do Exchange 2013 usando o Assistente para Configuração</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Verificar uma instalação do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Criar uma caixa de correio do Exchange 2013</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">Criar caixas de correio do usuário</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Configurar diretórios virtuais relacionados ao Exchange</p>

> [!TIP]  
> Essa etapa será necessária se você quiser usar Serviços Web do Exchange, o Outlook em Qualquer Lugar ou o catálogo de endereços offline. Ela também poderá ser necessária se você precisar alterar qualquer uma das configurações padrão para Painel de Controle do Exchange, Microsoft Office&nbsp;Outlook Web App ou Exchange ActiveSync.<BR>


</td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuração do servidor de Acesso para Cliente do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Adicionar certificados digitais ao servidor de Acesso para Cliente</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">Certificados digitais e SSL</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. Mover a caixa de correio de arbitragem</p></td>
<td><p><a href="move-the-exchange-2010-system-mailbox-to-exchange-2013-exchange-2013-help.md">Mover a caixa de correio de sistema do Exchange 2010 para o Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configurar a Unificação de Mensagens</p>

> [!TIP]  
> Esta etapa é opcional. É necessária apenas se você quiser usar a Unificação de Mensagens na sua organização.


</td>
<td><p><a href="upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md">Atualizar UM do Exchange 2010 para UM do Exchange 2013</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>12. Configurar o servidor de Transporte de Borda</p>

> [!TIP]  
> Esta etapa é opcional. Só será necessária se sua organização utilizar um servidor de Transporte de Borda.


</td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">Configurar o fluxo de mensagens da Internet por meio de um servidor de Transporte de Borda inscrito</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>13. Ativar e configurar o Outlook em Qualquer Lugar</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook em Qualquer Lugar</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. Configurar o ponto de conexão do serviço</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuração do servidor de Acesso para Cliente do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Configurar registros DNS</p></td>
<td><p><a href="https://technet.microsoft.com/pt-br/library/dn307232(v=exchg.150)">Configurar registros DNS para instalação de vários servidores do Exchange 2010</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16. mover caixas de correio do Exchange 2010 para Exchange 2013</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Movimentações de caixa de correio no Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. Mover dados de pastas públicas do Exchange 2013 para o Exchange 2013</p></td>
<td><p><a href="public-folders-exchange-2013-help.md">Pastas públicas</a></p>
<p><a href="https://technet.microsoft.com/pt-br/library/jj150486(v=exchg.150)">Use serial migração para migrar pastas públicas para o Exchange 2013 de versões anteriores</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>18. Tarefas pós-instalação</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Tarefas de pós-instalação do Exchange 2013</a></p></td>
</tr>
</tbody>
</table>

