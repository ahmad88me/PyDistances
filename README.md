# PyDistances: A Statistical Distances Python Package

This is a package for computing distances among observations of statistical variables, such as: Euclidean, Minkowski, Canberra, Pearson, Mahalanobis, Robust Mahalanobis, Gower, Generalized Gower and Related Metric Scaling (RelMS). A total of 41 statistical distances can be computed.


## Installation

```python
pip install PyDistances
```

## Example of use


```python
import PyDistances
```

```python
from PyDistances import Euclidean_Dist, Euclidean_Dist_Matrix, Minkowski_Dist, Minkowski_Dist_Matrix, Canberra_Dist, Canberra_Dist_Matrix, Pearson_Dist, Pearson_Dist_Matrix, Mahalanobis_Dist, Mahalanobis_Dist_Matrix, a_b_c_d_Matrix, Sokal_Similarity, Sokal_Dist, Sokal_Dist_Matrix, Jaccard_Similarity, Jaccard_Dist, Jaccard_Dist_Matrix, alpha, Matching_Similarity, Matching_Dist, Matching_Dist_Matrix, Gower_Similarity_Matrix, Gower_Dist_Matrix, Robust_Mahalanobis_Dist, Robust_Mahalanobis_Dist_Matrix, GeneralizedGowerDistance
```

### Getting data

We load the data we are going to work with throughout this tutorial. This data-set is available in the following link: https://github.com/FabioScielzoOrtiz/Distances_Package/blob/master/Tests/House_Price.csv
```python
Data = pd.read_csv('House_Price.csv')
```


```python
Data = Data.loc[0:150, ['latitude', 'longitude', 'price', 'size_in_m_2', 'balcony_recode', 'private_garden_recode', 'private_gym_recode', 'quality_recode', 'no_of_bathrooms', 'no_of_bedrooms']]
```


```python
Data_quant = Data.loc[:,['latitude', 'longitude', 'price', 'size_in_m_2']]
Data_binary = Data.loc[:,['balcony_recode', 'private_garden_recode', 'private_gym_recode']]
Data_multiclass = Data.loc[:,['quality_recode', 'no_of_bathrooms', 'no_of_bedrooms']]
```



```python
Data.head() # p1=4, p2=3, p3=3
```
|  latitude  |  longitude  |   price    |  size_in_m_2  |  balcony  |  private_garden  |  private_gym  |  quality  |  no_of_bathrooms  |  no_of_bedrooms  |
|:----------:|:-----------:|:----------:|:-------------:|:----------------:|:-----------------------:|:--------------------:|:----------------:|:-----------------:|:----------------:|
|  25.1132   |   55.1389   |  2.7e+06   |    100.242    |        1         |            0            |          0           |        2         |         2         |        1         |
|  25.1068   |   55.1512   |  2.85e+06  |    146.973    |        1         |            0            |          0           |        2         |         2         |        2         |
|  25.0633   |   55.1377   |  1.15e+06  |    181.254    |        1         |            0            |          0           |        2         |         5         |        3         |
|  25.2273   |   55.3418   |  2.85e+06  |    187.664    |        1         |            0            |          0           |        1         |         3         |        2         |
|  25.1143   |   55.1398   | 1.7292e+06 |    47.1018    |        0         |            0            |          0           |        2         |         1         |        0         |


<br>

## Computing Euclidean distance

We compute the Euclidean distance between observation of index 0 and itself.
```python
Euclidean_Dist(Data_quant.iloc[0,:], Data_quant.iloc[0,:])
```
    
     0.0


We compute the Euclidean distance between observation of index 0 and the one of index 2.

```python
Euclidean_Dist(Data_quant.iloc[0,:], Data_quant.iloc[2,:])
```

     1550000.002117049


We compute the Euclidean distances matrix for the data-set `Data_quant`.
```python
Euclidean_Dist_Matrix(Data_quant)
```
```
array([[       0.        ,   150000.00727904,  1550000.00211705, ...,
         1500000.00009635,  2700000.01899102, 12100000.00553371],
       [  150000.00727904,        0.        ,  1700000.00034565, ...,
         1650000.00026782,  2550000.0146678 , 11950000.00426352],
       [ 1550000.00211705,  1700000.00034565,        0.        , ...,
           50000.040973  ,  4250000.00673279, 13650000.00297389],
       ...,
       [ 1500000.00009635,  1650000.00026782,    50000.040973  , ...,
               0.        ,  4200000.01094663, 13600000.00447653],
       [ 2700000.01899102,  2550000.0146678 ,  4250000.00673279, ...,
         4200000.01094663,        0.        ,  9400000.00011113],
       [12100000.00553371, 11950000.00426352, 13650000.00297389, ...,
        13600000.00447653,  9400000.00011113,        0.        ]])
```

<br>

Now, we are going to repeat the same procedure with other available distances in `PyDistances`.

<br>

## Computing Minkowski distance


```python
Minkowski_Dist(Data_quant.iloc[0,:], Data_quant.iloc[0,:], q=1)
```

     0.0


```python
Minkowski_Dist(Data_quant.iloc[0,:], Data_quant.iloc[2,:], q=1)
```
     1550081.062526



```python
Minkowski_Dist_Matrix(Data_quant, q=1)
```
```
array([[       0.      ,   150046.748877,  1550081.062526, ...,
         1500017.050769,  2700320.266531, 12100365.997115],
       [  150046.748877,        0.      ,  1700034.338187, ...,
         1650029.78435 ,  2550273.554024, 11950319.272776],
       [ 1550081.062526,  1700034.338187,        0.      , ...,
           50064.027555,  4250239.302851, 13650284.955165],
       ...,
       [ 1500017.050769,  1650029.78435 ,    50064.027555, ...,
               0.      ,  4200303.29563 , 13600348.947944],
       [ 2700320.266531,  2550273.554024,  4250239.302851, ...,
         4200303.29563 ,        0.      ,  9400045.764238],
       [12100365.997115, 11950319.272776, 13650284.955165, ...,
        13600348.947944,  9400045.764238,        0.      ]])
```

<br>

## Computing Canberra distance

```python
Canberra_Dist(Data_quant.iloc[0,:], Data_quant.iloc[0,:])
```

      0.0

