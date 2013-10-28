# TinyMCE Validatable Plugin

This is a plugin for [TinyMCE](http://tinymce.com/) 4.x, dealing with the problem that targeted elements that have
validation rules applied, may prevent a form from being submitted.


## What's the deal?

TinyMCE injects the editor contents _after_ the browser based form validation applies, so the validation will be
applied on whatever the targeted element initially contained, thus validation will always fail in case the initial
elements contents do not match the validation rules.

Another problem is that the validation bubbles are not being displayed correctly, or even not all in case the field is
hidden (as in `display: none`). In Firefox for example the bubble is displayed "_behind_" the browser, in the bottom
left corner of the screen, in IE nothing is being shown at all, and Chromium based browsers throw an error.


## How does this plugin fix the problem?

This plugin can "fix" the problem in two ways.

1. By disabling the targeted element until the form is submitted. This causes the field to be simply skipped in the
validation stage, thus the form can submit properly even when the targeted elements contents doesn't match the
validation rules.

2. By moving the targeted element into the container of the linked editor, styling it so that it snaps to the
containers dimensions and lays underneath the editor, invisible, but not hidden (as in `display: none`), and injecting
the editor contents into the targeted element as you write. That way the browser based validation is correctly applied
to the editor contents, and possible validation bubbles appear.


## How to use?

Copy the `validatable` folder located in `js/tinymce/plugins/` into the `plugins` folder of your local TinyMCE
installation, and include the name of the plugin in the `plugins` option:

```js
tinymce.init({
	plugins: 'validatable'
});
```

In case you're fine with the default behavior, then that's all, you're ready to roll. If you want to configure the
behavior, here are the options:

* `validatable_exclude_from_validation` Possible values: `true`/`false`. Defaults to `false`. Defines whether to
exclude the targeted element from validation.
* `validatable_hide_completely` Possible values: `true`/`false`. Defaults to `false`. Defines whether the targeted
element is being hidden completely. Hidden completely means not even possible borders/outlines are being displayed
which may normally appear on validation errors.

```js
tinymce.init({
	plugins: 'validatable',
	validatable_exclude_from_validation: false,
	validatable_hide_completely: false
});
```


## Compatibility

Tested successfully with IE10+, Firefox 24+, Chrome 30+, Opera 12+.

Please use the [issue tracker](https://github.com/ndm2/tinymce-validatable/issues) to report successfully tested
OS/browser/version combinations that aren't listed here.


## Issues

Please use the [issue tracker](https://github.com/ndm2/tinymce-validatable/issues) to report problems.


## License

Licensed under [The MIT License](http://www.opensource.org/licenses/mit-license.php).