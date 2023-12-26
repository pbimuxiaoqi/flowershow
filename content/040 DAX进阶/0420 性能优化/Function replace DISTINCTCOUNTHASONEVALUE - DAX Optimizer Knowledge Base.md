# URL: https://kb.daxoptimizer.com/d/101400

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Function replace DISTINCTCOUNT/HASONEVALUE - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-function-replace-distinctcount-hasonevalue">
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
<div class="super-title">KB 101400</div>
<a href="/d/101400"><h1>Function replace DISTINCTCOUNT/HASONEVALUE</h1></a>
<hr/>
</header>
<p><a href="https://dax.guide/distinctcount/">DISTINCTCOUNT</a> function can be replaced by <a href="https://dax.guide/hasonevalue/">HASONEVALUE</a>.</p>
<h2 id="remarks">Remarks</h2>
<p>The code that compares the result of <a href="https://dax.guide/distinctcount/">DISTINCTCOUNT</a> with 1 can be replaced with the function <a href="https://dax.guide/hasonevalue/">HASONEVALUE</a>.
This recommendation does not have a relevant impact on performance, but it is a best practice that improves code readability.</p>
<h2 id="example">Example</h2>
<p>Replace <a href="https://dax.guide/distinctcount/">DISTINCTCOUNT</a> and the comparison with <a href="https://dax.guide/hasonevalue/">HASONEVALUE</a>.</p>
<h3 id="original-code">Original code</h3>
<pre>IF (
    <span class="issue"><span class="toedit">DISTINCTCOUNT</span> ( Customer[CustomerKey] ) <span class="toremove">= 1</span>,</span>
    "Customer Name : " &amp; Customer[Name],
    "Undefined"
)</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre>IF (
    <span class="issue"><span class="edited">HASONEVALUE</span> ( Customer[CustomerKey] ),</span>
    "Customer Name : " &amp; Customer[Name],
    "Undefined"
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