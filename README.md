# imagemin-avif-webpack-plugin

Webpack plugin to convert images to avif while also keeping the original files.

It uses [imagemin](https://www.npmjs.com/package/imagemin) and [imagemin-avif](https://www.npmjs.com/package/imagemin-avif) under the hood.

## Usage

In order to use this plugin, add it to your **webpack config**.



```js
module.exports = {
    plugins: [new ImageminAvifWebpackPlugin()]
};
```

## API

### ```new ImageminAvifWebpackPlugin( [options] );```

### options

Type: `Object`<br/>

Default:

```js
{
  config: [{
    test: /\.(jpe?g|png)/,
    options: {
      quality:  50,
      lossless: false,
      speed: 5,
      chromaSubsampling: '4:2:0'
    }
  }],
  overrideExtension: true,
  detailedLogs: false,
  silent: false,
  strict: true
}
```

#### config
Type ```Array<Object: {test, options} >```


The main config of the plugin which controls how different file types are converted. Each item in the array is an object with 2 properties:

* **test** - a RegExp selecting just certain images
* **options** -the converting options for the images that pass the above RegExp

⚠ The **options** object is actually the same one from the [imagemin-avif](https://www.npmjs.com/package/imagemin-avif) plugin so check their documentation for the available settings.

#### overrideExtension

Type: `boolean`<br>
Default: `true`

By default the plugin will override the original file extension, so you will get: `image.png` -> `image.avif`

In case you want to concat '.avif' at the end of the file name, set the config value to false. Ex: `image.png` -> `image.png.avif`.

#### detailedLogs

Type: `boolean`<br>
Default: `false`

By default the plugin will print to the console

1. the total number of megabytes saved by the avif images compared to the original ones
2. the number of images that failed being converted

This options tells the plugin to also log the size difference per converted image and the names of the images that failed conversion.

#### silent

Type: `boolean`<br>
Default: `false`

In case you don't want anything printed to the console set this option to false. This will override the `detailedLogs` option. <br>

#### strict

Type: `boolean`<br>
Default: `true`

By default the webpack build will fail if any of the images that match your RegExps fail the conversion.

This option tells the plugin to not crash the build and keep going :)
