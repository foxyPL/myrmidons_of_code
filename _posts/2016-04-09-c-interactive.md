---
id: 132
title: 'C# Interactive'
date: 2016-04-09T13:25:18+00:00
author: Łukasz Zaborski
layout: post
guid: http://www.siepaczekodu.pl/?p=132
permalink: /2016/04/09/c-interactive/
image: /wp-content/uploads/2016/04/cover.png
categories:
  - 'C#'
  - Visual Studio
---
W dzisiejszym wpisie chciałbym przedstawić nowe narzędzie udostępnione w Visual Studio 2015 jakim jest okno C# Interactive. Jest ono dostępne od wydania <a href="https://www.visualstudio.com/news/vs2015-update1-vs" target="_blank">Update 1</a>.

Jeśli kiedykolwiek zdarzało wam się irytować podczas tworzenia kolejnego projektu Console Application tylko po to aby wypróbować działanie kawałka kodu na pewno ucieszy was fakt że za pomocą C# Interactive już tego nie będziecie musieli robić 🙂 Okno to dostarcza mechanizm <a href="https://en.wikipedia.org/wiki/Read–eval–print_loop" target="_blank">REPL</a> które w pętli przyjmuje pojedyncze polecenie, wykonuje je a następnie od razu wyświetla wynik w tym przypadku dzięki kompilatorowi Roslyn.

A teraz oczywiście mały przykład. Okno C# Interactive otwieramy w następujący sposób: **View -> Other Windows -> C# Interactive**.

<a href="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Square.png" rel="attachment wp-att-135"><img class="size-full wp-image-135 aligncenter" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Square.png" alt="Square" width="435" height="174" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Square.png 435w, http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Square-300x120.png 300w" sizes="(max-width: 435px) 100vw, 435px" /></a>

W pierwszym poleceniu tworze zmienna area i przypisuje do niej obliczone pole koła. W następnym wywołujemy zmienną i od razu wynik zostaje wyświetlony na ekranie.

Edytor w oknie zapewnia nam podobne mechanizmy jak w domyślnym edytorze kodu takie jak IntelliSense.

<a href="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Anymous-e1460202641997.png" rel="attachment wp-att-138"><img class="aligncenter size-full wp-image-138" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Anymous-e1460202641997.png" alt="Anymous" width="505" height="298" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Anymous-e1460202641997.png 505w, http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Anymous-e1460202641997-300x177.png 300w" sizes="(max-width: 505px) 100vw, 505px" /></a>

C# Interactive przyjmuje nie tylko pojedyncze jednolinijkowe polecenia, możemy również definiować całe klasy i metody. Aby zacząć wpisywać kod w kolejnej lini należy użyć shift + enter.

<a href="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/PersonClass.png" rel="attachment wp-att-139"><img class="aligncenter size-full wp-image-139" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/PersonClass.png" alt="PersonClass" width="504" height="278" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/PersonClass.png 504w, http://www.siepaczekodu.pl/wp-content/uploads/2016/04/PersonClass-300x165.png 300w" sizes="(max-width: 504px) 100vw, 504px" /></a>

Korzystanie z Linq nie przysparza tutaj większych problemów.

<a href="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/linq2.png" rel="attachment wp-att-141"><img class="aligncenter size-full wp-image-141" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/linq2.png" alt="linq2" width="738" height="274" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/linq2.png 738w, http://www.siepaczekodu.pl/wp-content/uploads/2016/04/linq2-300x111.png 300w" sizes="(max-width: 738px) 100vw, 738px" /></a>

Jeżeli chemy skorzystać z tego narzędzia poza Visual Studio 2015, możemy uruchomić C# REPL w Developer Command Prompt for VS2015 wpisując następujące polecenie:

<pre>csi</pre>

###### 

###### Visual studio 2015 update 2

30 marca miało miejsce wydanie <a href="https://www.visualstudio.com/en-us/news/vs2015-update2-vs.aspx" target="_blank">Update 2</a> do Visual Studio 2015. Dodatek pozwala na przesłania fragmentu kodu z naszych projektów do okna C# Interactive. Można to zrobić przez zaznaczenie kodu i otwarcie menu kontekstowego i wybranie **Execute in Interactive** (albo za pomocą skrótu ctrl+e, ctra+e). Sktutkiem tego będzie przeniesienie zaznaczonych lini kodu i wywołanie ich w oknie jak na screenie poniżej.