```python
Canberra_Dist(Data_quant.iloc[0,:], Data_quant.iloc[2,:])
``` 

     0.6913917083019879

```python
Canberra_Dist_Matrix(Data_quant)
```

```
array([[0.        , 0.21629237, 0.69139171, ..., 0.463675  , 0.9485963 ,
        1.33838751],
       [0.21629237, 0.        , 0.53043317, ..., 0.52079671, 0.79157752,
        1.19854721],
       [0.69139171, 0.53043317, 0.        , ..., 0.23597883, 1.04765637,
        1.29619958],
       ...,
       [0.463675  , 0.52079671, 0.23597883, ..., 0.        , 1.20126891,
        1.44813664],
       [0.9485963 , 0.79157752, 1.04765637, ..., 1.20126891, 0.        ,
        0.51782969],
       [1.33838751, 1.19854721, 1.29619958, ..., 1.44813664, 0.51782969,
        0.        ]])
```

<br>

## Computing Pearson distance

```python
Pearson_Dist(Data_quant.iloc[0,:], Data_quant.iloc[0,:], variance=Data.var())
```

     0.0

```python
Pearson_Dist(Data_quant.iloc[0,:], Data_quant.iloc[2,:], variance=Data.var())
```

     1.5393297661160206


```python
Pearson_Dist_Matrix(Data_quant)
```
```
array([[0.        , 0.63961801, 1.53932977, ..., 1.03084131, 4.32943281,
        7.47171915],
       [0.63961801, 0.        , 1.20505141, ..., 1.09780711, 3.76643257,
        7.04893716],
       [1.53932977, 1.20505141, 0.        , ..., 0.84617436, 3.79891055,
        7.4670243 ],
       ...,
       [1.03084131, 1.09780711, 0.84617436, ..., 0.        , 4.44143053,
        7.87905955],
       [4.32943281, 3.76643257, 3.79891055, ..., 4.44143053, 0.        ,
        4.57460318],
       [7.47171915, 7.04893716, 7.4670243 , ..., 7.87905955, 4.57460318,
        0.        ]])
```


<br>

## Computing Mahalanobis distance

```python
Mahalanobis_Dist(Data_quant.iloc[0,:], Data_quant.iloc[2,:], S_inv=np.linalg.inv( np.cov(Data_quant , rowvar=False) ))
```

       0.0


```python
Mahalanobis_Dist(Data_quant.iloc[0,:], Data_quant.iloc[2,:], S_inv=np.linalg.inv( np.cov(Data_quant , rowvar=False) ))
```

      2.7671855371187757

```python
Mahalanobis_Dist_Matrix(Data_quant)
```

```
array([[0.        , 0.92801614, 2.76718554, ..., 1.52541554, 5.21105193,
        6.45997793],
       [0.92801614, 0.        , 1.96135599, ..., 0.98693199, 4.43479282,
        6.2920865 ],
       [2.76718554, 1.96135599, 0.        , ..., 1.3592188 , 3.4307313 ,
        7.27986558],
       ...,
       [1.52541554, 0.98693199, 1.3592188 , ..., 0.        , 4.41360406,
        7.01503103],
       [5.21105193, 4.43479282, 3.4307313 , ..., 4.41360406, 0.        ,
        7.4691448 ],
       [6.45997793, 6.2920865 , 7.27986558, ..., 7.01503103, 7.4691448 ,
        0.        ]])
```


<br>

## Computing Sokal similarity

```python
a,b,c,d,p = a_b_c_d_Matrix(Data_binary)
```


```python
Sokal_Similarity(i=0, r=2, a=a, d=d, p=p)
```

     1.0

```python
Sokal_Dist(i=0, r=2, a=a, d=d, p=p)
```
     0.0


```python
Sokal_Dist_Matrix(Data_binary)
```
```
array([[0.        , 0.        , 0.        , ..., 0.        , 0.        ,
        0.81649658],
       [0.        , 0.        , 0.        , ..., 0.        , 0.        ,
        0.81649658],
       [0.        , 0.        , 0.        , ..., 0.        , 0.        ,
        0.81649658],
       ...,
       [0.        , 0.        , 0.        , ..., 0.        , 0.        ,
        0.81649658],
       [0.        , 0.        , 0.        , ..., 0.        , 0.        ,
        0.81649658],
       [0.81649658, 0.81649658, 0.81649658, ..., 0.81649658, 0.81649658,
        0.        ]])
```


<br>

## Computing Jaccard similarity

```python
Jaccard_Similarity(i=0, r=2, a=a, d=d, p=p)
```
      1.0


```python
Jaccard_Dist(i=0, r=2, a=a, d=d, p=p)
```
     0.0

```python
Jaccard_Dist_Matrix(Data_binary)
```
```
array([[0., 0., 0., ..., 0., 0., 1.],
       [0., 0., 0., ..., 0., 0., 1.],
       [0., 0., 0., ..., 0., 0., 1.],
       ...,
       [0., 0., 0., ..., 0., 0., 1.],
       [0., 0., 0., ..., 0., 0., 1.],
       [1., 1., 1., ..., 1., 1., 0.]])
```


<br>

## Computing Matching similarity

```python
Matching_Similarity(x_i=Data_multiclass.iloc[0,:], x_r=Data_multiclass.iloc[2,:], Data=Data_multiclass)
```

    0.3333333333333333


```python
Matching_Dist(x_i=Data_multiclass.iloc[0,:], x_r=Data_multiclass.iloc[2,:], Data=Data_multiclass)
```

       1.1547005383792517


```python
Matching_Dist_Matrix(Data_multiclass)
```
```
array([[0.        , 0.81649658, 1.15470054, ..., 0.81649658, 1.15470054,
        1.41421356],
       [0.81649658, 0.        , 1.15470054, ..., 0.        , 1.15470054,
        1.41421356],
       [1.15470054, 1.15470054, 0.        , ..., 1.15470054, 0.81649658,
        1.15470054],
       ...,
       [0.81649658, 0.        , 1.15470054, ..., 0.        , 1.15470054,
        1.41421356],
       [1.15470054, 1.15470054, 0.81649658, ..., 1.15470054, 0.        ,
        1.15470054],
       [1.41421356, 1.41421356, 1.15470054, ..., 1.41421356, 1.15470054,
        0.        ]])
```

<br>

