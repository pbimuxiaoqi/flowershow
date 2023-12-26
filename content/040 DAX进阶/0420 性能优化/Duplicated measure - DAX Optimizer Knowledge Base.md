# URL: https://kb.daxoptimizer.com/d/100200

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>Duplicated measure - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-duplicated-measure">
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
<div class="super-title">KB 100200</div>
<a href="/d/100200"><h1>Duplicated measure</h1></a>
<hr/>
</header>
<p>There are multiple references to the same measure executed with an identical filter context.</p>
<h2 id="remarks">Remarks</h2>
<p>Two measure references can return different results when executed in different filter contexts, but within the same filter context the result should be the same. However, the formula engine might perform redundant evaluations of the same expressions even though the storage engine usually does not execute duplicated requests.</p>
<p>A possible optimization is to store the result of a measure reference in a variable, and then reference the variable. It is important to assign the variable only when the execution scope guarantees that the variable is used at least once, otherwise the result could be counterproductive and slow down the execution time instead of improving it.</p>
<h2 id="example-1">Example 1</h2>
<p><strong>Evaluate the measure only once and assign it to a variable.</strong> If the measure <em>ExchangeRate</em> does not depend on the rows iterated in <em>Sales</em>, compute the Exchange Rate in a variable before starting the iterator.</p>
<h3 id="original-code">Original code</h3>
<pre>IF ( 
    <span class="issue toedit">[Sales Quantity]</span> &gt; 0 &amp;&amp; <span class="issue toedit">[Sales Amount]</span> &gt; 0, 
    <span class="issue toedit">[Sales Quantity]</span> / <span class="issue toedit">[Sales Amount]</span>
)</pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre><span class="added">VAR _quantity = <span class="issue">[Sales Quantity]</span>
VAR _amount = <span class="issue">[Sales Amount]</span>
RETURN</span>
    IF ( 
        <span class="edited">_quantity</span> &gt; 0 &amp;&amp; <span class="edited">_amount</span> &gt; 0, 
        <span class="edited">_quantity</span> / <span class="edited">_amount</span>
    )</pre>
<h2 id="example-2">Example 2</h2>
<p><strong>Evaluate the measure only once in and assign it to a variable in a proper scope.</strong> <em>Sales Quantity</em> is evaluated twice in the FILTER iterator and can be computed only once in a variable defined in the same iterator. <em>Sales Quantity</em> before the iterator is evaluated only once in a different scope and does not require a variable.</p>
<h3 id="original-code-1">Original code</h3>
<pre>
IF (
    [Sales Quantity] &gt; 0,
    COUNTROWS ( 
        FILTER (
            Customer,
            <span class="issue toedit">[Sales Quantity]</span> &gt; 0
                &amp;&amp; <span class="issue toedit">[Sales Quantity]</span> &lt;= 5,
        )
    )
)</pre>
<h3 id="possible-optimization-1">Possible optimization</h3>
<pre>
IF (
    [Sales Quantity] &gt; 0,
    COUNTROWS ( 
        FILTER (
            Customer,
            <span class="added">VAR _quantity = [Sales Quantity]</span>
            <span class="added">RETURN</span>
                <span class="edited">_quantity</span> &gt; 0
                    &amp;&amp; <span class="edited">_quantity</span> &lt;= 5,
        )
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