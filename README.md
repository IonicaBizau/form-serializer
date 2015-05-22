Form Serializer
===============

Mono module that serialize an form object and emits it.

# Documentation

## Module configuration

The event module name is configurable (the default value is `serializedForm`).

```js
"miidName": {
    "module": "github/jillix/form-serializer/MODULE_VERSION"
  , "roles": [MONO_ROLES]
  , "config": {
        "html": "/path/to/html/file.html"
        "eventName": "editList"
      , "validators": {
            "fillForm": "namespace.form_serializer.validateData"
        }
      , "onFill": {
            "binds": [BIND_OBJECTS]
        }
      , "listen": {EVENT_OBJECTS}
    }
  , "operations": {
        "loadForm": {
            "roles": [1]
          , "params": [{
                "forms": {
                    "formId1": "/public/html/forms/myForm.html"
                }
            }]
        }
    }
}
```

## Public functions

<table>
    <thead>
        <tr>
            <th>Function Name</th>
            <th>Parameters</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>fillForm (data)</code></td>
            <td><code>data</code>: an object, as first function parameter. Use <code>config.onFille.binds</code> to fill the form.</td>
            <td>Fill the form using Bind Mono Module. The binds are configurable from <code>config.onFill.binds</code>. See for more information <a href="http://github.com/jillix/bind">Bind</a> module.</td>
        </tr>
        <tr>
            <td><code>showError (err) </code></td>
            <td><code>err</code>: a string, as first function parameter. It's the error message that appears in the alert</td>
            <td>Shows an error</td>
        </tr>
        <tr>
            <td><code>clearErrors () </code></td>
            <td>No parameters</td>
            <td>Clear all errors</td>
        </tr>
        <tr>
            <td><code>loadForm</code></td>
            <td><code>options</code>: object (formId is required), <code>callback</code>: callback function (optional)</code></td>
            <td>Loads dinamically a form as pointed in [#2](https://github.com/jillix/form-serializer/pull/2)</td>
        </tr>
    </tbody>
</table>

## How to use

Place in the module HTML `data-field` and `data-value` atributes.

<table>
    <thead>
        <tr>
            <th>Value</th>
            <th>Description</th>
            <th>Default value</th>
            <th>Required</th>
            <th>Example</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><code>data-field</code></td>
            <td>Name of the <code>key</code> from object.</td>
            <td>No default value.</td>
            <td>Yes</td>
            <td><code>data-field="author"</code></td>
        </tr>
        <tr>
            <td><code>data-value</code></td>
            <td>It's the name of the function how the value will be taken.</td>
            <td><code>val</code></td>
            <td>No (will take the default value)</td>
            <td><code>data-value="text"</code></td>
        </tr>
        <tr>
            <td><code>data-params</code></td>
            <td>Params of jQuery function set as <code>data-value</code>.</td>
            <td>No default value</td>
            <td>Not required.</td>
            <td><code>data-params="checked"</code></td>
        </tr>
        <tr>
            <td><code>data-convert-to</code></td>
            <td>
                The data type. Can be one of the following values:
                <ul>
                    <li><code>string</code></li>
                    <li><code>number</code></li>
                    <li><code>boolean</code></li>
                </ul>
            </td>
            <td>No default value</td>
            <td>Not required.</td>
            <td><code>data-convert-to="boolean"</code></td>
        </tr>
        <tr>
            <td><code>data-delete-if</code></td>
            <td>If provided, the field will be deleted if it's equal with the attribute value.</td>
            <td>No default value</td>
            <td>Not required.</td>
            <td><code>data-delete-if=""</code></td>
        </tr>
    </tbody>
</table>

# Example

```HTML
<form>
    <input type="text" data-field="author" value="Ionică Bizău" />
    <input type="checkbox" data-field="visible" data-value="prop" data-params="checked" value="Ionică Bizău" />
</form>
```

When the form above will be submitted the following JSON object will be generated and emited:

```JSON
{
    "author": "IonicaBizau"
  , "visible": false
}
```

# Changelog

### dev
 - features and fixes go here

### v0.3.2
 - Updated to Bind `v0.3.3`, Utils `v0.1.8` and Events `v0.3.1`

### v0.3.1
 - Changed owner to jillix
 - Updated to Bind `v0.3.1`

### v0.3.0
 - Upgraded deps

### v0.2.5
 - Updated to Events v0.1.11 and Utils v0.1.2

### v0.2.4
 - Removed close button from alert

### v0.2.3
 - Updated to Events v0.1.10

### v0.2.2
 - Bind v0.2.2 and Utils v0.1.1

### v0.2.1
 - added `data-delete-if` attribute feature
 - deleted deprecated `findValue` and `findFunction` because util library is already imported and contains these methods

### v0.2.0
 - Added Utils in dependencies
 - Added LICENSE
 - Upgraded Events module
 - Added Converters (see `data-convert-to`)
 - Added dot notation feature
 - Override `config.onFill.binds` if a second argument is provided in `fillForm` function

### v0.1.3
 - Fixed `loadForm` method callback callback

### v0.1.2
 - Added `loadForm` method. See [#2](https://github.com/jillix/form-serializer/pull/2) for details.

### v0.1.1
 - Updated to Events v0.1.8 and Bind v0.2.1

### v0.1.0
 - initial release
