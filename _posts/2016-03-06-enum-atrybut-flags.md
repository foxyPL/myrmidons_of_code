---
id: 59
title: 'Enum &#8211; atrybut Flags'
date: 2016-03-06T12:46:05+00:00
author: Łukasz Zaborski
layout: post
guid: http://www.siepaczekodu.pl/?p=59
permalink: /2016/03/06/enum-atrybut-flags/
image: /wp-content/uploads/2016/03/bit1-e1458760533208.jpg
categories:
  - 'C#'
  - Refactor
---
Jakiś czas temu wprowadzałem nową funkcjonalność do aplikacji webowej służącej do wprowadzania wniosków. Klasa POCO reprezentująca wniosek posiada kilkanaście właściwości typu bool. Wszystkie określają posiadanie danej wartości z tego samego zakresu kategori.

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">public class Application
{
    // Some others properties.
    
    public bool StateA { get; set; }
    public bool StateB { get; set; }
    public bool StateC { get; set; }
    public bool StateD { get; set; }
    public bool StateE { get; set; }
    public bool StateF { get; set; }
    //And over a dozen other state.
}</pre>

Taki zapis powoduje iż nasza tablica w bazie danych zawiera kilkanaście kolumn typu bit. Sprawdzanie stanu takiego wniosku może wyglądać następująco:

<pre class="EnlighterJSRAW" data-enlighter-language="null">public string GetApplicationState(Application application)
    {
        var states = new List&lt;string&gt;();
        if (application.StateA)
            states.Add("StateA");
        if (application.StateB)
            states.Add("StateB");
        if (application.StateA)
            states.Add("StateC");
        if (application.StateB)
            states.Add("StateD");
        if (application.StateA)
            states.Add("StateE");
        if (application.StateB)
            states.Add("StateF");
        // and more if statements
            
        return states;
    }</pre>

Oczywiście w momencie dodania nowej właściwości danej kategori, do tabeli w bazie danych dochodzi nowa kolumna a w metodzie GetApplicationState kolejny if sprawdzający wartość nowego pola, nie licząc pozostałych miejsc w których korzystamy z tych właściwości.

W takim przypadku do akcji wkraczają typy wyliczeniowe oraz atrybut <a href="https://msdn.microsoft.com/en-us/library/system.flagsattribute(v=vs.110).aspx" target="_blank">Flags</a>. Poniżej przykład jak może wyglądać enum dla naszego przypadku.

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">[Flags]
 public enum States
 {
   StateA = 1,
   StateB = 2,
   StateC = 4,
   StateD = 8,
   StateE = 16,
   StateF = 32
 }</pre>

Atrybut Flags pozwala traktować pole typu States jako wartość bitową. Daje nam to możliwość korzystania z niej jako kolekcji flag i operowania na niej za pomocą operacji bitowych. Korzystając z tego atrybutu należy pamiętać aby ręcznie określić stałe wartości każdego z elementów w typie wyliczeniowym, tymi wartościami muszą być kolejne potęgi liczby 2. Domyślnie wartość dla pierwszego elementu wynosiłaby 0 a każda kolejna byłaby inkrementowana o 1. Dzięki wartościom potęgi liczby 2 wartości podczas wykonywania operacji bitowych będą zawsze indywidualne.

Teraz zamiast posiadać w klasie wiele pól typu bool wystarczy nam jedno pole którego typem jest nasz nowy enum.

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">public class Application
    {
        // Some others properties.

        public States States { get; set; }
    }</pre>

Wartości do tej zmiennnej możemy wprowadzić w następujący sposób:

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">States = States.StateA | States.StateB | States.StateF;</pre>

A metode GetApplicationState skrócić o wiele lini kodu:

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">public string GetApplicationState(Application application)
{
    return application.States.ToString();
}</pre>

A teraz mały przykład pokazujący działanie powyższej metody:

<pre class="EnlighterJSRAW" data-enlighter-language="csharp">var application = new Application
{
    States = States.StateA | States.StateB | States.StateF
};
string states = ApplicationViewer.GetApplicationState(application);
Console.WriteLine(states);</pre>

Wynikiem będzie ciąg znaków: StateA, StateB, StateF

<div class='sfsi_Sicons' style='width: 100%; display: inline-block; vertical-align: middle; text-align:left'>
  <div style='margin:0px 8px 0px 0px; line-height: 24px'>
    <span>Udostępnij</span>
  </div>
  
  <div class='sfsi_socialwpr'>
    <div class='sf_fb' style='text-align:left;width:98px'>
      <div class="fb-like" href="http://www.siepaczekodu.pl/2016/03/06/enum-atrybut-flags/" width="180" send="false" showfaces="false"  action="like" data-share="true"data-layout="button" >
      </div>
    </div>
    
    <div class='sf_twiter' style='text-align:left;float:left;width:auto'>
      <a href="http://twitter.com/share" data-count="none" class="sr-twitter-button twitter-share-button" lang="en" data-url="http://www.siepaczekodu.pl/2016/03/06/enum-atrybut-flags/" data-text="Enum &#8211; atrybut Flags" ></a>
    </div>
    
    <div class='sf_google' style='text-align:left;float:left;max-width:62px;min-width:35px;'>
      <div class="g-plusone" data-href="http://www.siepaczekodu.pl/2016/03/06/enum-atrybut-flags/" data-size="large" data-annotation="none" >
      </div>
    </div>
  </div>
</div>