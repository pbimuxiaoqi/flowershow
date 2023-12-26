# URL: https://kb.daxoptimizer.com/d/101700

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>SUMX iterator cardinality reduction to single column - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-sumx-iterator-cardinality-reduction-to-single-column">
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
<div class="super-title">KB 101700</div>
<a href="/d/101700"><h1>SUMX iterator cardinality reduction to single column</h1></a>
<hr/>
</header>
<p>Investigate if the cardinality of the iterated table can be reduced by iterating a single column.</p>
<h2 id="remarks">Remarks</h2>
<p>The <a href="https://dax.guide/sumx/">SUMX</a> function iterates an entire table, but the expression evaluated for each row seems related to a single column of the table with a product operation that requires a context transition.</p>
<p>If the result of the measure is additive and consistent even when the context transition has only one value of the column instead of a row of the table, then the iterator cardinality can be reduced to the unique values of the column instead of iterating the entire table. Use <a href="https://dax.guide/distinct/">DISTINCT</a> to iterate the column values to be consistent with a table reference, or use <a href="https://dax.guide/values/">VALUES</a> to include the blank row if needed for the correct evaluation.</p>
<h2 id="example">Example</h2>
<p>Replace the <em>Customer</em> table reference with <a href="https://dax.guide/distinct/">DISTINCT</a> on <em>Customer[Discount]</em>.</p>
<h3 id="original-code">Original code</h3>
<pre>SUMX ( 
    <span class="issue toedit">Customer</span>, 
    Customer[Discount] * [Sales Amount] 
)</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre>SUMX ( 
    <span class="issue edited">DISTINCT ( Customer[Discount] )</span>, 
    Customer[Discount] * [Sales Amount] 
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