# URL: https://kb.daxoptimizer.com/d/100700

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Function replace GROUPBY/SUMMARIZE - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-function-replace-groupby-summarize">
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
<div class="super-title">KB 100700</div>
<a href="/d/100700"><h1>Function replace GROUPBY/SUMMARIZE</h1></a>
<hr/>
</header>
<p>The GROUPBY function can be replaced by <a href="https://dax.guide/summarize/">SUMMARIZE</a>.</p>
<h2 id="remarks">Remarks</h2>
<p>The <a href="https://dax.guide/groupby/">GROUPBY</a> function should be used only when the table cannot be used in <a href="https://dax.guide/summarize/">SUMMARIZE</a> or when there are specific features of <a href="https://dax.guide/groupby/">GROUPBY</a> that are necessary for the calculation. Whenever possible, use <a href="https://dax.guide/summarize/">SUMMARIZE</a> instead of <a href="https://dax.guide/groupby/">GROUPBY</a>.</p>
<h2 id="example">Example</h2>
<p>Replace <a href="https://dax.guide/groupby/">GROUPBY</a> with <a href="https://dax.guide/summarize/">SUMMARIZE</a>.</p>
<h3 id="original-code">Original code</h3>
<pre>SUMX (
    <span class="issue"><span class="toedit">GROUPBY</span> (
        'Sales',
        'Sales'[ProductKey],
        'Sales'[CustomerKey],
        'Sales'[DateKey]
    )</span>,
    [Sales Amount]
)</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre>SUMX (
    <span class="issue"><span class="edited">SUMMARIZE</span> (
        'Sales',
        'Sales'[ProductKey],
        'Sales'[CustomerKey],
        'Sales'[DateKey]
    )</span>,
    [Sales Amount]
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