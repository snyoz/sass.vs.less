<h1>Differences in SASS &amp; LESS</h1>
============

<ol>
  <li>VARIABLES</li>
  <li>NESTED SELECTORS</li>
  <li>MIXINS</li>
  <li>DYNAMIC MIXINS (with Arguments)</li>
  <li>SELECTOR INHERITANCE</li>
  <li>COLOR FUNCTIONS</li>
  <li>HANDLING WITH NUMBERS</li>
  <li>FUNCTIONS & LOOP CONDITIONALS</li>
  <li>MEDIA QUERIES</li>
  <li>NAMESPACES</li>
<ol>

<p><strong>Note:</strong> The following SASS Examples are used in SCSS Syntax</p>

<h2>VARIABLES</h2>
<p>SASS USES: <strong>$</strong></p>
<p>LESS USES: <strong>@</strong></p>

<pre>
Sass                     | Less
-------------------------+-----------------
$colorPrimary: #333;     | @colorPrimary: #333;
$siteWidth: 960px;       | @siteWidth: 960px;  
                         |
body {                   | body {
  color: $colorPrimary;  |   color: @colorPrimary;
  width: $siteWidth;     |   width: @siteWidth;
}                        | }
</pre>

<p><strong>SCOPING NOTE:</strong>SASS is using the var scoping of ruby. Less is using JavaScript Scoping. In future updates of SASS you will be able to change the scoping with special declarations.</p>

<strong>EXAMPLE:</strong>
<pre>
Sass                     | Less
-------------------------+-----------------
$color: black;                           |  @color: black;
                                         |
.scoped {                                |  .scoped {  
  $color: white;                         |    @color: white;
  color: $color;                         |    color: $color;
}                                        |  }  
                                         |
.unscoped {                              |  .unscoped {
  //SASS = white (overwritten by local)  |   // LESS = black (global)
  color: $color;                         |   color: @color;
}                                        |  }
</pre>
