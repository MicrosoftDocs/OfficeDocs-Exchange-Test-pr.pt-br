---
title: 'Lista de verificação: Implementar o UM do Exchange 2013: Exchange 2013 Help'
TOCTitle: 'Lista de verificação: Implementar o UM do Exchange 2013'
ms:assetid: 41b666a2-0d0d-471f-90a3-07c3c562af85
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ673520(v=EXCHG.150)
ms:contentKeyID: 52058814
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Lista de verificação: Implementar o UM do Exchange 2013

 

_**Aplica-se a:** Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:** 2015-03-09_

Use esta lista de verificação para instalar e implantar a Unificação de Mensagens (UM) em sua organização.

Antes de começar a trabalhar com essa lista de verificação, certifique-se de estar familiarizado com os conceitos em:

  - [Unificação de mensagens](unified-messaging-exchange-2013-help.md)

  - [Novos recursos de caixa postal](new-voice-mail-features-exchange-2013-help.md)

  - [Planejamento para o Unified Messaging](planning-for-unified-messaging-exchange-2013-help.md)

Para obter orientação passo a passo sobre como implantar a UM e o Microsoft Lync Server, consulte [Lista de verificação: Integrar o UM do Exchange 2013 com o Lync Server](checklist-integrate-exchange-2013-um-with-lync-server-exchange-2013-help.md).

## Lista de verificação para implantação da Unificação de Mensagens


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
<td><p> </p></td>
<td><p>Verifique se você atende aos pré-requisitos para instalação.</p></td>
<td><p><a href="exchange-2013-prerequisites-exchange-2013-help.md">Pré-requisitos do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p><strong> </strong></p></td>
<td><p>Instale os servidores de Acesso para Cliente e de Caixa de Correio necessários.</p>

> [!WARNING]
> Você deve implantar pelo menos um servidor de Caixa de Correio do Exchange 2013 em sua organização antes de configurar os gateways VoIP ou PBXs IP para enviar tráfego SIP e RTP UM para os servidores de Acesso para Cliente do Exchange 2013.


</td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar o Exchange 2013 usando o Assistente para Configuração</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Verifique a instalação e examine os logs de configuração do servidor.</p></td>
<td><p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Verificar uma instalação do Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Se necessário, instale os pacotes de idiomas da UM necessários.</p></td>
<td><p><a href="install-a-um-language-pack-exchange-2013-help.md">Instalar um pacote de idiomas para UM</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Crie o número de planos de discagem necessários para sua organização.</p></td>
<td><p><a href="create-a-um-dial-plan-exchange-2013-help.md">Criar um plano de discagem de UM</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Defina a configuração de segurança do plano de discagem.</p></td>
<td><p><a href="configure-the-voip-security-setting-exchange-2013-help.md">Definir a configuração de segurança de VoIP</a></p></td>
</tr>
<tr class="odd">
<td><p> </p></td>
<td><p>Configure o modo de inicialização da UM para cada servidor de Acesso para Cliente e de Caixa de Correio.</p></td>
<td><p><a href="configure-the-startup-mode-on-a-mailbox-server-exchange-2013-help.md">Configurar o modo de inicialização em um servidor de caixa de correio</a></p>
<p><a href="configure-the-startup-mode-on-a-client-access-server-exchange-2013-help.md">Configurar o modo de inicialização em um servidor de acesso para cliente</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure o número de chamadas concorrentes em seus servidores de Caixa de Correio.</p></td>
<td><p><a href="configure-the-number-of-incoming-calls-on-a-mailbox-server-exchange-2013-help.md">Configurar o número de chamadas de entrada em um servidor de caixa de correio</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Configure números do Outlook Voice Access e outras configurações.</p></td>
<td><p><a href="manage-a-um-dial-plan-exchange-2013-help.md">Gerenciar um plano de discagem de Unificação de mensagens</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure a discagem de saída para Unificação de Mensagens.</p></td>
<td><p><a href="authorize-calls-using-dialing-rules-exchange-2013-help.md">Autorizar chamadas usando regras de discagem</a></p>
<p><a href="authorize-calls-for-users-in-a-dial-plan-exchange-2013-help.md">Autorizar chamadas para usuários em um plano de discagem</a></p>
<p><a href="authorize-calls-for-a-group-of-users-exchange-2013-help.md">Autorizar chamadas para um grupo de usuários</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Criar o número necessário de atendedores automáticos.</p></td>
<td><p><a href="create-a-um-auto-attendant-exchange-2013-help.md">Criar um Atendedor Automático da UM</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure cada um dos atendedores automáticos da UM.</p></td>
<td><p><a href="set-up-a-um-auto-attendant-exchange-2013-help.md">Configurar um atendedor automático</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Crie, importe e habilite um novo certificado do Exchange para UM ou habilite um certificado de terceiros mutuamente confiável. Além disso, importe o certificado em todos os gateways VoIP; PBXs IP e SBCs.</p></td>
<td><p><a href="add-mailbox-and-client-access-servers-to-a-sip-uri-dial-plan-exchange-2013-help.md">Adicionar servidores de acesso para cliente e caixa de correio a um plano de discagem URI do SIP</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Reinicie o serviço Unificação de mensagens do Microsoft Exchange e o serviço Roteador de Chamadas da Unificação de Mensagens em todos os Exchange Servers para carregar os certificados necessários.</p></td>
<td><p><a href="stop-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Pare o serviço de Unificação de mensagens do Microsoft Exchange</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-service-exchange-2013-help.md">Iniciar o serviço de Unificação de mensagens do Microsoft Exchange</a></p>
<p><a href="stop-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Pare o serviço Microsoft Exchange Unified Messaging roteador de chamadas</a></p>
<p><a href="start-the-microsoft-exchange-unified-messaging-call-router-service-exchange-2013-help.md">Iniciar o serviço Microsoft Exchange Unified Messaging roteador de chamadas</a></p></td>
</tr>
<tr class="odd">
<td><p><strong> </strong></p></td>
<td><p>Crie uma política de caixa de correio da UM ou configure a política de caixa de correio da UM padrão.</p></td>
<td><p><a href="create-a-um-mailbox-policy-exchange-2013-help.md">Criar uma política de caixa de correio da UM</a></p>
<p><a href="manage-a-um-mailbox-policy-exchange-2013-help.md">Gerenciar uma política de caixa de correio de Unificação de mensagens</a></p></td>
</tr>
<tr class="even">
<td><p> </p></td>
<td><p>Habilite usuários para a Unificação de Mensagens com um número de ramal e um número E.164, se necessário.</p></td>
<td><p><a href="enable-a-user-for-voice-mail-exchange-2013-help.md">Habilitar um usuário para caixa postal</a></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Habilite os faxes de entrada (Opcional).</p></td>
<td><p><a href="enable-voice-mail-users-to-receive-faxes-exchange-2013-help.md">Permitir que os usuários de email de voz receber faxes</a></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Configure a caixa postal protegida (Opcional).</p></td>
<td><p><a href="protect-voice-mail-exchange-2013-help.md">Caixa postal protegida</a></p></td>
</tr>
</tbody>
</table>


Voltar ao início

