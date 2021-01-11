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

#### Preliminary onfigurations

After you obtain the login details for your account I recommend installing the following programs to work more easily on the servers: ssh and VS Code
You can find the list of supported ssh clients in [the VS Code docs](https://code.visualstudio.com/docs/remote/troubleshooting#_installing-a-supported-ssh-client)
- For Widows use https://docs.microsoft.com/en-us/windows-server/administration/openssh/openssh_install_firstuse to enable ssh
- For Linux install ssh using your system's package manager.
- For MacOS ssh should be available in the Terminal

You can find VS Code here: https://code.visualstudio.com/
After you install VS Code, install the following extensions
- Remote - SSH
- [Julia](https://www.julia-vscode.org/docs/dev/gettingstarted/#Installation-and-Configuration-1)

##### Configuring ssh access from VS Code
The next step is to configure the remote ssh access from VS Code to the servers. [Refer to the docs](https://code.visualstudio.com/docs/remote/ssh#_connect-to-a-remote-host) for detailed instructions. In the 3rd step choose Linux for the remote host platform.
##### Configuring the Julia extension
In VS Code extensions can have different configurations depending on whether you are runing locally or remotely. For the remote configuration go to the extension settings in the Remote tab and set the "Julia: Executable Path" to `/mnt/storage/julia.sh`.
I would also recommend the following settings (you can apply them in the User tab to have them available everywhere as a default)
- Set "Julia > Execution: Result Type" to "inline"
- Disable "Julia: Use Revise"
- Use the keyboard shortcuts form Juno: https://gist.github.com/kescobo/3bc5416d83343ebe53da73813d4a61e6

There are two PIC simulation programs installed on the server: EPOCH and smilei. The most used one is EPOCH.

#### Running EPOCH simulations

The `/mnt/storage/epoch` folder on the servers is used as a common storage location for all EPOCH simulations. In that folder there are multiple other folders corresponding
to various projects and their corresponding input and output files. Each simulation must have a separate folder which contains an `input.deck` file which specifies
the initial conditions according to the [EPOCH documentation](https://cfsa-pmw.warwick.ac.uk/mediawiki/index.php/EPOCH:Input_deck).
After you prepare the folder with the `input.deck` file inside you are ready to run the simulation. The simplest way to do this is with the `run` script in the
`/mnt/storage/epoch` folder. The syntax for using the script is the following:
```
./run [epoch_app] folder_with_input.deck [hostfile]
```

The `epoch_app` parameter can be one of the following:
- `epoch1d`: EPOCH 1D compiled with default options. The runscript accepts one argument which is the folder containing the input.deck file. Uses 1 local process.
- `epoch2d`: EPOCH 2D compiled with default options. The runscript accepts one argument which is the folder containing the input.deck file. Uses 20 local processes.
- `epoch3d`: EPOCH 3D compiled with default options. The runscript accepts two arguments which specify the folder containing the input.deck file and the hostfile. Uses 40 processes on the machines specified in the hostfile.
- `epoch3d_HC`: EPOCH 3D compiled with the Higuera-Cary push. The runscript accepts two arguments which specify the folder containing the input.deck file and the hostfile. Uses 40 processes on the machines specified in the hostfile.
- `epoch1d_tracking`: EPOCH 1D compiled with particle tracking and prefetch options. The runscript accepts one argument which is the folder containing the input.deck file. Uses 1 local process.
- `epoch2d_tracking`: EPOCH 2D compiled with particle tracking and prefetch options. The runscript accepts one argument which is the folder containing the input.deck file. Uses 20 local processes.
- `epoch3d_tracking`: EPOCH 3D compiled with particle tracking and prefetch options. The runscript accepts two arguments which specify the folder containing the input.deck file and the hostfile. Uses 40 processes on the machines specified in the hostfile.
- `epoch3d_tracking_HC`: EPOCH 3D compiled with the Higuera-Cary push and with particle tracking and prefetch options. The runscript accepts two arguments which specify the folder containing the input.deck file and the hostfile. Uses 40 processes on the machines specified in the hostfile.
- `epoch1d_photons`: EPOCH 1D compiled with support for photon particle type. The runscript accepts one argument which is the folder containing the input.deck file. Uses 1 local process.
- `epoch2d_photons`: EPOCH 2D compiled with support for photon particle type. The runscript accepts one argument which is the folder containing the input.deck file. Uses 20 local processes.
- `epoch2d_qed_all`: EPOCH 2D compiled with support for photon particle type, Bremsstrahlung processes and support for virtual photons which are used by the Trident process for pair production. The runscript accepts one argument which is the folder containing the input.deck file. Uses 20 local processes.
- `epoch2d_qed_all_HC`: EPOCH 2D compiled with the Higuera-Cary push and with support for photon particle type, Bremsstrahlung processes and support for virtual photons which are used by the Trident process for pair production. The runscript accepts one argument which is the folder containing the input.deck file. Uses 20 local processes.
- `epoch3d_photons`: EPOCH 3D compiled with support for photon particle type. The runscript accepts two arguments which specify the folder containing the input.deck file and the hostfile. Uses 40 processes on the machines specified in the hostfile.
- `epoch3d_photons_tracking`: EPOCH 3D compiled with support for photon particle type and particle tracking and prefetch options. The runscript accepts two arguments which specify the folder containing the input.deck file and the hostfile. Uses 40 processes on the machines specified in the hostfile.
- `epoch3d_qed_all`: EPOCH 3D compiled with support for photon particle type, Bremsstrahlung processes and support for virtual photons which are used by the Trident process for pair production. The runscript accepts two arguments which specify the folder containing the input.deck file and the hostfile. Uses 40 processes on the machines specified in the hostfile.
- `epoch3d_qed_all_HC`: EPOCH 3D compiled with the Higuera-Cary push and with support for photon particle type, Bremsstrahlung processes and support for virtual photons which are used by the Trident process for pair production. The runscript accepts two arguments which specify the folder containing the input.deck file and the hostfile. Uses 40 processes on the machines specified in the hostfile.
- `epoch3d_qed_all_tracking`: EPOCH 3D compiled with support for photon particle type, Bremsstrahlung processes, support for virtual photons which are used by the Trident process for pair production and particle tracking and prefetch options.
- `epoch3d_qed_all_tracking_HC`: EPOCH 3D compiled with the Higuera-Cary push, with support for photon particle type, Bremsstrahlung processes, support for virtual photons which are used by the Trident process for pair production and with particle tracking and prefetch options. The runscript accepts two arguments which specify the folder containing the input.deck file and the hostfile. Uses 40 processes on the machines specified in the hostfile.

The `hostfile` should be text file containing the name of the machines separated by a new line. There are already some files prepared in the `/mnt/storage/epoch` folder.
They are named: `h1`, `h2`, `h3` and `h4`. You should use them in that order according to availability.

### Reading / viewing simulation results

There are 2 ways of viewing the results of an EPOCH simulation availabe on the server: the VisIt version and the Julia version.

#### [The VisIt version](VisIt.md)
First, you have to install the VisIt client on you local machine. Download it from https://wci.llnl.gov/simulation/computer-codes/visit/executables. You will need v3.1.2 or newer.

#### The Julia version
- Open the `/mnt/storage/epoch/epoch.code-workspace` workspace.
