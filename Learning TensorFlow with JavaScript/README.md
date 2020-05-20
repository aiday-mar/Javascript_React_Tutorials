# Learning TensorFlow with JavaScript

In this README file I have taken notes while studying the course title 'learning tensorflow with javascript' which discusses how it is possible to implement deep learning algorithms on the web.

TensorFlow.js is an open source WebGL library for machine learning. It allows to train neural networks. Tensors are the central unit of numerical values, they shape our data into one or many arrays. Tensors are immutable, the values we assign to a tensor can't be changed. Variables on the other hand are mutable. Operations or ops are functions that allow to manipulate data stored in tensors or variables. An example is :

```
const d = tf.tensor2d([[1.0, 2.0], [3.0, 4.0]]);
const d_squared = d.square();
d_squared.print();
```

Models allow you to use operations to create an output. We can set up the page for the use of TensorFlow as follows :

```
<html lang="end">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <script src="https://cdn.jsdelivr.net/npm/@tensorflow/tfjs@0.12.0"></script>
  <title>Tensorflow demo</title>
</head>
<body>
  <script src="index.js"></script>
</body>
</html>
```

You can also create tensors as follows :

```
const shape = [4,2];
const data = tf.tensor([4,6,5,9,13,25,1,57], shape);
data.print();
```
