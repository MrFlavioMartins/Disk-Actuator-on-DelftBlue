# Disk Actuator model in OpenFOAM 



## Description

This repository contains an **OpenFOAM (v9/v10)** solver set for running at clusters (more specifically, at TU Delft's **DelftBlue** supercomputer). The flow physics captured in this OpenFOAM project consists of a custom actuator-surface model with lift-generating devices modeled as actuator lines. 

<p align="center">
<img src="Results/Velocity_Fields.png"  width="90%">
</p>

* The custom actuator-surface models are dynamically compiled during the run, so the user does not need to manually compile a custom OpenFOAM solver before submitting the job to the cluster

* The dimensions of the actuator surfaces are defined using the conventional **OpenFOAM's** `./system/topoSetDict` dictionary 

* The surface-actuator force fields are defined in the custom file `./ActuatorsSetup`, such that `Cx` is the thurst force coefficient of the actuator surface, `Cy` is the effective lift force coefficient of the lift-generating devices, `A`, the actuator surface's area, `upU` ($U_\infty$) is reference free-stream speed, such that:

    $ F_x = \frac{1}{2} \rho A U_\infty^2 C_x $

    $ F_y = \frac{1}{2} \rho A U_\infty^2 C_y $


The direction $x$ of the actuator-surface's force, $F_x$, is defied with the vector `RotorForceDir`; similarly, the direction of the lift force produced by the lifting-generating devices, `Fy`, is defined with `BladeForceDir`.


## Authors
  
* Flavio Martins ([@MrFlavioMartins](https://github.com/MrFlavioMartins), [ORCID](https://orcid.org/0000-0002-1374-5760), f.m.martins@tudelft.nl, Wind Energy Research Group, TU Delft, Delft/NL)


## Table of Contents

- [Requirements](#Requirements)
- [How to run](#How-to-run)
- [License](#License)
- [References](#References)
- [How to contribute](#How-to-contribue)

## Requirements  


To run this project, simply install on your local machine OpenFOAM v10, as per instruction's in the source's [website](https://openfoam.org/version/10/)

<!--- Add badges of requirements e.g.:  
    [![Python 3.6](https://img.shields.io/badge/Python-3.6-3776AB)](https://www.python.org/downloads/release/python-360/)  
-->  

<!--- Provide details of the software required   
    * Add a `requirements.txt` file to the root directory for installing the necessary dependencies.   
    * Describe how to install requirements e.g. when using pip:  

        To install requirements:

        ```
            setup
            pip install -r requirements.txt
        ```

    * Alternatively, create an INSTALL.md. 
    * Provide any further instructions on how others can make sure the scripts are running for benchmarking examples (e.g. by using computational notebooks such as Jupyter notebooks) 
-->

## How to run  

Below, it is illustrated how to run the OpenFOAM simulation on TU Delft's DelftBlue supercomputer from the folder `~/mySimulation/`.

Run from the project's root folder on the local machine:

```
rsync -avx ./  delftblue:~/mySimulation
ssh <netid>@login.delftblue.tudelft.nl
```

On the SSH environment:

```
cd ~/mySimulation/Solver
sbatch ALLRUN_MASTER.sh
```

To visualize the status of your request, use:

```
squeue --account <netid>
```

Subsequently, to print the evolution of the solution, one can use the command below to print the last 30 lines of the `./log.simpleFoam` file every 60 s:


```
watch -n 60 tail -n 30 log.simpleFoam
```



## License

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)  

The contents of this repository are licensed under a **Apache License 2.0** license.

TU Delft hereby disclaims all copyright interest in the program “**Disk Actuator model in OpenFOAM**”, an OpenFOAM case file with custom disk-actuator solver meant for running at clusters, written by the Author(s).  

    © 2023, Flavio Martins



## References

For more information on how to run OpenFOAM application on DelftBlue, refer to:

 * [DelftBlue documentation (OpenFOAM)](https://doc.dhpc.tudelft.nl/delftblue/howtos/openfoam/) 

For some backgound on Momentum theory, please refer to:

 * Burton, Tony, Nick Jenkins, David Sharpe, and Ervin Bossanyi. Wind energy handbook. John Wiley & Sons, 2011.
 * Katz, Joseph, and Allen Plotkin. Low-speed aerodynamics. Vol. 13. Cambridge university press, 2001

For more insights into fundamental aerodymics, also refer to:

* Anderson, John. Fundamentals of Aerodynamics. McGraw Hill, 2011.


## Citation

<!--- Make the repository citable 
    * If you will be using the Zenodo-Github integration, add the following reference and the DOI of the Zenodo repository:

        If you want to cite this repository in your research paper, please use the following information:
        Reference: [Making Your Code Citable](https://guides.github.com/activities/citable-code/)  

    * If you will be using the 4TU.ResearchData-Github integration, add the following reference and the DOI of the 4TU.ResearchData repository:

        If you want to cite this repository in your research paper, please use the following information:   
        Reference: [Connecting 4TU.ResearchData with Git](https://data.4tu.nl/info/about-your-data/getting-started)   
-->


## How to contribute

* Want to contribute? Append your names in a separate list of Contributors in the `Readme`; 

* Add your contributions in separate files specifying your copyright attribution at the top of the source files as commented text.