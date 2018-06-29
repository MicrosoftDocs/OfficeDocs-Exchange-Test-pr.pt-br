---
title: 'Exportar resultados de pesquisa de Descoberta Eletrônica para um arquivo PST: Exchange 2013 Help'
TOCTitle: Exportar resultados de pesquisa de Descoberta Eletrônica para um arquivo PST
ms:assetid: bc47f5f9-d056-4b69-b669-ae65fad541c8
ms:mtpsurl: https://technet.microsoft.com/pt-br/library/Dn440164(v=EXCHG.150)
ms:contentKeyID: 59635841
ms.date: 05/22/2018
mtps_version: v=EXCHG.150
ms.translationtype: MT
---

# Exportar resultados de pesquisa de Descoberta Eletrônica para um arquivo PST

 

_**Aplica-se a:**Exchange Online, Exchange Server 2013_

_**Tópico modificado em:**2017-09-07_

Você pode usar a ferramenta de exportação de descoberta eletrônica no Centro de administração do Exchange (EAC) para exportar os resultados de uma pesquisa de descoberta eletrônica In-loco para um arquivo de dados do Outlook, que também é chamado de um arquivo PST. Os administradores podem distribuir os resultados da pesquisa para outras pessoas dentro da organização, como um gerente de recursos humanos ou um gerente de registros, ou opostas advogado em um caso jurídico. Depois que os resultados da pesquisa são exportados para um arquivo PST, você ou outros usuários podem abri-los no Outlook para analisar ou imprimir mensagens retornadas nos resultados da pesquisa. Arquivos PST também podem ser abertos no eDiscovery de terceiros e relatórios de aplicativos. Este tópico mostra como fazer isso, bem como solucionar quaisquer problemas que talvez seja necessário.