## Computing Gower distance

From a theoretical perspective Gower (1971) has been followed.

```python
Gower_Similarity_Matrix(Data, p1=4, p2=3, p3=3)
```

```
array([[1.        , 0.85175283, 0.68485131, ..., 0.83008431, 0.62482353,
        0.34709882],
       [0.85175283, 1.        , 0.69489168, ..., 0.94863663, 0.63064768,
        0.35833279],
       [0.68485131, 0.69489168, 1.        , ..., 0.72293677, 0.73120218,
        0.48172501],
       ...,
       [0.83008431, 0.94863663, 0.72293677, ..., 1.        , 0.59776459,
        0.36311382],
       [0.62482353, 0.63064768, 0.73120218, ..., 0.59776459, 1.        ,
        0.55654437],
       [0.34709882, 0.35833279, 0.48172501, ..., 0.36311382, 0.55654437,
        1.        ]])
```

```python
Gower_Dist_Matrix(Data, p1=4, p2=3, p3=3)
```

```
array([[0.        , 0.38502879, 0.56138105, ..., 0.41220831, 0.61251651,
        0.808023  ],
       [0.38502879, 0.        , 0.55236611, ..., 0.22663488, 0.60774363,
        0.80104133],
       [0.56138105, 0.55236611, 0.        , ..., 0.52636796, 0.51845716,
        0.71991318],
       ...,
       [0.41220831, 0.22663488, 0.52636796, ..., 0.        , 0.63422032,
        0.79805149],
       [0.61251651, 0.60774363, 0.51845716, ..., 0.63422032, 0.        ,
        0.66592464],
       [0.808023  , 0.80104133, 0.71991318, ..., 0.79805149, 0.66592464,
        0.        ]])
```


<br>

## Computing Robust Mahalanobis distance

From a theoretical perspective Gnanadesikan (1997) and  Delvin et al. (1975) have been followed.

```python
Robust_Mahalanobis_Dist(x_i=Data_quant.iloc[0,:], x_r=Data_quant.iloc[2,:], Data=Data_quant, Method='MAD', epsilon=0.05, n_iters=20)
```
     2.1448247626892223

```python
Robust_Mahalanobis_Dist(x_i=Data_quant.iloc[0,:], x_r=Data_quant.iloc[2,:], Data=Data_quant, Method='trimmed', alpha=0.1, epsilon=0.05, n_iters=20)
```
     2.7434709885399884


```python
Robust_Mahalanobis_Dist(x_i=Data_quant.iloc[0,:], x_r=Data_quant.iloc[2,:], Data=Data_quant, Method='winsorized', alpha=0.1, epsilon=0.05, n_iters=20)
```
     2.8446274140577943

```python
Robust_Mahalanobis_Dist_Matrix(Data=Data_quant, Method='trimmed', alpha=0.1, epsilon=0.05, n_iters=20)
```

```
array([[ 0.        ,  0.89250845,  2.74347099, ...,  1.48503889,
         5.95276234,  8.49453068],
       [ 0.89250845,  0.        ,  1.99959936, ...,  0.96839524,
         5.33355737,  8.32070442],
       [ 2.74347099,  1.99959936,  0.        , ...,  1.36336733,
         4.12306341,  9.38094479],
       ...,
       [ 1.48503889,  0.96839524,  1.36336733, ...,  0.        ,
         5.1322854 ,  9.00337923],
       [ 5.95276234,  5.33355737,  4.12306341, ...,  5.1322854 ,
         0.        , 11.06785954],
       [ 8.49453068,  8.32070442,  9.38094479, ...,  9.00337923,
        11.06785954,  0.        ]])
```

<br>

## Computing Generalized Gower distance and Releted Metric Scaling

To end this tutorial we are going to compute both the Gower distance matrix and the Related Metric Scaling matrix for the mixed data-set `Data`. And we are going to do that considering all the possible combinations of the quantitative, binary and multiclass distances. Then, we will save all the resulting matrix in a Python dictionary.

From a theoretical perspective we have followed Cuadras and Fortiana (1998), Albarrán et al. (2015) and Grané et al. (2021).

```python
D_GG_list_maha_robust = []
D_RelMS_list_maha_robust = []
D_GG_list_not_maha_robust = []
D_RelMS_list_not_maha_robust = []

d1_list = ['Euclidean', 'Minkowski', 'Canberra', 'Pearson', 'Mahalanobis']
d2_list = ['Sokal', 'Jaccard']
d3_list = ['Matching']
```

```python
for d in itertools.product(d1_list, d2_list, d3_list) :
    Generalized_Gower_Distance_init = GeneralizedGowerDistance(Data=Data, p1=4, p2=3, p3=3, d1=d[0], d2=d[1], d3=d[2], q=1)
    D, D_2 = Generalized_Gower_Distance_init.compute(Related_Metric_Scaling=False)
    D_GG_list_not_maha_robust.append(D)
```

```python
for d in itertools.product(['Robust_Mahalanobis'], d2_list, d3_list, ['trimmed', 'winsorized', 'MAD']) :
   Generalized_Gower_Distance_init = GeneralizedGowerDistance(Data=Data, p1=4, p2=3, p3=3, d1=d[0], d2=d[1], d3=d[2], epsilon=0.05, Method=d[3], alpha=0.1)
   D, D_2 = Generalized_Gower_Distance_init.compute(Related_Metric_Scaling=False)
   D_GG_list_maha_robust.append(D)
```


```python
for d in itertools.product(d1_list, d2_list, d3_list) :
   Generalized_Gower_Distance_init = GeneralizedGowerDistance(Data=Data, p1=4, p2=3, p3=3, d1=d[0], d2=d[1], d3=d[2], q=1)
   D, D_2 = Generalized_Gower_Distance_init.compute(Related_Metric_Scaling=True, tol=0.009, d=2)
   D_RelMS_list_not_maha_robust.append(D)
```
 

```python
for d in itertools.product(['Robust_Mahalanobis'], d2_list, d3_list, ['trimmed', 'winsorized', 'MAD']) :
   Generalized_Gower_Distance_init = GeneralizedGowerDistance(Data=Data, p1=4, p2=3, p3=3, d1=d[0], d2=d[1], d3=d[2], epsilon=0.05, Method=d[3], alpha=0.1)
   D, D_2 = Generalized_Gower_Distance_init.compute(Related_Metric_Scaling=True, tol=0.009, d=2)
   D_RelMS_list_maha_robust.append(D)
```

