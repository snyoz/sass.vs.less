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


<h2>VARIABLES</h2>
<p>SASS USES: <strong>$</strong></p>
<p>LESS USES: <strong>@</strong></p>

<pre>
Sass             | Less
-----------------+-----------------
$color: red;     | @color: red;
div {            | div {
  color: $color; |   color: @color;
}                | }
</pre>
