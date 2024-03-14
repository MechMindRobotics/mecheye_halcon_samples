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

* [trigger_with_software_and_fixed_rate](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/profiler/trigger_with_software_and_fixed_rate.hdev):  
  Trigger one round of data acquisition with the signals input from software, trigger line scans at a fixed rate, and then retrieve the acquired data.
* [trigger_with_external_device_and_fixed_rate](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/profiler/trigger_with_external_device_and_fixed_rate.hdev):  
  Trigger data acquisition with signals input from the external device, trigger line scans at a fixed rate, and then retrieve the acquired data.
* [trigger_with_software_and_encoder](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/profiler/trigger_with_software_and_encoder.hdev):  
  Trigger data acquisition with signals input from software, trigger line scans with signals input from the encoder, and then retrieve the acquired data.
* [trigger_with_external_device_and_encoder](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/profiler/trigger_with_external_device_and_encoder.hdev):  
  Trigger data acquisition with signals input from the external device, trigger line scans with signals input from the encoder, and then retrieve the acquired data.
* [trigger_with_software_and_fixed_rate_continuous](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/profiler/trigger_with_software_and_fixed_rate_continuous.hdev):  
  Trigger multiple rounds of data acquisition with the signals input from software, trigger line scans at a fixed rate, and then retrieve the acquired data.
* [trigger_with_external_device_and_fixed_rate_continuous](https://github.com/MechMindRobotics/mecheye_halcon_samples/tree/master/profiler/trigger_with_external_device_and_fixed_rate_continuous.hdev):  
  Trigger multiple rounds of data acquisition with signals input from the external device, trigger line scans at a fixed rate, and then retrieve the acquired data.