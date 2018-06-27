---
title: 'Referência de permissões de implantação do Exchange 2013: Exchange 2013 Help'
TOCTitle: Referência de permissões de implantação do Exchange 2013
ms:assetid: b13412d0-0cc4-4c1d-bf31-cae3d3e211a9
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Ee681663(v=EXCHG.150)
ms:contentKeyID: 59635890
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Referência de permissões de implantação do Exchange 2013

 

_**Aplica-se a:**Exchange Server 2013_

_**Tópico modificado em:**2016-12-09_

Este tópico descreve as permissões necessárias para configurar uma organização do Microsoft Exchange Server 2013. Os grupos de segurança universal (USGs) associados aos grupos de funções de gerenciamento e outros grupos e entidades de segurança do Windows estão incluídos nas listas de controle de acesso (ACLs) de vários objetos do Active Directory. As ACLs controlam as operações que podem ser executadas em cada objeto. Ao compreender quais permissões são concedidas a cada grupo de função, grupo de segurança ou entidade de segurança, é possível determinar as permissões mínimas necessárias para instalar o Exchange 2013.

Em alguns casos, a ACL não é aplicada na propriedade comum, **ntSecurityDescriptor**, mas em outra propriedade, como a **msExchMailboxSecurityDescriptor**. O serviço de diretório não pode impor uma segurança que não esteja especificada no descritor de segurança do Windows. Na maioria dos casos, essas ACLs são replicadas para armazenar ACLs nos objetos adequados pelo serviço de armazenamento. Infelizmente, não existe uma ferramenta para visualizar estas ACLs de outra forma a não ser como dados binários não processados.

As colunas para cada tabela de permissões incluem as seguintes informações:

  - **Conta**   A entidade de segurança concedeu ou negou as permissões.

  - **Tipo de ACE**   Tipo de entrada de controle de acesso (ACE)
    
      - **ACE de Permissão**   Uma ACE de permissão concede autorização para que o usuário ou grupo associado à ACE acesse um item.
    
      - **ACE de Negação**   Uma ACE de negação impede o usuário ou o grupo associado à ACE de acessar um item.

  - **Herança**   O tipo de herança utilizado para objetos filho.
    
      - **Todos** indica que as permissões se aplicam ao objeto e a todos os sub-objetos.
    
      - **Desc** indica que as permissões se aplicam à classe de objeto listada na linha Na Propriedade/Aplicável A.
    
      - **Nenhum** indica que essas permissões se aplicam somente ao objeto.

  - **Permissões**   As permissões concedidas para a conta.

  - **Na Propriedade/Aplicável A**   Em alguns casos, permissões são aplicáveis somente a uma determinada propriedade, a um conjunto de propriedades ou a uma classe de objeto. Essas permissões limitadas são especificadas aqui.

  - **Comentários**   Quando aplicável, esta coluna explica por quê as permissões são necessárias ou fornece outras informações sobre as permissões.

As permissões normalmente são listadas na tabela pelos nomes usados na página de propriedades de Active Directory Segurança **do Editor de Serviço Interfaces (ADSI) Edit (AdsiEdit.msc)Security de**, na exibição **Avançada** da guia **Exibir/Ediart**. A página de propriedades de **Segurança** do ADSI Edit relaciona uma visualização mais condensada das permissões. A ferramenta LDP (Ldp.exe) exibe a máscara de acesso diretamente como valor numérico. O código de configuração refere-se às permissões por constantes predefinidas.

A tabela a seguir exibe as relações entre esses valores.


