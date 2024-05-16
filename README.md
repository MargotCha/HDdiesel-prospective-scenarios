# Synthetic diesel for trucks

Description
-----------

This is a repository containing scenarios that implement the projections developed in:
**Closed-loop LCA of technologies deployed at large scale using modified background data**\
*Margarita A. Charalambous, Romain Sacchi, Victor Tulus, Gonzalo Guillén Gosálbez*\
Under review.

It is meant to be used in `premise` in addition to a global IAM scenario, 
to analyze synthetic diesel for heavy-duty trucks. 

This data package contains all the files necessary for `premise` to implement
this scenario and modify market- and region specific supply shares
for fuel for trucks.

Sourced from publication
------------------------

If you use this data package in your research, please cite the following publication:
**Closed-loop LCA of technologies deployed at large scale using modified background data**\
*Margarita A. Charalambous, Romain Sacchi, Victor Tulus, Gonzalo Guillén Gosálbez*\
Under review.

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

This external scenario introduces synthetic diesel fuel in the fuel blend
for heavy-duty trucks.

Hydrogen
********

Efficiency improvements in hydrogen production and electrolysis are introduced.

We introduce 11 hydrogen production pathways:
* 10 PEM electrolysis
* 1 bio-based

Diesel fuel
********

We introduce 22 diesel production pathways by Fischer-Tropsch sysnthesis by combining hydrogen and CO2. 
For the CO2 we use:
* Direct air capture
* Post-combustion capture

This market re-links to ammonia-producing activities 
that consume hydrogen throughout the database.


Flow diagram
------------

![diagram diesel markets](assets/flow_diagram.png)

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

