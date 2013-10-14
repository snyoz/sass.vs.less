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

<p><strong>Note:</strong> The following SASS Examples below are shown in SCSS Syntax</p>

<h2>1.VARIABLES</h2>
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

<p><strong>SCOPING NOTE:</strong></p>
<p>SASS is using the var scoping of ruby. Less is using JavaScript Scoping. In future updates of SASS you will be able to change the scoping with special declarations.</p>

<strong>EXAMPLE:</strong>
<pre>
Sass                                     | Less
-----------------------------------------+-----------------
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

<h2>2.Nested Selectors</h2>
<p>The example below shows that there is <strong>no difference</strong> in nesting.</p>
<pre>
  Sass             | Less
-------------------+-----------------
p {                | p {
  a {              |   a {
    color: red;    |     color: red;
    &:hover {      |     &:hover {
      color: blue; |       color: blue;
    }              |     }
  }                |   }
}                  | }
</pre>

<h2>3.Mixins</h2>
<pre>
Sass                              | Less
----------------------------------+----------------------------------
@mixin bordered {                 | .bordered() {
  border-top: dotted 1px black;   |   border-top: dotted 1px black;
  border-bottom: solid 2px black; |   border-bottom: solid 2px black;
}                                 | }
                                  | 
#menu a {                         | #menu a {
  @include bordered;              |   .bordered;
}     
</pre>
<p><strong>Note:</strong></p>
<p>A Class with an empty argument " () " will be used as mixin in LESS. That means that they will not be compiled into the .css if they are not in use. Advantage: It is also possible to use normal classes as mixins.</p>

<h2>4.DYNAMIC MIXINS (with Arguments)</h2>
<pre>
Sass                              | Less
----------------------------------+----------------------------------
@mixin bordered($width: 2px) {    | .bordered(@width: 2px) {
  border: $width solid black;     |   border: @width solid black;
}                                 | }
                                  | 
#menu a {                         | #menu a {
  @include bordered(4px);         |   .bordered(4px);
}                                 | }
</pre>

<h2>5.Selector Inheritance</h2>
<pre>
Sass                        | Less (since 1.4.0)          | CSS Output
----------------------------+-----------------------------+---------------------------
.bordered {                 | .bordered {                 | .bordered, #menu a {
  border: 1px solid back;   |   border: 1px solid back;   |   border: 1px solid back;
}                           |  }                          |  }
                            |                             |
#menu a {                   | #menu a {                   |
  @extend .bordered;        |   &:extend(.bordered);      |
}                           | }                           |
                            |  // OR USE IT THIS WAY:     | 
                            | #menu a:extend(.bordered) { | 
                            | }
</pre>
