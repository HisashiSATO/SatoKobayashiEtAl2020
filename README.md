********************************************************************
Notes for SEIB-DGVM MPI-version (27/Feb/2020)
   Hisashi SATO (JAMSTEC)
   http://seib-dgvm.com/hsato/
********************************************************************
(1) This package enables the SEIB-DGVM to compute multigrid cells by using MPI parallel computation. This package also contains a R code for visualizing result of the multi-grid simulation. Ask your system administrator whether your environment satisfies this condition. You also have to prepare climate data. I do not distribute it online, because of the large size! If you want to get a copy of climatic data,  contact me, then I would I can help.

(2) Following files must be modified to meet machine environment and simulation design. Comment lines are available in these files.
  start_multiCTI.f90
  main_multiCTI.f90 
  Makefile
  go_l.bat
  go_l.sh
  parameter.f90
  
(3) Following parameters in parameter.txt will NOT be used for MPI simulations. Corresponding parameters are defined in start_mpi.f90.
  Fn_climate
  Fn_location
  Fn_spnin
  Fn_spnout
  
(4) To change simulation years, modify the parameter value of Simulation_year in the parameter.txt. If this simulation year is longer than climatic data, this code use climate data repeatedly. To change this feature, modify folllowing line, which will be found in the main_multiCTI.f90.
  if (year_climate==YearMaxClimate+1) year_climate=1
For example, if you want to repeat climate data of last year when simulation year exceeds data lenght, change as follows:
  if (year_climate==YearMaxClimate+1) year_climate=YearMaxClimate

(5) In the default code, distribution maps are generated using average results during last 10 years of the simulation. To change this period for average, alter the value in parameter YearForMean in start_multiCTI.f90.

(6) For executing code, copy whole files and directories in this folder to execution directory on your computation environment. Then, on the execution directory, type following command sequantially. The first command compiles the code, and the secound command conducts simulation and visualization.
  ifort AveragingSiteDetail_plane.f90 -o AveragingSiteDetail_plane.out
  ifort AveragingSiteDetail_mount.f90 -o AveragingSiteDetail_mount.out
  makefile
  sh go_l.sh &
