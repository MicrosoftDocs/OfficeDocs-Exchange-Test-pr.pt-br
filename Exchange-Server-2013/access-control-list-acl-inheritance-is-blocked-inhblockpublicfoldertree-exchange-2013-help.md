---
title: 'Herança de ACL (lista) do controle de acesso bloqueada: Exchange 2013 Help '
TOCTitle: Herança de ACL (lista) do controle de acesso é blocked_InhBlockPublicFolderTree
ms:assetid: e3b89c8a-d6f8-4864-8bf0-35a78ce87cc4
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.inhblockpublicfoldertree(v=EXCHG.150)
ms:contentKeyID: 50486894
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Herança de ACL (lista) do controle de acesso é blocked\_InhBlockPublicFolderTree

 

_**Aplica-se a:** Exchange Server_

_**Tópico modificado em:** 2015-03-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2007 ou Exchange Server 2010 não pode continuar porque não tem sido capazes propagar as permissões necessárias.

Configuração do Exchange requer que a herança de permissões será habilitada nos seguintes objetos do Exchange:

  - Objeto da organização do Exchange

  - Objeto do grupo administrativo do Exchange

  - Objeto container de servidores do Exchange

  - Objeto de lista de endereços do Exchange

  - Objeto de pasta pública do Exchange

  - Objeto da árvore de pastas públicas do Exchange

Falha ao habilitar a herança de permissões para esses objetos pode resultar em problemas de fluxo de email, problemas de montagem e outras interrupções no serviço de armazenamento.

Para resolver esse problema, certifique-se de que as "permissões de permitir sejam propagadas a este objeto e objetos filhos" configuração está habilitada para o objeto e, em seguida, execute novamente o programa de instalação do Exchange Server 2007 ou Exchange 2010.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Para reabilitar a herança de permissões para um objeto de configuração do Exchange usando o Exchange Server 2003 Exchange System Manager</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Habilite a guia de <strong>segurança</strong> para a caixa de propriedades de objeto do Gerenciador do sistema do Exchange, definindo um parâmetro do registro.</p>
<ol>
<li><p>Inicie o Editor de registro (Regedt32.exe).</p></li>
<li><p>Localize a seguinte chave do registro:</p>
<p><strong>HKEY_CURRENT_USER\Software\Microsoft\Exchange\EXAdmin</strong></p></li>
<li><p>No menu <strong>Editar</strong>, clique em <strong>novo</strong> e, em seguida, adicione o seguinte valor de registro:</p>
<p><strong>Nome do valor</strong>: ShowSecurityPage</p>
<p><strong>Tipo de dados</strong>: REG_DWORD</p>
<p><strong>Fracionário</strong>: binário</p>
<p><strong>Valor</strong>: 1</p></li>
<li><p>Feche o Editor do registro.</p></li>
</ol>

> [!TIP]
> Por padrão, na guia <STRONG>segurança</STRONG> não está habilitada na caixa de propriedades do objeto de configuração.


</li>
<li><p>Abra o Gerenciador de sistema do Exchange, o objeto find em questão, com o botão direito do objeto e selecione <strong>Propriedades</strong>.</p></li>
<li><p>Selecione a guia <strong>segurança</strong> e, em seguida, clique em <strong>Avançado</strong>.</p></li>
<li><p>Selecione <strong>Permitir que permissões herdadas do pai sejam propagadas a este objeto e todos os objetos filho</strong> para reabilitar a herança de permissões.</p></li>
<li><p>Reinicie o servidor do Exchange.</p></li>
</ol></td>
</tr>
</tbody>
</table>



> [!WARNING]
> Se você modificar incorretamente os atributos de objetos do Active Directory quando você usa o ADSI Edit, a ferramenta LDP ou outro cliente do LDAP versão 3, você pode causar problemas sérios. Esses problemas podem exigir que você reinstale o Microsoft Windows Server™ 2003, Exchange Server ou ambos. Modifica os atributos de objeto do Active Directory de sua responsabilidade.




<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Para reabilitar a herança de permissões para um objeto de configuração do Exchange usando o ADSIEdit do Exchange Server 2007 ou Exchange Server 2010</p></td>
</tr>
<tr class="even">
<td><ol>
<li><p>Instale o ADSI Edit.</p></li>
<li><p>Inicie o Editor ADSI. Clique em <strong>Iniciar</strong>, clique em <strong>Executar</strong>, digite <strong>ADSIEdit. msc</strong> na caixa de texto e, em seguida, clique em OK.</p></li>
<li><p>Navegue até o objeto em questão, com o botão direito do objeto e selecione <strong>Propriedades</strong>.</p></li>
<li><p>Selecione a guia <strong>segurança</strong> e, em seguida, clique em <strong>Avançado</strong>.</p></li>
<li><p>Selecione <strong>Permitir que permissões herdadas do pai sejam propagadas a este objeto e todos os objetos filho</strong> para reabilitar a herança de permissões.</p></li>
<li><p>Selecione <strong>Ok</strong> duas vezes para aplicar a alteração.</p></li>
<li><p>Aguarde a replicação do Active Directory propagar as alterações ou forçar a replicação do Active Directory, seguindo as orientações no artigo da Base de Conhecimento Microsoft 232072, &quot;Iniciando replicação entre o Active Directory direto replicação Partners&quot; (<a href="http://go.microsoft.com/fwlink/?linkid=3052&kbid=232072" class="uri">http://go.microsoft.com/fwlink/?linkid=3052&amp;kbid=232072</a>).</p></li>
</ol></td>
</tr>
</tbody>
</table>

