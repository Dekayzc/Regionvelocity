
# Regionvelocity

Region velocity is an extension of RNA velocity
(velocyto-team/velocyto.R) for long-read sequencing technology using
exons and introns counts as observed data to extrapolate future cell
state. It includes steady-state model and dynamical model using EM
algorithm in R.

## Pre-installation

Region velocity can be installed on linux systems and windows with
Rtools, requiring C++11, Open MP support, boost libaries, igraph library
and hdf5c++ library. The library installation in linux can refer from
velocyto-team/velocyto.R/dockers/debian9/Dockerfile. Windows
installation should refer the installation of libboost in Rtools.

## Install

    library(devtools)
    install_github("Dekayzc/Regionvelocity")

## Data

Published data is available in this package. Suffix "\_eyes" means
expression matrix (exons,introns,spliced counts, unspliced counts and
RNA counts) from monkey limbal cells and “sper” means expression matrix
from mouse spermary cells.

    Data sets in package ‘Regionvelocity’:

    cell_e_gexp_eyes                                
    cell_e_gexp_sper_ont_gene                       
    cell_e_gexp_sper_ont_trans                      
    cell_e_gexp_sper_pb                             
    cell_i_gexp_eyes                                
    cell_i_gexp_sper_ont_gene                       
    cell_i_gexp_sper_ont_trans                      
    cell_i_gexp_sper_pb                             
    cell_ls_gexp_sper_pb                            
    cell_lu_gexp_sper_pb                            
    cell_RNA_gexp_eyes                              
    cell_RNA_gexp_sper_ont_gene                     
    cell_RNA_gexp_sper_ont_trans                    
    cell_RNA_gexp_sper_pb                           
    cell_s_gexp_eyes                                
    cell_s_gexp_sper_ont_gene                       
    cell_s_gexp_sper_ont_trans                      
    cell_s_gexp_sper_pb                             
    cell_u_gexp_eyes                                
    cell_u_gexp_sper_ont_gene                       
    cell_u_gexp_sper_ont_trans                      
    cell_u_gexp_sper_pb                             

## Example

    library(Regionvelocity)
    data(cell_e_gexp_sper_pb)
    data(cell_i_gexp_sper_pb)
    data(cell_RNA_gexp_sper_pb)
    region_vel <- gene.region.velocity.estimates(cell_e_gexp_sper_pb, cell_i_gexp_sper_pb, theta.s = T, 
                                                 RNA_mat = cell_RNA_gexp_sper_pb,
                                                 fit.quantile = 0.05,
                                                 kCells = 10, n.cores = 8)
    dim(region_vel$projected)
    region_vel_EM <- gene.EM.velocity.estimates(region_vel,n.cores = 8)
    dim(region_vel_EM$projected)
