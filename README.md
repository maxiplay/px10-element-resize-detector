px10-element-resize-detector
============

Polymer element that can be included in other polymer elements or inside any other html element on the page and it 
fires a resize event when the target element size changes.

The original idea explained [here](http://www.backalleycoder.com/2013/03/18/cross-browser-event-based-element-resize-detection/)

The target element position needs to be relative.

## Using px10-element-resize-detector on a page

```html

    <ul id="list">
        <li>I'm an unordered list</li>
        <li>I was last resized:</li>
        <li id="resize_time">No resizing detected yet!</li>
        <px10-element-resize-detector></px10-element-resize-detector>
    </ul>

    <script>
        addEventListener('polymer-ready', function(event) {
    
            var listSizeDetector = document.querySelector("#list px10-element-resize-detector");
            listSizeDetector.addEventListener("resize",function(event){
                // the list element size changed            
            });
    
        });
    </script>

```

## Using px10-element-resize-detector in other polymer elements

The following is an example of a polymer-element that defines an attribute called 
monitor and enables and disables the resize monitoring with this attribute by creating a 
px10-element-resize-detector element.

```html
    <dom-module id="resize-test1">

        <style>
			:host {
				display: block;
			}
        </style>

        <template>

            <div id="message">
                Did not receive any resize messages.
            </div>
            <template if="{{monitor}}">
                <px10-element-resize-detector target="{{}}" on-resize="{{resize}}"></px10-element-resize-detector>
            </template>
            <content></content>
        </template>
        <script>
            Polymer({

                is : "resize-test1",

                properties : {

                    monitor : {
                        type : Boolean,
                        value : false
                    }
                },

                resize : function(event) {
                    this.$.message.innerHTML = "I was resized " + Date.now() / 1000 + ' seconds from the epoch';
                },
                monitorChanged : function(oldValue, newValue) {
                    if (!newValue) {
                        this.removeAttribute("monitor");
                    } else {
                        this.setAttribute("monitor", '');
                    }
                }
            });
        </script>
    </dom-module>

```
##Documentation 
[here](http://px10.github.io/px10-element-resize-detector/components/px10-element-resize-detector/)

##Demos
[Used inside other polymer element](http://px10.github.io/px10-element-resize-detector/components/px10-element-resize-detector/demos/in_other_elements.html)

[Used inside in a node in dom](http://px10.github.io/px10-element-resize-detector/components/px10-element-resize-detector/demo.html)

##Install 
Not on bower yet. 

## License
[MIT](LICENSE)
