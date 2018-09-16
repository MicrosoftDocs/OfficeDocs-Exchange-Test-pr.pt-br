---
title: 'Conformidade e política de sistema de mensagens: Exchange 2013 Help'
TOCTitle: Conformidade e política de sistema de mensagens
ms:assetid: 65f20a20-27a4-4f6e-9b27-f8705d65b8d9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Aa998599(v=EXCHG.150)
ms:contentKeyID: 50485859
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Conformidade e política de sistema de mensagens

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

O email se tornou um meio de comunicação confiável e onipresente para operadores de informações em organizações de todos os portes. As caixas de correio e os armazenamentos de mensagens se tornaram repositórios de dados valiosos. É importante que as organizações formulem políticas de mensagens que ditem o uso justo de seus sistemas de mensagens, ofereçam diretrizes aos usuários sobre como agir dentro das políticas e, onde necessário, forneçam detalhes sobre os tipos de comunicações que não devem ser permitidos.

As organizações também precisam criar políticas para gerenciar o ciclo de vida do email, reter mensagens pelo tempo necessário de acordo com os requisitos comerciais, legais e de regulamentação, preservar registros de email para fins de litígio e investigação e estar preparadas para pesquisar e fornecer os registros de email exigidos para atender às solicitações de descoberta eletrônica.

Também é preciso proteger-se do vazamento de informações confidenciais coletadas ou manipuladas por sua organização, como propriedade intelectual, segredos comerciais, planos de negócios e informações de identificação pessoal (PII).

## Política de mensagens e conformidade no Exchange 2013

