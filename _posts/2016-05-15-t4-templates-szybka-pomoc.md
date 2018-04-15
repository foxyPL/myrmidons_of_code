---
id: 163
title: 'T4 Templates &#8211; Szybka pomoc'
date: 2016-05-15T10:23:03+00:00
author: Łukasz Zaborski
layout: post
guid: http://www.siepaczekodu.pl/?p=163
permalink: /2016/05/15/t4-templates-szybka-pomoc/
image: /wp-content/uploads/2016/05/awhCbhLqRceCdjcPQUnn_IMG_0249.jpg
categories:
  - 'C#'
  - Visual Studio
---
Zakładając bloga miałem postanowienie publikować nowy wpis przynajmniej raz na dwa tygodnie. No ale tu praca magisterska, tu piwko&#8230; o zrobiło się cieplej to wyskoczę na rower 😛 Jak skończę pracę nad częścią pisemną magisterki na pewno będę chciał przedstawić na blogu przykłady wykorzystania biblioteki SignalR o której wcześniej <a href="http://www.siepaczekodu.pl/2016/03/02/signalr-pierwsze-starcie/" target="_blank">pisałem</a>.

Dziś chciałem krótko opisać narzędzie T4 Templates które ułatwiło mi prace podczas tworzenia skryptu zasilającego tabele w bazie danych. Tabela przechowuje wartości słownikowe.

