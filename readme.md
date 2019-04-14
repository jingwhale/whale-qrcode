# whale-qrcode
![npm version](https://img.shields.io/badge/npm-1.0.0-brightgreen.svg)

Generate QR Code matrix.

## Install
```
npm install whale-qrcode
```

## Usage
```
import QRCode from 'whale-qrcode';

const qrcode = new QRCode("https://www.jingwhale.cc/");

const modules = qrcode.qrcode.modules
```

## [Demo](https://github.com/jingwhale/whale-kit/blob/master/src/generateQrcode.js)
```
function generate(inputSettings, value){
  const qrcode = new QRCode(`${value}`)
  const options = Object.assign(getDefaultSettings(), inputSettings)
  const modules = qrcode.qrcode.modules
  const width = options.width
  const height = options.height
  const length = modules.length
  const xsize = width / (length + 2 * options.padding)
  const ysize = height / (length + 2 * options.padding)

  let layers = []
  for (let y = 0; y < length; y++) {
    for (let x = 0; x < length; x++) {
      let module = modules[x][y]
      if (module) {
        let px = (x * xsize + options.padding * xsize).toString()
        let py = (y * ysize + options.padding * ysize).toString()
        layers.push({
          type: sketch.Types.Shape,
          frame: {
            x: px,
            y: py,
            width: xsize,
            height: ysize,
          },
          style: {
            fills: [
              {
                color: `${options.color}`,
                fill: `${options.background}`
              }
            ],
            borders: []
          }
        })
      }
    }
  }

  const group = new sketch.Group({
        name: `qr-${value}`,
        parent: buttonRect.parent,
          frame: {
              x: buttonRect.frame.x,
              y: buttonRect.frame.y,
              width: options.width,
              height: options.height
          },
        layers:layers
      });
    }
}
```
