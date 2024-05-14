# Synthetic fuels for trucks

Description
-----------

This is a repository containing scenarios that implement the projections developed
in [insert publication]:

It is meant to be used in `premise` in addition to a global IAM scenario, 
to analyse teh fuel of synthetic fuels for heavy-duty trucks. 

This data package contains all the files necessary for `premise` to implement
this scenario and modify market- and region specific supply shares
for fuel for trucks.

Sourced from publication
------------------------

xxxx

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

| IAM scenario           | APS scenario            |
|------------------------|-------------------------|
| REMIND SSP2-Base       | Business As Usual       |
| REMIND SSP2-PkBudg1150 | Sustainable development |
| REMIND SSP2-PkBudg500  | Sustainable development |

What does this do?
------------------

This external scenario introduces a new synthetic fuel in the fuel blend
for heavy-duty trucks.


Flow diagram
------------

xxxx

How to use it?
--------------

```python

    import brightway2 as bw
    from premise import NewDatabase
    from datapackage import Package
    
    
    fp = r"https://raw.githubusercontent.com/MargotCha/HDfuels-prospective-scenarios/main/datapackage.json?token=GHSAT0AAAAAABRFQLPJH54SECNQQCO3BFYIY4QRBCA"
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