```python
D_GG_list = D_GG_list_not_maha_robust + D_GG_list_maha_robust
D_RelMS_list = D_RelMS_list_not_maha_robust + D_RelMS_list_maha_robust
```


```python
search_space = [x  for x in D_GG_list] + [x  for x in D_RelMS_list]
distance_names = ['GG_'+x[0]+'_'+x[1]+'_'+x[2]  for x in itertools.product(d1_list, d2_list, d3_list)] + ['GG_'+x[0]+'_'+x[1]+'_'+x[2]+'_'+x[3] for x in itertools.product(['Robust_Mahalanobis'], d2_list, d3_list, ['trimmed', 'winsorized', 'MAD'])] + ['RelMS_'+x[0]+'_'+x[1]+'_'+x[2] for x in itertools.product(d1_list, d2_list, d3_list)] + ['RelMS_'+x[0]+'_'+x[1]+'_'+x[2]+'_'+x[3] for x in itertools.product(['Robust_Mahalanobis'], d2_list, d3_list, ['trimmed', 'winsorized', 'MAD'])]
dic_distance_matrix = dict(zip(distance_names, search_space))
```

```python
dic_distance_matrix
```


```
{'GG_Euclidean_Sokal_Matching': array([[0.        , 1.01161446, 1.60800698, ..., 1.23798333, 1.92432848,
         6.35838514],
        [1.01161446, 0.        , 1.64229596, ..., 0.7889253 , 1.87696727,
         6.29319748],
        [1.60800698, 1.64229596, 0.        , ..., 1.42723912, 2.26882579,
         6.96673669],
        ...,
        [1.23798333, 0.7889253 , 1.42723912, ..., 0.        , 2.4635748 ,
         7.01727531],
        [1.92432848, 1.87696727, 2.26882579, ..., 2.4635748 , 0.        ,
         5.11270638],
        [6.35838514, 6.29319748, 6.96673669, ..., 7.01727531, 5.11270638,
         0.        ]]),
 'GG_Euclidean_Jaccard_Matching': array([[0.        , 1.01161446, 1.60800698, ..., 1.23798333, 1.92432848,
         6.21923207],
        [1.01161446, 0.        , 1.64229596, ..., 0.7889253 , 1.87696727,
         6.15257024],
        [1.60800698, 1.64229596, 0.        , ..., 1.42723912, 2.26882579,
         6.83997121],
        ...,
        [1.23798333, 0.7889253 , 1.42723912, ..., 0.        , 2.4635748 ,
         6.89143953],
        [1.92432848, 1.87696727, 2.26882579, ..., 2.4635748 , 0.        ,
         4.93857798],
        [6.21923207, 6.15257024, 6.83997121, ..., 6.89143953, 4.93857798,
         0.        ]]),
 'GG_Minkowski_Sokal_Matching': array([[0.        , 1.01161589, 1.60801451, ..., 1.23797549, 1.92440501,
         6.35838512],
        [1.01161589, 0.        , 1.64229192, ..., 0.78891568, 1.87702827,
         6.29317915],
        [1.60801451, 1.64229192, 0.        , ..., 1.42723962, 2.2688732 ,
         6.96667937],
        ...,
        [1.23797549, 0.78891568, 1.42723962, ..., 0.        , 2.46364348,
         7.01724763],
        [1.92440501, 1.87702827, 2.2688732 , ..., 2.46364348, 0.        ,
         5.11260609],
        [6.35838512, 6.29317915, 6.96667937, ..., 7.01724763, 5.11260609,
         0.        ]]),
 'GG_Minkowski_Jaccard_Matching': array([[0.        , 1.01161589, 1.60801451, ..., 1.23797549, 1.92440501,
         6.21923205],
        [1.01161589, 0.        , 1.64229192, ..., 0.78891568, 1.87702827,
         6.15255149],
        [1.60801451, 1.64229192, 0.        , ..., 1.42723962, 2.2688732 ,
         6.83991282],
        ...,
        [1.23797549, 0.78891568, 1.42723962, ..., 0.        , 2.46364348,
         6.89141134],
        [1.92440501, 1.87702827, 2.2688732 , ..., 2.46364348, 0.        ,
         4.93847416],
        [6.21923205, 6.15255149, 6.83991282, ..., 6.89141134, 4.93847416,
         0.        ]]),
 'GG_Canberra_Sokal_Matching': array([[0.        , 1.1089173 , 2.04873576, ..., 1.41070641, 2.47064802,
         3.88007815],
        [1.1089173 , 0.        , 1.81887649, ..., 1.10728448, 2.20656591,
         3.66760203],
        [2.04873576, 1.81887649, 0.        , ..., 1.51266848, 2.44536222,
         3.67890583],
        ...,
        [1.41070641, 1.10728448, 1.51266848, ..., 0.        , 2.92569072,
         4.05431191],
        [2.47064802, 2.20656591, 2.44536222, ..., 2.92569072, 0.        ,
         2.67423498],
        [3.88007815, 3.66760203, 3.67890583, ..., 4.05431191, 2.67423498,
         0.        ]]),
 'GG_Canberra_Jaccard_Matching': array([[0.        , 1.1089173 , 2.04873576, ..., 1.41070641, 2.47064802,
         3.64757349],
        [1.1089173 , 0.        , 1.81887649, ..., 1.10728448, 2.20656591,
         3.42068569],
        [2.04873576, 1.81887649, 0.        , ..., 1.51266848, 2.44536222,
         3.43280265],
        ...,
        [1.41070641, 1.10728448, 1.51266848, ..., 0.        , 2.92569072,
         3.83239234],
        [2.47064802, 2.20656591, 2.44536222, ..., 2.92569072, 0.        ,
         2.32407372],
        [3.64757349, 3.42068569, 3.43280265, ..., 3.83239234, 2.32407372,
         0.        ]]),
 'GG_Pearson_Sokal_Matching': array([[0.        , 1.0588577 , 1.62258227, ..., 1.13386485, 2.59878376,
         4.5833716 ],
        [1.0588577 , 0.        , 1.54980561, ..., 0.55073019, 2.36782324,
         4.41160916],
        [1.62258227, 1.54980561, 0.        , ..., 1.48883715, 2.15643298,
         4.46893998],
        ...,
        [1.13386485, 0.55073019, 1.48883715, ..., 0.        , 2.64592015,
         4.75194328],
        [2.59878376, 2.36782324, 2.15643298, ..., 2.64592015, 0.        ,
         3.34753806],
        [4.5833716 , 4.41160916, 4.46893998, ..., 4.75194328, 3.34753806,
         0.        ]]),
 'GG_Pearson_Jaccard_Matching': array([[0.        , 1.0588577 , 1.62258227, ..., 1.13386485, 2.59878376,
         4.38828909],
        [1.0588577 , 0.        , 1.54980561, ..., 0.55073019, 2.36782324,
         4.20857237],
        [1.62258227, 1.54980561, 0.        , ..., 1.48883715, 2.15643298,
         4.26863098],
        ...,
        [1.13386485, 0.55073019, 1.48883715, ..., 0.        , 2.64592015,
         4.56407174],
        [2.59878376, 2.36782324, 2.15643298, ..., 2.64592015, 0.        ,
         3.07502796],
        [4.38828909, 4.20857237, 4.26863098, ..., 4.56407174, 3.07502796,
         0.        ]]),
 'GG_Mahalanobis_Sokal_Matching': array([[0.        , 1.11128701, 1.9908619 , ..., 1.26642065, 2.97833241,
         4.17851469],
        [1.11128701, 0.        , 1.73337267, ..., 0.49510815, 2.64311668,
         4.11353573],
        [1.9908619 , 1.73337267, 0.        , ..., 1.5815777 , 1.99507289,
         4.39053781],
        ...,
        [1.26642065, 0.49510815, 1.5815777 , ..., 0.        , 2.63417571,
         4.3979867 ],
        [2.97833241, 2.64311668, 1.99507289, ..., 2.63417571, 0.        ,
         4.4698317 ],
        [4.17851469, 4.11353573, 4.39053781, ..., 4.3979867 , 4.4698317 ,
         0.        ]]),
 'GG_Mahalanobis_Jaccard_Matching': array([[0.        , 1.11128701, 1.9908619 , ..., 1.26642065, 2.97833241,
         3.96355535],
        [1.11128701, 0.        , 1.73337267, ..., 0.49510815, 2.64311668,
         3.89499193],
        [1.9908619 , 1.73337267, 0.        , ..., 1.5815777 , 1.99507289,
         4.18647921],
        ...,
        [1.26642065, 0.49510815, 1.5815777 , ..., 0.        , 2.63417571,
         4.19429052],
        [2.97833241, 2.64311668, 1.99507289, ..., 2.63417571, 0.        ,
         4.26956454],
        [3.96355535, 3.89499193, 4.18647921, ..., 4.19429052, 4.26956454,
         0.        ]]),
 'GG_Robust_Mahalanobis_Sokal_Matching_trimmed': array([[0.        , 1.0738818 , 1.81990287, ..., 1.17982158, 2.83584093,
         4.38026385],
        [1.0738818 , 0.        , 1.64744788, ..., 0.39866732, 2.61869851,
         4.3233478 ],
        [1.81990287, 1.64744788, 0.        , ..., 1.53344794, 1.97466567,
         4.56660697],
        ...,
        [1.17982158, 0.39866732, 1.53344794, ..., 0.        , 2.54962302,
         4.5492545 ],
        [2.83584093, 2.61869851, 1.97466567, ..., 2.54962302, 0.        ,
         5.16721825],
        [4.38026385, 4.3233478 , 4.56660697, ..., 4.5492545 , 5.16721825,
         0.        ]]),
 'GG_Robust_Mahalanobis_Sokal_Matching_winsorized': array([[0.        , 1.10035027, 1.96521318, ..., 1.24876507, 3.02193061,
         4.2158267 ],
        [1.10035027, 0.        , 1.72244788, ..., 0.45786845, 2.71169847,
         4.170886  ],
        [1.96521318, 1.72244788, 0.        , ..., 1.57396145, 2.01907767,
         4.45138733],
        ...,
        [1.24876507, 0.45786845, 1.57396145, ..., 0.        , 2.6589383 ,
         4.42575055],
        [3.02193061, 2.71169847, 2.01907767, ..., 2.6589383 , 0.        ,
         4.74960743],
        [4.2158267 , 4.170886  , 4.45138733, ..., 4.42575055, 4.74960743,
         0.        ]]),
 'GG_Robust_Mahalanobis_Sokal_Matching_MAD': array([[0.        , 1.09006233, 1.80375514, ..., 1.18201607, 2.67497233,
         4.55678538],
        [1.09006233, 0.        , 1.62058379, ..., 0.44488228, 2.40606721,
         4.40232615],
        [1.80375514, 1.62058379, 0.        , ..., 1.53278692, 1.93813141,
         4.46679441],
        ...,
        [1.18201607, 0.44488228, 1.53278692, ..., 0.        , 2.48916367,
         4.64371521],
        [2.67497233, 2.40606721, 1.93813141, ..., 2.48916367, 0.        ,
         4.16671594],
        [4.55678538, 4.40232615, 4.46679441, ..., 4.64371521, 4.16671594,
         0.        ]]),
 'GG_Robust_Mahalanobis_Jaccard_Matching_trimmed': array([[0.        , 1.0738818 , 1.81990287, ..., 1.17982158, 2.83584093,
         4.17570322],
        [1.0738818 , 0.        , 1.64744788, ..., 0.39866732, 2.61869851,
         4.11595944],
        [1.81990287, 1.64744788, 0.        , ..., 1.53344794, 1.97466567,
         4.37077626],
        ...,
        [1.17982158, 0.39866732, 1.53344794, ..., 0.        , 2.54962302,
         4.35264315],
        [2.83584093, 2.61869851, 1.97466567, ..., 2.54962302, 0.        ,
         4.99499053],
        [4.17570322, 4.11595944, 4.37077626, ..., 4.35264315, 4.99499053,
         0.        ]]),
 'GG_Robust_Mahalanobis_Jaccard_Matching_winsorized': array([[0.        , 1.10035027, 1.96521318, ..., 1.24876507, 3.02193061,
         4.00287155],
        [1.10035027, 0.        , 1.72244788, ..., 0.45786845, 2.71169847,
         3.95551209],
        [1.96521318, 1.72244788, 0.        , ..., 1.57396145, 2.01907767,
         4.25025118],
        ...,
        [1.24876507, 0.45786845, 1.57396145, ..., 0.        , 2.6589383 ,
         4.22339365],
        [3.02193061, 2.71169847, 2.01907767, ..., 2.6589383 , 0.        ,
         4.5616397 ],
        [4.00287155, 3.95551209, 4.25025118, ..., 4.22339365, 4.5616397 ,
         0.        ]]),
 'GG_Robust_Mahalanobis_Jaccard_Matching_MAD': array([[0.        , 1.09006233, 1.80375514, ..., 1.18201607, 2.67497233,
         4.36051361],
        [1.09006233, 0.        , 1.62058379, ..., 0.44488228, 2.40606721,
         4.19884049],
        [1.80375514, 1.62058379, 0.        , ..., 1.53278692, 1.93813141,
         4.26638468],
        ...,
        [1.18201607, 0.44488228, 1.53278692, ..., 0.        , 2.48916367,
         4.45127812],
        [2.67497233, 2.40606721, 1.93813141, ..., 2.48916367, 0.        ,
         3.95111474],
        [4.36051361, 4.19884049, 4.26638468, ..., 4.45127812, 3.95111474,
         0.        ]]),
 'RelMS_Euclidean_Sokal_Matching': array([[0.        , 1.01092438, 1.68587263, ..., 1.2435966 , 1.75479379,
         5.76354972],
        [1.01092436, 0.        , 1.72123768, ..., 0.78892531, 1.71977376,
         5.69924943],
        [1.68587264, 1.7212377 , 0.        , ..., 1.42997022, 2.20660915,
         6.5504967 ],
        ...,
        [1.24359658, 0.78892532, 1.42997021, ..., 0.        , 2.26671431,
         6.42377887],
        [1.7547938 , 1.71977375, 2.20660914, ..., 2.26671431, 0.        ,
         4.781135  ],
        [5.76354972, 5.69924943, 6.55049671, ..., 6.42377887, 4.78113499,
         0.        ]]),
 'RelMS_Euclidean_Jaccard_Matching': array([[0.        , 1.01092435, 1.68587263, ..., 1.24359659, 1.75479381,
         5.73873464],
        [1.01092437, 0.        , 1.72123769, ..., 0.78892532, 1.71977378,
         5.67208311],
        [1.68587264, 1.72123769, 0.        , ..., 1.42997021, 2.20660914,
         6.53309456],
        ...,
        [1.24359658, 0.78892529, 1.42997021, ..., 0.        , 2.26671431,
         6.41402297],
        [1.7547938 , 1.71977375, 2.20660914, ..., 2.2667143 , 0.        ,
         4.6957284 ],
        [5.73873463, 5.67208312, 6.53309457, ..., 6.41402297, 4.69572838,
         0.        ]]),
 'RelMS_Minkowski_Sokal_Matching': array([[0.        , 1.0104344 , 1.68473307, ..., 1.24302039, 1.75451827,
         5.7636572 ],
        [1.01043437, 0.        , 1.72039524, ..., 0.78891568, 1.71978231,
         5.69946617],
        [1.68473308, 1.72039525, 0.        , ..., 1.42922921, 2.20651554,
         6.55109162],
        ...,
        [1.24302037, 0.7889157 , 1.4292292 , ..., 0.        , 2.2667207 ,
         6.42402052],
        [1.75451827, 1.71978229, 2.20651553, ..., 2.2667207 , 0.        ,
         4.78235997],
        [5.7636572 , 5.69946616, 6.55109161, ..., 6.42402052, 4.78235997,
         0.        ]]),
 'RelMS_Minkowski_Jaccard_Matching': array([[0.        , 1.01043437, 1.68473307, ..., 1.24302038, 1.75451828,
         5.73875343],
        [1.01043439, 0.        , 1.72039525, ..., 0.78891569, 1.71978232,
         5.67221733],
        [1.68473307, 1.72039524, 0.        , ..., 1.4292292 , 2.20651553,
         6.5336026 ],
        ...,
        [1.24302038, 0.78891568, 1.4292292 , ..., 0.        , 2.2667207 ,
         6.41417732],
        [1.75451828, 1.7197823 , 2.20651553, ..., 2.2667207 , 0.        ,
         4.6969009 ],
        [5.73875342, 5.67221732, 6.5336026 , ..., 6.41417732, 4.6969009 ,
         0.        ]]),
 'RelMS_Canberra_Sokal_Matching': array([[0.        , 3.29475825, 3.63767326, ..., 3.42002989, 3.78234978,
         4.28387746],
        [3.29475817, 0.        , 3.54627477, ..., 3.36365755, 3.64707779,
         4.11290306],
        [3.63767327, 3.5462748 , 0.        , ..., 3.36371231, 3.88636668,
         4.26421609],
        ...,
        [3.42002989, 3.36365756, 3.36371231, ..., 0.        , 4.08835735,
         4.43146723],
        [3.78234979, 3.64707779, 3.88636667, ..., 4.08835736, 0.        ,
         3.55682862],
        [4.28387745, 4.11290305, 4.26421607, ..., 4.43146723, 3.55682862,
         0.        ]]),
 'RelMS_Canberra_Jaccard_Matching': array([[0.        , 3.29475816, 3.63767325, ..., 3.42002988, 3.7823498 ,
         4.18398249],
        [3.29475818, 0.        , 3.54627479, ..., 3.36365756, 3.64707782,
         4.00084943],
        [3.63767326, 3.54627478, 0.        , ..., 3.36371229, 3.88636666,
         4.15092751],
        ...,
        [3.42002988, 3.36365755, 3.36371228, ..., 0.        , 4.08835736,
         4.3378168 ],
        [3.78234979, 3.64707778, 3.88636666, ..., 4.08835735, 0.        ,
         3.36218137],
        [4.18398248, 4.00084941, 4.15092752, ..., 4.3378168 , 3.36218137,
         0.        ]]),
 'RelMS_Pearson_Sokal_Matching': array([[0.        , 1.04250916, 1.57029271, ..., 1.11835441, 2.35030151,
         3.99961285],
        [1.04250913, 0.        , 1.55642417, ..., 0.55073019, 2.17276224,
         3.83629275],
        [1.5702927 , 1.55642418, 0.        , ..., 1.44481248, 2.11094744,
         4.05200057],
        ...,
        [1.11835439, 0.55073021, 1.44481248, ..., 0.        , 2.43447697,
         4.16544183],
        [2.35030151, 2.17276223, 2.11094745, ..., 2.43447697, 0.        ,
         3.00502738],
        [3.99961283, 3.83629274, 4.05200056, ..., 4.16544183, 3.00502738,
         0.        ]]),
 'RelMS_Pearson_Jaccard_Matching': array([[0.        , 1.04250913, 1.57029271, ..., 1.11835441, 2.35030152,
         3.89789603],
        [1.04250915, 0.        , 1.55642418, ..., 0.55073023, 2.17276226,
         3.72479069],
        [1.5702927 , 1.55642415, 0.        , ..., 1.44481247, 2.11094744,
         3.94329467],
        ...,
        [1.11835439, 0.55073016, 1.44481248, ..., 0.        , 2.43447698,
         4.07654071],
        [2.35030152, 2.17276223, 2.11094745, ..., 2.43447697, 0.        ,
         2.77842982],
        [3.89789601, 3.72479067, 3.94329467, ..., 4.0765407 , 2.77842982,
         0.        ]]),
 'RelMS_Mahalanobis_Sokal_Matching': array([[0.        , 1.0872495 , 1.91566724, ..., 1.23718333, 2.78694322,
         3.59368169],
        [1.08724948, 0.        , 1.72190382, ..., 0.49510814, 2.51013925,
         3.52430362],
        [1.91566725, 1.72190383, 0.        , ..., 1.53860587, 1.97114821,
         3.91897956],
        ...,
        [1.23718333, 0.49510818, 1.53860586, ..., 0.        , 2.47401146,
         3.7944967 ],
        [2.78694323, 2.51013924, 1.97114821, ..., 2.47401146, 0.        ,
         4.10401609],
        [3.59368167, 3.52430361, 3.91897955, ..., 3.7944967 , 4.10401609,
         0.        ]]),
 'RelMS_Mahalanobis_Jaccard_Matching': array([[0.        , 1.08724947, 1.91566724, ..., 1.23718333, 2.78694323,
         3.46907215],
        [1.0872495 , 0.        , 1.72190383, ..., 0.49510817, 2.51013926,
         3.39550188],
        [1.91566724, 1.72190381, 0.        , ..., 1.53860586, 1.97114821,
         3.80535063],
        ...,
        [1.23718333, 0.49510812, 1.53860586, ..., 0.        , 2.47401147,
         3.68911387],
        [2.78694323, 2.51013924, 1.97114821, ..., 2.47401147, 0.        ,
         3.96214705],
        [3.46907213, 3.39550187, 3.80535063, ..., 3.68911387, 3.96214705,
         0.        ]]),
 'RelMS_Robust_Mahalanobis_Sokal_Matching_trimmed': array([[0.        , 1.05396495, 1.74951184, ..., 1.15390312, 2.67058462,
         3.82780883],
        [1.05396493, 0.        , 1.63479812, ..., 0.39866731, 2.51224528,
         3.76362714],
        [1.74951185, 1.63479814, 0.        , ..., 1.49657109, 1.961588  ,
         4.09825745],
        ...,
        [1.15390311, 0.39866735, 1.49657109, ..., 0.        , 2.41854434,
         3.97375586],
        [2.67058463, 2.51224527, 1.961588  , ..., 2.41854434, 0.        ,
         4.81269468],
        [3.82780882, 3.76362713, 4.09825744, ..., 3.97375586, 4.81269468,
         0.        ]]),
 'RelMS_Robust_Mahalanobis_Sokal_Matching_winsorized': array([[0.        , 1.07688717, 1.88851059, ..., 1.21940102, 2.83800382,
         3.64003684],
        [1.07688713, 0.        , 1.70819251, ..., 0.45786842, 2.58662722,
         3.59029333],
        [1.8885106 , 1.70819253, 0.        , ..., 1.53220354, 1.99808026,
         3.97860895],
        ...,
        [1.21940101, 0.45786849, 1.53220353, ..., 0.        , 2.50787408,
         3.829693  ],
        [2.83800382, 2.58662721, 1.99808026, ..., 2.50787408, 0.        ,
         4.38739858],
        [3.64003683, 3.59029333, 3.97860894, ..., 3.829693  , 4.38739858,
         0.        ]]),
 'RelMS_Robust_Mahalanobis_Sokal_Matching_MAD': array([[0.        , 1.06915308, 1.73228661, ..., 1.15789936, 2.45834684,
         3.97049139],
        [1.06915305, 0.        , 1.61195487, ..., 0.44488227, 2.24973009,
         3.81621214],
        [1.73228661, 1.61195488, 0.        , ..., 1.4894837 , 1.90536576,
         4.00431571],
        ...,
        [1.15789934, 0.44488231, 1.4894837 , ..., 0.        , 2.30824179,
         4.04102682],
        [2.45834685, 2.24973009, 1.90536577, ..., 2.30824178, 0.        ,
         3.79967402],
        [3.97049139, 3.81621213, 4.0043157 , ..., 4.04102682, 3.79967402,
         0.        ]]),
 'RelMS_Robust_Mahalanobis_Jaccard_Matching_trimmed': array([[0.        , 1.05396492, 1.74951184, ..., 1.15390312, 2.67058463,
         3.7103996 ],
        [1.05396495, 0.        , 1.63479813, ..., 0.39866734, 2.51224529,
         3.64245313],
        [1.74951185, 1.63479812, 0.        , ..., 1.49657109, 1.961588  ,
         3.98729219],
        ...,
        [1.15390311, 0.39866728, 1.49657109, ..., 0.        , 2.41854435,
         3.87035377],
        [2.67058464, 2.51224527, 1.961588  , ..., 2.41854434, 0.        ,
         4.69932707],
        [3.71039959, 3.64245311, 3.9872922 , ..., 3.87035377, 4.69932707,
         0.        ]]),
 'RelMS_Robust_Mahalanobis_Jaccard_Matching_winsorized': array([[0.        , 1.07688714, 1.88851059, ..., 1.21940102, 2.83800383,
         3.51619033],
        [1.07688715, 0.        , 1.70819252, ..., 0.45786846, 2.58662723,
         3.46347473],
        [1.88851059, 1.70819251, 0.        , ..., 1.53220354, 1.99808026,
         3.86606614],
        ...,
        [1.219401  , 0.45786843, 1.53220353, ..., 0.        , 2.50787409,
         3.72394257],
        [2.83800382, 2.58662721, 1.99808026, ..., 2.50787408, 0.        ,
         4.25828147],
        [3.51619032, 3.46347472, 3.86606614, ..., 3.72394256, 4.25828147,
         0.        ]]),
 'RelMS_Robust_Mahalanobis_Jaccard_Matching_MAD': array([[0.        , 1.06915304, 1.73228661, ..., 1.15789935, 2.45834686,
         3.86694579],
        [1.06915307, 0.        , 1.61195488, ..., 0.4448823 , 2.24973011,
         3.7045599 ],
        [1.7322866 , 1.61195486, 0.        , ..., 1.48948369, 1.90536575,
         3.89571711],
        ...,
        [1.15789934, 0.44488225, 1.48948369, ..., 0.        , 2.30824179,
         3.9478467 ],
        [2.45834686, 2.24973009, 1.90536576, ..., 2.30824179, 0.        ,
         3.64285626],
        [3.86694578, 3.70455988, 3.8957171 , ..., 3.9478467 , 3.64285626,
         0.        ]])}
```


