# URL: https://kb.daxoptimizer.com/d/101800

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Function usage RELATEDTABLE - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-function-usage-relatedtable">
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
<div class="super-title">KB 101800</div>
<a href="/d/101800"><h1>Function usage RELATEDTABLE</h1></a>
<hr/>
</header>
<p>Checks whether the <a href="https://dax.guide/relatedtable/">RELATEDTABLE</a> function is not needed as there is no active row context.</p>
<h2 id="remarks">Remarks</h2>
<p>If the <a href="https://dax.guide/relatedtable/">RELATEDTABLE</a> function is invoked without an active row context, it does not perform any action. Even though it does not impact performance because there is no context transition involved, it is better to remove the function to make the code easier to read, or re-evaluate the code structure in case the context transition was needed.</p>
<h2 id="example">Example</h2>
<p>Remove <a href="https://dax.guide/relatedtable/">RELATEDTABLE</a> as it is redundant and it does not produce any effect.</p>
<h3 id="original-code">Original code</h3>
<pre>Canada Sales :=
CALCULATE (
    [Sales Amount],
    FILTER ( 
        <span class="issue"><span class="toremove">RELATEDTABLE (</span>
            Customer
        <span class="toremove">)</span></span>,
        Customer[Country] = "Canada"
    )
)</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre>Canada Sales :=
CALCULATE (
    [Sales Amount],
    FILTER ( 
        <span class="issue">Customer</span>,
        Customer[Country] = "Canada"
    )
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