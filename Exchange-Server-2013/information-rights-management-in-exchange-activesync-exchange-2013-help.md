---
title: 'Gerenciamento de direitos de info no Exchange ActiveSync: Exchange 2013 Help'
TOCTitle: Gerenciamento de direitos de informação no Exchange ActiveSync
ms:assetid: ebf04460-4d61-4b00-86b9-85ec1dbbd6a1
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ff657743(v=EXCHG.150)
ms:contentKeyID: 50486948
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Gerenciamento de direitos de informação no Exchange ActiveSync

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Os operadores de informações costumam usar o email para trocar informações confidenciais. Para ajudar a proteger essas informações, as organizações podem usar o Gerenciamento de Direitos de Informação (IRM) para aplicar proteção persistente a conteúdo de mensagens. Como dispositivos móveis estão sendo cada vez mais usados para acessar email, é importante que os usuários de dispositivo móvel possam criar e consumir conteúdo protegido por IRM.

**Conteúdo**

Proteção de IRM Mobile no Exchange 2013

Requirements

Security

Enabling IRM in Exchange ActiveSync

Procurando tarefas de gerenciamento relacionadas ao IRM? Consulte [Procedimentos de gerenciamento de direitos de informação](information-rights-management-procedures-exchange-2013-help.md).

## Proteção de IRM Mobile no Exchange 2013

