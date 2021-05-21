---
description: Visualising your keras model
---

# Model Visualization

## Using built-in function \(keras.utils.plot_model\)

Source: [https://keras.io/visualization/](https://keras.io/visualization/)

```text
from keras.utils import plot_model
plot_model(model, to_file='model.png')
```

{% hint style="info" %}
You need to install `graphviz`\(using your os package manager; `brew` in macOS, for example\) and `pydot` \(using pip/conda\)
{% endhint %}

The parameter `show_shapes` is set to `False` by default, but it can be set to `True` to show \(layer\) output shapes.

### Example

```text
from keras.models import Sequential
from keras.layers import Dense
from keras.utils import plot_model

model = Sequential()
model.add(Dense(20, input_dim=4, activation='relu'))
model.add(Dense(5, activation='softmask'))

plot_model(model,
           to_file='model.png',
           show_shapes=True)
```
