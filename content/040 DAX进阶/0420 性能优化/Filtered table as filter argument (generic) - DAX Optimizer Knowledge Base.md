# URL: https://kb.daxoptimizer.com/d/100500

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Filtered table as filter argument (generic) - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-filtered-table-as-filter-argument-generic">
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
<div class="super-title">KB 100500</div>
<a href="/d/100500"><h1>Filtered table as filter argument (generic)</h1></a>
<hr/>
</header>
<p>A <a href="https://dax.guide/filter/">FILTER</a> function filtering an entire table is used as a filter argument in functions such as <a href="https://dax.guide/calculate/">CALCULATE</a>, <a href="https://dax.guide/calculatetable/">CALCULATETABLE</a>, etc.</p>
<h2 id="remarks">Remarks</h2>
<p>Instead of materializing an entire table in the filter context, it is better to only filter the columns involved.</p>
<p>By removing the table, it is important to <strong>keep the same semantics as the original filter</strong>, so that the result is not affected. To do that, apply <a href="https://dax.guide/removefilters/">REMOVEFILTERS</a> or <a href="https://dax.guide/keepfilters/">KEEPFILTERS</a> as needed.</p>
<p>Recommended articles:</p>
<ul>
<li><a href="https://www.sqlbi.com/articles/filter-arguments-in-calculate/">Filter arguments in CALCULATE</a></li>
<li><a href="https://www.sqlbi.com/articles/using-keepfilters-in-dax-updated/">Using KEEPFILTERS</a></li>
</ul>
<h2 id="example-1">Example 1</h2>
<p>Move the <a href="https://dax.guide/average/">AVERAGE</a> aggregation before <a href="https://dax.guide/calculate/">CALCULATE</a> and store the result in a variable. Remove the <em>Sales</em> iterator and use <a href="https://dax.guide/keepfilters/">KEEPFILTERS</a> around the condition to maintain the same semantics, so the filter is applied only to the <em>Sales[Unit Price]</em> column specified in the predicate instead of using the entire <em>Sales</em> table.</p>
<h3 id="original-code">Original code</h3>
<pre>CALCULATE (
    [Sales Amount],
    <span class="issue"><span class="toedit">FILTER ( Sales,</span> Sales[Unit Price] &gt; <span class="toedit">AVERAGE ( Sales[Unit Price] )</span> )</span>
)</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre><span class="added">VAR _AveragePrice = </span><span class="issue edited">AVERAGE ( Sales[Unit Price] )</span><span class="added">
RETURN</span>
    CALCULATE (
        [Sales Amount],
        <span class="issue"><span class="edited">KEEPFILTERS (</span> Sales[Unit Price] &gt; <span class="edited">_AveragePrice</span> )</span>
    )</pre>
<h2 id="example-2">Example 2</h2>
<p>Move the <a href="https://dax.guide/max/">MAX</a> aggregation before <a href="https://dax.guide/calculate/">CALCULATE</a> and store the result in a variable. Remove the <em>Date</em> iterator and add <a href="https://dax.guide/removefilters/">REMOVEFILTERS</a> on <em>Date</em> so that the filter context is removed from all the other columns of the <em>Date</em> table to keep the original semantics once the condition only filters <em>Date[Year]</em>.</p>
<h3 id="original-code-1">Original code</h3>
<pre>CALCULATE (
    [Sales Amount],
    <span class="issue"><span class="toremove">FILTER ( 
        ALL ( 'Date' ),</span>
        'Date'[Year] = <span class="toedit">YEAR ( MAX ( 'Date'[Date] ) )</span>
    <span class="toremove">)</span></span>
)</pre>
<h3 id="possible-optimization-1">Possible optimization</h3>
<pre><span class="added">VAR _Year = </span><span class="issue edited">YEAR ( MAX ( 'Date'[Date] ) )</span><span class="added">
RETURN</span>
RETURN
    CALCULATE (
        [Sales Amount],
        <span class="added">REMOVEFILTERS ( 'Date' ),</span>
        <span class="issue">'Date'[Year] = <span class="edited">_Year</span></span>
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