A tabela abaixo apresenta uma visão geral dos recursos de conformidade e políticas de mensagens do Microsoft Exchange Server 2013 e inclui links para tópicos que vão ajudá-lo a saber mais sobre esses recursos e a gerenciá-los.


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Recurso</th>
<th>Descrição</th>
<th>Recursos</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento de registros de mensagens (MRM)</p></td>
<td><p>Para manter a conformidade com as normas aplicáveis e atender aos requisitos legais ou comerciais, as organizações usam políticas de ciclo de vida de email como parte de sua política de mensagens. Perguntas comuns que devem ser respondidas por essas políticas incluem:</p>
<ul>
<li><p>Por quanto tempo as mensagens devem ser mantidas?</p></li>
<li><p>Onde as mensagens devem ser guardadas?</p></li>
<li><p>Todas as mensagens devem ser mantidas pelo mesmo período?</p></li>
</ul>
<p>O Exchange 2013 inclui recursos de MRM que permitem que você implemente as políticas de ciclo de vida de email de sua organização. Você pode usar o MRM para aplicar configurações de retenção uniformes a todas as mensagens, usar políticas de retenção personalizadas para aplicar uma configuração de retenção de linha de base à caixa de correio e, se quiser, permitir que os usuários classifiquem as mensagens para que possam ser mantidas por uma duração específica.</p></td>
<td><p><a href="https://docs.microsoft.com/pt-br/exchange/security-and-compliance/messaging-records-management/messaging-records-management">Gerenciamento de registros de mensagens</a></p></td>
</tr>
<tr class="even">
<td><p>Arquivo Morto In-loco</p></td>
<td><p>O <em>Arquivo morto in-loco</em> ajuda você a recuperar o controle dos dados de mensagem da organização, eliminando a necessidade de arquivos de armazenamento pessoal (.pst) e permitindo que os usuários armazenem as mensagens em uma <em>caixa de correio de arquivo morto</em> que seja acessível pelo Outlook 2010 ou mais recente e pelo Outlook Web App.</p></td>
<td><p><a href="in-place-archiving-in-exchange-2013-exchange-2013-help.md">Arquivamento In-loco do Exchange 2013</a></p></td>
</tr>
<tr class="odd">
<td><p>Retenção Local</p></td>
<td><p>Quando existe uma expectativa razoável de litígio, as organizações são solicitadas a preservar informações armazenadas eletronicamente (ESI), incluindo emails, pertinentes ao caso. A retenção local permite pesquisar e preservar mensagens que correspondam aos parâmetros de consulta. As mensagens são protegidas contra exclusão, modificação e adulteração, e podem ser preservadas indefinidamente ou por um período especificado.</p></td>
<td><p><a href="https://docs.microsoft.com/pt-br/exchange/security-and-compliance/in-place-and-litigation-holds">Retenção local e Retenção de litígio</a></p></td>
</tr>
<tr class="even">
<td><p>Descoberta eletrônica In-loco</p></td>
<td><p>A Descoberta eletrônica In-loco permite que você pesquise dados de caixa de correio em sua organização do Exchange, visualize resultados de pesquisa e copie-os para uma caixa de correio de descoberta.</p></td>
<td><p><a href="https://docs.microsoft.com/pt-br/exchange/security-and-compliance/in-place-ediscovery/in-place-ediscovery">Descoberta Eletrônica In-loco</a></p></td>
</tr>
<tr class="odd">
<td><p>Diário</p></td>
<td><p>O registro em diário pode ajudar a organização a atender requisitos legais, regulatórios e organizacionais de conformidade, registrando a comunicação por emails de entrada e de saída. Durante o planejamento para retenção e conformidade de mensagens, é importante compreender o registro no diário, como ele se adapta às políticas de conformidade da organização e como o Exchange 2013 pode ajudá-lo a proteger mensagens registradas no diário.</p></td>
<td><p><a href="journaling-exchange-2013-help.md">Registro no Diário</a></p></td>
</tr>
<tr class="even">
<td><p>Regras de Transporte</p></td>
<td><p>Usando regras de transporte, você pode procurar por condições específicas de mensagens que passam por sua organização e agir sobre elas. As regras de transporte permitem que você aplique políticas de mensagens a emails, proteja mensagens, proteja sistemas de mensagens e evite vazamento de informações.</p></td>
<td><p><a href="mail-flow-rules-transport-rules-in-exchange-2013-exchange-2013-help.md">Regras de fluxo de emails ou de transporte</a></p></td>
</tr>
<tr class="odd">
<td><p>Prevenção de Perda de Dados (DLP)</p></td>
<td><p>Os recursos de DLP vão ajudá-lo a proteger seus dados confidenciais e informar os usuários sobre suas políticas e normas. A DLP também pode ajudá-lo a impedir que usuários enviem informações confidenciais acidentalmente para pessoas não autorizadas. Ao configurar políticas de DLP, você pode identificar e proteger dados confidenciais analisando o conteúdo de seu sistema de mensagens, que inclui diversos tipos de arquivo associados. Os modelos de políticas de DLP fornecidos com o Exchange 2013 se baseiam em padrões regulamentares como os padrões de segurança de dados do setor de cartões (PCI-DSS) e PII. O DLP pode ser estendido; com isso, você pode incluir outras políticas importantes para sua organização. Além disso, com o novo recurso de dicas de política, você pode informar aos usuários sobre violações de políticas antes que dados confidenciais sejam enviados.</p></td>
<td><p><a href="https://docs.microsoft.com/pt-br/exchange/security-and-compliance/data-loss-prevention/data-loss-prevention">Prevenção de perda de dados</a></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Direitos de Informação (IRM)</p></td>
<td><p>O IRM (Gerenciamento de Direitos de Informação) oferece proteção online e offline persistente para mensagens e anexos de email usando os Rights Management Services (AD RMS) do Active Directory.</p></td>
<td><p><a href="information-rights-management-exchange-2013-help.md">Gerenciamento de Direitos de Informação</a></p></td>
</tr>
<tr class="odd">
<td><p>S/MIME</p></td>
<td><p>O Secure/Multipurpose Internet Mail Extensions (S/MIME) permite que as pessoas com caixas de correio do Office 365, do Exchange 2013 e do Exchange Online ajudem a proteger informações confidenciais enviando emails assinados e criptografados em suas organizações. Os administradores podem habilitar o S/MIME para caixas de correio do Office 365 sincronizando certificados de usuário entre o Office 365 e seu servidor local e, então, configurando o Outlook Online para oferecer suporte a S/MIME.</p></td>
<td><p><a href="s-mime-for-message-signing-and-encryption-exchange-2013-help.md">S/MIME para assinatura e criptografia de mensagens</a></p></td>
</tr>
<tr class="even">
<td><p>Registro em log de auditoria de Caixa de Correio</p></td>
<td><p>Como as caixas de correio têm boas chances de conter informações confidenciais de alto impacto sobre os negócios, além de informações de identificação pessoal, é importante que você acompanhe quem faz logon nas caixas de correio de sua organização e quais ações são realizadas. É especialmente importante monitorar o acesso de usuários que não sejam proprietários das caixas de correio em questão (conhecidos como usuários representantes). Com o registro em log de auditoria de caixa de correio, você pode registrar o acesso às caixas de correio por proprietários, representantes (incluindo administradores com permissões de acesso completo à caixa de correio) e administradores.</p></td>
<td><p><a href="mailbox-audit-logging-exchange-2013-help.md">Registro em log de auditoria da caixa de correio</a></p>
<p><a href="https://docs.microsoft.com/pt-br/exchange/security-and-compliance/exchange-auditing-reports/exchange-auditing-reports">Relatórios de auditoria do Exchange</a></p></td>
</tr>
<tr class="odd">
<td><p>Log de auditoria de administrador</p></td>
<td><p>Os logs de auditoria de administrador permitem que você mantenha um log de alterações efetuadas por administradores na organização e na configuração e no servidor do Exchange e nos destinatários do Exchange. Você pode usar o registro em log de auditoria do administrador como parte do seu processo de controle de alterações ou para acompanhar alterações e acessar configuração e destinatários por motivos de conformidade.</p></td>
<td><p><a href="administrator-audit-logging-exchange-2013-help.md">Log de auditoria de administrador</a></p></td>
</tr>
</tbody>
</table>

