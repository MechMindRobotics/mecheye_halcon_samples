# HALCON Samples

This documentation provides descriptions of the HALCON samples for Mech-Eye 3D Laser Profiler.

## Prerequisites for Controlling Laser Profiler with HALCON

1. [HALCON](https://www.mvtec.com/downloads) 20.11 or above has been installed on the computer.
2. [Mech-Eye SDK 2.2.0](https://downloads.mech-mind.com/?tab=tab-sdk) or above has been installed on the computer.
3. Laser profiler firmware version is consistent with Mech-Eye SDK version. If not, use Mech-Eye Viewer or the [firmware upgrade tool](https://docs.mech-mind.net/en/eye-3d-profiler/latest/api/api-camera-firmware-update.html) to upgrade the firmware.
4. The IP addresses of the laser profiler and the computer Ethernet port connected to the laser profiler are in the same subnet. Use Mech-Eye Viewer or the [IP configuration tool](https://docs.mech-mind.net/en/eye-3d-profiler/latest/api/api-ip-configuration.html) to set the laser profiler IP address.

## Connect to Laser Profiler

This section describes the method for connecting to a specific laser profiler. This method is used in all samples.

1. Open the sample in HDevelop.
2. Obtain all the available laser profilers by running the `info_framegrabber` operator (press the F6 key).
3. Select a laser profiler to connect:

    (1) In the **Control Variables** area, double-click **MechEyeProfilers** to display a list of all the available laser profilers.
    (2) In the list, double-click the laser profiler to which you want to connect, and copy the laser profiler name after **unique_name:** or **user_name:**.

    > Note: The laser profiler name after **user_name:** is the custom laser profiler name set in Mech-Eye Viewer. For instructions, please refer to the [user manual](https://docs.mech-mind.net/en/eye-3d-profiler/latest/viewer/connect-to-camera-and-set-ip.html#set-camera-name).

    (3) In the **Program Window**, locate the following line, and replace `LNX` with the copied laser profiler name.

    ```halcon
    DeviceInfo := 'LNX'
    ```

4. Run the sample by pressing the F5 key. The selected laser profiler will be connected.

> Note:
>
> * After executing the entire sample, please press the F2 key to reset program execution. Otherwise, the laser profiler cannot be connected by Mech-Eye Viewer.

## Description of Samples

* [perform_continuous_data_acquisition_externally_triggered](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/area_scan_3d_camera/perform_continuous_data_acquisition_externally_triggered.hdev):  
  Perform rounds of data acquisition continously and obtain the profile data (including intensity and depth data). Each round of data acquisition is triggered by the externally input signals, and the scanning of each line is triggered at a fixed rate.
* [perform_continuous_data_acquisition_software_triggered](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/area_scan_3d_camera/perform_continuous_data_acquisition_externally_triggered.hdev):  
  Perform rounds of data acquisition continously and obtain the profile data (including intensity and depth data). Each round of data acquisition is triggered by the software, and the scanning of each line is triggered at a fixed rate.
* [perform_single_round_of_data_acquisition_externally_triggered](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/area_scan_3d_camera/perform_continuous_data_acquisition_externally_triggered.hdev):  
  Perform one round of data acquisition, and obtain the profile data (including intensity and depth data). The data acquisition is triggered by the externally input signals, and the scanning of each line is triggered at a fixed rate.
* [perform_single_round_of_data_acquisition_software_triggered](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/area_scan_3d_camera/perform_continuous_data_acquisition_externally_triggered.hdev):  
  Perform one round of data acquisition, and obtain the profile data (including intensity and depth data). The data acquisition is triggered by the software, and the scanning of each line is triggered at a fixed rate.
