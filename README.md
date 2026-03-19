# su2assignment5
Implementation:
Speed of sound was added as new output by modifying 2 files in the source code: CFlowCompOutput.cpp and CFlowOutput.cpp
1. "SOUND_SPEED" was added to requestedScreenFields in the constructor so that it appears in the terminal by default
2. AddHistoryOutput("SOUND_SPEED", ...) was added in SetHistoryOutputFields(), registering it under the group "MAX_VALS" with HistoryFieldType::DEFAULT. The history value tracks the domain maximum speed of sound per iteration.
3. In LoadHistoryData(), a loop over all mesh points computes GetSoundSpeed(iPoint) and tracks the maximum value, which is then passed to SetHistoryOutputValue("SOUND_SPEED", max_sound_speed)
4. AddVolumeOutput("SOUND_SPEED", "Sound_Speed", "PRIMITIVE", ...) was added in SetVolumeOutputFields() inside the if (config->GetViscous()) block, and SetVolumeOutputValue("SOUND_SPEED", iPoint, Node_Flow->GetSoundSpeed(iPoint)) was added in LoadVolumeData() after the Mach number line.
5. In CFlowOutput.cpp, the same AddVolumeOutput and SetVolumeOutputValue calls were added as a fallback for the base class output path.
6. there were some issues with mpi so I had to disable mpi and build
7. I have used the same .cfg and .su2 files from assignment 2 so the results are not physically accurate, I took this exercise as source code editing experience solely
