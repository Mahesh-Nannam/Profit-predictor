
Project
Title:Predicting Company Profit Based on Expenditure and State Information
Background
Grasping the elements that drive a company's profitability is essential for effective strategic planning and decision-making.
Companies distribute their budgets across several categories—such as boosting productivity, managing administrative costs, 
and funding promotional campaigns—anticipating that these investments will enhance their profitability.
The dataset includes information on spending in these different categories for various companies, their locations, and the resulting profit outcomes.
Objective
The dataset consists of the following columns:
Productivity_Exp: Amount spent on productivity-related expenses 
Management_Exp: Amount spent on management-related expenses 
Promotions_Exp: Amount spent on promotional activities 
State: The state in which the company operates.
profit: The profit of the company 
Import Dataset
import pandas as pd 
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
df=pd.read_csv("companies.csv")
df
Productivity_Exp	Management_Exp	Promotions_Exp	State	Profit
0	220349.20	236897.80	521784.10	Texas	242261.83
1	217597.70	251377.59	493898.53	Illinois	241792.06
2	208441.51	201145.55	457934.54	Washington	241050.39
3	199372.41	218671.85	433199.62	Texas	232901.99
4	197107.34	191391.77	416168.42	Washington	216187.94
5	186876.90	199814.71	412861.36	Texas	206991.12
6	189615.46	247198.87	177716.82	Illinois	206122.51
7	185298.13	245530.06	373876.68	Washington	205752.60
8	175542.52	248718.95	361613.29	Texas	202211.77
9	178334.88	208679.17	354981.62	Illinois	199759.96
10	156913.08	210594.11	279160.95	Washington	196121.95
11	155671.96	191790.61	299744.55	Illinois	194259.40
12	148863.75	227320.38	299839.44	Washington	191585.52
13	146992.39	235495.07	302664.93	Illinois	184307.35
14	174943.24	256547.42	306512.92	Washington	182602.65
15	169523.61	222616.84	311776.23	Texas	179917.04
16	133013.11	221597.55	314346.06	Illinois	176992.93
17	149657.16	245077.58	332574.31	Texas	175370.37
18	146749.16	214175.79	344919.57	Washington	174266.90
19	141419.70	253514.11	50000.00	Texas	172776.86
20	131253.86	213867.30	348664.47	Illinois	168474.03
21	133389.47	253773.43	349737.29	Texas	161313.02
22	128994.56	222782.75	353319.26	Washington	160352.25
23	122532.53	205751.03	354768.73	Washington	158733.99
24	132044.01	199281.34	190574.81	Texas	158552.04
25	119664.71	239553.16	187962.62	Illinois	157404.34
26	130328.87	244135.98	184050.07	Washington	155733.54
27	127107.60	227864.55	403183.81	Texas	155008.31
28	121051.52	282645.56	168148.20	Washington	153282.38
29	120605.48	253032.06	157138.38	Texas	151004.64
30	116994.48	215641.28	141131.24	Washington	149937.59
31	116136.38	252701.92	138218.23	Texas	147483.56
32	118408.86	229219.61	96085.25	Illinois	147427.84
33	110493.95	203057.49	264634.81	Washington	146778.92
34	101426.07	257693.92	260797.67	Illinois	146712.80
35	101014.02	185047.44	255517.64	Texas	146479.51
36	83663.76	227056.21	251126.82	Washington	140708.19
37	99069.95	151283.14	247029.42	Illinois	139949.14
38	75229.59	165947.93	235265.10	Texas	131229.06
39	93558.51	182982.09	224999.30	Illinois	131005.76
40	83754.33	218546.05	222795.67	Illinois	128239.91
41	82892.92	184710.77	214470.71	Washington	127798.83
42	78640.93	196189.63	198001.11	Illinois	121498.49
43	70505.73	227382.30	85534.17	Texas	119758.98
44	77177.74	254806.14	78334.72	Illinois	115200.33
45	56000.23	224153.04	51903.93	Texas	114926.08
46	56315.46	215816.21	347114.46	Washington	99490.75
47	55000.00	235426.92	50000.00	Illinois	92559.73
48	55542.05	151743.15	50000.00	Texas	85673.41
49	55000.00	216983.80	95173.06	Illinois	64681.40
df.head()
Productivity_Exp	Management_Exp	Promotions_Exp	State	Profit
0	220349.20	236897.80	521784.10	Texas	242261.83
1	217597.70	251377.59	493898.53	Illinois	241792.06
2	208441.51	201145.55	457934.54	Washington	241050.39
3	199372.41	218671.85	433199.62	Texas	232901.99
4	197107.34	191391.77	416168.42	Washington	216187.94
Intial Checkup
df.info()
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 50 entries, 0 to 49
Data columns (total 5 columns):
 #   Column            Non-Null Count  Dtype  