<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th>Página de Resumo do ADSI Edit</th>
<th>Visualização Avançada do ADSI Edit, Guia Exibir/Editar</th>
<th>Entradas ACL aplicadas a um determinado objeto</th>
<th>Valor binário (máscara de acesso em LDP)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Controle Total</p></td>
<td><p>Controle Total</p></td>
<td><p><code>WRITE_OWNER | WRITE_DAC | READ_CONTROL | DELETE | ACTRL_DS_CONTROL_ACCESS | ACTRL_DS_LIST_OBJECT | ACTRL_DS_DELETE_TREE | ACTRL_DS_WRITE_PROP | ACTRL_DS_READ_PROP | ACTRL_DS_SELF | ACTRL_DS_LIST | ACTRL_DS_DELETE_CHILD | ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x000F01FF</code></p></td>
</tr>
<tr class="even">
<td><p>Leitura</p></td>
<td><p>Listar Conteúdo + Ler Todas as Propriedades + Permissões de Leitura</p></td>
<td><p><code>ACTRL_DS_LIST | ACTRL_DS_READ_PROP | READ_CONTROL</code></p></td>
<td><p><code>0x00020014</code></p></td>
</tr>
<tr class="odd">
<td><p>Gravar</p></td>
<td><p>Gravar Todas as Propriedades + Todas as Gravações Validadas</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP | ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000028</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Conteúdo da Lista</p></td>
<td><p><code>ACTRL_DS_LIST</code></p></td>
<td><p><code>0x00000004</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Ler Todas as Propriedades</p></td>
<td><p><code>ACTRL_DS_READ_PROP</code></p></td>
<td><p><code>0x00000010</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Gravar Todas as Propriedades</p></td>
<td><p><code>ACTRL_DS_WRITE_PROP</code></p></td>
<td><p><code>0x00000020</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Excluir</p></td>
<td><p><code>DELETE</code></p></td>
<td><p><code>0x00010000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Excluir Sub-árvore</p></td>
<td><p><code>ACTRL_DS_DELETE_TREE</code></p></td>
<td><p><code>0x00000040</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Permissões de Leitura</p></td>
<td><p><code>READ_CONTROL</code></p></td>
<td><p><code>0x00020000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Permissões para Modificação</p></td>
<td><p><code>WRITE_DAC</code></p></td>
<td><p><code>0x00040000</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Modificar Proprietário</p></td>
<td><p><code>WRITE_OWNER</code></p></td>
<td><p><code>0x00080000</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p>Todas as Gravações Validadas</p></td>
<td><p><code>ACTRL_DS_SELF</code></p></td>
<td><p><code>0x00000008</code></p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p>Todos os Direitos Estendidos</p></td>
<td><p><code>ACTRL_DS_CONTROL_ACCESS</code></p></td>
<td><p><code>0x00000100</code></p></td>
</tr>
<tr class="even">
<td><p>Criar Todos os Objetos Filho</p></td>
<td><p>Criar Todos os Objetos Filho</p></td>
<td><p><code>ACTRL_DS_CREATE_CHILD</code></p></td>
<td><p><code>0x00000001</code></p></td>
</tr>
<tr class="odd">
<td><p>Excluir Todos os Objetos Filho</p></td>
<td><p>Excluir Todos os Objetos Filho</p></td>
<td><p><code>ACTRL_DS_DELETE_CHILD</code></p></td>
<td><p><code>0x00000002</code></p></td>
</tr>
<tr class="even">
<td><p></p></td>
<td><p></p></td>
<td><p><code>ACTRL_DS_LIST_OBJECT</code></p></td>
<td><p><code>0x00000080</code></p></td>
</tr>
</tbody>
</table>


Direitos estendidos são direitos personalizados especificados por aplicativos específicos. Eles são especificados na ACL. No entanto, não têm significado para o Active Directory. O aplicativo específico impõe todos os direitos estendidos. Exemplos de direitos estendidos do Exchange são "Criar pasta pública" ou "Criar propriedades nomeadas no repositório de informações".

