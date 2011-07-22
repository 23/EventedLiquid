`Evented Liquid` is designed to build on top of an existing JavaScript implementation of [Liquid markup](http://www.liquidmarkup.org/) to allow a) template re-rendering upon custom events and b) consolidated control of the state of the UI display.

Generally,  the library implements three feature on top of existing Liquid functionality:

* `{% event 'play', 'pause' %} ... {% endevent ‰}` to denote part of the template in need of re-rendering whenever custom events such as `play` or `pause` occur.
* A light library to define and listen to such customer events: `.fire(event, [context])` to trigger and event and `.on(event, callback)` to listen to events.
* A global `context` hash (JavaScript object) mixing in properties to keep the state of display current.


#### A Liquid template

    <h3>What on?</h3>
    {% event 'play', 'pause' %}
      {% if context.playing > 18 %}
        It's on
      {% else %}
        It's off
      {% endif %}
    {% endevent %}

#### Some JavaScript code to go with it

    var el = new EventedLiquid(template, {playing:false, buffering:false, playlist:true});
    el.on('play', function(ev,context){
        ...
      });
    el.on('pause', function(ev,context){
        ...
      });
    el.play({playing:true});