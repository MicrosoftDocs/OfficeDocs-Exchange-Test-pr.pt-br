---
title: 'Azure: identificar meu problema com verificações automáticas – registros DNS'
TOCTitle: 'Azure: Ajudar a identificar meu problema com verificações automáticas - registros DNS'
ms:assetid: 1ef42cde-4df4-401a-b8f2-494630996ca8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn793619(v=EXCHG.150)
ms:contentKeyID: 62630005
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Azure: Ajudar a identificar meu problema com verificações automáticas - registros DNS

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2016-12-09_

Um dos problemas mais comuns de instalação de configuração é incorretamente a configuração de registros DNS. Você pode usar as verificações automáticas listadas abaixo para validar a configuração e ajuda você atualize seu ambiente.

Se você já tiver uma conta de usuário do Office 365, selecione entrar. Você não precisa de uma conta da ID do Windows Azure. Você pode ser solicitado para uma conta de usuário novamente quando as verificações executadas. Em caso afirmativo, sua conta de usuário está no formato de username@youroffice365login.domain e sua senha.

## Pré-requisitos

Verificaremos para ver se você tiver Assistente de Conexão do Azure Active Directory e Módulo Azure Active Directory para Windows PowerShell instalado.

O Assistente de Conexão do Azure Active Directory vem com duas versões: [32 bits](https://go.microsoft.com/fwlink/?linkid=286261) e [64 bits](https://go.microsoft.com/fwlink/?linkid=286262).

O Módulo Azure Active Directory para Windows PowerShell vem com duas versões: [32 bits](https://go.microsoft.com/fwlink/?linkid=286258) e [64 bits](https://go.microsoft.com/fwlink/?linkid=286259).

## Verificações de registros de DNS


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Aplicativo</p></td>
<td><p>Sintoma</p></td>
<td><p>Verificar</p></td>
</tr>
<tr class="even">
<td><p>Domínios</p></td>
<td><p>Meu domínio personalizado (por exemplo, contoso.com) não parece ser configurado com o Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Executar essa verificação</a></p></td>
</tr>
<tr class="odd">
<td><p>Domínios</p></td>
<td><p>Meu domínio personalizado (por exemplo, contoso.com) não parece ser configurado com o Office 365 (I usado um registro CNAME)</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Executar essa verificação</a></p></td>
</tr>
<tr class="even">
<td><p>Domínios</p></td>
<td><p>Meu domínio personalizado (por exemplo, contoso.com) não parece ser configurado com o Office 365 (I usado um registro TXT)</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834905">Executar essa verificação</a></p></td>
</tr>
<tr class="odd">
<td><p>Mensagem Instantânea</p></td>
<td><p>Meus usuários estão tendo problemas para inserir o seu cliente do Lync para funcionar</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834901">Executar essa verificação</a></p></td>
</tr>
<tr class="even">
<td><p>Mensagem Instantânea</p></td>
<td><p>Meus usuários estão tendo problemas para inserir o seu cliente do Lync para trabalhar com outras organizações</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834902">Executar essa verificação</a></p></td>
</tr>
<tr class="odd">
<td><p>Email</p></td>
<td><p>Não consigo fazer com o Outlook para configurar automaticamente com o Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834897">Executar essa verificação</a></p></td>
</tr>
<tr class="even">
<td><p>Email</p></td>
<td><p>Meu e-mail não parece ser o roteamento para o Office 365</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834898">Executar essa verificação</a></p></td>
</tr>
<tr class="odd">
<td><p>Email</p></td>
<td><p>Minha organização está recebendo uma boa quantidade de SPAM</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834903">Executar essa verificação</a></p></td>
</tr>
<tr class="even">
<td><p>Email</p></td>
<td><p>Não consigo fazer o trabalho do Exchange híbrido</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834904">Executar essa verificação</a></p></td>
</tr>
</tbody>
</table>

