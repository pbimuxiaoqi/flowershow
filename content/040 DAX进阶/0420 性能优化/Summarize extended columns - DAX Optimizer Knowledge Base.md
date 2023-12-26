# URL: https://kb.daxoptimizer.com/d/100600

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Summarize extended columns - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-summarize-extended-columns">
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
<div class="super-title">KB 100600</div>
<a href="/d/100600"><h1>Summarize extended columns</h1></a>
<hr/>
</header>
<p>Extended columns have been added within <a href="https://dax.guide/summarize/">SUMMARIZE</a> instead of using <a href="https://dax.guide/addcolumns/">ADDCOLUMNS</a> for the aggregations and <a href="https://dax.guide/summarize/">SUMMARIZE</a> only for the grouping columns.</p>
<h2 id="remarks">Remarks</h2>
<p>The <a href="https://dax.guide/summarize/">SUMMARIZE</a> behavior for aggregations may produce slower performances compared to an equivalent construct where <a href="https://dax.guide/addcolumns/">ADDCOLUMNS</a> extends the result of <a href="https://dax.guide/summarize/">SUMMARIZE</a> by adding the columns with the calculations.</p>
<p>Recommended articles:</p>
<ul>
<li><a href="https://www.sqlbi.com/articles/best-practices-using-summarize-and-addcolumns/">Best practices using SUMMARIZE and ADDCOLUMNS</a></li>
<li><a href="https://www.sqlbi.com/articles/all-the-secrets-of-summarize/">All the secrets of SUMMARIZE</a></li>
</ul>
<h2 id="example">Example</h2>
<p>Embed SUMMARIZE in an ADDCOLUMNS function moving there the aggregation expressions and the corresponding columns. Add CALCULATE for aggregations to get the equivalent filter context for the argument.</p>
<h3 id="original-code">Original code</h3>
<pre>
SUMMARIZE (
    Sales,
    Customer[Country], 
    'Product'[Brand], 
    <span class="issue">"Revenues", [Sales Amount],
    "Transactions", COUNTROWS ( Sales ),
    "Short Country", LEFT ( Customer[Country], 3 )</span>
)</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre><span class="added">ADDCOLUMNS (</span>
    SUMMARIZE (
        Sales,
        Customer[Country], 
        'Product'[Brand]
    <span class="added">)</span>, 
    <span class="issue">"Revenues", [Sales Amount],
    "Transactions",</span> <span class="added">CALCULATE (</span> <span class="issue">COUNTROWS ( Sales )</span> <span class="added">)</span>,
    <span class="issue">"Short Country", LEFT ( Customer[Country], 3 )</span>
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