[<img class="aligncenter size-full wp-image-164" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/05/DictionaryTable.png" alt="DictionaryTable" width="403" height="172" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2016/05/DictionaryTable.png 403w, http://www.siepaczekodu.pl/wp-content/uploads/2016/05/DictionaryTable-300x128.png 300w" sizes="(max-width: 403px) 100vw, 403px" />](http://www.siepaczekodu.pl/wp-content/uploads/2016/05/DictionaryTable.png)

Dane według których miałem przygotować skrypt znajdowały się w tabeli w dokumencie docx. Jako że było ich dużo nie uśmiechało mi się ręcznie kopiować pojedynczo każdego wiersza i wprowadzać kolejno wpisu

<pre class="EnlighterJSRAW" data-enlighter-language="sql">IF NOT EXISTS (SELECT TOP 1 * FROM dbo.Dictionary WHERE [key] = '59')
  INSERT INTO dbo.Dictionary ([key], [value], [description]) VALUES ( '59', 'item 6', ' Description Description Description 5')
GO</pre>

Wtedy przypomniałem sobie o szablonach T4. Szablony te składają się z bloku tekstu oraz części w której znajduję się kod. Po zapisie takiego szablonu logika znajdująca się w kodzie jest wywoływana i tworzony jest plik z rozszerzeniem zadeklarowanym w szablonie. Szybka lektura <a href="https://msdn.microsoft.com/en-us/library/bb126445.aspx" target="_blank">dokumentacji</a>, tworze nowy plik i szablonik gotowy 🙂

[<img class="aligncenter size-full wp-image-176" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/05/addTT.png" alt="addTT" width="785" height="444" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2016/05/addTT.png 785w, http://www.siepaczekodu.pl/wp-content/uploads/2016/05/addTT-300x170.png 300w, http://www.siepaczekodu.pl/wp-content/uploads/2016/05/addTT-768x434.png 768w" sizes="(max-width: 785px) 100vw, 785px" />](http://www.siepaczekodu.pl/wp-content/uploads/2016/05/addTT.png)

<div id="gist39109325" class="gist">
  <div class="gist-file">
    <div class="gist-data">
      <div class="js-gist-file-update-container js-task-list-container file-box">
        <div id="file-insertdictionary-tt" class="file">
          <div itemprop="text" class="blob-wrapper data type-text">
            <table class="highlight tab-size js-file-line-container" data-tab-size="8">
              <tr>
                <td id="file-insertdictionary-tt-L1" class="blob-num js-line-number" data-line-number="1">
                </td>
                
                <td id="file-insertdictionary-tt-LC1" class="blob-code blob-code-inner js-file-line">
                  <#@ template language="C#" #>
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L2" class="blob-num js-line-number" data-line-number="2">
                </td>
                
                <td id="file-insertdictionary-tt-LC2" class="blob-code blob-code-inner js-file-line">
                  <#@ output extension=".sql" #>
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L3" class="blob-num js-line-number" data-line-number="3">
                </td>
                
                <td id="file-insertdictionary-tt-LC3" class="blob-code blob-code-inner js-file-line">
                  <#@ assembly name="$(ProjectDir)bin\Debug\SiepaczeKoduSample.Infrastructure.dll" #>
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L4" class="blob-num js-line-number" data-line-number="4">
                </td>
                
                <td id="file-insertdictionary-tt-LC4" class="blob-code blob-code-inner js-file-line">
                  <#@ import namespace="System.Collections.Generic" #>
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L5" class="blob-num js-line-number" data-line-number="5">
                </td>
                
                <td id="file-insertdictionary-tt-LC5" class="blob-code blob-code-inner js-file-line">
                  <#@ import namespace="SiepaczeKoduSample.Infrastructure" #>
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L6" class="blob-num js-line-number" data-line-number="6">
                </td>
                
                <td id="file-insertdictionary-tt-LC6" class="blob-code blob-code-inner js-file-line">
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L7" class="blob-num js-line-number" data-line-number="7">
                </td>
                
                <td id="file-insertdictionary-tt-LC7" class="blob-code blob-code-inner js-file-line">
                  <#
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L8" class="blob-num js-line-number" data-line-number="8">
                </td>
                
                <td id="file-insertdictionary-tt-LC8" class="blob-code blob-code-inner js-file-line">
                  IList<Dictionary> dictionary = TemplateHelper.GetDictionary(@"C:\Users\Zaba\Pictures\SiepaczeKodu\Dictionary.csv");
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L9" class="blob-num js-line-number" data-line-number="9">
                </td>
                
                <td id="file-insertdictionary-tt-LC9" class="blob-code blob-code-inner js-file-line">
                  #>
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L10" class="blob-num js-line-number" data-line-number="10">
                </td>
                
                <td id="file-insertdictionary-tt-LC10" class="blob-code blob-code-inner js-file-line">
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L11" class="blob-num js-line-number" data-line-number="11">
                </td>
                
                <td id="file-insertdictionary-tt-LC11" class="blob-code blob-code-inner js-file-line">
                  <#foreach (var item in dictionary)
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L12" class="blob-num js-line-number" data-line-number="12">
                </td>
                
                <td id="file-insertdictionary-tt-LC12" class="blob-code blob-code-inner js-file-line">
                  {
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L13" class="blob-num js-line-number" data-line-number="13">
                </td>
                
                <td id="file-insertdictionary-tt-LC13" class="blob-code blob-code-inner js-file-line">
                  #>
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L14" class="blob-num js-line-number" data-line-number="14">
                </td>
                
                <td id="file-insertdictionary-tt-LC14" class="blob-code blob-code-inner js-file-line">
                  IF NOT EXISTS (SELECT TOP 1 * FROM dbo.Dictionary WHERE [key] = '<#= item.Key #>')
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L15" class="blob-num js-line-number" data-line-number="15">
                </td>
                
                <td id="file-insertdictionary-tt-LC15" class="blob-code blob-code-inner js-file-line">
                  INSERT INTO dbo.Dictionary ([key], [value], [description]) VALUES ( '<#= item.Key #>', '<#= item.Value #>', '<#= item.Description #>')
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L16" class="blob-num js-line-number" data-line-number="16">
                </td>
                
                <td id="file-insertdictionary-tt-LC16" class="blob-code blob-code-inner js-file-line">
                  GO
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L17" class="blob-num js-line-number" data-line-number="17">
                </td>
                
                <td id="file-insertdictionary-tt-LC17" class="blob-code blob-code-inner js-file-line">
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L18" class="blob-num js-line-number" data-line-number="18">
                </td>
                
                <td id="file-insertdictionary-tt-LC18" class="blob-code blob-code-inner js-file-line">
                  <#
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L19" class="blob-num js-line-number" data-line-number="19">
                </td>
                
                <td id="file-insertdictionary-tt-LC19" class="blob-code blob-code-inner js-file-line">
                  }
                </td>
              </tr>
              
              <tr>
                <td id="file-insertdictionary-tt-L20" class="blob-num js-line-number" data-line-number="20">
                </td>
                
                <td id="file-insertdictionary-tt-LC20" class="blob-code blob-code-inner js-file-line">
                  #>
                </td>
              </tr>
            </table>
          </div>
        </div>
      </div>
    </div>
    
    <div class="gist-meta">
      <a href="https://gist.github.com/Zabaa/d7c7617793abdeaf6c56aa3ecd7c9774/raw/2f300dfc5b1ef83246cea9f810b4990dd275d2a9/InsertDictionary.tt" style="float:right">view raw</a> <a href="https://gist.github.com/Zabaa/d7c7617793abdeaf6c56aa3ecd7c9774#file-insertdictionary-tt">InsertDictionary.tt</a> hosted with &#10084; by <a href="https://github.com">GitHub</a>
    </div>
  </div>
  
  <div class="gist-file">
    <div class="gist-data">
      <div class="js-gist-file-update-container js-task-list-container file-box">
        <div id="file-templatehelper-cs" class="file">
          <div itemprop="text" class="blob-wrapper data type-c">
            <table class="highlight tab-size js-file-line-container" data-tab-size="8">
              <tr>
                <td id="file-templatehelper-cs-L1" class="blob-num js-line-number" data-line-number="1">
                </td>
                
                <td id="file-templatehelper-cs-LC1" class="blob-code blob-code-inner js-file-line">
                  <span class="pl-k">public</span> <span class="pl-k">class</span> <span class="pl-en">TemplateHelper</span>
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L2" class="blob-num js-line-number" data-line-number="2">
                </td>
                
                <td id="file-templatehelper-cs-LC2" class="blob-code blob-code-inner js-file-line">
                  {
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L3" class="blob-num js-line-number" data-line-number="3">
                </td>
                
                <td id="file-templatehelper-cs-LC3" class="blob-code blob-code-inner js-file-line">
                  <span class="pl-k">public</span> <span class="pl-k">static</span> <span class="pl-en">IList</span><<span class="pl-en">Dictionary</span>> <span class="pl-en">GetDictionary</span>(<span class="pl-k">string</span> <span class="pl-smi">filePath</span>)
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L4" class="blob-num js-line-number" data-line-number="4">
                </td>
                
                <td id="file-templatehelper-cs-LC4" class="blob-code blob-code-inner js-file-line">
                  {
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L5" class="blob-num js-line-number" data-line-number="5">
                </td>
                
                <td id="file-templatehelper-cs-LC5" class="blob-code blob-code-inner js-file-line">
                  <span class="pl-en">IList</span><<span class="pl-en">Dictionary</span>> <span class="pl-en">dictionary</span>;
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L6" class="blob-num js-line-number" data-line-number="6">
                </td>
                
                <td id="file-templatehelper-cs-LC6" class="blob-code blob-code-inner js-file-line">
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L7" class="blob-num js-line-number" data-line-number="7">
                </td>
                
                <td id="file-templatehelper-cs-LC7" class="blob-code blob-code-inner js-file-line">
                  <span class="pl-k">var</span> <span class="pl-en">csvConfiguration </span>= <span class="pl-k">new</span> <span class="pl-en">CsvConfiguration</span>
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L8" class="blob-num js-line-number" data-line-number="8">
                </td>
                
                <td id="file-templatehelper-cs-LC8" class="blob-code blob-code-inner js-file-line">
                  {
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L9" class="blob-num js-line-number" data-line-number="9">
                </td>
                
                <td id="file-templatehelper-cs-LC9" class="blob-code blob-code-inner js-file-line">
                  Encoding = Encoding.UTF8,
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L10" class="blob-num js-line-number" data-line-number="10">
                </td>
                
                <td id="file-templatehelper-cs-LC10" class="blob-code blob-code-inner js-file-line">
                  CultureInfo = <span class="pl-k">new</span> <span class="pl-en">System</span>.Globalization.CultureInfo(<span class="pl-s"><span class="pl-pds">"</span>pl-PL<span class="pl-pds">"</span></span>)
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L11" class="blob-num js-line-number" data-line-number="11">
                </td>
                
                <td id="file-templatehelper-cs-LC11" class="blob-code blob-code-inner js-file-line">
                  };
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L12" class="blob-num js-line-number" data-line-number="12">
                </td>
                
                <td id="file-templatehelper-cs-LC12" class="blob-code blob-code-inner js-file-line">
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L13" class="blob-num js-line-number" data-line-number="13">
                </td>
                
                <td id="file-templatehelper-cs-LC13" class="blob-code blob-code-inner js-file-line">
                  <span class="pl-k">using</span> (<span class="pl-en">StreamReader</span> <span class="pl-en">reader</span> = File.OpenText(filePath))
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L14" class="blob-num js-line-number" data-line-number="14">
                </td>
                
                <td id="file-templatehelper-cs-LC14" class="blob-code blob-code-inner js-file-line">
                  {
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L15" class="blob-num js-line-number" data-line-number="15">
                </td>
                
                <td id="file-templatehelper-cs-LC15" class="blob-code blob-code-inner js-file-line">
                  <span class="pl-k">using</span>(<span class="pl-k">var</span> <span class="pl-en">csv </span>= <span class="pl-k">new</span> <span class="pl-en">CsvReader</span>(reader, csvConfiguration))
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L16" class="blob-num js-line-number" data-line-number="16">
                </td>
                
                <td id="file-templatehelper-cs-LC16" class="blob-code blob-code-inner js-file-line">
                  {
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L17" class="blob-num js-line-number" data-line-number="17">
                </td>
                
                <td id="file-templatehelper-cs-LC17" class="blob-code blob-code-inner js-file-line">
                  dictionary = csv.GetRecords<Dictionary>().ToList();
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L18" class="blob-num js-line-number" data-line-number="18">
                </td>
                
                <td id="file-templatehelper-cs-LC18" class="blob-code blob-code-inner js-file-line">
                  }
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L19" class="blob-num js-line-number" data-line-number="19">
                </td>
                
                <td id="file-templatehelper-cs-LC19" class="blob-code blob-code-inner js-file-line">
                  }
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L20" class="blob-num js-line-number" data-line-number="20">
                </td>
                
                <td id="file-templatehelper-cs-LC20" class="blob-code blob-code-inner js-file-line">
                  <span class="pl-k">return</span> dictionary;
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L21" class="blob-num js-line-number" data-line-number="21">
                </td>
                
                <td id="file-templatehelper-cs-LC21" class="blob-code blob-code-inner js-file-line">
                  }
                </td>
              </tr>
              
              <tr>
                <td id="file-templatehelper-cs-L22" class="blob-num js-line-number" data-line-number="22">
                </td>
                
                <td id="file-templatehelper-cs-LC22" class="blob-code blob-code-inner js-file-line">
                  }
                </td>
              </tr>
            </table>
          </div>
        </div>
      </div>
    </div>
    
    <div class="gist-meta">
      <a href="https://gist.github.com/Zabaa/d7c7617793abdeaf6c56aa3ecd7c9774/raw/2f300dfc5b1ef83246cea9f810b4990dd275d2a9/TemplateHelper.cs" style="float:right">view raw</a> <a href="https://gist.github.com/Zabaa/d7c7617793abdeaf6c56aa3ecd7c9774#file-templatehelper-cs">TemplateHelper.cs</a> hosted with &#10084; by <a href="https://github.com">GitHub</a>
    </div>
  </div>
</div>

W pierwszej linijce definiujemy z jakiego języka będziemy korzystali podczas tworzenia części logicznej. W kolejnej rozszerzenie pliku który zostanie utworzony po zapisie szablonu, w tym przypadku .sql. Dwie kolejne linijki odpowiadają za załadowanie i zaimportowanie biblioteki z której można korzystać w szablonie. Logika znajduję się miedzy symbolami <# &#8230; #>, to tam wywołuje statyczną metodę GetDictionary znajdującą się w bibliotece SiepaczeKoduSample.Infrastructure.dll.

Metoda pobiera dane z pliku csv którego utworzyłem wcześniej na podstawie tabelki z dokumentu. Plik ten wygląda następująco:

Key,Value,Description
  
55,item 2, Description Description Description 1
  
56,item 3, Description Description Description 2
  
57,item 4, Description Description Description 3
  
58,item 5, Description Description Description 4
  
59,item 6, Description Description Description 5

W bloku tekstowym umieściłem wyrażenia między symbolami <#= &#8230; #>. Po wywołaniu są one konwertowane jako string umieszczony w bloku tekstowym. Po zapisie szablonu zostaje utworzony dokument.

[<img class="size-full wp-image-174 alignnone" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/05/TT.png" alt="TT" width="241" height="111" />](http://www.siepaczekodu.pl/wp-content/uploads/2016/05/TT.png)

<pre class="EnlighterJSRAW" data-enlighter-language="sql">IF NOT EXISTS (SELECT TOP 1 * FROM dbo.Dictionary WHERE [key] = '55')
  INSERT INTO dbo.Dictionary ([key], [value], [description]) VALUES ( '55', 'item 2', ' Description Description Description 1 ')
GO

IF NOT EXISTS (SELECT TOP 1 * FROM dbo.Dictionary WHERE [key] = '56')
  INSERT INTO dbo.Dictionary ([key], [value], [description]) VALUES ( '56', 'item 3', ' Description Description Description 2')
GO

IF NOT EXISTS (SELECT TOP 1 * FROM dbo.Dictionary WHERE [key] = '57')
  INSERT INTO dbo.Dictionary ([key], [value], [description]) VALUES ( '57', 'item 4', ' Description Description Description 3')
GO

IF NOT EXISTS (SELECT TOP 1 * FROM dbo.Dictionary WHERE [key] = '58')
  INSERT INTO dbo.Dictionary ([key], [value], [description]) VALUES ( '58', 'item 5', ' Description Description Description 4')
GO

IF NOT EXISTS (SELECT TOP 1 * FROM dbo.Dictionary WHERE [key] = '59')
  INSERT INTO dbo.Dictionary ([key], [value], [description]) VALUES ( '59', 'item 6', ' Description Description Description 5')
GO</pre>

<div class='sfsi_Sicons' style='width: 100%; display: inline-block; vertical-align: middle; text-align:left'>
  <div style='margin:0px 8px 0px 0px; line-height: 24px'>
    <span>Udostępnij</span>
  </div>
  
  <div class='sfsi_socialwpr'>
    <div class='sf_fb' style='text-align:left;width:98px'>
      <div class="fb-like" href="http://www.siepaczekodu.pl/2016/05/15/t4-templates-szybka-pomoc/" width="180" send="false" showfaces="false"  action="like" data-share="true"data-layout="button" >
      </div>
    </div>
    
    <div class='sf_twiter' style='text-align:left;float:left;width:auto'>
      <a href="http://twitter.com/share" data-count="none" class="sr-twitter-button twitter-share-button" lang="en" data-url="http://www.siepaczekodu.pl/2016/05/15/t4-templates-szybka-pomoc/" data-text="T4 Templates &#8211; Szybka pomoc" ></a>
    </div>
    
    <div class='sf_google' style='text-align:left;float:left;max-width:62px;min-width:35px;'>
      <div class="g-plusone" data-href="http://www.siepaczekodu.pl/2016/05/15/t4-templates-szybka-pomoc/" data-size="large" data-annotation="none" >
      </div>
    </div>
  </div>
</div>