# URL: https://kb.daxoptimizer.com/d/101600

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>SUMX with IF predicate on iterator column - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-sumx-with-if-predicate-on-iterator-column">
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
<div class="super-title">KB 101600</div>
<a href="/d/101600"><h1>SUMX with IF predicate on iterator column</h1></a>
<hr/>
</header>
<p>The <a href="https://dax.guide/sumx/">SUMX</a> function contains an <a href="https://dax.guide/if/">IF</a> predicate on a single column filtering the iterated table.</p>
<h2 id="remarks">Remarks</h2>
<p>The <a href="https://dax.guide/if/">IF</a> condition in an iterator can be expensive from a performance standpoint. When the condition only references columns of the iterated table (or the expanded table using <a href="https://dax.guide/related/">RELATED</a>), then it is possible to filter the table through the filter context by using <a href="https://dax.guide/calculate/">CALCULATE</a>. Moreover, if the measure referenced in the second argument of <a href="https://dax.guide/if/">IF</a> is additive, then the <a href="https://dax.guide/sumx/">SUMX</a> iterator can be removed.</p>
<h2 id="example-1">Example 1</h2>
<p>Because the <em>Sales Amount</em> measure is additive, remove the <a href="https://dax.guide/sumx/">SUMX</a> iterator and the <a href="https://dax.guide/if/">IF</a> function. Wrap the <em>Sales Amount</em> measure in a <a href="https://dax.guide/calculate/">CALCULATE</a> function and move the condition from the first argument of the <a href="https://dax.guide/if/">IF</a> function to a filter argument of the <a href="https://dax.guide/calculate/">CALCULATE</a> function, embedded in <a href="https://dax.guide/keepfilters/">KEEPFILTERS</a>.</p>
<h3 id="original-code">Original code</h3>
<pre><span class="issue"><span class="toremove">SUMX (
    Date,
    IF (</span> <span class="toedit">'Date'[DateKey] = 1</span><span class="toremove">,</span> [Sales Amount] <span class="toremove">)
)</span></span></pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre><span class="issue"><span class="added">CALCULATE (</span> 
    [Sales Amount]<span class="added">,</span> 
    <span class="edited">KEEPFILTERS ( 'Date'[DateKey] = 1 )</span>
<span class="added">)</span></span></pre>
<h2 id="example-2">Example 2</h2>
<p>Because the <em>Sales Amount</em> measure is additive, remove the <a href="https://dax.guide/sumx/">SUMX</a> iterator and the <a href="https://dax.guide/if/">IF</a> and <a href="https://dax.guide/related/">RELATED</a> functions. Wrap the <em>Sales Amount</em> measure in a <a href="https://dax.guide/calculate/">CALCULATE</a> function and move the condition (without <a href="https://dax.guide/related/">RELATED</a>) from the first argument of the <a href="https://dax.guide/if/">IF</a> function to a filter argument of the <a href="https://dax.guide/calculate/">CALCULATE</a> function.</p>
<h3 id="original-code-1">Original code</h3>
<pre><span class="issue"><span class="toremove">SUMX (
    'Product',
    IF ( RELATED ( </span> <span class="toedit">'Product Category'[Category]</span> <span class="toremove">)</span><span class="toedit"> = "Audio"</span><span class="toremove">,</span> [Sales Amount] <span class="toedit"><span class="toremove">)
)</span></span></span></pre>
<h3 id="possible-optimization-1">Possible optimization</h3>
<pre><span class="issue"><span class="added">CALCULATE (</span> 
    [Sales Amount]<span class="added">,</span> 
    <span class="edited">KEEPFILTERS ( 'Product Category'[Category] = "Audio" )</span>
<span class="added">)</span></span></pre>
<h2 id="example-3">Example 3</h2>
<p>Because the <em>Last Customer Balance</em> measure is non-additive, remove the <a href="https://dax.guide/sumx/">SUMX</a> iterator and the <a href="https://dax.guide/if/">IF</a> and <a href="https://dax.guide/related/">RELATED</a> functions. Wrap the <em>Sales Amount</em> measure in a <a href="https://dax.guide/calculate/">CALCULATE</a> function and move the condition (without <a href="https://dax.guide/related/">RELATED</a>) from the first argument of the <a href="https://dax.guide/if/">IF</a> function to a filter argument of the <a href="https://dax.guide/calculate/">CALCULATE</a> function.</p>
<h3 id="original-code-2">Original code</h3>
<pre><span class="issue">SUMX (
    Customer,
    <span class="toremove">IF ( </span> <span class="toedit">Customer[Country] = "Canada"</span><span class="toremove">,</span> [Last Customer Balance] <span class="toremove">)</span>
)</span></pre>
<h3 id="possible-optimization-2">Possible optimization</h3>
<pre><span class="issue"><span class="added">CALCULATE (</span> 
    SUMX (
        Customer,
        [Last Customer Balance]
    )<span class="added">,</span>
    <span class="edited">KEEPFILTERS ( Customer[Country] = "Canada" )</span>
<span class="added">)</span></span></pre>
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