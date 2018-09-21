---
title: 'Lista de verificação: atualizar UM do Exchange 2010 para UM do Exchange 2013'
TOCTitle: 'Lista de verificação: Atualizar a UM do Exchange 2010 para a UM do Exchange 2013'
ms:assetid: 799bd1b1-a918-4bd8-911e-e6ca08bd7b52
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn169228(v=EXCHG.150)
ms:contentKeyID: 54651974
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lista de verificação: Atualizar a UM do Exchange 2010 para a UM do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2016-12-09_

Use esta lista de verificação para ajudar você a atualizar da Unificação de Mensagens (UM) do Exchange 2010 para a UM do Exchange 2013. Consulte estas informações quando estiver atualizando sua organização do Exchange 2010 e sua implantação de UM para o Exchange 2013. Para ver instruções passo a passo de atualização para a UM do Exchange 2013, consulte [Atualizar UM do Exchange 2010 para UM do Exchange 2013](upgrade-exchange-2010-um-to-exchange-2013-um-exchange-2013-help.md).

Antes de começar a trabalhar com essa lista de verificação, certifique-se de estar familiarizado com os conceitos em:

  - [Planejamento para o Unified Messaging](planning-for-unified-messaging-exchange-2013-help.md)

  - [Integração com a Unificação de MENSAGENS do sistema de telefone](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/telephone-system-integration-with-um)

  - [Conectar seu sistema de caixa postal à sua rede de telefone](https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/connect-voice-mail-system)

Para obter uma orientação passo a passo sobre como atualizar do Exchange 2007 UM para o Exchange 2013 UM, veja [Atualizar UM do Exchange 2007 para o UM do Exchange 2013](upgrade-exchange-2007-um-to-exchange-2013-um-exchange-2013-help.md).

## Lista de verificação para atualizar a UM do Exchange 2010 para a UM do Exchange 2013


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Pronto?</th>
<th>Tarefas</th>
<th>Tópico</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p></p></td>
<td><p>Implantar e configurar componentes de telefonia.</p></td>
<td><p><a href="connect-um-to-your-telephone-system-exchange-2013-help.md">Conectar UM ao seu sistema telefônico</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Examine os requisitos de sistema antes de instalar o Exchange 2013.</p></td>
<td><p><a href="exchange-2013-system-requirements-exchange-2013-help.md">Requisitos de sistema do Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Verifique se você atende aos pré-requisitos para instalação.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Instale os servidores de Acesso para Cliente e de Caixa de Correio necessários.</p>

> [!WARNING]
> Você deve implantar pelo menos um servidor de correio do Exchange 2013 em sua organização antes de configurar os gateways VoIP ou PBXs IP para enviar SIP de UM e tráfego RTP aos servidores de acesso para cliente do Exchange 2013.


</td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar o Exchange 2013 usando o Assistente para Configuração</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Verifique a instalação e examine os logs de configuração do servidor.</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Verificar uma instalação do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Se necessário, instale os pacotes de idiomas da UM necessários.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">Instalar um pacote de idiomas para UM</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Mover a caixa de correio do sistema Exchange 2010 usada para os prompts personalizados de UM para o Exchange 2013.</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Movimentações de caixa de correio no Exchange 2013</a></p>

> [!NOTE]
> Se a caixa de correio do sistema já tiver sido mudada, você ainda pode importar/exportar manualmente prompts personalizados do Exchange 2010 usando <A href="import-and-export-custom-greetings-announcements-menus-and-prompts-exchange-2013-help.md">Importar e exportar saudações personalizadas, anúncios, menus e prompts</A>.


</td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Exportar e importar certificados.</p></td>
<td><p><a href="deploying-certificates-for-um-exchange-2013-help.md">Implantar certificados para Unificação de mensagens</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configurar o modo de inicialização de UM em todos os servidores de Acesso para Cliente Exchange 2013.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurar o modo de inicialização em um servidor de acesso para cliente</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurar o modo de inicialização de UM em todos os servidores de Caixa de Correio Exchange 2013.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configurar o modo de inicialização em um servidor de caixa de correio</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Criar ou configurar planos de discagem de UM existentes.</p></td>
<td><p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-dial-plan">Criar um plano de discagem de UM</a></p>
<p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/manage-um-dial-plan">Gerenciar um plano de discagem de Unificação de mensagens</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Criar ou configurar gateways IP de UM existentes.</p></td>
<td><p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-ip-gateway">Criar um gateway IP de UM</a></p>
<p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/manage-um-ip-gateway">Gerenciar um gateway IP de UM</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Criar um grupo de busca de UM.</p></td>
<td><p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/connect-voice-mail-system/create-um-hunt-group">Criar um grupo de busca de UM</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Criar ou configurar atendedores automáticos de UM.</p></td>
<td><p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/create-a-um-auto-attendant">Criar um Atendedor Automático da UM</a></p>
<p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/automatically-answer-and-route-calls/manage-um-auto-attendant">Gerenciar um atendedor automático</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Criar ou configurar políticas de caixa de correio de UM.</p></td>
<td><p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/create-um-mailbox-policy">Criar uma política de caixa de correio da UM</a></p>
<p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-um-mailbox-policy">Gerenciar uma política de caixa de correio de Unificação de mensagens</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Mover caixas de correio habilitadas para UM existentes para o Exchange 2013.</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Movimentações de caixa de correio no Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Habilitar novos usuários para UM ou definir configurações para um usuário habilitado para UM existente.</p></td>
<td><p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/enable-a-user-for-voice-mail">Habilitar um usuário para caixa postal</a></p>
<p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/set-up-voice-mail/manage-voice-mail-settings">Gerenciar configurações de caixa postal de um usuário</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configurar seus gateways VoIP, IP PBXs e PBXs habilitados para SIP para enviar todas as chamadas de entrada aos servidores de Acesso para Cliente Exchange 2013.</p></td>
<td><p><a href="https://docs.microsoft.com/pt-br/exchange/voice-mail-unified-messaging/telephone-system-integration-with-um/configuration-notes-for-voip-gateways">Notas de configuração para gateways VoIP com suporte, IP PBXs e PBXs</a> <a href="connect-a-voip-gateway-ip-pbx-or-session-border-controller-to-um-exchange-2013-help.md">Conectar a um controlador de borda de sessão, PBX IP ou gateway VoIP para Unificação de MENSAGENS</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Desabilitar o atendimento de chamada nos servidores de UM do Exchange 2010.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296335">Desabilitar a Unificação de mensagens no Exchange 2010</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Remover um servidor de UM do Exchange 2010 de um plano de discagem.</p></td>
<td><p><a href="https://go.microsoft.com/fwlink/p/?linkid=296336">Remover um servidor de Unificação de MENSAGENS de um plano de discagem</a></p></td>
</tr>
</tbody>
</table>

