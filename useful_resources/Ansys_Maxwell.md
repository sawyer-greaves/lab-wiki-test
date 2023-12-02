[Home](../Home)
# Ansys Maxwell

Ansys Maxwell is Finite Element Analysis software contained within Ansys Electronics Desktop (AEDT), not Ansys Workbench, used to simulate electro-magnetic phenomena. Simulations can be performed for 2D or 3D, and either statically or transient.

# Tutorial Modules
The following modules were created by Ansys to onboard users into the software. The collection is a work in progress, as these modules are not listed conveniently on any Ansys webpage (at time of writing), and this list is the result of much google-foo.

- Module 1: 
    - [Basics](Ansys_Maxwell_Modules/Module_1_Basics.pdf)
    - [Workshop 1.1](Ansys_Maxwell_Modules/Workshop_1_1_Magnetostatic_2D.pdf) Magnetostatic 2D 
    - [Workshop 1.2](Ansys_Maxwell_Modules/Workshop_1_2_Magnetostatic_3D.pdf) Magnetostatic 3D 
- Module 2:
    - [Quasistatic Solvers](Ansys_Maxwell_Modules/Module_2_Quasistatic_Solvers.pdf)
    - [Workshop 2.1](Ansys_Maxwell_Modules/Workshop_2_1_Eddy_Current_Analysis.pdf) Eddy Current Analysis
    - [Workshop 2.2](Ansys_Maxwell_Modules/Workshop_2_2_Electrostatic_Analysis.pdf) Electrostatic Analysis
    - [Workshop 2.3](Ansys_Maxwell_Modules/Workshop_2_3_3D_Eddy_Current_Analysis.pdf) 3D Eddy Current Analysis
    - [Workshop 2.4](Ansys_Maxwell_Modules/Workshop_2_4_Electrostatic_Analysis.pdf) Electrostatic Analysis
- Module 3:
    - [Transient Solvers](Ansys_Maxwell_Modules/Module_3_Transient_Solvers.pdf) 
    - [Workshop 3.1](Ansys_Maxwell_Modules/Workshop_3_1_2D_Magnetic_Transient_Analysis.pdf) 2D Magnetic Transient Analysis 
        - Note: This workshop requires an Ansys supplied example file (WS3_1.aedt), which has not been located. The content is still worthwhile, as the procedure for Motion Setup is shown.
    - [Workshop 3.2](Ansys_Maxwell_Modules/Workshop_3_2_3D_Magnetic_Transient_Analysis.pdf) 3D Magnetic Transient Analysis
- Module 4:
    - [Postprocessing and Parametric](Ansys_Maxwell_Modules/Module_4_Postprocessing_and_Parametric.pdf)
    - [Workshop 4.1](Ansys_Maxwell_Modules/Workshop_4_1_Postprocessing.pdf) Postprocessing
    - [Workshop 4.2](Ansys_Maxwell_Modules/Workshop_4_2_Parametric_Analysis.pdf) Parametric Analysis
- Module 5:
    - [Multiphysics](Ansys_Maxwell_Modules/Module_5_Multiphysics.pdf)
    - [Workshop 5.2](Ansys_Maxwell_Modules/Workshop_5_2_Electromagnetic_Thermal_Coupling.pdf) Magnetic Thermal Coupling


# Scripting 
All Ansys software can be ran via external scripting. This gives the benefit of additional control regarding the mesh process, and most importantly the ability to automate simulations. 

## APDL and MAPDL
Ansys created their own scripting language APDL (Ansys Parametric Design Language) and MAPDL (Mechanical APDL) as a further extension of their scripting software. These are available at every licensing level, including the student license level. 

## PyAEDT
Alternatively, there are packages for Python that accomplish the same level of control. A user of Python and MAPDL found the process too unwieldy, and set about making PyAnsys. Ansys has since employed this person and encouraged them to expand their efforts to the various depths of Ansys software. [PyAEDT](https://aedt.docs.pyansys.com/version/stable/index.html) provides scripting abilities for the Electronic Desktop (AEDT) portion of Ansys that is a companion to Ansys Workbench, and contains Maxwell. Several installation methods are provided and explained [here](https://aedt.docs.pyansys.com/version/stable/Getting_started/Installation.html).

Installation Methods

- Install from a Python file:
    - Following this installation procedure installs PyAEDT to be run with CPython, which AEDT already includes. 
    - This option allows for console-style control, or to script via web-based Jupyter, from within the Tools>Toolkit options within AEDT. Once a script has been generated and saved locally to the device, the option "Run_PyAEDT_Script" allows for the generated script to run. 
    -This installation method does not install the PyAEDT package into any locally installed IDE.

- Install PyAEDT in Conda virtual environment:
    - Following this in installation procedure installs PyAEDT such that any IDE launched from Anaconda can access the package (i.e. Spyder, Jupyter, etc.).
    - Launching the virtual environment is done via the CMD.exe prompt within Anaconda.
    - PyAEDT scripts can then run within the Python IDE or your choice, and Ansys can boot from the script, with or without a graphical interface. 


Running a Script

After PyAEDT has been installed, a new entry will have been added to the dropdown menu of the Tools tab in the ribbon. Selecting `Tools`-`Toolkit`-`PersonalLib`-`PyAEDT` will show three options for interfacing with PyAEDT (if this option is not present in the toolbar, try restating Ansys first, then check installation). Regardless of the PyAEDT interface chosen, the commands and syntax are identical. Regardless of the PyAEDT interface chosen, the commands and syntax are identical. The three options are as follows:

- Console: This option opens a terminal and launches PyAEDT. From here, individual commands can be entered, and can be used in concert with the graphical portion of Ansys. This option can be quite useful for tinkering and testing commands (the commands can easily be undone by deleting the newly added feature through the graphical interface).
- Jupyter: This option opens a Jupyter notebook in the default browser, and allows for live scripting. (This option is not recommended, as it crashed every time the author tried to explore what it launched).
- Run PyAEDT Script: This option asks you to navigate to a extant Python script saved wherever. It then runs the code to completion. Inside the script when the Ansys instance options are declared, a boolean exists to declare if the script will open Ansys graphically or not.

Additionally, one can run generate Python scripts from the IDE, without ever (visually) opening Ansys. This option is recommended for stable, solid scripts, as debugging is very difficult this way.






## User Guides

The [PyAnsys](https://aedt.docs.pyansys.com/version/stable/User_guide/index.html) website provides several code examples, across all AEDT functionality, that include examples for the entire process. Additional resources can be found by navigating throughout. For command documentation see [PyAEDT API](https://aedt.docs.pyansys.com/version/stable/API/index.html).