#Machine learning

##Supervised vs unsupervised
- input feature output result
- Supervised: yes or no

##EDA
- Exploratory Data analysis is the first step in the data science process
- to understand dataset better
- to check features and shape
- to validate some hypothesis that you have in MiniCassandra
- to have a preliminary idea

##Dimensionality Reduction
###Principal component analysis(PCA)
- Principal component analysis (PCA) is a statistical procedure that uses an orthogonal transformation(正交变换) to convert a set of observations of possibly correlated variables (entities each of which takes on various numerical values) into a set of values of linearly uncorrelated variables called principal component
- 筛选出不必要的data,减少Noise
- 1.可以跳出几个相似的变量进行group. 2.通过正交,排序,选出关系很小的可以忽略掉的,减少PC.
- 特点:正交,排序
- centering -> rotating -> orthogonal transformation
- 使用欧式距离, 要求data必须standardize

///正交算出core relation, 如果一个core relation跟其他的component特别小,那么可以进行降维

###How any PCs are needed?
- A common rule of thumb when PCA is based on correlations is that axes with eigenvalues > 1(or 0.7)
- Assumes relationships among variables are LINEAR
- we can try use kernel PCA to mock linear

vic.da09@gmail.com
