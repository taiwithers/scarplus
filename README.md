# scarplus
As described in [paper], `scarplus` (stylised as SCAR+) is a wrapper/add-on/extension of Mike Chen's [MUFASA](https://github.com/mcyc/mufasa/).

The package contains several modules which you'll need to import and call functions from in order to replicate the analysis.

A minimal working example to run the ammonia analysis is:

```python
from scarplus import cloud, cloud_setup, scarplus_fitter

dm = cloud.DirectoryManager({'NH3':'path/to/store/generated/files',
							 'KEYSTONE':'path/to/store/downloaded/files'})

cloud_name = 'MonR1'
cloud_distance = 0.72 # kpc
cloud_distance_uncertainty = 0.05 # kpc

nh3_cloud = cloud.NH3_Cloud(cloud_name, dm)
cloud_setup.nh3_setup(nh3_cloud) # downloads data and does some pre-analysis

# perform the three-component fitting
scarplus_fitter.run_mufasa(nh3_cloud)
scarplus_fitter.choose_1c_model(nh3_cloud)
scarplus_fitter.choose_1or2c_model(nh3_cloud)
scarplus_fitter.run_trifit(nh3_cloud)
scarplus_fitter.choose_scarplus_mufasa(nh3_cloud)
scarplus_fitter.choose_absorption_refit_scarplus(nh3_cloud)
```

This will take some time, run on multiple cores by default, overwrite all files by default, and generate a great number of files. 
Most of this can be configured by changing keyword arguments.

There are also many plotting functions in the `plotting` module and these are also configurable.