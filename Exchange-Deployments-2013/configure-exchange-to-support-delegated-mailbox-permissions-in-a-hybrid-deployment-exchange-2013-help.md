---
title: 'Configurar o Exchange para oferecer suporte à caixa de correio delegada permissões em uma implantação híbrida: Exchange 2013 Help'
TOCTitle: Configurar o Exchange para oferecer suporte à caixa de correio delegada permissões em uma implantação híbrida
ms:assetid: a2a10cb3-4557-4ff5-8191-c653522f4512
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Mt784505(v=EXCHG.150)
ms:contentKeyID: 74447326
ms.date: 05/23/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Configurar o Exchange para oferecer suporte à caixa de correio delegada permissões em uma implantação híbrida

 

_<strong>Tópico modificado em:</strong>2018-01-30_

Permissões de caixa de correio delegada permitem que alguém para gerenciar alguma parte da caixa de correio de usuários para outro. Um exemplo comum disso é um assistente administrativo que precisa gerenciar caixas de correio e calendário de um executivo. Implantações híbridas entre uma organização do Exchange no local e o Office 365 suporte o **Acesso total** e a **Enviar em nome de** delegada permissões de caixa de correio. No entanto, dependendo da versão do Exchange que você instalou em sua organização local, você pode precisar executar configurações adicionais para usar a caixa de correio delegada permissões em uma implantação híbrida. O exemplo a seguir lista as versões do Exchange que suporte delegada permissões de caixa de correio em uma implantação híbrida e se a configuração adicional será necessária para essa versão.

  - **Exchange 2016** Nenhuma configuração adicional é necessária.

  - **Exchange 2013** Uma atualização do Exchange 2013 cumulativa (CU) de suporte e configuração adicionais são necessários.

  - **O Exchange 2010** Uma atualização com suporte do Exchange 2010 rolo (RU) e configuração adicionais são necessários.

Para obter mais informações sobre os requisitos específicos para oferecer suporte a caixa de correio delegada permissões em uma implantação híbrida, dê uma olhada em [Permissões em implantações híbridas do Exchange](permissions-in-exchange-hybrid-deployments-exchange-2013-help.md).

As seções a seguir passam você pela configuração do Exchange 2013 e Exchange 2010 implantações para habilitar o suporte para permissões de caixa de correio delegada local. Antes de seguir estas etapas, você precisará certificar-se de que você está no Exchange 2013 CU ou Exchange SP3 RU mais recente. Para obter mais informações, consulte [Pré-requisitos de implantação híbrida](hybrid-deployment-prerequisites-exchange-2013-help.md).

## Exchange 2013

O que você precisa fazer para habilitar o suporte para permissões de caixa de correio delegada depende de alguns fatores. Se você moveu as caixas de correio para o Office 365 e no momento:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>O exemplo a seguir foi instalado …</th>
<th>E a sincronização de objetos ACLable da organização foi …</th>
<th>Em seguida, você precisa …</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>A CU9 do Exchange 2013 ou anterior</p></td>
<td><p>Esse recurso não está disponível no Exchange 2013 CU9 e anteriores.</p></td>
<td><p>Configurar manualmente a cada caixa de correio para oferecer suporte a ACLs</p></td>
</tr>
<tr class="even">
<td><p>Exchange 2013 CU10 ou posterior</p></td>
<td><p>Desabilitado</p></td>
<td><ol>
<li><p>Habilitar a sincronização do objeto ACLable no nível da organização</p></li>
<li><p>Habilite manualmente as ACLs em cada caixa de correio movidas para o Office 365 antes da sincronização do objeto ACLable foi habilitada no nível da organização.</p></li>
</ol>
<p>Nenhuma configuração adicional é necessária para caixas de correio movidas para o Office 365 após a sincronização de objetos ACLable está habilitada no nível da organização.</p></td>
</tr>
<tr class="odd">
<td><p>Exchange 2013 CU10 ou posterior</p></td>
<td><p>Habilitado</p></td>
<td><p>Nenhuma configuração adicional é necessária</p></td>
</tr>
</tbody>
</table>


