# **XML to ESC/POS**

### Translation/Tradução

[🇧🇷](/README-pt_br.md)
[🇺🇸](/README.md)

---

Biblioteca JavaScript codificação para o protocolo ESC/POS da impressora térmica e fornece uma interface XML para preparar modelos para impressão.

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

## Testado manualmente nos seguintes ambientes ou plataformas

- [ ] React Native (Android)
- [ ] React Native (iOS)
- [ ] React Native Web
- [ ] Server side (NodeJs)
- [ ] Desktop applications (nwjs & electron)
- [ ] Other node environment (terminal)

# **Instalação**

```bash
yarn add xml-to-escpos
```

Ou

```bash
npm install xml-to-escpos --save
```

## **Exemplos**

### De XML simples

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

### De XML + Mustache Js

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

### Com um modelo XML + imagem png (base64)

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
- [ ] Improve image rendering

## Problemas comuns

Se houver algum atraso ao imprimir com esta biblioteca, isso se deve principalmente a manipulações de imagem (tente sem imagem 😬 )

## Links/recursos úteis

- [Manual de Comandos ESC/POS](notion://www.notion.so/resources/ESCPOS_Command_Manual.pdf)
- Uma [postagem no blog](https://www.visuality.pl/posts/thermal-printer-protocols-for-image-and-text#:~:text=How%20can%20we%20print%20an,command%20language%20of%20thermal%20printers) explicando sobre a impressão de imagens com ESC/POS
- Biblioteca semelhante para serverside - [node-escpos](https://github.com/song940/node-escpos).

- Limitações no framework react-native
  - [FileReader.readAsArrayBuffer](https://github.com/facebook/react-native/issues/21209) não foi implementado.
  - A maioria das bibliotecas populares de manipulação de imagem não tem suporte para react-native. por exemplo: [jimp](https://www.npmjs.com/package/jimp), [jpeg-js](https://www.npmjs.com/package/jpeg-js) e [sharp](https://www.npmjs.com/package/sharp). Podemos usar essas bibliotecas com alguma biblioteca de nó nativo implementada em react native (algum tipo de polyfill).
  - Use this [node-libs-react-native](https://www.npmjs.com/package/node-libs-react-native) if we need to use this library in react native (adds some mock or js implementation for fs, stream etc)
  - Use [node-libs-react-native](https://www.npmjs.com/package/node-libs-react-native) se precisar usar esta biblioteca em react-native (adiciona alguma implementação simulada ou js para fs, stream etc.)
  ***
  Contribuições de qualquer tipo são bem-vindas! ❤️
