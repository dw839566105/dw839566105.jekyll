### geometry

##### [Describe your detector](https://indico.cern.ch/event/58317/contributions/2047444/attachments/992295/1411052/D1b-placements.pdf)  
+ Derive your own concrete class from `G4VUserDetectorConstruction` abstract base class.  
+ Implementing the method `Construct()`:  
  – Modularize it according to each detector component or sub-detector:  
    + Construct all necessary materials  
    + Define shapes/solids required to describe the geometry  
    + Construct and place volumes of your detector geometry  
    - *Define sensitive detectors and identify detector volumes which to associate them*  
    - *Associate magnetic field to detector regions*  
    - *Define visualization attributes for the detector elements*  


##### Three conceptual layers
  + G4VSolid -- shape, size  
  + G4LogicalVolume -- daughter physical volumes, material, sensitivity, user limits, etc.  
  + G4VPhysicalVolume -- position, rotation

Code in exampleB1, the `World volume` is:
```
  G4double world_sizeXY = 1.2*env_sizeXY;
  G4double world_sizeZ  = 1.2*env_sizeZ;
  G4Material* world_mat = nist->FindOrBuildMaterial("G4_AIR");

  G4Box* solidWorld =
    new G4Box("World",                       //its name
       0.5*world_sizeXY, 0.5*world_sizeXY, 0.5*world_sizeZ);     //its size

  G4LogicalVolume* logicWorld =
    new G4LogicalVolume(solidWorld,          //its solid
                        world_mat,           //its material
                        "World");            //its name

  G4VPhysicalVolume* physWorld =
    new G4PVPlacement(0,                     //no rotation
                      G4ThreeVector(),       //at (0,0,0)
                      logicWorld,            //its logical volume
                      "World",               //its name
                      0,                     //its mother  volume
                      false,                 //no boolean operation
                      0,                     //copy number
                      checkOverlaps);        //overlaps checking
```
The `World volume` is a unique physical volume which represents the experimental area. It must exist
and fully contains all other components. The `Construct()` function need to return it(`physWorld`) finnaly.

#### Solid
`G4VSolid` is an abstract class. All solids in Geant4 derive from it.
- Defines but does not implement all functions required to:
  + compute distances to/from the shape
  + check whether a point is inside the shape
  + compute the extent of the shape
  + compute the surface normal to the shape at a given point
  + Once constructed, each solid is automatically registered in aspecific solid store

Different geometries are detailed illustrated in the Userguide.
For `Union`, `Subtraction` and `Intersection`


Surface area and geometrical volume of a generic solid or Boolean composition can be computed from the solid:
```
G4double GetSurfaceArea();
G4double GetCubicVolume();
```
Overall mass of a geometry setup (sub-detector) can be computed from the logical volume:

`G4double GetMass(G4Bool forced=false, G4Material* parameterisedMaterial=0);`

#### Logical Volume
```
G4LogicalVolume(G4VSolid* pSolid, G4Material* pMaterial,
  const G4String& name, G4FieldManager* pFieldMgr=0,
  G4VSensitiveDetector* pSDetector=0,
  G4UserLimits* pULimits=0,
  G4bool optimise=true);
```
+ Contains all information of volume **except** position:
  + Shape and dimension (G4VSolid)
  + Material, sensitivity, visualization attributes
  + Position of daughter volumes
  + Magnetic field, User limits
  + Shower parameterisation
+ Physical volumes of same type can share a logical volume
+ The pointers to solid and material must be **NOT** null
+ Once created it is automatically entered in the LV store
+ It is not meant to act as a base class

One or more volumes can be placed in a mother volume. `World volume` is the root volume of the hierarchy. One logical volume can be placed more than once.  
If the mother volume is placed more than once, all daughters by definition appear in each placed physical volume.  
The world volume must be a unique physical volume which fully contains with `some margin` all the other volumes.  

#### Physical Volume

- `G4PVPlacement` 1 Placement = One Volume
- `G4PVParameterised` 1 Parameterised = Many Volumes
  - Parameterised by the copy number
  - Parameterisation can be used only for volumes that either a) have no further daughters or b) are identical in size & shape.
- `G4PVReplica` 1 Replica = Many Volumes
  - Slicing a volume into smaller pieces (if it has a symmetry)

```
G4PVPlacement(G4RotationMatrix* pRot, // rotation of mother frame
  const G4ThreeVector& tlate, // position in rotated frame
  G4LogicalVolume* pCurrentLogical,
  const G4String& pName,
  G4LogicalVolume* pMotherLogical,
  G4bool pMany, // not used. Set it to false…
  G4int pCopyNo, // unique arbitrary index
  G4bool pSurfChk=false); // optional overlap check
```
Single volume positioned relatively to the `mother volume`.  
![Rotation](test.png)

