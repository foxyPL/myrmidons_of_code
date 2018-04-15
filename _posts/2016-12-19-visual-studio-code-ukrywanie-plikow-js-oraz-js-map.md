---
id: 212
title: 'Visual Studio Code &#8211; ukrywanie plików js oraz js.map'
date: 2016-12-19T23:27:07+00:00
author: Łukasz Zaborski
layout: post
guid: http://www.siepaczekodu.pl/?p=212
permalink: /2016/12/19/visual-studio-code-ukrywanie-plikow-js-oraz-js-map/
image: /wp-content/uploads/2016/12/3pgb5eqvaie-lorenzo-cafaro.jpg
categories:
  - Visual Studio Code
---
Angular zawsze był na moim celowniku technologi do zapoznania się a po jakimś czasie opanowania. Zaczynając naukę frameworka od zera (mam na myśli wersje Angular 2) postanowiłem przejść tutorial znajdujący się na jego oficjalnej [stronie](https://angular.io/docs/ts/latest/guide/). Jako edytor kodu wybrałem Visual Studio Code. Przechodząc kolejne etapu tutorialu ilość plików zawierających kod Typescript zwiększała się. Tym samym pojawiała się coraz większa ilość plików .js oraz js.map (były tworzone przez kompilator TypeScript który został włączony przez polecenie npm start). Po niedługim czasie zaczynało mnie to denerwować ponieważ pliki w edytorze mieszały się 🙂 Na szczęście 2 minuty w Google i udało mi się znaleźć rozwiązanie. W Visual Studio Code otwieramy Users lub Workspaces setting. Ustawienia znajdziemy w **File -> Preferenced -> Worspaces settings **lub wpisując _open workspace settings _po naciśnięciu kombinacji klawiszy Ctrl+Shift+P. Następnie nadpisujemy domyślne ustawienia elementu files.exclude dodając do kolekcji poniższe wartości.

<pre class="EnlighterJSRAW" data-enlighter-language="json">"**/*.js": {"when": "$(basename).ts"},
"**/*.map": {"when": "$(basename).map"}</pre>

W rezultacie nadpisany element będzie wyglądał następująco.

<pre class="EnlighterJSRAW" data-enlighter-language="json">"files.exclude": {
 "**/.git": true,
 "**/.svn": true,
 "**/.hg": true,
 "**/.DS_Store": true,
 "**/*.js": {"when": "$(basename).ts"},
 "**/*.map": {"when": "$(basename).map"}
}</pre>

A efekt można zauważyć od razu po zapisaniu pliku z ustawieniami.

[<img class="aligncenter size-full wp-image-215" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/12/vscodeFilesExclude.gif" alt="" width="1137" height="551" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2016/12/vscodeFilesExclude.gif 1137w, http://www.siepaczekodu.pl/wp-content/uploads/2016/12/vscodeFilesExclude-300x145.gif 300w, http://www.siepaczekodu.pl/wp-content/uploads/2016/12/vscodeFilesExclude-768x372.gif 768w, http://www.siepaczekodu.pl/wp-content/uploads/2016/12/vscodeFilesExclude-1024x496.gif 1024w" sizes="(max-width: 1137px) 100vw, 1137px" />](http://www.siepaczekodu.pl/wp-content/uploads/2016/12/vscodeFilesExclude.gif)

<div class='sfsi_Sicons' style='width: 100%; display: inline-block; vertical-align: middle; text-align:left'>
  <div style='margin:0px 8px 0px 0px; line-height: 24px'>
    <span>Udostępnij</span>
  </div>
  
  <div class='sfsi_socialwpr'>
    <div class='sf_fb' style='text-align:left;width:98px'>
      <div class="fb-like" href="http://www.siepaczekodu.pl/2016/12/19/visual-studio-code-ukrywanie-plikow-js-oraz-js-map/" width="180" send="false" showfaces="false"  action="like" data-share="true"data-layout="button" >
      </div>
    </div>
    
    <div class='sf_twiter' style='text-align:left;float:left;width:auto'>
      <a href="http://twitter.com/share" data-count="none" class="sr-twitter-button twitter-share-button" lang="en" data-url="http://www.siepaczekodu.pl/2016/12/19/visual-studio-code-ukrywanie-plikow-js-oraz-js-map/" data-text="Visual Studio Code &#8211; ukrywanie plików js oraz js.map" ></a>
    </div>
    
    <div class='sf_google' style='text-align:left;float:left;max-width:62px;min-width:35px;'>
      <div class="g-plusone" data-href="http://www.siepaczekodu.pl/2016/12/19/visual-studio-code-ukrywanie-plikow-js-oraz-js-map/" data-size="large" data-annotation="none" >
      </div>
    </div>
  </div>
</div>