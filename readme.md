# Vue clip component

Clip/mask component for [Vue](https://vuejs.org/) framework. Component acts as a tool for clipping other (parent) component.
It uses [hammerjs](https://hammerjs.github.io/) and supports desktop (and partialy mobile). Tested on chrome, firefox, edge and chrome mobile.

## Install

```bash
npm install @zipavlin/clip-tool
```

```html
<script src="//unpkg.com/@zipavlin/vue-clip-tool/dist/ClipTool.umd.min.js">
```

## Use

Include component in your Vue app and bind v-model or :value + @input attributes.  

This component is supposed to be used as a tool and will only return array of points that can be used to create css clip-path property for external source component.  
  
The easiest way to use this tool is to bind component's output object to vue style object.

```html
<template>
    <div id="app">
        <div :style="style">
            <clip-tool :width="width" :height="height" v-model="cliptool"></mrr-tool>
        </div>
    </div>
</template>

<script>
    import ClipTool from '@zipavlin/vue-clip-tool'

    export default {
        name: "App",
        components: { ClipTool },
        data() {
            return {
                width: 400,
                height: 400,
                cliptool: []
            }
        },
        computed: {
            style() {
                return {
                    background-color: 'deeppink',
                    width: this.width + 'px',
                    height: this.height + 'px',
                    clip-path: `polygon(${this.cliptool.map(x => x.join('%,')).join('% ')});`
                };
            }
        }
    }
</script>
```

## Props

### Width
Width of a component. You probably want to bind this with parent's width.

### Height
Width of a component. You probably want to bind this with parent's width.

### Value
Type __Array__ of __Arrays__ of __Int__
Example __[[10, 10], [20, 20], [30, 10]]__
Component supports binding with __v-model__ or __:value__ + __@input__ combination.

### Options
Type __Object__

| option            | default       | description                                           |
| ----------------- |:-------------:| -----------------------------------------------------:|
| stroke            | '#00C2FF'     | stroke color                                          |
| strokeWidth       | 2             | stroke width and point radius (in px)                 |
| strokeArea        | 20            | stroke and point's pointer event area                 |
| pathTitle         | null          | path title attribute                                  |
| pointTitle        | null          | point title attribute                                 |
| confirmText       | null          | confirm popup text when removing point                |
| minPointDistance  | 10            | minimum distance between points when adding a new one |

## Events

### input

Triggered on every edit (add, remove, move) event, except _while_ moving points.

### change

Same as __input__ event.

### contextmenu

Triggered on right click (mouse) or long touch (touch) on _wrap_ element with event object passed as only parameter.