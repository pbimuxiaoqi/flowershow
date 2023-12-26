# URL: https://kb.daxoptimizer.com/d/100800

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Filter modifier function not used as filter argument - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-filter-modifier-function-not-used-as-filter-argument">
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
<div class="super-title">KB 100800</div>
<a href="/d/100800"><h1>Filter modifier function not used as filter argument</h1></a>
<hr/>
</header>
<p>A filter modifier function (filter modifier or filter removal) is not used as a filter argument.</p>
<h2 id="remarks">Remarks</h2>
<p>A filter modifier like <a href="https://dax.guide/allexcept/">ALLEXCEPT</a> is materialized when used as a table argument in other functions like <a href="https://dax.guide/filter/">FILTER</a>. The filter modifier should be used as a filter argument, applying other predicates as individual filter arguments in <a href="https://dax.guide/calculate/">CALCULATE</a>. This way, the materialization of functions like <a href="https://dax.guide/allexcept/">ALLEXCEPT</a> is avoided providing better performance.</p>
<h2 id="example">Example</h2>
<p>Remove the <a href="https://dax.guide/filter/">FILTER</a> function so that <a href="https://dax.guide/allexcept/">ALLEXCEPT</a> acts as a filter modifier for <a href="https://dax.guide/calculate/">CALCULATE</a> and the filter context adds only a column filter on <em>Sales[Quantity]</em> instead of filter with the expanded table <em>Sales</em> without <em>Customer</em> columns.</p>
<h3 id="original-code">Original code</h3>
<pre>CALCULATE (
    SUM ( Sales[Quantity] ),
    <span class="toremove">FILTER (</span>
        <span class="issue">ALLEXCEPT ( Sales, Customer ),</span>
        Sales[Quantity] &gt; 1000
    <span class="toremove">)</span>
)</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre>CALCULATE (
    SUM ( Sales[Quantity] ),
    <span class="issue">ALLEXCEPT ( Sales, Customer ),</span>
    Sales[Quantity] &gt; 1000
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