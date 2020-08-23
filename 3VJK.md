# 3VJK docking

This is mostly repetition of the tutorial provided at

> https://ringo.ams.stonybrook.edu/index.php/2020_DOCK_tutorial_1_with_PDBID_3VJK

## Step 1: Prep work

1) Navigate to the DOCK folder

`cd /Volumes/JP_External/DOCK/dock6`

2) Create an appropriate folder

`mkdir 3VJK`

3) Create sub-folders within 3VJK

`cd 3VJK`

`mkdir 001.structure 002.surface_spheres 003.gridbox 004.dock 005.virtual_screen 006.virtual_screen_mpi 007.cartesianmin 008.rescore`
 
4) Download your PDB file from

> https://www.rcsb.org/structure/3vjk

## Step 2: Receptor preparation

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

## Step 3: Ligand preparation

     Open the receptor pdb file

     Select->residue->M-51
     
     Select->invert
      
     Actions->Atoms/Bonds->Delete 
     
     File->save as mol2 ->3VJK_ligand_noH.mol2

### Adding hydrogens and charges

     Tools->Structure editing-> add H
     
     Tools->Structure editing-> Add Charge 
     
## Step 4: Surface Generation & Sphere Selection

### Sphere generation

In Chimera open "3VJK_rec_woH.mol2"

     Actions -> Surface -> Show
     
     Tools -> Structure Editing -> Write DMS -> "3VJK_rec_surface.dms"
     
Move this to the directory "002.surface_spheres"


### Sphere selection

We need to create INSPH file in the bin directory by:

`vi INSPH`

Then, in the INSPH file, write the following script:

This script allows you to create an output file that contains "sphere information" in the receptor. The spheres are basically representations of empty space inside the protein. You want to make sure that these spheres overlap with each other but not with the receptor.

      3VJK_rec_surface.dms
      R 
      X 
      0.0 
      4.0 
      1.4 
      3VJK_receptor_woH.sph

Note, to save and exit the vim command, hit ESC and type :wq

Before running the sphgen, move 3VJK_rec_surface.dms to the bin directory

Then, run:

`./sphgen -i INSPH -o OUTSPH`

You should find 3VJK_receptor_woH.sph in the bin directory

Now, to find a subset of these spheres that overlap closely with the ligand (within 10 angstroms), we will run a sphere_selector script:

`./sphere_selector 3VJK_receptor_woH.sph ../3VJK/001.structure/3VJK_ligand_with_H.mol2 10.0`

Since the ligand.mol2 file is in the 001.structure directory, we needed to specify the directory

## Step 5: Generation of a box and grid

### Box generation

First, go to 003.gridbox and make an input file that contains parameters for the box

`vi showbox.in`

Then, write the following script lines:

    Y    #generate box#
    8.0    #how many angstroms the box edges should be from the spheres#
    ./../002.surface_spheres/select_spheres.sph     #the location of the selected spheres#
    1 
    3VJK.box.pdb     #name of the output file#

Then, navigate to the bin directory and run:

`./show box`

In the bin folder, 3VJK.box.pdb should be generated

### Grid generation
