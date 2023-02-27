## GEANT4 Learn Notes

Some reference
+ [ROOT Users Workshop 2013 - "ROOT - The Next Generation"](https://indico.cern.ch/event/217511/contributions/). 
+ [Geant4 Tutorial](https://indico.cern.ch/event/58317/timetable/#20100215) 
+ [XVI Seminar on Software for Nuclear, Subnuclear and Applied Physics](https://agenda.infn.it/event/17240/).  
+ [The 2nd GEANT4 school in China](https://indico.ihep.ac.cn/event/9624/).  

#### Study from the examples
The example codes are [here](https://gitlab.cern.ch/geant4/geant4/-/tree/master/examples).  
Some reference: [exampleB1解读](https://zhuanlan.zhihu.com/p/152018143).

##### ExampleB1
###### Code Structures
+ include
  + ActionInitialization.hh	
  + DetectorConstruction.hh	
  + EventAction.hh	
  + PrimaryGeneratorAction.hh
  + RunAction.hh
  + SteppingAction.hh
+ src
  + ActionInitialization.cc	
  + DetectorConstruction.cc	
  + EventAction.cc
  + PrimaryGeneratorAction.cc	
  + RunAction.cc
  + SteppingAction.cc
+ examples

The main program is `example.cc`, it uses 3
+ examples
  + G4RunManager
  + G4VisManager 
  + G4UImanager
to define the run, ...

Reference from [here](https://indico.cern.ch/event/58317/contributions/2047459/attachments/992306/1411069/ExtractingInfo.pdf)
+ Mandatory User Classes
  + G4VUserDetectorConstruction: The detector structure defination is in `DetectorConstruction.cc`, the key is physical volume and logical volume.
  + G4VUserPhysicsList
  + G4VUserActionInitialization
    + G4PrimaryGeneratorAction
    + RunAction `#include "G4Run.hh"`
    + EventAction `#include "G4Event.hh"`
    + ~~STackingAction `#include "G4Track.hh"`~~
    + ~~TrackingAction `#include "G4Track.hh"`~~
    + SteppingAction `#include "G4Step.hh"`


In the user action
|  |  |
|:--------| :---------:|
| Simulation is successively split into | Corresponding / related Objects | 
| Run consists of | G4RunManager, G4Run | 
| Event(s), consists of |  G4Event |
| Particle(s) transported in | G4Track, G4DynamicParticle |
| Steps through detector setup, | G4Step, G4StepPoint |
| depositing energy ionization), | G4Trajectory
| and creating secondaries | G4Stack |