## Habilitar a sincronização do objeto ACLable

Para habilitar a sincronização de objeto ACLable no nível da organização, faça o seguinte.

1.  Instale a versão mais recente do Azure Active Directory Connect (conexão AAD) em todos os servidores AAD se conectar. Isso é necessário para permitir que AAD conectar sincronizar os atributos necessários para dar suporte a permissões híbrida. Você pode baixar o AAD conectar do [Microsoft Azure Active Directory Connect](http://go.microsoft.com/fwlink/p/?linkid=510956).

2.  Abra o Shell de gerenciamento do Exchange em um servidor executando o mais recente disponível Exchange 2013 CU ou a CU imediatamente anterior.

3.  Execute o seguinte comando.
    
        Set-OrganizationConfig -ACLableSyncedObjectEnabled $True

Depois que você fizer isso, qualquer caixa de correio que podem ser movidos para o Office 365 será configurada corretamente para oferecer suporte à caixa de correio delegada permissões. Se as caixas de correio foram movidas para o Office 365 antes de concluir essas etapas, você precisará habilitar manualmente as ACLs nessas caixas de correio usando as etapas em Habilitar ACLs em caixas de correio remotas.


> [!IMPORTANT]
> ACLs não serão habilitadas em caixas de correio remotas criadas no Office 365. Se você criar uma caixa de correio remota no Office 365, você precisará siga as etapas nas ACLs habilitar na seção de caixas de correio remotas para permitir que as ACLs nessa caixa de correio remota. Para evitar essa etapa extra, recomendamos que você crie a caixa de correio em um servidor do Exchange no local e mova a caixa de correio para o Office 365.



## Habilitar as ACLs em caixas de correio remotas

Para habilitar as ACLs em caixas de correio movidas para o Office 365 antes da sincronização do objeto ACLable foi habilitada no nível da organização, faça o seguinte.

1.  Abra o Shell de gerenciamento do Exchange em um servidor executando o mais recente disponível Exchange 2013 CU ou a CU imediatamente anterior.

2.  Para habilitar as ACLs em uma única caixa de correio, execute o seguinte comando.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Para habilitar as ACLs em todas as caixas de correio movidas para o Office 365, execute o seguinte comando.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  Para verificar se as caixas de correio foram atualizadas com êxito, execute o seguinte comando.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

## Exchange 2010

Servidores Exchange 2010 SP3 suportam a configuração de ACLs em caixas de correio remotas, no entanto, essa configuração deve ser definido manualmente em cada caixa de correio. Diferentemente das versões mais recentes do Exchange, o Exchange 2010 não oferece a capacidade de definir esse recurso no nível da organização. Você precisa seguir as etapas abaixo em qualquer caixa de correio que você moveu anteriormente para o Office 365 e em qualquer caixa de correio que serão movidas de um servidor Exchange 2010 SP3 para o Office 365 no futuro.

## Habilitar as ACLs em caixas de correio remotas

Para habilitar as ACLs em caixas de correio movidas para o Office 365, faça o seguinte.

1.  Abra o Shell de gerenciamento do Exchange em um servidor executando o mais recente disponível Exchange 2010 SP3 RU ou o RU imediatamente anterior.

2.  Para habilitar as ACLs em uma única caixa de correio, execute o seguinte comando.
    
        Get-AdUser <Identity> | Set-AdObject -Replace @{msExchRecipientDisplayType=-1073741818}

3.  Para habilitar as ACLs em todas as caixas de correio movidas para o Office 365, execute o seguinte comando.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid | Set-ADObject -Replace @{msExchRecipientDisplayType=-1073741818}}

4.  Para verificar se as caixas de correio foram atualizadas com êxito, execute o seguinte comando.
    
        Get-RemoteMailbox | ForEach { Get-AdUser -Identity $_.Guid -Properties msExchRecipientDisplayType | Format-Table -AutoSize DistinguishedName, msExchRecipientDisplayType}