Em Exchange 2013, o IRM no Microsoft Exchange ActiveSync permite que os usuários acessem a funcionalidade avançada do IRM em qualquer dispositivo com suporte Exchange ActiveSync sem precisar configurar as permissões da AD RMS ou conecte o dispositivo a um computador e ativá-lo para IRM. Além disso, o dispositivo móvel não precisa estar executando o Windows. Exchange ActiveSync é licenciado pela Microsoft para fabricantes de dispositivos móveis, fabricantes originais dos equipamentos (OEMs) e outros. Para obter uma lista de licenciados de Exchange ActiveSync atual, expanda a seção de "Protocolo ActiveSync do Exchange" na página [Licenciamento de tecnologia da Microsoft](https://go.microsoft.com/fwlink/p/?linkid=198562) .

Os seguintes requisitos se aplicam:

  - Os servidores Acesso do Cliente na organização devem estar executando o UNRESOLVED\_TOKEN\_VAL(exExchange2010) SP1 ou mais recente.

  - Um servidor AD RMS deve estar implantado na organização.

  - O IRM deve estar habilitado para mensagens internas. Trata-se de um pré-requisito para todos os recursos do IRM no UNRESOLVED\_TOKEN\_VAL(exExchange2010). Para detalhes, consulte [Habilitar ou desabilitar o IRM para mensagens internas](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

O IRM deve estar habilitado na política de caixa de correio do Exchange ActiveSync. É possível habilitar ou desabilitar o IRM para conjuntos diferentes de usuários usando políticas de caixa de correio do Exchange ActiveSync diferentes.

## Requisitos

Voltar ao início

  - Os servidores de acesso para cliente em sua organização devem estar executando o Exchange 2010 SP1 ou posterior.

  - Quando você habilita o IRM no Exchange ActiveSync, o servidor Acesso do Cliente descriptografa mensagens protegidas por IRM antes de fornecer às mensagens o acesso pelo dispositivo móvel com suporte. Mediante a sincronização, as mensagens protegidas pelo IRM residem no dispositivo móvel em um formato descriptografado. A proteção do IRM é aplicada pelo aplicativo cliente de email compatível com IRM no dispositivo móvel.

  - IRM deve ser habilitado para mensagens internas. Este é um pré-requisito para todos os recursos IRM em Exchange 2010. Para obter detalhes, consulte [Habilitar ou desabilitar o IRM para mensagens internas](enable-or-disable-irm-for-internal-messages-exchange-2013-help.md).

  - Ao habilitar o IRM no Exchange ActiveSync, recomendamos usar as configurações de política do Exchange ActiveSync mostradas na tabela a seguir para ajudar a proteger dispositivos móveis.

  - Dispositivos que suportam Exchange ActiveSync protocol versão 14.1, incluindo telefones Windows, podem oferecer suporte para IRM no Exchange ActiveSync. Aplicativo de email móvel do dispositivo deve oferecer suporte a marca RightsManagementInformation definida na versão Exchange ActiveSync 14.1.

Configuração

## Segurança

Configurar usando o cmdlet New-ActiveSyncMailboxPolicy

IRM no Exchange ActiveSync não descriptografa anexos protegidos por IRM no servidor de acesso para cliente. Acesso aos arquivos protegidos por IRM é imposto pelo aplicativo utilizado para criar ou exibir o arquivo. Por exemplo, em um telefone de Windows, a proteção de IRM para arquivos do Microsoft Office é imposta pela [Microsoft Office Mobile](https://go.microsoft.com/fwlink/p/?linkid=205121). Para acessar arquivos protegidos por IRM Office, os usuários devem conecte o dispositivo em um computador e ativar Office Mobile com o servidor RMS.

Marque a caixa de seleção **Requerer senha**.

### Configurações de diretiva do Exchange ActiveSync

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Habilite a criptografia no dispositivo móvel.</th>
<th>Marque a caixa de seleção <strong>Requerer senha</strong> e selecione <strong>Exigir criptografia no dispositivo</strong>.</th>
<th>Defina o parâmetro <em>RequireDeviceEncryption</em> como <code>$true</code>.</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Quando você definir o parâmetro <em>RequireDeviceEncryption</em> como <code>$true</code>, os dispositivos móveis sem suporte à criptografia de dispositivo não poderão se conectar.</p></td>
<td><p>Não permita que dispositivos móveis não provisionáveis sejam sincronizados com o servidor do Exchange.</p></td>
<td><p>Desmarque a caixa de seleção <strong>Permitir dispositivos não configuráveis</strong>.</p></td>
</tr>
<tr class="even">
<td><p>Defina o parâmetro <em>AllowNonProvisionableDevices</em> como <code>$false</code>.</p></td>
<td><p>Para obter mais informações, consulte <a href="mobile-device-mailbox-policies-exchange-2013-help.md">Políticas de caixa de correio para dispositivos móveis</a>.</p></td>
<td><p>Defina o parâmetro de <em>RequireDeviceEncryption</em> para <code>$true</code>.</p>

> [!IMPORTANT]
> Quando você definir o parâmetro <EM>RequireDeviceEncryption</EM> como <CODE>$true</CODE>, dispositivos móveis que não oferecem suporte para criptografia de dispositivo não poderão se conectar.


</td>
</tr>
<tr class="odd">
<td><p>Para habilitar o IRM no Exchange ActiveSync, realize as seguintes tarefas:</p></td>
<td><p>Adicione a caixa de correio Federação (uma caixa de correio do sistema criada pela Instalação do Exchange 2013 e UNRESOLVED_TOKEN_VAL(exExchange2010)) ao grupo de superusuários no AD RMS. Isso permite aos servidores Exchange 2013 e UNRESOLVED_TOKEN_VAL(exExchange2010) acessar mensagens protegidas por IRM. Para detalhes, consulte <a href="add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md">Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super</a>.</p></td>
<td><p>Use o cmdlet <a href="https://technet.microsoft.com/pt-br/library/dd979792(v=exchg.150)">Set-IRMConfiguration</a> no Shell de Gerenciamento do Exchange para habilitar o IRM no servidor Acesso do Cliente. Isso habilita o IRM no Exchange ActiveSync e o IRM no Microsoft OfficeOutlook Web App para a organização. Para detalhes, consulte <a href="enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md">Habilitar ou desabilitar o gerenciamento de direitos de informação nos servidores de acesso do cliente</a>.</p></td>
</tr>
</tbody>
</table>


Para obter mais informações, consulte [Políticas de caixa de correio para dispositivos móveis](mobile-device-mailbox-policies-exchange-2013-help.md).

Voltar ao início

## Habilitar o IRM no Exchange ActiveSync

Para habilitar o IRM no Exchange ActiveSync, execute as seguintes tarefas:

1.  Adicione a caixa de correio de Federação (uma caixa de correio sistema criada pelo Exchange 2013 e Exchange 2010 instalação) para o grupo de superusuários no AD RMS. Isso permite que os servidores de Exchange 2013 e Exchange 2010 acessar mensagens protegidas por IRM. Para obter detalhes, consulte [Adicionar a caixa de correio de Federação ao grupo de usuários do AD RMS Super](add-the-federation-mailbox-to-the-ad-rms-super-users-group-exchange-2013-help.md).

2.  Use o cmdlet de [Set-IRMConfiguration](https://technet.microsoft.com/pt-br/library/dd979792\(v=exchg.150\)) em Exchange Management Shell para habilitar o IRM no servidor de acesso para cliente. Isso habilita o IRM no Exchange ActiveSync e o IRM no Microsoft OfficeOutlook Web App para sua organização. Para obter informações detalhadas, consulte [Habilitar ou desabilitar o gerenciamento de direitos de informação nos servidores de acesso do cliente](enable-or-disable-information-rights-management-on-client-access-servers-exchange-2013-help.md).

Voltar ao início

