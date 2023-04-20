# 7/22/22 Notes

- All classes in ROOT start with capital T

- `MyClass`:

  - is made by ROOT automatically and is a class
  - members of the class are labeled by MyClass
  - defined in .h file

- `Loop()` :

  - is a function

- `.h` Header File:

  - <b>Only change read file and NOTHING else </b>
  - the variable names are extracted and shown in the file
    - e.g.:
      - `double_t eventnumber;`
    - Need Pierre-Simon's definitions
  - `class MyClass {public: ...}` :
    - Public means we have access
    - if Private then others would not be able to access and change variables

- `vector` (cpp):

  - type of array
  - c-array is a pointer to memory
  - vector has more protection
  - superior to just c-array

- `Bool `:
  - C variable type
- `Bool_t` :
  - ROOT makes up its own variable types
- `branches`:

  - pointers/ROOT thing
  - makes each variable to be a branch

- 459 `MyClass:: MyClass(TTree *tree) : fchain(0)`
  - constructor
    - class::function(constructor)
- TFile: class
  - ROOTfile objects
  - `f = new TFile`(constructor of file class)
    - makes a new file object and we pass the root file we know
    - to use a different data file - change the new file
    - we can learn to chain together the data files
    - tells ROOT where to find the file
    - `f` is now a pointer
    - `f->` :
      - execute function GetOBj which is a member of TFile
    - `TFile`: is an obj with methods

-` MyClass::~MyClass()` - destructor - call when the program is done - clean up code - if borrowed memory then return the memory - without cleaner the memory will overload and crash

- 483 `if(!fChain) return 0;` :

  - code will get one entry out of chain

- 499 `void MyClass::Init(TTree *tree){...}` :

  - init method
  - from: 471 `init(Tree);`
  - a lot of pointers to functions
  - takes every item in the ROOt file and creating a pointer the corresponds to the variable names
  - e.g.: `double_t dz;`
    - `"dz", &dz(&= address), &b_event_dz);`
    - therefor all this links the data info to the file address locations

- `.C` file:
  - `loop()` method for the class created by robjon
  - 65 `Long64_t nentries = fChain -> GetEntriesFast();` :
    - allocated from the heap - not compiler
    - gets all the entries and fills them into the memory for access
- define histograms `69-78` - `TH1F` : 1D histogram - `TH2F` : 2D histogram - `new` - makes new instance (call constructor) - pass the info: - (`"label", "title", bin#, starting point, last point`) - `hNhits` is a pointer to the thing created (created by robjon)
  - `FILL` is a method of histogram class:
    - `hNhits -> FILL(Nhits)`
      - `p0PR` - momenta pattern recognition
  - for loop:
    - loops over all entries
- `Draw()`
  - with no parameters
    - fake scatter
    - given a bin in 2d Hgram
    - root will draw in the bin(150 points around the square)
      - if the bins are too large then this will be bad
      - make the bins small
      - 60 by 60 or 200 by 200
  - Can also use a lego version of scatter
  - usually tho fake scatter is fine (or color)
  - True scatter will: require saving in memory all the xy points
    - the more events the more memory
    - root cheats to be aware of "fake scatter"

# Want to do

- have lots of data files to loop through
- high stats

- process:
  - run the program on each file
  - out put the ROOT field
  - running the data from TX is a bpd file defined by Paul - are txt files
  - Cpp program reads in the files and extract out then patter reg. to find the energies, and creates an n-tuple
  - copy the files from storage in cloud
  - then make the root files
  - then chain
  - then run over huge number of events
  - to get better statistics
  - tolerance:
    - log book about it
  - the given ones were selected for TOF and calibration

# TOF Dependance

- TOF depend on xy position lin4 94
- the distance from the photomultiplier tube
- also depends on energy
  - T1-T4
  - calibrate that out as well
- this becomes a multidimensional problem
- look at small regions in xy to see if there is a dependence e
- then energy
- but requires many points
- 2D are used for correlations ! find them !
- Define fill draw.
