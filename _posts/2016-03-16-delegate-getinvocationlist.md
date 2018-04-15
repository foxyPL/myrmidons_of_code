---
id: 94
title: 'Delegate &#8211; GetInvocationList'
date: 2016-03-16T22:49:23+00:00
author: Łukasz Zaborski
layout: post
guid: http://www.siepaczekodu.pl/?p=94
permalink: /2016/03/16/delegate-getinvocationlist/
image: /wp-content/uploads/2016/03/Przechwytywanie.png
categories:
  - 'C#'
---
Jak wiemy delegaty w języku C# zawierają referencje do metod o określonych wcześniej parametrach oraz typie jaki dana metoda zwraca. Poniżej bardzo prosty przykład użycia delegaty.

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">public delegate string CustomParse(string s);

public static void InvokeStringParse()
{
    CustomParse customParse = s =&gt; s.ToLower();

    string result = customParse("Piwo To Moje Paliwo");
    Console.WriteLine(result);
}</pre>

Tak zadeklarowana delegata może zostać wywołana w rezultacie zwracając : &#8222;piwo to moje paliwo&#8221;.

Delegaty zapewniają nam <a href="https://msdn.microsoft.com/en-us/library/ms173175.aspx" target="_blank">multicasting</a>, oznacza to że delegata może wywołać wiele metod wcześniej do niej przypisanych za pomocą operatora + (oczywiście metod o tym samym schemacie).

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">public delegate string CustomParse(string s);

public static void InvokeStringParse()
{
    CustomParse customParse = s =&gt; s.ToLower();
    customParse += s =&gt; s.ToUpper();
    customParse += s =&gt; $"Length : {s.Length}";

    string result = customParse("Piwo To Moje Paliwo");
    Console.WriteLine(result);
}</pre>

W powyższym przykładzie customParse wywołuje w kolejności metody przypisane do instancji delegaty. Zmienna result zawiera wartość zwróconą z ostatniej wywołanej metody. W tym przypadku jest to &#8222;Length : 19&#8221;.

No dobra a co jeśli potrzebuje uzyskać każdą zwróconą wartość w przypadku kiedy do delegaty dodaliśmy więcej niż jedną metode? Wtedy możemy skorzystać z metody <a href="https://msdn.microsoft.com/query/dev14.query?appId=Dev14IDEF1&l=EN-US&k=k(System.MulticastDelegate.GetInvocationList);k(TargetFrameworkMoniker-.NETFramework,Version%3Dv4.6);k(DevLang-csharp)&rd=true" target="_blank">GetInvocationList</a>. Zwraca ona liste wywołań, dzięki czemu możemy kążdą z metod wywołać osobno według założonej przez nas kolejności.

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">public delegate bool ValidDelegate(string key);

public static void InvokeValidation()
{
    ValidDelegate validDelegate = ValidateLength;
    validDelegate += ValidateUpperCase;
    validDelegate += ValidateOnlyLettersAndNumbers;

    var results = new List&lt;bool&gt;();
    foreach (ValidDelegate del in validDelegate.GetInvocationList())
    {
        results.Add(del("Piwo-12"));
    }

    results.ForEach(r =&gt; Console.WriteLine(r));
}

private static bool ValidateLength(string key)
{
    return key.Length &gt;= 7;
}

private static bool ValidateUpperCase(string key)
{
    return key.Any(char.IsUpper);
}

private static bool ValidateOnlyLettersAndNumbers(string key)
{
    var regex = new Regex(@"^[a-zA-Z0-9]+$");
    return regex.IsMatch(key);
}</pre>

W pętli foreach rezultat wszystkich metod zapisywany jest do listy którą w następnym kroku możemy wyświetlić. Powyższy przykład wyświetli następujące wartości.

<pre class="EnlighterJSRAW" data-enlighter-language="no-highlight">True
True
False</pre>

Należy wspomnieć że zwracana lista wywołań przez metode GetInvocationList jest w kolejności w jakiej metody byłyby wykonywane podczas normalnego działania delegaty validDelegate(), a jako że lista implementuje interfejs System.Collections.Generic.IEnumerable<T> możemy wykonywać metody w wybranej przez nas kolejności. Przykładem może być odwrócenie kolejności.

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">foreach (ValidDelegate del in validDelegate.GetInvocationList().Reverse())
{
    results.Add(del("Piwo-12"));
}</pre>

Podmieniając te linijki kodu na ekranie pojawią sie następujące wartości.

<pre class="EnlighterJSRAW" data-enlighter-language="no-highlight">False
True
True</pre>

&nbsp;

<div class='sfsi_Sicons' style='width: 100%; display: inline-block; vertical-align: middle; text-align:left'>
  <div style='margin:0px 8px 0px 0px; line-height: 24px'>
    <span>Udostępnij</span>
  </div>
  
  <div class='sfsi_socialwpr'>
    <div class='sf_fb' style='text-align:left;width:98px'>
      <div class="fb-like" href="http://www.siepaczekodu.pl/2016/03/16/delegate-getinvocationlist/" width="180" send="false" showfaces="false"  action="like" data-share="true"data-layout="button" >
      </div>
    </div>
    
    <div class='sf_twiter' style='text-align:left;float:left;width:auto'>
      <a href="http://twitter.com/share" data-count="none" class="sr-twitter-button twitter-share-button" lang="en" data-url="http://www.siepaczekodu.pl/2016/03/16/delegate-getinvocationlist/" data-text="Delegate &#8211; GetInvocationList" ></a>
    </div>
    
    <div class='sf_google' style='text-align:left;float:left;max-width:62px;min-width:35px;'>
      <div class="g-plusone" data-href="http://www.siepaczekodu.pl/2016/03/16/delegate-getinvocationlist/" data-size="large" data-annotation="none" >
      </div>
    </div>
  </div>
</div>