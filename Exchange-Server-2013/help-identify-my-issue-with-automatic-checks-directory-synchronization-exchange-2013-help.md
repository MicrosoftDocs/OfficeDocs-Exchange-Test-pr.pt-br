---
title: 'Ajudar a identificar meu problema com verificações automáticas - sincronização de diretórios: Exchange 2013 Help'
TOCTitle: Ajudar a identificar meu problema com verificações automáticas - sincronização de diretórios
ms:assetid: e6ea900a-c382-444c-a8ce-54d392bfeca3
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn793977(v=EXCHG.150)
ms:contentKeyID: 62633047
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Ajudar a identificar meu problema com verificações automáticas - sincronização de diretórios

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Você pode usar as verificações automáticas abaixo para validar sua configuração e ajuda você atualize seu ambiente.

Se você já tiver uma conta de usuário do Office 365, selecione entrar. Você não precisa de uma conta da ID do Windows Azure. Você pode ser solicitado para uma conta de usuário novamente quando as verificações executadas. Em caso afirmativo, sua conta de usuário está no formato de username@youroffice365login.domain e sua senha.


> [!TIP]
> Se você receber mensagens de aviso de sincronização no portal do Office 365, erros de logs de eventos do servidor de sincronização, ou emails de notificação de sincronização de diretório não íntegros do Microsoft Online Services, você pode estar tendo algum tipo de problema de sincronização de diretório. A <A href="https://aka.ms/dsup">Solução de problemas de sincronização de diretório</A> é uma ferramenta de diagnóstico baseado na Web, projetada para ajudar a identificar tipos de falhas de sincronização comuns e estabelece soluções direcionadas para os problemas encontrados. A solução de problemas de sincronização de diretório deve ser executada no servidor DirSync.



## Pré-requisitos

Verificaremos para ver se você tiver Assistente de Conexão do Azure Active Directory e Módulo Azure Active Directory para Windows PowerShell instalado.

O Assistente de Conexão do Azure Active Directory vem com duas versões: [32 bits](https://go.microsoft.com/fwlink/?linkid=286261) e [64 bits](https://go.microsoft.com/fwlink/?linkid=286262).

O Módulo Azure Active Directory para Windows PowerShell vem com duas versões: [32 bits](https://go.microsoft.com/fwlink/?linkid=286258) e [64 bits](https://go.microsoft.com/fwlink/?linkid=286259).

## Verificações de sincronização de diretório


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
<td><p>Sincronização de diretório</p></td>
<td><p>Não tenho certeza se todas as minhas contas de usuário do Active Directory atendem aos requisitos para sincronização de diretórios.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834884">Executar essa verificação</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronização de diretório</p></td>
<td><p>Não tenho certeza se minha níveis funcionais de domínio do Active Directory estão definidas corretamente para o Windows Server 2003 ou superior.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Executar essa verificação</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronização de diretório</p></td>
<td><p>Não tenho certeza se a sincronização de diretórios ocorreu nas últimas três horas.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">Executar essa verificação</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronização de diretório</p></td>
<td><p>Não tenho certeza se minha Active Directory tem quaisquer atributos de usuário duplicado que bloqueiam a sincronização de diretório.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834883">Executar essa verificação</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronização de diretório</p></td>
<td><p>Não tenho certeza se a sincronização de diretórios é habilitada no Office 365.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834887">Executar essa verificação</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronização de diretório</p></td>
<td><p>Não tenho certeza se pode implantar o Office 365 limitações de cotação.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834920">Executar essa verificação</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronização de diretório</p></td>
<td><p>Não tenho certeza se pode implantar o Office 365 e usar a configuração de sincronização de diretório padrão.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834876">Executar essa verificação</a></p></td>
</tr>
<tr class="odd">
<td><p>Sincronização de diretório</p></td>
<td><p>Não tenho certeza se usa o Active Directory e pode oferecer suporte a sincronização de diretórios.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834886">Executar essa verificação</a></p></td>
</tr>
<tr class="even">
<td><p>Sincronização de diretório</p></td>
<td><p>Não tenho certeza se todos os meus grupos do Active Directory atendem aos requisitos para sincronização de diretórios.</p></td>
<td><p><a href="https://go.microsoft.com/?linkid=9834913">Executar essa verificação</a></p></td>
</tr>
</tbody>
</table>

