# 3VJK docking

This is mostly repetition of the tutorial provided at

> https://ringo.ams.stonybrook.edu/index.php/2020_DOCK_tutorial_1_with_PDBID_3VJK

## Prep work

1) Navigate to the DOCK folder

`cd /Volumes/JP_External/DOCK/dock6`

2) Create an appropriate folder

`mkdir 3VJK`

3) Create sub-folders within 3VJK

`cd 3VJK`

 `mkdir 001.structure 002.surface_spheres 003.gridbox 004.dock 005.virtual_screen 006.virtual_screen_mpi 007.cartesianmin 008.rescore`
 
4) Download your PDB file from

> https://www.rcsb.org/structure/3vjk

## Receptor preparation

### Chimeras: Open 3VJK.pdb that you downloaded

     Select -> Chain -> B 
     
     Actions -> Atoms/ Bonds -> Delete
     
     Select -> Residue -> All nonstandard
     
     Actions -> Atoms/ Bonds -> Delete
     
     File -> Save Mol2 -> "3VJK_rec_woH.mol2"

### Adding hydrogens and charges

     Structure Editing -> Add H -> Ok
     
     Structure Editing -> Add Charge -> (AM1BCC charges should be selected) -> Ok
     
     Save this as a mol2 file "3VJK_rec_dockprep.mol2" and move it to the directory "001.structure"

## Ligand preparation

     Open the receptor pdb file

     Select->residue->M-51
     
     Select->invert
      
     Actions->Atoms/Bonds->Delete 
     
     File->save as mol2 ->3VJK_ligand_noH.mol2

### Adding hydrogens and charges

     Tools->Structure editing-> add H
     
     Tools->Structure editing-> Add Charge 
     
## Surface Generation & Sphere Selection

### Sphere generation

In Chimera open "3VJK_rec_woH.mol2"

     Actions -> Surface -> Show
     
     Tools -> Structure Editing -> Write DMS -> "3VJK_rec_surface.dms"
     
Move this to the directory "002.surface_spheres"


### Sphere selection

We need to create INSPH file in the bin 