---  ------            --------------  -----  
 0   Productivity_Exp  50 non-null     float64
 1   Management_Exp    50 non-null     float64
 2   Promotions_Exp    50 non-null     float64
 3   State             50 non-null     object 
 4   Profit            50 non-null     float64
dtypes: float64(4), object(1)
memory usage: 2.1+ KB
df.tail()
Productivity_Exp	Management_Exp	Promotions_Exp	State	Profit
45	56000.23	224153.04	51903.93	Texas	114926.08
46	56315.46	215816.21	347114.46	Washington	99490.75
47	55000.00	235426.92	50000.00	Illinois	92559.73
48	55542.05	151743.15	50000.00	Texas	85673.41
49	55000.00	216983.80	95173.06	Illinois	64681.40
df.describe()
Productivity_Exp	Management_Exp	Promotions_Exp	Profit
count	50.000000	50.000000	50.000000	50.000000
mean	128721.615600	221344.639600	261025.097800	162012.639200
std	45902.256482	28017.802755	122290.310726	40306.180338
min	55000.000000	151283.140000	50000.000000	64681.400000
25%	94936.370000	203730.875000	179300.132500	140138.902500
50%	128051.080000	222699.795000	262716.240000	157978.190000
75%	156602.800000	244842.180000	349469.085000	189765.977500
max	220349.200000	282645.560000	521784.100000	242261.830000
Data Visualization
df.shape
#2.Draw the kdeplot using Productivity_Exp
sns.kdeplot(data=df,x="Productivity_Exp")
C:\Users\KOUSHIK\anaconda3\Lib\site-packages\seaborn\_oldcore.py:1119: FutureWarning: use_inf_as_na option is deprecated and will be removed in a future version. Convert inf values to NaN before operating instead.
  with pd.option_context('mode.use_inf_as_na', True):
<Axes: xlabel='Productivity_Exp', ylabel='Density'>

