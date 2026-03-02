``` python
import pandas as pd
import numpy as np

np.random.seed(0)
df2 = pd.DataFrame(np.random.randn(10,4), columns=['A','B','C','D'])

def style_negative(v, props=''):
    return props if v < 0 else None
s2 = df2.style.map(style_negative, props='color:red;')\
              .map(lambda v: 'opacity: 20%;' if (v < 0.3) and (v > -0.3) else None)

def highlight_max(s, props=''):
    return np.where(s == np.nanmax(s.values), props, '')

# darkblue, pink
s2.apply(highlight_max, props='color:white;background-color:#00008b', axis=0)\
.apply(highlight_max, props='color:white;background-color: #ffc0cb;', axis=1)\
.apply(highlight_max, props='color:white;background-color:purple', axis=None)
```

|     | A         | B         | C         | D         |
|-----|-----------|-----------|-----------|-----------|
| 0   | 1.764052  | 0.400157  | 0.978738  | 2.240893  |
| 1   | 1.867558  | -0.977278 | 0.950088  | -0.151357 |
| 2   | -0.103219 | 0.410599  | 0.144044  | 1.454274  |
| 3   | 0.761038  | 0.121675  | 0.443863  | 0.333674  |
| 4   | 1.494079  | -0.205158 | 0.313068  | -0.854096 |
| 5   | -2.552990 | 0.653619  | 0.864436  | -0.742165 |
| 6   | 2.269755  | -1.454366 | 0.045759  | -0.187184 |
| 7   | 1.532779  | 1.469359  | 0.154947  | 0.378163  |
| 8   | -0.887786 | -1.980796 | -0.347912 | 0.156349  |
| 9   | 1.230291  | 1.202380  | -0.387327 | -0.302303 |
