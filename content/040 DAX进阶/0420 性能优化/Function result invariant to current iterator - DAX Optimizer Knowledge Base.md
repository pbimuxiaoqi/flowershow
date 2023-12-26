# URL: https://kb.daxoptimizer.com/d/102000

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Function result invariant to current iterator - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-function-result-invariant-to-current-iterator">
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
<div class="super-title">KB 102000</div>
<a href="/d/102000"><h1>Function result invariant to current iterator</h1></a>
<hr/>
</header>
<p>The function within an expression argument of an iterator function does not use the iterator’s row context and can therefore be optimized using a variable.</p>
<h2 id="remarks">Remarks</h2>
<p>The part of an expression executed in a row context that do not depend on the row context might require redundant evaluations of the formula engine, resulting in additional CPU cost. In this case, the function call is identified as part of such redundant expression.</p>
<p>A possible optimization is to store the result of the function call in a variable, and then reference the variable. It is important to assign the variable only when the execution scope guarantees that the variable is used at least once, otherwise the result could be counterproductive and slow down the execution time instead of improving it.</p>
<h2 id="example">Example</h2>
<p><strong>Evaluate the measure before the iterator and assign it to a variable.</strong> The function <a href="https://dax.guide/year/">YEAR</a> depends on a variable assigned before the <a href="https://dax.guide/filter/">FILTER</a> iterator, so also <a href="https://dax.guide/year/">YEAR</a> can be evaluated before <a href="https://dax.guide/filter/">FILTER</a>.</p>
<h3 id="original-code">Original code</h3>
<pre>VAR _LastDate = LASTDATE()
VAR _FilterYear =
    FILTER (
        'Date',
        'Date'[Year] = <span class="issue toedit">YEAR ( _LastDate )</span>
    )
RETURN
    CALCULATE (
        [Sales Amount],
        _FilterYear
    )</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre>VAR _LastDate = LASTDATE()
<span class="added">VAR _Year = <span class="issue">YEAR ( _LastDate )</span></span>
VAR _FilterYear =
    FILTER (
        'Date',
        'Date'[Year] = <span class="edited">_Year</span>
    )
RETURN
    CALCULATE (
        [Sales Amount],
        _FilterYear
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