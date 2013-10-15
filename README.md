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
  <li>SERVER SIDE IMPORTS</li>
  <li>OUTPUT FORMATTING</li>
  <li>COMMENTS</li>
</ol>

<p><strong>Note:</strong> The following SASS Examples below are shown in SCSS Syntax</p>

<h2>1.VARIABLES</h2>
<p>SASS USES: <code>$</code></p>
<p>LESS USES: <code>@</code></p>

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

<h2>6.Color Functions</h2>

<strong>Note:</strong>
<p>Both SASS & LESS provide similar color functions</p>
<p><a href="http://sass-lang.com/documentation/Sass/Script/Functions.html">See all in <strong>SASS</strong></a></p>
<p><a href="http://lesscss.org/#reference">See all in <strong>LESS</strong></a></p>

<p><strong>Accessors:</strong></p>
<ul>
	<li><code>red($color)</code></li>
	<li><code>green($color)</code></li>
	<li><code>blue($color)</code></li>
	<li><code>hue($color)</code></li>
	<li><code>saturation($color)</code></li>
	<li><code>lightness($color)</code></li>
	<li><code>alpha($color)</code></li>
</ul>

<p><strong>Mutators:</strong></p>
<ul>
	<li><code>lighten($color, $amount)</code></li>
	<li><code>darken($color, $amount)</code></li>
	<li><code>saturate($color, $amount)</code></li>
	<li><code>desaturate($color, $amount)</code></li>
	<li><code>adjust-hue($color, $amount)</code></li>
	<li><code>opacify($color, $amount)</code></li>
	<li><code>transparentize($color, $amount)</code></li>
	<li><code>mix($color1, $color2[, $amount])</code></li>
	<li><code>grayscale($color)</code></li>
	<li><code>compliment($color)</code></li>
</ul>

<h2>7.Handling with Numbers</h2>

<p>Christ Eppstein said that SASS supports "supports unit-based arithmetic": Complex units are supported in any intermediate form and will only raise an error if you try to print out the value of a complex unit.</p>
<p>Sass will let you define your own units and will happily print out unknown units into your css. Less will not. Sass does this as a form of future proofing against changes in the w3c specification or in case a browser introduces a non-standard unit.</p>
<p>SASS:</p>
<pre>
1cm * 1em => 1 cm * em
2in * 3in => 6 in * in
(1cm / 1em) * 4em => 4cm
2in + 3cm + 2pc => 3.514in
3in / 2in => 1.5
</pre>
<p>LESS:</p>
<pre>
1cm * 1em => Error
2in * 3in => 6in
(1cm / 1em) * 4em => Error
2in + 3cm + 2pc => Error
3in / 2in => 1.5in	
</pre>

<h2>8.Functions & Loop Conditionals</h2>

<h3>Control Directives</h3>
<p>SASS:</p>
<ul>
	<li><code>@IF</code></li>
	<li><code>@ELSE IF</code></li>
	<li><code>@ELSE</code></li>
	<li><code>@THEN</code></li>
	<li><code>@FOR</code></li>
	<li><code>@WHILE</code></li>
</ul>
<p>LESS:</p>
<ul>
	<li><code>WHEN</code></li>
</ul>

<h3>Functions Example - Mixin</h3>
<strong>Note:</strong>
<p>Let's say we want to create a mixin function that makes the background-color depend from the font lightness of the font color:</p>

<p>Do it with SASS:</p>
<pre>
@if lightness($color) > 30% {
  background-color: black;
}
@else {
  background-color: white;
}
</pre>

<p>Do it with LESS:</p>
<pre>
.mixin (@color) when (lightness(@color) > 30%) {
  background-color: black;
}
.mixin (@color) when (lightness(@color) = 30%) {
  background-color: white;
}
</pre>

<h3>Generate a useful easy Loop with <strong>SASS:</strong></h3>
<pre>
$emotions: happy sad excited mustached;
@each $emotion in $emotions {
	.feeling-#{emotion} {
	background-image:
	url("images/feeling-#{$emotion}");
	}
}	
</pre>

<p>SASS Loop Compiled to <strong>CSS:</strong></p>
<pre>
.feeling-happy {
	background-image: url("images/feeling-happy");
}
.feeling-sad {
	background-image: url("images/feeling-sad");
}		
.feeling-excited {
	background-image: url("images/feeling-excited");
}	
.feeling-mustached {
	background-image: url("images/feeling-mustached");
}	
</pre>
<p><strong>Note:</strong></p><p>It is also possible to generate Loops with LESS but it's a little bit more complicated with the <code>WHEN</code> directive. Loops could be very useful if you have to generate a lot of code. It saves your time.</p>

<h2>9.Media Queries</h2>

<strong>Note:</strong>
<p>It's very useful to use variables for the naming of Media Query Breakpoints</p>

<p>SASS EXAMPLE (for LESS use the variables with an <code>@</code>:</p>
<pre>
$small-breakpoint: 480px;
$medium-breakpoint: 768px;
$large-breakpoint: 1024px;

div {
	width: 100%;

	@media screen and (min-width: $small-breakpoint) {
	width: 100px;
	display: inline-block;
	}

	@media screen and (min-width: $medium-breakpoint) {
	width: 200px;	
	}

	@media screen and (min-width: $large-breakpoint) {
	width: 400px;
	}

}
</pre>

<p>With SASS you can do it more fancy with <strong>Control Directives</strong>:</p>

<pre>
@mixin respond-to($name){
	@if $name == small-screen {
		@media only screen and (min-width: 320px) {
			@content
		}
	}
	@if $name == large-screen {
		@media only screen and (min-width: 960px) {
			@content
		}
	}		
}

aside {
	width: 25%;
	@include respond-to(small-screen) {
		width: 100%;
	}	
}
</pre>

<h2>10.Namespaces</h2>
<p><strong>Note:</strong></p>
<p>Less provides the feature of Namespaces that SASS can't do. The founder of SASS considered this feature and decided that adding it would create fragility and unexpected interconnectedness.</p>

<p>How to code Namespaces with LESS:</p>
<pre>
#bundle () {
  .red { background-color: red }
  .green { background-color: green }
}

.foo {
  #bundle > .red;
}
</pre>
<p>In compiled <strong>CSS</strong>:</p>
<pre>
.foo {
  background-color: red;
}
</pre>


<h2>11.Server Side Imports</h2>
<p><code>SASS</code>& <code>LESS</code> will <code>@import</code> other files. That's very useful because you can build your css modular, scalable and maintainable.</p>

<h2>12.Output formatting</h2>

<p>3 Outputs of <strong>LESS</strong></p>
<ul>
	<li><code>normal</code></li>
	<li><code>compressed</code></li>
	<li><code>yui-compressed</code></li>
</ul>

<p>4 Outputs of <strong>SASS</strong></p>
<ul>
	<li><code>nested</code></li>
	<li><code>compact</code></li>
	<li><code>compressed</code></li>
	<li><code>expanded</code></li>
</ul>

<h2>13.Comments</h2>
<p>Both Support C-Style (<code>/* */</code>) and C++ Style Comments (<code>//</code>) </p>


