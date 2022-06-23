# TFJS-CustomImageClassification
Building Mobilenet Based Custom Image Classification Model on the Browser with Tensorflow.js and Angular


# eisbilen/TFJS-CustomImageClassification with missing angular files

eisbilen/TFJS-CustomImageClassification is missing a package.json which makes it a bit difficult to run locally and learn from.

I have added a basic package.json to get this project running in angular. I'm not sure what package versions were used originally for this project but these are the ones I found that allow the project to compile and run. I know that these are not the exact packages originally used because I had to modify two lines in app.component.ts


Note: A lot of the libraries are out of date.


When you run it you will get this error
```
WARNING in ./node_modules/@tensorflow/tfjs-core/dist/tf-core.esm.js
Module not found: Error: Can't resolve 'crypto' in 'C:\Users\kgathuru\Htdocs\malaria\node_modules\@tensorflow\tfjs-core\dist'
```

To fix this manually edit `node_modules/@angular-devkit/build-angular/src/angular-cli-files/models/webpack-configs/browser.js' and changed the following line:

```javascript
// old:
node: false,
// new:
node: { crypto: true, stream: true },
```

Source of fix
https://github.com/tensorflow/tfjs/issues/494#issuecomment-403575354

# Tensorflow.js
There are several ways of fine tuning a deep learning model but doing this on the web browser with WebGL acceleration is something that we experienced not such a long time ago, with the introduction of Tensorflow.js. In this example, I will use Tensorflow.js together with Angular to build a Web App which trains a convolutional neural network to detect malaria infected cells with the help of Mobilenet and Kaggle dataset containing 27.558 infected and uninfected cell images.

# Mobilenet as Base Model
As I mentioned above, I will use mobilenet as a base model for our custom image classifier. The pre-trained mobilenet model, which is tensorflow.js compatible, is relatively small, 20MB, and can be directly downloaded from the Google api storage folder. 

There will be 2 classes, which are uninfected and parasitized cells, we would like to classify with our custom model whereas the original mobilenet model is trained to classify 1000 different objects.
I will use all mobilenet layers other than last 5 layers, and add a dense layer with 2 units and softmax activation on top of this truncated model to make the modified model suitable for our classification task.
We will not train all layers, as this will require a lot of time and computational power. It is also not necessary for our case as we use a pre-trained model which has a lot of representations learned already. Instead, we will freeze majority of the layers and keep only last 2 ones trainable.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).

