# Ajax

[toc]


## What is Ajax? 

Ajax is the acronym for Asynchronous JavaScript And XML. XML is a data exchange format and UX is software developer shorthand for User Experience. Ajax is an Internet communications technique that allows a web page displayed in a user’s browser to request specific information from a server and display this new information on the same page without the need to reload the entire page. You can already imagine how this improves the user experience.

While XML is the traditional data exchange format used, the exchange can actually be any convenient format. When working with PHP code, many developers favor JSON because the internal data structure created from the transmitted data stream is easier to interface with.

To see Ajax in action, go to your WordPress administration area and add a category or tag. Pay close attention when you click the Add New button, notice the page changes but does not actually reload. Not convinced? Check your browser’s back history, if the page had reloaded, you would see two entries for the page.

Ajax does not even require a user action to work. Google Docs automatically saves your document every few minutes with Ajax without you needing to initiate a save action.

[Top ↑](https://developer.wordpress.org/plugins/javascript/ajax/#top)

## Why use Ajax? 

Obviously, it improves the user experience. Instead of presenting a boring, static page, Ajax allows you to present a dynamic, responsive, user friendly experience. Users can get immediate feedback that some action they took was right or wrong. No need to submit an entire form before finding out there is a mistake in one field. Important fields can be validated as soon as the data is entered. Or suggestions could be made as the user types.

Ajax can dramatically decrease the amount of data flowing back and forth. Only the pertinent data needs to be exchanged instead of all of the page content, which is what happens when the page reloads.

Specifically related to WordPress plugins, Ajax is by far the best way to initiate a process independent of WordPress content. If you’ve programmed PHP before, you would likely do this by simply linking to a new PHP page. The user following the link initiates the process. The problem with this is that you cannot access any WordPress functions when you link to a new external PHP page. In the past, developers accessed WordPress functions by including the core file `wp-load.php` on their new PHP page. The problem with doing that is you cannot possibly know the correct path to this file anymore. The WordPress architecture is now flexible enough that the /wp-content/ and your plugin files can be moved from its usual location to one level from the installation root. You cannot know where wp-load.php is relative to your plugin files, and you cannot know the absolute path to the installation folder either.

What you can know is where to send an Ajax request, because it is defined in a global JavaScript variable. Your PHP Ajax handler script is actually an action hook, so all WordPress functions are automatically available to it, unlike an external PHP file.

[Top ↑](https://developer.wordpress.org/plugins/javascript/ajax/#top)

## How Do I Use Ajax? 

If you are new to WordPress but have experience using Ajax in other environments, you will need to relearn a few things. The way WordPress implements Ajax is most likely different than what you are used to. If everything is new to you, no problem. You will learn the basics here. Once you’ve developed a basic Ajax exchange, it’s a cinch to expand on that base and develop that killer app with an awesome user interface!

There are two major components of any Ajax exchange in WordPress. The client side JavaScript or jQuery and the server side PHP. All Ajax exchanges follow the following sequence of events.

1. Some sort of page event initiates a JavaScript or jQuery function. That function gathers some data from the page and sends it via a HTTP request to the server.Because handling HTTP requests with JavaScript is awkward and jQuery is bundled into WordPress anyway, we are going to focus only on jQuery code from here on out. Ajax with straight JavaScript is possible, but it’s not worth doing it when jQuery is available.
2. The server receives the request and does something with the data. It may assemble related data and send it back to the client browser in the form of an HTTP response. This is not a requirement, but since keeping the user informed about what’s going on is desirable, it’s very rare not to send some kind of response.
3. The jQuery function that sent the initial Ajax request receives the server response and does something with it. It may update something on the page and/or present a message to the user by some means.

[Top ↑](https://developer.wordpress.org/plugins/javascript/ajax/#top)

## Using Ajax with jQuery 

Now we will define the “do stuff” portion from the [snippet in the article on jQuery](https://developer.wordpress.org/plugin/javascript/jquery/#selector-and-event). We will use the [$.post()](http://api.jquery.com/jQuery.post/) method, which takes 3 parameters: the URL to send the POST request to, the data to send, and a callback function to handle the server response. Before we do that though, we have a bit of advance planning to get out of the way. We do the following assignment for use later in the callback function. The purpose will be more evident in the [Callback section](https://developer.wordpress.org/plugins/javascript/ajax/#callback).

```js
var this2 = this;
```

### URL

All WordPress Ajax requests must be sent to `wp-admin/admin-ajax.php`. The correct, complete URL needs to come from PHP, jQuery cannot determine this value on its own, and you cannot hardcode the URL in your jQuery code and expect anyone else to use your plugin on their site. If the page is from the administration area, WordPress sets the correct URL in the global JavaScript variable `ajaxurl`. For a page from the public area, you will need to establish the correct URL yourself and pass it to jQuery using `wp_localize_script()`. This will be covered in more detail in the [PHP section](https://developer.wordpress.org/plugin/javascript/enqueuing/). For now just know that the URL that will work for both the front and back end is available as a property of a global object that you will define in the PHP segment. In jQuery it is referenced like so:

```js
my_ajax_obj.ajax_url
```

[Top ↑](https://developer.wordpress.org/plugins/javascript/ajax/#top)

### Data 

All data that needs to be sent to the server is included in the data array. Besides any data needed by your app, you must send an action parameter. For requests that could result in a change to the database you need to send a nonce so the server knows the request came from a legitimate source. Our example data array provided to the `.post()` method looks like this:

```js
{_ajax_nonce: my_ajax_obj.nonce, //nonce
  action: "my_tag_count",        //action
  title: this.value              //data
}
```

Each component is explained below.

[Top ↑](https://developer.wordpress.org/plugins/javascript/ajax/#top)

### Nonce 

[Nonce](https://codex.wordpress.org/WordPress_Nonces) is a portmanteau of “Number used ONCE”. It is essentially a unique hexadecimal serial number assigned to each instance of any form served. The nonce is established with PHP script and passed to jQuery the same way the URL was, as a property in a global object. In this case it is referenced as `my_ajax_obj.nonce`.

---
> **Note:**
>
> A true nonce needs to be refreshed every time it is used so the next Ajax call has a new, unused nonce to send as verification. As it happens, the WordPress nonce implementation is not a true nonce. The same nonce can be used as many times as necessary in a 24 hour period. Generating a nonce with the same seed phrase will always yield the same number for a 12 hour period after which a new number will finally be generated.
>
> If your app needs serious security, implement a true nonce system where the server sends a new, fresh nonce in response to an Ajax request for the script to use to verify the next request.
---

It’s easiest if you key this nonce value to `_ajax_nonce`. You can use a different key if it’s coordinated with the PHP code verifying the nonce, but it’s easier to just use the default value and not worry about coordination. Here is the way the declaration of this key-value pair appears:

```js
_ajax_nonce: my_ajax_obj.nonce
```

[Top ↑](https://developer.wordpress.org/plugins/javascript/ajax/#top)

### Action 

All WordPress Ajax requests must include an action argument in the data. This value is an arbitrary string that is used in part to construct an action tag you use to hook your Ajax handler code. It’s useful for this value to be a very brief description of the Ajax call’s purpose. Unsurprisingly, the key for this value is *‘action’*. In this example, we will use `"my_tag_count"` as our action value. The declaration of this key-value pair looks like this:

```js
action: "my_tag_count"
```

Any other data the server needs to do its task is also included in this array. If there are a lot of fields to transmit, there are two common formats to combine data fields into a single string for more convenient transmission, XML and JSON. Using these formats is optional, but whatever you do does need to be coordinated with the PHP script on the server side. More information on these formats is available in the following Callback section. It is more common to receive data in this format than to send it, but it can work both ways.

In our example, the server only needs one value, a single string for the selected book title, so we will use the key *‘title’*. In jQuery, the object that fired the event is always contained in the variable `this`. Accordingly, the value of the selected element is `this.value`. Our declaration of this key-value pair appears like so:

```js
title: this.value
```

[Top ↑](https://developer.wordpress.org/plugins/javascript/ajax/#top)

### Callback 

The callback handler is the function to execute when a response comes back from the server after the request is made. Once again, we usually see an anonymous function here. The function is passed one parameter, the server response. The response could be anything from a yes or no to a huge XML database. JSON formatted data is also a useful format for data. The response is not even required. If there is none, then no callback need be specified. In the interest of UX, it’s always a good idea to let the user know what happened to any request, so it is recommended to always respond and provide some indication that something happened.

In our example, we replace the current text following the radio input with the server response, which includes the number of posts tagged by the book title. Here is our anonymous callback function:

```js
function(data) {
    this2.nextSibling.remove();
    $(this2).after(data);
}
```

`data` contains the entire server response. Earlier we assigned to `this2` the object that triggered the change event (referenced as `this`) with the line `var this2 = this;`. This is because variable scope in closures only extends one level. By assigning `this2` in the event handler (the part that initially just contained *“/\* do stuff \*/”*), we are able to use it in the callback where `this` would be out of scope.

The server response can take on any form. Significant quantities of data should be encoded into a data stream for easier handling. XML and JSON are two common encoding schemes.

#### XML 

XML is the classic data exchange format for Ajax. It is after all the ‘X’ in Ajax. It continues to be a viable exchange format even though it can be difficult to work with using native PHP functions. Many PHP programmers prefer the JSON exchange format for that reason. If you do use XML, the parsing method depends on the browser being used. Use Microsoft.XMLDOM ActiveX for Internet Explorer and use DOMParser for everything else.

[Top ↑](https://developer.wordpress.org/plugins/javascript/ajax/#top)

#### JSON 

JSON is often favored for its light weight and ease of use. You can actually parse JSON using `eval()`, but don’t do that! The use of `eval()` carries significant security risks. Instead, use a dedicated parser, which is also faster. Use the global instance of the parser object `JSON`. To ensure that it is available, be sure it is enqueued with other scripts on the page. More information about enqueuing is included later in the [PHP section](https://developer.wordpress.org/plugins/javascript/ajax/#json).

[Top ↑](https://developer.wordpress.org/plugins/javascript/ajax/#top)

#### Other

As long as the data format is coordinated with the PHP handler, it can be any format you like, such as comma delimited, tab delimited, or any kind of structure that works for you.

[Top ↑](https://developer.wordpress.org/plugins/javascript/ajax/#top)

#### Client Side Summary 

Now that we’ve added our callback as the final parameter for the `$.post()` function, we’ve completed our sample jQuery Ajax script. All the pieces put together look like this:

```js
jQuery(document).ready(function($) {           //wrapper
    $(".pref").change(function() {             //event
        var this2 = this;                      //use in callback
        $.post(my_ajax_obj.ajax_url, {         //POST request
           _ajax_nonce: my_ajax_obj.nonce,     //nonce
            action: "my_tag_count",            //action
            title: this.value                  //data
        }, function(data) {                    //callback
            this2.nextSibling.remove();        //remove current title
            $(this2).after(data);              //insert server response
        });
    });
});
```

This script can either be output into a `block` on the web page or contained in its own file. This file can reside anywhere on the Internet, but most plugin developers place it in a `/js/` subfolder of the plugin’s main folder. Unless you have reason to do otherwise, you may as well follow convention. For this example we will name our file `myjquery.js`