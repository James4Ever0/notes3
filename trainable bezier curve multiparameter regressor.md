---
title: trainable bezier curve multiparameter regressor
created: '2022-09-18T13:57:31.469Z'
modified: '2022-09-18T16:05:23.092Z'
---

# trainable bezier curve multiparameter regressor

[bezier](https://pypi.org/project/bezier/)

first, we need a bezier curve connects (0,0) and (1,1)

```python
def bezierCurve(input_value:float, start=(0,0), end=(1,1), skew=0):
  # skew: (-0.5,0.5) otherwise this shit will look ugly.
  x_start, y_start = start
  x_end, y_end = end
  assert x_start <= input_value
  assert x_end >= input_value
  x_diff = x_end - x_start
  y_diff = y_end - y_start
  nodes1 = np.asfortranarray(
      [
          [x_start, x_diff * (0.5 + skew), x_end],
          [y_start, y_diff * (0.5 - skew), y_end],
      ]
  )
  curve1 = bezier.Curve(nodes1, degree=2)
  curve_params = {'x_start':x_start, 'x_diff':x_diff}
  return curve1, curve_params

def evaluateBezierCurve(input_value,curve, curve_params)
  s = (input_value - x_start)/x_diff
  points = curve.evaluate(s)
  # we only get the single point.
  point = points.T[0]
  x,y = point
  result = y
  return result

```

then, we define our very recursive or flexible regressor:

```python
def multiParameterExponentialNetwork(*args, input_bias=0.1, curve_function=bezierCurve, function_kwargs = {'start':(0,0),'end':(1,1)'skew':0}):
  curve = 
  value = function(input_bias,**function_kwargs)
  for index, input_value in enumerate(args):
    apply_list = [input_value]*(index+1)
    for apply_item in apply_list:
      value += (1-value)*function(apply_item, **function_kwargs)
  return value

```
