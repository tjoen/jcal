
# jCal

jCal is a simple jQuery plugin for date selection. It doesn't rely on any other plugins (like the jQuery UI) so it is relatively lightweight compared to other alternatives.

The interface provides buttons for selecting the current day, the month (without specifying a day), or clearing the input field altogether.

Although it does not require [Twitter Bootstrap](http://twitter.github.io/bootstrap/), jCal works nicely with it, and uses the Bootstrap button classes on the UI controls.

## Using jCal

### Markup and JavaScript

jCal assumes that there are two input field on the page - one which shows a formatted date (e.g. '1 Jan 2013') and another hidden field which contains the actual value that will be sent to the database, in mysql format, e.g. '2013-01-01'.

The 'value field' is the one with a 'name' attribute - the formatted field does not need one. The formatted (visible) field is the one on which we attach the plugin. The html markup should look something like this:
```
<label for="f_mydate">
    Pick a date
</label>
<input type="hidden" id="f_mydate" name="mydate" value="2013-01-01" />
<input type="text" class="jcal" data-value-field="f_mydate" data-jcal-render-to="#jcal" />
<div id="jcal"></div>
```

We're linking the 'formatted date' field to the 'value field' by means of the 'data-value-field' attribute. We're also specifying a jQuery selector of a div to which we want to render the calendar picker html.

We can then call the plugin (in this example on any element with a class 'jcal'):
```
$('input.jcal').each(function() {
    var obj = $(this);
    var value_field_id = obj.attr('data-value-field');
    obj.jcal({
        'value_field': value_field_id
    });
});
```

### Options

- *value_field* - The ID of the field in which the hidden value will be stored. This is intended to be the value that will be posted back to the server.
- *render_to* - The jQuery selector used to specify the fic into which the calendar interface will be rendered. Alternatively, this option can be specified using a data attribute, as in the example above.
- *position* - Where to position the calendar when it appears. The options are:
-- *centered* - The calendar will be centered in the middle of the browser window. This is the default behaviour.
-- *positioned* - The calendar will be positioned below the input field. This behaves more like the [jQuery UI Datepicker](http://jqueryui.com/datepicker/) plugin.

### $.jcal.cal()

The `$.jcal` object provides a function for generating calendars and blocks of dates, `$.jcal.cal()`. Given a year, month and optionally the currently selected day, this function returns a multidimensional array, where each row itself contains exactly seven items representing the days of the week, starting at Monday. Each day is represented as an array comprising `[year, month, day, visible, selected]`.

For example, for the selected date 3rd May 2013, our array would look like this:
```
[
    [                        // first row of results
        [2013, 4, 29, 0, 0], // 29th Apr, not visible, not selected
        [2013, 4, 30, 0, 0],
        [2013, 5, 1, 1, 0],  // 1st May, visible, not selected
        [2013, 5, 2, 1, 0],
        [2013, 5, 3, 1, 1],  // 3rd May, visible, selected
        [2013, 5, 4, 1, 0],
        [2013, 5, 5, 1, 0]
    ],
    [                        // second row of results
        [2013, 5, 6, 1, 0],
        [2013, 5, 7, 1, 0],
        [2013, 5, 8, 1, 0],
        // etc...
    ],
    // down to...
    [                        // last (5th) row of results
        [2013, 5, 27, 1, 0],
        [2013, 5, 28, 1, 0],
        [2013, 5, 29, 1, 0],
        [2013, 5, 30, 1, 0],
        [2013, 5, 31, 1, 0],
        [2013, 5, 1, 0, 0],  // 1st June, not visible, not selected
        [2013, 5, 2, 0, 0]
    ]
 ]
```

### A note about formatting

This plugin was written for Artlogic Media Ltd and handles date fields in our house style (both in terms of the hidden value and the display value). It may not be your house style. If you would like to use this plugin, help yourself and adapt it as you want.

That said, the hidden value matches the standard MySQL format, so it should be useful generally. Providing multi-language support is a simple matter of modifying the `$.jcal.short_month_names` and `$.jcal.long_month_names` properties.

## License

jCal is dual-licensed under the [MIT license](https://github.com/artlogicmedia/jcal/blob/master/MIT-LICENSE.md) and the [GNU Public License version 2](https://github.com/artlogicmedia/jcal/blob/master/GPLv2-LICENSE.md).

## Authorship information

jCal is written and maintained by [Artlogic Media](http://artlogic.net/).
