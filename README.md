# **XML to ESC/POS**

### Translation/Tradução

[🇧🇷](README-pt_br.md)
[🇺🇸](README.md)

---

Cross platform JavaScript library that implements the thermal printer ESC / POS protocol and provides an XML interface for preparing templates for printing.

## **Features**

- [x] Text
- [x] Text line
- [x] Feed line
- [x] Bold text
- [x] Underline text
- [x] Font size
- [x] Small mode
- [x] White mode
- [x] Align
- [x] QRcode
- [x] Paper cut node
- [x] Image (base64) (png only)
- [x] XML with mustache

## **Tested manually on following environments or platforms**

- [x] React Native (Android)
- [x] React Native (iOS)
- [x] React Native Web
- [x] Server side (NodeJs)
- [x] Desktop applications (nwjs & electron)
- [x] Other node environment (terminal)

# **Installation**

```bash
yarn add xml-to-escpos
```

Or

```bash
npm install xml-to-escpos --save
```

## **Examples**

### **From plain XML**

```tsx
import { EscPos } from 'escpos-xml';

const xml = `
  <?xml version="1.0" encoding="UTF-8"?>
  <document>
    <text-line>hello world</text-line>
  </document>
`;

const buffer = EscPos.getBufferFromXML(xml);
// send this buffer to a stream (eg.: bluetooth, wifi, usb, etc.)
```

### **From XML + Handlebars**

```tsx
import { EscPos } from 'xml-to-escpos';

const xml = `
  <?xml version="1.0" encoding="UTF-8"?>
  <document>
    <text-line>{{foo}}</text-line>
  </document>
`;

const input = {
  foo: 'hello world',
};

const buffer = EscPos.getBufferFromTemplate(template, input);
// send this buffer to a stream (eg.: bluetooth, wifi, usb, etc.)
```

### **With an XML template + png image (base64)**

```tsx
const template = `<?xml version="1.0" encoding="UTF-8"?>
  <document>
    <align mode="center">
      <bold>
        <text-line size="1:0">{{title}}</text-line>
      </bold>
        
      <image density="d24">
        {{base64PngImage}}
      </image>
    </align>    
  </document>`;

const input = {
  title: 'PNG - base64',
  base64PngImage: `data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAADIAAAAyCAIAAACRXR/mAAAAdklEQVR4nOzQMQ2AUBAEUQInhOCDDq8EAVigQgUaEPA1TLLFFTMCNi9by35Moa5vTU3NqaFsskiySLJIskiySLJIskiySLJIskiySE1Zdf5baut579RU07dkkWSRZJFkkWSRZJFkkWSRZJFkkWSRmrJGAAAA///HQgaco1VmUwAAAABJRU5ErkJggg==`,
};

const buffer = EscPos.getBufferFromTemplate(template, input);
// send this buffer to a stream (eg.: bluetooth, wifi, usb, etc.)
```

---

## **TODO**

- [ ] Font styles (font family)
- [ ] Barcode
- [ ] Image bitmap conversion improvements
- [ ] jpeg support
- [ ] Add example apps to repo
- [ ] Removed uglify for some reason, need to bring it back
- [ ] Improve image rendering

## **Common issues**

If there is any delay you observe while printing with this library it is mostly due to image manipulations (try without image 😬 )

## **Useful links / resources**

- [ESC / POS Commands manual](notion://www.notion.so/resources/ESCPOS_Command_Manual.pdf)
- A [blog post](https://www.visuality.pl/posts/thermal-printer-protocols-for-image-and-text#:~:text=How%20can%20we%20print%20an,command%20language%20of%20thermal%20printers) explaiing about printing images with ESCPOS
- Similar library for serverside - [node-escpos](https://github.com/song940/node-escpos).

- _Limitations on the react-native framework_
  - [FileReader.readAsArrayBuffer](https://github.com/facebook/react-native/issues/21209) was not implemented.
  - Most of popular image manupulation libraries does not have support for react-native. eg : [jimp](https://www.npmjs.com/package/jimp), Most of popular image manupulation libraries does not have support for react-native. eg : [jimp](https://www.npmjs.com/package/jimp), [jpeg-js](https://www.npmjs.com/package/jpeg-js) and [sharp](https://www.npmjs.com/package/sharp). We can use these libraries with some native node lib implemented in react native (some sort of polyfill).
  - Use this [node-libs-react-native](https://www.npmjs.com/package/node-libs-react-native) if we need to use this library in react native (adds some mock or js implementation for fs, stream etc)
  ***
  Contributions of any kind welcome! :heart:
