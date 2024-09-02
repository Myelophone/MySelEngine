# Simplifier

This is a lightweight jQuery-like library created using vanilla JavaScript to simplify frequent js functions and operations. It supports basic DOM manipulation, event handling, and AJAX requests, and is compatible with IE11.

## Features

- DOM Manipulation (addClass, removeClass, toggleClass, etc.)
- Event Handling (on)
- AJAX Requests (GET, POST, and custom requests)

## Usage

Add next small script (to load the simplifier script in modern way and to check whether dom is loaded) inline into the header in Your project:

```html
<script>
  !function (t, e) { "use strict"; t = t || "domready", e = e || window; var n = [], o = !1, d = !1; function a() { if (!o) { o = !0; for (var t = 0; t < n.length; t++)n[t].fn.call(window, n[t].ctx); n = [] } } function c() { "complete" === document.readyState && a() } e[t] = function (t, e) { if ("function" != typeof t) throw new TypeError("callback for domready(fn) must be a function"); o ? setTimeout(function () { t(e) }, 1) : (n.push({ fn: t, ctx: e }), "complete" === document.readyState || !document.attachEvent && "interactive" === document.readyState ? setTimeout(a, 1) : d || (document.addEventListener ? (document.addEventListener("DOMContentLoaded", a, !1), window.addEventListener("load", a, !1)) : (document.attachEvent("onreadystatechange", c), window.attachEvent("onload", a)), d = !0)) } }("domready", window); (function (e, t) { typeof module != "undefined" && module.exports ? module.exports = t() : typeof define == "function" && define.amd ? define(t) : this[e] = t() })("$script", function () { function p(e, t) { for (var n = 0, i = e.length; n < i; ++n)if (!t(e[n])) return r; return 1 } function d(e, t) { p(e, function (e) { return t(e), 1 }) } function v(e, t, n) { function g(e) { return e.call ? e() : u[e] } function y() { if (!--h) { u[o] = 1, s && s(); for (var e in f) p(e.split("|"), g) && !d(f[e], g) && (f[e] = []) } } e = e[i] ? e : [e]; var r = t && t.call, s = r ? t : n, o = r ? e.join("") : t, h = e.length; return setTimeout(function () { d(e, function t(e, n) { if (e === null) return y(); !n && !/^https?:\/\//.test(e) && c && (e = e.indexOf(".js") === -1 ? c + e + ".js" : c + e); if (l[e]) return o && (a[o] = 1), l[e] == 2 ? y() : setTimeout(function () { t(e, !0) }, 0); l[e] = 1, o && (a[o] = 1), m(e, y) }) }, 0), v } function m(n, r) { var i = e.createElement("script"), u; i.setAttribute("async", true); i.onload = i.onerror = i[o] = function () { if (i[s] && !/^c|loade/.test(i[s]) || u) return; i.onload = i[o] = null, u = 1, l[n] = 2, r() }, i.async = 1, i.src = h ? n + (n.indexOf("?") === -1 ? "?" : "&") + h : n, t.insertBefore(i, t.lastChild) } var e = document, t = e.getElementsByTagName("head")[0], n = "string", r = !1, i = "push", s = "readyState", o = "onreadystatechange", u = {}, a = {}, f = {}, l = {}, c, h; return v.get = m, v.order = function (e, t, n) { (function r(i) { i = e.shift(), e.length ? v(i, r) : v(i, t, n) })() }, v.path = function (e) { c = e }, v.urlArgs = function (e) { h = e }, v.ready = function (e, t, n) { e = e[i] ? e : [e]; var r = []; return !d(e, function (e) { u[e] || r[i](e) }) && p(e, function (e) { return u[e] }) ? t() : !function (e) { f[e] = f[e] || [], f[e][i](t), n && n(r) }(e.join("|")), v }, v.done = function (e) { v([null], e) }, v });
</script>
```

And use it similarly to jQuery at any place on the page:

```html
<script>
$script.get('src/simplifier.js', function () {
 domready(function () {
     
     // Your functionality goes below
     
     $('button').on('click', function () {
       alert('Button clicked!');
     });

     $.get('https://jsonplaceholder.typicode.com/posts/1', function (data) {
         console.log(data);
     }, function (xhr, status, error) {
         console.error('Error:', error);
     });

     $.post('https://jsonplaceholder.typicode.com/posts', {
         title: 'foo',
         body: 'bar',
         userId: 1
     }, function (data) {
         console.log(data);
     }, function (xhr, status, error) {
         console.error('Error:', error);
     }, 'application/json');
 });
});
</script>
```
