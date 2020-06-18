# vuetify

### Display

 https://vuetifyjs.com/ko/styles/display

- 12 point grid system

| code | types                  | range       |
| ---- | ---------------------- | ----------- |
| xs   | small to large handset | <600px      |
| sm   | tablet                 | 600 - 960   |
| md   | laptop                 | 960 - 1264  |
| lg   | desktop                | 1264 - 1904 |
| xl   | 4k and ultra-wides     | >1904px     |

-  visibility

  

### text

https://vuetifyjs.com/ko/styles/text



### text resizing

```vue
<script src="https://unpkg.com/vue"></script>
<script src="https://unpkg.com/vue-resize-text"></script>

<template>
  <div>
    <div v-resize-text="{ratio:1.3, minFontSize: '30px', maxFontSize: '100px', delay: 200}">Hello Vue</div>
  </div>
</template>

<script>
  import ResizeText from 'vue-resize-text'
  export default {
    directives: {
        ResizeText
     }
  };
</script>
```

 

### image resizing

```cmd
npm install --save vue-image-upload-resize
```

```vue

```

