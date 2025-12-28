# corrections on cloud
**these are changing data on cloud after everything is measured during aggregation phases**
# corrections in camera config 
- **these are changing measurements prior to sending to Cloud**
- the are set for each entrance
	- when multiple values for a given track can be set (because source entrance has different value than sink entrance) then SINK has higher priority and it's correction will be used. 
	- when only source or sink has correction it will be applied to all tracks with given sink/source

code explains it better:
```python
bias = 0  
# sink is more important  
if track.source_i_ in self.gender_biases:  
	bias = self.gender_biases[track.source_i_]  
if track.sink_i_ in self.gender_biases:  
	bias = self.gender_biases[track.sink_i_]
```

## gender
[[gender prediction]]
### bias 
```yaml
- type: 2
  id: 1
  accept_nearby: false
  gender_bias: -0.1
  points:  # entrance0
```
will do in [[footfall]]/footfall.py main loop:
`gender = min(max(0.0, gender + bias), 1.0)`

thus, when using gender_bias -0.1 it will skew measurements thus that there will be more females (gender < 0.5) values than before bias correction.

### prior
this config completely ignores NN predictions, it is last resort option
```yaml
- type: 2
  id: 0
  female_prior: 0.42
```

in [[footfall]] /footfall.py main loop, it will override neural network prediction and do:
```python
offset = (random.random() - 0.5) / 10  
gender = float(random.random() > (self.female_priors[track.source_i_]) + offset)
```

`offset` serves as a way how to set standard deviation. It can be probably written in more rigorous way...

*when using prior, gender output is only in {0, 1}*

## age 
available in [[ff v1.22.19]]

camera config example:
```yaml
- type: 2
  id: 0
  age_priors: [0.13, 0.2669, 0.4077, 0.1914]
  points:  # entrance0

```

there is an option to define priors for gaussian mixture
```python
self.age_means = [5, 24, 40, 70]  
self.age_stds = [3.0, 3.5, 4.5, 4.5]

def get_sample_from_distribution(priors, means, stds):  
	# get random number  
	r = np.random.rand()  
	# get index of the distribution  
	idx = np.argmax(r < np.cumsum(priors))  
	# get sample from the distribution  
	return min(max(0, np.random.normal(means[idx], stds[idx], 1)[0]), 100)


```

# Responsibilities
[[PROJECTS/iC/wiki/Personal/Filip Naiser]]