## Computational Cost Testing

In this case, we are going to use the entire `House_Price.csv` dataset, which has 1905 rows, to perform a computational cost test (in terms of time) of the new distance metrics included in `PyDistances`.

```python
Data = pd.read_csv('House_Price.csv')
Data = Data.loc[:, ['latitude', 'longitude', 'price', 'size_in_m_2', 'balcony_recode', 'private_garden_recode', 'private_gym_recode', 'quality_recode', 'no_of_bathrooms', 'no_of_bedrooms']]
```

```python
Data.shape
```
```      
(1905, 10)
```

```python
Generalized_Gower_Distance_init = GeneralizedGowerDistance(Data=Data, p1=4, p2=3, p3=3, d1='Robust_Mahalanobis', d2='Jaccard', d3='Matching', epsilon=0.05, Method='trimmed', alpha=0.1)
D, D_2 = Generalized_Gower_Distance_init.compute(Related_Metric_Scaling=False)

# Time: 1.11 minutes.
```

```python
Generalized_Gower_Distance_init = GeneralizedGowerDistance(Data=Data, p1=4, p2=3, p3=3, d1='Robust_Mahalanobis', d2='Jaccard', d3='Matching', epsilon=0.05, Method='winsorized', alpha=0.1)
D, D_2 = Generalized_Gower_Distance_init.compute(Related_Metric_Scaling=False)

# Time: 1.15 minutes.
```