Para obter informações sobre as permissões configuradas durante uma instalação de Exchange Server 2010 da Microsoft, consulte a [Referência de permissões de implantação do Exchange 2010](https://go.microsoft.com/fwlink/p/?linkid=402924).

## Preparar Permissões do Active Directory

As tabelas de permissões desta seção mostram as permissões definidas quando o comando `Setup /PrepareAD` é executado.


> [!TIP]
> As permissões descritas nesta seção são as permissões padrão configuradas ao implantar o Exchange 2013 usando o modelo de permissões compartilhadas. Se você implantou o Exchange 2013 usando o modelo de permissões divididas do Active Directory, as permissões padrão são diferentes. Para obter mais informações sobre as alterações nas permissões padrão ao usar as permissões divididas do Active Directory ou sobre os modelos de permissões divididas e compartilhadas em geral, consulte <A href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</A> em <A href="understanding-split-permissions-exchange-2013-help.md">Compreendendo as permissões de divisão</A>. Se não escolher usar permissões divididas do Active Directory quando instalar o Exchange, o Exchange usará as permissões compartilhadas.



## Permissões de Contêiner do Microsoft Exchange

A tabela a seguir exibe as permissões definidas no contêiner do Microsoft Exchange dentro da partição de configuração.

### Nome distinto do objeto: CN=Microsoft Exchange,CN=Serviços,CN=Configuração,DC=\<domínio\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Conta de Instalação</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p></p></td>
<td><p>Esta é a conta utilizada para executar o comando <code>/PrepareAD</code>.</p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Nenhum</p></td>
<td><p>Propriedade de Leitura</p>
<p>Conteúdo da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões para Modificação</p></td>
<td><p>msExchSmtpRceiveConnector</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p>
<p>Objeto de Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Instalação Delegada</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Permissões de Contêiner da Descoberta Automática do Microsoft Exchange

A tabela a seguir exibe as permissões definidas no contêiner da Descoberta Automática do Microsoft Exchange, dentro da partição de configuração.

### Nome distinto do objeto: CN=Descoberta Automática do Microsoft Exchange,CN=Serviços,CN=Configuração,DC=\<domínio\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Permissões de Contêiner da Organização do Microsoft Exchange

As tabelas de permissões desta seção exibem as permissões configuradas na Organização do Microsoft Exchange e nos subcontêineres dentro da partição de configuração.

### Nome distinto do objeto: CN=\<organização\>,CN=Microsoft Exchange,CN=Serviços,CN=Configuração,DC=\<domínio\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta(s)</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Administradores de Empresa</p>
<p>Administradores de Domínio Raiz</p>
<p>Conta de Instalação</p>
<p>Gerenciamento da Organização</p></td>
<td><p>ACE de Negação</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Como</p>
<p>Receber Como</p></td>
<td><p></p></td>
<td><p>Administradores do Windows não têm permissão para abrir caixas de correio.</p></td>
</tr>
<tr class="even">
<td><p>Administradores de Empresa</p>
<p>Administradores de Esquema</p>
<p>Administradores de Domínio Raiz</p>
<p>Conta de Instalação</p>
<p>Gerenciamento da Organização</p></td>
<td><p>ACE de Negação</p></td>
<td><p>Todos</p></td>
<td><p>Representação dos Serviços Web do Exchange</p>
<p>Serialização de Token dos Serviços Web do Exchange</p></td>
<td><p></p></td>
<td><p>Direito estendido</p></td>
</tr>
<tr class="odd">
<td><p>Administradores de Empresa</p>
<p>Administradores de Esquema</p>
<p>Administradores de Domínio Raiz</p>
<p>Conta de Instalação</p></td>
<td><p>ACE de Negação</p></td>
<td><p>Todos</p></td>
<td><p>Acesso ao Transporte de Repositório</p>
<p>Delegação Restrita de Repositório</p>
<p>Acesso de Leitura ao Repositório</p>
<p>Acesso de Leitura e Gravação ao Repositório</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sistema Local</p></td>
<td><p>Permitir</p></td>
<td><p>Todos</p></td>
<td><p>Todos os Direitos Estendidos</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Negação</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpace</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuários Autenticados</p></td>
<td><p>Permitir</p></td>
<td><p>Nenhum</p></td>
<td><p>Leitura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Autoridade NT\Serviço de Rede</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores de Disponibilidade Gerenciada</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Todos os Direitos Estendidos</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchOwningServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchDatabaseCreated</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUserCulture</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>siteFolderGUID</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>siteFolderServer</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchEDBOffline</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchPatchMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>publicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar pasta pública de nível superior</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar pasta pública de nível superior</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Exibir status do armazenamento de informações</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Exibir status do repositório de informações</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Administrar o armazenamento de informações</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Administrar repositório de informações</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar propriedades nomeadas no repositório de informações</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar propriedades nomeadas no repositório de informações</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar ACL de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar ACL de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar cotas de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar cotas de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar ACL administrativo de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar ACL administrativo de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar vencimento de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar vencimento de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar lista de réplica de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar lista de réplicas de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar retenção de item excluído de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Modificar retenção de item excluído de pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Habilitar Pasta Pública para Email</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Todos</p>
<p>Autoridade NT\Logon Anônimo</p>
<p></p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar propriedades nomeadas no repositório de informações</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Todos</p>
<p>Autoridade NT\Logon Anônimo</p>
<p></p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar pasta pública</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Todos</p>
<p>Autoridade NT\Logon Anônimo</p>
<p></p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p><code>/ msExchPrivateMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Todos</p>
<p>Autoridade NT\Logon Anônimo</p>
<p></p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p><code>/ siteAddressing</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Todas as Listas de Endereços,CN=Contêiner das Listas de Endereços,CN=\<organização\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Conteúdo da Lista</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Listas de Endereços Offline,CN=Contêiner de Listas de Endereços, CN=\<organização\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Fazer Download do Catálogo de Endereços Offline</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Endereçamento,CN=\<organização\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Diretivas de Destinatário,CN=\<organização\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchLastAppliedRecipientFilter</code></p>
<p><code>msExchRecipientFilterFlags</code></p></td>
</tr>
</tbody>
</table>


## Permissões de Configuração de Contêiner de Partição

As tabelas de permissões desta seção exibem as permissões configuradas pelo comando `Setup /PrepareAD` em vários contêineres dentro da partição de configuração.

### Nome distinto do objeto: CN=Sites,CN=Configuração,DC=\<domínio\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchVersion / site</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchVersion / site-link</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchPartnerId / site</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchMinorPartnerId / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchResponsibleforSites / site</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p></p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchTransportSiteFlags / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchCost / site-link</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p>
<p>Sistema Local</p>
<p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p><code>/ msExchEdgeSyncEHFConnector</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p>
<p>Sistema Local</p>
<p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p><code>/ msExchEdgeSyncMservConnector</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Filhos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p>
<p>Excluir Árvore</p></td>
<td><p><code>msExchEdgeSyncServiceConfig / site</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p>
<p>Sistema Local</p>
<p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p><code>/ msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Filhos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p>
<p>Excluir Árvore</p></td>
<td><p><code>msExchEdgeSyncMservConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p>
<p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Filhos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p>
<p>Excluir Árvore</p></td>
<td><p><code>msExchEdgeSyncEHFConnector / msExchEdgeSyncServiceConfig</code></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Objetos Excluídos,CN=Configuração,DC=\<domínio\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Conteúdo da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administração da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Conta de Instalação</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissão de Leitura</p>
<p>Permissão de Gravação</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p>Esta é a conta utilizada para executar o comando <code>/PrepareAD</code>.</p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Serviço de Rede</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Conteúdo da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Permissões do Grupo Administrativo do Exchange

O comando `Setup /PrepareAD` também configura as permissões a seguir nos grupos administrativos da organização.

### Nome distinto do objeto: CN=\<grupo admin\>,CN=Grupos Administrativos,CN=\<organização\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Acessar Serviço de Atualização de Destinatário</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Permite que Administradores de Destinatários do Exchange marquem destinatários com informações sobre o endereço do proxy.</p></td>
</tr>
<tr class="even">
<td><p>Sistema Local</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Acessar Serviço de Atualização de Destinatário</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Permite que os servidores carimbem destinatários com informações sobre o endereço do proxy.</p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Acessar Serviço de Atualização de Destinatário</p></td>
<td><p><code>msExchExchangeServer</code></p></td>
<td><p>Permite que Administradores de Pasta Pública do Exchange marquem destinatários com informações sobre o endereço do proxy.</p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Configurações Avançadas de Segurança,CN=\<grupo admin\>,CN=Grupos Administrativos,CN=\<organização\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Nenhum</p></td>
<td><p>Conteúdo da Lista</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Criptografia,CN=Configurações Avançadas de Segurança,CN=\<grupo admin\>,CN=Grupos Administrativos,CN=\<organização\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Nenhum</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Matrizes,CN=\<grupo admin\>,CN=Grupos Administrativos,CN=\<organização\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Nenhum</p></td>
<td><p>Conteúdo da Lista</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Grupos de Disponibilidade de Banco de Dados,CN=\<grupo admin\>,CN=Grupos Administrativos,CN=\<organização\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Nenhum</p></td>
<td><p>Conteúdo da Lista</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Bancos de Dados,CN=\<grupo admin\>,CN=Grupos Administrativos,CN=\<organização\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Nenhum</p></td>
<td><p>Conteúdo da Lista</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Servidores,CN=\<grupo admin\>,CN=Grupos Administrativos,CN=\<organização\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Negação</p></td>
<td><p>Todos</p></td>
<td><p>Receber Como</p></td>
<td><p></p></td>
<td><p>Os Servidores do Exchange não têm permissão para abrir caixas de correio.</p></td>
</tr>
<tr class="even">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Nenhum</p></td>
<td><p>Conteúdo da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Permissões de Contêiner de Grupos de Segurança do Microsoft Exchange

As tabelas de permissões desta seção mostram as permissões configuradas no contêiner dos Grupos de Segurança do Microsoft Exchange, dentro da partição de domínio raiz.

### Nome distinto do objeto: OU=Grupos de Segurança do Microsoft Exchange,DC=\<domínio raiz\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p></td>
<td><p><code>/ Group</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Excluir</p></td>
<td><p><code>/ group</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Member / group</code></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Gerenciamento da Organização,OU=Grupos de Segurança do Microsoft Exchange,DC=\<domínio raiz\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Gerenciamento de Pasta Pública,OU=Grupos de Segurança do Microsoft Exchange,DC=\<domínio raiz\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=ExchangeLegacyInterop,OU=Grupos de Segurança do Microsoft Exchange,DC=\<domínio raiz\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Servidores Exchange,OU=Grupos de Segurança do Microsoft Exchange,DC=\<domínio raiz\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Administradores de Domínio Raiz</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Membros de Leitura</p>
<p>Membros de Gravação</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Administradores de Domínios Filho</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Membros de Leitura</p>
<p>Membros de Gravação</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Preparar Domínio

As tabelas a seguir mostram as permissões definidas quando o comando `Setup /PrepareDomain` é executado.


> [!TIP]
> As permissões descritas nesta seção são as permissões padrão configuradas ao implantar o Exchange 2013 usando o modelo de permissões compartilhadas. Se você implantou o Exchange 2013 usando o modelo de permissões divididas do Active Directory, as permissões padrão são diferentes. Para obter mais informações sobre as alterações nas permissões padrão ao usar as permissões divididas do Active Directory ou sobre os modelos de permissões divididas e compartilhadas em geral, consulte <A href="understanding-split-permissions-exchange-2013-help.md">Active Directory split permissions</A> em <A href="understanding-split-permissions-exchange-2013-help.md">Compreendendo as permissões de divisão</A>. Se não escolher usar permissões divididas do Active Directory quando instalar o Exchange, o Exchange usará as permissões compartilhadas.



### Nome distinto do objeto: DC=\<domínio\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>AUTORIDADE NT\REDE</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>Concede permissões de leitura do serviço de Transporte.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Sincronização da Replicação</p></td>
<td><p></p></td>
<td><p>Direito estendido</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p>
<p>Listar Filhos</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p>
<p>Listar Filhos</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>WriteDACL</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>WriteDACL</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Excluir Árvore</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Excluir Árvore</p>
<p></p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir</p></td>
<td><p><code>/ contact</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir</p></td>
<td><p><code>/ inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir</p></td>
<td><p><code>/ user</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir</p></td>
<td><p><code>/ organizationUnit</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir</p></td>
<td><p><code>/ group</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p></td>
<td><p><code>/ computer</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Redefinir Senha no Próximo Logon</p></td>
<td><p></p></td>
<td><p>Direito estendido</p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Alterar Senha</p></td>
<td><p><code> / user</code></p></td>
<td><p>Direito estendido</p></td>
</tr>
<tr class="odd">
<td><p>Configuração Delegada</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=AdminSDHolder,CN=Sistema,DC=\<domínio\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>AUTORIDADE NT\REDE</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p>Concede permissões de leitura do serviço de Transporte.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>groupType</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchMailboxSecurityDescriptor</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMServerWritableFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUserCultulre</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>memberOf</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>canonicalName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Sincronização da Replicação</p></td>
<td><p></p></td>
<td><p>Direito estendido</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p>
<p>Listar Filhos</p></td>
<td><p><code>msExchActiveSyncDevices / User</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p>
<p>Listar Filhos</p></td>
<td><p><code>msExchActiveSyncDevices / inetOrgPerson</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchSafeSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchMobileMailboxFlags</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchSafeRecipientsHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>userCertificate</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMDtmfMap</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchBlockedSendersHash</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMSpokenName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchUMPinChecksum</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>thumbnailPhoto</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>displayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Public Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchPublicDelegates</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>adminDisplayName</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p><code>/ msExchDynamicDistributionList</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>textEncodedORAddress</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>showInAddressBook</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>legacyExchangeDN</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Personal Information</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>proxyAddresses</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>displayNamePrintable</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>mail</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>pwdLastSet</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>sAMAccountName</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>Member</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>wwwHomePage</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>countryCode</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>userAccountControl</code></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Permissões do Windows do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>managedBy</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Configuração Delegada</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>User Account Restrictions</code></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Objetos Excluídos,DC=\<domínio\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Conteúdo da Lista</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Objetos de Sistema do Microsoft Exchange,DC=\<domínio\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AUTORIDADE NT\REDE</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Permissões de Leitura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões de Leitura</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>garbageCollPeriod</code></p></td>
</tr>
<tr class="even">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>adminDisplayName</code></p></td>
</tr>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>modifyTimeStamp</code></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Negação</p></td>
<td><p>Todos</p></td>
<td><p>Excluir Árvore</p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de LeituraExcluir Árvore</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Excluir Filho</p>
<p></p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Excluir Filho</p>
<p></p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>/ publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Alterar Senha</p>
<p>Redefinir Senha no Próximo Logon</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p></td>
<td><p><code>/ msExchSystemMailbox</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p></td>
<td><p><code>/ user</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p>legacyExchangeDN / publicFolder</p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Gerenciamento de Pasta Pública</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>mail / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>displayNamePrintable / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>displayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>textEncodedORAddress / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>proxyAddresses / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>cn / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>showInAddressBook / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>legacyExchangeDN / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>Exchange Personal Information / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>msDSPhoneticDisplayName / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>msExchPFContacts / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>garbageCollPeriod / publicFolder</code></p></td>
</tr>
<tr class="odd">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>name / publicFolder</code></p></td>
</tr>
<tr class="even">
<td><p>Subsistema Confiável do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p>
<p>Propriedade de Gravação</p></td>
<td><p><code>msExchPublicDelegates / publicFolder</code></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Servidores do Domínio de Instalação do Exchange,CN=Objetos do Sistema Exchange da Microsoft ,DC=\<domínio\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Gerenciamento da Organização</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Instalação de Função de Servidor

Durante a instalação das funções de servidor de Acesso para Cliente e de Caixa de Correio, a Instalação adiciona o USG de Gerenciamento da Organização ao grupo de segurança do administrador do computador local, para que os membros do grupo de função de gerenciamento chamado Gerenciamento da Organização possam gerenciar o servidor.

A tabela de permissões a seguir exibe as permissões configuradas na instalação das funções de servidor de Acesso para Cliente ou de Caixa de Correio.

### Nome distinto do objeto: CN=\<servidor\>,CN=Servidores,CN=\<grupo admin\>,CN=Grupos Administrativos,CN=\<organização\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>MACHINE$</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>MACHINE$</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Nenhum</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p><code>msExchServerSite</code></p>
<p><code>msExchEdgeSyncCredential</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Acesso ao Transporte de Repositório</p>
<p>Delegação Restrita de Repositório</p>
<p>Acesso Somente Leitura ao Repositório</p>
<p>Acesso de Leitura e Gravação ao Repositório</p></td>
<td><p></p></td>
<td><p>Direitos estendidos</p></td>
</tr>
<tr class="even">
<td><p>AUTORIDADE NT\REDE</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Serialização de Token dos Serviços Web do Exchange</p></td>
<td><p></p></td>
<td><p>Direito estendido</p>
<p>Concedido somente a objetos da função de servidor de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>AUTORIDADE NT\REDE</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Sistema Local</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Permissões de Leitura</p>
<p>Conteúdo da Lista</p>
<p>Propriedade de Leitura</p>
<p>Objeto da Lista</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Configuração Delegada</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Controle Total</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Configuração Delegada</p></td>
<td><p>ACE de Negação</p></td>
<td><p>Todos</p></td>
<td><p>Criar Filho</p>
<p>Excluir Filho</p></td>
<td><p><code>/ msExchPublicMDB</code></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Configuração Delegada</p></td>
<td><p>ACE de Negação</p></td>
<td><p>Todos</p></td>
<td><p>Receber Como</p>
<p>Enviar Como</p></td>
<td><p></p></td>
<td><p>Direito estendido</p></td>
</tr>
</tbody>
</table>


## Grupos de Disponibilidade de Banco de Dados

As tabelas de permissões desta seção mostram as permissões configuradas que estão relacionadas aos grupos de disponibilidade de banco de dados e seus membros.

### Nome distinto do objeto: CN=\<NomeDAG\>,CN=Grupos de Disponibilidade de Banco de Dados,CN=\<grupo admin\>,CN=Grupos Administrativos,CN=\<organização\>

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
<col style="width: 20%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Nenhum</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Transporte de Borda

Se um servidor de Transporte de Borda for instalado e for estabelecida uma Inscrição de Borda com a organização do Exchange, as permissões da tabela de permissões a seguir serão definidas quando o servidor de Transporte de Borda for instanciado na organização.

### Nome distinto do objeto: CN=\<servidor\>,CN=Servidores,CN=\<grupo admin\>,CN=Grupos Administrativos,CN=\<organização\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Propriedade de Gravação</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Nenhum</p></td>
<td><p>Propriedades de Leitura</p></td>
<td><p></p></td>
<td><p>A ACE é definida no esquema dos objetos do <code>msExchExchangeServer</code> de classe <code>defaultSecurityDescriptor</code>.</p></td>
</tr>
</tbody>
</table>


## Instalação de Servidor de Caixa de Correio

Durante a instalação do primeiro servidor de Caixa de Correio, os seguintes contêiners serão criados, caso ainda não existam. A tabela de permissões a seguir exibe as permissões aplicadas.

### Nome distinto do objeto: CN=Configuração de Disponibilidade,CN=\<organização\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Desc</p></td>
<td><p>Propriedade de Leitura</p></td>
<td><p><code>msExchAvailabilityUserPassword / msExchAvailabilityAddressSpaceObjects</code></p></td>
<td><p>Direito estendido</p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=\<Servidor\> Padrão,CN= Conectores de Recebimento SMTP,CN=Protocolos,CN=\<Servidor\>,CN=Servidores,CN=\<grupo admin\>,CN=\<organização\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Negação</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Floresta</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Negação</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos da Organização</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Qualquer Remetente</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Qualquer Remetente</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Qualquer Remetente</p></td>
<td><p></p></td>
<td><p>Este é o identificador de segurança (SID) conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Qualquer Remetente</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Qualquer Remetente</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar EXCH50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar EXCH50</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar EXCH50</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar EXCH50</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XShadow</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSessionParams</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSessionParams</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Floresta</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar xAttr</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar xAttr</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XProxyFrom de floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XProxyFrom de floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSysProbe de floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSysProbe de floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar propriedades estendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar propriedades estendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar propriedades estendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar índice Fast de XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar índice Fast de XMessageContext</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar índice Fast de XMessageContext</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar XMessageContext do cache de destinatários do AD</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar XMessageContext do cache de destinatários do AD</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar XMessageContext do cache de destinatários do AD</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Sinalizador de Autenticação</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Sinalizador de Autenticação</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Sinalizador de Autenticação</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Sinalizador de Autenticação</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Sinalizador de Autenticação</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Antispam</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Antispam</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Antispam</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Antispam</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Antispam</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Limite de Tamanho da Mensagem</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Limite de Tamanho da Mensagem</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Limite de Tamanho da Mensagem</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Limite de Tamanho da Mensagem</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Limite de Tamanho da Mensagem</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos da Organização</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos da Organização</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos da Organização</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens ao Servidor</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens ao Servidor</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens ao Servidor</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens ao Servidor</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens ao Servidor</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Remetente de Domínio Autoritativo</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Remetente de Domínio Autoritativo</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Remetente de Domínio Autoritativo</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Remetente de Domínio Autoritativo</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Remetente de Domínio Autoritativo</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Antispam</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens ao Servidor</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


### Nome distinto do objeto: CN=Cliente \<Servidor\>,CN=Conectores de Recebimento SMTP,CN=Protocolos,CN=\<Servidor\>,CN=Servidores,CN=\<grupo admin\>,CN=\<organização\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Antispam</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Usuários Autenticados</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens ao Servidor</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSessionParams</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSessionParams</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSessionParams</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Qualquer Remetente</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Qualquer Remetente</p></td>
<td><p></p></td>
<td><p>Este é o identificador de segurança (SID) conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Qualquer Remetente</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Qualquer Remetente</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Exch50</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Exch50</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Exch50</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens para qualquer Destinatário</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XShadow</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>ExchangeLegacyInterop</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Floresta</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos de Floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar xAttr</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar xAttr</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar xAttr</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XProxyFrom</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XProxyFrom de floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XProxyFrom de floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Sinalizador de Autenticação</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Sinalizador de Autenticação</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Sinalizador de Autenticação</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Sinalizador de Autenticação</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSysProbe</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSysProbe de floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar XSysProbe de floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Sinalizador de Autenticação</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Antispam</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Antispam</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Antispam</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Antispam</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar propriedades estendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar propriedades estendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar propriedades estendidas de XMessageContext</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar índice Fast de XMessageContext</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar índice Fast de XMessageContext</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar índice Fast de XMessageContext</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Limite de Tamanho da Mensagem</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Limite de Tamanho da Mensagem</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Limite de Tamanho da Mensagem</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Ignorar Limite de Tamanho da Mensagem</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos da Organização</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos da Organização</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Cabeçalhos da Organização</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar XMessageContext do cache de destinatários do AD</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar XMessageContext do cache de destinatários do AD</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar XMessageContext do cache de destinatários do AD</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens ao Servidor</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens ao Servidor</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens ao Servidor</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Mensagens ao Servidor</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Remetente de Domínio Autoritativo</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Remetente de Domínio Autoritativo</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Remetente de Domínio Autoritativo</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Aceitar Remetente de Domínio Autoritativo</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
</tbody>
</table>


## Criação do Conector de Envio SMTP

A tabela a seguir exibe as permissões definidas na criação de conectores de Envio.

### Nome distinto do objeto: CN=\<Nome do Conector\>,CN=Conexões,CN=\<grupo de roteamento\>,CN=Grupos de Roteamento, CN=\<grupo admin\>,CN=\<organização\>

<table style="width:100%;">
<colgroup>
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
<col style="width: 16%" />
</colgroup>
<thead>
<tr class="header">
<th>Conta</th>
<th>Tipo de ACE</th>
<th>Herança</th>
<th>Permissões</th>
<th>Na propriedade/ Aplicável a</th>
<th>Comentários</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>AUTORIDADE NT\LOGON ANÔNIMO</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos da Organização</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos da Organização</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos da Organização</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos de Floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos de Floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos de Floresta</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar XShadow</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar XShadow</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar XShadow</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-10</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p>Esse é o SID conhecido para servidores parceiros.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Cabeçalhos de Roteamento</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para Servidores do Exchange Herdados.</p></td>
</tr>
<tr class="odd">
<td><p>Servidores do Exchange</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Exch50</p></td>
<td><p></p></td>
<td><p></p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-21</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Exch50</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Caixa de Correio.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-22</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Exch50</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores de Transporte de Borda.</p></td>
</tr>
<tr class="even">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-23</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Exch50</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para servidores protegidos externamente.</p></td>
</tr>
<tr class="odd">
<td><p>S-1-9-1419165041-1139599005-3936102811-1022490595-24</p></td>
<td><p>ACE de Permissão</p></td>
<td><p>Todos</p></td>
<td><p>Enviar Exch50</p></td>
<td><p></p></td>
<td><p>Este é o SID conhecido para Servidores do Exchange Herdados.</p></td>
</tr>
</tbody>
</table>

