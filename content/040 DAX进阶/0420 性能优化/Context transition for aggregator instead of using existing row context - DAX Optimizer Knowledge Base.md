# URL: https://kb.daxoptimizer.com/d/101100

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Context transition for aggregator instead of using existing row context - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-context-transition-for-aggregator-instead-of-using-existing-row-context">
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
<div class="super-title">KB 101100</div>
<a href="/d/101100"><h1>Context transition for aggregator instead of using existing row context</h1></a>
<hr/>
</header>
<p>An aggregator function (like <a href="https://dax.guide/sum/">SUM</a>, <a href="https://dax.guide/min/">MIN</a>, <a href="https://dax.guide/max/">MAX</a>, …) is executed within a context transition instead of using a column reference in the existing row context.</p>
<h2 id="remarks">Remarks</h2>
<p>The row context of an iterator is transformed into a filter context with the context transition produced by <a href="https://dax.guide/calculate/">CALCULATE</a>, providing a filter context that has only one row when the iterated table has unique rows. In this condition, the aggregation function only groups a single row, returning the same result that would have been obtained by using a column reference on the existing row context.</p>
<p>From a performance standpoint, the context transition consumes CPU and memory, so removing the need of a context transition and removing the aggregation improves performance. The optimization is possible only when the iterated table has unique rows, otherwise the result could be different.</p>
<h2 id="example">Example</h2>
<p>Remove <a href="https://dax.guide/calculate/">CALCULATE</a> and <a href="https://dax.guide/sum/">SUM</a> so that the column reference is evaluated within the row context produced by the iteration over Store.</p>
<h3 id="original-code">Original code</h3>
<pre>SUMX ( 
    Store, 
    <span class="issue"><span class="toremove">CALCULATE ( SUM (</span> Store[Square Meters] <span class="toremove">) )</span></span> 
)</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre>SUMX ( 
    Store, 
    <span class="issue">Store[Square Meters]</span> 
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