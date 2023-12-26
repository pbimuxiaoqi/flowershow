# URL: https://kb.daxoptimizer.com/d/101900

<!DOCTYPE html>

<html lang="en">
<head>
<meta charset="utf-8"/>
<meta content="IE=edge" http-equiv="X-UA-Compatible"/>
<meta content="width=device-width, initial-scale=1.0" name="viewport"/>
<title>SUMX iterator excessive CallbackDataId - DAX Optimizer Knowledge Base</title>
<meta content="#12B465" name="theme-color"/>
<link href="/assets/images/icon-228.png" media="(prefers-color-scheme: light)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228-dark.png" media="(prefers-color-scheme: dark)" rel="shortcut icon" sizes="228x228"/>
<link href="/assets/images/icon-228.png" rel="apple-touch-icon"/>
<link href="/assets/style/main.min.css" rel="stylesheet"/>
</head>
<body class="page-sumx-iterator-excessive-callbackdataid">
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
<div class="super-title">KB 101900</div>
<a href="/d/101900"><h1>SUMX iterator excessive CallbackDataId</h1></a>
<hr/>
</header>
<p>Avoid excessive CallbackDataId calls by reducing iterator cardinality.</p>
<h2 id="remarks">Remarks</h2>
<p>The presence of a function with a column reference iterating a large table can produce a large number of calls to the formula engine with the same values. With a <a href="https://dax.guide/sumx/">SUMX</a> iterator and an expression that computes a product wiht an additive measure, it could be possible to reduce the cardinality of the iterator and produce the same result. The benefit is a reduced number of callbacks to the formula engine, which results in better performance.</p>
<h2 id="example-1">Example 1</h2>
<p>Store in a variable the <a href="https://dax.guide/sum/">SUM</a> of <em>Sales[Line Amount]</em> for each <em>Sales[Order Date]</em>, then iterate the variable and compute the product by <em>ExchangeRate[Rate]</em> calling <a href="https://dax.guide/lookupvalue/">LOOKUPVALUE</a> for each <em>Sales[Order Date]</em> instead of each row in <em>Sales</em>.</p>
<h3 id="original-code">Original code</h3>
<pre><span class="issue">SUMX (
    <span class="toedit">Sales</span>,
    <span class="toedit">Sales[LineAmount]</span></span>
        * LOOKUPVALUE (
            ExchangeRates[Rate],
            ExchangeRates[Date], <span class="issue">Sales[Order Date]</span>
        )
<span class="issue">)</span></pre>
<h3 id="possible-optimization">Possible optimization</h3>
<pre><span class="added">VAR _AggregateAtGranularity = 
    ADDCOLUMNS ( 
        VALUES ( <span class="issue">Sales[Order Date]</span> ),    
        "@Amount", CALCULATE ( SUM ( <span class="issue">Sales[LineAmount]</span> ) ) 
    )
VAR Result =</span>
    <span class="issue">SUMX (
        <span class="edited">_AggregateAtGranularity</span>,
        <span class="edited">[@Amount]</span></span>
            * LOOKUPVALUE (
                ExchangeRates[Rate],
                ExchangeRates[Date], <span class="issue">Sales[Order Date]</span>
            )
    <span class="issue">)</span>
<span class="added">RETURN Result</span></pre>
<h2 id="example-2">Example 2</h2>
<p>Store in a variable the <a href="https://dax.guide/sum/">SUM</a> of <em>Sales[Line Amount]</em> for each <em>Date[Year]</em> that is referenced in <em>Sales</em>, then iterate the variable and compute the product by <em>Rates[InflationRate]</em> calling <a href="https://dax.guide/lookupvalue/">LOOKUPVALUE</a> for each <em>Date[Year]</em> instead of each row in <em>Sales</em>.</p>
<h3 id="original-code-1">Original code</h3>
<pre><span class="issue">SUMX (
    <span class="toedit">Sales</span>,
    <span class="toedit">Sales[LineAmount]</span></span>
        * LOOKUPVALUE (
            Rates[InflationRate],
            Rates[Year], <span class="issue"><span class="toremove">RELATED (</span> 'Date'[Year] <span class="toremove">)</span></span>
        )
<span class="issue">)</span></pre>
<h3 id="possible-optimization-1">Possible optimization</h3>
<pre><span class="added">VAR _GroupByDependency = 
    SUMMARIZE (
        Sales, 
        <span class="issue">'Date'[Year]</span>
    )
VAR _AggregateAtGranularity = 
    ADDCOLUMNS ( 
        _GroupByDependency,    
        "@Amount", CALCULATE ( SUM ( <span class="issue">Sales[LineAmount]</span> ) ) 
    )
VAR Result =</span>
    <span class="issue">SUMX (
        <span class="edited">_AggregateAtGranularity</span>,
        <span class="edited">[@Amount]</span></span>
            * LOOKUPVALUE (
                Rates[InflationRate],
                Rates[Year], <span class="issue">'Date'[Year]</span>
            )
    <span class="issue">)</span>
<span class="added">RETURN Result</span></pre>
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