# URL: https://kb.daxoptimizer.com/d/100900

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Blank comparison - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-blank-comparison">
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
<div class="super-title">KB 100900</div>
<a href="/d/100900"><h1>Blank comparison</h1></a>
<hr/>
</header>
<p><a href="https://dax.guide/blank/">BLANK</a> is used for comparison in a binary operator where the operator is not strict equal to (==).</p>
<h2 id="remarks">Remarks</h2>
<p>When the <a href="https://dax.guide/blank/">BLANK</a> function is used as an operand in a binary comparison operation, the engine performs an implicit conversion to compare the computed value with both 0 and <a href="https://dax.guide/blank/">BLANK</a>, which has a small CPU cost. 
Moreover, a comparison with BLANK is often incorrect as 0 or an empty string (“”) returns TRUE if compared with <a href="https://dax.guide/op/equal-to/">=</a> to <a href="https://dax.guide/blank/">BLANK</a>.</p>
<h2 id="example">Example</h2>
<p>Replace the <a href="https://dax.guide/op/equal-to/">=</a> operator with <a href="https://dax.guide/op/strictly-equal-to/">==</a> os use <a href="https://dax.guide/isblank/">ISBLANK</a> to get the right behavior and better performance.</p>
<h3 id="original-code">Original code</h3>
<pre>CALCULATE (
    [Sales Amount], 
    <span class="issue">Product[Brand] <span class="toedit">=</span> BLANK()</span>
)</pre>
<h3 id="possible-optimization-1">Possible optimization 1</h3>
<pre>CALCULATE (
    [Sales Amount], 
    <span class="issue">Product[Brand] <span class="edited">==</span> BLANK()</span>
)</pre>
<h3 id="possible-optimization-2">Possible optimization 2</h3>
<pre>CALCULATE (
    [Sales Amount], 
    <span class="issue"><span class="added">ISBLANK (</span> Product[Brand] <span class="added">)</span></span>
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