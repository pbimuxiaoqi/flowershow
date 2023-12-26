# URL: https://kb.daxoptimizer.com/d/100300

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Duplicated function - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-duplicated-function">
<header class="main nosearch">
<div class="logo">
<img class="light" src="/assets/images/logo.svg"/><img class="dark" src="/assets/images/logo-dark.svg"/>
</div>
<div class="title">Knowledge Base</div>
<div class="controls">
<!--<a href="#" class="ctrl change-theme" title="Change Theme"><span class="ctrl icon-theme-auto"></span></a>-->
<a class="ctrl border solo" href="https://app.daxoptimizer.com/" target="_blank">Open App</a>
</div>
</header>
<div class="page">
<div class="content-no-nav">
<article class="markdown-body">
<header>
<div class="super-title">KB 100300</div>
<a href="/d/100300"><h1>Duplicated function</h1></a>
<hr/>
</header>
<p>There are multiple executions of the same DAX function with the same arguments.</p>
<h2 id="remarks">Remarks</h2>
<p>If a function is called with the same arguments within the same filter context, it returns the same value. However, the formula engine may perform redundant evaluations, resulting in additional CPU cost.</p>
<p>A possible optimization is to store the result of a function call in a variable, and then reference the variable. It is important to assign the variable only when the execution scope guarantees that the variable is used at least once, otherwise the result could be counterproductive and slow down the execution time instead of improving it.</p>
<p>There are functions that do not depend on the filter context for the result they produce, so the optimization is possible for those functions even though they are executed in different filter contexts. For example, <a href="https://dax.guide/lastdate/">LASTDATE</a> and <a href="https://dax.guide/sum/">SUM</a> depend on the filter context, whereas <a href="https://dax.guide/trunc/">TRUNC</a> and <a href="https://dax.guide/int/">INT</a> do not depend depend on the filter context but only on the value passed to them.</p>
<h2 id="example">Example</h2>
<p><strong>Evaluate the function only once and assign it to a variable.</strong> If the measure <em>ExchangeRate</em> does not depend on the rows iterated in <em>Sales</em>, compute the Exchange Rate in a variable before starting the iterator.</p>
<h3 id="original-code">Original code</h3>
<pre>VAR _LastBalance =
    CALCULATE ( 
        [Balance],
        <span class="issue toedit">LASTDATE ( 'Date'[Date] )</span>
    )
VAR _LastExpenses =
    CALCULATE ( 
        [Amount],
        Account[Type] = "Expenses",
        <span class="issue toedit">LASTDATE ( 'Date'[Date] )</span>
    )
RETURN LastBalance - LastExpenses</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre><span class="added">VAR _LastDate = <span class="issue">LASTDATE ( 'Date'[Date] )</span></span>
VAR _LastBalance =
    CALCULATE ( 
        [Balance],
        <span class="edited">_LastDate</span>
    )
VAR _LastExpenses =
    CALCULATE ( 
        [Amount],
        Account[Type] = "Expenses",
        <span class="edited">_LastDate</span>
    )
RETURN LastBalance - LastExpenses</pre>
<footer>
</footer>
</article>
</div>
</div>
<footer class="main">
<div class="wrapper">
<div class="copy">
            Copyright © Tabular Tools Corp. All rights reserved.  <a href="https://www.daxoptimizer.com">www.daxoptimizer.com</a>  |  <a href="https://www.daxoptimizer.com/legal/privacy/">Privacy Policy</a>  |  <a href="https://github.com/tabulartools/dax-optimizer/">Report an Issue</a>  |  <a href="mailto:daxoptimizer@tabulartools.com">Contact us</a>
</div>
</div>
</footer>
<script src="/assets/scripts/cookiehelper.min.js"></script>
<script src="/assets/scripts/main.min.js"></script>
</body>
</html>