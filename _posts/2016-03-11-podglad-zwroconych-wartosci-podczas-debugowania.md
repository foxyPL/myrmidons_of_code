---
id: 75
title: Podgląd zwróconych wartości podczas debugowania
date: 2016-03-11T18:27:42+00:00
author: Łukasz Zaborski
layout: post
guid: http://www.siepaczekodu.pl/?p=75
permalink: /2016/03/11/podglad-zwroconych-wartosci-podczas-debugowania/
image: /wp-content/uploads/2016/03/2016-03-16-19.25.27.jpg
categories:
  - Visual Studio
---
Często podczas debugowania miałem problem z sprawdzeniem co dana metoda zwraca w momencie kiedy call stack znajdował się na linijce z return. Przykładowo mając poniższą metode nie byłem w stanie podejrzeć jakie wartości są zwracane.

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">public IEnumerable&lt;Course&gt; GetCoursesStartingTommorow()
{
    return _courses.Where(c =&gt; c.StartDate.Date == DateTime.Now.AddDays(1).Date);
}</pre>

<!--more-->

Wtedy musiałem dodać zmienną która przechowywała wartości z linq i dopiero w kolejnej linijce zwracałem rezultat. Nie ukrywam że było to dla mnie dosyć irytujące 🙂

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">public IEnumerable&lt;Course&gt; GetCoursesStartingTommorow()
{
    var result = _courses.Where(c =&gt; c.StartDate.Date == DateTime.Now.AddDays(1).Date);
    return result;
}</pre>

Na szczęścię jedną z nowych funkcjonalności jaką wprowadza Visual Studio 2015 jest możliwość podglądu takich wartości. Możemy to zrobić otwierając podczas debugowania okno Locals lub Autos (różnicą okna Autos jest to że pokazuje wartości zmiennych z aktualnej oraz poprzedniej lini kodu) w momencie kiedy debugger znajduje się w lini po wywołaniu return.

<a href="http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos3.png" target="_blank" rel="attachment wp-att-83"><img class="aligncenter wp-image-83 size-full" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos3.png" alt="Autos3" width="1106" height="390" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos3.png 1106w, http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos3-300x106.png 300w, http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos3-768x271.png 768w, http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos3-1024x361.png 1024w" sizes="(max-width: 1106px) 100vw, 1106px" /></a>

W pierwszym wierszu widzimy zwracane obiekty (System.Linq.Enumerable.Where<TSource> returned).

Zwrócone wartości możemy rownież sprawdzić w trakcie rozpoczęcia pętli foreach.

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">var coursesService = new CourseService();
foreach (var course in coursesService.GetCoursesStartingTommorow())
{
    Console.WriteLine(course.Name);
}</pre>

Po wywołaniu metody GetCoursesStartingTommorow możemy sprawdzić jej rezultat w oknie Autos lub Locals.

<a href="http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos4.png" rel="attachment wp-att-86"><img class="aligncenter size-full wp-image-86" src="http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos4.png" alt="Autos4" width="1105" height="524" srcset="http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos4.png 1105w, http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos4-300x142.png 300w, http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos4-768x364.png 768w, http://www.siepaczekodu.pl/wp-content/uploads/2016/03/Autos4-1024x486.png 1024w" sizes="(max-width: 1105px) 100vw, 1105px" /></a>

&nbsp;

Innym sposobem na sprawdzanie zwracanej wartości jest wprowadzenie w Immediate Window polecenia $ReturnValue zaraz po wywołaniu metody. Daje to następujący wynik:

<pre class="EnlighterJSRAW" data-enlighter-language="no-highlight">$ReturnValue
{System.Linq.Enumerable.WhereListIterator&lt;SiepaczeKodySamples.ReturnValues.Course&gt;}
    base: {System.Linq.Enumerable.WhereListIterator&lt;SiepaczeKodySamples.ReturnValues.Course&gt;}
$ReturnValue.First()
{SiepaczeKodySamples.ReturnValues.Course}
    Id: 1
    Name: "Cooking course"
    StartDate: {2016-03-12 19:12:17}
</pre>

Jednak aby można było skorzystać z tej funkcji należy włączyć opcje w Visual Studio:

**Tools -> Options -> Debugging > Use the legacy C# and VB expression evaluators**

<div class='sfsi_Sicons' style='width: 100%; display: inline-block; vertical-align: middle; text-align:left'>
  <div style='margin:0px 8px 0px 0px; line-height: 24px'>
    <span>Udostępnij</span>
  </div>
  
  <div class='sfsi_socialwpr'>
    <div class='sf_fb' style='text-align:left;width:98px'>
      <div class="fb-like" href="http://www.siepaczekodu.pl/2016/03/11/podglad-zwroconych-wartosci-podczas-debugowania/" width="180" send="false" showfaces="false"  action="like" data-share="true"data-layout="button" >
      </div>
    </div>
    
    <div class='sf_twiter' style='text-align:left;float:left;width:auto'>
      <a href="http://twitter.com/share" data-count="none" class="sr-twitter-button twitter-share-button" lang="en" data-url="http://www.siepaczekodu.pl/2016/03/11/podglad-zwroconych-wartosci-podczas-debugowania/" data-text="Podgląd zwróconych wartości podczas debugowania" ></a>
    </div>
    
    <div class='sf_google' style='text-align:left;float:left;max-width:62px;min-width:35px;'>
      <div class="g-plusone" data-href="http://www.siepaczekodu.pl/2016/03/11/podglad-zwroconych-wartosci-podczas-debugowania/" data-size="large" data-annotation="none" >
      </div>
    </div>
  </div>
</div>