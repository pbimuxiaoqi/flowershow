# URL: https://kb.daxoptimizer.com/d/101000

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Function replace IFERROR/DIVIDE - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-function-replace-iferror-divide">
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
<div class="super-title">KB 101000</div>
<a href="/d/101000"><h1>Function replace IFERROR/DIVIDE</h1></a>
<hr/>
</header>
<p>The <a href="https://dax.guide/iferror/">IFERROR</a> function can be replaced by <a href="https://dax.guide/divide/">DIVIDE</a>.</p>
<h2 id="remarks">Remarks</h2>
<p>The <a href="https://dax.guide/iferror/">IFERROR</a> function catches any error, including conversion errors. When the expression is a <a href="https://dax.guide/op/division/">division operator</a>, the error that is more likely to happen is a division by zero. The <a href="https://dax.guide/divide/">DIVIDE</a> function specifically manages the division by zero condition without intercepting any other error, resulting in faster execution time.</p>
<h2 id="directquery">DirectQuery</h2>
<p>You can <a href="https://docs.daxoptimizer.com/glossary/ignored"><strong>Ignore</strong></a> the issue if the model is in DirectQuery mode.</p>
<p>This optimization can be counterproductive in <a href="https://docs.daxoptimizer.com/reference/directquery-models">DirectQuery models</a>. The <a href="https://dax.guide/iferror/">IFERROR</a> function is usually folded into a query to the underlying database, whereas the <a href="https://dax.guide/divide/">DIVIDE</a> function is not. Therefore, this optimization should be used only when the model is in Import mode.</p>
<h2 id="example">Example</h2>
<p>Replace the <a href="https://dax.guide/iferror/">IFERROR</a> function with <a href="https://dax.guide/divide/">DIVIDE</a>, moving the denominator expression in the second argument of <a href="https://dax.guide/divide/">DIVIDE</a>. The second argument of <a href="https://dax.guide/iferror/">IFERROR</a> becomes the third argument of <a href="https://dax.guide/divide/">DIVIDE</a>.</p>
<h3 id="original-code">Original code</h3>
<pre><span class="issue"><span class="toedit">IFERROR (</span>
    [Amount] <span class="toedit">/</span> [Quantity], 
    0
)</span></pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre><span class="issue"><span class="edited">DIVIDE (</span>
    [Amount]<span class="edited">,</span>
    [Quantity],
    0
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