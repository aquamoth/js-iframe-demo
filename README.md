Javascript can't access functions in an IFrame directly. IFrames can access functions in their parent though.

[Test it by following this link][1]. Due to browser security restrictions the code must be loaded from the same webserver and doesn't work if run directly from the filesystem.

I've intentionally included the child iframe twice to illustrate that any number of children can be registered with this technique. I leave it as an excercise to the reader to add a third iframe... :)

## index.html

The javascript has a function `registerChild()` that it never calls itself, but can be called from child pages to register their endpoints.

When the button is clicked, all registered callbacks are called with the string "blue". It is then up to the childs endpoint to do something good with that. In this case changing its own background color.

## child.html

The javascript of the child checks if there is a parent (it is running inside an iframe) and that the parent provides a function called `registerChild()`. It then calls that function with a reference to its own function `setBackground()`.

When the parent later calls the callback with the string "blue", it turns around and sets its own bodys background color to that value. 


  [1]: https://rawgit.com/aquamoth/JS-iframe-demo/master/index.html
