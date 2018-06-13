---
title: 'Logon único com implantações híbridas: Exchange 2013 Help'
TOCTitle: Logon único com implantações híbridas
ms:assetid: 050606f9-718d-4a1f-b7a6-50b08c6e9e07
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Hh563846(v=EXCHG.150)
ms:contentKeyID: 50487105
ms.date: 01/10/2018
mtps_version: v=EXCHG.150
ms.translationtype: HT
---

# Logon único com implantações híbridas

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013, Exchange Server 2016_

_**Tópico modificado em:**2016-01-29_

O logon único (SSO) com a qual os usuários podem acessar ambas as organizações, local e do Office 365, com um único nome de usuário e senha. Ele oferece aos usuários uma experiência clássica de logon e permite aos administradores controlar facilmente as políticas de conta para caixas de correio da organização do Exchange Online usando ferramentas de gerenciamento locais do Active Directory. Embora não seja necessário, recomendamos que você configure uma implantação híbrida com o logon único habilitado. Sem o logon único, os usuários precisarão se lembrar de dois conjuntos diferentes de credenciais, um para a organização local e outro para o Office 365. Veja algumas outras vantagens do logon único:

  - **Arquivamento do Exchange Online**   Quando o logon único é implantado, os usuários locais do Outlook são solicitados a fornecer as credenciais ao acessar conteúdo arquivado na organização do Exchange Online pela primeira vez. No entanto, os usuários podem evitar a solicitação de credenciais temporariamente no futuro selecionando "salvar senha". Eles receberão solicitações de credenciais novamente quando a senha da conta local for alterada. Se o logon único não estiver implantado em organizações do Exchange e o Arquivamento Online do Exchange estiver habilitado, o UPN (nome principal do usuário) local deverá corresponder à conta do Exchange Online, e os usuários sempre receberão uma solicitação para fornecer suas credenciais locais ao acessar seus arquivos mortos.

  - **Controle de política**   Você pode controlar políticas de conta por meio do Active Directory, isso dá a você a capacidade de gerenciar políticas de senha, restrições de estação de trabalho, controles de bloqueio e muito mais, sem ter que realizar tarefas adicionais na sua organização do Office 365.

  - **Chamadas de suporte reduzidas** Senhas esquecidas são uma fonte comum de chamadas de suporte em todas as empresas. Se os usuários tiverem menos senhas para lembrar, será menos provável se esquecerem delas.

Você tem duas opções ao implantar o logon único: sincronização de senha e Serviços de Federação do Active Directory (AD FS). As duas opções são fornecidas pelo Azure Active Directory Connect. É altamente recomendável usar o método de sincronização de senha, a menos que você tenha uma necessidade específica que exija o AD FS. A sincronização de senha oferece muitos dos mesmos benefícios do AD FS, sem a complexidade de sua implantação. A tabela a seguir mostra algumas vantagens e desvantagens comuns de cada opção.


> [!TIP]
> Por padrão, se você implantar o AD FS e seus servidores locais do AD FS não puderem ser acessados pela Internet por qualquer motivo, o Office 365 voltará à sincronização de senha para autenticar os usuários. Isso permite que os usuários com caixas de correio do Office 365 continuem trabalhando normalmente, mesmo que seus servidores locais não estejam disponíveis.



Para saber mais sobre cada opção, confira [Opções de logon único de usuário do Azure AD Connect](http://go.microsoft.com/fwlink/p/?linkid=723514)


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Método de logon único</p></th>
<th><p>Vantagens</p></th>
<th><p>Desvantagens</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Sincronização de senha (recomendado)</p></td>
<td><ul>
<li><p>Significativamente menos complexo do que o AD FS</p></li>
<li><p>Os usuários podem fazer logon no Office 365 mesmo que o Active Directory local não esteja disponível.</p></li>
<li><p>São exigidos menos servidores adicionais para implantar a sincronização de senha.</p></li>
<li><p>Não são exigidos certificados de terceiros.</p></li>
<li><p>Não exige acesso externo ao Active Directory local por meio do AD FS.</p></li>
<li><p>A implantação geralmente pode ser concluída em apenas algumas horas.</p></li>
</ul></td>
<td><ul>
<li><p>Desabilitar uma conta de usuário no Active Directory local não a desabilitará no Office 365. Você precisa desativar a conta no Portal de administração do Office 365 manualmente.</p></li>
<li><p>Requer o Active Directory local. Outros serviços de diretório não são compatíveis.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>AD FS</p></td>
<td><ul>
<li><p>As alterações de senha são imediatas.</p></li>
<li><p>Ao desabilitar um usuário em seu Active Directory local, você desabilita o acesso desse usuário à rede local e à conta do Office 365.</p></li>
<li><p>É compatível com serviços de diretório que não sejam o Active Directory.</p></li>
<li><p>É compatível com implantações muito grandes e diversas.</p></li>
<li><p>É compatível com a autenticação de dois fatores.</p></li>
</ul></td>
<td><ul>
<li><p>Requer mais servidores, e pelo menos um deles precisa residir em sua rede de perímetro.</p></li>
<li><p>Requer um endereço IP público e que a porta TCP 443 esteja aberta em seu firewall.</p></li>
<li><p>Requer conectividade com o Active Directory local para detectar alterações realizadas em senhas de contas e se uma conta foi habilitada ou desabilitada recentemente.</p></li>
</ul></td>
</tr>
</tbody>
</table>

