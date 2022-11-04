# System Description - Accelerators
| Component | Quantity | Description |
|---|---|---|
|  |  |  |
| Graphcore IPU | 16 | 16 IPUs direct-attached to a server. |
| Future Intel Agilex FPGA Accelerator | 20 | Agilex FPGA with a broad hierarchy of memory including DDR5, HBM2e and Optane Persistent Memory |
| NextSilicon coprocessor | 20 | Reconfigurable accelerator with an optimizer continuously evaluating application behavior. |
| NEC Vector Engine | 24 | Vector computing card with 8 cores and HBM2 memory. |
| Intel Ponte Vecchio GPU | 100 | Intel GPU for HPC, DL Training, AI Inference |
| Liqid Intel Optane PCIe SSDs | 6 | 3 TB PCIe SSD cards addressable as memory using Intel Memory Drive Technology |

| Hardware Profile | Application examples |
|---|---|
| Primarily distributed memory parallel | WRF, CHARMM, STAR, OpenFOAM, CESM, HMMER, STAR, METIS, Gaussian, Bioconda, Molecular Dynamics (MD, NAMD etc.) |
| Double precision GPU intensive | MD (LAMMPS, GROMACS, NAMD) VASP, Quantum Espresso, WRF |
| Half/Single precision GPU intensive | LAMMPS, TensorFlow, GROMACS, Python, AMBER |
| Large memory, variable core count | CESM, CWPSU, Bowtie, R, Orca, GAMESS, Cufflink |
| Large memory, GPU intensive | ParaView, TensorFlow (Keras), Pytorch, Caffe, Orca, WRF |

| Hardware Profile | Application examples |
|---|---|
| Vector Engine | Plasma Simulation, Weather / Climate Simulation, NumPy acceleration, Earth Sciences, Oil and Gas - Seismic Imaging and Reservoir Simulation, Chemistry – VASP and Quantum ESPRESSO, AI / ML – Statistical Machine Learning and Data Frame (Apache Spark / Big Data) |
| Graphcore IPU | LSTM Neural Networks, Markov Chain Monte Carlo, Graph data, Natural Language Processing (Deep Learning) |
| FPGA | Big Data, Deep Learning Inference, Streaming data analysis, Genomics, AI Models for embedded use cases, CXL memory interface, Microcontroller emulation for Autonomy simulations, MD codes |
| Optane PCIe SSD | Bioinformatics, Computational Fluid Dynamics, R, WRF, MD codes |
| NextSilicon | Computational Fluid Dynamics (OpenFOAM), Molecular Dynamics (NAMD, AMBER, LAMMPS), Weather/Environment modeling (WRF), Biosciences (BLAST), Graph Search (Pathfinder), Cosmology (HACC), Quantum ChromoDynamics (MILC) |