# URL: https://kb.daxoptimizer.com/d/100400

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Filtered table as iterator - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-filtered-table-as-iterator">
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
<div class="super-title">KB 100400</div>
<a href="/d/100400"><h1>Filtered table as iterator</h1></a>
<hr/>
</header>
<p>A filtered table is used as an iterator instead of modifying the filter context.</p>
<h2 id="remarks">Remarks</h2>
<p>An iterator over the result of <a href="https://dax.guide/filter/">FILTER</a> results in nested iterators, which are not ideal for an optimal query plan. Whenever possible, the table iterated by <a href="https://dax.guide/filter/">FILTER</a> should be filtered through the filter context, moving the filter condition(s) in <a href="https://dax.guide/calculate/">CALCULATE</a> filter argument(s).</p>
<h2 id="example-1">Example 1</h2>
<p><strong>Move the filter condition in a CALCULATE filter argument.</strong> Remove the <a href="https://dax.guide/filter/">FILTER</a> iterator and wrap <a href="https://dax.guide/sumx/">SUMX</a> into a <a href="https://dax.guide/calculate/">CALCULATE</a>, placing the filter condition into a filter argument wrapped into <a href="https://dax.guide/keepfilters/">KEEPFILTERS</a> to maintain the original semantics.</p>
<h3 id="original-code">Original code</h3>
<pre>SUMX (
    <span class="issue"><span class="toremove">FILTER (</span> 
        Sales, 
        <span class="toremove">RELATED (</span> <span class="toedit">Customer[Country]</span> <span class="toremove">)</span> <span class="toedit">= "Canada"</span>
    <span class="toremove">),</span></span>
    Sales[Line Amount]
)</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre><span class="added">CALCULATE (</span>
    SUMX (
        <span class="issue">Sales,</span>
        Sales[Line Amount]
    )<span class="added">,</span>
    <span class="added">KEEPFILTERS ( </span><span class="edited">Customer[Country] = "Canada"</span> <span class="added">)</span>
<span class="added">)</span>
</pre>
<h2 id="example-2">Example 2</h2>
<p><strong>Move the filter conditions evaluated by an AND operator in two CALCULATE filter arguments.</strong> Remove the <a href="https://dax.guide/filter/">FILTER</a> iterator and wrap <a href="https://dax.guide/sumx/">SUMX</a> into a <a href="https://dax.guide/calculate/">CALCULATE</a>, splitting the <a href="https://dax.guide/op/and/">&amp;&amp;</a> arguments in two filter arguments, each one wrapped into <a href="https://dax.guide/keepfilters/">KEEPFILTERS</a> to maintain the original semantics.</p>
<h3 id="original-code-1">Original code</h3>
<pre>SUMX (
    <span class="issue"><span class="toremove">FILTER (</span> 
        Sales, 
        <span class="toremove">RELATED (</span> <span class="toedit">Customer[Country]</span> <span class="toremove">)</span> <span class="toedit">= "Canada"</span>
            <span class="toremove">&amp;&amp; RELATED (</span> <span class="toedit">Customer[City]</span> <span class="toremove">)</span> <span class="toedit">= "Vancouver"</span>
    ),</span>
    Sales[Line Amount]
)</pre>
<h3 id="possible-optimization-1">Possible optimization</h3>
<pre><span class="added">CALCULATE (</span>
    SUMX (
        <span class="issue">Sales,</span>
        Sales[Line Amount]
    )<span class="added">,</span>
    <span class="added">KEEPFILTERS ( </span><span class="edited">Customer[Country] = "Canada"</span> <span class="added">)</span><span class="added">,</span>
    <span class="added">KEEPFILTERS ( </span><span class="edited">Customer[City] = "Vancouver"</span> <span class="added">)</span>
<span class="added">)</span>
</pre>
<h2 id="example-3">Example 3</h2>
<p><strong>Move the filter conditions evaluated by an OR operator in one CALCULATE filter argument.</strong> Remove the <a href="https://dax.guide/filter/">FILTER</a> iterator and wrap <a href="https://dax.guide/sumx/">SUMX</a> into a <a href="https://dax.guide/calculate/">CALCULATE</a>, placing the filter condition based on an <a href="https://dax.guide/op/or/">||</a> operator into a single filter argument wrapped into <a href="https://dax.guide/keepfilters/">KEEPFILTERS</a> to maintain the original semantics.</p>
<h3 id="original-code-2">Original code</h3>
<pre>SUMX (
    <span class="issue"><span class="toremove">FILTER (</span> 
        Sales, 
        <span class="toremove">RELATED (</span> <span class="toedit">Customer[Country]</span> <span class="toremove">)</span> <span class="toedit">= "Canada"</span>
            <span class="toedit">||</span> <span class="toremove">RELATED (</span> <span class="toedit">Customer[City]</span> <span class="toremove">)</span> <span class="toedit">= "Seattle"</span>
    ),</span>
    Sales[Line Amount]
)</pre>
<h3 id="possible-optimization-2">Possible optimization</h3>
<pre><span class="added">CALCULATE (</span>
    SUMX (
        <span class="issue">Sales,</span>
        Sales[Line Amount]
    )<span class="added">,</span>
    <span class="edited">Customer[Country] = "Canada"</span>
        <span class="edited">|| Customer[City] = "Seattle"</span>
<span class="added">)</span>
</pre>
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