<a href="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/ExecuteInInteractive.png" rel="attachment wp-att-143"><img class="aligncenter size-full wp-image-143" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/ExecuteInInteractive.png" alt="ExecuteInInteractive" width="850" height="442" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/ExecuteInInteractive.png 850w, http://www.siepaczekodu.pl/wp-content/uploads/2016/04/ExecuteInInteractive-300x156.png 300w, http://www.siepaczekodu.pl/wp-content/uploads/2016/04/ExecuteInInteractive-768x399.png 768w" sizes="(max-width: 850px) 100vw, 850px" /></a>

Dodatek zapewnia również łatwiejsze korzystanie z polecenia #r który służy do wczytywania bibliotek.

<pre class="EnlighterJSRAW" data-enlighter-language="no-highlight">#r "C:\Program Files (x86)\Reference Assemblies\Microsoft\Framework\.NETFramework\v4.5.2\System.Xml.dll"</pre>

Jeśli chcemy załadować projekt z naszej solucji wystarczy kliknąć prawym przyciskiem myszy dany projekt i wybrać w menu kontekstowym **Initialize Interactive with Project**. W projekcie Service znajduje się klasa Salaries:

<pre class="EnlighterJSRAW" data-enlighter-language="null">namespace Services
{
    public enum AgreementType
    {
        FullTimeJob,
        PartTimeJob,
        ContractJob
    }

    public class Salaries
    {
        public double ComputeTax(AgreementType agreementType, double salary)
        {
            switch (agreementType)
            {
                case AgreementType.FullTimeJob:
                    return salary - (salary * 0.23);
                case AgreementType.PartTimeJob:
                    return salary - (salary * 0.20);
                case AgreementType.ContractJob:
                    return salary - (salary * 0.18);
                default:
                    throw new InvalidEnumArgumentException();
            }
        }
    }
}</pre>

Wywołanie Initialize Interactive with Project wygląda następująco:

<a href="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Przechwytywanie.png" rel="attachment wp-att-145"><img class="aligncenter size-full wp-image-145" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Przechwytywanie.png" alt="Przechwytywanie" width="934" height="343" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Przechwytywanie.png 934w, http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Przechwytywanie-300x110.png 300w, http://www.siepaczekodu.pl/wp-content/uploads/2016/04/Przechwytywanie-768x282.png 768w" sizes="(max-width: 934px) 100vw, 934px" /></a>

###### Podsumowanie

Jestem zadowolony z nowej funkcjonalności jaką zapewnia Visual Studio. Na pewno do przetestowania małych fragmentów kodu nie będę już zmuszony do tworzenia kolejnego projektu Console Application. Oczywiście do testowania kodu nadają się lepiej testy jednostkowe ale gdy chcemy na szybko sprawdzić działanie nowo poznanej biblioteki albo napisanej przed chwilą naszej nowej metody C# Interactive nadaje się do tego bardzo dobrze 🙂

###### Źródła

  * <a href="https://github.com/dotnet/roslyn/wiki/Interactive-Window" target="_blank">https://github.com/dotnet/roslyn/wiki/Interactive-Window</a>
  * <a href="https://www.visualstudio.com/en-us/news/vs2015-update2-vs.aspx" target="_blank">https://www.visualstudio.com/en-us/news/vs2015-update2-vs.aspx</a>

<div class='sfsi_Sicons' style='width: 100%; display: inline-block; vertical-align: middle; text-align:left'>
  <div style='margin:0px 8px 0px 0px; line-height: 24px'>
    <span>Udostępnij</span>
  </div>
  
  <div class='sfsi_socialwpr'>
    <div class='sf_fb' style='text-align:left;width:98px'>
      <div class="fb-like" href="http://www.siepaczekodu.pl/2016/04/09/c-interactive/" width="180" send="false" showfaces="false"  action="like" data-share="true"data-layout="button" >
      </div>
    </div>
    
    <div class='sf_twiter' style='text-align:left;float:left;width:auto'>
      <a href="http://twitter.com/share" data-count="none" class="sr-twitter-button twitter-share-button" lang="en" data-url="http://www.siepaczekodu.pl/2016/04/09/c-interactive/" data-text="C# Interactive" ></a>
    </div>
    
    <div class='sf_google' style='text-align:left;float:left;max-width:62px;min-width:35px;'>
      <div class="g-plusone" data-href="http://www.siepaczekodu.pl/2016/04/09/c-interactive/" data-size="large" data-annotation="none" >
      </div>
    </div>
  </div>
</div>