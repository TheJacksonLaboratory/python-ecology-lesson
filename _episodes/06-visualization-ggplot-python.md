---
title: Plotting with ggplot
teaching: 0
exercises: 0
objectives:
    - Be able to create a ggplot object
    - Be able to set universal plot settings
    - Be able to modify an existing ggplot object
    - Be able to change the aesthetics of a plot such as colour
    - Be able to edit the axis labels
    - Know how to use a step-by-step approach to build complex plots
    - Be able to create, scatter plots, box plots and time series plots
    - Use the `facet_wrap` and `facet_grid` commands to create a collection of plots splitting the data by a factor variable
    - Be able to create customized plot styles to meet their needs
---
## Data Download
- [surveys_complete.csv](https://raw.githubusercontent.com/TheJacksonLaboratory/python-ecology-lesson/gh-pages/data_output/surveys_complete.csv)

## Disclaimer

Python has powerful built-in plotting capabilities such as `matplotlib`, but
for this exercise, we will be using the [`ggplot`](http://ggplot.yhathq.com/)
package, which facilitates the creation of highly-informative plots of
structured data based on the R implementation of
[`ggplot2`](http://ggplot2.org/) and [The Grammar of
Graphics](http://link.springer.com/book/10.1007%2F0-387-28695-0) by Leland
Wilkinson.



```python
import pandas as pd

surveys_complete = pd.read_csv('http://bit.ly/2nHHLz3', index_col=0)

# OR

surveys_complete = pd.read_csv('surveys_complete.csv', index_col=0)

surveys_complete.index.name = 'X'
surveys_complete
```


<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>record_id</th>
      <th>month</th>
      <th>day</th>
      <th>year</th>
      <th>plot_id</th>
      <th>species_id</th>
      <th>sex</th>
      <th>hindfoot_length</th>
      <th>weight</th>
      <th>genus</th>
      <th>species</th>
      <th>taxa</th>
      <th>plot_type</th>
    </tr>
    <tr>
      <th>X</th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1</th>
      <td>845</td>
      <td>5</td>
      <td>6</td>
      <td>1978</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>32</td>
      <td>204</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1164</td>
      <td>8</td>
      <td>5</td>
      <td>1978</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>34</td>
      <td>199</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1261</td>
      <td>9</td>
      <td>4</td>
      <td>1978</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>32</td>
      <td>197</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1756</td>
      <td>4</td>
      <td>29</td>
      <td>1979</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>33</td>
      <td>166</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1818</td>
      <td>5</td>
      <td>30</td>
      <td>1979</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>32</td>
      <td>184</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1882</td>
      <td>7</td>
      <td>4</td>
      <td>1979</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>32</td>
      <td>206</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2133</td>
      <td>10</td>
      <td>25</td>
      <td>1979</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>33</td>
      <td>274</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2184</td>
      <td>11</td>
      <td>17</td>
      <td>1979</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>30</td>
      <td>186</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2406</td>
      <td>1</td>
      <td>16</td>
      <td>1980</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>33</td>
      <td>184</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>10</th>
      <td>3000</td>
      <td>5</td>
      <td>18</td>
      <td>1980</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>31</td>
      <td>87</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>11</th>
      <td>3002</td>
      <td>5</td>
      <td>18</td>
      <td>1980</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>33</td>
      <td>174</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>12</th>
      <td>4667</td>
      <td>7</td>
      <td>8</td>
      <td>1981</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>30</td>
      <td>130</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>13</th>
      <td>4859</td>
      <td>10</td>
      <td>1</td>
      <td>1981</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>34</td>
      <td>208</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>14</th>
      <td>5048</td>
      <td>11</td>
      <td>23</td>
      <td>1981</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>34</td>
      <td>192</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>15</th>
      <td>5299</td>
      <td>1</td>
      <td>25</td>
      <td>1982</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>32</td>
      <td>165</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>16</th>
      <td>5485</td>
      <td>2</td>
      <td>24</td>
      <td>1982</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>34</td>
      <td>202</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>17</th>
      <td>5558</td>
      <td>3</td>
      <td>29</td>
      <td>1982</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>33</td>
      <td>211</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>18</th>
      <td>5583</td>
      <td>3</td>
      <td>29</td>
      <td>1982</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>31</td>
      <td>120</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>19</th>
      <td>5966</td>
      <td>5</td>
      <td>22</td>
      <td>1982</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>32</td>
      <td>40</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>20</th>
      <td>6020</td>
      <td>6</td>
      <td>28</td>
      <td>1982</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>33</td>
      <td>222</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>21</th>
      <td>6023</td>
      <td>6</td>
      <td>28</td>
      <td>1982</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>30</td>
      <td>100</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>22</th>
      <td>6036</td>
      <td>6</td>
      <td>28</td>
      <td>1982</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>33</td>
      <td>120</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>23</th>
      <td>6479</td>
      <td>8</td>
      <td>16</td>
      <td>1982</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>31</td>
      <td>112</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>24</th>
      <td>6500</td>
      <td>8</td>
      <td>16</td>
      <td>1982</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>33</td>
      <td>152</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>25</th>
      <td>8022</td>
      <td>6</td>
      <td>18</td>
      <td>1983</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>30</td>
      <td>126</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>26</th>
      <td>8263</td>
      <td>8</td>
      <td>16</td>
      <td>1983</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>32</td>
      <td>147</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>27</th>
      <td>8387</td>
      <td>9</td>
      <td>11</td>
      <td>1983</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>32</td>
      <td>138</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>28</th>
      <td>8394</td>
      <td>9</td>
      <td>11</td>
      <td>1983</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>32</td>
      <td>161</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>29</th>
      <td>8407</td>
      <td>9</td>
      <td>11</td>
      <td>1983</td>
      <td>2</td>
      <td>NL</td>
      <td>M</td>
      <td>33</td>
      <td>148</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>30</th>
      <td>8514</td>
      <td>10</td>
      <td>16</td>
      <td>1983</td>
      <td>2</td>
      <td>NL</td>
      <td>F</td>
      <td>32</td>
      <td>151</td>
      <td>Neotoma</td>
      <td>albigula</td>
      <td>Rodent</td>
      <td>Control</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>30434</th>
      <td>28588</td>
      <td>9</td>
      <td>20</td>
      <td>1998</td>
      <td>7</td>
      <td>PM</td>
      <td>F</td>
      <td>19</td>
      <td>26</td>
      <td>Peromyscus</td>
      <td>maniculatus</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30435</th>
      <td>28589</td>
      <td>9</td>
      <td>20</td>
      <td>1998</td>
      <td>7</td>
      <td>PM</td>
      <td>F</td>
      <td>20</td>
      <td>17</td>
      <td>Peromyscus</td>
      <td>maniculatus</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30436</th>
      <td>28590</td>
      <td>9</td>
      <td>20</td>
      <td>1998</td>
      <td>7</td>
      <td>PM</td>
      <td>F</td>
      <td>20</td>
      <td>17</td>
      <td>Peromyscus</td>
      <td>maniculatus</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30437</th>
      <td>28668</td>
      <td>10</td>
      <td>24</td>
      <td>1998</td>
      <td>7</td>
      <td>PM</td>
      <td>F</td>
      <td>20</td>
      <td>25</td>
      <td>Peromyscus</td>
      <td>maniculatus</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30438</th>
      <td>28805</td>
      <td>11</td>
      <td>21</td>
      <td>1998</td>
      <td>7</td>
      <td>PM</td>
      <td>M</td>
      <td>20</td>
      <td>13</td>
      <td>Peromyscus</td>
      <td>maniculatus</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30439</th>
      <td>29489</td>
      <td>4</td>
      <td>17</td>
      <td>1999</td>
      <td>7</td>
      <td>PM</td>
      <td>M</td>
      <td>21</td>
      <td>21</td>
      <td>Peromyscus</td>
      <td>maniculatus</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30440</th>
      <td>15946</td>
      <td>4</td>
      <td>2</td>
      <td>1989</td>
      <td>7</td>
      <td>RF</td>
      <td>M</td>
      <td>17</td>
      <td>11</td>
      <td>Reithrodontomys</td>
      <td>fulvescens</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30441</th>
      <td>16652</td>
      <td>11</td>
      <td>4</td>
      <td>1989</td>
      <td>7</td>
      <td>RF</td>
      <td>F</td>
      <td>18</td>
      <td>15</td>
      <td>Reithrodontomys</td>
      <td>fulvescens</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30442</th>
      <td>25710</td>
      <td>5</td>
      <td>10</td>
      <td>1997</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>26</td>
      <td>31</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30443</th>
      <td>26042</td>
      <td>6</td>
      <td>10</td>
      <td>1997</td>
      <td>7</td>
      <td>PB</td>
      <td>F</td>
      <td>27</td>
      <td>24</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30444</th>
      <td>26096</td>
      <td>6</td>
      <td>10</td>
      <td>1997</td>
      <td>7</td>
      <td>PB</td>
      <td>F</td>
      <td>26</td>
      <td>30</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30445</th>
      <td>26356</td>
      <td>7</td>
      <td>9</td>
      <td>1997</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>27</td>
      <td>32</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30446</th>
      <td>26475</td>
      <td>7</td>
      <td>9</td>
      <td>1997</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>28</td>
      <td>36</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30447</th>
      <td>26546</td>
      <td>7</td>
      <td>29</td>
      <td>1997</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>27</td>
      <td>37</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30448</th>
      <td>26776</td>
      <td>9</td>
      <td>27</td>
      <td>1997</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>26</td>
      <td>37</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30449</th>
      <td>26819</td>
      <td>9</td>
      <td>27</td>
      <td>1997</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>30</td>
      <td>40</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30450</th>
      <td>28332</td>
      <td>8</td>
      <td>22</td>
      <td>1998</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>26</td>
      <td>27</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30451</th>
      <td>28336</td>
      <td>8</td>
      <td>22</td>
      <td>1998</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>26</td>
      <td>23</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30452</th>
      <td>28337</td>
      <td>8</td>
      <td>22</td>
      <td>1998</td>
      <td>7</td>
      <td>PB</td>
      <td>F</td>
      <td>27</td>
      <td>30</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30453</th>
      <td>28338</td>
      <td>8</td>
      <td>22</td>
      <td>1998</td>
      <td>7</td>
      <td>PB</td>
      <td>F</td>
      <td>25</td>
      <td>23</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30454</th>
      <td>28585</td>
      <td>9</td>
      <td>20</td>
      <td>1998</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>26</td>
      <td>25</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30455</th>
      <td>28667</td>
      <td>10</td>
      <td>24</td>
      <td>1998</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>26</td>
      <td>25</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30456</th>
      <td>29231</td>
      <td>2</td>
      <td>20</td>
      <td>1999</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>26</td>
      <td>28</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30457</th>
      <td>30355</td>
      <td>2</td>
      <td>5</td>
      <td>2000</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>27</td>
      <td>20</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30458</th>
      <td>32085</td>
      <td>5</td>
      <td>26</td>
      <td>2001</td>
      <td>7</td>
      <td>PB</td>
      <td>F</td>
      <td>22</td>
      <td>37</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30459</th>
      <td>32477</td>
      <td>8</td>
      <td>25</td>
      <td>2001</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>28</td>
      <td>32</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30460</th>
      <td>33103</td>
      <td>11</td>
      <td>17</td>
      <td>2001</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>28</td>
      <td>41</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30461</th>
      <td>33305</td>
      <td>12</td>
      <td>15</td>
      <td>2001</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>29</td>
      <td>44</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30462</th>
      <td>34524</td>
      <td>7</td>
      <td>13</td>
      <td>2002</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>25</td>
      <td>16</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
    <tr>
      <th>30463</th>
      <td>35382</td>
      <td>12</td>
      <td>8</td>
      <td>2002</td>
      <td>7</td>
      <td>PB</td>
      <td>M</td>
      <td>26</td>
      <td>30</td>
      <td>Chaetodipus</td>
      <td>baileyi</td>
      <td>Rodent</td>
      <td>Rodent Exclosure</td>
    </tr>
  </tbody>
</table>
<p>30463 rows × 13 columns</p>
</div>


We will make the same plot using the `ggplot` package.

`ggplot` is a plotting package that makes it simple to create complex plots
from data in a dataframe. It uses default settings, which help creating
publication quality plots with a minimal amount of settings and tweaking.

ggplot graphics are built step by step by adding new elements.

To build a ggplot we need to:

- bind the plot to a specific data frame using the `data` argument


- define aesthetics (`aes`), by selecting the variables to be plotted and the variables to define the presentation
     such as plotting size, shape color, etc.,








```python
%matplotlib inline
from ggplot import *
```


# Plotting with ggplot

```python
ggplot( aesthetics= aes(x = 'weight', y = 'hindfoot_length'), data = surveys_complete)
```


![png](../fig/output_6_0.png)





    <ggplot: (-9223372036552543572)>




- add `geoms` -- graphical representation of the data in the plot (points,
     lines, bars). To add a geom to the plot use `+` operator:




```python
ggplot( aes(x = 'weight', y = 'hindfoot_length'), data = surveys_complete) + geom_point()
```


![png](../fig/output_8_0.png)





    <ggplot: (295366541)>




The `+` in the `ggplot2` package is particularly useful because it allows you
to modify existing `ggplot` objects. This means you can easily set up plot
"templates" and conveniently explore different types of plots, so the above
plot can also be generated with code like this:




```python
# Create
surveys_plot = ggplot( aes(x = 'weight', y = 'hindfoot_length'), data = surveys_complete)

# Draw the plot
surveys_plot + geom_point()
```


![png](../fig/output_10_0.png)





    <ggplot: (295593725)>




Notes:

- Anything you put in the `ggplot()` function can be seen by any geom layers
  that you add (i.e., these are universal plot settings). This includes the x and
  y axis you set up in `aes()`.
- You can also specify aesthetics for a given geom independently of the
  aesthetics defined globally in the `ggplot()` function.


# Building your plots iteratively

Building plots with ggplot is typically an iterative process. We start by
defining the dataset we'll use, lay the axes, and choose a geom.




```python
ggplot(aes(x = 'weight', y = 'hindfoot_length'), data = surveys_complete, ) + geom_point()
```


![png](../fig/output_12_0.png)




Then, we start modifying this plot to extract more information from it. For
instance, we can add transparency (alpha) to avoid overplotting.




```python
ggplot(aes(x = 'weight', y = 'hindfoot_length'), data = surveys_complete) + \
    geom_point(alpha = 0.1)
```


![png](../fig/output_14_0.png)





    <ggplot: (295894448)>




We can also add colors for all the points




```python
ggplot(aes(x = 'weight', y = 'hindfoot_length'),data = surveys_complete) + \
    geom_point(alpha = 0.1, color = "blue")
```


![png](../fig/output_16_0.png)

Or to color each species in the plot differently:




```python
ggplot(aes(x = 'weight', y = 'hindfoot_length', color='species_id'),data = surveys_complete) + \
    geom_point( alpha = 0.1)
```


![png](../fig/output_18_0.png)





    <ggplot: (295600781)>




# Challenge

Visualising the distribution of `weight` and `hindfoot_length` within each species.


```python
ggplot( aes(x = 'species_id', y = 'hindfoot_length'), data = surveys_complete) + geom_boxplot()
```


![png](../fig/output_21_0.png)

> Boxplots are useful summaries, but hide the *shape* of the distribution. For
> example, if there is a bimodal distribution, this would not be observed with a
> boxplot. An alternative to the boxplot is the violin plot (sometimes known as a
> beanplot), where the shape (of the density of points) is drawn.
>
> - Vizualize the distribution of `weight` within each species (`species_id`). Create a boxplot to visualize the data. remember to add the title and lables
> - Replace the box plot with a violin plot; see `geom_violin()`
>
> In many types of data, it is important to consider the *scale* of the
> observations.  For example, it may be worth changing the scale of the axis to
> better distribute the observations in the space of the plot.  Changing the scale
> of the axes is done similarly to adding/modifying other components (i.e., by
> incrementally adding commands).
>
> - Represent weight on the log10 scale; see `scale_y_log(base=10)`



```python
## Challenges:
##  1. Vizualize the distribution of `weight` within each species (`species_id`). 
##       Create a boxplot to visualize the data. remember to add the title and lables
ggplot( aes(x = 'species_id', y = 'weight'), data = surveys_complete) + \
     geom_boxplot() + \
     xlab('species_id') + \
     ylab('weights') + \
     ggtitle('weights distribution per species')
```


```python
## Challenges:
##  2. Replace the box plot with a violin plot; see `geom_violin()`.

ggplot( aes(x = 'species_id', y = 'weight'), data = surveys_complete) + \
     geom_violin() + \
     xlab('species_id') + \
     ylab('weights') + \
     ggtitle('weights distribution per species')
```


```python
## Challenges:
##  3. Represent weight on the log10 scale; see `scale_y_log()`.
ggplot( aes(x = 'species_id', y = 'weight'), data = surveys_complete) + \
     geom_violin() + \
     xlab('species_id') + \
     ylab('weights base 10') + \
     ggtitle('weights distribution per species') +\
     scale_y_log(base=10)
```



# Plotting time series data

Let's calculate number of counts per year for each species. To do that we need
to group data first and count records within each group.



```python
yearly_counts = surveys_complete[['year','species_id','species']].groupby(['year', 'species_id']).count().reset_index()
yearly_counts.columns = ['year','species_id', 'n']
yearly_counts
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year</th>
      <th>species_id</th>
      <th>n</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1977</td>
      <td>DM</td>
      <td>181</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1977</td>
      <td>DO</td>
      <td>12</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1977</td>
      <td>DS</td>
      <td>29</td>
    </tr>
    <tr>
      <th>3</th>
      <td>1977</td>
      <td>OL</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>1977</td>
      <td>PE</td>
      <td>2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>1977</td>
      <td>PF</td>
      <td>22</td>
    </tr>
    <tr>
      <th>6</th>
      <td>1977</td>
      <td>PP</td>
      <td>3</td>
    </tr>
    <tr>
      <th>7</th>
      <td>1977</td>
      <td>RM</td>
      <td>2</td>
    </tr>
    <tr>
      <th>8</th>
      <td>1978</td>
      <td>DM</td>
      <td>336</td>
    </tr>
    <tr>
      <th>9</th>
      <td>1978</td>
      <td>DO</td>
      <td>21</td>
    </tr>
    <tr>
      <th>10</th>
      <td>1978</td>
      <td>DS</td>
      <td>272</td>
    </tr>
    <tr>
      <th>11</th>
      <td>1978</td>
      <td>NL</td>
      <td>23</td>
    </tr>
    <tr>
      <th>12</th>
      <td>1978</td>
      <td>OL</td>
      <td>35</td>
    </tr>
    <tr>
      <th>13</th>
      <td>1978</td>
      <td>OT</td>
      <td>45</td>
    </tr>
    <tr>
      <th>14</th>
      <td>1978</td>
      <td>PE</td>
      <td>12</td>
    </tr>
    <tr>
      <th>15</th>
      <td>1978</td>
      <td>PF</td>
      <td>33</td>
    </tr>
    <tr>
      <th>16</th>
      <td>1978</td>
      <td>PM</td>
      <td>2</td>
    </tr>
    <tr>
      <th>17</th>
      <td>1978</td>
      <td>PP</td>
      <td>23</td>
    </tr>
    <tr>
      <th>18</th>
      <td>1978</td>
      <td>RM</td>
      <td>2</td>
    </tr>
    <tr>
      <th>19</th>
      <td>1978</td>
      <td>SH</td>
      <td>1</td>
    </tr>
    <tr>
      <th>20</th>
      <td>1979</td>
      <td>DM</td>
      <td>183</td>
    </tr>
    <tr>
      <th>21</th>
      <td>1979</td>
      <td>DO</td>
      <td>28</td>
    </tr>
    <tr>
      <th>22</th>
      <td>1979</td>
      <td>DS</td>
      <td>183</td>
    </tr>
    <tr>
      <th>23</th>
      <td>1979</td>
      <td>NL</td>
      <td>30</td>
    </tr>
    <tr>
      <th>24</th>
      <td>1979</td>
      <td>OL</td>
      <td>43</td>
    </tr>
    <tr>
      <th>25</th>
      <td>1979</td>
      <td>OT</td>
      <td>63</td>
    </tr>
    <tr>
      <th>26</th>
      <td>1979</td>
      <td>PE</td>
      <td>16</td>
    </tr>
    <tr>
      <th>27</th>
      <td>1979</td>
      <td>PF</td>
      <td>16</td>
    </tr>
    <tr>
      <th>28</th>
      <td>1979</td>
      <td>PM</td>
      <td>6</td>
    </tr>
    <tr>
      <th>29</th>
      <td>1979</td>
      <td>PP</td>
      <td>19</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>262</th>
      <td>2000</td>
      <td>OT</td>
      <td>145</td>
    </tr>
    <tr>
      <th>263</th>
      <td>2000</td>
      <td>PB</td>
      <td>545</td>
    </tr>
    <tr>
      <th>264</th>
      <td>2000</td>
      <td>PE</td>
      <td>13</td>
    </tr>
    <tr>
      <th>265</th>
      <td>2000</td>
      <td>PM</td>
      <td>2</td>
    </tr>
    <tr>
      <th>266</th>
      <td>2000</td>
      <td>PP</td>
      <td>368</td>
    </tr>
    <tr>
      <th>267</th>
      <td>2000</td>
      <td>RM</td>
      <td>15</td>
    </tr>
    <tr>
      <th>268</th>
      <td>2000</td>
      <td>SH</td>
      <td>7</td>
    </tr>
    <tr>
      <th>269</th>
      <td>2001</td>
      <td>DM</td>
      <td>292</td>
    </tr>
    <tr>
      <th>270</th>
      <td>2001</td>
      <td>DO</td>
      <td>77</td>
    </tr>
    <tr>
      <th>271</th>
      <td>2001</td>
      <td>NL</td>
      <td>44</td>
    </tr>
    <tr>
      <th>272</th>
      <td>2001</td>
      <td>OT</td>
      <td>153</td>
    </tr>
    <tr>
      <th>273</th>
      <td>2001</td>
      <td>PB</td>
      <td>520</td>
    </tr>
    <tr>
      <th>274</th>
      <td>2001</td>
      <td>PE</td>
      <td>35</td>
    </tr>
    <tr>
      <th>275</th>
      <td>2001</td>
      <td>PF</td>
      <td>26</td>
    </tr>
    <tr>
      <th>276</th>
      <td>2001</td>
      <td>PM</td>
      <td>3</td>
    </tr>
    <tr>
      <th>277</th>
      <td>2001</td>
      <td>PP</td>
      <td>258</td>
    </tr>
    <tr>
      <th>278</th>
      <td>2001</td>
      <td>RM</td>
      <td>15</td>
    </tr>
    <tr>
      <th>279</th>
      <td>2001</td>
      <td>SH</td>
      <td>9</td>
    </tr>
    <tr>
      <th>280</th>
      <td>2002</td>
      <td>DM</td>
      <td>302</td>
    </tr>
    <tr>
      <th>281</th>
      <td>2002</td>
      <td>DO</td>
      <td>243</td>
    </tr>
    <tr>
      <th>282</th>
      <td>2002</td>
      <td>NL</td>
      <td>42</td>
    </tr>
    <tr>
      <th>283</th>
      <td>2002</td>
      <td>OL</td>
      <td>7</td>
    </tr>
    <tr>
      <th>284</th>
      <td>2002</td>
      <td>OT</td>
      <td>119</td>
    </tr>
    <tr>
      <th>285</th>
      <td>2002</td>
      <td>PB</td>
      <td>868</td>
    </tr>
    <tr>
      <th>286</th>
      <td>2002</td>
      <td>PE</td>
      <td>57</td>
    </tr>
    <tr>
      <th>287</th>
      <td>2002</td>
      <td>PF</td>
      <td>18</td>
    </tr>
    <tr>
      <th>288</th>
      <td>2002</td>
      <td>PM</td>
      <td>1</td>
    </tr>
    <tr>
      <th>289</th>
      <td>2002</td>
      <td>PP</td>
      <td>375</td>
    </tr>
    <tr>
      <th>290</th>
      <td>2002</td>
      <td>RM</td>
      <td>20</td>
    </tr>
    <tr>
      <th>291</th>
      <td>2002</td>
      <td>SH</td>
      <td>9</td>
    </tr>
  </tbody>
</table>
<p>292 rows × 3 columns</p>
</div>




Timelapse data can be visualised as a line plot with years on x axis and counts
on y axis.




```python
ggplot(aes(x = 'year', y = 'n'),data = yearly_counts) + \
     geom_line()
```


![png](../fig/output_35_0.png)





    <ggplot: (-9223372036580461736)>




Unfortunately this does not work, because we plot data for all the species
together. We need to tell ggplot to draw a line for each species by modifying
the aesthetic function to include `group = species_id`.



```python
ggplot(aes(x = 'year', y = 'n', group='species_id'),data = yearly_counts) + geom_line()
```


We will be able to distinguish species in the plot if we add colors.


```python
ggplot(aes(x = 'year', y = 'n', color='species_id'),data = yearly_counts) + geom_line()
```


# Faceting

ggplot has a special technique called *faceting* that allows to split one plot
into multiple plots based on a factor included in the dataset. We will use it to
make one plot for a time series for each species.


```python
ggplot(aes(x = "year", y = "n", colour = "species_id"),data = yearly_counts) + \
    geom_line() + \
    facet_wrap("species_id")
    
```


Now we would like to split line in each plot by sex of each individual
measured. To do that we need to make counts in data frame grouped by year,
species_id, and sex:


```python
yearly_sex_counts = surveys_complete.groupby( ['year','species_id', 'sex']).count()
yearly_sex_counts['n']  = yearly_sex_counts['record_id']
yearly_sex_counts = yearly_sex_counts['n'].reset_index()
yearly_sex_counts
```


We can now make the faceted plot splitting further by sex (within a single plot):



```python
 ggplot(aes(x = "year", y = "n", color = "species_id", group = "sex"), data = yearly_sex_counts, ) + \
     geom_line() + \
         facet_wrap( "species_id")
```


Usually plots with white background look more readable when printed.  We can set
the background to white using the function `theme_bw()`. Additionally you can also remove
the grid.



```python
 ggplot(aes(x = "year", y = "n", color = "species_id", group = "sex"),data = yearly_sex_counts ) + \
     geom_line() + \
            facet_wrap( "species_id") + \
                theme_bw() + \
                theme()
```


To make the plot easier to read, we can color by sex instead of species (species
are already in separate plots, so we don't need to distinguish them further).


```python
ggplot(aes(x = "year", y = "n", color = "sex", group = "sex"), data = yearly_sex_counts) + \
    geom_line() + \
    facet_wrap("species_id") + \
    theme_bw() 
```



# Challenge

> Use what you just learned to create a plot that depicts how the average weight
> of each species changes through the years.

<!-- Answer

```python
yearly_weight = surveys_complete[["year", "species_id","weight"]].groupby(["year", "species_id"]).mean().reset_index()
yearly_weight.columns =   ["year", "species_id","avg_weight"]  
yearly_weight
```


```python
ggplot( aes(x="year", y="avg_weight", color = "species_id", group = "species_id"),data = yearly_weight) + \
    geom_line() + \
    facet_wrap("species_id") + \
    theme_bw()
```

-->




```python
## Plotting time series challenge:
##  Use what you just learned to create a plot that depicts how the
##  average weight of each species changes through the years.

```


The `facet_wrap` geometry extracts plots into an arbitrary number of dimensions
to allow them to cleanly fit on one page. On the other hand, the `facet_grid`
geometry allows you to explicitly specify how you want your plots to be
arranged via formula notation (`rows ~ columns`; a `.` can be used as
a placeholder that indicates only one row or column).

Let's modify the previous plot to compare how the weights of male and females
has changed through time.



```python
## One column, facet by rows
yearly_sex_weight = surveys_complete[
    ['year','sex','species_id','weight']].groupby(
    ["year", "sex", "species_id"]).mean().reset_index()
yearly_sex_weight.columns = ['year','sex','species_id','avg_weight']
yearly_sex_weight
```

```python
ggplot( aes(x="year", y="avg_weight", color = "species_id", group = "species_id"),data = yearly_sex_weight) + \
    geom_line() + \
    facet_grid("sex")
```


```python
# One row, facet by column
ggplot(data = yearly_sex_weight, aes(x=year, y=avg_weight, color = species_id, group = species_id)) +
    geom_line() +
    facet_grid(. ~ sex)
```


```python
# One row, facet by column
ggplot( aes(x="year", y="avg_weight", color = "species_id", group = "species_id"),data = yearly_sex_weight) + \
    geom_line() + \
    facet_grid(None, "sex")
```


# Customization

Take a look at the ggplot2 cheat sheet
(https://www.rstudio.com/wp-content/uploads/2015/08/ggplot2-cheatsheet.pdf), and
think of ways to improve the plot. You can write down some of your ideas as
comments in the Etherpad.

Now, let's change names of axes to something more informative than 'year'
and 'n' and add a title to this figure:


```python
ggplot( aes(x = "year", y = "n", color = "sex", group = "sex"),data = yearly_sex_counts) + \
    geom_line() + \
    facet_wrap( "species_id" ) + \
    labs(title = 'Observed species in time',
         x = 'Year of observation',
         y = 'Number of species') + \
    theme_bw() 
```


The axes have more informative names, but their readability can be improved by
increasing the font size. While we are at it, we'll also change the font family:



```python
ggplot( aes(x = "year", y = "n", color = "sex", group = "sex"),data = yearly_sex_counts) + \
    geom_line() + \
    facet_wrap( "species_id" ) + \
    theme_bw() + \
    theme(axis_title_x = element_text(size=16, family="Arial"),
         axis_title_y = element_text(size=16, family="Arial")) + \
    labs(title = 'Observed species in time',
        x = 'Year of observation',
        y = 'Number of species')
```


After our manipulations we notice that the values on the x-axis are still not
properly readable. Let's change the orientation of the labels and adjust them
vertically and horizontally so they don't overlap. You can use a 90 degree
angle, or experiment to find the appropriate angle for diagonally oriented
labels.


```python
ggplot( aes(x = "year", y = "n", color = "sex", group = "sex"),data = yearly_sex_counts) + \
    geom_line() + \
    facet_wrap( "species_id" ) + \
    labs(title = 'Observed species in time',
        x = 'Year of observation',
        y = 'Number of species') + \
    theme_bw() + \
    theme(axis_text_x = element_text(color="grey", size=10, angle=90, hjust=.5, vjust=.5),
          axis_text_y = element_text(color="grey", size=10, hjust=0),
         ) 
```


If you like the changes you created to the default theme, you can save them as
an object to easily apply them to other plots you may create:





```python
arial_grey_theme <- theme(axis.text.x = element_text(colour="grey20", size=12, angle=90, hjust=.5, vjust=.5),
                          axis.text.y = element_text(colour="grey20", size=12),
                          text=element_text(size=16, family="Arial"))
ggplot(surveys_complete, aes(x = species_id, y = hindfoot_length)) +
    geom_boxplot() +
    arial_grey_theme
```


```python
arial_grey_theme = theme(axis_text_x = element_text(color="grey", size=10, angle=90, hjust=.5, vjust=.5),
                          axis_text_y = element_text(color="grey", size=10))
ggplot(surveys_complete, aes(x = 'species_id', y = 'hindfoot_length')) + \
    geom_boxplot() + \
    arial_grey_theme
```


With all of this information in hand, please take another five minutes to either
improve one of the plots generated in this exercise or create a beautiful graph
of your own. Use the RStudio ggplot2 cheat sheet, which we linked earlier for
inspiration.

Here are some ideas:

* See if you can change thickness of the lines.
* Can you find a way to change the name of the legend? What about its labels?
* Use a different color palette (see http://www.cookbook-r.com/Graphs/Colors_(ggplot2)/)

After creating your plot, you can save it to a file in your favourite format.
You can easily change the dimension (and its resolution) of your plot by
adjusting the appropriate arguments (`width`, `height` and `dpi`):


```python
my_plot =  ggplot(yearly_sex_counts, aes(x = "year", y = "n", color = "sex", group = "sex")) 
my_plot += geom_line() 
my_plot += facet_wrap("species_id") 
my_plot += labs(title = 'Observed species in time',
                x = 'Year of observation',
                y = 'Number of species') 
my_plot += theme_bw() 
my_plot += theme(axis_text_x = element_text(color="grey", size=10, angle=90, hjust=.5, vjust=.5),
                        axis_text_y = element_text(color="grey", size=10))
my_plot.save("name_of_file.png", width=15, height=10)
```


```python
## Final plotting challenge:
##  With all of this information in hand, please take another five
##  minutes to either improve one of the plots generated in this
##  exercise or create a beautiful graph of your own. Use the RStudio
##  ggplot2 cheat sheet for inspiration:
##  https://www.rstudio.com/wp-content/uploads/2015/08/ggplot2-cheatsheet.pdf

```
