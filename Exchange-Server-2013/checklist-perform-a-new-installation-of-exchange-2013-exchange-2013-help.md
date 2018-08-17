---
title: 'Lista de verificação: executar uma nova instalação do Exchange 2013'
TOCTitle: 'Lista de verificação: Executar uma nova instalação do Exchange 2013'
ms:assetid: f70d9dd3-7370-472e-b05e-1ea1671272b2
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff805042(v=EXCHG.150)
ms:contentKeyID: 50487036
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lista de verificação: Executar uma nova instalação do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

Use esta lista de verificação para implantar o Microsoft Exchange Server 2013. Antes de começar a trabalhar com essa lista de verificação, verifique se está familiarizado com os conceitos discutidos em:

  - [Planejamento e implantação](planning-and-deployment-for-exchange-2013-installation-instructions.md)

  - [Lista de verificação de segurança de implantação](deployment-security-checklist-exchange-2013-help.md)

Essa lista de verificação é genérica por fornecer orientação para um cenário comum.


> [!NOTE]  
> O Assistente de Implantação do Exchange Server oferece orientação personalizada passo a passo sobre como implantar o Exchange Server. O Assistente de Implantação pode ajudar a implantar uma nova instalação do Exchange Server 2013, atualizar uma versão anterior para o Exchange 2013 ou configurar uma implantação híbrida do Exchange 2013 e do Exchange Online. Para saber mais, confira <A href="exchange-server-deployment-assistant-exchange-2013-help.md">Assistente de implantação do Exchange Server</A>.



## Lista de verificação para uma nova instalação do Exchange 2013


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
<td><p>Tópico</p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>1. Ler as notas de versão</p></td>
<td><p><a href="release-notes-for-exchange-2013-exchange-2013-help.md">Notas de versão do Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>2. Verifique os requisitos do sistema.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos de sistema do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>3. Confirme se as etapas de pré-requisitos estão concluídas.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>4. Configure o namespace não contíguo.</p>

> [!NOTE]  
> Esta etapa é opcional. É necessária apenas se sua organização estiver executando um namespace separado.


</td>
<td><p><a href="disjoint-namespace-scenarios-exchange-2013-help.md">Cenários de namespace separado</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>5. Instale a função de servidor de Caixa de Correio.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar o Exchange 2013 usando o Assistente para Configuração</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>6. Instale a função de servidor de Acesso para Cliente.</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar o Exchange 2013 usando o Assistente para Configuração</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>7. Instale a função de servidor Transporte de Borda.</p>

> [!NOTE]  
> Esta etapa é opcional. Será necessária apenas se você quiser instalar um servidor de Transporte de Borda. Para obter mais informações, consulte <A href="edge-transport-servers-exchange-2013-help.md">Servidores de Transporte de Borda</A>.


</td>
<td><p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Instalar a função de Transporte de Borda do Exchange 2013 usando o Assistente para Configuração</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>8. Crie uma inscrição do EdgeSync.</p>
<p>Esta etapa é opcional. Será necessária apenas se você tiver instalado um servidor de Transporte de Borda e quiser configurar uma inscrição do EdgeSync entre seu servidor de Transporte de Borda e um servidor de Transporte de Hub. Para obter mais informações, consulte <a href="edge-subscriptions-exchange-2013-help.md">Inscrições de Borda</a>.</p></td>
<td><p><a href="configure-internet-mail-flow-through-a-subscribed-edge-transport-server-exchange-2013-help.md">Configurar o fluxo de mensagens da Internet por meio de um servidor de Transporte de Borda inscrito</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>9. Configure o Transporte.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 1: Create a Send connector</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>10. Adicione os domínios adicionais aceitos.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 2: Add additional accepted domains</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>11. Configure políticas de endereço de email.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 3: Configure the default email address policy</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>12. Configure definições em diretórios virtuais, incluindo o catálogo de endereços offline, os Serviços da Web do Exchange, o Centro de Administração do Exchange (EAC), o Outlook Web App e diretórios virtuais do Exchange ActiveSync.</p>

> [!NOTE]  
> Essa etapa será necessária se você quiser usar Serviços Web do Exchange, o Outlook em Qualquer Lugar ou o catálogo de endereços offline. Isso também pode ser necessário caso seja preciso alterar qualquer uma das configurações padrão para EAC, Outlook Web App ou Exchange ActiveSync.


</td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 4: Configure external URLs</a></p>
<p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 5: Configure internal URLs</a></p></td>
</tr>
<tr class="even">
<td> </td>
<td><p>13. Adicione certificados digitais no servidor de Acesso para Cliente.</p></td>
<td><p><a href="configure-mail-flow-and-client-access-exchange-2013-help.md">Step 6: Configure an SSL certificate</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>14. Configure a Unificação de Mensagens.</p>

> [!NOTE]  
> Esta etapa é opcional. É necessária apenas se desejar usar Unificação de Mensagens em sua organização.


</td>
<td><p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Implantando a caixa postal e Unificação de MENSAGENS</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>15. Configure as opções adicionais da Unificação de Mensagens e do Lync Server.</p>

> [!NOTE]  
> Esta etapa é opcional. Só é necessário se você tiver configurado a Unificação de Mensagens em sua organização e quiser integrá-la ao Lync Server.


</td>
<td><p><a href="deploying-exchange-2013-um-and-lync-server-overview-exchange-2013-help.md">Implantando a visão geral da Unificação de MENSAGENS do Exchange 2013 e Lync Server</a></p></td>
</tr>
<tr class="odd">
<td> </td>
<td><p>16. Tarefas pós-instalação.</p></td>
<td><p><a href="exchange-2013-post-installation-tasks-exchange-2013-help.md">Tarefas de pós-instalação do Exchange 2013</a></p></td>
</tr>
</tbody>
</table>

