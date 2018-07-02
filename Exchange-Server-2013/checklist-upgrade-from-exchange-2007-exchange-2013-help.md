---
title: 'Lista de verificação: Atualização do Exchange 2007: Exchange 2013 Help'
TOCTitle: 'Lista de verificação: Atualização do Exchange 2007'
ms:assetid: 53aaa370-4562-43e4-9b75-7a705400c5a5
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff805032(v=EXCHG.150)
ms:contentKeyID: 51407877
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lista de verificação: Atualização do Exchange 2007

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Use essa lista de verificação para atualizar do Microsoft Exchange Server 2007 para o Exchange Server 2013. Antes de começar a trabalhar com essa lista de verificação, verifique se você está familiarizado com os conceitos discutidos em:

  - [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Novidades do Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md)

Esta lista de verificação é genérica, fornecendo orientações para um cenário de atualização típico.


> [!TIP]
> O Assistente de Implantação do Exchange Server oferece orientação personalizada passo a passo sobre como implantar o Exchange Server. O Assistente de Implantação pode ajudar a implantar uma nova instalação do Exchange Server 2013, atualizar uma versão anterior para o Exchange 2013 ou configurar uma implantação híbrida do Exchange 2013 e do Exchange Online. Para saber mais, confira <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente de implantação do Exchange Server</A>.



## Lista de verificação para atualização do Exchange 2007 para o Exchange 2013


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
<td><p>1. Ler as notas de versão</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Notas de versão do Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. Verificar os requisitos do sistema</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos de sistema do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. Confirmar se as etapas de pré-requisitos foram realizadas</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</a></p>
<p><a href="deployment-security-checklist-exchange-2013-help.md">Lista de verificação de segurança de implantação</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. Configurar o namespace separado</p>

> [!TIP]
> Esta etapa é opcional. É necessária apenas se a sua organização estiver executando um namespace separado.


</td>
<td><p><a href="configure-the-dns-suffix-search-list-for-a-disjoint-namespace-exchange-2013-help.md">Configurar a lista de pesquisa de sufixo DNS para um namespace separado</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>5. Selecionar um catálogo de endereços offline para todos os bancos de dados de caixa de correio do Exchange 2007</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/?linkid=320546">Downloads de como provisionar destinatários para o catálogo de Endereços Offline</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>6. Criar um nome de host do Exchange herdado</p></td>
<td><p><a href="https://technet.microsoft.com/pt-br/library/dn130105(v=exchg.150)">Criar um nome de host do Exchange herdado</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>7. Instalar o Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar o Exchange 2013 usando o Assistente para Configuração</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Instalar a função de Transporte de Borda do Exchange 2013 usando o Assistente para Configuração</a></p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Verificar uma instalação do Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Criar uma caixa de correio do Exchange 2013</p></td>
<td><p><a href="create-user-mailboxes-exchange-2013-help.md">Criar caixas de correio do usuário</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Configurar diretórios virtuais relacionados ao Exchange</p>

> [!TIP]
> Essa etapa será necessária se você quiser usar Serviços Web do Exchange, o Outlook em Qualquer Lugar ou o catálogo de endereços offline. Ela também poderá ser necessária se você precisar alterar qualquer uma das configurações padrão para Painel de Controle do Exchange, Microsoft Office&nbsp;Outlook Web App ou Exchange ActiveSync.<BR>


<p></p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuração do servidor de Acesso para Cliente do Exchange 2013</a></p>
<p></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>10. Configurar certificados do Exchange 2013</p></td>
<td><p><a href="digital-certificates-and-ssl-exchange-2013-help.md">Certificados digitais e SSL</a></p>
<p></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configurar certificados do Exchange 2007</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/?linkid=320553">Gerenciando SSL para um servidor de acesso do cliente</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>12. Configurar o servidor de Transporte de Borda</p>

> [!TIP]
> Esta etapa é opcional. Só será necessário se sua organização utilizar um servidor de Transporte de Borda.


</td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">Configurar o fluxo de mensagens da Internet por meio de um servidor de Transporte de Borda inscrito</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>13. Configurar a Unificação de Mensagens</p>

> [!TIP]
> Esta etapa é opcional. É necessária apenas se você quiser usar a Unificação de Mensagens na sua organização.


</td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">Planejamento para o Unified Messaging</a></p>
<p><a href="deploy-exchange-2013-um-exchange-2013-help.md">Implementar o UM do Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>14. Habilitar e configurar o Outlook Anywhere</p></td>
<td><p><a href="outlook-anywhere-exchange-2013-help.md">Outlook em Qualquer Lugar</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Configurar um ponto de conexão do serviço</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuração do servidor de Acesso para Cliente do Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>16. Configurar URLs do Exchange 2007</p></td>
<td><p><a href="https://technet.microsoft.com/pt-br/library/dn282262(v=exchg.150)">Configurar URLs externas do Exchange 2007</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>17. Configurar registros DNS</p></td>
<td><p><a href="https://technet.microsoft.com/pt-br/library/dn283988(v=exchg.150)">Configurar os registros de DNS para a instalação de múltiplos servidores do Exchange 2007</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>18. Mover as caixas de correio do Exchange 2007 para o Exchange 2013</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Movimentações de caixa de correio no Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>19. Mover dados de pastas públicas do Exchange 2013 para o Exchange 2013</p>

> [!TIP]
> Esta etapa é opcional. É necessária apenas se sua organização utiliza pastas públicas.


</td>
<td><p><a href="public-folders-exchange-2013-help.md">Pastas públicas</a></p>
<p><a href="https://technet.microsoft.com/pt-br/library/jj150486(v=exchg.150)">Use serial migração para migrar pastas públicas para o Exchange 2013 de versões anteriores</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>20. Tarefas pós-instalação</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Tarefas de pós-instalação do Exchange 2013</a></p></td>
</tr>
</tbody>
</table>

