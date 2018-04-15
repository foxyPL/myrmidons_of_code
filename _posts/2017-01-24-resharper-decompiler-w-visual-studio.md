---
id: 225
title: Resharper decompiler w Visual Studio
date: 2017-01-24T21:48:22+00:00
author: Łukasz Zaborski
layout: post
guid: http://www.siepaczekodu.pl/?p=225
permalink: /2017/01/24/resharper-decompiler-w-visual-studio/
image: /wp-content/uploads/2017/01/i_lgq8jzfge-joao-silas.jpg
categories:
  - Resharper
  - Visual Studio
---
Niedawno rzuciłem okiem na projekt [Rider](https://www.jetbrains.com/rider/). Jest to nowe wieloplatformowe IDE nad którym pracuje firma JetBrains obecnie w wersji early build. W przyszłości może to być alternatywa dla Visual Studio ponieważ możemy za jego pomocą tworzyć projekty .NET/NET Core/Mono nie tylko na systemach Windows ale również Linux oraz macOS.

Przeglądając kod przypadkiem znalazłem ciekawą funkcje Rider-a. Naciskając klawisz F12 na systemowej klasie lub metodzie IDE dekompiluję daną bibliotekę aby od razu potem wyświetlić jej kod źródłowy. To samo tyczy się dodanych do naszego projektu zewnętrznych bibliotek. Przykłady możemy zobaczyć poniżej.

[<img class="aligncenter size-full wp-image-233" src="http://www.siepaczekodu.pl/wp-content/uploads/2017/01/rider1.gif" alt="" width="1265" height="740" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2017/01/rider1.gif 1265w, http://www.siepaczekodu.pl/wp-content/uploads/2017/01/rider1-300x175.gif 300w, http://www.siepaczekodu.pl/wp-content/uploads/2017/01/rider1-768x449.gif 768w, http://www.siepaczekodu.pl/wp-content/uploads/2017/01/rider1-1024x599.gif 1024w" sizes="(max-width: 1265px) 100vw, 1265px" />](http://www.siepaczekodu.pl/wp-content/uploads/2017/01/rider1.gif)

&nbsp;

Jako że projekt Rider jest połączeniem IntelliJ oraz ReSharper-a sprawdziłem czy taka funkcjonalność została stworzona dla Visual Studio po zainstalowaniu ReSharper-a (wersja R# 9.2, VS 2015). No i oczywiście że jest 🙂 Aby ją aktywować przechodzimy do **ReSharper => Options => Tools => External Sources **i zaznaczamy opcje **Decompile methods **po wybraniu opcji **Navigate to Sources**. Jeśli checkbox Decompile methods nie będzie zaznaczony wyświetlą się metadane przedstawiające metode.

[<img class="aligncenter size-full wp-image-235" src="http://www.siepaczekodu.pl/wp-content/uploads/2017/01/decompileMethod.png" alt="" width="1004" height="599" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2017/01/decompileMethod.png 1004w, http://www.siepaczekodu.pl/wp-content/uploads/2017/01/decompileMethod-300x179.png 300w, http://www.siepaczekodu.pl/wp-content/uploads/2017/01/decompileMethod-768x458.png 768w" sizes="(max-width: 1004px) 100vw, 1004px" />](http://www.siepaczekodu.pl/wp-content/uploads/2017/01/decompileMethod.png)

Po tym możemy cieszyć się tą samą opcją w Visual Studio 🙂

[<img class="aligncenter size-full wp-image-236" src="http://www.siepaczekodu.pl/wp-content/uploads/2017/01/vs1.gif" alt="" width="1362" height="756" />](http://www.siepaczekodu.pl/wp-content/uploads/2017/01/vs1.gif)

Bez zaznaczenia powyższej opcji dostęp do zdekompilowanych źródeł możemy osiągnąć przez otwarcie menu kontekstowego a następnie wybranie opcji **Navigate => Decompiled Sources**.

[<img class="aligncenter size-full wp-image-238" src="http://www.siepaczekodu.pl/wp-content/uploads/2017/01/navigate.png" alt="" width="1079" height="733" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2017/01/navigate.png 1079w, http://www.siepaczekodu.pl/wp-content/uploads/2017/01/navigate-300x204.png 300w, http://www.siepaczekodu.pl/wp-content/uploads/2017/01/navigate-768x522.png 768w, http://www.siepaczekodu.pl/wp-content/uploads/2017/01/navigate-1024x696.png 1024w" sizes="(max-width: 1079px) 100vw, 1079px" />](http://www.siepaczekodu.pl/wp-content/uploads/2017/01/navigate.png)

Więcej informacji na temat ustawień nawigacji za pomocą ReSharper-a możemy znaleźć w [dokumentacji](https://www.jetbrains.com/help/resharper/2016.3/Reference__Options__Tools__External_Sources.html) projektu.

<div class='sfsi_Sicons' style='width: 100%; display: inline-block; vertical-align: middle; text-align:left'>
  <div style='margin:0px 8px 0px 0px; line-height: 24px'>
    <span>Udostępnij</span>
  </div>
  
  <div class='sfsi_socialwpr'>
    <div class='sf_fb' style='text-align:left;width:98px'>
      <div class="fb-like" href="http://www.siepaczekodu.pl/2017/01/24/resharper-decompiler-w-visual-studio/" width="180" send="false" showfaces="false"  action="like" data-share="true"data-layout="button" >
      </div>
    </div>
    
    <div class='sf_twiter' style='text-align:left;float:left;width:auto'>
      <a href="http://twitter.com/share" data-count="none" class="sr-twitter-button twitter-share-button" lang="en" data-url="http://www.siepaczekodu.pl/2017/01/24/resharper-decompiler-w-visual-studio/" data-text="Resharper decompiler w Visual Studio" ></a>
    </div>
    
    <div class='sf_google' style='text-align:left;float:left;max-width:62px;min-width:35px;'>
      <div class="g-plusone" data-href="http://www.siepaczekodu.pl/2017/01/24/resharper-decompiler-w-visual-studio/" data-size="large" data-annotation="none" >
      </div>
    </div>
  </div>
</div>