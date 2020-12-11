# PIC Tutorials

This document provides some guidance for students getting started with Particle in cell (PIC) simulations.

## Overview
1. The Particle in cell (PIC) method
2. Running PIC simulations on the cluster
3. Reading / viewing simulation results

### The Particle in cell (PIC) method
Since there is a lot of literature on this topic, I will just enumerate some of the sources that I've used and found useful.

#### Short version
- R. Lehe, “Electromagnetic Particle-In-Cell codes”, presented at the USPAS 2018: Simulation of Beam and Plasma Systems, Old Dominion University Hampton, VA, Jan. 15, 2018, Accessed: Aug. 15, 2019. [Online]. Available: https://people.nscl.msu.edu/~lund/uspas/sbp_2018/lec_em_pic/A1a_EM_PIC.pdf.
- R. Lehe, “Electromagnetic wave propagation in Particle-In-Cell codes”, presented at the USPAS 2018: Simulation of Beam and Plasma Systems, Old Dominion University Hampton, VA, Jan. 15, 2018, Accessed: Aug. 15, 2019. [Online]. Available: https://people.nscl.msu.edu/~lund/uspas/sbp_2018/lec_em_pic/A1b_EM_Waves.pdf.
- Section 1.5 of A. O’Neil, “Laser Wakefield Accelerator Simulations Using EPOCH”, MSci Thesis, Queen’s University Belfast, 2017. Available: https://pure.qub.ac.uk/portal/files/147720282/Aaron_ONeill_40007530.pdf

#### Long version
- C. K. Birdsall and A. B. Langdon, Plasma physics via computer simulation. Bristol: Institute of Physics Pub., 2005.
- R. W. Hockney and J. W. Eastwood, Computer simulation using particles, Special student ed. Bristol [England]; Philadelphia: A. Hilger, 1988.

#### Theses
- A. O’Neil, “Laser Wakefield Accelerator Simulations Using EPOCH”, MSci Thesis, Queen’s University Belfast, 2017. Available: https://pure.qub.ac.uk/portal/files/147720282/Aaron_ONeill_40007530.pdf
- S. Micluța-Câmpeanu, “Laser Wakefield Acceleration - Studies using Particle in Cell Method”, MSci Thesis, University of Bucharest, 2019. Available: [SebastianM-C/MasterThesis](https://github.com/SebastianM-C/MasterThesis)
- M. Dolineanu, “Studies of Laser Wakefield Acceleration and Gamma-Ray Generation by Laser-Irradiated Structured Targets using Particle-in-Cell Numerical Simulations”, Bachelor Thesis, University of Bucharest, 2020. Available: [DolineanuMircea/Bachelor-Thesis](https://github.com/DolineanuMircea/Bachelor-Thesis)
- P. Valenta, “Tight-focusing of short intense laser pulses in particle-in-cell simulations of laser-plasma interaction”, MSci Thesis, Czech Technical University, Prague, 2016. Available: http://kfe.fjfi.cvut.cz/~valenpe7/master_thesis.pdf
- M. Toggweiler, “An adaptive time integration method for more eﬃcient simulation of particle accelerators”, MSci Thesis, ETH Zurich, 2011. Available: https://doi.org/10.3929/ethz-a-006911936
- A. Huebl, “Injection Control for Electrons in Laser-Driven Plasma Wakes on the Femtosecond Time Scale,” 2014. Available: https://zenodo.org/record/15924

### Running PIC simulations on the cluster

After you obtain the login details for your account I recommend installing the following programs to work more easily on the servers: ssh and VS Code
You can find the list of supported ssh clients in [the VS Code docs](https://code.visualstudio.com/docs/remote/troubleshooting#_installing-a-supported-ssh-client)
- For Widows use https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse to enable ssh
- For Linux install ssh using your system's package manager.
- For MacOS ssh should be available in the Terminal

You can find VS Code here: https://code.visualstudio.com/
After you install VS Code, install the following extensions
- Remote - SSH
- [Julia](https://www.julia-vscode.org/docs/dev/gettingstarted/#Installation-and-Configuration-1)

#### Configuring ssh access from VS Code
The next step is to configure the remote ssh access from VS Code to the servers. [Refer to the docs](https://code.visualstudio.com/docs/remote/ssh#_connect-to-a-remote-host) for detailed instructions. In the 3rd step choose Linux for the remote host platform.
#### Configuring the Julia extension
In VS Code extensions can have different configurations depending on whether you are runing locally or remotely. For the remote configuration go to the extension settings in the Remote tab and set the "Julia: Executable Path" to `/mnt/storage/julia.sh`.
I would also recommend the following settings (you can apply them in the User tab to have them available everywhere as a default)
- Set "Julia > Execution: Result Type" to "inline"
- Disable "Julia: Use Revise"
- Use the keyboard shortcuts form Juno: https://gist.github.com/kescobo/3bc5416d83343ebe53da73813d4a61e6

There are two PIC simulation programs installed on the server: EPOCH and smilei. The most used one is EPOCH.

### Reading / viewing simulation results

There are 2 ways of viewing the results of an EPOCH simulation availabe on the server: the VisIt version and the Julia version.

#### [The VisIt version](VisIt.md)
First, you have to install the VisIt client on you local machine. Download it from https://wci.llnl.gov/simulation/computer-codes/visit/executables. You will need v3.1.2 or newer.

#### The Julia version
- Open the `/mnt/storage/epoch/epoch.code-workspace` workspace.
