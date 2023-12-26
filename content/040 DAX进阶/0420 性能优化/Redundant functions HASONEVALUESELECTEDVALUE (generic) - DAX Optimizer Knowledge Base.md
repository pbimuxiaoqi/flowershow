# URL: https://kb.daxoptimizer.com/d/101500

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Redundant functions HASONEVALUE/SELECTEDVALUE (generic) - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-redundant-functions-hasonevalue-selectedvalue-generic">
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
<div class="super-title">KB 101500</div>
<a href="/d/101500"><h1>Redundant functions HASONEVALUE/SELECTEDVALUE (generic)</h1></a>
<hr/>
</header>
<p>The expression involving <a href="https://dax.guide/hasonevalue/">HASONEVALUE</a> and <a href="https://dax.guide/selectedvalue/">SELECTEDVALUE</a> functions can be optimized by removing <a href="https://dax.guide/hasonevalue/">HASONEVALUE</a>.</p>
<h2 id="remarks">Remarks</h2>
<p><a href="https://dax.guide/selectedvalue/">SELECTEDVALUE</a> returns a non-blank value when there is only one value visible in the referenced column. Embedding <a href="https://dax.guide/selectedvalue/">SELECTEDVALUE</a> in a condition related to <a href="https://dax.guide/hasonevalue/">HASONEVALUE</a> can be redundant: removing <a href="https://dax.guide/hasonevalue/">HASONEVALUE</a> can slightly improve the performance. The code must be refactored so that it returns the same value as the original code, which might be not possible in certain scenarios.</p>
<h2 id="example">Example</h2>
<p>Remove the outer <a href="https://dax.guide/if/">IF</a> function and the <a href="https://dax.guide/hasonevalue/">HASONEVALUE</a> condition.</p>
<h3 id="original-code">Original code</h3>
<pre><span class="issue"><span class="toremove">IF (</span>
    <span class="toremove">HASONEVALUE( Customer[Country] ),</span>
    IF (
        SELECTEDVALUE( Customer[Country] ) = "Canada",
        [Sales Amount]
    )
<span class="toremove">)</span></span></pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre><span class="issue">IF (
    SELECTEDVALUE( Customer[Country] ) = "Canada",
    [Sales Amount]
)</span></pre>
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