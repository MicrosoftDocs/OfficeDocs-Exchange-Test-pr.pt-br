---
title: 'Atualização do Exchange 2007 para o Exchange 2013: Exchange 2013 Help'
TOCTitle: Atualização do Exchange 2007 para o Exchange 2013
ms:assetid: a604b96d-2a51-480f-937f-45ad753c2cad
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ898581(v=EXCHG.150)
ms:contentKeyID: 51407892
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Atualização do Exchange 2007 para o Exchange 2013

 

_**Aplica-se a:** Exchange Online, Exchange Server, Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

O Microsoft Exchange Server 2010 e o Exchange Server 2007 têm múltiplas funções de servidor: Acesso para Cliente, Caixa de Correio, Transporte de Hub, Unificação de Mensagens e Transporte de Borda. Com o Exchange Server 2013, reduzimos a quantidade de funções de servidor de cinco para três: Acesso para Cliente, Caixa de Correio e Transporte de Borda. A Unificação de Mensagens agora é considerada um componente ou sub-recurso dos recursos relacionados à voz oferecidos no Exchange 2013. (Para obter mais detalhes sobre as alterações, consulte \&quot;Arquitetura do Exchange 2013 \&quot; em [Novidades do Exchange 2013](what-s-new-in-exchange-2013-exchange-2013-help.md).)

Quando você está atualizando sua organização do Exchange 2007 existente para Exchange 2013, há um período em que servidores do Exchange 2007 e do Exchange 2013 coexistirão dentro de sua organização. É possível manter este modo por um período de tempo indefinido ou concluir imediatamente a atualização para o Exchange 2013 movendo todos os recursos do Exchange 2007 para o Exchange 2013, e, em seguida, descomissionando os servidores Exchange 2007 . Você terá um cenário de coexistência se as seguintes condições forem verdadeiras:

  - O Exchange 2013 está implantado em uma organização existente do Exchange.

  - Mais de uma versão do Microsoft Exchange fornece serviços de mensagens à organização.

Não é possível atualizar uma organização existente do Exchange 2003 diretamente para o 2013. Primeiro, é necessário atualizar a organização do Exchange 2003 para uma organização do Exchange 2007 ou do Exchange 2010 e, em seguida, atualizar essa organização do Exchange 2007 ou do Exchange 2010 para o Exchange 2013. Convém atualizar a organização do Exchange 2003 para o Exchange 2010 e depois atualizar do Exchange 2010 para o Exchange 2013.


> [!WARNING]
> É necessário remover todas as instâncias do Exchange 2003 da organização antes de poder atualizar para o Exchange 2013.