## O que você precisa saber antes de começar?

  - Tempo estimado para conclusão: O tempo irá variar conforme a quantidade e o tamanho dos resultados da pesquisa que será exportada.

  - Para executar este procedimento ou estes procedimentos, você precisa receber permissões. Para ver de que permissões você precisa, consulte o Entrada "In-Place eDiscovery" no tópico [Permissões de política e conformidade de mensagens](messaging-policy-and-compliance-permissions-exchange-2013-help.md) .

  - O computador usado para exportar os resultados da pesquisa para um arquivo PST deve atender aos seguintes requisitos de sistema:
    
      - versões de 32 ou 64 bits do Windows 7 e versões posteriores
    
      - Microsoft .NET Framework 4.7
    
      - Um navegador com suporte:
        
          - Internet Explorer 10 e versões posteriores
            
            OU
        
          - Mozilla Firefox ou Google Chrome. Se você usar qualquer um desses navegadores, certifique-se de que você instala a extensão de *ClickOnce* . Para instalar o suplemento do ClickOnce, consulte [Mozilla ClickOnce complementos](https://addons.mozilla.org/en-us/firefox/search/?q=clickonce%26cat=1%2c0%26appver=%26platform=) ou [ClickOnce para Google Chrome](https://chrome.google.com/webstore/search/clickonce?_category=extensions).

  - Você precisa de uma caixa de correio ativa associada à conta que deseja exportar.

  - Certifique-se de que as configurações de Intranet local são corretamente configurados no Internet Explorer. Certifique-se de que **https://\*.outlook.com** é adicionada à zona da intranet Local.

  - Verifique se que as seguintes URLS não estão listadas na zona sites confiáveis:
    
      - https://\*.outlook.com
    
      - https://r4.res.outlook.com
    
      - https://\*.res.outlook.com

  - Para informações sobre atalhos de teclado que possam se aplicar aos procedimentos neste tópico, consulte [Atalhos de teclado no Centro de administração do Exchange](keyboard-shortcuts-in-the-exchange-admin-center-exchange-online-protection-help.md).


> [!TIP]
> Está enfrentando problemas? Peça ajuda nos fóruns do Exchange. Visite os fóruns em: <A href="https://go.microsoft.com/fwlink/p/?linkid=60612">Exchange Server</A>, <A href="https://go.microsoft.com/fwlink/p/?linkid=267542">Exchange Online</A>, ou <A href="https://go.microsoft.com/fwlink/p/?linkid=285351">Proteção do Exchange Online</A>.



## Use o Centro de administração do Exchange para exportar os resultados da pesquisa de descoberta eletrônica In-loco para um PST

1.  Vá em **Gerenciamento de conformidade** \> **Descoberta Eletrônica In-loco & bloquear**.

2.  Na exibição de lista, selecione a pesquisa de Descoberta Eletrônica In-Loco da você deseja exportar os resultados e depois clique em **Exportar para um arquivo PST**.
    
    ![Exportar para um arquivo PST](images/Dn440164.1ebee2ac-89b3-49fa-b70c-a07c9a65f958(EXCHG.150).gif "Exportar para um arquivo PST")  

3.  Na janela **Ferramenta de Exportação de PST de Descoberta Eletrônica**, faça o seguinte:
    
      - Clique em **Procurar** para especificar o local para o qual você deseja baixar o arquivo PST.
    
      - Clique na caixa de seleção **Habilitar deduplicação** para excluir as mensagens duplicadas. Somente uma única instância de uma mensagem será incluída no arquivo PST.
    
      - Clique na caixa de seleção **Incluir itens não pesquisáveis** para incluir itens da caixa de correio que não puderam ser pesquisados (por exemplo, mensagens com anexos dos tipos de arquivo que não puderam ser indexadas pela Pesquisa do Exchange). Os itens não pesquisáveis são exportados para um arquivo PST separado.
        

        > [!IMPORTANT]
        > A inclusão de itens não pesquisáveis, quando você exporta resultados de pesquisa do eDiscovery, demora mais quando as caixas de correio contêm muitos itens não pesquisáveis. Para reduzir o tempo necessário à exportação de resultados de pesquisa e evitar arquivos de exportação PST grandes, considere as seguintes recomendações: 
        > <UL>
        > <LI>
        > <P>Crie várias pesquisas de eDiscovery para que cada uma delas pesquise um menor número de caixas de correio de origem.</P>
        > <LI>
        > <P>Se quiser exportar todo o conteúdo da caixa de correio em um intervalo específico de datas (não especificando palavras-chave nos critérios de pesquisa), então todos os itens não pesquisáveis pertencentes a esse intervalo de datas serão automaticamente incluídos nos resultados de pesquisa. Portanto, não marque a caixa de seleção <STRONG>Incluir itens não pesquisáveis</STRONG>.</P></LI></UL>



4.  Clique em **Iniciar** para exportar os resultados da pesquisa para um arquivo PST.
    
    Uma janela é exibida contendo as informações do status sobre o processo de exportação.

## Mais informações

  - Você pode reduzir o tamanho do fileby de exportação de PST exportando apenas os itens não pesquisáveis. Para fazer isso, criar ou editar uma pesquisa, especifique uma data de início no futuro e remova qualquer palavra-chave na caixa **palavras-chave**. Isto resultará em nenhuma resultados de pesquisa estão sendo retornados. Quando você copiar ou exporta os resultados da pesquisa e selecione a caixa de seleção **incluir itens não pesquisáveis**, apenas os itens não pesquisáveis serão copiados para a caixa de correio de descoberta ou exportados para um arquivo PST.

  - Se você habilitou a deduplicação, todos os resultados da pesquisas serão exportados em um único arquivo PST. Se você não habilitou a deduplicação, um arquivo PST separado é exportado para cada caixa de correio incluída na pesquisa. E conforme citado anteriormente, os itens não pesquisáveis são exportados para um arquivo PST separado.

  - Além dos arquivos PST que possuem os resultados da pesquisa, dois outros arquivos também são exportados:
    
      - Um arquivo de configuração (arquivo no formato .txt) que contém informações sobre a solicitação de exportação de PST, tais como o nome da pesquisa de Descoberta Eletrônica que foi exportada, a data e a hora da exportação, se a deduplicação e os itens não pesquisáveis foram habilitados, a consulta da pesquisa, e as caixas de correio de origem que foram pesquisadas.
    
      - Um log de resultados da pesquisa (arquivo no formato .csv) que contém uma entrada para cada mensagem retornada nos resultados da pesquisa. Cada entrada identifica a caixa de correio de origem onde a mensagem está localizada. Se você habilitou a deduplicação, isto ajuda a identificar todas as caixas de correio que possuem mensagem duplicada.

  - O nome da pesquisa é a primeira parte do nome do arquivo para cada arquivo que é exportado. Além disso, a data e a hora da solicitação de exportação é anexada ao nome do arquivo de cada arquivo PST e no log de resultados.

  - Para saber mais sobre desduplicação e itens não pesquisáveis, veja:
    
      - [Estimate, preview, and copy search results](in-place-ediscovery-exchange-2013-help.md)
    
      - [Itens não pesquisáveis na descoberta eletrônica do Exchange](unsearchable-items-in-exchange-ediscovery-exchange-2013-help.md)

  - Para exportar os resultados da pesquisa de descoberta eletrônica do Centro de descoberta eletrônica no SharePoint ou SharePoint Online, consulte [Exportar conteúdo do eDiscovery e criar relatórios](https://go.microsoft.com/fwlink/p/?linkid=324757).

## Solução de problemas


<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Sintoma</th>
<th>Causa possível</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Não é possível exportar para um arquivo PST.</p></td>
<td><ul>
<li><p>Não há nenhuma caixa de correio ativa associada à conta. Para exportar um arquivo PST, você deve ter uma conta ativa.</p></li>
<li><p>Sua versão do Internet Explorer está desatualizada. Tente a IE atualizando a versão 10 ou posterior. Ou tente outro navegador.</p></li>
<li><p>Critérios de pesquisa inseridos na consulta de <strong>filtro com base nos critérios</strong> está incorreta. Por exemplo, um nome de usuário é inserida em vez de um endereço de email. Para obter mais informações sobre como filtrar com base nos critérios, consulte <a href="modify-an-in-place-ediscovery-search-exchange-2013-help.md">Modificar uma pesquisa de descoberta eletrônica In-loco</a>.</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p>Não é possível exportar os resultados de pesquisa em uma máquina específica. Exporte funciona conforme o esperado em uma máquina diferente.</p></td>
<td><p>As credenciais do Windows erradas foram salvos no <strong>Gerenciador de credenciais</strong>. Desmarque suas credenciais e fazer logon novamente.</p></td>
</tr>
<tr class="odd">
<td><p>a ferramenta de exportação de PST do eDiscovery não será iniciada.</p></td>
<td><p>Configurações de zona da intranet local não estão configuradas corretamente no Internet Explorer. Certifique-se de que *. outlook.com, *. office365, *. sharepoint.com e *. onmicrosoft.com são adicionados aos sites confiável de zona da intranet Local.</p>
<p>Para adicionar esses sites à zona confiáveis no Internet Explorer, consulte <a href="https://windows.microsoft.com/en-us/windows/security-zones-adding-removing-websites#1tc=windows-7">zonas de segurança: adicionando ou removendo sites</a>.</p></td>
</tr>
</tbody>
</table>

