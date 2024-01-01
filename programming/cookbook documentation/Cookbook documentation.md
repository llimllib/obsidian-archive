I believe that the humble cookbook is an underused form of documentation for programming languages and frameworks.

## bl.ocks.org

My favorite cookbook of all time is the, sadly defunct, bl.ocks.org. It looked something like this:

![[Pasted image 20231231153557.png]]

To use it, you would create a github gist [like this one](https://gist.github.com/mbostock/5249328), which would have a brief text and some [[d3.js]] code to create an HTML element and event listeners, allowing it to create an interactive diagram.

The beauty of blocks was that it was:

- simple to create
- easy to copy somebody's example
- let you search for simple examples of how to use a particular d3 api
- inspiring

I believe that blocks was responsible for a great deal of the popularity of d3; I know that it is certainly how I picked it up.

## observable

The success and limitations of bl.ocks.org are almost certainly what led Bostock et al to create [[observable]], which I sometimes enjoy using. In creating a much nicer editing environment for javascript code, however, they have damaged the utility of the site for bringing examples to life on the web. 

Code written inside of observable depends on the observable runtime, and on many useful utilities otherwise baked into the site. This is undeniably convenient when writing notebooks, but makes it an intimidating prospect to bring them out from observable into a normal website.

As such, I've used observable when I want something done and showable quickly, but I don't use it when I want to end up with a webpage.

This also makes it more painful as a learning resource; when I view somebody's observable notebook that demonstrates a technique I'd like to copy and modify, it can be quite challenging to track down all its dependencies and figure out how to include them in a web page I'm building.

In contrast, on bl.ocks.org, the site's incredible simplicity meant that it was very easy to bring an example into my own code.

I don't mean to throw stones here - the point of observable is not to help me write code - I just want to clarify that in choosing a different point on the design space of cookbooks, they've increased the utility of the website in one way and decreased its utility as a cookbook for documentation.

## others

There are lots more examples, with which I have a lot less experience.

A cookbook example that I love, but wish I understood better, is the wonderful [shadertoy](https://www.shadertoy.com/view/XsXXDB), which I think has similarly helped a great deal of people learn to program shaders.

Another example is [codepen](https://codepen.io/), which lets you post snippets of HTML/javascript/CSS that work together to demonstrate techniques for building web pages. Codepen has spawned many very similar services.