```python
Generalized_Gower_Distance_init = GeneralizedGowerDistance(Data=Data, p1=4, p2=3, p3=3, d1='Robust_Mahalanobis', d2='Jaccard', d3='Matching', epsilon=0.05, Method='MAD', alpha=0.1)
D, D_2 = Generalized_Gower_Distance_init.compute(Related_Metric_Scaling=False)

# Time: 1.12 minutes.
```

```python
Generalized_Gower_Distance_init = GeneralizedGowerDistance(Data=Data, p1=4, p2=3, p3=3, d1='Robust_Mahalanobis', d2='Jaccard', d3='Matching', epsilon=0.05, Method='trimmed', alpha=0.1)
D, D_2 = Generalized_Gower_Distance_init.compute(Related_Metric_Scaling=True)

# Time: 1.58 minutes.
```

```python
Generalized_Gower_Distance_init = GeneralizedGowerDistance(Data=Data, p1=4, p2=3, p3=3, d1='Robust_Mahalanobis', d2='Jaccard', d3='Matching', epsilon=0.05, Method='winsorized', alpha=0.1)
D, D_2 = Generalized_Gower_Distance_init.compute(Related_Metric_Scaling=True)

# Time: 1.53 minutes.
```

```python
Generalized_Gower_Distance_init = GeneralizedGowerDistance(Data=Data, p1=4, p2=3, p3=3, d1='Robust_Mahalanobis', d2='Jaccard', d3='Matching', epsilon=0.05, Method='MAD', alpha=0.1)
D, D_2 = Generalized_Gower_Distance_init.compute(Related_Metric_Scaling=True)

# Time: 1.55 minutes.
```