data = pd.get_dummies(df,columns=['State'], drop_first=False)
data.head()
Productivity_Exp	Management_Exp	Promotions_Exp	Profit	State_Illinois	State_Texas	State_Washington
0	220349.20	236897.80	521784.10	242261.83	False	True	False
1	217597.70	251377.59	493898.53	241792.06	True	False	False
2	208441.51	201145.55	457934.54	241050.39	False	False	True
3	199372.41	218671.85	433199.62	232901.99	False	True	False
4	197107.34	191391.77	416168.42	216187.94	False	False	True
Correleation
data.corr()
Productivity_Exp	Management_Exp	Promotions_Exp	Profit	State_Illinois	State_Texas	State_Washington
Productivity_Exp	1.000000	0.241955	0.724248	0.972900	-0.143165	0.039068	0.105711
Management_Exp	0.241955	1.000000	-0.032154	0.200717	-0.015478	0.005145	0.010493
Promotions_Exp	0.724248	-0.032154	1.000000	0.747766	-0.168875	-0.033670	0.205685
Profit	0.972900	0.200717	0.747766	1.000000	-0.145837	0.031368	0.116244
State_Illinois	-0.143165	-0.015478	-0.168875	-0.145837	1.000000	-0.515152	-0.492366
State_Texas	0.039068	0.005145	-0.033670	0.031368	-0.515152	1.000000	-0.492366
State_Washington	0.105711	0.010493	0.205685	0.116244	-0.492366	-0.492366	1.000000
data1=data.drop(columns=['Profit'])
data1.tail()
Productivity_Exp	Management_Exp	Promotions_Exp	State_Illinois	State_Texas	State_Washington
45	56000.23	224153.04	51903.93	False	True	False
46	56315.46	215816.21	347114.46	False	False	True
47	55000.00	235426.92	50000.00	True	False	False
48	55542.05	151743.15	50000.00	False	True	False
49	55000.00	216983.80	95173.06	True	False	False
data1.head()
Productivity_Exp	Management_Exp	Promotions_Exp	State_Illinois	State_Texas	State_Washington
0	220349.20	236897.80	521784.10	False	True	False
1	217597.70	251377.59	493898.53	True	False	False
2	208441.51	201145.55	457934.54	False	False	True
3	199372.41	218671.85	433199.62	False	True	False
4	197107.34	191391.77	416168.42	False	False	True
data2=data.iloc[:,3:4]
data2.head()
Profit
0	242261.83
1	241792.06
2	241050.39
3	232901.99
4	216187.94
Train test split
from sklearn.model_selection import train_test_split
x_train,x_test,y_train,y_test=train_test_split(data1,data2,test_size=0.2,random_state=2)
x_train.head()
Productivity_Exp	Management_Exp	Promotions_Exp	State_Illinois	State_Texas	State_Washington
24	132044.01	199281.34	190574.81	False	True	False
48	55542.05	151743.15	50000.00	False	True	False
17	149657.16	245077.58	332574.31	False	True	False
12	148863.75	227320.38	299839.44	False	False	True
27	127107.60	227864.55	403183.81	False	True	False
x_test.head()
Productivity_Exp	Management_Exp	Promotions_Exp	State_Illinois	State_Texas	State_Washington
36	83663.76	227056.21	251126.82	False	False	True
47	55000.00	235426.92	50000.00	True	False	False
28	121051.52	282645.56	168148.20	False	False	True
9	178334.88	208679.17	354981.62	True	False	False
13	146992.39	235495.07	302664.93	True	False	False
x_train.shape
(40, 6)
x_test.shape
(10, 6)
from sklearn.linear_model import LinearRegression
lr=LinearRegression()
x_train.head()
Productivity_Exp	Management_Exp	Promotions_Exp	State_Illinois	State_Texas	State_Washington
24	132044.01	199281.34	190574.81	False	True	False
48	55542.05	151743.15	50000.00	False	True	False
17	149657.16	245077.58	332574.31	False	True	False
12	148863.75	227320.38	299839.44	False	False	True
27	127107.60	227864.55	403183.81	False	True	False
y_train.head()

Import Linear regression
lr.fit(x_train,y_train)
LinearRegression()
In a Jupyter environment, please rerun this cell to show the HTML representation or trust the notebook.
On GitHub, the HTML representation is unable to render, please try loading this page with nbviewer.org.
x_test
Productivity_Exp	Management_Exp	Promotions_Exp	State_Illinois	State_Texas	State_Washington
36	83663.76	227056.21	251126.82	False	False	True
47	55000.00	235426.92	50000.00	True	False	False
28	121051.52	282645.56	168148.20	False	False	True
9	178334.88	208679.17	354981.62	True	False	False
13	146992.39	235495.07	302664.93	True	False	False
0	220349.20	236897.80	521784.10	False	True	False
44	77177.74	254806.14	78334.72	True	False	False
46	56315.46	215816.21	347114.46	False	False	True
39	93558.51	182982.09	224999.30	True	False	False
23	122532.53	205751.03	354768.73	False	False	True
lr.predict([[56315,215816.61,347114,0,0,1]])
C:\Users\PC\anaconda3\Lib\site-packages\sklearn\base.py:439: UserWarning: X does not have valid feature names, but LinearRegression was fitted with feature names
  warnings.warn(
array([[104934.73902582]])
y_test
Profit
36	140708.19
47	92559.73
28	153282.38
9	199759.96
13	184307.35
0	242261.83
44	115200.33
46	99490.75
39	131005.76
23	158733.99
from sklearn .metrics import mean_absolute_error,mean_squared_error,r2_score
y_pred=lr.predict(x_test)
y_pred
array([[124061.28471146],
       [ 96009.23798771],
       [149637.26360778],
       [205786.53229364],
       [177636.76349543],
       [242765.18597815],
       [113906.99972437],
       [104935.14415875],
       [134532.35238001],
       [159460.29711996]])
y_test.values

Mean Error
mean_absolute_error(y_test,y_pred)
4793.2668379191
mean_squared_error(y_test,y_pred)
42765360.65268925
Conclusion
The goal of this analysis is to build a predictive model that can accurately forecast a company's profit based on its expenditures in
productivity,management,and promotions,as well as its state of operation.
Insights
1.Importing data set
2.Data visualization
3.Linear regression model
4.Correlation
5.Train_test_split
6.Mean Error
