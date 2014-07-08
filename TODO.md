TODO for Vicalib
================

- [ ] Usage message
- [ ] Example argument lists
- [ ] null pointer checks
- [ ] Split files for shorter builds
- [ ] Ceres/miniglog/glog conflicts
- [ ] Calibration without IMU (see below)


Calibration without IMU
-----------------------
Variable is_inertial_active_ is true even if -nocalibrate_imu parameter is given. 
Checking variable FLAGS_calibrate_imu was added as a patch.
There are other errors that I suspect have to do with the IMU: Vicalib crashes when calibrating the RGB camera only of an Asus camera.

File: vicalibrator.h. Line: 862: problem_->SetParameterBlockVariable(biases_.data());
(biases_ is a vector containing [0 0 0 0 0 0])
Error: 
F/problem_impl.cc:65 Check failed: it != parameter_map.end() Parameter block not found: 0x7fc26981c670
Abort trap: 6

Invocation:
./vicalib -cam convert:[fmt=MONO8]//openni:[rgb=1,depth=0,ir=0]// -nocalibrate_imu -use_only_when_static -exit_vicalib_on_finish -grid_preset=1 -models="fov" -num_vicalib_frames=1000
