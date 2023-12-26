# URL: https://kb.daxoptimizer.com/d/101200

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Function usage (LAST/FIRST)NONBLANK(VALUES) - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-function-usage-last-first-nonblank-values">
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
<div class="super-title">KB 101200</div>
<a href="/d/101200"><h1>Function usage (LAST/FIRST)NONBLANK(VALUES)</h1></a>
<hr/>
</header>
<p>The use of <a href="https://dax.guide/firstnonblank/">FIRSTNONBLANK</a>, <a href="https://dax.guide/lastnonblank/">LASTNONBLANK</a>, <a href="https://dax.guide/firstnonblankvalue/">FIRSTNONBLANKVALUE</a>, and <a href="https://dax.guide/lastnonblankvalue/">LASTNONBLANKVALUE</a> is not optimal for performance.</p>
<h2 id="remarks">Remarks</h2>
<p>The “NONBLANK” functions are all iterators that evaluate an expression for each row of the table iterated, just to check whether the result is blank or not. When a column reference is provided as the first argument, all the values in the filter context for that column are iterated.</p>
<p>Most of the times, these functions are used primarily to retrieve the last date when there is a transaction in a table in the current filter context. The same result can be obtained in a more efficient way by using <a href="https://dax.guide/min/">MIN</a> or <a href="https://dax.guide/max/">MAX</a> on the column, as it removes the need of a more complex calculation that usually requires also a context transition.</p>
<p>The unusual case when it is not possible to optimize the code is when the blank result of the expression does not depend only on the presence of data corresponding to the row context of the iterator, like a <em>Revenues</em> measure that can return BLANK even though there are transaction in the aggregated <em>Sales</em> table.</p>
<p>These functions can be removed by rewriting the expression as suggested in the following article:</p>
<ul>
<li><a href="https://www.sqlbi.com/articles/optimizing-lastnonblank-and-lastnonblankvalue-calculations/">Optimizing LASTNONBLANK and LASTNONBLANKVALUE calculations</a></li>
</ul>
<h2 id="example-1">Example 1</h2>
<p>Store in a variable the result of <a href="https://dax.guide/max/">MAX</a> and use that value to filter <em>‘Date’[Date]</em> instead of using <a href="https://dax.guide/lastnonblank/">LASTNONBLANK</a>.</p>
<h3 id="original-code">Original code</h3>
<pre>CALCULATE (
    [Balance Amount],
    <span class="issue"><span class="toremove">LASTNONBLANK (</span> 'Date'[Date]<span class="toremove">, [Balance Amount] )</span></span>
)</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre><span class="added">VAR _LastDate = MAX ( 'Date'[Date] )
RETURN</span>
    CALCULATE (
        [Balance Amount],
        <span class="issue">'Date'[Date] <span class="added">= _LastDate</span></span>
    )</pre>
<h2 id="example-2">Example 2</h2>
<p>Remove <a href="https://dax.guide/lastnonblankvalue/">LASTNONBLANKVALUE</a>, store in a variable the result of <a href="https://dax.guide/max/">MAX</a> and use that value to filter <em>‘Date’[Date]</em> in a <a href="https://dax.guide/calculate/">CALCULATE</a> function.</p>
<h3 id="original-code-1">Original code</h3>
<pre><span class="issue"><span class="toremove">LASTNONBLANKVALUE (</span> 
    <span class="toedit">'Date'[Date],</span>
    <span class="toedit">[Balance Amount]</span></span>
)</pre>
<h3 id="possible-optimization-1">Possible optimization</h3>
<p>Both expressions in the original code can be replaced by using the following implementation.</p>
<pre><span class="added">VAR _LastDate = MAX ( <span class="issue">'Date'[Date]</span> )
RETURN
    CALCULATE (</span>
        <span class="issue"><span class="edited">[Balance Amount],</span>
        <span class="edited">'Date'[Date] = _LastDate</span></span>
    )</pre>
<h2 id="example-3">Example 3</h2>
<p>Store in a variable the result of <a href="https://dax.guide/min/">MIN</a> and use that value to filter <em>‘Date’[Date]</em> instead of using <a href="https://dax.guide/firstnonblank/">FIRSTNONBLANK</a>.</p>
<h3 id="original-code-2">Original code</h3>
<pre>CALCULATE (
    [Balance Amount],
    <span class="issue"><span class="toremove">FIRSTNONBLANK (</span> 'Date'[Date]<span class="toremove">, [Balance Amount] )</span></span>
)</pre>
<h3 id="possible-optimization-2">Possible optimization</h3>
<pre><span class="added">VAR _FirstDate = MIN ( 'Date'[Date] )
RETURN</span>
    CALCULATE (
        [Balance Amount],
        <span class="issue">'Date'[Date] <span class="added">= _FirstDate</span></span>
    )</pre>
<h2 id="example-4">Example 4</h2>
<p>Remove <a href="https://dax.guide/firstnonblankvalue/">FIRSTNONBLANKVALUE</a>, store in a variable the result of <a href="https://dax.guide/min/">MIN</a> and use that value to filter <em>‘Date’[Date]</em> in a <a href="https://dax.guide/calculate/">CALCULATE</a> function.</p>
<h3 id="original-code-3">Original code</h3>
<pre><span class="issue"><span class="toremove">FIRSTNONBLANKVALUE (</span> 
    <span class="toedit">'Date'[Date],</span>
    <span class="toedit">[Balance Amount]</span></span>
)</pre>
<h3 id="possible-optimization-3">Possible optimization</h3>
<p>Both expressions in the original code can be replaced by using the following implementation.</p>
<pre><span class="added">VAR _FirstDate = MIN ( <span class="issue">'Date'[Date]</span> )
RETURN
    CALCULATE (</span>
        <span class="issue"><span class="edited">[Balance Amount],</span>
        <span class="edited">'Date'[Date] = _FirstDate</span></span>
    )</pre>
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