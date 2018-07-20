---
title: 'Habilitar o suporte para agentes de transporte de legado: Exchange 2013 Help'
TOCTitle: Habilitar o suporte para agentes de transporte de legado
ms:assetid: 00617e87-7199-406e-b4a3-94378f657f1f
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/JJ591524(v=EXCHG.150)
ms:contentKeyID: 50484853
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Habilitar o suporte para agentes de transporte de legado

 

_**Aplica-se a:** Exchange Server 2013_

_**Tópico modificado em:** 2015-03-09_

No Microsoft Exchange Server 2013, agentes de transporte criados usando o Microsoft .NET Framework versão 4.0 são suportados por padrão. O Exchange 2013 tem suporte a agentes de transporte criados usando versões anteriores do .NET Framework, mas o suporte a esses agentes de transporte legados não é habilitado por padrão. Para habilitar o suporte a agentes de transporte legados, você precisa modificar o arquivo XML apropriado de configuração de aplicativos. Os arquivos que você precisa modificar dependem de onde o agente de transporte está instalado:


<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Servidor</th>
<th>Arquivos de configuração do aplicativo</th>
<th>Serviço do Microsoft Windows</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Servidor de Acesso para Cliente</p></td>
<td><p>%ExchangeInstallPath%Bin\MSExchangeFrontendTransport.exe.config</p></td>
<td><p>Transporte de Front-End do Microsoft Exchange (MSExchangeFrontendTransport)</p></td>
</tr>
<tr class="even">
<td><p>Servidor de Caixa de Correio</p></td>
<td><ul>
<li><p>%ExchangeInstallPath%Bin\EdgeTransport.exe.config</p></li>
<li><p>%ExchangeInstallPath%Bin\MSExchangeTransport.exe.config</p></li>
</ul></td>
<td><p>Transporte do Microsoft Exchange (MSExchangeTransport)</p></td>
</tr>
</tbody>
</table>


O suporte a agentes de transporte legados é controlado por chaves nos arquivos de configuração do aplicativo. Por padrão, nenhuma das chaves exigidas está presente nos arquivos de configuração do aplicativo. Você deve adicionar manualmente as chaves. A tabela a seguir explica cada parâmetro com mais detalhes.


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tecla</th>
<th>Descrição</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><em>useLegacyV2RuntimeActivationPolicy</em></p></td>
<td><p>Essa chave ativa ou desativa o suporte para os agentes de transporte legado. Os valores válidos para este parâmetro são <code>true</code> ou <code>false</code>. Se essa chave não for especificada, o valor padrão será <code>false</code>.</p></td>
</tr>
<tr class="even">
<td><p><em>supportedRuntime version</em></p></td>
<td><p>Essa chave especifica a versão do Microsoft .NET Framework exigida pelo agente. Os valores válidos para essa chave são:</p>
<ul>
<li><p><code>v4.0</code> ou <code>v4.0.30319</code></p></li>
<li><p><code>v3.5</code> ou <code>v3.5.21022</code></p></li>
<li><p><code>v3.0</code> ou <code>v3.0.4506</code></p></li>
<li><p><code>v2.0</code> ou <code>v2.0.50727</code></p></li>
</ul>
<p>Você especifica vários valores usando diversas instâncias separadas da chave <em>supportedRuntime version</em>.</p>
<p>Ao habilitar o suporte a agente de transporte legado usando a chave <em>useLegacyV2RuntimeActivationPolicy</em>, você sempre deve especificar o valor <code>v4.0</code>, além dos valores exigidos pelo agente de transporte legado.</p></td>
</tr>
</tbody>
</table>


## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: 15 minutos

  - Permissões do Exchange não se aplicam aos procedimentos neste tópico. Esses procedimentos são realizados no sistema operacional do Exchange Server.

  - As mudanças que você salvar no arquivo de configuração de um aplicativo serão aplicadas após a reinicialização do serviço correspondente.

  - Quando você reinicia qualquer serviço associado aos arquivos de configuração de aplicativos, o fluxo de email no servidor é interrompido temporariamente.

  - Quaisquer configurações personalizadas em cada servidor feitas nos arquivos de configuração de aplicativo XML do Exchange, por exemplo, os arquivos web.config em servidores de acesso para cliente ou o arquivo EdgeTransport.exe.config em servidores de Caixa de Correio, são substituídos quando você instala uma Atualização Cumulativa do Exchange (CU). Não deixe de salvar essas informações para poder reconfigurar facilmente o servidor após a instalação. Você deve redefinir essas configurações depois de instalar uma Atualização Cumulativa.

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Usar o Prompt de comando para configurar o suporte para os agentes de transporte legado

Use o procedimento a seguir para habilitar o suporte para os agentes de transporte legado:

1.  Em uma janela do Prompt de comando, no servidor do Exchange 2013 no qual você deseja configurar o suporte a agente de transporte legado, abra o arquivo de configuração de aplicativo apropriado no Bloco de Notas executando o seguinte comando:
    
        Notepad %ExchangeInstallPath%Bin\<AppConfigFile>
    
    Por exemplo, para abrir o arquivo de configuração EdgeTransport.exe em um servidor de Caixa de Correio, execute o seguinte comando:
    
        Notepad %ExchangeInstallPath%Bin\EdgeTransport.exe.config

2.  Localize a chave *\</configuration\>* no fim do arquivo e cole as seguintes chaves antes da chave *\</configuration\>*:
    
        <startup useLegacyV2RuntimeActivationPolicy="true">
           <supportedRuntime version="v4.0" />
           <supportedRuntime version="v3.5" />
           <supportedRuntime version="v3.0" />
           <supportedRuntime version="v2.0" />
        </startup>

3.  Quando tiver terminado, salve e feche o arquivo de configuração do aplicativo.

4.  Repita as etapas de 1 a 3 para modificar os outros arquivos de configuração de aplicativo.

5.  Reinicie o serviço associado do Windows executando o seguinte comando:
    
        net stop <service> && net start <service>
    
    Por exemplo, se você modificar o arquivo EdgeTransport.exe.config, terá que reiniciar o serviço Transporte do Microsoft Exchange executando o seguinte comando:
    
        net stop MSExchangeTransport && net start MSExchangeTransport

6.  Repita a etapa 5 para reiniciar os serviços associados aos outros arquivos de configuração de aplicativo modificados.

## Como saber se funcionou?

Você vai saber que este procedimento funciona se o agente de transporte legado for instalado com êxito. Se tentar instalar um agente de transporte legado sem seguir os procedimentos deste tópico, você receberá um erro semelhante ao seguinte:

    Mixed mode assembly is built against version '<version>' of the runtime and cannot be loaded in the 4.0 runtime without additional configuration information.

