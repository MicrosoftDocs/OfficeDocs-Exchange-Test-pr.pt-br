---
title: 'Componente do IIS 7 não installed_LonghornIIS7HttpCompressionDynamicNotInstalled: Exchange 2013 Help'
TOCTitle: Componente do IIS 7 não installed_LonghornIIS7HttpCompressionDynamicNotInstalled
ms:assetid: d909e329-2436-43f9-af75-a5ee14e67ebf
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/ms.exch.setupreadiness.longhorniis7httpcompressiondynamicnotinstalled(v=EXCHG.150)
ms:contentKeyID: 50486764
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Componente do IIS 7 não installed\_LonghornIIS7HttpCompressionDynamicNotInstalled

 

_**Aplica-se a:**Exchange Server_

_**Tópico modificado em:**2015-03-09_

O conteúdo neste tópico não foi atualizado para o Microsoft Exchange Server 2013. Mesmo assim, ele ainda pode se aplicar ao Exchange 2013. Se você ainda precisar de ajuda, verifique os recursos da comunidade, abaixo.

Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: [Exchange Server](https://go.microsoft.com/fwlink/p/?linkid=60612), [Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=267542), ou [Proteção do Exchange Online](https://go.microsoft.com/fwlink/p/?linkid=285351).

Instalação do Microsoft Exchange Server 2010 ou a instalação do Microsoft Exchange Server 2007 não pode instalar a função de servidor acesso para cliente (CAS) ou a função de servidor de caixa de correio em um computador baseado no Microsoft Windows Server 2008 ou em um computador baseado no Windows Server 2008 R2 porque os componentes de servidor de informações da Internet (IIS) 7 necessários não estão instalados.

A instalação do Exchange 2010 e o programa de instalação do Exchange 2007 exigem que o computador baseado no Windows Server 2008 ou o computador baseado no Windows Server 2008 R2, em que você está instalando a função de CAS já tem os seguintes componentes IIS 7 instalados.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Componentes necessários do IIS 7 para a função de servidor CAS</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Compressão de Conteúdo Dinâmico</p></td>
</tr>
<tr class="even">
<td><p>Compressão de Conteúdo Estático</p></td>
</tr>
<tr class="odd">
<td><p>Autenticação básica</p></td>
</tr>
<tr class="even">
<td><p>Autenticação do Windows</p></td>
</tr>
<tr class="odd">
<td><p>Autenticação Digest 7 do IIS</p></td>
</tr>
<tr class="even">
<td><p>ASP.NET</p></td>
</tr>
<tr class="odd">
<td><p>Mapeamento de certificado de cliente</p></td>
</tr>
<tr class="even">
<td><p>Pesquisa no diretório</p></td>
</tr>
<tr class="odd">
<td><p>Erros de HTTP</p></td>
</tr>
<tr class="even">
<td><p>Log HTTP</p></td>
</tr>
<tr class="odd">
<td><p>Redirecionamento HTTP</p></td>
</tr>
<tr class="even">
<td><p>Rastreamento</p></td>
</tr>
<tr class="odd">
<td><p>Filtros ISAPI</p></td>
</tr>
<tr class="even">
<td><p>Monitor de solicitações</p></td>
</tr>
<tr class="odd">
<td><p>Conteúdo Estático</p></td>
</tr>
</tbody>
</table>


A instalação do Exchange 2010 e o programa de instalação do Exchange 2007 exigem que o computador baseado no Windows Server 2008 ou o computador baseado no Windows Server 2008 R2, em que você está instalando a função de servidor de caixa de correio já tem os seguintes componentes IIS 7 instalados.


<table>
<colgroup>
<col style="width: 100%" />
</colgroup>
<thead>
<tr class="header">
<th><strong>Componentes necessários do IIS 7 para a função de servidor de caixa de correio</strong></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Autenticação básica</p></td>
</tr>
<tr class="even">
<td><p>Autenticação do Windows</p></td>
</tr>
</tbody>
</table>


Para resolver esse problema, siga as etapas apropriadas para instalar os componentes necessários do IIS 7 no computador de destino e, em seguida, execute novamente o programa de instalação do Microsoft Exchange.

Instalar os componentes do IIS 7 para a função de servidor CAS, usando o Gerenciador do servidor do Windows Server 2008

1.  Clique em **Iniciar**, clique em **Ferramentas Administrativas** e em **Gerenciador do Servidor**.

2.  No painel de navegação, expanda **funções**, clique com o botão **Servidor da Web (IIS)** e clique em **Adicionar serviços de função**.

3.  No painel **Selecionar Serviços de função**, role para baixo até o **IIS**.

4.  Na área de **segurança**, clique para selecionar as caixas de seleção a seguintes:
    
      - **Autenticação básica**
    
      - **Autenticação Digest**
    
      - **Autenticação do Windows**

5.  Na área de **desempenho**, clique para selecionar as caixas de seleção a seguintes:
    
      - **Compactação estática**
    
      - **Compactação dinâmica**

6.  No painel **Selecionar Serviços de função**, clique em **Avançar** e, em seguida, clique em **instalar** no painel **Confirmar seleções de instalações**.

7.  Clique em **Fechar** para sair do assistente Adicionar serviços de função.

Instalar os componentes do IIS 7 para a função de servidor de caixa de correio usando o Gerenciador do servidor do Windows Server 2008

1.  Clique em **Iniciar**, clique em **Ferramentas Administrativas** e em **Gerenciador do Servidor**.

2.  No painel de navegação, expanda **funções**, clique com o botão **Servidor da Web (IIS)** e clique em **Adicionar serviços de função**.

3.  No painel **Selecionar Serviços de função**, role para baixo até o **IIS**.

4.  Na área de **segurança**, clique para selecionar as caixas de seleção a seguintes:
    
      - **Autenticação básica**
    
      - **Autenticação do Windows**

5.  No painel **Selecionar Serviços de função**, clique em **Avançar** e, em seguida, clique em **instalar** no painel **Confirmar seleções de instalações**.

6.  Clique em **Fechar** para sair do assistente Adicionar serviços de função.

