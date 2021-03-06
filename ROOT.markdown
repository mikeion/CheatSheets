## Macros

    // build into `.so` for interactive use
    root [0] .L ArrayOfHists.C+
    Info in <TUnixSystem::ACLiC>: creating shared library ./ArrayOfHists_C.so
    root [1] arr_of_hists()

    // quick and easy compile - use g++ or clang or whatever is appropriate
    $ g++ -o ArrayOfHists.exe ArrayOfHists.C `root-config --cflags --libs`
    $ ./ArrayOfHists.exe

## Histograms

    // Get better color palette.
    gStyle->SetPalette(1);
    
    // Command line rebin
    h1->Rebin(); // by 2
    h1->Rebin(5); // by 5
    
    // Set background color to white
    'Canvas 1'->SetFillColor(kWhite);

    // print contents to file (bin, lower edge, err)
    histo->Print("all"); > histo_out.txt

## Chains

    TChain ch("ch","ch")
    ch->Add("SIM_minerva_00000513*.root/CCInclusiveReco",0)

    TChain ch("ch","ch");
    ch->Add("02/SIM_minerva_00000002_Subruns_*.root/RecoTracks",0)
    ch->Add("04/SIM_minerva_00000004_Subruns_*.root/RecoTracks",0)
    ch.MakeClass("RecoTracks")


## Trees

    TFile *_file0 = TFile::Open("/minerva/data/users/perdue/mc_production/nogrid/minerva/ana/v9r0p2/00/00/11/00/SIM_minerva_00001100_0001_Ana_Tuple_v1_v9r0p2.root")
    TTree *mytree = _file0->Get("CCInclusiveReco")
    mytree->Draw("ev_gate","n_prim_tracks_kinked>0")

    TTree *mytree = _file0->Get("RecoTracks");
    TTree *mytree = _file0->Get("MLVFSamplePrepTool");
    TTree *mytree = _file0->Get("NukeCC")

    NukeCC->GetEntries();

    TTree *mytree = _file0->Get("NuECCQE")
    mytree->MakeClass("NuECCQE")

### Trees - Draw

    mytree->Draw("myvar","","",1)      # 1 event
    mytree->Draw("myvar","","",1,10)   # 1 event, use 10th event
    mytree->Draw("myvar","","",10,10)  # 10 events, start with 10th


### Trees - Print

    mytree->Scan("myvar[0]","","",1,1)  # print element 0 of myvar array (1 event, start at 1)


## Math

    root [3] TMath::Factorial(3)
    (Double_t)6.00000000000000000e+00
    root [6] TMath::Factorial(3)*TMath::Factorial(3)/TMath::Factorial(6)
    (double)5.00000000000000028e-02
    root [7] 36/720
    (const int)0
    root [8] double(36/720)
    (const double)0.00000000000000000e+00
    root [9] 36./720.
    (const double)5.00000000000000028e-02
    root [10] double(36)/720
    (const double)5.00000000000000028e-02


## Classes

http://www-glast.slac.stanford.edu/software/root/howto/writing_root_classes.htm


## GENIE Interactive Examples

    $ genie gntp.100.ghep.root
    genie[2] TTree *mytree = 0;
    genie[3] _file0->GetObject("gtree", mytree);
    genie[4] Long64_t nEntries = mytree->GetEntries();
    genie[5] cout << nEntries << endl;
    1000
    genie[6] genie::NtpMCEventRecord* myentry = new genie::NtpMCEventRecord();
    // ... (this will produce the welcome message)
    genie[7] mytree->SetBranchAddress("gmcrec", &myentry);
    genie[8] mytree->GetEntry(0);
    genie[9] myentry->PrintToStream(cout);
    // ... (a lot of stuff)
    genie[10] myentry->event->XSec()
    (const double)1.48164559715832651e-10

    genie [1] TChain ch("gtree")
    genie [2] ch->Add("/pnfs/minerva/scratch/users/minervapro/mc_production_genie_DFR_v10r8p4/grid/central_value/minerva/genie/v10r8p4/00/01/00/11/SIM_minerva_00010011_*_ghep.root/gtree",0)
    genie [3] Long64_t nEntries = ch->GetEntries();
    genie [4] cout << nEntries << endl;
    100000
    genie [5] genie::NtpMCEventRecord* myentry = new genie::NtpMCEventRecord();
    // ...
    genie [6] ch->SetBranchAddress("gmcrec", &myentry);
    genie [7] ch->GetEntry(0);
    genie [8] myentry->PrintToStream(cout);
    // ...
    genie [9] ch->GetEntry(2000);
    genie [10] myentry->PrintToStream(cout);
    // ...
    genie [11] myentry->event->XSec()
    (const double)3.35586289456737729e-12
    genie [12] myentry->event.Summary()->ProcInfo()->IsMEC()
    (const bool)1
    genie [13] myentry->event.Summary()->ProcInfo()->ScatteringTypeId()
    (const genie::ScatteringType_t)10
    genie [14] myentry->event.Summary()->ProcInfo()->InteractionTypeAsString()
    (class TString)"Weak[CC]"
    genie [15] myentry->event.Summary()->ProcInfo()->ScatteringTypeAsString()
    (class TString)"MEC"