Você pode migrar todas as suas caixas de correio do Exchange 2003 para o Exchange Online. Para saber mais sobre essa abordagem, confira [Maneiras de migrar várias contas de email para o Office 365](https://go.microsoft.com/fwlink/p/?linkid=524030).

A tabela a seguir lista os cenários em que a há suporte para a coexistência entre o Exchange 2013 e versões anteriores do Exchange.

### Coexistência de versões anteriores do Exchange Server e o Exchange 2013

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Versão do Exchange</th>
<th>Coexistência da organização do Exchange</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Exchange Server 2003 e versões anteriores</p></td>
<td><p>Sem suporte</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2007</p></td>
<td><p>Compatível com as seguintes versões mínimas do Exchange:</p>
<ul>
<li><p>1Pacote cumulativo de atualizações 10 do Exchange 2007 Service Pack 3 (SP3) em todos os servidores Exchange 2007 da organização, inclusive nos servidores de Transporte de Borda.</p></li>
<li><p>Atualização Cumulativa 2 (CU2) ou posterior do Exchange 2013 em todos os servidores Exchange 2013 da organização.</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>Exchange 2010</p></td>
<td><p>Compatível com as seguintes versões mínimas do Exchange:</p>
<ul>
<li><p>2 Exchange 2010 SP3 em todos os servidores Exchange 2010, inclusive nos servidores de Transporte de Borda.</p></li>
<li><p>CU2 ou posterior do Exchange 2013 em todos os servidores Exchange 2013 da organização.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Organização mista do Exchange 2010 e do Exchange 2007</p></td>
<td><p>Compatível com as seguintes versões mínimas do Exchange:</p>
<ul>
<li><p>1Pacote cumulativo de atualizações 10 do Exchange 2007 SP3 em todos os servidores Exchange 2007 da organização, inclusive nos servidores de Transporte de Borda.</p></li>
<li><p>2 Exchange 2010 SP3 em todos os servidores Exchange 2010, inclusive nos servidores de Transporte de Borda.</p></li>
<li><p>CU2 ou posterior do Exchange 2013 em todos os servidores Exchange 2013 da organização.</p></li>
</ul></td>
</tr>
</tbody>
</table>


1   Para criar uma inscrição do EdgeSync entre um servidor de Transporte de Hub do Exchange 2007 e um servidor de Transporte de Borda do Exchange 2013 SP1, você deve instalar o pacote cumulativo de atualizações 13 do Exchange 2007 SP3 ou posterior no servidor de Transporte de Hub do Exchange 2007.

2   Para criar uma inscrição do EdgeSync entre um servidor de Transporte de Hub do Exchange 2010 e um servidor de Transporte de Borda do Exchange 2013 SP1, você deve instalar o pacote cumulativo de atualizações 5 do Exchange 2010 SP3 ou posterior no servidor de Transporte de Hub do Exchange 2010.

## Coexistência de modo misto do Exchange 2013 e do Exchange 2007 com o Exchange 2010

Se possuir sites do Active Directory com tanto o Exchange 2010 quanto o Exchange 2007 instalados, siga as instruções de atualização do Exchange 2010 e doExchange 2007, e execute as etapas de atualização necessárias para ambos.

## Visão geral do processo de atualização

Para ajudá-lo a obter uma visão geral do processo de atualização do Exchange 2007 para o Exchange 2013, reunimos recursos relacionados a cada tarefa principal na tabela a seguir. Para obter as instruções específicas passo a passo, consulte [Lista de verificação: Atualização do Exchange 2007](checklist-upgrade-from-exchange-2007-exchange-2013-help.md).


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tarefa</th>
<th>Tópico</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Saiba mais sobre os componentes e funções do Exchange 2013.</p></td>
<td><p><a href="what-s-new-in-exchange-2013-exchange-2013-help.md">Novidades do Exchange 2013</a></p>
<p><a href="client-access-server-exchange-2013-help.md">Servidor de Acesso para Cliente</a></p>
<p><a href="mailbox-server-exchange-2013-help.md">Servidor de Caixa de Correio</a></p>
<p><a href="mail-flow-exchange-2013-help.md">Fluxo de mensagens</a></p>
<p><a href="unified-messaging-exchange-2013-help.md">Unificação de mensagens</a></p></td>
</tr>
<tr class="even">
<td><p>Instalação do Exchange 2013</p></td>
<td><p><a href="install-exchange-2013-using-the-setup-wizard-exchange-2013-help.md">Instalar o Exchange 2013 usando o Assistente para Configuração</a></p>
<p><a href="install-the-exchange-2013-edge-transport-role-using-the-setup-wizard-exchange-2013-help.md">Instalar a função de Transporte de Borda do Exchange 2013 usando o Assistente para Configuração</a> (opcional)</p>
<p><a href="verify-an-exchange-2013-installation-exchange-2013-help.md">Verificar uma instalação do Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Adicionar certificados digitais no servidor de Acesso para Cliente</p></td>
<td><p><a href="exchange-2013-client-access-server-configuration-exchange-2013-help.md">Configuração do servidor de Acesso para Cliente do Exchange 2013</a></p>
<p><a href="digital-certificates-and-ssl-exchange-2013-help.md">Certificados digitais e SSL</a></p>
<p><a href="create-a-digital-certificate-request-exchange-2013-help.md">Criar uma solicitação de certificado digital</a></p></td>
</tr>
<tr class="even">
<td><p>Configurar os diretórios virtuais relacionados ao Exchange</p></td>
<td><p><a href="default-settings-for-exchange-virtual-directories-exchange-2013-help.md">Configurações padrão para os diretórios virtuais do Exchange</a></p></td>
</tr>
<tr class="odd">
<td><p>Mover caixas de correio do Exchange 2010</p></td>
<td><p><a href="mailbox-moves-in-exchange-2013-exchange-2013-help.md">Movimentações de caixa de correio no Exchange 2013</a></p></td>
</tr>
<tr class="even">
<td><p>Configurar regras de transporte</p></td>
<td><p><a href="edge-subscriptions-exchange-2013-help.md">Inscrições de Borda</a> (só é necessário se você tiver instalado um servidor de Transporte de Borda)</p>
<p><a href="mail-routing-exchange-2013-help.md">Roteamento de mensagens</a></p>
<p><a href="shadow-redundancy-exchange-2013-help.md">Redundância de sombra</a></p>
<p><a href="delivery-reports-for-administrators-exchange-2013-help.md">Notificações de entrega para administradores</a></p></td>
</tr>
<tr class="odd">
<td><p>Configurar e implantar UM</p></td>
<td><p><a href="planning-for-unified-messaging-exchange-2013-help.md">Planejamento para o Unified Messaging</a></p>
<p><a href="deploying-voice-mail-and-um-exchange-2013-help.md">Implantando a caixa postal e Unificação de MENSAGENS</a></p></td>
</tr>
</tbody>
</table>

