# Synthetic diesel for trucks

Description
-----------

This is a repository containing scenarios that implement the projections developed in:
**Integrating emerging technologies deployed at scale within prospective life cycle assessment**\
*Margarita A. Charalambous, Romain Sacchi, Victor Tulus, Gonzalo Guillén Gosálbez*

It is meant to be used in `premise` in addition to a global IAM scenario, 
to analyze synthetic diesel for heavy-duty trucks. 

This data package contains all the files necessary for `premise` to implement
this scenario and modify market- and region specific supply shares
for trucks.

Sourced from publication
------------------------

If you use this data package in your research, please cite the following publication:
**Charalambous et al., 2024. Integrating emerging technologies deployed at scale within prospective life cycle assessment, Sustainable Production and Consumption.**\
DOI: https://doi.org/10.1016/j.spc.2024.08.016

Data validation 
---------------

xxxx

Test 
----

xxxx

Ecoinvent database compatibility
--------------------------------

ecoinvent 3.8 cut-off

IAM scenario compatibility
---------------------------

The following coupling is done between IAM scenarios and the ammonia market scenarios (APS):

| IAM scenario           | APS scenario            | Climate policy                    |
|------------------------|-------------------------|-----------------------------------|
| REMIND SSP2-Base       | Business As Usual       | None                              |
| REMIND SSP2-PkBudg1150 | Sustainable development | Paris Agreement                   |
| REMIND SSP2-PkBudg500  | Sustainable development | Paris Agreement                   |
| REMIND SSP2-NPi        | Sustainable development | National Policies Implemented     |
| REMIND SSP2-NDC        | Sustainable development | National Determined Contributions |
| REMIND SSP1-Base       | Business As Usual       | None                              |
| REMIND SSP1-PkBudg1150 | Sustainable development | Paris Agreement                   |
| REMIND SSP1-PkBudg500  | Sustainable development | Paris Agreement                   |
| REMIND SSP1-NPi        | Sustainable development | National Policies Implemented     |
| REMIND SSP1-NDC        | Sustainable development | National Determined Contributions |
| REMIND SSP5-Base       | Business As Usual       | None                              |
| REMIND SSP5-PkBudg1150 | Sustainable development | Paris Agreement                   |
| REMIND SSP5-PkBudg500  | Sustainable development | Paris Agreement                   |
| REMIND SSP5-NPi        | Sustainable development | National Policies Implemented     |
| REMIND SSP5-NDC        | Sustainable development | National Determined Contributions |


What does this do?
------------------

This external scenario introduces synthetic diesel fuel destined to replace the synthetic fraction of the diesel market which is fueling heavy-duty trucks.

We introduce efficiency improvements in hydrogen production and electrolysis.

We include 11 *hydrogen production pathways* and two technologies for capturing CO₂:
* For **H<sub>2</sub>**: 10 PEM electrolysis and 1 bio-based
* For **CO<sub>2</sub>**: one direct air capture (DAC) and one post-combustion capture

Resulting in **22 diesel production pathways** by combining **H<sub>2</sub>** and **CO<sub>2</sub>**.

Here we do not modify the technosphere using specific keywords of premise, but we perform the modifications later using inventory matrices. 
As shown in the [Integrated-LCA repository](https://github.com/MargotCha/Integrated-LCA-master) and the IntLCA package that can be installed through [pypi](https://pypi.org/project/IntLCA-dev/). 


Flow diagram
------------
The locations that the synthetic diesel which is included in this data package will be added are shown with light blue in figure:
<img src="https://github.com/MargotCha/HDdiesel-prospective-scenarios/blob/main/flow_diagram.png" width="300" />

How to use it?
--------------

```python

    import brightway2 as bw
    from premise import NewDatabase
    from datapackage import Package
    
    
    fp = r"https://raw.githubusercontent.com/MargotCha/HDdiesel-prospective-scenarios/main/datapackage.json?token=GHSAT0AAAAAACSIUT3TGN2FEDOVFGKKKJPAZSGACQQ"
    synfuel = Package(fp)
    
    bw.projects.set_current("your_bw_project")
    
    ndb = NewDatabase(
            scenarios = [
                {"model":"remind", "pathway":"SSP2-Base", "year":2050,},
                {"model":"remind", "pathway":"SSP2-PkBudg1150", "year":2030,},
            ],        
            source_db="ecoinvent 3.8 cutoff",
            source_version="3.8",
            key='xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx',
            external_scenarios=[
                synfuel, # <-- list datapackages here
            ] 
        )
```