We can compare these times with the one obtained by (simple) Gower distance.

```python
Gower_Dist_Matrix(Data, p1=4, p2=3, p3=3)

# Time: 38 seconds.
```

```python

```

```python

```

# Bibliography

Albarrán, I.,  P. Alonso, and A. Grané  “Profile Identification via Weighted Related Metric Scaling: An Application to Dependent Spanish Children.” Journal of the Royal Statistical Society. Series A, Statistics in Society 178, no. 3 (2015): 593–618. https://doi.org/10.1111/rssa.12084stex:B88856BB540BB0134A72028E02D7B00CBED08217.

Cuadras, C. M., and J. Fortiana. “Chapter 25 - Visualizing Categorical Data with Related Metric Scaling.” In Visualization of Categorical Data, 365–76. Academic Press, 1998. https://doi.org/10.1016/B978-012299045-8/50028-0.

Devlin, S. J., R. Gnanadesikan, and J. R. Kettenring. “Robust Estimation and Outlier Detection with Correlation Coefficients.” Biometrika 62, no. 3 (1975): 531–45. https://doi.org/10.1093/biomet/62.3.531.

Grané, A.,  Manzi G. and S. Salini. "Smart Visualization of Mixed Data". Stats  n.º 4 (2021): 472–485. https://doi.org/10.3390/stats4020029


Gower, J. C. “A General Coefficient of Similarity and Some of Its Properties.” Biometrics 27, no. 4 (1971): 857–71.  https://doi.org/10.2307/2528823.

Gnanadesikan, R. Methods for Statistical Data Analysis of Multivariate Observations. 2nd ed. New York  etc.: : John Wiley and Sons, 1997.

